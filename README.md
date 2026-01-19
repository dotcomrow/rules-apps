# rules-apps
App-of-apps scaffolding for registering Drools/KIE rule containers after artifacts
are published to GitHub Packages.

This repo is intended to be managed by Argo CD. It contains the ApplicationSet
that discovers rule app repositories and syncs their `manifests/` directories.
No business rule source code or per-app manifests should live here.

## Usage

1) Create an Argo CD ApplicationSet from `manifests/applicationset.yaml`.
2) Tag each rules app repo with the GitHub topic `drools-rules-app`.
3) In each rules app repo, add a `manifests/` directory with the registration and Workbench import jobs.
4) Commit and push; Argo CD will auto-discover repos with the topic and sync them.

## Prereqs

- Argo CD namespace `argocd`, project `rules-apps`.
- Argo CD SCM token secret `github-scm-token` with key `token` (for repo discovery).
- Vault Kubernetes auth role `drools` allows the Job service account.
- KIE Server reachable at:
  `http://kie-server.drools.svc.cluster.local:8080/kie-server/services/rest/server`
- KIE Server Maven settings include access to GitHub Packages for the rules artifacts.
- Workbench import uses a GitHub token with repo read/write for the rule repo.
