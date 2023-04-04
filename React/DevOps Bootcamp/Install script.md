# azure_env_setup

This script is intended to setup the environment in a Mac with all the required tools for our Dev Ops bootcamp. For Windows installation you can use this [repo](https://github.com/amiguel215/dev_tools_installer)

# Instructions:

1. Clone or the repo or download the `azure_env_setup.sh` file.
2. Run the script directly in finder or from terminal `./psInitial.sh`.
3. If the script fails, you probably need to change the permissions of the file, you can run `chmod +x psInitial.sh` to change its permissions.
4. Azure PowerShell tools must be manually installed, open PS and run the following command:
```powershell
Install-Module -Name Az -Scope CurrentUser -Repository PSGallery -Force
```


# Installed tools:

- [Homebrew](https://brew.sh/) package manager for Mac.
- [Powershell Core](https://github.com/Powershell/Powershel) 
- [Git](https://git-scm.com/)
- VS Code.
- [Bicep](https://learn.microsoft.com/en-us/azure/azure-resource-manager/bicep/)