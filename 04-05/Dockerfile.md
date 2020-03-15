```sh
cat <<EOF > /opt/k8s/work/istio_first/Dockerfile
FROM tiangolo/uwsgi-nginx-flask:python3.7-alpine3.8
COPY ./app /app
VOLUME [ "/app" ]
EOF
```

