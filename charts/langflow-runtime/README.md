# LangFlow runtime chart

Deploy LangFlow flows to Kubernetes with this Helm chart.

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
