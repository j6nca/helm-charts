# flux

## Setup

```
curl -s https://fluxcd.io/install.sh | sudo bash
flux bootstrap git \
  --url=ssh://git@github.com/j6nca/k8s-sandbox \
  --branch=main \
  --private-key-file=/home/jng/.ssh/id_rsa \
  --path=gitops/flux
```