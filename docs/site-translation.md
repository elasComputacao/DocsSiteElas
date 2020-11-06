---
id: site-translation
title: Como adicionar uma tradução?
sidebar_label: Como adicionar uma tradução?
---

Uma das formas de contribuir com o nosso site é traduzindo-o para novos idiomas! 

Abaixo temos um tutorial de como adicionar um novo idioma. 

## 1. Adicione um ícone

Em [enums/icons.ts](site-enums#iconsts) temos todos os ícones utilizados no site, inclusive os que representam os idiomas.

De modo geral, utilizamos um ícone de uma bandeira que representa um país que fala aquela língua. Até então retiramos esses ícones do site [Flaticon](https://www.flaticon.com/).

Para adicionar o ícone, dentro da estrutura de icons.ts adicione o nome do ícone (de preferência, siga o padrão nomeDoPaisFlag) apontando para a URL ou endereço da imagem.

Caso queira adicionar a imagem à estrutura do site ao invés de utilizar uma URL, isso poderá ser feito colocando a imagem na pasta assets/images e apontando o nome do ícone para o caminho até a mesma.

Abaixo um exemplo da adição da bandeira da França:

```
const icons = {
    rainbowRibbon: "https://www.flaticon.com/svg/static/icons/svg/2292/2292506.svg",
    yellowRibbon: "https://www.flaticon.com/svg/static/icons/svg/240/240485.svg",
    blueRibbon: "https://www.flaticon.com/svg/static/icons/svg/240/240383.svg",
    pinkRibbon: "https://www.flaticon.com/svg/static/icons/svg/242/242132.svg",
    greenRibbon: "https://www.flaticon.com/svg/static/icons/svg/240/240434.svg",
    brasilFlag: "https://www.flaticon.com/svg/static/icons/svg/3022/3022546.svg",
    usaFlag: "https://www.flaticon.com/svg/static/icons/svg/3013/3013911.svg",
    spainFlag: "https://www.flaticon.com/svg/static/icons/svg/3013/3013899.svg",
    lgbtFlag: "https://www.flaticon.com/svg/static/icons/svg/2620/2620727.svg",
    girlPower: "https://www.flaticon.com/svg/static/icons/svg/2597/2597227.svg",
    blackLivesMatter: "https://www.flaticon.com/svg/static/icons/svg/3100/3100124.svg",
    franceFlag: "https://www.bandeiradafranca.com", // <===
}

export default icons;
```

## 2. Adicione o idioma à lista de idiomas

Em [enums/langs.ts](/site-enums#langsts) temos a listagem de todos os idiomas.

Para que a sua contribuição seja aceita pelo site, você deve adicionar a linguagem nessa estrutura, seguindo o seguinte template:

```
    {
        id: //ID do idioma, um número que o representa,
        src: //Ícone adicionado no passo anterior. Referencie-o utilizando icons.nomeDoIcone,
        subtitle: //Nome do idioma escrito nele,
        initials: //Sigla que o representa,
        ref: //Referência para ele no site
    }, 
```

Veja os exemplos já existentes para Português e Inglês [aqui](/site-enums#langsts).

## 3. Criando pasta de traduções

Você precisará criar uma pasta para receber as traduções de texto. Essa pasta deverá ser nomeada com a referência colocada na estrutura acima e ficar na pasta [enums](/site-enums).

Clique [aqui](https://github.com/elasComputacao/Site/tree/master/templates/traducao/enums) para ter acesso a estrutura da pasta, com os templates necessários para as traduções.

No arquivo [lang-infos.ts](/site-enums#langs-infosts), você apenas precisa copiar e colar o objeto criado na estrutura acima. 

Já em texts.ts você colocará toda a real tradução do site. É dele que a homepage do site irá consumir os textos que serão mostrados aos usuários. Para cada texto, insira a tradução referente à estrutura original em Português, que pode ser vista [aqui](/site-enums#textsts).

## 4. Criando a referência para a tradução

Depois de ter o conteúdo traduzido, agora iremos criar a referência para que ela possa ser acessada!

Dentro da pasta [pages](/site-pages) crie também uma pasta nomeada com a referência para o idioma. Dentro da pasta deverão ter os arquivos [index.tsx](/site-pages#indextsx) e [schedule.tsx](/site-pages#scheduletsx), que você pode ter acessar um template [aqui](https://github.com/elasComputacao/Site/tree/master/templates/traducao/pages).

Em **index.tsx**, importe os enums referentes ao idioma, adicionando a referência no caminho: 

```
import {bio, projects, sections, supports, buttonTexts, noEvents} from '../../enums/referencia_do_idioma/texts'
import {langInfo} from '../../enums/referencia_do_idioma/lang-infos'
```

Após isso, a página inicial já deverá estar traduzida.

Para **schedule.tsx**, importe também os enums referentes ao idioma com a referência no caminho:

```
import {schedule} from '../../enums/referencia_do_idioma/texts'
```

Feito isso, o idioma deverá ser adicionado ao site e estará pronto para ser acessado!
