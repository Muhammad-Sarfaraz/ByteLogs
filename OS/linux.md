# Linux

#### Get Current Dir Size
```sh
du -sh .
```

#### Clean All Files Inside a Dir
```sh
rm -rf ./*
```


#### Get Storage Information
```sh
df -h
```

#### Clear Unnecessary Logs
```sh
sudo journalctl --vacuum-time=1d
sudo journalctl --vacuum-size=500M
```

