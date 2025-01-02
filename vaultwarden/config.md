## Configuracao inicial

```sh
sudo apt-get update
```

### Instalando o `curl`:

```sh
sudo apt-get install ca-certificates curl
```

### Instalando o  `Docker`:

```sh
sudo install -m 0755 -d /etc/apt/keyrings
```

```sh
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
```

```sh
sudo chmod a+r /etc/apt/keyrings/docker.asc
```

```sh
# Add the repository to Apt sources:
    8  echo   "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
    9    $(. /etc/os-release && echo "$VERSION_CODENAME") stable" |   sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

```sh
sudo apt-get update
```

### Instalando o `Docker-compose`

```sh
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

### Docker/CLI

Obtendo a ultima Imagem do Vaultwarden

```sh
docker pull vaultwarden/server:latest
```

Criando o container do `vaultwarden`

```sh
docker run --detach --name vaultwarden   --env DOMAIN="https://YOUR_DOMAIN"   --volume /vw-data/:/data/   --restart unless-stopped   --publish 80:80   vaultwarden/server:latest
```

### Docker Compose

Criando a partir do 'compose.yaml'

```yaml
services:
  vaultwarden:
    image: vaultwarden/server:latest
    container_name: vaultwarden
    restart: unless-stopped
    environment:
      DOMAIN: "https://vw.domain.tld"
    volumes:
      - ./vw-data/:/data/
    ports:
      - 80:80
```



```sh
sudo docker compose up -d
```