# Setup VS Code devcontainer configuration on M1 MacBookPro

## Rancher Desktop exploration for devcontainer environment

After seeing several open issues on using podman-desktop/podman for devcontainers, I started looking at other alternatives. Docker Desktop & Rancher Desktop were my other choices. Rancher Desktop is open source and specific references in the VS Code docs said it was an acceptable alternative to Docker Desktop. Rancher can also be used for kubernetes easily, but can turn this off if not needed.

I decided to install Rancher Desktop and give it a try. I attempted to clear out any configuration items relating to my podman setup. It took a while to get the DOCKER_HOST value specific to podman to go away. Restarting VS Code after removing the DOCKER_HOST env variable from .zshrc was needed.

I also experienced a Dialog box when I tried to run devcontainers with Rancher that indicated I needed to install Docker version 17.12.0 or later. To get around this, I had to set docker path in VS Code settings (Devcontainer extension) to ~/.rd/bin/docker. I think the restart of Code was also instrumental in keeping that install dialog from reappearing.

### Rancher devcontainer testing

The first test I did was directly from the Rancher Desktop docs in the tutorials section. I got the javascript/node devcontainer running without too many issues.

The second test was my dev-container-podman-rust repository, which now has a bogus name since I am moving to Rancher instead. The runArgs value which had worked in podman, did not work in Rancher. After some research, I replaced the runArgs content and was able to get things running.

(podman version)

```json
"runArgs": [
    "--userns=keep-id:uid=1000,gid=1000"
],
```

(Rancher version)

```json
"runArgs": [
    "--user=1000:1000"
]
```

While this was successful, I'm not confident that the syntax I used with podman was totally right. And I'm not sure any runArgs are needed for Rancher. For now, I'll leave it as is and revisit the topic at some future date.

## Try setting up podman based container development on MBP FAILED

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
