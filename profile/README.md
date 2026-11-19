## 📋 Description
MQTT ESL project develop team.

## 🎯 Ultimate Goal
为商店更换智能电子价签及配备电子价签管理系统。
电子价签管理系统需要分别适配不同品牌的电子价签。

## 🏗️ Structure
```mermaid
flowchart LR
	subgraph Hardware["📡 硬件"]
		ESL1["ESL 1<br/>品牌 A"] <-->|无线通信| AP[AP]
		ESL2["ESL 2<br/>品牌 B"] <-->|无线通信| AP
		ESL3["ESL 3<br/>品牌 C"] <-->|无线通信| AP
		ESL4["ESL 4<br/>品牌 D"] <-->|无线通信| AP
	end
	subgraph Backend["🧠 后端"]
		Client[MQTT Client]
		Adapter[MQTT Adapter]
		Manager[Info Manager]
		MCP[MCP Server]
		NormalServer["RESTful Server"]
		Client <-->|服务调用| Adapter
		Adapter <-->|管理请求| Manager
		Manager <-->|暴露接口| MCP
		Manager <-->|暴露接口| NormalServer
	end
	subgraph Service["⚙️ 服务"]
		MQTT[MQTT Server]
		MySQL[(MySQL)]
	end
	Client <-->|MQTT 协议| MQTT
	AP <-->|MQTT 通信| MQTT
	Manager <-->|数据读写| MySQL
	subgraph FrontendSystem["🌐 前端"]
		ChatUI["对话控制界面"]
		DashboardUI["精细控制界面"]
		RestClient[RESTful API Client]
		ChatUI -->|文字指令| RestClient
		DashboardUI -->|精细指令| RestClient
	end
	NormalServer <-->|HTTP 协议| RestClient

	classDef blue fill:#EFF6FF,stroke:#3B82F6,color:#1E3A8A;
	classDef purple fill:#F3E8FF,stroke:#7C3AED,color:#4C1D95;
	classDef orange fill:#FFF7ED,stroke:#F59E0B,color:#92400E;
	classDef green fill:#ECFDF5,stroke:#10B981,color:#065F46;
	class MySQL green;
	linkStyle 0,1,2,3 stroke:#3B82F6,stroke-width:2px;
	linkStyle 8,9 stroke:#7C3AED,stroke-width:2px;
	linkStyle 4,5,6,7,11,12,13 stroke:#F59E0B,stroke-width:2px;
	linkStyle 10 stroke:#10B981,stroke-width:2px;
```

## 🧩 Module Features
### 🧠 Backend
[mqtt-esl-management-backend](https://github.com/MQTT-ESL-Dev/mqtt-esl-management-backend)
* Language: Python
* Dependencies:
```toml
dependencies = [
    "pydantic",
    "paho-mqtt",
    "sqlalchemy",
    "sqlmodel",
    "fastapi[standard]",
]
```
#### MQTT Adapter
适配不同品牌、不同型号的 MQTT 响应，并对数据进行清洗和标准化处理后交给 `Info Manager`。

#### MQTT Client
通过 `paho-mqtt` 库与 MQTT Server 建立通信连接并进行相关操作。

#### Info Manager
负责数据库连接和信息存储。

#### MCP Server
提供 MCP 接口。

#### RESTful Server
提供 RESTful HTTP 接口。

### 🌐 Frontend
[mqtt-esl-management-frontend](https://github.com/MQTT-ESL-Dev/mqtt-esl-management-frontend)
* Language: Typescript
* Build Tool: Vite
* Framework: Vue
#### 对话控制界面
通过文字输入生成控制指令，适合批量、粗略地修改多个 ESL。

#### 精细控制界面
展示 ESL 在线状态，支持对单个 ESL 进行精细化修改。
