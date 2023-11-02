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
