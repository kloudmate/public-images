# public-images

The open-source container images a KloudMate on-prem install runs (Kubernetes operators,
datastores, monitoring), copied unchanged from their upstream registries into one place:
`ghcr.io/kloudmate/public-images`.

A customer network that may reach only a few hosts then pulls every open-source image from
GitHub instead of Docker Hub, quay.io, ghcr.io and registry.k8s.io. Each image keeps its path
and tag; only the registry changes:

```
quay.io/strimzi/operator:0.45.2  ->  ghcr.io/kloudmate/public-images/strimzi/operator:0.45.2
docker.io/grafana/grafana:13.3.0 ->  ghcr.io/kloudmate/public-images/grafana/grafana:13.3.0
```

Every image here is public and pulls without a login. KloudMate's own images are not here.

## How it updates

[`images.txt`](images.txt) lists every image. Each KloudMate on-prem release adds its list;
nothing is removed, so older releases keep pulling. A push to `images.txt` runs the
[Mirror](.github/workflows/mirror.yml) workflow, which copies what's new and checks that every
image pulls without a login. A package GitHub creates for the first time is private until an
org owner makes it public once in its settings; the workflow lists any that still are.

## Licences

Each image is redistributed unchanged under its own licence, which the image carries. This
repository adds none of its own to them.
