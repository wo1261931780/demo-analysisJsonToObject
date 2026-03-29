# 🔧 demo-analysisJsonToObject - JSON自动解析工具

![Java](https://img.shields.io/badge/Java-17+-orange?logo=java)
![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.4.1-brightgreen?logo=springboot)
![Jackson](https://img.shields.io/badge/Jackson-2.x-blue)
![License](https://img.shields.io/badge/License-AGPL--3.0-blue.svg)

## 📖 项目简介

demo-analysisJsonToObject是一个全自动JSON解析工具,能够将JSON数据自动解析并转换为Java实体类对象。支持从文件、API请求等多种数据源读取JSON,并提供灵活的解析配置。

## 🎯 核心功能

- **自动解析**: 将JSON字符串自动转换为Java实体对象
- **多数据源支持**: 支持JSON文件、API请求、字符串输入
- **类型推断**: 自动推断JSON字段类型,生成对应的Java类型
- **嵌套对象支持**: 支持多层嵌套JSON结构的解析
- **批量处理**: 支持批量JSON文件的解析和转换

## 📝 项目来源

本项目为个人学习项目,用于演示Spring Boot中Jackson库的JSON解析功能

## 📊 项目架构

```mermaid
flowchart TB
    subgraph Input["📥 输入层"]
        JSON["JSON文件"]
        API["API请求"]
    end
    
    subgraph Controller["🎮 控制层"]
        JC["JsonController<br/>接收请求"]
    end
    
    subgraph Service["⚙️ 业务层"]
        JFS["JsonFileService<br/>核心解析服务"]
        Parse["JSON解析"]
        Convert["对象转换"]
    end
    
    subgraph Output["📤 输出层"]
        Entity["实体类对象"]
        Response["API响应"]
    end
    
    subgraph Tech["🛠️ 技术栈"]
        SB["Spring Boot 3.4.1"]
        JD["Jackson"]
        JDK["Java 17"]
    end

    Input --> Controller
    Controller --> Service
    Service --> Parse
    Parse --> Convert
    Convert --> Output
    
    JSON --> JC
    API --> JC
    JC --> JFS
    JFS --> Entity
    JFS --> Response
    
    Tech --> SB
    Tech --> JD
    Tech --> JDK
    JD --> Parse
    SB --> Controller

    classDef inputStyle fill:#e3f2fd,stroke:#1565c0,stroke-width:2px
    classDef ctrlStyle fill:#fff3e0,stroke:#f57c00,stroke-width:2px
    classDef svcStyle fill:#f3e5f5,stroke:#7b1fa2,stroke-width:2px
    classDef outStyle fill:#e8f5e9,stroke:#388e3c,stroke-width:2px
    classDef techStyle fill:#fce4ec,stroke:#c2185b,stroke-width:2px
    
    class JSON,API inputStyle
    class JC ctrlStyle
    class JFS,Parse,Convert svcStyle
    class Entity,Response outStyle
    class SB,JD,JDK techStyle
```

## 🔄 核心流程

```mermaid
sequenceDiagram
    participant Client as 客户端
    participant Controller as JsonController
    participant Service as JsonFileService
    participant Jackson as Jackson解析器
    participant Entity as 实体对象

    Client->>Controller: 发送JSON数据
    Controller->>Service: 调用解析服务
    Service->>Jackson: 解析JSON
    Jackson-->>Service: 返回JsonNode
    Service->>Entity: 转换为实体对象
    Entity-->>Service: 实体实例
    Service-->>Controller: 返回结果
    Controller-->>Client: 响应数据
```
