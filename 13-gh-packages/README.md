# Laboratório Prático: Publicando Imagens Docker no GitHub Packages

## Visão Geral

Neste laboratório você vai aprender como usar o **GitHub Packages** como um **registro de imagens Docker** privado ou público

Você vai:
- Criar uma imagem Docker simples
- Fazer login no registro do GitHub
- Publicar a imagem usando GitHub Packages
- Verificar a imagem no portal

## Pré-requisitos

- Conta no GitHub
- Docker instalado na máquina local
- GitHub CLI ou token com escopo `write:packages` e `read:packages`

---

## Passo 1: Criar um repositório no GitHub

1. Acesse [https://github.com](https://github.com)
2. Clique em **New repository**
3. Nomeie como `docker-lab`
4. Marque como **Public** ou **Private** (depende do uso)
5. Clique em **Create repository**

---

## Passo 2: Criar o Dockerfile local

```Dockerfile
# Dockerfile
FROM alpine
CMD ["echo", "Hello from GitHub Packages"]
```

Salve esse arquivo com o nome `Dockerfile`

---

## Passo 3: Criar o arquivo `.dockerignore` (opcional)

```bash
.git
README.md
```

---

## Passo 4: Fazer login no GitHub Packages

```bash
echo "<TOKEN>" | docker login ghcr.io -u iesodias --password-stdin
```

> Dica: você pode gerar um token em https://github.com/settings/tokens com escopos `write:packages`, `read:packages`, `delete:packages`

---

## Passo 5: Criar o nome da imagem com escopo GitHub

```bash
docker build -t ghcr.io/iesodias/docker-lab:1.0.0 .
```

---

## Passo 6: Publicar a imagem no GitHub Packages

```bash
docker push ghcr.io/iesodias/docker-lab:1.0.0
```

---

## Passo 7: Visualizar a imagem no Portal do GitHub

1. Vá para o repositório `docker-lab`
2. Clique na aba **Packages** (do lado direito ou abaixo do título)
3. Clique no nome da imagem Docker publicada
4. Você verá:
   - O nome e tag da imagem
   - Comandos de instalação (pull)
   - Visibilidade e permissões

---

## Passo 8: Testar a imagem

Você pode baixar e testar a imagem com:

```bash
docker pull ghcr.io/iesodias/docker-lab:1.0.0
docker run ghcr.io/iesodias/docker-lab:1.0.0
```

---

## Observações

- O GitHub usa o domínio `ghcr.io` para GitHub Container Registry
- Imagens privadas só podem ser acessadas com autenticação
- É possível usar GitHub Actions para publicar automaticamente em `ghcr.io`




