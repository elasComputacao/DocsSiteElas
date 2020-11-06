---
id: site-functions
title: Functions
sidebar_label: Functions
---

## Visão geral
O diretório functions compreende as funções utilizadas na lógica do front-end do site. 

Nele existem dois arquivos:

- **connections.ts**: Arquivo com funções que se conectam a APIs

- **functions.ts**: Arquivo com funções de lógica dos componentes

## connections.ts

Em connections.ts existem funções que se conectam a APIs e retornam dados úteis para compor o front-end de maneira mais automatizada.

Visão geral do arquivo:

```
import { Octokit } from "@octokit/rest";

export async function getUsersFromGitHub() {
    const octokit = new Octokit(
        {
          auth: process.env.REACT_APP_GITHUB_TOKEN,
          baseUrl: 'https://api.github.com',
        }
      );
  
      return(octokit.orgs.listMembers({
        org: "elasComputacao",
        per_page: 100,
        type: "",
      }));
}   
```

Abaixo estão elencadas as funções existentes no arquivo.

### getUsersFromGitHub

Essa função acessa a API do GitHub com a finalidade de retornar as membras da organização. Até então, são pegas apenas aquelas que mantém a privacidade da organização como pública em seu perfil. 

Abaixo está o escopo da função:

```
export async function getUsersFromGitHub() {
    const octokit = new Octokit( 
        {
          auth: process.env.REACT_APP_GITHUB_TOKEN,
          baseUrl: 'https://api.github.com',
        }
      ); //Instanciando um objeto Octokit, passando um objeto com a autenticação e a URL da API do GitHub
  
      return(octokit.orgs.listMembers({
        org: "elasComputacao",
        per_page: 100,
        type: "",
      })); //Retornando array com objetos que representam as membras da comunidade.
}   
```

Foi utilizada a biblioteca [Octokit](https://github.com/octokit), um cliente para a API do GitHub, para fazer o acesso à mesma. Mais informações sobre seu funcionamento na [documentação do Octokit](https://octokit.github.io/rest.js/v18).


## functions.ts

No arquivo functions.ts temos funções que atuam na lógica do front-end do site.

Visão geral do arquivo:

```
export function arrayShuffle(array:any[]) {
    const size = array.length;
    
    for (let index = 0; index < array.length; index++) {
        const randomNumber = Math.floor(Math.random() * size);
        const element1 = array[index];
        const element2 = array[randomNumber];
        array[randomNumber] = element1;
        array[index] = element2;
    }
}

export function mouseMonitoring() {
    const header = window.document.getElementById("header")
    const main = window.document.getElementById("main")
    const scroll = window.scrollY;

    window.addEventListener('mousemove', (event) => {
        var pos = event.clientY;
        if (scroll > 380 && ((pos >= 0 && pos < 100 && window.innerWidth < 1080) || (pos >= 0 && pos < 140 && window.innerWidth > 1080))) {
          header.style.position = "fixed";
          main.style.marginTop = window.innerWidth < 1080 ? "76px" : "101px";
        } else {
          header.style.position = "relative";
          main.style.marginTop = "0px";    
        }
    })
}
```

Abaixo temos detalhes sobre as funções implementadas.

### arrayShuffle(array: any[])

Essa função recebe um array como entrada e troca os elementos nas posições do mesmo de forma aleatória. Ela é utilizada para a randomização do componente do Painel de membras do site, para que todas possam aparecer em evidência. 

```
export function arrayShuffle(array:any[]) {
    const size = array.length; //Tamanho do array de entrada
    
    for (let index = 0; index < array.length; index++) { //Iterando sobre o array
        
        //Utilizando a função random de Math para gerar um número aleatório no intervalo [0, size[
        const randomNumber = Math.floor(Math.random() * size); 

        //Pegando os elementos que iremos trocar de posição
        const element1 = array[index];
        const element2 = array[randomNumber];

        //Trocando os elementos de posição
        array[randomNumber] = element1;
        array[index] = element2;
    }
}
```
Os elementos são trocados n (tamanho do array) vezes dentro do array e de forma aleatória, o que assegura a aleatoriedade das posições.

### mouseMonitoring()

Essa função é responsável pelo efeito de esconder/aparecer do header na página. Com ela, podemos monitorar a posição do mouse na tela e mudar a propriedade de estilo do cabeçalho de relative para fixed, dependendo da posição que o usuário está passando o cursor.

```
export function mouseMonitoring() {
    const header = window.document.getElementById("header") //Pegando elemento do header por id
    const main = window.document.getElementById("main") //Pegando elemento do main por id
    const scroll = window.scrollY; //Pegando a posição de scroll vertical da página

    window.addEventListener('mousemove', (event) => { // Monitorando o evento de movimento do mouse
        var pos = event.clientY; //Pegando a posição atual do mouse na vertical

        //Verificando se as coordenadas do mouse na tela condizem com a posição que 
        //o header deve aparecer. Caso seja, mudamos de relative para fixed, caso não, 
        //mudamos de fixed para relative.
        if (scroll > 380 && 
        ((pos >= 0 && pos < 100 && window.innerWidth < 1080) || 
        (pos >= 0 && pos < 140 && window.innerWidth > 1080))) {
          header.style.position = "fixed";
          main.style.marginTop = window.innerWidth < 1080 ? "76px" : "101px"; //Ajuste da posição vertical do main na mudança de posição do header
        } else {
          header.style.position = "relative";
          main.style.marginTop = "0px";    //Ajuste da posição vertical do main na mudança de posição do header
        }
    })
}
```

### hasEventsMonth(events: any[])

Essa função é reponsável por monitorar a presença de eventos existentes no mês atual. Ela varre um array de eventos, passado como parâmetro e se encontrado pelo menos um evento para o mês, retorna true, caso contrário, retorna false.

```
export function hasEventsMonth(events: any[]) {
    
  //Iterando sobre o array passado
  for (let index = 0; index < events.length; index++) {
    const element = events[index]; //Pegando o elemento da vez 

    //Se o mês for igual ao mês atual, retorna true
    if (Number(element.month) == new Date().getMonth() + 1) {
      return true;
    }
  }    

  //Caso não encontre eventos para o mês, retorna false
  return false;
}
```

### setAutoSupport(supportsObject)

Essa função é responsável por identificar qual a causa que deve ser mostrada no [IconStatus](./site-components#iconstatus). Ela pega as informações de [supports.ts](./site-enums#supportsts), identifica se há alguma causa em campanha no mês, caso não haja, sorteia um de forma aleatória e retorna um objeto que representa uma causa (mais detalhes em [supports](./site-enums#supports)).

```
export function setAutoSupport(supportsObject) {
  
  const month = new Date().getMonth() + 1; //Pega o mês atual
  
  //Pega as chaves de supportMonth, que representam os meses das campanhas, e os coloca em um array 
  const keysMonth = Object.keys(supportsMonth); 

  //Caso haja uma campanha para o mês atual...
  if (keysMonth.includes(String(month))) {
    const key = supportsMonth[month]; //Pegando a chave que referencia a campanha (o nome dela)
    return supportsObject[key]; //Retornando o objeto referente a campanha do mês
  }

  //Caso não haja uma campanha para o mês...

  //Gerando um índice aleatório entre 0 e o tamanho do array supportAllTime
  const random = Math.floor(supportsAllTime.length * Math.random());
  
  //Pegando a chave que referencia a campanha (o nome dela)
  const key = supportsAllTime[random];

  //Retornando o objeto a campanha sorteada de forma aleatória  
  return supportsObject[key];

}
```

```
```
