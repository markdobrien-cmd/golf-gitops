# golf-gitops

The desired state of every environment for the [golf booking system](https://github.com/markdobrien-cmd/golf-booking).

Argo CD watches this repository and makes the EKS cluster match it. Nobody deploys by running `kubectl` or `helm` by hand:

- CI in `golf-booking` builds an image and commits its new tag here for `dev`.
- Promotion to `prod` is a pull request that copies a tested tag from `dev` to `prod`.
- Rolling back is `git revert`.

Keeping this separate from the application repo means CI's tag bumps don't retrigger application builds, and this repo's history is an audit log of exactly what ran where, and when.

Contents arrive in Phase 6 of the [roadmap](https://github.com/markdobrien-cmd/golf-booking#roadmap):

```
bootstrap/root-app.yaml   # the app of apps
platform/                 # cluster add-ons: load balancer controller, external-secrets, monitoring
apps/dev/  apps/prod/     # per-environment values, including image tags
```
