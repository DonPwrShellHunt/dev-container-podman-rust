# Try setting up podman based container development on MBP

There is evidence that podman is supported, at least to some degree by the Dev Containers extension.

The magic sauce is this set of lines in devcontainer.json

```json
 "runArgs": [
     "--userns=keep-id:uid=1000,gid=1000"
 ],
     "containerUser": "vscode",
     "updateRemoteUserUID": true,
     "containerEnv": {
         "HOME": "/home/vscode"
     }
```

## Podman-Desktop upgraded

1.4.0 to 1.5.2 done on 20231103

Immediately relaunched Dev-container-test project and expect continued operational goodness!

## Test onboarding of podman-desktop given podman is removed

Are we running in rootless mode, and
do we have write access to project file?

1. Yes, we are still running in rootless mode
1. Yes, we can write to project files
