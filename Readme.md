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

# Use this repo in the ci-cd pipeline of the other repo like below:

On the .github/workflow, we will have a file to write ci-cd, where we can add a stage names `Update and push the image in argo-deployment repo` and script will be like below:

```
git clone https://github.com/Sumeetrana/argo-deployment
cd argo-deployment
Command to update image in manifest.yml file with the latest image that we pushed
git add .
git commit -m "Updated image"
git push (with personal access token)
```
