# bw-env

Populate local environment variables from Bitwarden

## Overview

`bw-env` is a zsh function that retrieves passwords from Bitwarden and sets environment variables based on the name(s) in the `username` field,

## Installation and configuration

You must have the [Bitwarden CLI](https://bitwarden.com/help/cli/#download-and-install) (`bw`) installed and configured.

```
git clone https://github.com/FulcrumOps/bw-env.git
cd bw-env
cp bw-env ~/.zsh_autoload_functions/bw-env
echo 'autoload -Uz bw-env' >> ~/.zshrc
```

Reload your shell afterwards.

## Storing a secret

Let's store a Github PAT.

1. In Bitwarden, create a Login. Set the name to something unique, like "Github PAT".
1. In the `username` field, put `GITHUB_TOKEN GITHUB_OAUTH_TOKEN`.
1. In the `password` field, put the token value you've obtained from Github. If you put multiple values in here, they will pair up with the keys in the `username` field, with the last password being used for any extra keys.
1. Save the login.

## Setting env vars

Now, we can pull the variable names and password value(s) out of Bitwarden:

1. Run `bw sync` (not always necessary, but is required if you make any changes or add new logins).
1. Run `bw-env Github PAT` (or whatever your unique name is).
1. `GITHUB_TOKEN` and `GITHUB_OAUTH_TOKEN` will now be populated in your shell.
