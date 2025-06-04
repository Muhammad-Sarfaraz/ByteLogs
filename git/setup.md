# Setup

#### Generate SSH Key
```bash
ssh-keygen -t rsa -b 4096 -C "<your_email@example.com>"
cat ~/.ssh/id_rsa.pub
```
#### Set User Information
- Global
```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

- Local Repo
```bash
git config user.name "Your Name"
git config user.email "your_email@example.com"
```

#### Check Remote Branch
```bash
git remote -v
```

#### Update SSH URL
```bash
git remote set-url origin git@github.com:example/example.git



# Mac
ls ~/.ssh

ssh-keygen -t ed25519 -C "email"
eval "${ssh-agent -s}"
ssh-add ~/.ssh/id_ed25519
pbcopy < ~/.ssh/id_ed25519.pub
ssh -T git@github.com


```

#### Clone All Repositories
```bash
gh repo list ORG_NAME --limit 1000 --json sshUrl -q '.[].sshUrl' | xargs -n1 git clone
```
