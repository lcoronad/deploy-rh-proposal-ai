# Deploy-rh-proposal-ai

Comand to generate ApplicationSet of ArgoCD, and this generate all applications

kustomize build bootstrap/base | oc apply -f -

To verify the yamls generate, you can run this commands

kustomize build apps/chatbot-ui/base/
kustomize build apps/ocp-agent-service/base/
kustomize build apps/llama-stack-server-milvus-rhoai/base/

To apply manually each application, you can run this commands

oc apply -k apps/chatbot-ui/base/ -n rh-proposal-ai
oc apply -k apps/ocp-agent-service/base/ -n rh-proposal-ai
oc apply -k apps/llama-stack-server-milvus-rhoai/base/ -n rh-proposal-ai

To register MCP Server manually into Llama Stack Server run this command in pod's terminal

llama-stack-client toolgroups register --provider-id model-context-protocol --mcp-endpoint http://ocp-agent-service.rh-proposal-ai.svc.cluster.local:7860/gradio_api/mcp/sse ocp::proposal