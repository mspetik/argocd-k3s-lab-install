# ArgoCD – k3s lab instalace

Výukový instalátor ArgoCD pro k3s cluster.

argocd-k3s-lab-install/
├── kustomization.yaml          # hlavní řídicí soubor Kustomize
└── patches/
    ├── argocd-namespace.yaml   # namespace pro ArgoCD
    ├── argocd-server-lb.yaml   # změna Service na LoadBalancer
    ├── argocd-insecure.yaml    # spuštění ArgoCD UI v HTTP režimu
    └── argocd-repo-secret.yaml # registrace Git repozitáře


Co instalace provede:
- nainstaluje ArgoCD
- nastaví Service typu LoadBalancer
- zapne HTTP režim (--insecure)
- zaregistruje GitHub repozitář pro GitOps

Instalace:

kubectl apply -k .

nebo 

kubectl apply -k https://github.com/mspetik/argocd-k3s-lab-install.git

Po instalaci ověření 

kubectl get svc -n argocd

Výsledek by měl být:

argocd-server   LoadBalancer   …   192.168.0.xxx   80/TCP

Otevři v prohlížeči:

http://192.168.0.xxx

Přihlášení:
uživatel: admin
heslo:

kubectl -n argocd get secret argocd-initial-admin-secret \
-o jsonpath="{.data.password}" | base64 -d
