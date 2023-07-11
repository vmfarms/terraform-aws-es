# Pre Commit Hooks

We use `pre-commit` to validate the code before commiting to the repository. This will help us to keep the code clean and safe. To install `pre-commit` please follow the [instructions](https://pre-commit.com/#install).

## Checks

Make sure you familiarize yourself with the [pre-commit](https://pre-commit.com/) framework and the following hooks. Make sure you have installed all of them on your local machine:

### Built-in hooks

 - [check-json](https://github.com/pre-commit/pre-commit-hooks#check-json): Check that JSON files are valid
 - [check-merge-conflict](https://github.com/pre-commit/pre-commit-hooks#check-merge-conflict): Check for files that contain merge conflict strings
 - [check-shebang-scripts-are-executable](https://github.com/pre-commit/pre-commit-hooks#check-shebang-scripts-are-executable): Check that shebang scripts are executable
 - [check-vcs-permalinks](https://github.com/pre-commit/pre-commit-hooks#check-vcs-permalinks): Check that files contain VCS permalinks
 - [check-yaml](https://github.com/pre-commit/pre-commit-hooks#check-yam): Check that YAML files are valid
 - [detect-aws-credentials](https://github.com/pre-commit/pre-commit-hooks#detect-aws-credentials): Detect AWS credentials
 - [detect-private-key](https://github.com/pre-commit/pre-commit-hooks#detect-private-key): Detect private keys
 - [double-quote-string-fixer](https://github.com/pre-commit/pre-commit-hooks#double-quote-string-fixer): Fix double quoted strings
 - [end-of-file-fixer](https://github.com/pre-commit/pre-commit-hooks#end-of-file-fixer): Makes sure files end in a newline and only a newline
 - [fix-byte-order-marker](https://github.com/pre-commit/pre-commit-hooks#fix-byte-order-marker): Fix byte order marker (BOM) in files
 - [fix-encoding-pragma](https://github.com/pre-commit/pre-commit-hooks#fix-encoding-pragma): Fix encoding pragma in files
 - [mixed-line-ending](https://github.com/pre-commit/pre-commit-hooks#mixed-line-ending): Normalize line endings to be consistent
 - [pretty-format-json](https://github.com/pre-commit/pre-commit-hooks#pretty-format-json): Pretty format JSON files
 - [trailing-whitespace](https://github.com/pre-commit/pre-commit-hooks#trailing-whitespace): Trims trailing whitespace

### Extra hooks

 - [tfsec](https://github.com/aquasecurity/tfsec): tfsec is a static analysis security scanner for your Terraform code. It scans your .tf files to detect potential security issues. To install it, please follow the [instructions](https://github.com/aquasecurity/tfsec#installation).
 - [terraform-docs](https://terraform-docs.io/): Terraform Docs is a utility to generate documentation from Terraform modules in various output formats. To install it, please follow the [instructions](https://terraform-docs.io/user-guide/installation/).
 - [checkov](https://www.checkov.io/): Checkov is a static code analysis tool for infrastructure-as-code. It scans cloud infrastructure provisioned using Terraform, Cloudformation, Kubernetes, Serverless or ARM templates and detects security and compliance misconfigurations. To install it, please follow the [instructions](https://www.checkov.io/2.Basics/Installing%20Checkov.html).
 - [terraform validate](https://www.terraform.io/docs/commands/validate.html): The terraform validate command validates the configuration files in a directory, referring only to the configuration and not accessing any remote services such as remote state, provider APIs, etc. It uses your current Terraform installation to run. No need to install any extra dependency.
 - [terraform fmt](https://www.terraform.io/docs/commands/fmt.html): The terraform fmt command is used to rewrite Terraform configuration files to a canonical format and style. It uses your current Terraform installation to run. No need to install any extra dependency.
 - [tflint](https://github.com/terraform-linters/tflint): TFLint is a Terraform linter focused on possible errors, best practices, etc. To install it, please follow the [instructions](https://github.com/terraform-linters/tflint#installation).
 - [TruffleHog](https://github.com/trufflesecurity/trufflehog): TruffleHog searches through git repositories for secrets, digging deep into commit history and branches. This is effective at finding secrets accidentally committed. To install it, please follow the [instructions](https://github.com/trufflesecurity/trufflehog#floppy_disk-installation).
 - [commitlint](https://commitlint.js.org/#/): commitlint checks if your commit messages meet the [conventional commit format](https://www.conventionalcommits.org/en/v1.0.0/). To install it, please follow the [instructions](https://commitlint.js.org/#/guides-local-setup).


## Usage

### How it works

`pre-commit` is a framework for managing and maintaining multi-language pre-commit hooks. The hooks are run in the order they are specified in the `.pre-commit-config.yaml` file. If any of the hooks fail, the commit is aborted.

### How to install

To install `pre-commit` in your local repository, run:
```bash
pre-commit install
```

Note: If you are using `pyenv` and `pyenv-virtualenv`, you need to install `pre-commit` in the virtual environment of your project. For example:

```bash
pyenv virtualenv 3.8.5 my-project
pyenv activate my-project
pip install pre-commit
pre-commit install
```

### How to uninstall

To uninstall `pre-commit` in your local repository:

```bash
pre-commit uninstall
```

### How to run manually

To run `pre-commit` manually, run:

```bash
pre-commit run --all-files
```

## Skipping issues

### From tfsec

If you want to skip a specific issue from `tfsec`, you can add the following comment in the line you want to skip:

```hcl
#tfsec:ignore:aws-ec2-no-public-egress-sgr:exp:2024-01-02
```

For more information about issue suppression, please follow this instructions: https://aquasecurity.github.io/tfsec/v1.0.0-rc.1/getting-started/configuration/ignores/

Where `aws-ec2-no-public-egress-sgr` is the ID of the issue you want to skip. You will find the ID of the issue when you run `pre-commit run --all-files` and `tfsec` detects an issue.
The `exp` is the expiration date of the issue. After that date, the issue will be detected again.

### From checkov

If you want to skip a specific issue from `checkov`, you can add the following comment in the line you want to skip:

```hcl
#checkov:skip=CKV_AWS_23:The security group doesn't have a description
```
Where `CKV_AWS_23` is the ID of the issue you want to skip. You will find the ID of the issue when you run `pre-commit run --all-files` and `checkov` detects an issue.
To suppress a checkov issue in other formats than HCL, please follow this instructions: https://www.checkov.io/2.Basics/Suppressing%20and%20Skipping%20Policies.html


Make sure to add the comment in the same line where the issue is detected. Otherwise, it will not work. Try to avoid skipping issues as much as possible.
We understand that sometimes it is necessary due to the nature of the code. However, if you are skipping issues because you don't agree with the recommendation, please open an issue in the repository and let us know.
