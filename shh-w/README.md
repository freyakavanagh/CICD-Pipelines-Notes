# SSH to Push to GitHub

SSH is superior to HTTPS when it comes to security as it uses a keypair rather than just a username and password.
    - Main issue is where you store the key pair


You can regenerate a public key from a private key, but not the other way around.
    - .pem file is the private key
    - public key can be stored on the website e.g. AWS


Give each key an identifiable name.

## SSH Key Steps

![](../ReadMeImages/shhsetupdiagram.jpeg)

1. Generate a key pair in the SSH folder
2. Register the public key on GitHub
3. Add the private key to the SSH regiser
4. Create a test repo
5. Push changes to repo using SSH


SSH is used to authenticate in many ways on many services. Jenkins needs SSH to authenticate e.g. EC2 instances


1. cd into .ssh
2. ssh-key -t rsa -b 4096 -C "freyakavanagh@rocketmail.com"
   - -t = type
   - -b = number of bytes
   - -C = email
3. Name the key e.g. freya-github-key
4. empty for no passphrase
5. .pub is the public key
6. Got to GitHub, settings, SSH and GPG Keys
7. Add new SSH Key
8. Match name to key folder, Authentication Key, Enter whole key (cat "name")
9. command in terminal .ssh file: eval `ssh-agent -s`
10. ssh-add key name
11. authenticate key: ssh -T git@github.com 
12. set up new repo to test
13. create folder in terminal
14. initialise etc., push
