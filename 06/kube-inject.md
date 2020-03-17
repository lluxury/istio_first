```sh
# Update resources on the fly before applying.
kubectl apply -f <(istioctl kube-inject -f <resource.yaml>)

# Create a persistent version of the deployment with Envoy sidecar
# injected.
istioctl kube-inject -f deployment.yaml -o deployment-injected.yaml

# Update an existing deployment.
kubectl get deployment -o yaml | istioctl kube-inject -f - | kubectl apply -f -

# Capture cluster configuration for later use with kube-inject
kubectl -n istio-system get cm istio-sidecar-injector  -o jsonpath="{.data.config}" > /tmp/inj-template.tmpl
kubectl -n istio-system get cm istio -o jsonpath="{.data.mesh}" > /tmp/mesh.yaml
kubectl -n istio-system get cm istio-sidecar-injector -o jsonpath="{.data.values}" > /tmp/values.json
# Use kube-inject based on captured configuration
istioctl kube-inject -f samples/bookinfo/platform/kube/bookinfo.yaml \
	--injectConfigFile /tmp/inj-template.tmpl \
	--meshConfigFile /tmp/mesh.yaml \
	--valuesFile /tmp/values.json
```

