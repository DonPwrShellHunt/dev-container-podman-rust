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

In late February 2024 I revisited testing dev containers, in particularly my dev-container-test in github. This is a very simple hello world Rust example, but I am using Podman rather than Docker.

Podman Desktop and podman were reinstalled, which is documented elsewhere, and after cleaning up previous dev container artifacts (see Dev Container commands in vscode palette) and updating the Dev Containers extension it worked.

By worked, I mean I am able to edit the source files and do a `cargo run` within the container to output the literal text.

Podman Desktop is on version 1.7.1.
Podman is on version 4.9.2.

Brew is no longer used in these installs, as podman docs suggest using their installer technology (pkg download).

## Test onboarding of podman-desktop given podman is removed

I had some issues with the onboarding process due to several podman components still running/or existing. Once those were identified and squashed, the onboarding proceeded reasonably well.

Are we running in rootless mode, and
do we have write access to project file?

1. Yes, we are still running in rootless mode
1. Yes, we can write to project files

And are we able to `cargo run` from the container workspace and get output?

* `YES` Feb 25, 2024
