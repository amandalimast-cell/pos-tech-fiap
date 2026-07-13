# Guia rápido de Git para a Pós-Tech FIAP

Este arquivo serve como lembrete dos comandos básicos para:

- enviar minhas alterações para o meu GitHub;
- receber atualizações do repositório original da professora;
- entender quando usar Pull Request.

---

## 1. Como estão configurados os repositórios

No meu projeto:

```text
origin   = meu repositório no GitHub
upstream = repositório original da professora
```

Para conferir:

```bash
git remote -v
```

Resultado esperado:

```text
origin    https://github.com/amandalimast-cell/POSTECH_AI_SCIENTIST.git (fetch)
origin    https://github.com/amandalimast-cell/POSTECH_AI_SCIENTIST.git (push)
upstream  https://github.com/AnaRaquelCafe/POSTECH_AI_SCIENTIST.git (fetch)
upstream  https://github.com/AnaRaquelCafe/POSTECH_AI_SCIENTIST.git (push)
```

---

## 2. Enviar minhas alterações para o meu GitHub

Depois de criar ou alterar arquivos:

### Ver o que foi alterado

```bash
git status
```

### Adicionar os arquivos para o próximo commit

Para adicionar tudo:

```bash
git add .
```

Ou para adicionar somente um arquivo:

```bash
git add nome-do-arquivo.ipynb
```

### Criar o commit

```bash
git commit -m "Adiciona exercícios de análise exploratória"
```

A mensagem deve explicar de forma simples o que foi feito.

### Enviar para o meu GitHub

```bash
git push origin main
```

Na primeira vez, posso usar:

```bash
git push -u origin main
```

O `-u` faz o Git lembrar que a branch local `main` está ligada à `origin/main`.

### Fluxo completo

```bash
git status
git add .
git commit -m "Descrição da alteração"
git push origin main
```

---

## 3. Receber atualizações da professora

Antes de atualizar, é recomendado verificar se tenho alterações locais:

```bash
git status
```

Se houver alterações importantes, devo fazer commit antes.

### Buscar e incorporar as atualizações

```bash
git pull upstream main
```

Esse comando baixa as alterações do repositório da professora e tenta incorporá-las à minha branch atual.

Depois, para manter meu GitHub atualizado:

```bash
git push origin main
```

### Fluxo completo

```bash
git status
git pull upstream main
git push origin main
```

---

## 4. Alternativa mais controlada para atualizar

Em vez de usar `git pull` diretamente, posso separar em duas etapas.

### Buscar as atualizações

```bash
git fetch upstream
```

### Incorporar na minha branch

```bash
git merge upstream/main
```

Depois:

```bash
git push origin main
```

Fluxo:

```bash
git fetch upstream
git merge upstream/main
git push origin main
```

---

## 5. Quando usar Pull Request

Pull Request, ou PR, serve para propor que alterações de uma branch ou repositório sejam incorporadas em outro.

### Não preciso de Pull Request para:

- salvar alterações no meu próprio GitHub;
- criar commits;
- fazer push para o meu fork;
- manter meu repositório pessoal atualizado.

Para isso, basta:

```bash
git add .
git commit -m "Descrição"
git push origin main
```

### Preciso de Pull Request quando:

- quero sugerir uma alteração para o repositório original da professora;
- quero juntar uma branch de trabalho na branch `main`;
- estou colaborando com outras pessoas em um projeto.

Exemplo:

```text
Minha branch ou meu fork
        ↓
Pull Request
        ↓
Repositório ou branch de destino
```

O Pull Request normalmente é aberto pelo site do GitHub.

---

## 6. Exemplo usando uma branch

Criar uma branch para um exercício:

```bash
git checkout -b exercicio-idhm
```

Depois de trabalhar:

```bash
git add .
git commit -m "Adiciona análise do IDHM"
git push -u origin exercicio-idhm
```

Depois posso abrir um Pull Request no GitHub para juntar:

```text
exercicio-idhm → main
```

Isso é útil para praticar um fluxo mais próximo do mercado.

---

## 7. Resumo rápido

### Enviar alterações para o meu GitHub

```bash
git status
git add .
git commit -m "Descrição da alteração"
git push origin main
```

### Receber atualizações da professora

```bash
git pull upstream main
git push origin main
```

### Conferir os repositórios configurados

```bash
git remote -v
```

### Criar uma nova branch

```bash
git checkout -b nome-da-branch
```

### Trocar de branch

```bash
git checkout main
```

---

## 8. Cuidados importantes

- `git pull` baixa atualizações.
- `git push` envia alterações.
- `git commit` registra uma versão local.
- `git add` seleciona o que entrará no commit.
- `git status` mostra o estado atual do projeto.
- Evitar alterar diretamente os arquivos originais da professora quando possível.
- Preferir criar arquivos ou pastas próprias para exercícios.
- Fazer commits pequenos e com mensagens claras.
