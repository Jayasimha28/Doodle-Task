# Doodle-Task

# Launch Kubernetes cluster locally:

# Using minikube: 
Ref: https://minikube.sigs.k8s.io/docs/start/


# Custom namespace creation:
kubectl apply -f Custom-Namespace.yaml


# Infinispan Deployment:
kubectl apply -f Infinispan.yaml

# Postgres Deployment:
kubectl apply -f Postgresql-Deployment.yaml


# KeyCloak Deployment:

Create secret for SSL Certification using below command. Please generate SSL certificate on your own.

kubectl create secret tls my-tls --key="keycloak-jay.com.key" --cert="keycloak-jay.com.crt" -n jay

kubectl apply -f Keycloak-Deployment.yaml
