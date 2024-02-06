# K8S IAM

## Introduction

This project is a keycloak based identity and access management solution for kubernetes.

## Prerequisites

### Understand

Before deploying, ensure that an egress is created via the keycloak-sendgrid-egress-policy.yaml file. This is required for the keycloak email verification process.
If you do not deploy this policy, the keycloak pod will not be able to send emails to users for verification.

I only discoverd this after 14 hours of debugging, so I hope this saves you some time.

## About

This project used the Bitnami Keycloak helm chart to deploy keycloak to a kubernetes cluster. The chart is configured to use a postgres database, and the chart is configured to use the default keycloak realm.

## Deployment

To deploy, run the following commands:

```bash
kubectl create namespace keycloak
kubectl apply -f user-cluster-role-binding.yaml
kubectl apply -f keycloak-sendgrid-egress-policy.yaml
kubectl apply -f group-cluster-role-binding.yaml
kubectl apply -f certificate.yaml
```

Then run the helmchart command to deploy keycloak:

``` bash
helm upgrade --install keycloak --namespace keycloak bitnami/keycloak --reuse-values -f values.yaml 
```