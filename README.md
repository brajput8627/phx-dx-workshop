# PHXDUG DX Development Workshop
The goals of this project are to:
* Setup a development environment for Salesforce DX
* Convert an existing MDAPI project into a DX Project
* Modularize a DX Project into multiple DX Projects

## Phase One - Env Setup

Download and install the following components:
* [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
* [Salesforce DX CLI](https://developer.salesforce.com/tools/sfdxcli)
* [VS Code](https://code.visualstudio.com/)
* [Salesforce Extension Pack](https://marketplace.visualstudio.com/items?itemName=salesforce.salesforcedx-vscode)

Signup for the following accounts, or use existing Accounts if you have them already:
* [Salesforce Developer Edition](https://developer.salesforce.com/signup)
* [GitHub.com Account](https://github.com/join)

### Step 1 - Enable Dev Hub
* Enable Dev Hub in your Developer Org
    * https://developer.salesforce.com/docs/atlas.en-us.sfdx_setup.meta/sfdx_setup/sfdx_setup_enable_devhub.htm

### Step 2 - Authorize your Dev Hub
* Link your Dev Hub to your development environment
    * `sfdx force:auth:web:login --setdefaultdevhubusername --setalias=devhub`

### Step 3 - Convert and Create a DX Project
* Create a DX Project 
    * `sfdx force:project:create --projectname dx-workshop --defaultpackagedir app`
* Convert the `mdapi` project by running the following from the `dx-workshop` directory
    * `sfdx force:mdapi:convert -r ../mdapi`

### Step 4 - Create a Scratch Org and Push your DX Project
* Copy the following content into the `config/project-scratch-def.json` file
```
{
  "orgName": "dx-workshop",
  "edition": "Developer",
  "features": [
    "API",
    "AuthorApex",
    "ForceComPlatform"
  ],
  "settings": {
    "orgPreferenceSettings": {
      "s1DesktopEnabled": true
    }
  }
}

```

* Create a Scratch Org by running the following from the `dx-workshop` directory
    * `sfdx force:org:create --definitionfile config/project-scratch-def.json --setdefaultusername --setalias=dx-workshop`

* Push the sources to the scratch org by running the following from the `dx-workshop` directory
    * `sfdx force:source:push`