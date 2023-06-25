# bw-env

Populate local environment variables from Bitwarden. This was inspired by [my colleague at Gruntwork](https://blog.gruntwork.io/how-to-securely-store-secrets-in-bitwarden-cli-and-load-them-into-your-zsh-shell-when-needed-f12d4d040df) and then improved slightly.

This content is also on my [blog](https://fulcrumops.com/blog/bitwarden-env-vars).

## Overview

`bw-env` is a zsh function that retrieves passwords from Bitwarden and sets environment variables based on the key(s) in the `username` field and the password(s) in the `password` field.

![bw-env.gif](img/bw-env.gif)
## Installation and configuration

You must have the [Bitwarden CLI](https://bitwarden.com/help/cli/#download-and-install) (`bw`) installed and configured.

### Clone this repository and cd into it

```
# Clone this repository and cd into it
git clone https://github.com/FulcrumOps/bw-env.git
cd bw-env
```

### Copy the bw-env script into place

```
cp bw-env ~/.zsh_autoload_functions/bw-env
```
### Add the autoload command to your .zshrc file
```
echo 'autoload -Uz bw-env' >> ~/.zshrc
```

### Reload your shell

## Storing a secret

Let's store a Github PAT.

1. In Bitwarden, create a Login. Set the name to something unique. In this example, we'll use "Github PAT".
1. In the `username` field, put `GITHUB_TOKEN GITHUB_OAUTH_TOKEN`.
1. In the `password` field, put the token value you've obtained from Github. If you put multiple values in here, they will pair up with the keys in the `username` field, with the last password being used for any extra keys.
1. Save the login.

## Setting env vars

Now, we can pull the variable names and password value(s) out of Bitwarden:

1. Run `bw sync` (not usually necessary, but is required if you make any changes or add new logins).
1. Run `bw-env Github PAT` (or whatever your unique name is).
1. `GITHUB_TOKEN` and `GITHUB_OAUTH_TOKEN` will now be populated in your shell.
