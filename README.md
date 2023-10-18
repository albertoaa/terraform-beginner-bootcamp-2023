# Terraform Beginner Bootcamp 2023
This project is going to utilize semantic versioning for it's tagging.
[semver.org](https://semver.org/)

The general format would be as follows.
Given a version number **MAJOR.MINOR.PATCH**, increment the:

- **MAJOR** ex: `1.0.1`
- **MINOR** version when you add functionality in a backward compatible manner
- **PATCH** version when you make backward compatible bug fixes

Additional labels for pre-release and build metadata are available as extensions to the MAJOR.MINOR.PATCH format.

## Install Terraform CLI

### Considerations about Linux distribution and OS
This project is built using Ubuntu 22.04 image. You can check which Linux distribution are you using by checking this [link](https://www.ionos.com/digitalguide/server/know-how/how-to-check-your-linux-version/#:~:text=The%20command%20%E2%80%9Cuname%20%2Dr%E2%80%9D,the%20Linux%20kernel%20is%205.4.) and adjust the installation steps according to your specific distribution.

You can try the following command on your terminal to check Linux distribution:
```
cat /etc/os-release 

PRETTY_NAME="Ubuntu 22.04.3 LTS"
NAME="Ubuntu"
VERSION_ID="22.04"
VERSION="22.04.3 LTS (Jammy Jellyfish)"
VERSION_CODENAME=jammy
ID=ubuntu
ID_LIKE=debian
HOME_URL="https://www.ubuntu.com/"
SUPPORT_URL="https://help.ubuntu.com/"
BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"
UBUNTU_CODENAME=jammy
```

### Considerations with the Terraform CLI Changes
The Terraform CLI installation instructions have changed due to gpg keyring changes. The latest instructions for installing Terraform CLI are included using the latest [Terraform Installation Guide](https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli) and the [gitpod.yml](.gitpod.yml) file was modified to include a new script with these steps.

### Refactoring into Bash scripts
As mentioned above a bash script [./bin/install_terraform_cli](./bin/install_terraform_cli) was created to abstract the installation steps from [gitpod.yml](.gitpod.yml) and just execute it from there.

- Keep the Gitpod Task file([.gitpod.yml](.gitpod.yml)) tidy.
- Easier debug and manually execution of Terraform CLI installation.
- Make Terraform CLI installation reusable for other projects.

### Shebang Considerations
A Shebang(pronounced Sha-bang) tells the bash script what program will interpret the script in order to execute it properly. You read more about it here: [Shebang Wikipedia Page](https://en.wikipedia.org/wiki/Shebang_(Unix)). eg. `#!/bin/bash`.

ChatGPT recommended we use this format for more portability `#!/usr/bin/env bash` so it was included on the Terraform CLI installation script([./bin/install_terraform_cli](./bin/install_terraform_cli)).

### Execution Considerations
When executing this script we can use the shorthand notation `./`.

eg. `./bin/install_terraform_cli`

If we are using a script in [gitpod.yml](.gitpod.yml) file we need to point to a program to interpret it.

eg. `source ./bin/install_terraform_cli`

### Linux File Permissions Considerations
You can use [chmod](https://en.wikipedia.org/wiki/Chmod) to add permissions to particular files in your filesystem. In this project we needed to add execution permissions to the Terraform CLI installation script([./bin/install_terraform_cli](./bin/install_terraform_cli)) by issuing the command `chmod u+x ./bin/install_terraform_cli`

### Gitpod Tasks Lifecycle(Before, Init, Command)
We need to be carefull when using init since it won't re-run a task when restarting an existing workspace.
https://www.gitpod.io/docs/configure/workspaces/tasks#prebuild-and-new-workspaces


## Install AWS CLI
AWS CLI it's installed on the project via the script [./bin/install_aws_cli](./bin/install_aws_cli).

[Getting Started with AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)

[AWS CLI Env Vars](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-envvars.html)

### AWS Credentials
We can always check if credentials are set correctly by issuing the following AWS CLI command: `aws sts get-caller-identity`

If everything is setup correctly you should see a JSON response similar to this:

```json
{
    "UserId": "BIDAX3JPUs33ZO3PN0PJW",
    "Account": "123456789012",
    "Arn": "arn:aws:iam::123456789012:user/terraform_beginner_bootcamp"
}
```