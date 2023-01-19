## Tutorial https://cloud.google.com/community/tutorials/nginx-ingress-gke
## https://docs.nginx.com/nginx-ingress-controller/installation/installation-with-manifests/
## install helm
- choco install kubernetes-helm

## create deployment
- kubectl create deployment hello-app --image=gcr.io/google-samples/hello-app:1.0

## expose port 8080
- kubectl expose deployment hello-app --port=8080 --target-port=8080

## Deploy NGINX Ingress Controller
- helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx or
- helm repo add nginx-stable https://helm.nginx.com/stable
- helm repo update or 

## Deploy an NGINX controller Deployment and Service
- helm install ingress-nginx ingress-nginx/ingress-nginx
- helm install embrio-ingress-nginx-controller nginx-stable/nginx-ingress -n embrio-development 
- helm install my-release nginx-stable/nginx-ingress --set controller.image.repository=myregistry.example.com/nginx-plus-ingress --set controller.nginxplus=true
- helm install embrio-ingress-nginx-controller ingress-nginx/ingress-nginx -n embrio-development --create-namespace \
  --set=installCRDs=false \
  --set=managedNamespaces='{embrio-development, embrio-staging}' \
  --set=createClusterScopedResources=false \
  --set=webhook.enabled=false \
  --set=config.validateStorageClass=false