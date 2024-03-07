[[R]]
[[RStudio]]

### Helpful links:
* [Keyboard shortcuts](https://support.rstudio.com/hc/en-us/articles/200711853-Keyboard-Shortcuts-in-the-RStudio-IDE)
* [Getting started on RStudio at Aetna](https://github.aetna.com/analytics-org/abc-tech-repo/blob/719152aa9a3ae2563eddfa9db85baaaaa90a9489/programming/r/odbc.md)

Steps:
* Install two packages:
```R
install.packages("sparklyr")
install.packages("aetnar")
```
* Make sure your password is up to date
```R
aetnar::encrypt_password()
```

