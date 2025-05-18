# Minecraft Server Helm Chart

Helm Chart para deploy de um servidor Minecraft (Bedrock ou Java) em Kubernetes.

---

## Descrição

Este Helm Chart facilita a implantação de um servidor Minecraft dentro de um cluster Kubernetes, utilizando imagens oficiais da comunidade [itzg](https://hub.docker.com/u/itzg) para as versões Bedrock e Java do servidor.

---

## Funcionalidades

- Suporte para versões **Bedrock** e **Java** do Minecraft.
- Configuração customizável via Helm values.
- Persistência de dados com PersistentVolumeClaim.
- Configurações de recursos (CPU, memória, armazenamento) ajustáveis.
- Suporte à definição de parâmetros do servidor (gamemode, dificuldade, número máximo de jogadores, etc).
- Configuração automática de portas e volumes conforme a versão do servidor.

---

## Imagens usadas

- [itzg/minecraft-bedrock-server](https://hub.docker.com/r/itzg/minecraft-bedrock-server)
- [itzg/minecraft-server (Java edition)](https://hub.docker.com/r/itzg/minecraft-server)

---

## Documentação base

- [Docker Minecraft Server Docs](https://docker-minecraft-server.readthedocs.io/en/latest/)
- [Minecraft Server.properties (Bedrock Edition)](https://minecraft.fandom.com/wiki/Server.properties#Bedrock_Edition_3)

---

## Como usar

### Instalação

Clone este repositório e ajuste os valores no arquivo `values.yaml` para configurar seu servidor Minecraft.

```bash
helm install mc-server ./Minecraft-Server -f values.yaml
```

---

## Valores configuráveis (`values.yaml`)

```yaml
mcVersion: bedrock # "bedrock" ou "java"

server_config:
  SERVER_NAME: My-server
  SERVER_PORT: 19132 # 25565 para Java, 19132 para Bedrock
  GAMEMODE: creative # opções: survival, creative, adventure, spectator
  DIFFICULTY: peaceful # opções: peaceful, easy, normal, hard
  MAX_PLAYERS: 10
  ONLINE_MODE: True # Verifica jogadores no banco de dados oficial do Minecraft
  MOTD: "hello"

resources:
  cpu_max: "1000m"        # Limite de CPU
  mem_max: "1000Mi"       # Limite de memória
  storage_size: "1Gi"     # Tamanho do armazenamento persistente
  storage_path: "/data/mc-server-data"  # Path para armazenamento no container
```

---

## Estrutura do Chart

- **Deployment:** Cria o pod do servidor Minecraft com configuração adaptada para Bedrock ou Java.
- **ConfigMap:** Armazena as configurações do servidor (EULA, parâmetros do server.properties).
- **PVC:** PersistentVolumeClaim para armazenar dados persistentes do servidor.
- **Affinity:** Configuração para rodar o pod em nós workers.

---

## Observações

- Ajuste o parâmetro `mcVersion` para alternar entre as versões Bedrock e Java.
- Certifique-se que o cluster Kubernetes possua recursos suficientes para atender as configurações definidas.
- Para customizações avançadas, altere o `values.yaml` conforme necessário.

---

## Contato

Para dúvidas e contribuições, abra uma issue ou envie um pull request.
