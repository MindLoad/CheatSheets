---
Title: SSH
Date: 2024-10-11 12:44
tags:
  - cheatsheet
---
# Copy private/public keys to another machine
1. Copy your private (e.g. `~/.ssh/id_rsa`) and public (e.g. `~/.ssh/id_rsa.pub`) from your H1 machine to your H2 machine in location `~/.ssh`
2. On H2, change the permission of the private key to be less accessible (otherwise next step will fail) with the command `chmod 600 ~/.ssh/id_rsa`
3. 3. Final Step. on H2, now use the command `ssh-add ~/.ssh/id_rsa` to enable the private-public key pair to be used to identify yourself from H2 to any server that you will connect to by using the private-public key that you imported.


