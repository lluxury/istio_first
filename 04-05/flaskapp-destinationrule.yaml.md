

```yaml
cat <<EOF > /opt/k8s/work/istio_first/flaskapp-destinationrule.yaml
apiVersion: networking.istio.io/v1alpha3
kind: DestinationRule
metadata:
  name: flaskapp
spec:
  host: flaskapp.default.svc.cluster.local
  trafficPolicy:
  subsets:
  - name: v1
    labels:
      version: v1
  - name: v2
    labels:
      version: v2
EOF
```

