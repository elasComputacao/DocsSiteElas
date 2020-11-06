---
id: site-pages
title: Pages
sidebar_label: Pages
---

O diretório src/pages, por padrão do Gatsby, é onde as páginas do site deverão ser postas.

## Visão geral

Em geral, na raiz da pasta pages temos os arquivos **404.tsx**, referente a página de erro 404, **index.tsx** e **schedule.tsx**, que são referentes à versão em português do site. 

Para cada idioma disponível, temos uma pasta nomeada com a sigla que representa esse idioma. Dentro da pasta de cada idioma temos também os arquivos **index.tsx** e **schedule.tsx**.

Vejamos abaixo mais detalhes desses arquivos:

- **index.tsx**: Em cada versão de idioma, o index.tsx se refere a página inicial do site. O Gatsby reconhece arquivos nomeados dessa forma como a primeira página a ser lida, desse modo, ao acessar o site com a rota do idioma indicada, sempre nos será mostrada a homepage traduzida pelo idioma indicado. Por exemplo, https://elascomputacao.github.io/en nos retorna a homepage em inglês, já a rota raiz, indicada por "/" nos retorna a versão em português do site, que fica no root da pasta pages.

- **schedule.tsx**: Esse arquivo é referente à página da agenda. Para cada idioma temos uma tradução da mesma, que pode ser acessada pela rota do idioma seguido da rota da schedule. Por exemplo, a agenda em português pode ser acessada por https://elascomputacao.github.io/schedule e em inglês por https://elascomputacao.github.io/en/schedule.


## index.tsx

Iremos passar pelas partes do index.tsx. Como exemplo, pegaremos o arquivo para a versão em português.

### Importações

Abaixo segue a visão geral de todas as importações feitas nesse arquivo:

```
import React, { useEffect, useState } from 'react';

//Importando módulos externos
import {MapPin, Mail} from 'react-feather';
import ReactCardCarousel from 'react-card-carousel'
import {Link} from 'react-scroll'

//Importando imagens
import logoHorizontal from '../assets/logos/elas_horizontal.png';
import logoVertical from '../assets/logos/elas_vertical.png';
import instagram from '../assets/redes-sociais/instagram.svg';
import github from '../assets/redes-sociais/github.svg';
import twitter from '../assets/redes-sociais/twitter.svg';
import cabecalho from '../assets/images/header.png';

//Importando informações e conteúdo da página
import socialNetwork from '../enums/social-network'
import langs from '../enums/langs'
import infos from '../enums/infos';
import partnerships from '../enums/partnerships'
import {bio, events, projects, sections, supports, buttonTexts, noEvents} from '../enums/pt/texts'
import {langInfo} from '../enums/pt/lang-infos'

//Importando componentes
import Section from '../components/Section';
import ContactCard from '../components/ContactCard';
import IconStatus from '../components/IconStatus';
import Dropdown from '../components/DropDown';
import PictureLink from '../components/PictureLink';
import EventCard from '../components/EventCard';
import ProjectCard from '../components/ProjectCard';

//Importando funções utilizadas
import { arrayShuffle, mouseMonitoring, hasEventsMonth } from '../functions/functions';
import { getUsersFromGitHub } from '../functions/connections';

//Importando estilo
import '../styles/home.css'
```

A primeira delas é o React:
```
import React, { useEffect, useState } from 'react';
```

Depois, importamos os módulos externos utilizados no desenvolvimento do projeto. Esses módulos já foram listados na seção [Site](./site) dessa documentação:
```
//Importando módulos externos
import {MapPin, Mail} from 'react-feather';
import ReactCardCarousel from 'react-card-carousel'
import {Link} from 'react-scroll'
```

Fazemos as importações das imagens utilizadas no site, encontradas na pasta assets:
```
//Importando imagens
import logoHorizontal from '../assets/logos/elas_horizontal.png';
import logoVertical from '../assets/logos/elas_vertical.png';
import instagram from '../assets/redes-sociais/instagram.svg';
import github from '../assets/redes-sociais/github.svg';
import twitter from '../assets/redes-sociais/twitter.svg';
import cabecalho from '../assets/images/cabecalho.png';
```

Importamos os enums com informações e conteúdo das páginas da sua referida tradução:
```
//Importando informações e conteúdo da página
import socialNetwork from '../enums/social-network'
import langs from '../enums/langs'
import infos from '../enums/infos';
import partnerships from '../enums/partnerships'
import {bio, events, projects, sections, supports, buttonTexts, noEvents} from '../enums/pt/texts'
import {langInfo} from '../enums/pt/lang-infos'
```
Para saber mais sobre essas estruturas, confira a seção [Enums](./site-enums).


Também importamos os componentes criados para o site:
```
//Importando componentes
import Section from '../components/Section';
import ContactCard from '../components/ContactCard';
import IconStatus from '../components/IconStatus';
import Dropdown from '../components/DropDown';
import PictureLink from '../components/PictureLink';
import EventCard from '../components/EventCard';
import ProjectCard from '../components/ProjectCard'; 
```
Mais informações sobre essas estrutura em [Components](./site-components).

Por fim, importamos as funções:
```
//Importando funções utilizadas
import { arrayShuffle, mouseMonitoring, hasEventsMonth } from '../functions/functions';
import { getUsersFromGitHub } from '../functions/connections';
```
Para mais detalhes, siga para [Functions](./site-functions).

E os estilos:
```
//Importando estilo
import '../styles/home.css'
```

### Componente

Agora iremos partir para a parte do componente da página inicial. Primeiramente, abordaremos as partes lógicas e depois cada parte do TSX presente nele.

#### Lógica

Na parte lógica que há no componente existe um [efeito Hook](https://pt-br.reactjs.org/docs/hooks-custom.html) que é disparado sempre que a página é carregada. Nessa função, pegamos a listagem de usuárias do GitHub e randomizamos a ordem delas no array, guardando em uma constante setada por um useState, que também é um [Hook](https://pt-br.reactjs.org/docs/hooks-reference.html) de React, desse modo, o valor guardado por essa constante pode ser utilizado no restante do código.

Abaixo temos a visão da parte lógica:
```
  const [users, setUsers] = useState([]); //Array de usuárias do GitHub
  const [randomIndex, setRandomIndex] = useState([]) //Array de índices misturados

  //Função disparada em todo carregamento da página
  useEffect(() => {

    document.title = "Elas@Computação UFCG" //Título da página
    
    //Chamando função para pegar usuárias do GitHub
    getUsersFromGitHub().then(({data}) => {
        setUsers(data); //Setando os dados pegos no array de usuárias
        var array = [...Array(data.length).keys()]; //Pegando todos os índices do array das usuárias
        arrayShuffle(array); //Misturando índices para randomizar o painel
        setRandomIndex(array); //Setando índices randomizados
    })
  }, [])
```

#### TSX

Agora, iremos visualizar parte a parte da estrutura do TSX do nosso site. Todo o conteúdo da página é envolvido por uma div, que delimita o conteúdo próprio da homepage:

```
<div id="home-page" onMouseOver={() => mouseMonitoring()}>
                        .
                        .
                        .
</div>
```

##### Cabeçalho

A parte do cabeçalho compreende a seguinte estrutura:
```
<header id="header">
  <nav>
      <a href="#" className="image">
        <img src={logoHorizontal} alt="Logo Elas@Computação Horizontal"/>
      </a>
    <ul>
      <li>
        <Link to={`${sections.about}`}>{sections.about}</Link>
      </li>
      <li>
        <Link to={`${sections.panel}`}>{sections.panel}</Link>
      </li>
      <li>
        <Link to={`${sections.projects}`}>{sections.projects}</Link>
      </li>
      <li>
        <Link to={`${sections.events}`}>{sections.events}</Link>
      </li>
      <li>
        <Link to={`${sections.partnerships}`}>{sections.partnerships}</Link>
      </li>
      <li>
        <Link to={`${sections.contact}`}>{sections.contact}</Link>
      </li>
    </ul>
  </nav>
  <Dropdown
    title=""
    defaultImg={langInfo.src}
    items={langs}
  />
</header>
```

De modo geral, nele temos um nav que lista os links utilizados para navegar dentro do escopo do próprio site.

```
<li>
    <Link to={`${sections.contact}`}>{sections.contact}</Link>
</li>
```

Esses links pegam a referencia do arquivo [texts.ts](./site-enums#textsts) de sua referida versão de tradução e utilizam o componente [Link do react-scroll](https://www.npmjs.com/package/react-scroll) para deslizar pela página até o id da seção referente.

Também podemos enquadrar na estrutura de cabeçalho a imagem inicial da página:
```
 <img className="wellcome-image" src={cabecalho} alt="Elas@Computação UFCG"/>
```

#### Main
Na estrutura do main existem as seções do site. Cada seção é representada por um componente [Section](./site-components#section). No total, são 5 seções encontradas dentro do main:

1. **Sobre**

    Essa é a seção que introduz a organização para o usuário. Nela temos um texto falando um pouco sobre o Elas@Computação e contextualizando a criação da comunidade com o cenário atual das mulheres na TI, além de um [IconStatus](./site-components#iconstatus) com o logo do Elas@Computação.

    ```
    <Section title={sections.about} className="section-about" color="#fff6f3">
          
          <div className="text">
          {
            bio.map(paragraph => {
              return(<p className="paragraph">
                {paragraph}
              </p>);
            })
          }
          </div>
          
          <IconStatus 
            icon={logoVertical} 
            status={supports.outubroRosa.icon} 
            statusText={supports.outubroRosa.description}
          />
        </Section>
    ```
2. **Painel**

    Nessa seção listamos as integrantes do Elas@Computação com os ícones de seus GitHubs. Nela existe uma listagem de componentes [PictureLink](./site-components#picturelink) que representam cada uma das membras.

    ```
    <Section title={sections.panel} className="section-panel">
    { randomIndex.map(index => {
            return(
            <PictureLink 
                href={`${socialNetwork.github}/${users[index].login}`}
                pic={users[index].avatar_url}
                text={users[index].login}
                key={users[index].id}
            />
            );
        })
        }
    </Section>
    ```

    Os dados são pegos da API do GitHub pela [parte lógica](#lógica) do componente da homepage.

3. **Projetos**
    
    Essa seção compreende os projetos do Elas@Computação. Cada projeto é representado por um [ProjectCard](./site-components#projectcard) e são listados com as informações pegas em [texts.ts](./site-enums#textsts).

    ```
    <Section title={sections.projects} className="section-projects" color="#fff6f3">  
        <div id="carousel-component">
            <ReactCardCarousel disable_keydown={ true } autoplay={ true } autoplay_speed={ 15000 } className={"carousel-component"}>
                {
                projects.map(
                    element => {
                    return(
                        <ProjectCard 
                        key={element.title}
                        imageURL={element.imageURL} 
                        title={element.title} 
                        description={element.description}
                        href={element.href}
                        type={"normal"}
                        color={element.color}
                        buttonText={buttonTexts.projectCard}
                    />);
                    }
                )
                }
            </ReactCardCarousel>
        </div>
    </Section>
    ```
    Também utilizamos o componente [ReactCardCarousel](https://www.npmjs.com/package/react-card-carousel) para compor nosso carrossel de projetos.

4. **Eventos**:

    Na seção de eventos listamos tudo o que temos marcado para o mês. Nela também é possível encontrar o link de redirecionamento para a agenda.

    ```
    <Section title={sections.events} className="section-events" subtitle={buttonTexts.sectionEvents} link="/schedule">
          {
            !hasEventsMonth(events) ? 
              <EventCard
              note
              title=""
              day=""
              month=""
              year=""
              time=""
              local=""
              eventURL=""
              href=""
              description={noEvents}
              />
            :
            events.map(event => {
              return(Number(event.month) == new Date().getMonth() + 1 ? 
                <EventCard 
                eventURL={event.eventURL}
                href={event.pageURL}
                local={event.local}
                time={event.time} title={event.title}
                day={event.day} month={event.month} year={event.year}
                description={event.description}
                />
               : "");
            })
          }
    </Section>
    ```
    Verificamos a existência de eventos utilizando a [função hasEventsMonth](./site-functions/haseventsmonthevents-any) e os listamos partindo das informações pegas em [texts.ts](./site-enums#textsts).
    Utilizamos componentes [EventCard](./site-components#eventcard) para representar os eventos. 

5. **Parceiros**

    Nessa seção listamos os parceiros do Elas@Computação. As informações sobre cada parceiro é pega em [partnerships.ts](./site-enums#partnershipsts).

    ```
    <Section title={sections.partnerships} className="section-partnerships" color="#fff6f3">
        {partnerships.map(element => {
        return(
            <PictureLink text={element.title} href={element.href} pic={element.pic}/>
        );
        })}
    </Section>
    ```

    Cada parceiro é representado por um [PictureLink](./site-components#picturelink).



**IMPORTANTE**: As seções alternam de cor para deixar mais claro quando há uma troca de ambiente dentro da página inicial do site. Para isso, a propriedade "color" de [Section](./site-components#section) é setada com a cor "#fff6f3"

#### Footer

O footer é também a parte de Contato do site. Em geral, nele encontramos informações de como contatar a organização, como as redes sociais, email e localização.

```
<footer>
    <h1 id={sections.contact}>{sections.contact}</h1>
    <div className="footer-content">
        <div className="contact">
        <ContactCard href="https://goo.gl/maps/xx1zhPUttKVzUSTQ6" content={infos.location}>
            <MapPin />
        </ContactCard>        
        <ContactCard copy content={infos.email}>
            <Mail/>
        </ContactCard>
        </div>
        <div className="social-networks">
        <a target="_blank" href={socialNetwork.instagramElas}>
            <img src={instagram} alt="Instagram"/>
        </a>
        <a target="_blank" href={socialNetwork.githubElas}>
            <img src={github} alt="GitHub"/>
        </a>
        <a target="_blank" href="">
            <img src={twitter} alt="Twitter"/>
        </a>
        </div>
    </div>
    <div className="background">
    </div>
    <div className="copyright">
        <a href="#">
        <img src={logoHorizontal} alt="Logo Elas@Computação Horizontal"/>
        </a>
        <span>© 2020 Elas@Computação</span>
    </div>
    </footer>
```

#### Separadores

Toda seção é separada por uma div que atua como um separador, para ficar mais evidente a existência das repartições.

```
<div className="division"></div>
```

## schedule.tsx

Essa é a página da nossa agenda, onde ficam listados todos os eventos marcados até então. 

A estrutura é bem mais simples do que a da homepage, visto que a agenda só tem um cabeçalho e um main que é composto apenas de um grande componente de calendário, porém contém um pouco mais de lógica, utilizada para evidenciar os dias de evento.

### Importações

Abaixo está a visão geral das importações:
```
import React, { useEffect, useState } from 'react'

import { enGB } from 'date-fns/locale'
import { getDate, getMonth, getYear } from 'date-fns'
import { DatePickerCalendar} from 'react-nice-dates'
import {ArrowLeft} from 'react-feather';

import {events} from '../enums/pt/texts'

import '../styles/schedule.css'
import 'react-nice-dates/build/style.css'
```

Como sempre, iniciamos importando o React:
```
import React, { useEffect, useState } from 'react'
```

Depois importamo alguns módulos para nos ajudar com a estilização e lógica da página:
```
import { enGB } from 'date-fns/locale'
import { getDate, getMonth, getYear } from 'date-fns'
import { DatePickerCalendar} from 'react-nice-dates'
import {ArrowLeft} from 'react-feather';
```

Importamos as informações acerca dos eventos:
```
import {events} from '../enums/pt/texts'
```

E os estilos:
```
import '../styles/schedule.css'
import 'react-nice-dates/build/style.css'
```

Grande parte da agenda foi montada em cima do [React Nice Dates](https://reactnicedates.hernansartorio.com/).

### Componente

A parte mais complexa do conteúdo do componente dessa página é a lógica utilizada. 

Em questões do TSX, a página é bem simples, contendo apenas um header e um main. De mesmo modo que o index.tsx, esse componente é envolto por uma div que contém todo o conteúdo da página.

#### Lógica

De mesmo modo, para construir a parte lógica utilizamos a [documentação do React Nice Dates](https://reactnicedates.hernansartorio.com/) como referência.

Abaixo temos o código comentado, sinalizando o significado e funcionamento de cada parte:

```
  const [date, setDate] = useState<Date>() //Pega a data clicada
  const [title, setTitle] = useState("") //Seta o título do evento na data clicada
  const [description, setDescription] = useState("") //Seta a descrição do evento na data marcada

  //Efeito Hook disparado a cada vez que a constante date muda de valor
  useEffect(() => {
    getEventInfo(date); //Pega as informações da data clicada
  },[date])

  //Efeito Hook disparado ao carregar a página
  useEffect(() => {
    document.title = "Agenda - Elas@Computação UFCG" //Título da página
    setTitle("Clique em uma data para saber mais") //Título inicial das informações mostradas no header
    setDescription("Datas em evidência indicam um evento marcado para o dia") //Descrição inicial das informações mostradas no header
  }, [])

  //Função que checa se existe um evento marcado para uma data passada
  function checkDate(date) {
    //Iterando nos eventos
    for (let index = 0; index < events.length; index++) {
      const element = events[index]; //Pegando evento da vez
      const newDate = new Date(Number(element.year), Number(element.month) - 1, Number(element.day)) //Construindo objeto Date com as informações de data
      
      //Se a data for igual a passada, retorna true
      if (getDate(newDate) == getDate(date) && getMonth(newDate) == getMonth (date) && getYear(newDate) == getYear(date)) {
        return true
      }
    }
    //Senão, retorna false
    return false
  }

  //Modificadores de estilo
  const modifiers = {
    highlight: date => checkDate(date),
  }
  
  //Nomes das classes de modificadores
  const modifiersClassNames = {
    highlight: '-highlight',
  }
  
  //Função que pega e seta as informações de uma data clicada
  function getEventInfo(date) {

    //Iterando sobre os eventos
    for (let index = 0; index < events.length; index++) {
      const element = events[index]; //Pegando o evento da vez

      //Se houver um evento marcado para o dia clicado, seta as informações no header
      if (getDate(date) == Number(element.day) && getMonth(date) + 1 == Number(element.month) && getYear(date) == Number(element.year)) {
        setTitle(`${element.title} - ${element.day}/${element.month}/${element.year} (${element.time})`)
        setDescription(element.description)
        return
      } else { //Senão, indica nada marcado para o dia
        setTitle(date ? `Nenhum evento marcado para ${getDate(date)}/${getMonth(date) + 1}/${getYear(date)}` : "")
        setDescription("")
      }
      setDate(date) //Seta a data clicada
    }
  }
```

A lógica utilizada nos modificadores para automatizar a listagem das datas marcadas foi tirada da seção ["Customizing days" da documentação do React Nice Days](https://reactnicedates.hernansartorio.com).


#### Cabeçalho

O cabeçalho da agenda possui uma estrutura bastante simples: um link de volta para a homepage e uma parte textual que mostra informações em tempo real sobre a data clicada no calendário (feito pela parte lógica). A estrutura geral é mostrada abaixo:

```
<div className="schedule-header">
    <a href="/">
        <ArrowLeft size={16}/>
        Voltar para a homepage
    </a>
    <div className="event-info">
        <h4>{title}</h4>
        <p>{description}</p>
    </div>
</div>
```

#### Main

O main é composto por um único componente o [DatePickerCalendar de React Nice Days](https://reactnicedates.hernansartorio.com).

```
<main>
    <DatePickerCalendar
        date={date}
        onDateChange={(e:Date) => setDate(e)} 
        locale={enGB}
        modifiers={modifiers}
        modifiersClassNames={modifiersClassNames}
    />
</main>
```

De modo geral, esse componente consegue fixar datas clicadas no calendário, explicando a escolha do uso do mesmo.