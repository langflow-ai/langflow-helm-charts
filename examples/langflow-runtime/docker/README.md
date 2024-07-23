# Package the flow as docker image

You can package the flow as a docker image and refer to it in the chart.

```bash
# Download the flows
wget https://raw.githubusercontent.com/datastax/langflow-charts/main/examples/flows/basic-prompting-hello-world.json
# Build the docker image locally
docker build -t myuser/langflow-hello-world:1.0.0 .
# Push the image to DockerHub
docker push myuser/langflow-hello-world:1.0.0
```

The use the runtime chart to deploy the application:

```bash
helm repo add langflow https://langflow-ai.github.io/langflow-helm-charts
helm repo update
helm install langflow-runtime langflow/langflow-runtime \
    --set "image.repository=myuser/langflow-hello-world" \
    --set "image.tag=1.0.0"
```
