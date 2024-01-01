+++
title = 'Configure GitHub SSH on Mac OS'
date = 2024-01-01T00:00:00-06:00
draft = false
+++

I bought a new apple laptop and configure my development environment. I configured the GitHub SSH setup to push and pull the repositories. The below steps to create SSH and configure the key.

~~~bash
# Generate SSH Key.
# Accepts the default values and enter the passphrase value
ssh-keygen -t ed25519 -C “<email>”

# Generated the public and private key ed25519  
cd ~/.ssh

# Start the SSH agent in the background
eval “$(ssh-agent -s)”

# Create config file
touch ~/.ssh/config

# Edit config file in VS Code
code config

# Add the below lines in the config file
Host * 
  AddKeysToAgent yes
  UseKeychain yes
  IdentityFile ~/.ssh/id_ed25519

# Add the cert in MacOS keychain
ssh-add —apple-use-keychain ~/.ssh/id_ed25519

# Copy the cert in to clipboard
pbcopy < ~/.ssh/id_ed25519.pub

# Navigate to GitHub settings and select “Access” section of the sidebar and click “SSH and GPG Keys”
# Add the public key in the “Key” field

# Test the SSH connection
ssh -T git@github.com
~~~

