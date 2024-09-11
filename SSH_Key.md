# SSH key

## SSH Generation
```
ssh-keygen -t -rsa -b 4096 -C "comment, typically your email to help identify"
```
the system will ask where do you want to save it, hit entry to use the default location: ```~/.ssh/id_rsa```
when asking for pass pharase, you can type in a password to further protect the key.

this generate 2 keys ```id_rsa``` and ```id_rsa.pub```, you will need to copy the content of ```id_rsa.pub``` to your server's ```authorized_keys``` folder, located under ```~/.ssh/```, if the file do not exits, create one.
after the change, make sure to alter it's permissions:

* windows:
```
icacls C:\Users\<YourUserName>\.ssh\authroized_keys /inheritance:r
icacls C:\Users\<YourUserName>\.ssh\authroized_keys /grant <YourUserName>:F
```
The first line removes all permissions the file inheritance from it's group, and the second line give the user full control of the file.

Also better to configure it to only allow private ssh key logins on the server: 
Open ```C:\ProgramData\ssh\sshd_config```
add configure these 2 options:
```
PubkeyAuthentication yes
PasswordAuthentication no
```
Restart the service to reflect the change:
```
Restart-Service sshd
```

* Linux
```
chmod 700 ~/.ssh
chomd 600 ~/.ssh/authroized_keys
```

## To use SSH key to log in
first, start the ```ssh-agent```
* windows
```
Start-Service ssh-agent
Set-Service -Name ssh-agent -StartupType Automatic
```

* Linux:
```
eval $(ssh-agent -s)
```

add the ssh private key to the agent:
```
ssh-add /path/to/ssh_key
```
if permissions are too open, change it:
```
chmod 600 /path/to/ssh_key
```
you may need to type in the password