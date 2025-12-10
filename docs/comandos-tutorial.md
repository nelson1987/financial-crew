# Tutorial de Comandos

Este documento registra todos os comandos executados durante o desenvolvimento do projeto, explicando o intuito e propósito de cada um.

## Objetivo

Este tutorial serve como:
- **Referência** para reprodução dos passos do projeto
- **Aprendizado** sobre os comandos e ferramentas utilizadas
- **Documentação** do processo de desenvolvimento

---

## Comandos Executados

### 1. Criação da Estrutura de Documentação

#### Comando
```bash
mkdir docs
```

#### Intuito
Criar a pasta `/docs` que será o local centralizado para toda a documentação do projeto.

#### Contexto
- Todos os documentos do projeto devem ser armazenados nesta pasta
- A documentação funciona como uma wiki com referência no README
- Estrutura similar ao MkDocs para organização

#### Resultado
- Pasta `/docs` criada na raiz do projeto
- Pronta para receber os documentos de documentação

---

### 2. Comandos WSL (Windows Subsystem for Linux)

Para uma lista completa de comandos WSL e troubleshooting, consulte o [Tutorial WSL Windows](./tutorial-wsl-windows.md).

#### Comandos Principais

**Instalação automática:**
```powershell
wsl --install
```

**Verificar versão:**
```powershell
wsl --version
```

**Listar distribuições:**
```powershell
wsl --list --verbose
```

**Definir WSL 2 como padrão:**
```powershell
wsl --set-default-version 2
```

**Reiniciar WSL:**
```powershell
wsl --shutdown
```

#### Intuito
Estes comandos são utilizados para instalar, configurar e gerenciar o WSL no Windows, permitindo executar ambientes Linux nativamente no Windows.

#### Contexto
- WSL é necessário para desenvolvimento de infraestrutura de data analytics
- Permite usar ferramentas Linux no ambiente Windows
- WSL 2 oferece melhor performance que WSL 1

#### Referência Completa
Consulte o [Tutorial WSL Windows](./tutorial-wsl-windows.md) para:
- Instalação passo a passo
- Solução de problemas comuns
- Comandos avançados de gerenciamento

---

### 3. Comandos Git (Controle de Versão)

Para um tutorial completo e didático do Git, consulte o [Tutorial Git para Iniciantes](./tutorial-git.md).

#### Comandos Essenciais

**Configuração inicial:**
```bash
git config --global user.name "Seu Nome"
git config --global user.email "seu.email@exemplo.com"
```

**Inicializar repositório:**
```bash
git init
```

**Verificar status:**
```bash
git status
```

**Adicionar arquivos:**
```bash
git add .
git add arquivo.txt
```

**Fazer commit:**
```bash
git commit -m "Mensagem descritiva"
```

**Ver histórico:**
```bash
git log
git log --oneline
```

**Clonar repositório:**
```bash
git clone https://github.com/usuario/projeto.git
```

**Enviar para remoto:**
```bash
git push origin main
```

**Baixar do remoto:**
```bash
git pull origin main
```

**Criar e mudar de branch:**
```bash
git checkout -b nome-da-branch
```

**Mesclar branches:**
```bash
git merge nome-da-branch
```

#### Intuito
Git é o sistema de controle de versão padrão da indústria, essencial para:
- Controlar versões do código
- Trabalhar em equipe
- Fazer backup do código
- Gerenciar diferentes versões do projeto

#### Contexto
- Git é fundamental para qualquer projeto de software
- Permite rastrear todas as mudanças no código
- Facilita colaboração entre desenvolvedores
- Integração com GitHub, GitLab e outras plataformas

#### Referência Completa
Consulte o [Tutorial Git para Iniciantes](./tutorial-git.md) para:
- Instalação passo a passo no Windows
- Conceitos básicos explicados de forma didática
- Todos os comandos com exemplos práticos
- Fluxos de trabalho comuns
- Solução de problemas

---

### 4. Comandos Docker no WSL

Para um tutorial completo de instalação e configuração do Docker no WSL, consulte o [Tutorial Docker no WSL](./tutorial-docker-wsl.md).

#### Comandos de Instalação

**Atualizar sistema:**
```bash
sudo apt update && sudo apt upgrade -y
```

**Instalar dependências:**
```bash
sudo apt install -y ca-certificates curl gnupg lsb-release
```

**Adicionar chave GPG do Docker:**
```bash
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```

**Adicionar repositório:**
```bash
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

**Instalar Docker:**
```bash
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

**Adicionar usuário ao grupo docker:**
```bash
sudo usermod -aG docker $USER
```

**Iniciar Docker:**
```bash
sudo service docker start
```

#### Comandos Essenciais do Docker

**Verificar instalação:**
```bash
docker --version
docker compose version
```

**Testar Docker:**
```bash
docker run hello-world
```

**Gerenciar containers:**
```bash
docker ps                    # Listar containers rodando
docker ps -a                 # Listar todos os containers
docker run -it ubuntu bash   # Executar container interativo
docker stop <container-id>   # Parar container
docker rm <container-id>     # Remover container
```

**Gerenciar imagens:**
```bash
docker images                # Listar imagens
docker pull ubuntu:latest    # Baixar imagem
docker rmi <imagem>          # Remover imagem
```

**Docker Compose:**
```bash
docker compose up -d         # Iniciar serviços em background
docker compose down          # Parar serviços
docker compose ps            # Listar serviços
docker compose logs          # Ver logs
```

#### Intuito
Docker permite criar, executar e gerenciar containers, facilitando:
- Isolamento de ambientes de desenvolvimento
- Deploy consistente de aplicações
- Gerenciamento de dependências
- Criação de ambientes reproduzíveis

#### Contexto
- Docker no WSL permite usar containers Linux no Windows
- Instalação direta no WSL evita necessidade do Docker Desktop
- Essencial para desenvolvimento de infraestrutura e data analytics
- Docker Compose facilita orquestração de múltiplos containers

#### Referência Completa
Consulte o [Tutorial Docker no WSL](./tutorial-docker-wsl.md) para:
- Instalação passo a passo completa
- Configuração e troubleshooting
- Solução de problemas comuns
- Comandos avançados e melhores práticas

---

## Como Usar Este Tutorial

### Para Desenvolvedores
1. Siga os comandos na ordem apresentada
2. Leia a explicação de cada comando antes de executá-lo
3. Adapte os comandos conforme necessário para seu ambiente

### Para Documentação
- Adicione novos comandos conforme forem executados
- Mantenha a explicação clara e detalhada
- Inclua contexto sobre quando e por que o comando foi usado

---

## Próximos Passos

Este documento será atualizado conforme novos comandos forem executados durante o desenvolvimento do projeto.

---

**Última atualização:** 2025-01-10

