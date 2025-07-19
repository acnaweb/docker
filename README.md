
# 🐳 Tutorial: Aprendendo Docker na Prática

Este tutorial cobre os principais conceitos de imagens, containers, volumes, execução interativa, integração com Docker Hub e versionamento de imagens.

---

## 📦 1. Baixando uma Imagem Base

**Objetivo:** Obter uma imagem oficial do Ubuntu

```bash
docker pull ubuntu
```

> Isso faz o download da imagem `ubuntu` do Docker Hub, que será usada como base para nossos containers.

---

## 🔍 2. Verificando Imagens Locais

```bash
docker images
```

> Lista todas as imagens já baixadas no ambiente local.

---

## 🛠️ 3. Criando Imagens Personalizadas (Build)

**Objetivo:** Criar uma imagem chamada `devops` a partir de um `Dockerfile`.

```bash
docker build -t devops .
docker build -t devops:0.1.0 .
docker build -t devops:0.2.0 .
```

- `-t`: nomeia e marca a imagem
- `.`: indica que o `Dockerfile` está no diretório atual

> Usar *tags* (`:0.1.0`) ajuda no controle de versões da imagem.

---

## 🚀 4. Executando Containers

**A partir de imagem oficial:**

```bash
docker run ubuntu
```

**A partir da imagem personalizada:**

```bash
docker run devops:0.2.0
```

**Com terminal interativo:**

```bash
docker run -it ubuntu /bin/bash
```

- `-it`: abre terminal interativo
- `/bin/bash`: inicia o shell bash

---

## 🔄 5. Compartilhando Arquivos com o Container (Volumes)

**Montar o diretório atual no container:**

```bash
docker run -it -v .:/shared ubuntu /bin/bash
docker run -it -v .:/shared devops /bin/bash
```

- `-v .:/shared`: monta o diretório atual (`.`) no caminho `/shared` do container

---

## 📋 6. Listando Containers

```bash
docker ps -a     # Lista todos os containers (ativos ou não)
docker ps -qa    # Lista apenas os IDs de todos os containers
```

---

## 🧾 7. Visualizando Logs do Container

```bash
docker logs [ID]
```

> Substitua `[ID]` pelo ID real do container.

---

## 🗑️ 8. Removendo Containers

```bash
docker rm [ID]             # Remove um container parado
docker rm -f [ID]          # Força a remoção mesmo que esteja ativo
docker rm -f $(docker ps -qa)  # Remove todos os containers
```

> Use com cuidado! O último comando limpa tudo!

---

## 🧠 9. Acessando um Container Ativo

```bash
docker exec -it [ID] /bin/bash
```

> Permite "entrar" no container para debug ou administração.

---

## ☁️ 10. Publicando Imagens no Docker Hub

**Criar repositório no Docker Hub**  
Acesse [https://hub.docker.com](https://hub.docker.com) e crie um repositório público ou privado.

**Autenticar-se no Docker**

```bash
docker login
```

> Informe suas credenciais do Docker Hub.

**Tag e push da imagem**

```bash
docker tag devops:0.2.0 seu_usuario/devops:0.2.0
docker push seu_usuario/devops:0.2.0
```

> Substitua `seu_usuario` pelo seu nome de usuário no Docker Hub.

---

## ✅ Conclusão

Com essas etapas, você terá passado por:

| Etapa                    | Conceito Prático                      |
|-------------------------|----------------------------------------|
| `pull`                  | Baixar imagens do Docker Hub           |
| `build`                 | Criar imagem a partir de um Dockerfile |
| `run`                   | Executar containers                    |
| `-it`, `-v`             | Interação e compartilhamento           |
| `exec`, `logs`          | Acesso e depuração                     |
| `ps`, `rm`              | Gestão de containers                   |
| `tag`, `push`           | Versionamento e publicação             |


---

## 🧹 11. Limpando Recursos Não Utilizados

**Remover containers, imagens, volumes e redes não utilizados:**

```bash
docker system prune -a
docker system prune -a --volumes
```

- `-a`: remove *tudo* que não está em uso (containers, imagens, redes)
- `--volumes`: inclui volumes não utilizados

> ⚠️ Atenção: esses comandos removem recursos de forma agressiva. Use com cautela!
