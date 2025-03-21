# Setup

#### Generate SSH Key
```bash
ssh-keygen -t rsa -b 4096 -C "<your_email@example.com>"
cat ~/.ssh/id_rsa.pub
```
#### Set User Information
```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

#### Check Remote Branch
```bash
git remote -v
```

#### Update SSH URL
```bash
git remote set-url origin git@github.com:example/example.git

```

#### Clone All Repositories
```bash
gh repo list OasisUrban --limit 1000 --json sshUrl -q '.[].sshUrl' | xargs -n1 git clone
```
