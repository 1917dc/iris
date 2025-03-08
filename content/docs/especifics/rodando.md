---
title: 2.1 - Rodando localmente
type: docs
prev: docs/folder/
---

## Rodando o frontend localmente

### Linux & Windows

Com o `git` instalado:
```bash
cd && git clone https://github.com/1917dc/iris.git
```
> [!CAUTION]
> Sempre verifique a branch que contém as alterações mais recentes no projeto, nunca use branches desatualizadas.

Dentro da pasta do projeto, no seu terminal favorito, use o seguinte comando para a instalação de dependências respectivas ao frontend:
```bash
npm i # ou npm install
```

> [!IMPORTANT]
> Certifique-se de criar o arquivo `.env` no diretório base do frontend, dentro dele coloque: `BACKEND_URL = http://localhost:8080`.

Para rodar a parte do frontend use no seu terminal favorito o comando:
```bash
npm run dev
```

## Rodando o backend localmente
### Linux & Windows

```bash
cd && git clone https://github.com/D0ntP4nic42/iris-api.git
```

Dentro da pasta do projeto, use o seguinte comando para inicializar a API do backend:
```bash
docker compose up --build # o build só é necessário quando alterações no código do backend forem feitas.
```

Caso nenhum erro ocorra, muito provavelmente a API já estará rodando, e portanto o frontend já pode ser totalmente utilizado.

Dentro do arquivo `application.properties` no backend, temos os dados pré-cadastrados da aplicação, eles devem ser usados para realização de testes de uso que necessitam de login dentro da aplicação.