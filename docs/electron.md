# Electron Study Tips
## Install Packages Behind Proxy
```
npx cross-env ELECTRON_GET_USE_PROXY=true GLOBAL_AGENT_HTTPS_PROXY=http://127.0.0.1:10809 npm install --save-dev electron
```
