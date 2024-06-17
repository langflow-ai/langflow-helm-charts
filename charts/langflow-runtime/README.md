# LangFlow runtime chart

Deploy LangFlow flows to Kubernetes with this Helm chart.
Using a dedicated deployment for a set of flows is fundamental in production environments in order to have a granular resource control.


## Import a flow

There are two ways to import a flow:

1. **From a remote location**: You can reference a flow stored in a remote location, such as a URL or a Git repository by customizing the `values.yaml` file in the section `downloadFlows`:

```yaml
downloadFlows:
  flows:
    - url: https://raw.githubusercontent.com/langflow-ai/langflow/dev/tests/data/BasicChatwithPromptandHistory.json
#      basicAuth: "myuser:mypassword"
#      headers:
#        Authorization: "Bearer my-key"
```

2. **Packaging the flow as docker image**: You can add a flow from to a docker image based on Langflow runtime and refer to it in the chart.
   See an example in the `apps` directory.

## Deploy the flow

Install the chart (using option 1):

```bash
helm repo add langflow https://langflow-ai.github.io/langflow-helm-charts
helm repo update
helm install langflow-runtime langflow/langflow-runtime \
    --set "downloadFlows.flows[0].uuid=4ca07770-c0e4-487c-ad42-77c6039ce02e" \
    --set "downloadFlows.flows[0].url=https://raw.githubusercontent.com/datastax/langflow-charts/main/examples/langflow-runtime/just-chat/justchat.json" \
    --set replicaCount=1
```

Tunnel the service to localhost:

```bash
kubectl port-forward svc/langflow-langflow-runtime 7860:7860
```

Call the flow API endpoint:
```bash
curl -X POST \
    "http://localhost:7860/api/v1/run/4ca07770-c0e4-487c-ad42-77c6039ce02e?stream=false" \
    -H 'Content-Type: application/json'\
    -d '{
      "input_value": "message",
      "output_type": "chat",
      "input_type": "chat",
      "tweaks": {
          "ChatInput-1BPcY": {},
          "ChatOutput-J1bsS": {}
      }
    }'
```

## Scale the flows

In order to add more resources to the flows container, you could decide to scale:
- Horizontally, by adding more replicas of the deployment
- Vertically, by adding more cpu/memory resources to the deployment


### Scale horizontally

To scale horizontally you only need to modify the `replicaCount` parameter in the chart.

```yaml
helm install langflow-runtime langflow/langflow-runtime \
    --set "downloadFlows.flows[0].uuid=4ca07770-c0e4-487c-ad42-77c6039ce02e" \
    --set "downloadFlows.flows[0].url=https://raw.githubusercontent.com/datastax/langflow-charts/main/examples/langflow-runtime/just-chat/justchat.json" \
    --set replicaCount=5
```

### Scale vertically

By default the deployment doesn't have any limits and it could consume all the node resources. 
In order to limit the available resources, you can modify the `resources` value:

```yaml
resources:
  limits:
    cpu: 100m
    memory: 128Mi
  requests:
    cpu: 100m
    memory: 128Mi
```


To scale vertically you only need modify the `resources`

```
helm install langflow-runtime langflow/langflow-runtime \
    --set "downloadFlows.flows[0].uuid=4ca07770-c0e4-487c-ad42-77c6039ce02e" \
    --set "downloadFlows.flows[0].url=https://raw.githubusercontent.com/datastax/langflow-charts/main/examples/langflow-runtime/just-chat/justchat.json" \
    --set replicaCount=5
```
