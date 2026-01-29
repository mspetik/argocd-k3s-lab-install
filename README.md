# ArgoCD – k3s lab instalace

Výukový instalátor ArgoCD pro k3s cluster.

Co instalace provede:
- nainstaluje ArgoCD
- nastaví Service typu LoadBalancer
- zapne HTTP režim (--insecure)
- vypne NetworkPolicy (kvůli k3s labům)
- zaregistruje GitHub repozitář pro GitOps

Instalace:

kubectl apply -k .

Po instalaci:

kubectl get svc -n argocd

Otevři v prohlížeči:

http://<EXTERNAL-IP>

Přihlášení:
uživatel: admin
heslo:

kubectl -n argocd get secret argocd-initial-admin-secret \
-o jsonpath="{.data.password}" | base64 -d
