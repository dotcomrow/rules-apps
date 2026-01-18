# rules-apps
App-of-apps scaffolding for registering Drools/KIE rule containers after artifacts
are published to GitHub Packages.

This repo is intended to be managed by Argo CD. Each directory under `manifests/apps/`
is an Argo application payload (a Job that registers a container on the KIE Server).
No business rule source code should live here.

## Usage

1) Create an Argo CD ApplicationSet from `manifests/applicationset.yaml`.
2) Add a new rules app by copying `manifests/apps/example` and editing the coordinates.
3) Commit and push; Argo CD will run the registration Job in the drools namespace.

## Prereqs

- Argo CD namespace `argocd`, project `rules-apps`.
- Vault Kubernetes auth role `drools` allows the Job service account.
- KIE Server reachable at:
  `http://kie-server.drools.svc.cluster.local:8080/kie-server/services/rest/server`
