# k8s-install-istio
```
export ISTIO_VERSION=1.14.3
wget https://github.com/istio/istio/releases/download/$ISTIO_VERSION/istioctl-$ISTIO_VERSION-linux-amd64.tar.gz
tar xf istioctl-$ISTIO_VERSION-linux-amd64.tar.gz
cd istioctl-$ISTIO_VERSION
istioctl version
```

```
istioctl operator init
kubectl get po -n istio-operator
istioctl manifest apply -f istio-operator.yamml
kubectl get svc,po -n istio-system
```

```
kubectl create ns istio-test
kubectl label namespace istio-test istio-injection=enabled
kubectl apply -f samples/sleep/sleep.yaml -n istio-test
kubectl get po -n istio-test
```

```
kubectl create -f samples/addons/kiali.yaml
kubectl get po,svc -n istio-system -l app=kiali
kubectl create -f samples/addons/jaeger.yaml
```
