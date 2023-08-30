# Contributing Guidelines

Contributions are welcome via GitHub pull requests. 

To contribute to homelab-ansible, please use pull requests on a branch of your own fork.

This document outlines the process to help get your contribution accepted.

## Sign Your Commits

Contributors must sign their commits locally using GPG.

See GitHub documentation [here](https://docs.github.com/en/authentication/managing-commit-signature-verification/signing-commits).

## How to Contribute

1. Fork this repository, develop and test your changes.
2. Remember to sign your commits locally using GPG as described above.
3. Submit a pull request.

### Step-by-step 

After creating your fork on GitHub, you can do:

```bash
$ git clone --recursive git@github.com:your-name/homelab-ansible
$ cd homelab-ansible
$ git checkout -b your-branch-name
# DO SOME CODING HERE
$ git add your new files
$ git commit -S -m "YOUR_COMMIT_MESSAGE"
$ git push origin your-branch-name
```

You will then be able to create a pull request from your commit.

## Coding Conventions

This project uses Ansible-lint in order to adopt proven practices and avoid pitfalls that could make code harder to maintain.

