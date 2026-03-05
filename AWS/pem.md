#### Windows
Permission issues on .pem file on windows OS.
```sh
icacls aws.pem /inheritance:r
icacls aws.pem /grant:r "$($env:USERNAME):(R)"
icacls mwdev.pem /inheritance:r
```
