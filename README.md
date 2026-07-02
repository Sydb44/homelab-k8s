# homelab-k8s

Kubernetes manifests for everything running on my k3s cluster (a two-node setup, the Arch workstation as control plane and a Debian box as worker). Each top-level folder is one service and deploys with `kubectl apply -f <folder>/` — Gitea, its Actions runner, Grafana, Prometheus, Vaultwarden, Nextcloud, Paperless-ngx, Uptime Kuma, Traefik as the ingress controller, node-exporter for metrics, a Restic cronjob backing up to Backblaze B2, and cloudflared for the tunnel that gets everything onto the internet without opening a port.

Anything sensitive is SOPS-encrypted before it's committed — look for `secret.yaml` files, they're not readable without the age key even though the filename doesn't say so. CI runs kubeconform on every push to catch broken manifests before they hit the cluster.
