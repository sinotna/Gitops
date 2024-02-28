# Initial installation 

ArgoCD
1. cd argo-cd
2. helm install argocd ./ -n argocd --create-namespace
3. ArgoCD should be up and running now. The secret "argocd/argocd-initial-admin-secret" is created with the admin password

**All application deployment to namespace** [link](https://argo-cd.readthedocs.io/en/stable/operator-manual/app-any-namespace/#:~:text=The%20Application%20's%20namespace%20must,source%20Application%20resources%20from%20globally.)

App Apps

This branch is the app of apps method.
The argocd templates directory contains the AppProject.yaml and the Platform-rootapp.yaml files. The platform-rootapp will point to gitops-apps repo. This repo is holding the application's yaml files (kind: Application) which are pointing to the app's repository. 
 
All applications will automatically start after applying the application sets.
 > kubectl apply -f appilcationsets.yaml



# Sealed Secrets


The secrets are encrypted using the sealed secrets services

Steps to encrypt a secret:

1. Get the sealed secrets public key. 
    > kubeseal --fetch-cert --controller-name=sealed-secrets --controller-namespace=sealed-secrets > pub-sealed-secrets.pem
1. Encrypt the secret using the pub key.
    > kubeseal --cert pub-sealed-secrets.pem < secret-example.yaml > mysealed-secret.yaml
1. Apply the mysealed-secret.yaml
    > kubectl apply -f seales-secret-example.yaml