---
title: 1.0 Dependências
type: docs
prev: /
next: docs/folder/
---

# Frontend
## NVM
### Windows
- [Download](https://github.com/coreybutler/nvm/releases)
> [!TIP]
> Reinicie seu PowerShell após a instalação, caso o NVM não esteja sendo identificado.

<br>Em caso de bugs relacionados a instalação, recorra à documentação oficial: [NVM Windows](https://github.com/coreybutler/nvm-windows)

### Linux
```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.1/install.sh | bash
```
Exporte o diretório para o seu perfil de terminal, por padrão o terminal usado é o `bash`, portanto o comando abaixo deve ser colado no `~/.bashrc`, caso você esteja usando `zsh` o comando deve ser colado no `~/.zshrc`.
```bash
export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm
```
- Instalação do Node
```bash
nvm install node
```
Após isso, você deve ter a versão estável mais atual do Node, e deve ser capaz de rodar os comandos relacionados ao [npm](https://www.npmjs.com/).

# Backend

> [!WARNING]
> Para evitar problemas locais rodando o back-end, sempre opte por rodar o projeto [`dockerizado`](https://www.reddit.com/r/Frontend/comments/yvem0t/comment/iwe0mma/?utm_source=share&utm_medium=web3x&utm_name=web3xcss&utm_term=1&utm_content=share_button).
> IDE's de Java costumam baixar a JDK automaticamente quando rodamos o projeto, então não se vê necessário mostrar o processo de instalação da JDK, só se certifique de estar utilizando a versão 21.

## Docker
### Windows
[Docker Desktop - Windows](https://docs.docker.com/desktop/setup/install/windows-install/)

> [!TIP]
> Você também pode rodar o projeto utilizando [WSL 2](https://learn.microsoft.com/pt-br/windows/wsl/install). WSL é um sistema Linux emulado dentro da sua máquina Windows. 
> Caso escolha essa forma, siga o passo-a-passo da seção de Linux.

### Linux

#### Distribuições baseadas em Ubuntu

##### Pré-requisitos de instalação
```bash
sudo apt update
sudo apt install apt-transport-https ca-certificates curl gnupg
```
##### Adicionar a chave GPG oficial do Docker
```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker.gpg
```
##### Adicionar o repositório Docker no sistema
- **Ubuntu 22**:
```bash
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu noble stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```
- **Ubuntu 21**:
```bash
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu jammy stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

##### Atualização de pacotes
```bash
sudo apt update
```
##### Instalação do Docker
```bash
sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

#### Distribuições baseadas em Arch
```bash
sudo pacman -S docker
```

#### Pós instalação

Verifique a instalação:

```bash
sudo docker run hello-world
```
- O output deve conter:
```bash
Hello from Docker!
```

Removendo a necessidade do `sudo` para execução de comandos Docker:
```bash
sudo usermod -aG docker ${USER}
```
```bash
newgrp docker
```
