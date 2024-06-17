# LangFlow IDE chart

Helm chart for LangFlow as IDE with a persistent storage or an external database (for example PostgreSQL).


## Quick start

Install the chart:

```bash
helm repo add langflow https://langflow-ai.github.io/langflow-helm-charts
helm repo update
helm install langflow-ide langflow/langflow-ide -n langflow --create-namespace
```


## Examples
See more examples in the [examples directory](https://github.com/langflow-ai/langflow-helm-charts/tree/main/examples/langflow-ide).