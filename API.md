openacc api 协议
---------

# 常规接口

## 授权

### 用户名/密码登录

请求包：

```
POST /v1/users/token
Content-Type: application/x-www-form-urlencoded

grant_type=password&
client_id=<ClientAppId>&
device_id=<DeviceId>&
username=<UserName>& (或者email=<Email> 或者 uid=<UserId> 三选一）
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
POST /v1/users/token
Content-Type: application/x-www-form-urlencoded

grant_type=refresh_token&
client_id=<ClientAppId>&
device_id=<DeviceId>&
refresh_token=<RefreshToken>&
scope=<Scope>
```

返回包同 "用户名/密码登录"。


# 管理员接口

## 创建账号

请求包：

```
POST /v1/users
Content-Type: application/x-www-form-urlencoded
Authorization: Qiniu <AdminToken>

username=<UserName>&
password=<Password>&
email=<Email>&
email_verified=<IsEmailVerified>
```

返回包：

```
200 OK
Content-Type: application/json

{
  "id": <UserId>
}
```

## 重置密码

请求包：

```
POST /v1/users/forget/password
Authorization: Qiniu <AdminToken>

username=<UserName>& (或者email=<Email> 或者 uid=<UserId> 三选一）
password=<Password>
```

返回包：

```
200 OK
```

## 激活邮箱/重置邮箱

请求包：

```
POST /v1/users/email
Authorization: Qiniu <AdminToken>

username=<UserName>& (或者email=<Email> 或者 uid=<UserId> 三选一）
new_email=<NewEmail>&
email_verified=<IsEmailVerified>
```

返回包：

```
200 OK
```

## 冻结/取消冻结用户

请求包：

```
POST /v1/users/enable
Authorization: Qiniu <AdminToken>

username=<UserName>& (或者email=<Email> 或者 uid=<UserId> 三选一）
val=<Enabled>
```

返回包：

```
200 OK
```

## 查询用户

请求包：

```
GET /v1/users/info?username=<UserName>& (或者email=<Email> 或者 uid=<UserId> 三选一）
Authorization: Qiniu <AdminToken>
```

返回包：

```
200 OK
```
