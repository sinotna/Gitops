# Initial installation 

ArgoCD
1. cd argo-cd
2. helm install argocd ./ -n argocd --create-namespace
3. ArgoCD should be up and running now. The secre "argocd/argocd-initial-admin-secret" is created with the admin password

Application Sets