# k8s-install-istio

Install istioctl
```
export ISTIO_VERSION=1.14.3
wget https://github.com/istio/istio/releases/download/$ISTIO_VERSION/istio-$ISTIO_VERSION-linux-amd64.tar.gz
tar xf istio-$ISTIO_VERSION-linux-amd64.tar.gz
cd istio-$ISTIO_VERSION
sudo mv bin/istioctl /usr/local/bin/
istioctl version
```

Init istio 
```
istioctl operator init
kubectl get po -n istio-operator
istioctl install --set profile=default
kubectl get svc,po -n istio-system
```

Set auto injection
```
kubectl create ns istio-test
kubectl label namespace istio-test istio-injection=enabled
kubectl apply -f samples/sleep/sleep.yaml -n istio-test
kubectl get po -n istio-test
```

Install kiali and jaeger
```
kubectl create -f samples/addons/kiali.yaml
kubectl get po,svc -n istio-system -l app=kiali
kubectl create -f samples/addons/jaeger.yaml
```

Integrate external prometheus and grafana
```
kubectl apply -n monitoring -f istio-metrics-aggregation.yaml
kubectl apply -n monitoring -f istio-prometheus.yaml
https://istio.io/latest/docs/ops/integrations/grafana/
```
