# Knative

## Installing knative

```
kubectl apply -f https://github.com/knative/serving/releases/download/knative-v1.2.0/serving-crds.yaml

kubectl apply -f https://github.com/knative/serving/releases/download/knative-v1.2.0/serving-core.yaml

kubectl apply -f https://github.com/knative/net-kourier/releases/download/knative-v1.2.0/kourier.yaml

kubectl patch configmap/config-network \
  --namespace knative-serving \
  --type merge \
  --patch '{"data":{"ingress.class":"kourier.ingress.networking.knative.dev"}}'
```

## Verifying

```
kubectl get pods -n knative-serving
```

## Get External IP

```
kubectl --namespace kourier-system get service kourier
```

## Setup Domain

Replace knative.talha.com with whatever domain you want to use.
For testing purposes, you can use your local DNS server or edit the ```/etc/hosts``` file or make your requests to the knative service with the appropirate ```HOST``` header.

```
kubectl patch configmap/config-domain \
  --namespace knative-serving \
  --type merge \
  --patch '{"data":{"knative.talha.com":""}}' 
```