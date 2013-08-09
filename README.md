# man page for deb-publish-simple
## NAME 
**deb-publish-simple** is a simplified workflow to publish one or more programs to one or more distribution/releases on one publication server.

## SYNOPSIS
**deb-publish-simple** [objectPath] [ objectId1 ... objectIdN ] -action [ actionArg1 .. actionArgM]

## DESCRIPTION 
### distrib.release
Use this object path to manage distrib/releases. Example: ubuntu raring. You can add/remove a distro/release from the default distrib/releases to which you publish your programs. 

### distrib-releases
Use this object path to view or all manage all distrib/releases.

### file
There are two default files containing default configuration fields: **defaults** and **domain**. Use this object path to view or manage these default files.

### file.field
You can add any default field of your own choosing to the **defaults** and **domain** files. The following are standard and mandatory  
**defaults:** email_signature, name_signature  
**domain:**name, root_pwd, user_name, user_pwd  
You can add any field that you would like to add by default to the _build.conf_ file in the **defaults** file.

### folder
A scriptbox program is contained in a folder. Use this object path to carry out operations on scriptbox program folders.

### server
Use this object path to perform operations on the publication server.

### simul-server
Use this object path to install or unstall a simulation publication server locally.


## OPTIONS

### --help
shows the general help paragraph.

### [objectpath] --help
shows general help for the object path.

### --version
shows the program's version.

### --license
shows the program's license.

### distrib.release.arg [obj] -show-direct-install
This command shows the direct installation instructions for the distrib/release specified. Example:  
**deb-publish-simple** distrib.release ubuntu raring -show-direct-install

### distrib.release.arg [obj] -remove-default
This command removes a default distrib/release for which to publish the scriptbox programs for. Example:  
**deb-publish-simple** distrib.release ubuntu raring -remove-default

### distrib.release.arg [obj] -show-deb-client-install
This command shows the **deb-client** installation instructions for the distrib/release specified. Example:  
**deb-publish-simple** distrib.release ubuntu raring -show-deb-client-install

### distrib.release.arg [obj] -add-default
This command adds a default distrib/release for which to publish the programs. Example:  
**deb-publish-simple** distrib.release ubuntu raring -add-default

### distrib-releases -show
This command shows the default distrib/releases to which to publish programs. Example:  
**deb-publish-simple** distrib-releases -show

### file [obj] -show
This command shows all the default values for **defaults** or **domain**. Example:  
**deb-publish-simple** file defaults -show  
**deb-publish-simple** file domain -show

### file.field.arg [obj] -remove
This command removes the value for a default configuration parameter. There are two sets of default configuration parameters: **defaults** and **domain**. Example:  
**deb-publish-simple** file.field defaults author_name -remove

### file.field.arg [obj] -show
This command outputs the value for a default configuration parameter. There are two sets of default configuration parameters: **defaults** and **domain**. Example:  
**deb-publish-simple** file.field defaults author_name -show  
John Doe


### file.field.arg [obj] -set [arg]
This command sets the value for a default configuration parameter. There are two sets of default configuration parameters: **defaults** and **domain**. Example:  
**deb-publish-simple** file.field defaults author_name -set "John Doe"

### folder [obj] -apply-defaults
This command applies the **defaults** to a particular scriptbox folder. Example:  
**deb-publish-simple** myprogram -apply-defaults

### folder [obj] -unpublish
This command unpublishes a scriptbox folder from all the default distributions. It requires to have entered the following configurations:  
**domain:name, user_name**  
**deb-publish-simple** folder myprogram -unpublish

### folder [obj] -publish
This command publishes a scriptbox folder to all the default distributions. It requires to have entered the following configurations:  
**defaults:email_signature, name_signature**  
**domain:name, user_name, user_pwd**  
Example:  
**deb-publish-simple** folder myprogram -publish

### server -uninstall
This command uninstalls the server on the domain from which to publish the programs. 
It requires to have entered the following configurations:  
**domain:** name, root_pwd  
Example:  
**deb-publish-simple** server -uninstall  
This command will uninstall all server components on server _packages.myserver.org_

### server -install
This command installs the server on the domain from which to publish the programs. It requires to have entered the following configurations:  
**defaults:email_signature, name_signature**  
**domain:name, root_pwd, user_name, user_pwd**  
Example:  
**deb-publish-simple** file.field domain name -set packages.myserver.org  
**deb-publish-simple** server -install  
This command will install all server components required on server _packages.myserver.org_

### simul-server -install
This command installs the simulation server locally on your own machine. It requires to have entered the following configurations:  
**domain:name**  
sudo **deb-publish-simple** simul-server -install 

### simul-server -uninstall
This command uninstalls the simulation server locally. It requires to have entered the following configurations:  
**domain:name**  
sudo **deb-publish-simple** simul-server -uninstall 

## ENVIRONMENT 
### CONF_FOLDER
By default, **deb-publish-simple** will look for its configuration files in the ~/.deb-publish-simple folder. You can override this with the **CONF_FOLDER** environment variable. Example:  
CONF_FOLDER=/home/john/deb-conf-alternative **deb-publish-simple** ...  
Setting the variable just before invoking **deb-publish-simple** will point the CONF_FOLDER elsewhere.

## EXIT-STATUS 
### 0
A zero exit code means that everything went ok.
### 1
A one exit code is usually an error generated by **deb-publish-simple** itself.
### other
Another exit code is always an error generated by one of the underlying programs invoked by **deb-publish-simple**.

## FILES 
###  ~/.deb-publish-simple
This folder contains the configuration files for **deb-publish-simple**.

###  ~/.deb-publish-simple/defaults.conf
This file can contain any field that you would like to copy automatically with **apply-defaults** to your program folder.**
_Mandatory fields:_  
**email_signature**: Default signatory email.  
**name_signature**: Default signatory name.  
  
_Optional fields:_  
**author_name**: Default author name.  
**author_email**: Default author email.  
**report_bugs**: Default person to report bugs to.  
**license**: Default license.  
**home_page**: Default home page.  
**urgency**: Default debian urgency level.  
**deb_section**: Default debian section.  
**deb_priority**: Default debian priority.  
**man_section**: Default man page section priority; which is by convention a number.  
  
_Unlikely fields:_  
**deb_other_build_dependencies**: Default comma-separated list of other build dependencies.  
**deb_dependencies**: Default comma-separated list of dependencies.  
**deb_replaces**: Default list of packages to replace.  

###  ~/.deb-publish-simple/domain.conf
_Mandatory fields:_  
**name:** Default domain name.  
**root_pwd:** Root password for the repository server publishing the domain.  
**user_name:** User account in which to manage the domain on the repository server.  
**user_pwd:** Password for the user account in which to manage the domain on the repository server.  

###  ~/.deb-publish-simple/distrib-releases.conf
This file contains one line per distrib/release to which to publish by default. Example:  
ubuntu precise  
ubuntu raring  

## AUTHOR
Erik Poupaert <erik@sankuru.biz>

## REPORTING-BUGS
Report bugs to: erik@sankuru.biz

# COPYRIGHT
Licensed under: GPL
