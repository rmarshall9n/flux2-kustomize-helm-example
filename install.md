# installation

## config

```sh
export GITHUB_TOKEN= &&
export GITHUB_USER=rmarshall9n &&
export GITHUB_REPO=flux2-kustomize-helm-example
```

## staging

```sh
k3d cluster create staging -c cluster-staging.yaml

flux bootstrap github \
    --components-extra=image-reflector-controller,image-automation-controller \
    --read-write-key \
    --context=k3d-staging \
    --owner=${GITHUB_USER} \
    --repository=${GITHUB_REPO} \
    --branch=main \
    --personal \
    --path=clusters/staging

watch flux get helmreleases --all-namespaces

kubectl get helmcharts --all-namespaces

flux reconcile kustomization flux-system --with-source

kubectl get helmrelease/api-chart -oyaml -n staging | grep 'image:'

k get imagerepository -n flux-system
k get imagepolicy -n flux-system
k -n flux-system describe imagerepositories podinfo
flux get image policy
```

## production

```sh
k3d cluster create production -c cluster-production.yaml

flux bootstrap github \
    --components-extra=image-reflector-controller,image-automation-controller \
    --read-write-key \
    --context=k3d-production \
    --owner=${GITHUB_USER} \
    --repository=${GITHUB_REPO} \
    --branch=main \
    --personal \
    --path=clusters/production
```
