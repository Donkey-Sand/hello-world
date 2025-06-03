# React + AWS Cognito 项目完整会话记录

## 🗣️ 会话概览

### 会话摘要

**Jo:** 一个react写的前端程序，迁移到aws上，如何处理？  
**GPT:** 给出 S3 + CloudFront / Amplify / EC2 三种方案和详细步骤对比。

**Jo:** 需要后端，使用Python而写的，也要一起迁移  
**GPT:** 推荐 React 前端部署到 S3 + 后端使用 Lambda + API Gateway，列出详细架构和部署方式对比。

**Jo:** 初步定下了Lambda + API Gateway  
**GPT:** 展开介绍 Lambda 架构部署与 Serverless 配置方式。

**Jo:** 设置登录机制，使用 Cognito  
**GPT:** 说明 Cognito User Pool、JWT Token 认证流程与 React/Amplify 配合方式。


## 🖼️ 身份验证流程图

![Cognito Authentication Flow](./react_cognito_auth_flow.png)



---

## 💡 GPT 回答内容概要（含代码）

### React 前端部署方式（摘要）
- 使用 `npm run build` 生成静态资源
- 推荐部署方式：S3 + CloudFront 或 AWS Amplify Hosting
- 若有 API 后端，则使用 Lambda + API Gateway

### 后端部署（Python FastAPI + Lambda）
- 使用 Serverless Framework 部署 FastAPI 到 AWS Lambda
- 使用 API Gateway 接收请求，并通过 JWT 验证（Cognito Authorizer）

- 1. React 用户登录 → Cognito 返回 JWT Token
2. React 发 API 请求 → 请求头带上 Authorization: Bearer xxx
3. API Gateway 验证这个 Token（通过 Cognito Authorizer）
4. 验证通过 → 请求转发给 Lambda
5. Lambda 返回数据给前端

### 用户登录注册流程
- 使用 AWS Amplify 集成 Cognito 登录注册
- 注册后需邮箱验证码验证（可选）
- 登录后返回 JWT Token
- 前端调用 API 时在 header 中附上 Authorization: Bearer <JWT>

### 示例代码模块
- `Register.js`: 用户注册
- `Confirm.js`: 验证邮箱验证码
- `Login.js`: 登录并保存 Token
- `ProtectedAPI.js`: 使用 JWT Token 调用受保护的 API
- `App.js`: 整合以上组件
- `aws-exports.js`: Cognito 配置信息



> 📁 本文档可在 VS Code、Notion、Obsidian 等工具中查看，配合图片查看整体架构。
