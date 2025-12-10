# financial-crew

Projeto tutorial para criação de infra para data analytics

## 📚 Documentação

A documentação completa do projeto está disponível na pasta `/docs` e funciona como uma wiki:

- **[Índice da Documentação](./docs/index.md)** - Ponto de entrada da documentação
- **[Regras do Projeto](./docs/regras-projeto.md)** - Regras e convenções do projeto
- **[Tutorial de Comandos](./docs/comandos-tutorial.md)** - Comandos executados e seus propósitos
- **[Tutorial WSL Windows](./docs/tutorial-wsl-windows.md)** - Instalação do WSL com troubleshooting
- **[Tutorial Git](./docs/tutorial-git.md)** - Git para iniciantes com comandos essenciais
- **[Tutorial Docker WSL](./docs/tutorial-docker-wsl.md)** - Docker no WSL sem Docker Desktop

## 🚀 Como Baixar o Projeto

### Pré-requisitos

Antes de baixar o projeto, certifique-se de ter o Git instalado no seu sistema:

- **Windows:** Consulte o [Tutorial Git](./docs/tutorial-git.md) para instalação
- **Linux/Mac:** O Git geralmente já vem instalado. Verifique com `git --version`

### Método 1: Clonar com HTTPS (Recomendado)

Este é o método mais simples e recomendado para a maioria dos usuários:

```bash
# Clonar o repositório
git clone https://github.com/nelson1987/financial-crew.git

# Entrar na pasta do projeto
cd financial-crew
```

**Vantagens:**
- Funciona sem configuração adicional
- Não requer chaves SSH
- Ideal para iniciantes

### Método 2: Clonar com SSH

Se você já configurou chaves SSH no GitHub:

```bash
# Clonar o repositório usando SSH
git clone git@github.com:nelson1987/financial-crew.git

# Entrar na pasta do projeto
cd financial-crew
```

**Vantagens:**
- Mais seguro
- Não pede credenciais a cada operação
- Recomendado para desenvolvedores experientes

### Método 3: Baixar ZIP

Se você não tem Git instalado ou prefere não usar linha de comando:

1. Acesse: https://github.com/nelson1987/financial-crew
2. Clique no botão verde **"Code"**
3. Selecione **"Download ZIP"**
4. Extraia o arquivo ZIP no local desejado

**Nota:** Este método não permite atualizar o projeto facilmente. Recomendamos usar Git.

### Verificar Instalação

Após clonar o projeto, verifique se tudo está correto:

```bash
# Verificar se está na pasta correta
pwd

# Listar arquivos do projeto
ls -la

# Verificar status do Git
git status
```

### Atualizar o Projeto

Se você já clonou o projeto anteriormente e quer atualizar para a versão mais recente:

```bash
# Entrar na pasta do projeto
cd financial-crew

# Baixar as últimas mudanças
git pull origin main
```

### Precisa de Ajuda?

- **Não sabe usar Git?** Consulte o [Tutorial Git para Iniciantes](./docs/tutorial-git.md)
- **Problemas ao clonar?** Verifique sua conexão com a internet e permissões do repositório
- **Erro de autenticação?** Configure suas credenciais do GitHub ou use SSH