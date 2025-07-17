# n8n

## Create Custom Node
- Clone ``` https://github.com/n8n-io/n8n-nodes-starter ```
```bash
npm i
npm run build
npm link
```
- Env Linking with n8n (Windows)
```js
setx N8N_CUSTOM_EXTENSIONS "C:\folder\n8n\n8n-nodes-starter"
```

## Run with Docker

```bash
docker exec -it n8n sh
docker stop n8n
docker rn n8n
docker logs n8n --tail 50

```
```bash
docker run -d \
  --name n8n \
  -p 5678:5678 \
  -e N8N_TRUST_PROXY=true
  -e WEBHOOK_URL=https://n8n.xyz.com \
  -v ~/.n8n:/home/node/.n8n \
  n8nio/n8n
```
## Make it to Production
- Include cert auto-renewal
```bash
sudo certbot --nginx -d n8n.xyz.com
```

- Configure nginx reverse proxy
```
server {
    listen 443 ssl;
    listen [::]:443 ssl;
    server_name n8n.xyz.com;

    location / {
        proxy_pass http://localhost:5678;

        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";

        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }

    ssl_certificate /etc/letsencrypt/live/n8n.xyz.com/fullchain.pem; # managed by Certbot
    ssl_certificate_key /etc/letsencrypt/live/n8n.xyz.com/privkey.pem; # managed by Certbot
}


server {

    if ($host = app.xyz.com) {
        return 301 https://$host$request_uri;
    } # managed by Certbot

    if ($host = n8n.xyz.com) {
        return 301 https://$host$request_uri;
    }

    listen 80 ;
    listen [::]:80 ;
    server_name app.xyz.com;
    return 404; # managed by Certbot
}
```

## Setup Gmail OAuth2 with n8n

#### 1. Create OAuth2 Credentials in Google Cloud Console
- Go to: [https://console.cloud.google.com](https://console.cloud.google.com)
- Create a new project
- Enable **Gmail API**
- Go to **APIs & Services** → **Credentials**
- Click **Create Credentials** → **OAuth 2.0 Client ID**

## Configure OAuth2 Client
- **Application Type**: Web Application
- **Authorized redirect URIs**:
  ```
  https://your-n8n-domain.com/oauth2-redirect
  ```

#### 2. Add Credentials in n8n
- Open your **n8n** instance
- Go to: `Credentials` → `Google OAuth2`
- Click **Create New**

## Input the following:
- **Client ID**: *(from Google Cloud Console)*
- **Client Secret**: *(from Google Cloud Console)*
- **Redirect URI**: 
  ```
  https://your-n8n-domain.com/oauth2-redirect
  ```
  Then, sign with gmail will pop-up.
