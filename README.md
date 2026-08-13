# homelab-config (retired 2026-08-13)

This repo is archived. Everything in it moved to
[homelab-applications](https://github.com/FireBall1725/homelab-applications).

It held one `apps/<name>/app-config.json` per application plus
`appsets/apps.yaml`. The JSON carried four keys & only one of them did any work:

- `namespace` is now the second path segment in `apps/<namespace>/<name>/`
- `targetRevision` was `"HEAD"` in all 57 files
- `replace` was `false` in all 57 files
- `createNamespace` was read through `{{ or .createNamespace true }}`, & `or false
  true` returns `true`, so the five apps that set it to `false` had been getting
  `CreateNamespace=true` the whole time

The ApplicationSet lives at `appsets/apps.yaml` in homelab-applications & runs a
git directory generator over `apps/*/*`. Adding a directory adds an app; there's
no second file to keep in sync.

Nothing in the cluster reads this repo. `Application/app-bootstrap` points at
homelab-applications, & `homelab-config.git` was removed from the
`homelab-gitops` AppProject `sourceRepos`. Both are OpenTofu resources in
`~/Documents/terraform/talos-cluster/core-argocd.tf`.

History is kept here for anyone tracing why an app landed in the namespace it did.
