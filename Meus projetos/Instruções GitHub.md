# Guia de Git e GitHub — Pós-Tech FIAP

Este guia explica como ficou organizada a estrutura dos estudos, como enviar alterações para o meu GitHub, como atualizar o material da professora e quando usar Pull Request.

---

# 1. Estrutura do projeto

A estrutura ficou assim:

```text
pos-tech-fiap-amanda/
├── .git
├── readme.md
├── Meus projetos/
│   └── Instruções GitHub.md
└── POSTECH_AI_SCIENTIST/
```

## O que cada parte significa

### `pos-tech-fiap-amanda`

É o meu repositório principal.

Tudo o que estiver dentro dessa pasta pode ser controlado pelo Git principal, exceto conteúdos de submódulos, que possuem um controle separado.

### `.git`

É uma pasta oculta criada pelo Git.

Ela guarda:

- histórico de commits;
- branches;
- configurações do repositório;
- endereço do GitHub;
- informações sobre arquivos alterados.

A pasta que contém o `.git` é considerada a raiz do repositório.

Por isso, os comandos do Git principal devem ser executados dentro de:

```text
C:\Users\amand\Documents\pos-tech-fiap-amanda
```

ou em alguma subpasta dela, desde que não esteja dentro de outro repositório Git.

### `Meus projetos`

É a pasta destinada aos meus próprios arquivos, exercícios, notebooks e projetos da pós.

Exemplo:

```text
Meus projetos/
├── fase-1/
├── notebooks/
├── dados/
└── Instruções GitHub.md
```

### `POSTECH_AI_SCIENTIST`

É o material complementar da professora.

Essa pasta foi adicionada como um **submódulo Git**.

Isso significa que ela continua conectada ao repositório original da professora, mas aparece dentro do meu repositório principal.

---

# 2. O que é um repositório Git

Um repositório Git é uma pasta acompanhada pelo Git.

O Git registra:

- arquivos novos;
- arquivos alterados;
- arquivos excluídos;
- histórico de versões;
- branches;
- commits.

Para verificar se estou dentro de um repositório:

```bash
git status
```

Se aparecer:

```text
fatal: not a git repository
```

significa que o terminal está em uma pasta que não contém `.git` e também não está dentro de uma pasta controlada pelo Git.

---

# 3. Repositório principal e submódulo

Neste projeto existem dois repositórios Git.

## Repositório principal

Local:

```text
pos-tech-fiap-amanda
```

Remoto:

```text
https://github.com/amandalimast-cell/pos-tech-fiap.git
```

Função:

- armazenar meus projetos;
- armazenar meus arquivos de estudo;
- registrar a referência do material da professora;
- enviar minhas alterações para o meu GitHub.

## Submódulo

Local:

```text
pos-tech-fiap-amanda/POSTECH_AI_SCIENTIST
```

Remoto:

```text
https://github.com/AnaRaquelCafe/POSTECH_AI_SCIENTIST.git
```

Função:

- manter o material original da professora separado;
- receber atualizações do repositório original;
- evitar misturar o histórico da professora com o meu histórico.

---

# 4. O que significa `origin`

`origin` é o apelido padrão dado ao repositório remoto principal.

No meu repositório principal:

```text
origin = meu GitHub
```

Para conferir:

```bash
git remote -v
```

Resultado esperado na pasta principal:

```text
origin  https://github.com/amandalimast-cell/pos-tech-fiap.git (fetch)
origin  https://github.com/amandalimast-cell/pos-tech-fiap.git (push)
```

## `fetch`

É o endereço usado para baixar informações do GitHub.

## `push`

É o endereço usado para enviar commits ao GitHub.

As duas linhas não representam dois repositórios. São apenas duas funções diferentes do mesmo remoto.

---

# 5. Por que não existe `upstream` na pasta principal

Neste projeto, o material da professora foi adicionado como submódulo.

Por isso, a pasta principal precisa apenas do meu `origin`.

```text
pos-tech-fiap-amanda
└── origin = meu GitHub
```

Já dentro do submódulo:

```text
POSTECH_AI_SCIENTIST
└── origin = GitHub da professora
```

Para conferir o remoto da professora:

```powershell
cd .\POSTECH_AI_SCIENTIST
git remote -v
```

Resultado esperado:

```text
origin  https://github.com/AnaRaquelCafe/POSTECH_AI_SCIENTIST.git (fetch)
origin  https://github.com/AnaRaquelCafe/POSTECH_AI_SCIENTIST.git (push)
```

Depois, para voltar ao repositório principal:

```powershell
cd ..
```

---

# 6. O que é um submódulo

Um submódulo é um repositório Git dentro de outro repositório Git.

O repositório principal não salva todos os arquivos internos do submódulo diretamente.

Ele salva uma referência para um commit específico do submódulo.

Exemplo:

```text
Meu repositório
└── registra que o material da professora está no commit ABC123
```

Quando o material da professora for atualizado, o submódulo passa para outro commit.

Depois, o repositório principal precisa registrar essa nova referência.

## Arquivo `.gitmodules`

Quando o submódulo foi criado, o Git adicionou:

```text
.gitmodules
```

Esse arquivo guarda:

- nome do submódulo;
- caminho local;
- URL do repositório original.

Exemplo aproximado:

```ini
[submodule "POSTECH_AI_SCIENTIST"]
    path = POSTECH_AI_SCIENTIST
    url = https://github.com/AnaRaquelCafe/POSTECH_AI_SCIENTIST.git
```

---

# 7. Comando `git status`

O comando:

```bash
git status
```

mostra o estado atual do repositório.

Ele informa:

- branch atual;
- arquivos alterados;
- arquivos novos;
- arquivos excluídos;
- arquivos preparados para commit;
- situação em relação ao GitHub.

---

# 8. O que significa `Untracked files`

Exemplo:

```text
Untracked files:
    Meus projetos/
```

Significa que o Git encontrou arquivos novos que ainda não foram adicionados ao controle de versão.

Esses arquivos existem no computador, mas ainda não fazem parte de nenhum commit.

Para começar a acompanhá-los:

```bash
git add .
```

Ou apenas um arquivo específico:

```bash
git add "Meus projetos/Instruções GitHub.md"
```

## Pastas vazias

O Git não controla pastas vazias.

Uma pasta só aparece no Git quando contém pelo menos um arquivo.

---

# 9. O que significa `Changes not staged for commit`

Exemplo:

```text
Changes not staged for commit:
    modified: arquivo.ipynb
    deleted: readme.md
```

Significa que um arquivo já acompanhado pelo Git foi alterado ou excluído, mas ainda não foi preparado para commit.

Para adicionar a alteração:

```bash
git add arquivo.ipynb
```

Para adicionar todas:

```bash
git add .
```

Para desfazer uma alteração em um arquivo:

```bash
git restore nome-do-arquivo
```

Exemplo:

```bash
git restore readme.md
```

Isso restaura o arquivo para a última versão registrada.

---

# 10. O que significa `Changes to be committed`

Exemplo:

```text
Changes to be committed:
    new file: .gitmodules
    new file: POSTECH_AI_SCIENTIST
```

Significa que os arquivos já passaram pelo `git add`.

Eles estão na área de preparação, chamada de **staging area**.

Agora estão prontos para entrar no próximo commit.

---

# 11. Comando `git add`

O comando `git add` seleciona alterações para o próximo commit.

## Adicionar tudo

```bash
git add .
```

O ponto significa:

```text
todas as alterações da pasta atual e suas subpastas
```

## Adicionar apenas um arquivo

```bash
git add nome-do-arquivo.md
```

## Adicionar uma pasta

```bash
git add "Meus projetos"
```

## Importante

`git add` não envia nada ao GitHub.

Ele apenas prepara arquivos para o próximo commit.

---

# 12. Comando `git commit`

O commit cria um registro local das alterações.

Exemplo:

```bash
git commit -m "Organiza estrutura de estudos"
```

## Função do `-m`

O parâmetro `-m` significa mensagem.

Por isso, deve sempre ser acompanhado de um texto:

```bash
git commit -m "Descrição do que foi feito"
```

Este comando está incompleto:

```bash
git commit -m
```

Ele gera erro porque falta a mensagem.

## Boas mensagens de commit

```text
Adiciona exercícios de análise exploratória
Atualiza material complementar da FIAP
Corrige leitura do arquivo de IDHM
Organiza notebooks da fase 1
```

A mensagem deve ser curta e explicar o que foi alterado.

---

# 13. Comando `git push`

O comando `git push` envia commits locais para o GitHub.

Exemplo:

```bash
git push
```

Também pode ser escrito de forma explícita:

```bash
git push origin feat/initial-config
```

Isso significa:

```text
enviar a branch feat/initial-config para o remoto origin
```

## Primeira vez em uma branch

Pode ser necessário usar:

```bash
git push -u origin feat/initial-config
```

O `-u` conecta a branch local à branch remota.

Depois disso, normalmente basta:

```bash
git push
```

---

# 14. Fluxo para enviar minhas alterações ao GitHub

Dentro da pasta principal:

```powershell
cd C:\Users\amand\Documents\pos-tech-fiap-amanda
```

Depois:

```bash
git status
git add .
git commit -m "Descrição da alteração"
git push
```

## Função de cada etapa

```text
git status
```

Mostra o que mudou.

```text
git add .
```

Seleciona as alterações.

```text
git commit
```

Registra uma versão local.

```text
git push
```

Envia o commit ao GitHub.

---

# 15. Branch atual

No momento, a branch usada é:

```text
feat/initial-config
```

Para verificar:

```bash
git branch
```

A branch atual aparece com `*`.

Exemplo:

```text
* feat/initial-config
  main
```

Também aparece no `git status`:

```text
On branch feat/initial-config
```

---

# 16. O que é uma branch

Uma branch é uma linha separada de desenvolvimento.

Ela permite fazer alterações sem mexer imediatamente na branch principal.

Exemplo:

```text
main
└── versão principal

feat/initial-config
└── organização inicial do projeto
```

## Criar uma branch

Forma moderna:

```bash
git switch -c nome-da-branch
```

Exemplo:

```bash
git switch -c feat/analise-idhm
```

Forma antiga, ainda muito usada:

```bash
git checkout -b feat/analise-idhm
```

## Trocar para uma branch existente

```bash
git switch main
```

Ou:

```bash
git checkout main
```

---

# 17. Quando usar Pull Request

Pull Request, ou PR, é uma solicitação para juntar alterações de uma branch em outra.

Exemplo:

```text
feat/initial-config
        ↓
   Pull Request
        ↓
       main
```

## Não preciso de Pull Request para

- salvar commits localmente;
- enviar minha branch ao meu GitHub;
- atualizar arquivos dentro da mesma branch;
- usar `git push`.

## Preciso de Pull Request quando

- quero juntar uma branch de trabalho na `main`;
- quero revisar alterações antes de incorporá-las;
- estou trabalhando com outras pessoas;
- quero propor uma alteração em outro repositório.

No meu caso, depois de enviar:

```bash
git push
```

posso abrir no GitHub um Pull Request:

```text
feat/initial-config → main
```

---

# 18. Atualizar o material da professora

O material da professora fica dentro do submódulo.

## Etapa 1: entrar no submódulo

```powershell
cd C:\Users\amand\Documents\pos-tech-fiap-amanda\POSTECH_AI_SCIENTIST
```

Ou, a partir da pasta principal:

```powershell
cd .\POSTECH_AI_SCIENTIST
```

## Etapa 2: verificar alterações locais

```bash
git status
```

É importante evitar alterações locais nos arquivos originais da professora.

## Etapa 3: baixar atualizações

```bash
git pull origin main
```

Isso atualiza a cópia local do material da professora.

## Etapa 4: voltar ao repositório principal

```powershell
cd ..
```

## Etapa 5: registrar a nova versão do submódulo

```bash
git status
git add POSTECH_AI_SCIENTIST
git commit -m "Atualiza material complementar da FIAP"
git push
```

## Por que precisa fazer commit na pasta principal

O submódulo pode ter mudado para um commit novo.

O repositório principal precisa registrar qual nova versão do material está sendo usada.

---

# 19. Fluxo completo para atualizar a professora

```powershell
cd C:\Users\amand\Documents\pos-tech-fiap-amanda\POSTECH_AI_SCIENTIST
git status
git pull origin main
cd ..
git status
git add POSTECH_AI_SCIENTIST
git commit -m "Atualiza material complementar da FIAP"
git push
```

---

# 20. Aviso `LF will be replaced by CRLF`

Exemplo:

```text
warning: LF will be replaced by CRLF
```

Isso não é erro.

É um aviso sobre quebra de linha em arquivos de texto.

## LF

Formato normalmente usado em Linux e macOS.

## CRLF

Formato normalmente usado no Windows.

O Git informa que poderá adaptar as quebras de linha ao sistema Windows.

Na maioria dos casos, posso ignorar esse aviso.

---

# 21. Clonar este projeto futuramente

Como o projeto contém submódulo, o ideal é clonar usando:

```bash
git clone --recurse-submodules https://github.com/amandalimast-cell/pos-tech-fiap.git
```

Isso baixa:

- meu repositório;
- o submódulo da professora.

## Caso o projeto já tenha sido clonado sem o submódulo

Usar:

```bash
git submodule update --init --recursive
```

---

# 22. Atualizar todos os submódulos

Também existe o comando:

```bash
git submodule update --remote
```

Ele busca a versão remota configurada do submódulo.

Depois, ainda é necessário registrar a mudança no projeto principal:

```bash
git add POSTECH_AI_SCIENTIST
git commit -m "Atualiza material complementar da FIAP"
git push
```

Para estudos, o fluxo manual entrando na pasta do submódulo costuma ser mais fácil de entender.

---

# 23. Cuidados com o submódulo

Evitar criar meus próprios exercícios dentro de:

```text
POSTECH_AI_SCIENTIST
```

Essa pasta deve ser usada principalmente como material de consulta.

Meus arquivos devem ficar em:

```text
Meus projetos
```

Isso reduz o risco de conflitos quando o material da professora for atualizado.

---

# 24. Comandos mais usados

## Ver o estado do repositório

```bash
git status
```

## Ver os remotos

```bash
git remote -v
```

## Ver branches

```bash
git branch
```

## Adicionar todas as alterações

```bash
git add .
```

## Criar commit

```bash
git commit -m "Descrição"
```

## Enviar para o GitHub

```bash
git push
```

## Baixar alterações do remoto

```bash
git pull
```

## Restaurar um arquivo

```bash
git restore nome-do-arquivo
```

## Criar uma branch

```bash
git switch -c nome-da-branch
```

## Trocar de branch

```bash
git switch nome-da-branch
```

---

# 25. Resumo dos fluxos

## Enviar meus projetos

Na pasta principal:

```bash
git status
git add .
git commit -m "Descrição da alteração"
git push
```

## Atualizar o material da professora

```bash
cd POSTECH_AI_SCIENTIST
git pull origin main
cd ..
git add POSTECH_AI_SCIENTIST
git commit -m "Atualiza material complementar da FIAP"
git push
```

## Levar uma branch para a `main`

```text
1. Fazer alterações na branch
2. git add .
3. git commit
4. git push
5. Abrir Pull Request no GitHub
6. Revisar
7. Fazer merge na main
```

---

# 26. Mapa mental

```text
ARQUIVOS NO COMPUTADOR
        ↓ git add
STAGING AREA
        ↓ git commit
HISTÓRICO LOCAL
        ↓ git push
GITHUB
```

Para receber alterações:

```text
GITHUB
   ↓ git pull
COMPUTADOR
```

No caso do material da professora:

```text
GitHub da professora
        ↓ git pull dentro do submódulo
POSTECH_AI_SCIENTIST
        ↓ commit da nova referência
Meu repositório principal
        ↓ git push
Meu GitHub
```
