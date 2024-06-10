# LangFlow IDE chart

Helm chart for LangFlow as IDE.

## Quick start

Install the chart:

```
helm repo add datastax-langflow-charts https://datastax.github.io/langflow-charts
helm repo update
helm install langflow-ide datastax-langflow-charts/langflow-ide -n langflow --create-namespace
```
