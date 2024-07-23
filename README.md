# NeSI analysis environment OOD Jupyter app

JupyterLab app for running on the NeSI OOD Analysis Environment

## Docker commands

Docker login
```
echo $PAT | docker login ghcr.io -u USERNAME --password-stdin
```

Build and Tag
```
docker build --no-cache -t ghcr.io/lbrick/ood-jupyter-k8s-app/ood-jupyter-k8s:v0.2 .
```

Push
```
docker push ghcr.io/lbrick/ood-jupyter-k8s-app/ood-jupyter-k8s:v0.2
```