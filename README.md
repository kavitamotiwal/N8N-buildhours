{
  "name": "Orchestrator pattern - Agent as tool",
  "nodes": [
    {
      "parameters": {
        "options": {
          "systemMessage": "You are a helpful assistant who can do research and newsletter creation and delivery. You have necessary agents as tools to do research and for newsletter creation and delivery.\nDo not invoke any agent more than once.\nWhen you receive any topic from the user, do research and create a newsletter and send it out on Gmail and update the Google doc."
        }
      },
      "type": "@n8n/n8n-nodes-langchain.agent",
      "typeVersion": 3.1,
      "position": [
        416,
        0
      ],
      "id": "16aa17a7-488f-42c3-9104-d5499fa82c99",
      "name": "Orchestrator"
    },
    {
      "parameters": {
        "options": {}
      },
      "type": "@n8n/n8n-nodes-langchain.chatTrigger",
      "typeVersion": 1.4,
      "position": [
        160,
        0
      ],
      "id": "bfc0ec77-22e8-4fea-bb90-74c1f137d68e",
      "name": "When chat message received",
      "webhookId": "5bafc0cd-c64e-494d-907a-f1ce9cf05cf6"
    },
    {
      "parameters": {
        "contextWindowLength": 100
      },
      "type": "@n8n/n8n-nodes-langchain.memoryBufferWindow",
      "typeVersion": 1.3,
      "position": [
        432,
        208
      ],
      "id": "b1883452-6dd1-4c7b-8999-a61591cd51b0",
      "name": "Simple Memory"
    },
    {
      "parameters": {
        "toolDescription": "Research agent which can do web search, deep research to find relevant information for any topic.\nCall this agent only when you want to do any research.",
        "text": "={{ /*n8n-auto-generated-fromAI-override*/ $fromAI('Prompt__User_Message_', ``, 'string') }}",
        "options": {
          "systemMessage": "You are a research assistant which can do web search, deep research to find relevant information for any topic. You can leverage the serpapi tool to do web searches. Do not use the tool more than 3 times."
        }
      },
      "type": "@n8n/n8n-nodes-langchain.agentTool",
      "typeVersion": 3,
      "position": [
        576,
        208
      ],
      "id": "e825bb56-06e7-4093-b56f-d52d4713156c",
      "name": "Research agent"
    },
    {
      "parameters": {
        "toolDescription": "Newsletter agent can create beautiful html content for a newsletter and can send it out on email and create a document with the same newsletter content.\nCall this agent when you want to create, send or upload the newsletter",
        "text": "={{ /*n8n-auto-generated-fromAI-override*/ $fromAI('Prompt__User_Message_', ``, 'string') }}",
        "options": {
          "systemMessage": "You are a Newsletter agent who can create beautiful html content for a newsletter and can send it out on email and create a document on Google Drive with the same newsletter content.\nYou have necessary tools to send the email and to update content on a existing Google drive document."
        }
      },
      "type": "@n8n/n8n-nodes-langchain.agentTool",
      "typeVersion": 3,
      "position": [
        832,
        192
      ],
      "id": "6dbcb72b-4933-4923-8742-36e710f76f35",
      "name": "Newsletter agent"
    },
    {
      "parameters": {
        "contextWindowLength": 20
      },
      "type": "@n8n/n8n-nodes-langchain.memoryBufferWindow",
      "typeVersion": 1.3,
      "position": [
        592,
        416
      ],
      "id": "1120fb25-ca19-4df0-aded-7b2bf44233a5",
      "name": "Simple Memory1"
    },
    {
      "parameters": {
        "options": {}
      },
      "type": "@n8n/n8n-nodes-langchain.toolSerpApi",
      "typeVersion": 1,
      "position": [
        736,
        416
      ],
      "id": "9622eff4-05c1-4942-a740-9d9209411c84",
      "name": "SerpAPI",
      "credentials": {
        "serpApi": {
          "id": "GkLNaHMOcFDGacKD",
          "name": "SerpAPI account"
        }
      }
    },
    {
      "parameters": {
        "contextWindowLength": 20
      },
      "type": "@n8n/n8n-nodes-langchain.memoryBufferWindow",
      "typeVersion": 1.3,
      "position": [
        960,
        432
      ],
      "id": "d99e5e02-5865-45a8-94bb-dcaa9377c221",
      "name": "Simple Memory2"
    },
    {
      "parameters": {
        "endpointUrl": "http://localhost:5678/mcp/0d700126-82c6-4bd9-93b4-25e7271851af",
        "options": {}
      },
      "type": "@n8n/n8n-nodes-langchain.mcpClientTool",
      "typeVersion": 1.2,
      "position": [
        1072,
        400
      ],
      "id": "f3f5ea79-cad0-46b0-975c-3e187585dc6b",
      "name": "MCP Client"
    },
    {
      "parameters": {
        "model": {
          "__rl": true,
          "mode": "list",
          "value": "gpt-5-mini"
        },
        "builtInTools": {},
        "options": {}
      },
      "type": "@n8n/n8n-nodes-langchain.lmChatOpenAi",
      "typeVersion": 1.3,
      "position": [
        288,
        208
      ],
      "id": "3345daa5-b75e-433c-a0f5-0031556d60c1",
      "name": "OpenAI Chat Model",
      "credentials": {
        "openAiApi": {
          "id": "wAjo9M82r8ZAEvNu",
          "name": "OpenAI account"
        }
      }
    },
    {
      "parameters": {
        "model": {
          "__rl": true,
          "mode": "list",
          "value": "gpt-5-mini"
        },
        "builtInTools": {},
        "options": {}
      },
      "type": "@n8n/n8n-nodes-langchain.lmChatOpenAi",
      "typeVersion": 1.3,
      "position": [
        448,
        416
      ],
      "id": "dc9a5027-544d-4f9e-8ec6-7562b5ee485f",
      "name": "OpenAI Chat Model1",
      "credentials": {
        "openAiApi": {
          "id": "wAjo9M82r8ZAEvNu",
          "name": "OpenAI account"
        }
      }
    },
    {
      "parameters": {
        "model": {
          "__rl": true,
          "mode": "list",
          "value": "gpt-5-mini"
        },
        "builtInTools": {},
        "options": {}
      },
      "type": "@n8n/n8n-nodes-langchain.lmChatOpenAi",
      "typeVersion": 1.3,
      "position": [
        848,
        544
      ],
      "id": "e2c50f2c-2ab7-4d2d-8f54-d7d44c369922",
      "name": "OpenAI Chat Model2",
      "credentials": {
        "openAiApi": {
          "id": "wAjo9M82r8ZAEvNu",
          "name": "OpenAI account"
        }
      }
    }
  ],
  "pinData": {},
  "connections": {
    "When chat message received": {
      "main": [
        [
          {
            "node": "Orchestrator",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Simple Memory": {
      "ai_memory": [
        [
          {
            "node": "Orchestrator",
            "type": "ai_memory",
            "index": 0
          }
        ]
      ]
    },
    "Research agent": {
      "ai_tool": [
        [
          {
            "node": "Orchestrator",
            "type": "ai_tool",
            "index": 0
          }
        ]
      ]
    },
    "Newsletter agent": {
      "ai_tool": [
        [
          {
            "node": "Orchestrator",
            "type": "ai_tool",
            "index": 0
          }
        ]
      ]
    },
    "Simple Memory1": {
      "ai_memory": [
        [
          {
            "node": "Research agent",
            "type": "ai_memory",
            "index": 0
          }
        ]
      ]
    },
    "SerpAPI": {
      "ai_tool": [
        [
          {
            "node": "Research agent",
            "type": "ai_tool",
            "index": 0
          }
        ]
      ]
    },
    "Simple Memory2": {
      "ai_memory": [
        [
          {
            "node": "Newsletter agent",
            "type": "ai_memory",
            "index": 0
          }
        ]
      ]
    },
    "MCP Client": {
      "ai_tool": [
        [
          {
            "node": "Newsletter agent",
            "type": "ai_tool",
            "index": 0
          }
        ]
      ]
    },
    "OpenAI Chat Model": {
      "ai_languageModel": [
        [
          {
            "node": "Orchestrator",
            "type": "ai_languageModel",
            "index": 0
          }
        ]
      ]
    },
    "OpenAI Chat Model1": {
      "ai_languageModel": [
        [
          {
            "node": "Research agent",
            "type": "ai_languageModel",
            "index": 0
          }
        ]
      ]
    },
    "OpenAI Chat Model2": {
      "ai_languageModel": [
        [
          {
            "node": "Newsletter agent",
            "type": "ai_languageModel",
            "index": 0
          }
        ]
      ]
    }
  },
  "active": false,
  "settings": {
    "executionOrder": "v1",
    "binaryMode": "separate"
  },
  "versionId": "eec607e3-fb7c-4b95-8f1d-bd54bcbba7ee",
  "meta": {
    "templateCredsSetupCompleted": true,
    "instanceId": "6089fa415c55765801aa79a5bee2005464d7cf177f40340b0b199ddff0a06d13"
  },
  "id": "PcfkHzJBM5ABHoUV",
  "tags": [
    {
      "updatedAt": "2026-06-27T04:29:54.255Z",
      "createdAt": "2026-06-27T04:29:54.255Z",
      "id": "JSxYqykowNq02i1p",
      "name": "N8N Class"
    }
  ]
}
