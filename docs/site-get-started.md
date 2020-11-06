---
id: site-get-started
title: Primeiros Passos 
sidebar_label: Primeiros Passos
---


## Preparando o ambiente
O site do Elas@Computação é feito utilizando [Gatsby](https://www.gatsbyjs.com), desse modo, para que você consiga contribuir é preciso tê-lo instalado na sua máquina:

Instale o Gatsby CLI na sua máquina
```
npm install -g gatsby-cli
```

Mais detalhes podem ser vistos na [documentação do Gatsby](https://www.gatsbyjs.com/docs/quick-start/).

## Executando o projeto localmente

Para rodar o projeto de forma local, siga os passos:

1. Clone o [repositório do site](https://github.com/elasComputacao/Site)
``` 
git clone https://github.com/elasComputacao/Site.git
``` 

2. No seu terminal, se dirija até o diretório clonado
```
cd Site
```

3. E depois até a pasta project:
```
cd project
```

4. Em project, execute o comando:
```
gatsby develop
```

Após isso, o projeto estará rodando localmente para desenvolvimento em [localhost:8000](https://localhost:8000).

Caso sua porta 8000 esteja ocupada ou ocorra algum problema para executar na mesma, você poderá usar o comando

```
gatsby develop -p <numero da porta>
```

Por exemplo, o comando abaixo roda o projeto em localhost:8080

```
gatsby develop -p 8080
```
