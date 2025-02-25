# SSH Key Configuration Lab

## Objective  
Generate public and private SSH keys on macOS and configure passwordless SSH access to an Ubuntu VM. Set up a shortcut command (`ssh ivolve`) to connect without specifying the username, IP, or key.

## Configuration Steps

### 1. Generate SSH Key Pair (macOS)
```bash
ssh-keygen -t rsa -b 4096 -f ~/.ssh/id_rsa
```
### 2. Copy Public Key to Ubuntu VM
```bash
ssh-copy-id -i ~/.ssh/id_rsa.pub hager@192.168.105.11
```
### 3. Configure SSH Client (macOS)
Create/edit ~/.ssh/config:
```bash
Host ivolve
    HostName 192.168.105.11
    User hager
    IdentityFile ~/.ssh/id_rsa
    IdentitiesOnly yes
```
### 4. Enable Passphrase Caching 
```bash
eval "$(ssh-agent -s)"
ssh-add --apple-use-keychain ~/.ssh/id_rsa
```
### 5. Test Connection
```bash
ssh ivolve
```
### output 
![Alt text](Screen4.png)