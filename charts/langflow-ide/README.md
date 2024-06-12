# LangFlow IDE chart

Helm chart for LangFlow as IDE.

## Quick start

Install the chart:

```bash
helm repo add langflow https://langflow-ai.github.io/langflow-helm-charts
helm repo update
helm install langflow-ide langflow/langflow-ide -n langflow --create-namespace
```