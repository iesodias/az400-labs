# Laboratório Prático: Estratégia de Versionamento com Git e GitHub

## Visão Geral

Neste laboratório você vai aprender como aplicar uma estratégia de versionamento em projetos utilizando Git e GitHub

Você vai entender como usar **branches**, **commits semânticos** e **tags** para controlar versões de forma profissional

## Pré-requisitos

- Git instalado (https://git-scm.com)
- Conta no GitHub
- Repositório criado (pode ser vazio ou com README)

---

## Passo 1: Clonar o repositório

```bash
git clone https://github.com/seu-usuario/seu-repositorio.git
cd seu-repositorio
```

---

## Passo 2: Criar a branch de desenvolvimento principal

```bash
git checkout -b develop
```

A branch `develop` será usada para desenvolver novas funcionalidades

---

## Passo 3: Criar uma branch para uma nova feature

```bash
git checkout -b feat/adicionar-api
```

Prefixos recomendados:
- `feat/` = nova funcionalidade
- `fix/` = correção de bug
- `docs/` = documentação
- `refactor/` = refatoração

---

## Passo 4: Fazer alterações e commitar com mensagem semântica

```bash
echo "console.log('API funcionando')" > api.js
git add api.js
git commit -m "feat: adiciona endpoint inicial da API"
```

---

## Passo 5: Fazer merge na branch develop

```bash
git checkout develop
git merge feat/adicionar-api
```

---

## Passo 6: Criar uma tag de versão

```bash
git tag v1.0.0
git push origin v1.0.0
```

Regras comuns para versionamento semântico:
- `vMAJOR.MINOR.PATCH`
- Exemplo: `v1.2.0`, `v2.0.0`

---

## Passo 7: Criar release no GitHub (opcional)

1. Vá até o repositório no GitHub
2. Clique em **Releases** > **Draft a new release**
3. Escolha a tag `v1.0.0`
4. Adicione título e descrição
5. Clique em **Publish release**

---

## Passo 8: Histórico de versões

Para listar todas as tags (versões):

```bash
git tag
```

Para ver o log de commits desde uma versão:

```bash
git log v1.0.0..
```

---

## Passo 9: Corrigir um bug e criar nova versão

```bash
git checkout -b fix/ajuste-api
# corrige o código
 git add .
 git commit -m "fix: corrige bug no retorno da API"
 git checkout develop
 git merge fix/ajuste-api
 git tag v1.0.1
 git push origin v1.0.1
```

---

## Passo 10: Limpar branches locais (opcional)

```bash
git branch -d feat/adicionar-api
git branch -d fix/ajuste-api
```

---