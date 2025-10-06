Kubernetes SIGs: https://github.com/kubernetes-sigs
https://github.com/ahmetb/kubectl-node_resource?tab=readme-ov-file

- install kubectl view-allocations and 

- install kubectl krew plugin:

  kubectl krew install node-resource
  OR
(
  set -x; cd "$(mktemp -d)" &&
  OS="$(uname | tr '[:upper:]' '[:lower:]')" &&
  ARCH="$(uname -m | sed 's/x86_64/amd64/;s/arm.*$/arm/')" &&
  KREW="krew-${OS}_${ARCH}" &&
  curl -fsSLO "https://github.com/kubernetes-sigs/krew/releases/latest/download/${KREW}.tar.gz" &&
  tar zxvf "${KREW}.tar.gz" &&
  ./"${KREW}" install krew
)

export PATH="${KREW_ROOT:-$HOME/.krew}/bin:$PATH"

kubectl krew install view-allocations
kubectl krew install node-resource

kubectl view-allocations --group-by node --show-zero
kubectl node-resource allocation --sort-by=memory-percent --summary=hide
kubectl node-resource allocation --summary=only
kubectl node-resource utilization --summary=only 
kubectl node-resource utilization --json
kubectl node-resource allocation --show-gpu --gpu-resource-key=amd.com/gpu
kubectl node-resource utilization --show-cpu --show-memory
kubectl node-resource allocation --show-cpu=false --show-memory --show-ephemeral-storage --show-gpu

kubectl top nodes
kubectl top pods --all-namespaces


Install Metrics Server
kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml
kubectl get deployment metrics-server -n kube-system

