```yaml
cat <<EOF > /opt/k8s/work/istio_first/flaskapp-default-vs-v2.yaml
apiVersion: networking.istio.io/v1alpha3
kind: VirtualService
metadata:
  name: flaskapp-default-v2
spec:
  hosts:
  - flaskapp
  http:
  - route:
    - destination:
        host: flaskapp
        subset: v2
EOF
```

