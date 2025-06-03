1. React 用户登录 → Cognito 返回 JWT Token
2. React 发 API 请求 → 请求头带上 Authorization: Bearer xxx
3. API Gateway 验证这个 Token（通过 Cognito Authorizer）
4. 验证通过 → 请求转发给 Lambda
5. Lambda 返回数据给前端
