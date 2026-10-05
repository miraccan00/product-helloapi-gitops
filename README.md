# product-helloapi-gitops

The product team's deploy repo for [hellofiber](https://github.com/miraccan00/hellofiber), part of the
*GitOps in Production* series on [miraccanyilmaz.me](https://miraccanyilmaz.me). Argo CD reads it through the
`products` ApplicationSet in [platform-gitops](https://github.com/miraccan00/platform-gitops); each
article's runnable lab is a folder in [blog-wiki](https://github.com/miraccan00/blog-wiki).

| Article | Branch used |
|---|---|
| Argo CD in HA, Explained by Breaking It · [EN](https://miraccanyilmaz.me/en/blog/argocd-ha-app-of-apps/) · [TR](https://miraccanyilmaz.me/blog/argocd-ha-app-of-apps/) | `blog-04` |
| Argo CD SSO Integration: OIDC and RBAC with ZITADEL · [EN](https://miraccanyilmaz.me/en/blog/argocd-sso-zitadel/) · [TR](https://miraccanyilmaz.me/blog/argocd-sso-zitadel/) | `blog-04` (unchanged) |
| Moving Secrets into Vault: From base64 in Git to Vault and ESO Without Downtime · [EN](https://miraccanyilmaz.me/en/blog/vault-eso-secret-migration/) · [TR](https://miraccanyilmaz.me/blog/vault-eso-secret-migration/) | `blog-04` (unchanged) |

```
chart/                      Helm chart: Deployment + Service, MESSAGE/APP_ENV, /healthz probes
overlays/dev/               kustomization (helmCharts) + values.yaml: image tag, replicas, env
overlays/prod/              same, prod values
```

Shipping a new build = changing `image.tag` in `overlays/<env>/values.yaml`. Argo CD syncs it; nobody runs
`kubectl` or `helm` against the cluster. Platform-gitops pins this repo to `blog-04`, so `main` can move
without changing what the labs deploy.
