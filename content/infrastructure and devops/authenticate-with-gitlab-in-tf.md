---
title: 'Authenticate With Gitlab in Tf'
date: 2023-02-17T08:23:58+05:30
draft: false
---

# How to authenticate with gitlab for fetching module

To authenticate with GitLab in Terraform and fetch a module from a GitLab repository, you can use a personal access token. Here are the general steps:

1. Generate a personal access token: In GitLab, go to your user settings and generate a personal access token with the "api" scope. Take note of the token value, as you won't be able to see it again.
2. Set the GitLab access token as an environment variable: In the shell or environment where you will run Terraform, set the **`TF_CLI_CONFIG_FILE`** environment variable to point to a file where you will store the Terraform configuration. Then add the GitLab access token as a variable to the **`credentials`** section of this file. For example, if you are using the Bash shell:

```
bashCopy code
export TF_CLI_CONFIG_FILE="$HOME/.terraformrc"
echo 'credentials "gitlab.com" {
  token = "<your-personal-access-token>"
}' >> "$TF_CLI_CONFIG_FILE"

```

This will create a **`~/.terraformrc`** file with the GitLab personal access token.

1. Use the GitLab repository as a module source: In your Terraform configuration, you can use the GitLab repository as a module source. For example, to fetch the **`example`** module from the **`my-group/my-project`** GitLab repository:

```
javascriptCopy code
module "example" {
  source = "git::https://gitlab.com/my-group/my-project.git//example?ref=v1.2.3"
}

```

This will fetch the **`example`** module from the **`my-group/my-project`** repository, using the GitLab personal access token from the **`~/.terraformrc`** file.

Note that the **`//example`** in the **`source`** URL refers to the module subdirectory within the repository. If the module is at the root of the repository, you can omit this. The **`?ref=v1.2.3`** specifies the version of the module to fetch. You can replace this with a branch, tag, or commit hash.
