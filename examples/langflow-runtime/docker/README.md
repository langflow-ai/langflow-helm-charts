# Package the flow as docker image

You can package the flow as a docker image and refer to it in the chart.

```bash
# Download the flows
wget https://raw.githubusercontent.com/datastax/langflow-charts/main/examples/flows/justchat.json
# Build the docker image locally
docker build -t myuser/langflow-just-chat:1.0.0 .
# Push the image to DockerHub
docker push myuser/langflow-just-chat:1.0.0
```

The use the runtime chart to deploy the application:

```bash
helm repo add datastax-langflow-charts https://datastax.github.io/langflow-charts
helm repo update
helm install langflow-runtime datastax-langflow-charts/langflow-runtime \
    --set "image.repository=myuser/langflow-just-chat" \
    --set "image.tag=1.0.0" \
```
