# SSH & GitHub Setup

Bootstrap steps for configuring GitHub SSH authentication over port 443 on a fresh Fedora environment.

## 1. Generate SSH Key

```bash
ssh-keygen -t ed25519 -C "reeloc10@users.noreply.github.com"
cat ~/.ssh/id_ed25519.pub
```

Add the public key to **GitHub → Settings → SSH and GPG keys**.

## 2. Verify Host Key & Configure `known_hosts`

Verify the host key fingerprint against the official documentation:
* [GitHub's SSH key fingerprints](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/githubs-ssh-key-fingerprints)

- Copy the listed keys manually to ssh known hosts file.
- Add a 2nd copy to be replacing github.com with [ssh.github.com]:443

```bash
ls -alh ~/.ssh/known_hosts
nvim ~/.ssh/known_hosts
:%s/github.com/[ssh.github.com]:443/gc
ls -alh ~/.ssh/known_hosts
```

## 3. Verify & Switch Remote URLs

Test the SSH handshake:

```bash
ssh -T -p 443 git@ssh.github.com
# Expected: Hi reeloc10! You've successfully authenticated, but GitHub does not provide shell access.
```

Switch existing HTTPS clones to SSH:

```bash
git remote set-url origin ssh://git@ssh.github.com:443/reeloc10/fedora-setup
```
