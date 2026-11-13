## 📋 Description
MQTT ESL project develop team.

## 🎯 Ultimate Goal
为商店更换智能电子价签及配备电子价签管理系统。
电子价签管理系统需要分别适配不同品牌的电子价签。

## 🏗️ Structure
```mermaid
flowchart LR
	ESL1["ESL 1<br/>品牌 A"] <-->|无线通信| AP[AP]
	ESL2["ESL 2<br/>品牌 B"] <-->|无线通信| AP
	ESL3["ESL 3<br/>品牌 C"] <-->|无线通信| AP
	ESL4["ESL 4<br/>品牌 D"] <-->|无线通信| AP
	AP <-->|MQTT 通信| MQTT[MQTT Server]
	subgraph MQTTSystem[MQTT ESL 管理系统]
		Client[MQTT Client]
		Adapter[MQTT Adapter]
		Manager[Info Manager]
		MCP[MCP Server]
		NormalServer["RESTful Server"]
		Client <-->|服务调用| Adapter
		Adapter <-->|管理请求| Manager
		Manager <-->|MCP 调用| MCP
		Manager <-->|RESTful API| NormalServer
	end
	Client <-->|MQTT 协议| MQTT
	Frontend[ESL Management Frontend]
	LanguageFrontend[ESL 管理语言识别前端]
	NormalServer <-->|RESTful API| Frontend
	MCP <-->|MCP 协议| LanguageFrontend
	subgraph Service["⚙️ Service"]
		SQLite[(SQLite)]
	end
	Manager <-->|数据读写| SQLite

	classDef blue fill:#EFF6FF,stroke:#3B82F6,color:#1E3A8A;
	classDef purple fill:#F3E8FF,stroke:#7C3AED,color:#4C1D95;
	classDef orange fill:#FFF7ED,stroke:#F59E0B,color:#92400E;
	classDef green fill:#ECFDF5,stroke:#10B981,color:#065F46;
	class SQLite green;
	linkStyle 0,1,2,3 stroke:#3B82F6,stroke-width:2px;
	linkStyle 4,9 stroke:#7C3AED,stroke-width:2px;
	linkStyle 5,6,7,8,10,11 stroke:#F59E0B,stroke-width:2px;
	linkStyle 12 stroke:#10B981,stroke-width:2px;
```

## 🧩 Module Features
### MQTT Adapter
xxxx

### MQTT Client
xxxx

### Info Manager
xxxx

### MCP Server
xxxx

### RESTful Server
xxxx

### ESL Management Frontend
xxxx
