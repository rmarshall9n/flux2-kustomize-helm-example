# installation

## config

```sh
export GITHUB_TOKEN=
export GITHUB_USER=rmarshall9n
export GITHUB_REPO=flux2-kustomize-helm-example
```

## staging

```sh
k3d cluster create staging -c cluster-staging.yaml

flux bootstrap github \
    --context=k3d-staging \
    --owner=${GITHUB_USER} \
    --repository=${GITHUB_REPO} \
    --branch=main \
    --personal \
    --path=clusters/staging

watch flux get helmreleases --all-namespaces
```

## production

```sh
k3d cluster create production -c cluster-production.yaml

flux bootstrap github \
    --context=k3d-staging \
    --owner=${GITHUB_USER} \
    --repository=${GITHUB_REPO} \
    --branch=main \
    --personal \
    --path=clusters/staging
```
