# gitops

Declarative state for my Kubernetes sandbox. Argo CD watches this repo
and reconciles the cluster to whatever is committed here.

Cluster itself is provisioned separately: [kind-cluster](https://github.com/hashelka/kind-cluster)
(Terraform → kind → Argo CD bootstrap).

## How it works

Nothing here is applied by hand. A change reaches the cluster by being
merged: Argo CD detects the new desired state and syncs it. If something
is changed directly in the cluster, Argo reports the drift instead of
silently accepting it — the reconciliation loop is the point, not the
automation of deployment.