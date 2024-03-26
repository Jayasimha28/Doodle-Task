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

## Create secret for SSL Certification using below command. Please generate SSL certificate on your own.

# Hostname: keycloak-jay.com

# ****command to create .jks***
keytool -genkey -alias server -keyalg RSA -keysize 2048 -keystore keycloak-jay.com.jks

# *****command to check .jks file*****
keytool -list -v -keystore keycloak-jay.com.jks

*****Generating p12 from .jks file****
keytool -importkeystore -srckeystore keycloak-jay.com.jks -destkeystore keycloak-jay.com.p12 -srcstoretype JKS -deststoretype PKCS12 -deststorepass admin1234

# *** creating .key file from p12 *****
openssl pkcs12 -in keycloak-jay.com.p12 -nodes -nocerts | openssl rsa -out keycloak-jay.com.key


# ******* from p.12 to crt****
openssl pkcs12 -in keycloak-jay.com.p12 -nokeys -out keycloak-jay.com.crt

# **** creating pem file ***
openssl pkc1s2  -in keycloak-jay.com.p12 -out keycloak-jay.pem


kubectl create secret tls my-tls --key="keycloak-jay.com.key" --cert="keycloak-jay.com.crt" -n jay

kubectl apply -f Keycloak-Deployment.yaml

# TO enable Port mapping and access from Browser


kubectl port-forward service/keycloak 8085:8080 -n jay

kubectl port-forward service/infinispan 8086:11222 -n jay

