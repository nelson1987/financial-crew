# Tutorial: Instalação do WSL no Windows

Este tutorial detalha o processo completo de instalação do Windows Subsystem for Linux (WSL) no Windows, incluindo todos os problemas comuns e suas soluções.

## 📋 Pré-requisitos

- Windows 10 versão 2004 ou superior (Build 19041 ou superior)
- Windows 11 (todas as versões)
- Acesso de administrador
- Conexão com a internet (para download das distribuições)

## 🔍 Verificando a Versão do Windows

Antes de começar, verifique se seu Windows é compatível:

### Comando PowerShell
```powershell
winver
```

Ou verifique a build:
```powershell
systeminfo | findstr /B /C:"OS Name" /C:"OS Version"
```

**Requisito mínimo:** Windows 10 versão 2004 (Build 19041) ou superior.

---

## 🚀 Método 1: Instalação Automática (Recomendado)

### Passo 1: Instalar WSL com um único comando

Execute no PowerShell como **Administrador**:

```powershell
wsl --install
```

Este comando:
- Habilita os recursos necessários do Windows
- Instala o WSL 2 como versão padrão
- Instala o Ubuntu como distribuição padrão
- Instala o Windows Terminal (opcional)

### ⚠️ Problema 1: "wsl --install não é reconhecido"

**Erro:**
```
wsl : O termo 'wsl' não é reconhecido como nome de cmdlet, função, arquivo de script ou programa operável.
```

**Causa:** Versão antiga do Windows ou WSL não está disponível.

**Solução:**
1. Atualize o Windows para a versão mais recente
2. Use o Método 2 (instalação manual) abaixo

---

## 🔧 Método 2: Instalação Manual

Se o método automático não funcionar, siga estes passos:

### Passo 1: Habilitar Recursos do Windows

Execute no PowerShell como **Administrador**:

```powershell
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
```

```powershell
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```

### ⚠️ Problema 2: Erro ao habilitar recursos

**Erro:**
```
Erro: 0x800f080c
O recurso solicitado não está disponível neste sistema.
```

**Causa:** Versão do Windows incompatível ou recursos já habilitados.

**Soluções:**
1. Verifique se está usando Windows 10 versão 2004 ou superior
2. Execute o Windows Update
3. Verifique se os recursos já estão habilitados:
   ```powershell
   Get-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
   ```

### Passo 2: Reiniciar o Computador

**IMPORTANTE:** Reinicie o computador após habilitar os recursos.

```powershell
Restart-Computer
```

### Passo 3: Instalar o Pacote de Atualização do Kernel do WSL2

Baixe e instale o pacote de atualização do kernel do WSL2:

**Download:** [WSL2 Linux kernel update package](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi)

Execute o arquivo `.msi` baixado e siga o assistente de instalação.

### ⚠️ Problema 3: Erro ao instalar o pacote MSI

**Erro:**
```
Erro 2503 ou 2502 ao instalar o MSI
```

**Causa:** Permissões insuficientes ou bloqueio de antivírus.

**Soluções:**
1. Execute o instalador como Administrador (clique com botão direito → Executar como administrador)
2. Desative temporariamente o antivírus
3. Verifique se não há processos bloqueando a instalação

### Passo 4: Definir WSL 2 como Versão Padrão

Após reiniciar, execute:

```powershell
wsl --set-default-version 2
```

### ⚠️ Problema 4: "WSL 2 requer uma atualização do componente do kernel"

**Erro:**
```
WSL 2 requer uma atualização do componente do kernel.
```

**Causa:** Pacote de atualização do kernel não foi instalado corretamente.

**Solução:**
1. Verifique se o pacote MSI foi instalado (Passo 3)
2. Reinstale o pacote se necessário
3. Reinicie o computador novamente

### Passo 5: Instalar uma Distribuição Linux

#### Opção A: Via Microsoft Store

1. Abra a Microsoft Store
2. Procure por "Ubuntu" ou "WSL"
3. Escolha uma distribuição (Ubuntu, Debian, etc.)
4. Clique em "Instalar"

#### Opção B: Via Linha de Comando

```powershell
wsl --install -d Ubuntu
```

Ou para outras distribuições:
```powershell
wsl --install -d Debian
wsl --install -d openSUSE-Leap-15-3
```

### ⚠️ Problema 5: Erro ao baixar distribuição

**Erro:**
```
Erro: 0x80070003 ou 0x80040154
```

**Causa:** Problemas com a Microsoft Store ou cache corrompido.

**Soluções:**
1. Limpe o cache da Microsoft Store:
   ```powershell
   wsreset.exe
   ```
2. Reinicie o serviço Windows Update:
   ```powershell
   net stop wuauserv
   net start wuauserv
   ```
3. Tente instalar via linha de comando (Opção B acima)

### Passo 6: Configurar o Usuário Linux

Após a instalação, será solicitado:
- **Nome de usuário:** (escolha um nome)
- **Senha:** (digite uma senha - não aparecerá na tela)

### ⚠️ Problema 6: Distribuição não inicia após instalação

**Erro:**
```
A distribuição não inicia ou fecha imediatamente
```

**Causa:** Problemas com WSL 1 vs WSL 2 ou configuração incorreta.

**Soluções:**
1. Verifique a versão do WSL:
   ```powershell
   wsl --list --verbose
   ```
2. Converta para WSL 2 se necessário:
   ```powershell
   wsl --set-version Ubuntu 2
   ```
3. Verifique logs de erro:
   ```powershell
   wsl --status
   ```

---

## 🔄 Verificando e Convertendo Versões do WSL

### Verificar versões instaladas

```powershell
wsl --list --verbose
```

Ou versão curta:
```powershell
wsl -l -v
```

### Converter WSL 1 para WSL 2

```powershell
wsl --set-version <Distribuição> 2
```

Exemplo:
```powershell
wsl --set-version Ubuntu 2
```

**Nota:** A conversão pode levar alguns minutos.

### ⚠️ Problema 7: Erro ao converter para WSL 2

**Erro:**
```
Erro: 0x80370102
```

**Causa:** Virtualização não habilitada na BIOS/UEFI ou Hyper-V conflitando.

**Soluções:**
1. Habilite virtualização na BIOS/UEFI:
   - Reinicie e entre na BIOS (geralmente F2, F10, Del)
   - Procure por "Virtualization Technology" ou "VT-x" / "AMD-V"
   - Habilite e salve
2. Verifique se Hyper-V está habilitado:
   ```powershell
   Get-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V-All
   ```
3. Se necessário, desabilite Hyper-V temporariamente:
   ```powershell
   dism.exe /Online /Disable-Feature:Microsoft-Hyper-V-All
   ```
   (Reinicie após desabilitar)

---

## 🛠️ Solução de Problemas Adicionais

### Problema 8: WSL não aparece no menu Iniciar

**Solução:**
1. Execute manualmente:
   ```powershell
   wsl
   ```
2. Ou use o Windows Terminal:
   ```powershell
   wt
   ```

### Problema 9: Erro de permissões ao acessar arquivos do Windows

**Causa:** Problemas com montagem de unidades do Windows.

**Solução:**
- Acesse arquivos do Windows via `/mnt/c/`, `/mnt/d/`, etc.
- Evite editar arquivos do Windows diretamente do WSL (use cópias)

### Problema 10: Performance lenta do WSL 2

**Soluções:**
1. Certifique-se de que está usando WSL 2:
   ```powershell
   wsl --set-default-version 2
   ```
2. Armazene arquivos do projeto dentro do sistema de arquivos do WSL (não em `/mnt/`)
3. Desative o antivírus para a pasta do WSL:
   - Adicione exclusão para: `\\wsl$\`

### Problema 11: Erro "The requested operation could not be completed"

**Causa:** Serviços do WSL não estão rodando.

**Solução:**
```powershell
# Reiniciar serviços do WSL
wsl --shutdown
# Aguarde alguns segundos
wsl
```

### Problema 12: Distribuição corrompida

**Solução:**
1. Exporte dados importantes (se houver)
2. Desregistre a distribuição:
   ```powershell
   wsl --unregister Ubuntu
   ```
3. Reinstale a distribuição

---

## ✅ Verificação Final

Após a instalação, verifique se tudo está funcionando:

### 1. Verificar versão do WSL

```powershell
wsl --version
```

### 2. Listar distribuições instaladas

```powershell
wsl --list --verbose
```

### 3. Testar acesso ao Linux

```powershell
wsl
```

Dentro do WSL, teste:
```bash
uname -a
lsb_release -a
```

### 4. Verificar acesso ao sistema de arquivos do Windows

Dentro do WSL:
```bash
ls /mnt/c/
```

---

## 📝 Comandos Úteis do WSL

### Gerenciamento de Distribuições

```powershell
# Listar distribuições
wsl --list --verbose

# Definir distribuição padrão
wsl --set-default <Distribuição>

# Encerrar todas as distribuições
wsl --shutdown

# Executar comando específico
wsl -d Ubuntu -- ls -la

# Exportar distribuição
wsl --export Ubuntu ubuntu-backup.tar

# Importar distribuição
wsl --import Ubuntu C:\WSL\Ubuntu ubuntu-backup.tar
```

### Atualização do WSL

```powershell
# Atualizar WSL
wsl --update

# Verificar status
wsl --status
```

---

## 🎯 Resumo dos Problemas e Soluções

| Problema | Solução Principal |
|----------|-------------------|
| `wsl --install` não reconhecido | Atualizar Windows ou usar instalação manual |
| Erro 0x800f080c ao habilitar recursos | Verificar versão do Windows e executar Windows Update |
| Erro 2503/2502 ao instalar MSI | Executar como administrador, desativar antivírus |
| WSL 2 requer atualização do kernel | Instalar pacote MSI do kernel WSL2 |
| Erro 0x80070003 ao baixar distribuição | Limpar cache da Store (`wsreset.exe`) |
| Distribuição não inicia | Converter para WSL 2, verificar logs |
| Erro 0x80370102 na conversão | Habilitar virtualização na BIOS |
| Performance lenta | Usar WSL 2, armazenar arquivos dentro do WSL |
| Serviços não respondem | Executar `wsl --shutdown` e reiniciar |

---

## 📚 Recursos Adicionais

- [Documentação oficial do WSL](https://docs.microsoft.com/pt-br/windows/wsl/)
- [Guia de instalação da Microsoft](https://docs.microsoft.com/pt-br/windows/wsl/install)
- [Troubleshooting do WSL](https://docs.microsoft.com/pt-br/windows/wsl/troubleshooting)

---

## 🔄 Atualizações Futuras

Este tutorial será atualizado conforme novos problemas forem identificados e resolvidos.

**Última atualização:** 2025-01-10

