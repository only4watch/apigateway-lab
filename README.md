# apigateway-lab
...existing code...
# apigateway-lab

A small demo that provisions a Namespace, two sample apps (hello-app and echo-v2),
a GKE managed HTTP Gateway and two HTTPRoutes that expose those services.

Quick overview of resources in this repo:
- Namespace: [`gateway-demo.Namespace`](k8s/01-namespace.yaml) — defined in [k8s/01-namespace.yaml](k8s/01-namespace.yaml)
- hello-app Deployment & Service: [`hello-app.Deployment`](k8s/02-hello-app.yaml), [`hello-svc.Service`](k8s/02-hello-app.yaml) — defined in [k8s/02-hello-app.yaml](k8s/02-hello-app.yaml)
- Gateway (GKE L7 managed): [`external-http-gw.Gateway`](k8s/03-gateway.yaml) — defined in [k8s/03-gateway.yaml](k8s/03-gateway.yaml)
- HTTPRoute for hello-app: [`hello-route.HTTPRoute`](k8s/04-httproute.yaml) — defined in [k8s/04-httproute.yaml](k8s/04-httproute.yaml)
- echo-v2 Deployment & Service: [`echo-v2.Deployment`](k8s/05-second-app.yaml), [`echo-v2.Service`](k8s/05-second-app.yaml) — defined in [k8s/05-second-app.yaml](k8s/05-second-app.yaml)
- Multi-service HTTPRoute (traffic split): [`multi-service-route.HTTPRoute`](k8s/06-multi-service.yaml) — defined in [k8s/06-multi-service.yaml](k8s/06-multi-service.yaml)

Prerequisites
- kubectl configured to a GKE cluster with the Gateway API and the
  `gke-l7-regional-external-managed` GatewayClass available.
- Appropriate IAM / cluster permissions to create Gateways and Services.

Deploy
1. Apply all manifests:
   ```sh
   kubectl apply -f k8s/