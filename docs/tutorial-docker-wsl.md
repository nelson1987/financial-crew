# Tutorial: Instalação do Docker no WSL (Sem Docker Desktop)

Este tutorial detalha como instalar e configurar o Docker diretamente no WSL, sem utilizar o Docker Desktop no Windows.

## 📋 Pré-requisitos

- WSL 2 instalado e funcionando
- Ubuntu ou outra distribuição Linux no WSL
- Acesso de administrador (sudo)
- Conexão com a internet

**Importante:** Este tutorial assume que você já tem o WSL 2 configurado. Se não tiver, consulte o [Tutorial WSL Windows](./tutorial-wsl-windows.md).

---

## 🔍 Verificando o WSL

Antes de começar, verifique se o WSL está funcionando:

### Abrir o WSL

```powershell
wsl
```

Ou abra diretamente o Ubuntu no menu Iniciar.

### Verificar versão do WSL

Dentro do WSL, execute:

```bash
wsl --version
```

Ou verifique a distribuição:

```bash
cat /etc/os-release
```

### Verificar se está usando WSL 2

No PowerShell do Windows:

```powershell
wsl --list --verbose
```

**Resultado esperado:**
```
  Ubuntu    Running    2
```

Se mostrar `1`, você precisa converter para WSL 2. Consulte o [Tutorial WSL Windows](./tutorial-wsl-windows.md).

---

## 🚀 Instalação do Docker no WSL

### Passo 1: Atualizar o Sistema

Primeiro, atualize os pacotes do sistema:

```bash
sudo apt update
sudo apt upgrade -y
```

**Tempo estimado:** 5-10 minutos (dependendo da conexão)

### ⚠️ Problema 1: Erro ao atualizar pacotes

**Erro:**
```
E: Could not get lock /var/lib/dpkg/lock-frontend
```

**Causa:** Outro processo está usando o gerenciador de pacotes.

**Solução:**
```bash
# Verificar processos
ps aux | grep apt

# Se necessário, matar processos
sudo killall apt apt-get

# Remover locks
sudo rm /var/lib/apt/lists/lock
sudo rm /var/cache/apt/archives/lock
sudo rm /var/lib/dpkg/lock*

# Tentar novamente
sudo apt update
```

---

### Passo 2: Instalar Dependências Necessárias

Instale os pacotes necessários para o Docker:

```bash
sudo apt install -y \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
```

**O que faz:**
- `ca-certificates`: Certificados SSL/TLS
- `curl`: Ferramenta para baixar arquivos
- `gnupg`: Ferramenta de criptografia (para verificar assinaturas)
- `lsb-release`: Informações sobre a distribuição Linux

### ⚠️ Problema 2: Erro ao instalar dependências

**Erro:**
```
E: Unable to locate package <nome-do-pacote>
```

**Causa:** Repositórios não atualizados ou nome incorreto do pacote.

**Solução:**
```bash
# Atualizar novamente
sudo apt update

# Verificar se o pacote existe
apt search <nome-do-pacote>

# Se não encontrar, verificar se os repositórios estão corretos
sudo apt update && sudo apt upgrade
```

---

### Passo 3: Adicionar Chave GPG Oficial do Docker

Adicione a chave GPG oficial do Docker para verificar os pacotes:

```bash
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```

**O que faz:**
- Cria o diretório para chaves GPG
- Baixa a chave pública do Docker
- Salva a chave no local correto

### ⚠️ Problema 3: Erro ao baixar chave GPG

**Erro:**
```
curl: (6) Could not resolve host
```

**Causa:** Problema de conexão com a internet ou DNS.

**Solução:**
```bash
# Verificar conexão
ping -c 3 google.com

# Se não funcionar, verificar DNS
cat /etc/resolv.conf

# Se necessário, configurar DNS manualmente
sudo bash -c 'echo "nameserver 8.8.8.8" > /etc/resolv.conf'
sudo bash -c 'echo "nameserver 8.8.4.4" >> /etc/resolv.conf'
```

---

### Passo 4: Adicionar Repositório do Docker

Adicione o repositório oficial do Docker:

```bash
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

**O que faz:**
- Adiciona o repositório oficial do Docker
- Configura para usar a versão estável
- Usa a chave GPG que adicionamos anteriormente

### ⚠️ Problema 4: Erro "lsb_release: command not found"

**Causa:** Pacote `lsb-release` não instalado.

**Solução:**
```bash
sudo apt install -y lsb-release
```

Depois, execute novamente o comando do Passo 4.

---

### Passo 5: Atualizar Lista de Pacotes

Atualize a lista de pacotes para incluir o Docker:

```bash
sudo apt update
```

**Resultado esperado:**
```
Get:1 https://download.docker.com/linux/ubuntu jammy InRelease [48.9 kB]
...
```

### ⚠️ Problema 5: Erro ao atualizar com repositório do Docker

**Erro:**
```
E: The repository 'https://download.docker.com/linux/ubuntu ... Release' does not have a Release file.
```

**Causa:** Versão do Ubuntu não suportada ou nome incorreto.

**Solução:**
1. Verificar versão do Ubuntu:
   ```bash
   lsb_release -cs
   ```

2. Se necessário, usar uma versão específica. Para Ubuntu 22.04 (Jammy):
   ```bash
   echo \
     "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
     jammy stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
   ```

3. Atualizar novamente:
   ```bash
   sudo apt update
   ```

---

### Passo 6: Instalar Docker Engine

Instale o Docker Engine, Docker CLI e Containerd:

```bash
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

**O que instala:**
- `docker-ce`: Docker Community Edition (motor principal)
- `docker-ce-cli`: Interface de linha de comando
- `containerd.io`: Runtime de containers
- `docker-buildx-plugin`: Plugin para builds avançados
- `docker-compose-plugin`: Plugin para Docker Compose

**Tempo estimado:** 5-10 minutos

### ⚠️ Problema 6: Erro ao instalar Docker

**Erro:**
```
E: Unable to locate package docker-ce
```

**Causa:** Repositório não foi adicionado corretamente.

**Solução:**
1. Verificar se o repositório foi adicionado:
   ```bash
   cat /etc/apt/sources.list.d/docker.list
   ```

2. Se estiver vazio ou incorreto, refazer os passos 3 e 4

3. Atualizar novamente:
   ```bash
   sudo apt update
   ```

4. Tentar instalar novamente

---

### Passo 7: Verificar Instalação

Verifique se o Docker foi instalado corretamente:

```bash
docker --version
```

**Resultado esperado:**
```
Docker version 24.x.x, build xxxxx
```

Verifique também o status do serviço:

```bash
sudo systemctl status docker
```

**Nota:** No WSL, o systemd pode não estar habilitado. Isso é normal e será resolvido no próximo passo.

---

## 🔧 Configuração do Docker no WSL

### Passo 8: Adicionar Usuário ao Grupo Docker

Por padrão, apenas o root pode executar comandos Docker. Adicione seu usuário ao grupo `docker`:

```bash
sudo usermod -aG docker $USER
```

**O que faz:**
- Adiciona seu usuário ao grupo `docker`
- Permite executar comandos Docker sem `sudo`

**Importante:** Você precisará fazer logout e login novamente (ou reiniciar o WSL) para que a mudança tenha efeito.

### ⚠️ Problema 7: Ainda precisa usar sudo após adicionar ao grupo

**Causa:** Mudanças de grupo não foram aplicadas.

**Solução:**
```bash
# Fechar e reabrir o WSL
exit
```

No PowerShell:
```powershell
wsl --shutdown
wsl
```

Ou simplesmente feche e abra novamente o terminal WSL.

---

### Passo 9: Iniciar Docker Manualmente (WSL sem systemd)

No WSL, o systemd pode não estar habilitado. Inicie o Docker manualmente:

```bash
sudo service docker start
```

Verifique se está rodando:

```bash
sudo service docker status
```

**Resultado esperado:**
```
 * Docker is running
```

### ⚠️ Problema 8: Docker não inicia automaticamente no WSL

**Causa:** WSL não usa systemd por padrão.

**Soluções:**

#### Solução A: Iniciar manualmente (simples)

Crie um alias ou adicione ao `.bashrc`:

```bash
echo 'sudo service docker start > /dev/null 2>&1' >> ~/.bashrc
```

Agora o Docker iniciará automaticamente ao abrir o WSL.

#### Solução B: Habilitar systemd no WSL (avançado)

1. Edite o arquivo de configuração do WSL no Windows:
   ```powershell
   notepad C:\Users\SeuUsuario\.wslconfig
   ```

2. Adicione:
   ```ini
   [boot]
   systemd=true
   ```

3. Reinicie o WSL:
   ```powershell
   wsl --shutdown
   wsl
   ```

4. Verifique se systemd está funcionando:
   ```bash
   systemctl status
   ```

---

### Passo 10: Testar Docker

Teste se o Docker está funcionando corretamente:

```bash
docker run hello-world
```

**Resultado esperado:**
```
Hello from Docker!
This message shows that your installation appears to be working correctly.
...
```

Se você ainda precisar usar `sudo`, verifique se fez logout/login após adicionar ao grupo docker.

### ⚠️ Problema 9: Erro "Cannot connect to the Docker daemon"

**Erro:**
```
Cannot connect to the Docker daemon. Is the docker daemon running on this host?
```

**Causa:** Serviço Docker não está rodando.

**Solução:**
```bash
# Iniciar Docker
sudo service docker start

# Verificar status
sudo service docker status

# Tentar novamente
docker run hello-world
```

---

## 🐳 Comandos Docker Essenciais

Agora que o Docker está instalado, aqui estão os comandos mais usados:

### Verificar Informações do Docker

```bash
docker info
docker version
```

### Gerenciar Imagens

```bash
# Listar imagens
docker images

# Baixar imagem
docker pull ubuntu:latest

# Remover imagem
docker rmi <nome-da-imagem>
```

### Gerenciar Containers

```bash
# Listar containers rodando
docker ps

# Listar todos os containers
docker ps -a

# Executar container
docker run -it ubuntu bash

# Parar container
docker stop <container-id>

# Iniciar container parado
docker start <container-id>

# Remover container
docker rm <container-id>
```

### Executar Container Interativo

```bash
docker run -it --name meu-container ubuntu bash
```

**Flags:**
- `-i`: Modo interativo
- `-t`: Aloca um terminal
- `--name`: Nome do container

### Executar Container em Background

```bash
docker run -d --name meu-container ubuntu sleep 3600
```

**Flag:**
- `-d`: Modo detached (background)

### Ver Logs do Container

```bash
docker logs <container-id>
docker logs -f <container-id>  # Seguir logs em tempo real
```

### Executar Comando em Container Rodando

```bash
docker exec -it <container-id> bash
```

---

## 🔄 Docker Compose

Docker Compose já foi instalado como plugin. Use-o assim:

### Verificar Instalação

```bash
docker compose version
```

### Exemplo de Uso

Crie um arquivo `docker-compose.yml`:

```yaml
version: '3.8'

services:
  web:
    image: nginx:latest
    ports:
      - "8080:80"
    volumes:
      - ./html:/usr/share/nginx/html
```

Execute:

```bash
docker compose up -d
```

**Comandos úteis:**
```bash
docker compose up          # Iniciar serviços
docker compose up -d       # Iniciar em background
docker compose down        # Parar e remover serviços
docker compose ps          # Listar serviços
docker compose logs        # Ver logs
```

---

## 🛠️ Solução de Problemas Adicionais

### Problema 10: Docker muito lento no WSL

**Causa:** Arquivos sendo acessados via `/mnt/c/` (sistema de arquivos do Windows).

**Solução:**
- **Sempre trabalhe dentro do sistema de arquivos do WSL** (`~/projetos` em vez de `/mnt/c/Users/...`)
- Mova seus projetos para dentro do WSL:
  ```bash
  # Criar pasta de projetos no WSL
  mkdir -p ~/projetos
  cd ~/projetos
  
  # Clonar ou copiar projetos aqui
  ```

### Problema 11: Erro de permissão ao montar volumes

**Erro:**
```
Permission denied
```

**Solução:**
```bash
# Verificar permissões
ls -la /caminho/do/volume

# Ajustar permissões se necessário
sudo chmod -R 755 /caminho/do/volume
```

**Melhor prática:** Use volumes nomeados em vez de bind mounts:
```bash
docker volume create meu-volume
docker run -v meu-volume:/dados ubuntu
```

### Problema 12: Porta já em uso

**Erro:**
```
Bind for 0.0.0.0:8080 failed: port is already allocated
```

**Solução:**
```bash
# Verificar qual processo está usando a porta
sudo lsof -i :8080

# Ou usar outra porta
docker run -p 8081:80 nginx
```

### Problema 13: Espaço em disco insuficiente

**Erro:**
```
no space left on device
```

**Solução:**
```bash
# Limpar imagens não utilizadas
docker system prune -a

# Verificar uso de espaço
docker system df

# Limpar volumes não utilizados
docker volume prune
```

---

## ✅ Verificação Final

Execute estes comandos para verificar se tudo está funcionando:

### 1. Verificar Instalação

```bash
docker --version
docker compose version
```

### 2. Verificar Permissões

```bash
docker ps
```

Se funcionar sem `sudo`, as permissões estão corretas.

### 3. Testar Container

```bash
docker run hello-world
```

### 4. Testar Docker Compose

Crie um `docker-compose.yml` simples:

```yaml
version: '3.8'
services:
  test:
    image: hello-world
```

Execute:

```bash
docker compose up
```

---

## 🎯 Resumo dos Problemas e Soluções

| Problema | Solução Principal |
|----------|-------------------|
| Erro de lock ao atualizar | Matar processos apt e remover locks |
| Pacote não encontrado | Atualizar repositórios (`sudo apt update`) |
| Erro ao baixar chave GPG | Verificar conexão e DNS |
| Repositório sem Release file | Verificar versão do Ubuntu e ajustar |
| Docker não inicia automaticamente | Adicionar `sudo service docker start` ao `.bashrc` |
| Precisa usar sudo | Adicionar usuário ao grupo docker e fazer logout/login |
| Cannot connect to daemon | Iniciar serviço Docker (`sudo service docker start`) |
| Performance lenta | Trabalhar dentro do sistema de arquivos do WSL |
| Porta já em uso | Verificar processo ou usar outra porta |
| Espaço insuficiente | Limpar imagens e volumes não utilizados |

---

## 📚 Próximos Passos

Agora que o Docker está instalado, você pode:

1. **Aprender Docker Compose** - Orquestrar múltiplos containers
2. **Criar suas próprias imagens** - Escrever Dockerfiles
3. **Trabalhar com volumes** - Persistir dados
4. **Configurar redes Docker** - Conectar containers
5. **Usar Docker em produção** - Deploy de aplicações

---

## 🔗 Recursos Adicionais

- [Documentação Oficial do Docker](https://docs.docker.com/)
- [Docker no WSL 2](https://docs.docker.com/desktop/wsl/)
- [Docker Compose Documentation](https://docs.docker.com/compose/)
- [Best Practices para Dockerfiles](https://docs.docker.com/develop/dev-best-practices/)

---

## 💡 Dicas Importantes

1. **Sempre trabalhe dentro do WSL** - Não use `/mnt/c/` para projetos Docker
2. **Inicie o Docker manualmente** - Adicione ao `.bashrc` se systemd não estiver habilitado
3. **Use Docker Compose** - Facilita muito o gerenciamento de múltiplos containers
4. **Limpe regularmente** - Use `docker system prune` para liberar espaço
5. **Aprenda Dockerfiles** - Essencial para criar suas próprias imagens

---

**Última atualização:** 2025-01-10

