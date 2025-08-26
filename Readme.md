# Install Argocd
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

# Start argocd ui server using port forwarding, because argocd ui service is CLusterIP
k port-forward svc/arcocd-server -n argocd 8080:443

# Username
username: admin

# Get password
k -n argocd get secret argocd-initial-admin-secret -o json

# Decode password, as secrets are stored in base64 format
echo "<base64 password>" | base64 --decode
