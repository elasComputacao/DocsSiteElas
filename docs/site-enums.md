---
id: site-enums
title: Enums
sidebar_label: Enums
---

## Visão geral

Na pasta enums encontramos a seguinte estrutura:

Duas pastas, referentes às informações que diferem em cada uma das traduções do site:

- **en**: Pasta com todas as informações para a versão em inglês do site
- **pt**: Pasta com todas as informações para a versão em português do site

Arquivos avulsos, que reunem informações que pertencem a todas as traduções:

- **icons.ts**: Arquivo com todos os endereços de ícones utilizados no site

- **infos.ts**: Informações gerais, como endereço e e-mail

- **langs.ts**: Linguagens disponíveis no site

- **social-network.ts**: Endereços de redes sociais

- **events.ts**: Eventos agendados

- **supports.ts**: Arquivo com as causas suportadas pelo Elas organizados por apoiados em uma época do ano (derivados de campanhas de concientização) ou o tempo inteiro.

## Traduções

As pastas referentes às traduções seguem a mesma estrutura:

- **lang-infos.ts**: Informações gerais da língua

- **texts.ts**: Informações textuais e conteúdo das páginas

### langs-infos.ts
Segue abaixo a estrutura geral do arquivo langs-infos.ts:

```
import icons from '../icons'

export const langInfo = {
    id: 1, //ID referente ao idioma
    src: icons.usaFlag, //Endereço para o ícone que representa o idioma
    subtitle: "English", //Título do idioma
    initials: "en", //Sigla
    ref: "en" //Referência para a rota em que ele é acessado no site
}
```

### texts.ts

O arquivo texts.ts contém várias estruturas, mostradas em conjunto abaixo, porém iremos destrinchá-las uma a uma.

```
import icons from '../icons'
import cafeComElas from '../../assets/images/cafe-com-elas.png';
import hacktoberelas from '../../assets/images/hacktoberelas.png'
import raioxdelas from '../../assets/images/raiox-delas.png'
import dev from '../../assets/images/dev-elas.png'
import { icon } from 'leaflet';

export const sections = {
    about: "Sobre",
    panel: "Painel",
    projects: "Projetos",
    events: "Eventos",
    contact: "Contatos",
    language: "Idiomas",
    partnerships: "Parcerias",
}

export const supports = {
    setembroAmarelo: {
        description: "O Elas@Computação apoia a campanha do Setembro Amarelo em prevenção ao suicídio. Se você estiver passando por problemas relacionados a sua saúde mental ou conhece alguém que está passando por alguma dificuldade, procure ajuda profissional.",
        icon: icons.yellowRibbon,
    },
    outubroRosa: {
        description: "O Elas@Computação apoia a campanha do Outubro Rosa em prevenção ao câncer de mama.",
        icon: icons.pinkRibbon,
    },
    prideMonth: {
        description: "O Elas@Computação é favorável a toda e qualquer forma de amor ❤️.",
        icon: icons.lgbtFlag,
    },
    blm: {
        description: "Vidas Negras Importam.",
        icon: icons.blackLivesMatter,
    }, 
    novembroAzul: {
        description: "O Elas@Computação apoia a campanha do Novembro Azul em prevenção ao câncer de próstata e em atenção à saúde masculina.",
        icon: icons.blueRibbon,
    },
    christmas: {
        description: "Boas Festas!",
        icon: icons.santaClaus,
    }
}

export const projects = [
    {
        imageURL: cafeComElas,
        color: "#ded1c8",
        title: "Café com Elas", 
        description: "O Café com Elas promove conversas e palestras de mulheres da TI, para estimular discussões voltadas para a área, nosso lugar, espaço e papel, buscando criar um ambiente acolhedor para a participação das meninas na comunidade.",
        href: "https://github.com/elasComputacao/CafeComElas"
    },
    {
        imageURL: raioxdelas,
        color: "",
        title: "Raio-X", 
        description: "Um ambiente web criado com o intuito de mostrar informações sobre a participação das mulheres no curso de Bacharelado em Ciência da Computação na Universidade Federal de Campina Grande, para alertar e motivar a comunidade feminina de TI dentro e fora da UFCG.",
        href: "https://github.com/elasComputacao/Raio-X"
    },
    {
        imageURL: hacktoberelas,
        color: "#072541",
        title: "HacktoberElas", 
        description: "Quer celebrar o opensource com o Elas@Computação? O HacktoberElas é uma iniciativa criada com o intuito de instigar, iniciar e preparar a comunidade em geral a contribuir com softwares livres!",
        href: "https://github.com/elasComputacao/"
    },
    {
        imageURL: dev,
        color: "#e8e8e8",
        title: "Blog no DEV", 
        description: "Estamos no DEV! Um espaço para nossa comunidade produzir e publicar conteúdos sobre tecnologia em geral e também levantar a participação de mulheres brasileiras da TI na plataforma. Segue a gente no DEV!",
        href: "https://dev.to/elascomputacao"
    }
]

export const bio = [
    'Somos uma comunidade nascida na Universidade Federal de Campina Grande em maio de 2017, com o intuito de trazer mais mulheres para o curso de Ciência da Computação e de gerar uma rede de apoio e visibilidade pautada na sororidade e no empoderamento de todas as meninas que fazem parte desse meio.',

    'Atualmente, cerca de apenas 20% das pessoas que atuam na área de TI no Brasil são mulheres. Isso se deve a uma gama de fatores que vão desde o ambiente escolar, que não incentiva o interesse feminino nas STEM (sigla em inglês para "Ciências, Tecnologias, Engenharias e Matemática"), até na própria vivência acadêmica, que promove a evasão de meninas que adentram em cursos da área pela falta de acolhimento e representatividade.',
        
    'Por isso, o Elas@Computação tem como principal objetivo incentivar a entrada, perpetuar e enaltecer as mulheres que já estão e as que desejam adentrar no mundo das Tecnologias da Informação, buscando mudar o cenário de desigualdade de gênero existente nesse contexto.'
           
]

export const buttonTexts = {
    projectCard: "Confira",
    sectionEvents: "Confira a agenda"
}

export const noEvents = "Nenhum evento confirmado para este mês"

export const schedule = {
    pageTitle: "Agenda",
    initialTitle: "Clique em uma data para saber mais",
    initialDescription: "Datas em evidência indicam um evento marcado para o dia",
    noEvents: "Nenhum evento marcado para",
}
```

Para cada idioma, as estruturas deverão ser mantidas, alterando apenas os valores para as devidas traduções.

#### sections

A constante sections guarda o nome de todas as seções existentes na homepage.
Abaixo temos o recorte de como essa estrutura se dá no arquivo pt/texts.ts, com
o nome das seções em português.

```
export const sections = {
    about: "Sobre",
    panel: "Painel",
    projects: "Projetos",
    events: "Eventos",
    contact: "Contatos",
    language: "Idiomas",
    partnerships: "Parcerias",
}
```

#### supports
A constante supports corresponde a um objeto que guarda outros objetos referentes às causas apoiadas pelo Elas@Computação, como mostrado abaixo: 

```
export const supports = {
    setembroAmarelo: {
        description: "O Elas@Computação apoia a campanha do Setembro Amarelo em prevenção ao suicídio. Se você estiver passando por problemas relacionados a sua saúde mental ou conhece alguém que está passando por alguma dificuldade, procure ajuda profissional.",
        icon: icons.yellowRibbon,
    },
    outubroRosa: {
        description: "O Elas@Computação apoia a campanha do Outubro Rosa em prevenção ao câncer de mama.",
        icon: icons.pinkRibbon,
    },
    prideMonth: {
        description: "O Elas@Computação é favorável a toda e qualquer forma de amor ❤️.",
        icon: icons.lgbtFlag,
    },
    blm: {
        description: "Vidas Negras Importam.",
        icon: icons.blackLivesMatter,
    }, 
    novembroAzul: {
        description: "O Elas@Computação apoia a campanha do Novembro Azul em prevenção ao câncer de próstata e em atenção à saúde masculina.",
        icon: icons.blueRibbon,
    },
    christmas: {
        description: "Boas Festas!",
        icon: icons.santaClaus,
    }
}
```

Para cada um desses objetos, temos a descrição do suporte a causa e um caminho para um ícone que a representa, como exemplificado abaixo.

```
prideMonth: {
        description: "O Elas@Computação é favorável a toda e qualquer forma de amor ❤️.", //descrição
        icon: icons.lgbtFlag, //ícone
    }
```

#### projects
A constante projects consiste em uma lista de objetos que compõem os projetos do Elas@Computação, como mostrado abaixo:

```
export const projects = [
    {
        imageURL: cafeComElas,
        color: "#ded1c8",
        title: "Café com Elas", 
        description: "O Café com Elas promove conversas e palestras de mulheres da TI, para estimular discussões voltadas para a área, nosso lugar, espaço e papel, buscando criar um ambiente acolhedor para a participação das meninas na comunidade.",
        href: "https://github.com/elasComputacao/CafeComElas"
    },
    {
        imageURL: raioxdelas,
        color: "",
        title: "Raio-X", 
        description: "Um ambiente web criado com o intuito de mostrar informações sobre a participação das mulheres no curso de Bacharelado em Ciência da Computação na Universidade Federal de Campina Grande, para alertar e motivar a comunidade feminina de TI dentro e fora da UFCG.",
        href: "https://github.com/elasComputacao/Raio-X"
    },
    {
        imageURL: hacktoberelas,
        color: "#072541",
        title: "HacktoberElas", 
        description: "Quer celebrar o opensource com o Elas@Computação? O HacktoberElas é uma iniciativa criada com o intuito de instigar, iniciar e preparar a comunidade em geral a contribuir com softwares livres!",
        href: "https://github.com/elasComputacao/"
    },
    {
        imageURL: dev,
        color: "#e8e8e8",
        title: "Blog no DEV", 
        description: "Estamos no DEV! Um espaço para nossa comunidade produzir e publicar conteúdos sobre tecnologia em geral e também levantar a participação de mulheres brasileiras da TI na plataforma. Segue a gente no DEV!",
        href: "https://dev.to/elascomputacao"
    }
]
```

Cada objeto segue a seguinte estrutura:
```
{
    imageURL: cafeComElas, //Caminho para imagem
    color: "#ded1c8", //Cor de fundo da imagem
    title: "Café com Elas",  //Título do projeto
    description: "O Café com Elas promove conversas e palestras de mulheres da TI, para estimular discussões voltadas para a área, nosso lugar, espaço e papel, buscando criar um ambiente acolhedor para a participação das meninas na comunidade.", //Descrição curta do projeto
    href: "https://github.com/elasComputacao/CafeComElas" //URL para mais detalhes
}
```

#### bio

A bio consiste em um array, no qual cada elemento que o compõe é referente a um parágrafo da seção "Sobre" do site. A estrutura geral é mostrada abaixo:

```
export const bio = [
    'Somos uma comunidade nascida na Universidade Federal de Campina Grande em maio de 2017, com o intuito de trazer mais mulheres para o curso de Ciência da Computação e de gerar uma rede de apoio e visibilidade pautada na sororidade e no empoderamento de todas as meninas que fazem parte desse meio.',

    'Atualmente, cerca de apenas 20% das pessoas que atuam na área de TI no Brasil são mulheres. Isso se deve a uma gama de fatores que vão desde o ambiente escolar, que não incentiva o interesse feminino nas STEM (sigla em inglês para "Ciências, Tecnologias, Engenharias e Matemática"), até na própria vivência acadêmica, que promove a evasão de meninas que adentram em cursos da área pela falta de acolhimento e representatividade.',
        
    'Por isso, o Elas@Computação tem como principal objetivo incentivar a entrada, perpetuar e enaltecer as mulheres que já estão e as que desejam adentrar no mundo das Tecnologias da Informação, buscando mudar o cenário de desigualdade de gênero existente nesse contexto.'
           
]
```

#### buttonTexts
Objeto com os textos dos botões existentes na página

```
export const buttonTexts = {
    projectCard: "Confira",
    sectionEvents: "Confira a agenda"
}
```

#### noEvents
Texto da nota de quando não há eventos a serem listados:

```
export const noEvents = "Nenhum evento confirmado para este mês"
```

#### schedule 
Textos da página da agenda:

```
export const schedule = {
    pageTitle: "Agenda", //Título da página
    initialTitle: "Clique em uma data para saber mais", //Título inicial do header
    initialDescription: "Datas em evidência indicam um evento marcado para o dia", //Descrição inicial
    noEvents: "Nenhum evento marcado para", //Mensagem de ausência de evento
}
```

## Outros arquivos

### icons.ts

Esse arquivo contém todos os ícones utilizados no site. Cada ícone é referenciado por um nome e aponta para uma URL de uma imagem. 

Até então, utilizamos as imagens do site [flaticon.com](https://www.flaticon.com/).

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
    santaClaus: "https://www.flaticon.com/svg/static/icons/svg/601/601393.svg"
}

export default icons;
```

### infos.ts

Esse arquivo contém informações gerais de localidade e contato com a nossa comunidade.

```
const infos = {
    email: "elas@computacao.ufcg.edu.br",
    location: "Universidade Federal de Campina Grande - UFCG, Campus Central, R. Aprígio Veloso, 882 - Universitário, Campina Grande - PB - Brasil, 58428-830",
}

export default infos;
```

### langs.ts

Esse arquivo possui uma array com todos os idiomas suportados pelo site. Cada idioma é representado por um objeto, que será mostrado com mais detalhes.

A configuração geral do arquivo é dado abaixo.

```
import icons from './icons'

const langs = [
    {
        id: 0,
        src: icons.brasilFlag,
        subtitle: "Português",
        initials: "pt",
        ref: "/"
    }, 
    {
        id: 1,
        src: icons.usaFlag,
        subtitle: "English",
        initials: "en",
        ref: "en"
    },
]

export default langs;
```

Abaixo temos em detalhes a configuração dos objetos que representam os idiomas:

```
{
    id: 0, //Identificador único numérico para o idioma
    src: icons.brasilFlag, //Caminho para ícone que representa um país que fala o idioma
    subtitle: "Português", //Título do idioma
    initials: "pt", //Sigla que o define
    ref: "/" //Referência para acesso da versão traduzida para ele no site
}
```

### partnerships.ts

Esse arquivo guarda todos os parceiros da nossa comunidade e também compreende um array de objetos que representam um parceiro. Abaixo, a visão geral do arquivo:

```
import pet from '../assets/images/pet.png';
import mulherTech from '../assets/images/mulher-tech.png'

const partnerships = [
    {
        title: "OpenDev",
        href: "https://opendevufcg.org/",
        pic: "https://avatars2.githubusercontent.com/u/42285400?s=200&v=4",
    },
    {
        title: "CAESI",
        href: "https://caesiufcg.github.io/",
        pic: "https://avatars0.githubusercontent.com/u/37838513?s=200&v=4",
    },
    {
        title: "PyLadies - PB",
        href: "https://github.com/pyladiespb-org",
        pic: "https://avatars0.githubusercontent.com/u/44339004?s=200&v=4",
    },
    {
        title: "PET Computação",
        href: "https://www.dsc.ufcg.edu.br/~pet/",
        pic: pet,
    },
    {
        title: "Mulher Tech Sim Senhor",
        href: "http://mulhertechsim.sr/",
        pic: mulherTech,
    }
]

export default partnerships;
```

Em detalhes, um objeto que representa um parceiro segue a seguinte configuração:

```
{
    title: "OpenDev",//Nome do parceiro
    href: "https://opendevufcg.org/",//URL para site ou outro portal de mais informações sobre
    pic: "https://avatars2.githubusercontent.com/u/42285400?s=200&v=4",//URL ou caminho para imagem ou logo do parceiro
}
```

### social-network.ts

Esse arquivo compreende todas as redes sociais acessadas a partir do site.

```
const socialNetwork = {
    github: "https://github.com",
    githubElas: "https://github.com/elasComputacao",
    instagramElas: "https://www.instagram.com/elascomputacao",
}

export default socialNetwork;
```

### events.ts

O arquivo events.ts consiste em um array de objetos que representam um evento da comunidade, como mostrado abaixo:

```
const events = [
    {
        title: "Café com Elas",
        description: '"Café com Elas" na programação da Jornada Acadêmica Computação@UFCG.',
        day: "5",
        month: "11",
        year: "2020",
        time: "20h",
        local: "Discord CCC",
        pageURL: "",
        eventURL: "",
    },
]

export default events;
```

A estrutura dos objetos segue o seguinte padrão:

```
{
    title: "Café com Elas", //Título do evento
    description: '"Café com Elas" na programação da Jornada Acadêmica Computação@UFCG.', //Descrição breve do evento
    day: "5", //Dia 
    month: "11", //Mês
    year: "2020", //Ano
    time: "20h", //Horário
    local: "Discord CCC", //Local do evento
    pageURL: "", //URL para página do evento
    eventURL: "", //URL para evento em agenda
}
```

### supports.ts

Arquivo que organiza as causas suportadas pelo Elas@Computação por suportes a campanhas em um período do ano ou causas sociais, de modo a automatizar a forma que são mostradas no site.

Abaixo temos a visão geral do arquivo:

```
export const supportsMonth = {
    6: "prideMonth",
    9: "setembroAmarelo",
    10: "outubroRosa",
    11: "novembroAzul",
    12: "christmas",
}

export const supportsAllTime = [
    "prideMonth", "blm"
]
```

A primeira estrutura é um objeto que tem como chave um número que representa o mês que uma causa é apoiada, derivada de uma campanha de concientização. Desse modo, podemos deixar que durante toda a duração do mês esse suporte seja mostrado no site.

```
export const supportsMonth = {
    6: "prideMonth",
    9: "setembroAmarelo",
    10: "outubroRosa",
    11: "novembroAzul",
    12: "christmas",
}
```

Já a segunda estrutura é um array com o nome de todas as causas que são apoiadas, mas não possuem em si uma campanha de concientização que se prolonga em um mês. Esses são mostrados no site de forma aleatória, quando não há uma causa específica para o mês em questão.

```
export const supportsAllTime = [
    "prideMonth", "blm"
]
```

Detalhes sobre o nome das causas e como esses objetos são organizados em [supports](./site-enums#supports).
