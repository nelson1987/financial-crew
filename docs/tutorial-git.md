# Tutorial: Git para Iniciantes

Este tutorial apresenta o Git de forma didática para quem está começando no mundo da engenharia de software.

## 📖 O que é Git?

**Git** é um sistema de controle de versão distribuído. Em termos simples, é uma ferramenta que permite:

- **Salvar o histórico** de mudanças nos seus arquivos
- **Trabalhar em equipe** sem perder código
- **Voltar no tempo** se algo der errado
- **Criar versões** diferentes do seu projeto (branches)
- **Sincronizar código** entre diferentes computadores

### Analogia Simples

Imagine o Git como uma **máquina do tempo** para seus arquivos:
- Você pode salvar "fotos" (commits) do seu projeto em diferentes momentos
- Se algo der errado, você volta para uma "foto" anterior
- Você pode trabalhar em diferentes "realidades" (branches) ao mesmo tempo
- Outras pessoas podem ver e usar suas "fotos" (repositórios remotos)

---

## 🚀 Instalação do Git no Windows

### Método 1: Instalação via Site Oficial (Recomendado)

#### Passo 1: Baixar o Git

1. Acesse: [https://git-scm.com/download/win](https://git-scm.com/download/win)
2. O download começará automaticamente
3. Aguarde o download do arquivo `.exe` (aproximadamente 50MB)

#### Passo 2: Executar o Instalador

1. Execute o arquivo baixado (ex: `Git-2.xx.x-64-bit.exe`)
2. Clique em **"Next"** na tela de boas-vindas

#### Passo 3: Escolher Componentes

**Recomendado para iniciantes:**
- ✅ Git Bash Here
- ✅ Git GUI Here
- ✅ Associate .git* configuration files with the default text editor
- ✅ Associate .sh files to be run with Bash

Clique em **"Next"**.

#### Passo 4: Escolher Editor Padrão

**Para iniciantes, recomendo:**
- **Nano** (mais simples) ou
- **Notepad++** (se já tiver instalado) ou
- **Visual Studio Code** (se já tiver instalado)

Clique em **"Next"**.

#### Passo 5: Ajustar PATH

**Recomendado:** Deixe a opção padrão selecionada:
- ✅ "Git from the command line and also from 3rd-party software"

Clique em **"Next"**.

#### Passo 6: Escolher HTTPS

**Recomendado:** Deixe a opção padrão:
- ✅ "Use the OpenSSL library"

Clique em **"Next"**.

#### Passo 7: Configurar Line Endings

**Recomendado para Windows:**
- ✅ "Checkout Windows-style, commit Unix-style line endings"

Isso evita problemas ao trabalhar com pessoas que usam Linux/Mac.

Clique em **"Next"**.

#### Passo 8: Terminal Emulator

**Recomendado:**
- ✅ "Use MinTTY (the default terminal of MSYS2)"

Clique em **"Next"**.

#### Passo 9: Opções Extras

Deixe as opções padrão marcadas:
- ✅ Default (fast-forward or merge)
- ✅ Git Credential Manager
- ✅ Enable file system caching

Clique em **"Install"**.

#### Passo 10: Aguardar Instalação

Aguarde alguns minutos enquanto o Git é instalado.

#### Passo 11: Finalizar

Clique em **"Finish"**.

### ⚠️ Problema: Git não é reconhecido após instalação

**Erro:**
```
'git' não é reconhecido como um comando interno ou externo
```

**Solução:**
1. Feche e reabra o terminal/PowerShell
2. Se ainda não funcionar, reinicie o computador
3. Verifique se o Git foi instalado corretamente:
   - Abra o PowerShell
   - Digite: `git --version`
   - Deve mostrar algo como: `git version 2.xx.x`

### Método 2: Instalação via Winget (Windows 11)

Se você tem Windows 11, pode instalar via linha de comando:

```powershell
winget install --id Git.Git -e --source winget
```

### Método 3: Instalação via Chocolatey

Se você tem Chocolatey instalado:

```powershell
choco install git -y
```

---

## ✅ Verificar Instalação

Após a instalação, verifique se o Git está funcionando:

### No PowerShell ou CMD:

```powershell
git --version
```

**Resultado esperado:**
```
git version 2.xx.x.windows.x
```

### No Git Bash:

Abra o Git Bash (procure no menu Iniciar) e digite:

```bash
git --version
```

---

## 🔧 Configuração Inicial do Git

Antes de começar a usar o Git, você precisa se identificar:

### Configurar seu Nome

```bash
git config --global user.name "Seu Nome"
```

**Exemplo:**
```bash
git config --global user.name "João Silva"
```

### Configurar seu Email

```bash
git config --global user.email "seu.email@exemplo.com"
```

**Exemplo:**
```bash
git config --global user.email "joao.silva@email.com"
```

### Verificar Configurações

```bash
git config --list
```

Ou verificar uma configuração específica:

```bash
git config user.name
git config user.email
```

### ⚠️ Importante

- Use o **mesmo email** que você usa no GitHub/GitLab (se tiver conta)
- Essas configurações são **globais** (válidas para todos os projetos)
- Para mudar depois: execute os mesmos comandos com novos valores

---

## 📚 Conceitos Básicos do Git

Antes de aprender os comandos, entenda estes conceitos:

### 1. Repositório (Repository / Repo)

É uma **pasta** onde o Git está controlando as versões dos arquivos.

- **Repositório Local:** Fica no seu computador
- **Repositório Remoto:** Fica na internet (GitHub, GitLab, etc.)

### 2. Commit

É um **"salvamento"** do estado dos seus arquivos em um momento específico.

- Como uma **foto** do seu projeto
- Sempre tem uma **mensagem** explicando o que foi feito
- Tem um **ID único** (hash)

### 3. Branch (Ramo)

É uma **linha de desenvolvimento** separada.

- Por padrão, todo repositório tem uma branch chamada **`main`** (ou `master`)
- Você pode criar outras branches para trabalhar em features diferentes
- Permite trabalhar em várias coisas ao mesmo tempo sem se confundir

### 4. Working Directory (Diretório de Trabalho)

É a **pasta atual** onde você está trabalhando.

### 5. Staging Area (Área de Preparação)

É uma **área intermediária** onde você coloca arquivos antes de fazer commit.

- Como uma **"caixa"** onde você coloca coisas antes de guardá-las
- Permite escolher **quais arquivos** vão no próximo commit

### 6. Remote (Remoto)

É uma **cópia do repositório** que fica em outro lugar (geralmente na internet).

- **origin** é o nome padrão do repositório remoto
- Permite **sincronizar** seu código com outros computadores/pessoas

---

## 🎯 Comandos Essenciais do Git

### 1. Inicializar um Repositório

**Comando:**
```bash
git init
```

**O que faz:**
- Cria um novo repositório Git na pasta atual
- Cria uma pasta oculta `.git` com todas as informações do Git

**Quando usar:**
- Quando você quer começar a controlar versões de um projeto novo

**Exemplo:**
```bash
cd meu-projeto
git init
```

**Resultado:**
```
Initialized empty Git repository in C:/meu-projeto/.git/
```

---

### 2. Verificar Status dos Arquivos

**Comando:**
```bash
git status
```

**O que faz:**
- Mostra quais arquivos foram modificados
- Mostra quais arquivos estão na staging area
- Mostra quais arquivos ainda não estão sendo rastreados pelo Git

**Quando usar:**
- **Sempre!** Use frequentemente para saber o estado do seu repositório
- Antes de fazer commit
- Quando não tem certeza do que mudou

**Exemplo de saída:**
```
On branch main
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   arquivo.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        novo-arquivo.js

no changes added to commit (use "git add" to stage and/or "git commit -a")
```

---

### 3. Adicionar Arquivos à Staging Area

**Comando:**
```bash
git add <arquivo>
```

**O que faz:**
- Adiciona um arquivo específico à staging area
- Prepara o arquivo para ser commitado

**Quando usar:**
- Quando você modificou arquivos e quer incluí-los no próximo commit

**Exemplos:**

Adicionar um arquivo específico:
```bash
git add arquivo.txt
```

Adicionar todos os arquivos modificados:
```bash
git add .
```

Adicionar todos os arquivos de uma pasta:
```bash
git add pasta/
```

Adicionar todos os arquivos de um tipo:
```bash
git add *.js
```

---

### 4. Fazer Commit (Salvar Mudanças)

**Comando:**
```bash
git commit -m "mensagem descritiva"
```

**O que faz:**
- Salva uma "foto" do estado atual dos arquivos na staging area
- Cria um ponto no histórico que você pode voltar depois

**Quando usar:**
- Depois de adicionar arquivos com `git add`
- Quando você completou uma tarefa ou fez uma mudança significativa

**Exemplos:**

Commit simples:
```bash
git commit -m "Adiciona função de login"
```

**Dicas para mensagens de commit:**
- Seja **descritivo** e **claro**
- Use **verbo no imperativo**: "Adiciona", "Corrige", "Remove"
- Escreva em **português** (ou inglês, conforme padrão do time)
- Exemplos bons:
  - ✅ "Adiciona validação de email no formulário"
  - ✅ "Corrige bug de cálculo de desconto"
  - ✅ "Remove código não utilizado"
- Exemplos ruins:
  - ❌ "commit"
  - ❌ "mudanças"
  - ❌ "fix"

---

### 5. Ver Histórico de Commits

**Comando:**
```bash
git log
```

**O que faz:**
- Mostra todos os commits feitos no repositório
- Mostra autor, data, mensagem e ID de cada commit

**Quando usar:**
- Para ver o histórico de mudanças
- Para encontrar um commit específico
- Para entender o que foi feito no projeto

**Exemplo de saída:**
```
commit abc123def456...
Author: João Silva <joao@email.com>
Date:   Mon Jan 10 10:30:00 2025 -0300

    Adiciona função de login

commit 789ghi012jkl...
Author: João Silva <joao@email.com>
Date:   Sun Jan 9 15:20:00 2025 -0300

    Cria estrutura inicial do projeto
```

**Versão mais compacta:**
```bash
git log --oneline
```

**Resultado:**
```
abc123d Adiciona função de login
789ghi0 Cria estrutura inicial do projeto
```

**Ver últimas 5 commits:**
```bash
git log -5
```

---

### 6. Clonar um Repositório Remoto

**Comando:**
```bash
git clone <url-do-repositorio>
```

**O que faz:**
- Baixa uma cópia completa de um repositório remoto
- Cria uma pasta local com todo o código e histórico

**Quando usar:**
- Quando você quer baixar um projeto do GitHub/GitLab
- Quando você quer trabalhar em um projeto que já existe

**Exemplos:**

Clonar do GitHub:
```bash
git clone https://github.com/usuario/projeto.git
```

Clonar em uma pasta específica:
```bash
git clone https://github.com/usuario/projeto.git minha-pasta
```

---

### 7. Ver Diferenças (Diff)

**Comando:**
```bash
git diff
```

**O que faz:**
- Mostra as diferenças entre arquivos modificados e a última versão commitada
- Mostra linha por linha o que foi adicionado, removido ou modificado

**Quando usar:**
- Antes de fazer commit, para revisar o que mudou
- Para entender o que foi modificado

**Exemplo de saída:**
```diff
diff --git a/arquivo.txt b/arquivo.txt
index 1234567..abcdefg 100644
--- a/arquivo.txt
+++ b/arquivo.txt
@@ -1,3 +1,4 @@
 Linha 1
 Linha 2
+Linha 3 adicionada
 Linha 3
```

**Ver diferenças de um arquivo específico:**
```bash
git diff arquivo.txt
```

**Ver diferenças na staging area:**
```bash
git diff --staged
```

---

### 8. Desfazer Mudanças

#### Descartar mudanças em arquivos não commitados

**Comando:**
```bash
git restore <arquivo>
```

**O que faz:**
- Descarta as mudanças feitas em um arquivo
- Volta o arquivo para o estado do último commit

**Quando usar:**
- Quando você fez mudanças que não quer manter
- Quando quer "resetar" um arquivo

**Exemplo:**
```bash
git restore arquivo.txt
```

**Descartar todas as mudanças:**
```bash
git restore .
```

#### Remover arquivo da staging area

**Comando:**
```bash
git restore --staged <arquivo>
```

**O que faz:**
- Remove um arquivo da staging area
- O arquivo volta para "modificado" mas não commitado

**Quando usar:**
- Quando você adicionou um arquivo por engano à staging area

---

### 9. Adicionar Repositório Remoto

**Comando:**
```bash
git remote add origin <url>
```

**O que faz:**
- Conecta seu repositório local a um repositório remoto
- `origin` é o nome padrão (você pode usar outro nome)

**Quando usar:**
- Quando você criou um repositório local e quer conectá-lo ao GitHub/GitLab
- Quando você quer adicionar um repositório remoto adicional

**Exemplo:**
```bash
git remote add origin https://github.com/usuario/meu-projeto.git
```

**Ver repositórios remotos configurados:**
```bash
git remote -v
```

---

### 10. Enviar Commits para o Remoto (Push)

**Comando:**
```bash
git push origin main
```

**O que faz:**
- Envia seus commits locais para o repositório remoto
- Sincroniza seu código com o servidor (GitHub/GitLab)

**Quando usar:**
- Depois de fazer commits localmente
- Quando você quer compartilhar seu código
- Para fazer backup do seu código na nuvem

**Exemplo:**
```bash
git push origin main
```

**Primeira vez (configurar upstream):**
```bash
git push -u origin main
```

O `-u` configura o "upstream", então nas próximas vezes você pode usar apenas:
```bash
git push
```

---

### 11. Baixar Mudanças do Remoto (Pull)

**Comando:**
```bash
git pull origin main
```

**O que faz:**
- Baixa mudanças do repositório remoto
- Integra essas mudanças com seu código local

**Quando usar:**
- Quando outras pessoas fizeram mudanças no repositório
- Quando você trabalha em vários computadores
- Para manter seu código atualizado

**Exemplo:**
```bash
git pull origin main
```

**Se você configurou upstream:**
```bash
git pull
```

---

### 12. Criar uma Branch (Ramo)

**Comando:**
```bash
git branch <nome-da-branch>
```

**O que faz:**
- Cria uma nova branch (mas não muda para ela)

**Quando usar:**
- Quando você quer trabalhar em uma feature sem afetar o código principal
- Para experimentar algo sem risco

**Exemplo:**
```bash
git branch feature-login
```

**Criar e mudar para a branch:**
```bash
git checkout -b feature-login
```

Ou (Git 2.23+):
```bash
git switch -c feature-login
```

---

### 13. Mudar de Branch

**Comando:**
```bash
git checkout <nome-da-branch>
```

**O que faz:**
- Muda para outra branch
- Seus arquivos mudam para o estado daquela branch

**Quando usar:**
- Quando você quer trabalhar em outra branch
- Para voltar para a branch principal

**Exemplo:**
```bash
git checkout main
```

**Método moderno (Git 2.23+):**
```bash
git switch main
```

---

### 14. Listar Branches

**Comando:**
```bash
git branch
```

**O que faz:**
- Lista todas as branches locais
- Mostra qual branch você está usando (com *)

**Quando usar:**
- Para ver todas as branches disponíveis
- Para confirmar em qual branch você está

**Exemplo de saída:**
```
  feature-login
* main
  feature-dashboard
```

**Listar branches remotas também:**
```bash
git branch -a
```

---

### 15. Mesclar Branches (Merge)

**Comando:**
```bash
git merge <nome-da-branch>
```

**O que faz:**
- Integra mudanças de uma branch na branch atual
- Combina o código de duas branches

**Quando usar:**
- Quando você terminou uma feature e quer integrá-la na branch principal
- Para combinar código de diferentes branches

**Exemplo:**
```bash
# Estar na branch main
git checkout main
# Mesclar a feature-login na main
git merge feature-login
```

---

## 🔄 Fluxo de Trabalho Básico

Aqui está o fluxo mais comum de trabalho com Git:

### Cenário: Trabalhando em um Projeto Existente

```bash
# 1. Baixar últimas mudanças
git pull origin main

# 2. Criar uma branch para sua feature
git checkout -b minha-feature

# 3. Fazer suas mudanças nos arquivos
# (editar, criar, deletar arquivos)

# 4. Ver o que mudou
git status
git diff

# 5. Adicionar arquivos modificados
git add .

# 6. Fazer commit
git commit -m "Adiciona minha feature"

# 7. Enviar para o remoto
git push origin minha-feature

# 8. (Opcional) Voltar para main e mesclar
git checkout main
git merge minha-feature
git push origin main
```

### Cenário: Começando um Projeto Novo

```bash
# 1. Criar pasta do projeto
mkdir meu-projeto
cd meu-projeto

# 2. Inicializar Git
git init

# 3. Criar arquivos
# (criar seus arquivos de código)

# 4. Adicionar arquivos
git add .

# 5. Primeiro commit
git commit -m "Commit inicial do projeto"

# 6. (Opcional) Conectar ao GitHub/GitLab
git remote add origin https://github.com/usuario/meu-projeto.git

# 7. Enviar para o remoto
git push -u origin main
```

---

## 🎓 Comandos Adicionais Úteis

### Ver informações de um commit específico

```bash
git show <hash-do-commit>
```

### Renomear arquivo

```bash
git mv arquivo-antigo.txt arquivo-novo.txt
```

### Deletar arquivo

```bash
git rm arquivo.txt
```

### Ver quem modificou cada linha

```bash
git blame arquivo.txt
```

### Ignorar arquivos (.gitignore)

Crie um arquivo `.gitignore` na raiz do projeto:

```
# Ignorar arquivos Python
__pycache__/
*.pyc

# Ignorar arquivos Node
node_modules/
npm-debug.log

# Ignorar arquivos de IDE
.vscode/
.idea/

# Ignorar arquivos de sistema
.DS_Store
Thumbs.db
```

---

## ⚠️ Problemas Comuns e Soluções

### Problema 1: "fatal: not a git repository"

**Erro:**
```
fatal: not a git repository (or any of the parent directories): .git
```

**Causa:** Você não está em uma pasta que é um repositório Git.

**Solução:**
- Execute `git init` na pasta do projeto, ou
- Navegue até uma pasta que já é um repositório Git

---

### Problema 2: Conflitos no Merge

**Erro:**
```
Auto-merging arquivo.txt
CONFLICT (content): Merge conflict in arquivo.txt
```

**Causa:** O mesmo arquivo foi modificado de formas diferentes em duas branches.

**Solução:**
1. Abra o arquivo com conflito
2. Procure por marcadores como:
   ```
   <<<<<<< HEAD
   seu código
   =======
   código da outra branch
   >>>>>>> branch-name
   ```
3. Escolha qual código manter (ou combine ambos)
4. Remova os marcadores
5. Adicione o arquivo: `git add arquivo.txt`
6. Complete o merge: `git commit`

---

### Problema 3: Commit na branch errada

**Solução:**
```bash
# Desfazer último commit (mas manter mudanças)
git reset --soft HEAD~1

# Mudar para branch correta
git checkout branch-correta

# Fazer commit novamente
git commit -m "sua mensagem"
```

---

### Problema 4: Esqueceu de fazer pull antes de push

**Erro:**
```
! [rejected]        main -> main (fetch first)
```

**Solução:**
```bash
# Baixar mudanças
git pull origin main

# Resolver conflitos se houver
# (seguir passos do Problema 2)

# Enviar novamente
git push origin main
```

---

## 📚 Recursos para Aprender Mais

- [Documentação Oficial do Git](https://git-scm.com/doc)
- [GitHub Guides](https://guides.github.com/)
- [Atlassian Git Tutorial](https://www.atlassian.com/git/tutorials)
- [Learn Git Branching](https://learngitbranching.js.org/) - Tutorial interativo

---

## ✅ Checklist para Iniciantes

Use esta checklist para garantir que você está usando Git corretamente:

- [ ] Git instalado e configurado (`git --version` funciona)
- [ ] Nome e email configurados (`git config --list`)
- [ ] Entende a diferença entre `git add`, `git commit` e `git push`
- [ ] Sabe verificar status (`git status`)
- [ ] Sabe ver histórico (`git log`)
- [ ] Sabe criar e mudar de branches
- [ ] Sabe fazer pull antes de começar a trabalhar
- [ ] Sabe fazer push após commits
- [ ] Criou um `.gitignore` para o projeto

---

## 🎯 Próximos Passos

Depois de dominar estes comandos básicos, você pode aprender:

1. **Git Rebase** - Reorganizar commits
2. **Git Stash** - Guardar mudanças temporariamente
3. **Git Cherry-pick** - Aplicar commits específicos
4. **Git Tags** - Marcar versões importantes
5. **Git Hooks** - Automatizar tarefas
6. **Git Workflows** - Fluxos de trabalho em equipe (Git Flow, GitHub Flow)

---

**Última atualização:** 2025-01-10

