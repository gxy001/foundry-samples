# Text Translation Agent

## Summary
This code sample helps create agents that handle multilingual text processing, including dynamic language detection and bidirectional translation using Azure AI Translator service. 

## Use Cases
1. **Text Translation**: Translate text between multiple languages for seamless communication.
2. **Business Communication**: Enable businesses to localize content for global audiences.
3. **Educational Content**: Translate learning materials to make them accessible to non-native speakers.

## Architecture Overview
The system consists of:
- An AI Agent created with Azure AI Agent Service using `gpt-4o` as the base model.
- Azure AI Translator integrated for language detection and translation.
- A Bicep template to automate provisioning of Azure resources.

```text
+----------------+                         
|   User Query   |                         
| (Any Language) |                         
+-------+--------+                         
        |                                  
        v                                  
+-------------------+        invokes        +----------------------------+
| Translation Agent | ------------------->  | Azure AI Translator (API)  |
|     (AI Agent)    | <-------------------  | (Language Translation)     |
+-------------------+        results        +----------------------------+
        |                                  
        v                                  
+-------------------------------+           
| Agent Respond translated text |                   
+-------------------------------+           

```

## Setup Instructions

### Prerequisites
- Python 3.8+
- Azure CLI
- Azure subscription
- Agent setup: deploy the latest agent setup using ([this custom deployment](hhttps://aka.ms/basic-agent-deployment)).
  - The above creates:
    1. AI Services resource (type: Microsoft.CognitiveServices/accounts),
    2. AI Project (type: Microsoft.CognitiveServices/accounts/projects),
    3. Model deployment (type: Microsoft.CognitiveServices/accounts/deployments) 
- A custom connection of the resource that supports Azure AI Translator service is added to the project of your Agent. 
  - You can use the translator service with Azure AI Foundry resource, AI hub resource or Azure AI Translator resource. 
  - In your agent project management center, use "Custom keys" connection when adding the custom connection in the connected resources page. 
  - To add a "Custom keys" connection, add a key value pair with Ocp-Apim-Subscription-Key as the key name, and the resource key as the value. For Azure AI Foundry resource and AI hub resource, you can find the resource key value in the resource overview page in the Azure AI Foundry portal management center. You can also find the key of any type of resources in the Azure portal. 
  - For more info to create a connection, see [Create a connection](https://learn.microsoft.com/azure/ai-foundry/how-to/connections-add)
  - For more info about Azure AI Translator service, see [Text translation Overview](https://learn.microsoft.com/en-us/azure/ai-services/translator/text-translation/overview)

### Steps
1. **Clone the Repository**

2. **Set Config Variables**

4. **Run the Agent Script**
```bash
 python template.py
```

## ⚙️ Configuration Guide
| Parameter Name                         | Description                                                                       |
|----------------------------------------|-----------------------------------------------------------------------------------|
| `project_endpoint`                     | Endpoint for the project this agent is using                                      |
| `model_name`                           | Name of the model deployment to be used for the Agent                             |
| `translator_resource_connection_name`  | Name of the translator resource connection added in the agent project             |
| `connection_id`                        | Connection ID for the translator resource connection added in the agent project   |

## Sample Data Instructions
You can try the sample user messages and test the interaction by invoking the agent with prompts as listed in the next section.

## Example Agent Interaction
### User: 
Translate this Chinese poem to English: 白日依山尽，黄河入海流

### Agent:
At the end of the day, the Yellow River flows into the sea.

### User: 
translate this text to Chinese, Spanish, and Korean: Translator Agent handles multilingual text processing, including dynamic language detection and bidirectional translation using Translator service. The translator agent is triggered when the user message has the “translation intent”.

### Agent: 
Here are the translations:

Chinese: Translator Agent 处理多语言文本，包括使用 Translator服务的动态语言检测和双向翻译。当用户消息具有 “translation intent” 时，将触发翻译代理。
Spanish: Translator Agent se encarga del procesamiento de texto multilingüe, incluida la detección dinámica de idiomas y la traducción bidireccional mediante el servicio Translator. El agente traductor se activa cuando el mensaje del usuario tiene la "intención de traducción".
Korean: Translator Agent는 Translator 서비스를 사용하여 동적 언어 감지 및 양방향 번역을 포함한 다국어 텍스트 처리를 처리합니다. 변환기 에이전트는 사용자 메시지에 "번역 의도"가 있을 때 트리거됩니다.

### User: 
localize this text to Japanese and Germany: The agent can detect the source language for the input text unless the source language is defined in the user message. 

### Agent: 
Here are the localized texts:

Japanese: エージェントは、入力テキストのソース言語を検出できます。ただし、ソース言語がユーザー・メッセージで定義されていない場合に限ります。
German: Der Agent kann die Ausgangssprache für den Eingabetext erkennen, es sei denn, die Ausgangssprache ist in der Benutzermeldung definiert.

## Customization Tips
- Modify the system instructions in `template.py` to your specif needs (e.g., special handling on some terminologies).
- Extend the agent with other useful tools or APIs (using OpenAPI spec).

## License
This project is licensed under the MIT License. See the [LICENSE](./LICENSE) file for details.
