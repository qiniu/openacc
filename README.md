openacc
=======

提供账号认证、授权等相关的服务。
账号服务本身逻辑不复杂，难在如何与业务解耦（以便在扩展新业务可共享账号系统），如何做到安全、做到高性能。

# 协议

## 授权

### 用户名/密码登录

请求包：

```
POST /oauth2/token
Content-Type: application/x-www-form-urlencoded

grant_type=password&
client_id=<ClientAppId>&
device_id=<DeviceId>&
username=<User>&
password=<Password>&
scope=<Scope>
```

返回包：

```
200 OK
Content-Type: application/json

{
  access_token: <AccessToken>
  token_type: <TokenType> #目前只有bearer
  expires_in: <ExpireSconds>
  refresh_token: <RefreshToken>
}
```

### RefreshToken续约

请求包：

```
POST /oauth2/token
Content-Type: application/x-www-form-urlencoded

grant_type=refresh_token&
client_id=<ClientAppId>&
device_id=<DeviceId>&
refresh_token=<RefreshToken>&
scope=<Scope>
```

返回包同 "用户名/密码登录"。

## 创建账号

请求包：

```
POST /v1/users
Content-Type: application/x-www-form-urlencoded
Authorization: Qiniu <AdminToken>

username=<User>&
password=<Password>&
email=<Email>&
email_verified=<IsEmailVerified>
```

* 这是管理员 api。
* 用户名（username）和邮箱（email）都是 unique key，都可以用于登陆。

返回包：

```
200 OK
Content-Type: application/json

{
  "id": <UserId>
}
```
