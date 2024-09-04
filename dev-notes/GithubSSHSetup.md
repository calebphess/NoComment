# Setting Up GitHub with SSH Keys
To make things simpler this assumes you are setting up your ssh key from a dev ec2 instance running amazon linux 2023.

## Getting Started
1. First you need to have terminal access in whatever environment you are working in
2. Second you need to generate a new ssh key. You can do this by running the following command:
  - `ssh-keygen -o -t rsa -C "email@domain.com"`
  - hit enter to save the key in the default location in ~/.ssh/id_rsa
  - hit enter again to not use a passphrase
  - hit enter again to confirm the empty passphrase
3. Next you need to copy the SSH key to add it to GitHub
  - `cat ~/.ssh/id_rsa.pub`
  - copy the output of this command
4. Go to GitHub and click on your profile in the top right corner
5. Click on settings
6. Click on SSH and GPG keys
7. Click on New SSH key
8. Give your key a title referencing the device you are using
9. Paste the key you copied from the terminal into the key field
10. Click Add SSH key


