# Google Cloud
- See tracking https://github.com/ObrienlabsDev/blog/issues/47
## RAG Engine

- Europe-west3 ff rag engine https://docs.cloud.google.com/vertex-ai/generative-ai/docs/rag-engine/rag-overview
- https://github.com/ObrienlabsDev/blog/issues/47
- https://github.com/GoogleCloudPlatform/generative-ai/tree/main/gemini/use-cases/retrieval-augmented-generation
- https://github.com/facebookresearch/faiss
- https://github.com/vllm-project/vllm
- https://docs.cloud.google.com/kubernetes-engine/docs/tutorials/serve-llama-gpus-vllm

## Vertex AI Search (part of Gen App Builder)
Vertex AI Search is a part of Vertex AI Agent Builder
- https://cloud.google.com/enterprise-search?utm_source=chatgpt.com&hl=en
- https://cloud.google.com/generative-ai-app-builder/pricing?hl=en
- Create a project and get $1000 US of credits for 1 year - make sure to attach a billing id that does not have a pervious credit for...
- "Trial for Gen App Builder" - Following SKUs.
Vertex AI Search: Search API Request Count - Standard (services/74B1-77CF-C302/skus/BADA-EE26-7BDA)
Vertex AI Search: Search API Request Count - Enterprise (services/74B1-77CF-C302/skus/93D6-7280-CF05)
Vertex AI Search: Search API Request Count - LLM Add-on (services/74B1-77CF-C302/skus/151B-D7A2-B5B5)
Vertex AI Search and Conversation: Data Index (services/74B1-77CF-C302/skus/BC7D-6A97-90F8)
Audio interactions with Vertex AI Conversation - Voice Experience (services/FBC0-AA4A-C89A/skus/1A04-3B12-74DC)
Text interactions with Vertex AI Conversation - Chat Experience (services/FBC0-AA4A-C89A/skus/90FE-6D2B-0AE1)

<img width="1855" height="809" alt="Screenshot 2026-02-05 at 14 41 42" src="https://github.com/user-attachments/assets/a8cca459-684e-42ae-b169-08ef18703f5a" />
- proceed with https://cloud.google.com/products/agent-builder?hl=en
- you will see the followiing credit added to your account
- Trial for Gen App Builder Available	100% $1,355.26 $1,355.26	One-time	Gen_App_Builder_12b94822648ba1a2828e16bead90637469df7d0d4b62db9ffbdafe32d38cf185 Certain usage; see the terms of the promotion for details. February 5, 2026
- 
<img width="1598" height="125" alt="Screenshot 2026-02-05 at 14 50 38" src="https://github.com/user-attachments/assets/c5217f16-7277-432b-bb43-f7620b6fd445" />

## Navigate to your gen app builder project
- TODO: determine regional resources - for PII and PBMM data in the vector store
- https://console.cloud.google.com/gen-app-builder/engines?referrer=search&project=gen-app-builder-old&supportedpurview=project
- conversational agent
- https://conversational-agents.cloud.google.com/projects/gen-app-builder-old/enable?targetUrl=%2Fprojects%2Fgen-app-builder-old%2Flocations%2Fglobal%2Fagents%3Fdialog%3DagentCreationOptions
- 
<img width="1855" height="552" alt="Screenshot 2026-02-05 at 14 53 54" src="https://github.com/user-attachments/assets/f06045dd-3db0-4fbe-807c-0e6fe30522c7" />
- enable dialog flow
<img width="1859" height="527" alt="Screenshot 2026-02-05 at 14 54 23" src="https://github.com/user-attachments/assets/3db26e70-f5ce-400e-8614-75113a5ac48f" />
- create custom or prebuilt agent
<img width="1851" height="823" alt="Screenshot 2026-02-05 at 14 56 06" src="https://github.com/user-attachments/assets/2fff24c5-8358-4e4f-8f64-beb4c21aba6a" />
- create custom in northamerica-northeast1 (Montreal)
<img width="1857" height="1073" alt="Screenshot 2026-02-05 at 14 57 29" src="https://github.com/user-attachments/assets/ad3270b8-6b57-47cf-90c6-e2d814cc1203" />
- using prebuilt feedback flow - https://cloud.google.com/dialogflow/cx/docs/concept/prebuilt-component/feedback
<img width="1851" height="831" alt="Screenshot 2026-02-05 at 15 00 23" src="https://github.com/user-attachments/assets/1d1e5704-c79d-4371-b4b4-66b68583aea9" />

<img width="1856" height="874" alt="Screenshot 2026-02-05 at 15 01 14" src="https://github.com/user-attachments/assets/974d6583-38b0-4b88-97bb-8e1ab0b5eeb5" />

- todo: intruduce RAG document additions


