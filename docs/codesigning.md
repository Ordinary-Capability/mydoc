# Self-sign App Files with Private Certificate
## Run **makecert** with administrator account to generate issuer's **.pvk** and **.cer** files
```
makecert -r -pe -n "CN=fullhan.com" -ss CA -sr CurrentUser -a sha256 -cy authority -sky signature -sv fullhanCA.pvk fullhanCA.cer
```
Input *password1* in prompt ui.
## Add the cert to local store
```
certutil -user -addstore Root fullhanCA.cer
```

## Run **makecert** again to generate subject's PVK files
```
makecert -pe -n "CN=fullhan.com" -a sha256 -cy end -sky signature -ic fullhanCA.cer -iv fullhanCA.pvk -sv fullhanSPC.pvk fullhanSPC.cer
```
Input *password2* in prompt ui.
## Convert subject's PVK file to **.pfx** file which is used to code signing certificate.
```
pvk2pfx -pvk fullhanSPC.pvk -spc fullhanSPC.cer -pfx fullhanSPC.pfx -po "password3"
```

## Use **SignTool** and **.pfx** file to sign files (.exe, .dll)
```
SignTool sign /f fullhanSPC.pfx /fd SHA256 /p fullhan /t http://timestamp.digicert.com F:\tmp\self_signed_demo\bin\Debug\net7.0\self_signed_demo.exe
```

## Verify the signed files
```
SignTool verify /pa F:\tmp\self_signed_demo\bin\Debug\net7.0\self_signed_demo.exe
```

