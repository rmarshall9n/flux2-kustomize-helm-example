# installation

## config

```sh
export GITHUB_TOKEN=<your-token>
export GITHUB_USER=<your-username>
export GITHUB_REPO=<repository-name>
```

## staging

```sh
k3d cluster create -c cluster-staging.yaml

flux bootstrap github \
    --context=k3d-staging \
    --owner=${GITHUB_USER} \
    --repository=${GITHUB_REPO} \
    --branch=main \
    --personal \
    --path=clusters/staging
```

## production

```sh
k3d cluster create -c cluster-production.yaml

flux bootstrap github \
    --context=k3d-staging \
    --owner=${GITHUB_USER} \
    --repository=${GITHUB_REPO} \
    --branch=main \
    --personal \
    --path=clusters/staging
```
