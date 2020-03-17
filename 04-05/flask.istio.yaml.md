```yaml
cd /opt/k8s/work/first_istio
cat > flask.istio.yaml  <<EOF
apiVersion: v1
kind: Service
metadata:
  name: flaskapp
  labels:
    app: flaskapp
spec:
  selector:
    app: flaskapp
  ports:
    - name: http
      port: 80
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: flaskapp-v1
  labels:
    app: flaskapp
    version: v1
spec:
  replicas: 1
  selector:
    matchLabels:
      app: flaskapp
      version: v1
  template:
    metadata:
      labels:
        app: flaskapp
        version: v1
    spec:
      containers:
      - name: flaskapp
        image: dustise/flaskapp
        # imagePullPolicy: Always
        imagePullPolicy: IfNotPresent

        env:
        - name: version
          value: v1
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: flaskapp-v2
  labels:
    app: flaskapp
    version: v2
spec:
  replicas: 1
  selector:
    matchLabels:
      app: flaskapp
      version: v2
  template:
    metadata:
      labels:
        app: flaskapp
        version: v2
    spec:
      containers:
      - name: flaskapp
        image: dustise/flaskapp
        # imagePullPolicy: Always
        imagePullPolicy: IfNotPresent

        env:
        - name: version
          value: v2
EOF
```


