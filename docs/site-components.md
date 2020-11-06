---
id: site-components
title: Components
sidebar_label: Components
---

## Visão Geral

Esse diretório compreende todos os componentes desenvolvidos para o site. 

De modo geral, todos estão organizados em pastas que contém dois arquivos:

- **index.tsx**: Código em TSX do componente.

- **styles.css**: Estilo aplicado no componente.

Os componentes existentes são:

- **ContactCard**: Card para informações de contato

- **DropDown**: Botão com efeito de expansão. Utilizado para os idiomas.

- **EventCard**: Card para eventos.

- **IconStatus**: Ícone com status. Utilizado para mostrar as causas apoiadas pelo Elas@Computação.

- **ItemContent**: Item contido no DropDown.

- **LinkButton**: Botão com link de redirecionamento.

- **PictureLink**: Link com imagem. Utilizado para representar as membras no painel e também os parceiros.

- **ProjectCard**: Card para projetos.

- **Section**: Seções do site.

- **Tooltip**: Componente com efeito de tooltip.

Abaixo estão especificados detalhes de todos os componentes.

## ContactCard

O componente ContactCard compreende a estutura utilizada para representar uma informação de contato ou localização. No site, pode ser encontrado no footer, mostrando o e-mail e o endereço da comunidade. 

Visão geral do código:

```
import React, { useState } from 'react';
import {CopyToClipboard} from 'react-copy-to-clipboard';

import './styles.css'

interface Properties {
    icon?: string;
    content: string;
    copy?: boolean;
    href?:string;
}
const ContactCard:React.FC<Properties> = ({content, copy, href, children}) => {

  const [status, setStatus] = useState(false)

  function showStatus(val) {
    const element = window.document.getElementById("status");
    if (val && copy) {
      element.style.visibility = "visible";
    } else if (copy){
      element.style.visibility = "hidden";
      setStatus(false);
    }
  }

  return (
      <div onMouseOver={() => showStatus(true)}
      onMouseOut={() => showStatus(false)}>
        {
          copy ? 
          <CopyToClipboard text={content} 
            onCopy={() => setStatus(true)}>
            <div id="contactcard-component">
              <div className="icon">
                {children}
              </div>
              <p id="text-content" className="copy">
                {content}
              <span id="status">
                {status ? "Copiado!" : "Clique para copiar!"}
              </span>
              </p>
            </div>
          </CopyToClipboard> :
          <a href={href} target="_blank" id="contactcard-component">
            <div className="icon">
              {children}
            </div>
            <p id="text-content">
              {content}
            </p>
          </a>
        }
      </div>
  );
}

export default ContactCard;
```

### Propriedades

- **content**: Conteúdo em texto que deverá aparecer no componente. Ex: elas@computacao.ufcg.edu.br

- **copy**: Booleano que indica se o conteúdo pode ser copiado ao clicar

- **href**: Endereço para redirecionar o usuário ao clicar no componente.

- **children**: Por padrão, no children pode ser passado um ícone que será exibido juntamente da informação de contato/localização. Isso dá mais liberdade para que se possam passar também ícones de bibliotecas muito utilizadas em React, como a [Feather Icons](https://feathericons.com/).

### Mais informações

Para o efeito de copiar ao clicar, utilizamos o módulo [CopyToClipboard](https://www.npmjs.com/package/react-copy-to-clipboard).

## DropDown

Esse componente é consiste em uma [lista suspensa](https://pt.wikipedia.org/wiki/Menu_drop-down). No site, ele é utilizado para optar pelos idiomas disponíveis.

Visão geral do código:

```
import React, { useEffect, useState } from 'react';
import {css} from 'emotion';
import { useMenuState, Menu, MenuItem, MenuButton } from "reakit/Menu";
import ItemContent from '../ItemContent';
import { ChevronDown, ChevronUp } from 'react-feather';

import './styles.css'

const styles = css`
  display: flex;
  flex-direction: column;
  background: white;
  transition: opacity 250ms ease-in-out, transform 250ms ease-in-out;
  opacity: 0;
  transform-origin: top center;
  transform: scaleY(0);
  [data-enter] & {
    opacity: 1;
    transform: scaleY(1);
  }
`;

interface Properties {
  title: string;
  defaultImg: string;
  items: {
    src: string;
    subtitle: string;
    ref: string;
  }[];
};

const DropDown:React.FC<Properties> = ({title, defaultImg, items}) => {
  const menu = useMenuState({ animated: 250 });

  const [url, setURL] = useState("");

  useEffect(() => {
    setURL(window.location.href)
  }, []);

  function verifyLocation(href) {
    if (!url.split("/").includes(href)) {
      return href;
    } else {
      return "#";
    }
  }

  return (
      <div id="dropdown-component">
          <MenuButton {...menu} className="button">
            <span>{title}</span>
            <img src={defaultImg} alt="Lang" className="selected"/>
            <ChevronDown className="icon"/>
          </MenuButton>
          <Menu
            {...menu}
            aria-label={title}
            style={{ border: 0, background: "none", padding: 0 }}
          >
            <div className={styles}>
              {items.map((item) => {
                return(
                <MenuItem {...menu} className="menu-item">
                  <a href={verifyLocation(item.ref)}>
                    <ItemContent
                      title={item.subtitle}
                      src={item.src}
                    />
                  </a>
                </MenuItem>);
              })}
            </div>
          </Menu>
      </div>
  );
}

export default DropDown;
```

### Propriedades

- **title**: Título a ser exibido no botão. Ex: Idioma

- **defaultImg**: Imagem default a ser mostrada no botão junto do título. Ex: icons.brasilFlag

- **items**: Array de objetos que representam um item a ser listado pela lista suspensa. No nosso caso, a lista passada é a contida no arquivo [langs.ts](http://localhost:3000/docs/site-enums#langsts)

### Mais informações

Esse componente é escrito em cima do [Menu do Reakit](https://reakit.io/docs/menu/), adaptando apenas para o funcionamento dentro da finalidade que desejamos no site.

Além disso, o componente [ItemContent](#itemcontent) é utilizado em seu conteúdo para representar cada item da lista suspensa.

## EventCard

Aqui temos o componente utilizado para representar um evento no site. A estilização desse é feita baseada em uma nota adesiva e utilizamos na seção de Eventos.

Visão geral do código:

```
import React, { useState } from 'react';

import './styles.css'

interface Properties {
    title?: string;
    day?: string;
    month?: string;
    year?: string;
    description: string;
    time?: string;
    eventURL?: string;
    href?: string;
    local?: string;
    note?: boolean;
}
const EventCard:React.FC<Properties> = ({note, title, day, month, year, description, time, local, eventURL, href}) => {
  const [isOver, setIsOver] = useState(false);
  const dateTime = day != "" && month != "" && year != "" && time != "" ? `${day}/${month}/${year} - ${time}` : ""

  return (
    note ? 
    <div id="eventcard-component" onMouseOver={() => setIsOver(true)} onMouseOut={() => setIsOver(false)}>
    <div className="header-note">
      <div className="pin">
         <div className="pin-part">
         </div>
       </div>
      </div>
      <p className="note">
        {description}
      </p>
   </div>:
    <div id="eventcard-component" onMouseOver={() => setIsOver(true)} onMouseOut={() => setIsOver(false)}>
     <div className="header-note">
       <div className="pin">
          <div className="pin-part">
          </div>
        </div>
        <div className="title">
          <h3>{title}</h3>
          <div className="infos">
            <span>{dateTime}</span>
            <span>{local}</span>
          </div>
        </div>
       </div>
       <p>
         {description}
       </p>
      <div className={isOver ?  "more" : "more-hidden"}>
        {eventURL.trim() == "" ?
        <a className="block">Adicionar à agenda</a>
        :
        <a href={eventURL}>Adicionar à agenda</a>
        }

        {href.trim() == "" ?
        <a className="block">Saber mais</a>
        :
        <a href={href}>Saber mais</a>
        }
      </div> 
    </div>
  );
}
```

### Propriedades

- **title**: Título da nota adesiva. Ex: Café com Elas

- **day**: Dia do evento. Ex: 05

- **month**: Mês do evento. Ex: 11

- **year**: Ano do evento. Ex: 2020

- **description**: Descrição breve sobre o evento. Ex: Café com elas na JACC

- **time**: Horário que irá ocorrer o evento. Ex: 19h

- **eventURL**: URL para adicionar o evento à agenda ou acessar uma plataforma que sediará o evento de forma remota

- **href**: URL para site ou ambiente para mais informações sobre o evento

- **local**: Onde o evento irá ocorrer. Ex: Google Meet

- **note**: Booleano que representa opção para a nota apenas mostrar a descrição passada, em caso de não houver eventos a serem listados

### Mais informações 

Esse componente foi todo feito à mão para ser adicionado à proposta do site. 

## IconStatus

O IconStatus é um componente utilizado para mostrar uma imagem que contém um ícone de status abaixo. No site, ele é utilizado para mostrar as causas que o Elas@Computação apoia, deixando em evidência algum movimento em campanha no momento.

Visão geral do código:

```
import React from 'react';

import Tooltip from '../Tooltip';

import './styles.css'

interface Properties {
    icon: string;
    status: string;
    statusText: string;
}

const IconStatus:React.FC<Properties> = ({icon, status, statusText}) => {
  return (
    <div id="iconstatus-component">
      <img className="icon" src={icon} alt="Icon"/>     
      <Tooltip position="bottom" slim={false} text={statusText}>
        <img src={status}  alt="Status" className="status"/>
      </Tooltip>
    </div>
  );
}

export default IconStatus;
```

### Propriedades 

- **icon**: Imagem principal do componente, que ficará em evidência. Ex: elas_vertical

- **status**: Imagem que aparecerá como status atual da imagem, ficará no canto inferior direito da imagem original. Ex: icons.lgbtFlag

- **statusText**: Texto que será exibido ao passar o mouse por cima do status em um Tooltip. Ex: O Elas@Computação é favorável a todo tipo de amor.

### Mais informações

O componente [Tooltip](#tooltip) é utilizado dentro desse para o efeito de mostrar o texto de apoio à causa ao passar o mouse por cima do ícone de status.


## ItemContent

Esse componente representa um item de um [DropDown](#dropdown).

Visão geral do código:

```
import React from 'react';

import './styles.css'

interface Properties {
    src: string;
    title: string;
}

const ItemContent:React.FC<Properties> = ({src, title}) => {
  return (
    <div id="itemcontent-component">
        <img src={src} alt={title}/>
        <span>{title}</span>
    </div>
  );
}

export default ItemContent;
```

### Propriedades

- **src**: Caminho/endereço para uma imagem que representa o item. Ex: icons.brasilFlag

- **title**: Título do item. Ex: Português

### Mais informações

Esse componente foi feito apenas para representar de maneira mais adequada um item em uma lista suspensa no formato que se desejava no site.


## LinkButton

Componente de botão com redirecionamento para uma URL. Utilizado nas seções e nos cards de projeto.

Visão geral do código:

```
import React from 'react';

import './styles.css'

interface Properties {
    href: string;
    title: string;
}

const LinkButton:React.FC<Properties> = ({href, title}) => {
  return (
    <a id="linkbutton-component" href={href} target="_blank">
        <span>{title}</span>
    </a>
  );
}

export default LinkButton;
```

### Propriedades 

- **href**: URL que o botão irá redirecionar. Ex: /schedule

- **title**: Título do botão. Ex: Conferir

### Mais informações

Esse componente foi feito com a finalidade de reaproveitamento do código e do estilo de botão. 


## PictureLink

Componente de link com imagem. Utilizamos em duas seções do site: no Painel, para representar as membras e redirecionar para seus respectivos GitHubs e nas Parcerias, para representar nossos parceiros e redirecionar para seus sites/GitHubs.

Visão geral do código:

```
import React from 'react';
import Tooltip from '../Tooltip';

import './styles.css'

interface Properties {
    pic: string;
    href: string;
    text: string;
};

const PictureLink:React.FC<Properties> = ({pic, href, text}) =>  {

  return (
    <div id="picturelink-component">
        <Tooltip position="bottom" slim={true} text={`${text}`}>
            <a href={href} target="_blank">
              <img src={pic} alt={text}/>
            </a>
        </Tooltip>
    </div>
  );
}

export default PictureLink;
```

### Propriedades

- **pic**: URL ou caminho para imagem que aparecerá no componente. Ex: icons.brasilFlag

- **href**: URL que irá redirecionar o usuário. Ex: https://www.github.com/elasComputacao

- **text**: Texto que aparecerá no tooltip com informações acerca do que se trata o link. Ex: OpenDev UFCG

### Mais informações

O componente [Tooltip](#tooltip) também é utilizado na implementação desse componente. 


## ProjectCard

ProjectCard é o componente que representa um card de projeto. No site, podemos vê-los no carrossel de projetos na seção Projetos.

Visão geral do código:
```
import React from 'react';
import LinkButton from '../LinkButton';

import './styles.css'

interface Properties {
    title: string;
    description: string;
    imageURL: string;
    href: string;
    type: string;
    color?: string;
    buttonText: string;
}
const ProjectCard:React.FC<Properties> = ({title, description, imageURL, href, type, color, buttonText}) => {
  
  const DEFAULT_COLOR = "#fff6f3";

  const backgroundStyle = {
    backgroundColor: color && color == "" ? DEFAULT_COLOR : color
  }


  return (
    <div id="projectcard-component" className={type}>
      <div className="img-content" style={backgroundStyle}>
        <img src={imageURL}/>
      </div>
      <div className="content">
        <h3>{title}</h3>
        <p>
          {description}
        </p>
        <LinkButton
        href={href}
        title={buttonText}
        />
      </div>
    </div>
  );
}

export default ProjectCard;
```

### Propriedades

- **title**: Título/nome do card. Ex: Café com Elas

- **description**: Descrição breve sobre o conteúdo. Ex: O Café com Elas promove conversas e palestras de mulheres da TI, para estimular discussões voltadas para a área, nosso lugar, espaço e papel, buscando criar um ambiente acolhedor para a participação das meninas na comunidade.

- **imageURL**: URL ou caminho para imagem que ilustra o card.

- **href**: URL para site ou outra plataforma com mais informações. Ex: https://github.com/elasComputacao

- **type**: Sinalização para se o card deve ficar em destaque ou não. Pode assumir os valores "normal" para demonstração comum e "spotlight" para evidenciar.

- **color**: Cor de fundo para a imagem. Caso não seja recebida uma cor, por default é setada a cor "#fff6f3". O padrão utilizado é o hexadecimal. Ex: #ffffff

- **buttonText**: Texto a ser apresentado no LinkButton. Ex: Conferir

### Mais informações

O componente [LinkButton](#linkbutton) é utilizado na implementação desse componente. 

## Section

Componente utilizado para representar as seções do site.

Visão geral do código:
```
import React, { useEffect, useState } from 'react';
import { ChevronsDown, ChevronsUp } from 'react-feather';
import LinkButton from '../LinkButton';

import './styles.css'

interface Properties {
    title: string;
    className?: string;
    toggle?: boolean;
    subtitle?: string;
    link?:string;
    color?:string;
}
const Section:React.FC<Properties> = ({title, children, className, toggle, subtitle, link, color}) => {
  
  const [hidden, setHidden] = useState(true);
  const [text, setText] = useState("");

  useEffect(() => {
    if (toggle) {
      handleToggle();
    }
  }, [])

  function handleToggle() {
    const section = window.document.getElementById(className);
    if (hidden) {
      if (window.innerWidth > 1080) {
        section.style.maxHeight = "416px";
      } else {
        section.style.maxHeight = "246px";
      }
    } else {
      section.style.maxHeight = "600vh";
    }
    setHidden(!hidden);
  }

  return (
    <div id="section-component" className={className} style={{backgroundColor: color}}>
        <div id={title}></div>
          <h1>{title}</h1>
          <div className="children" id={className}>
              {children}
          </div>
          {toggle ? 
            <button className="toggle" 
            onClick={handleToggle}
            onMouseOver={() => {hidden ? setText("Mostrar menos") : setText("Mostrar mais")}}
            onMouseOut={() => setText("")}
            >
              {hidden ? <ChevronsUp className="icon"/> : <ChevronsDown className="icon"/>}
            </button> : <></>
          }
          {toggle ? 
            <span className="status">{text}</span> : <></>
          }
          {link ? <LinkButton title={subtitle} href={link}/> : <></>}
    </div>
  );
}

export default Section;
```

### Propriedades

- **title**: Título da seção. Ex: Sobre

- **className**: Nome da classe CSS para estilização exclusiva. Ex: section-about

- **toggle**: Booleano que, se passado (true), adiciona uma opção de esconder ou expandir parte do conteúdo da seção.

- **subtitle**: Texto utilizado no LinkButton para redirecionamento, caso passado. Ex: Confira a agenda

- **link**: Booleano que indica se a seção tem um link de redirecionamento que completa seu conteúdo. Um exemplo para tal pode ser visto na seção [Eventos](https://elascomputacao.github.io#Eventos) do site, que redireciona para a agenda. 

- **color**: Cor de fundo da section, padrão em hexadecimal.

### Mais informações

[LinkButton](#linkbutton) também é utilizado na implementação desse componente. 


## Tooltip

Componente de efeito de tooltip.

Visão geral do código:
```
import React from "react";

import {
  useTooltipState,
  Tooltip as ReakitTooltip,
  TooltipReference,
} from "reakit/Tooltip";

import './styles.css'

const Tooltip = ({ children, text, slim, position, ...props }) => {
  const tooltip = useTooltipState({placement: position});
  return (
    <>
      <TooltipReference {...tooltip} ref={children.ref} {...children.props}>
        {(referenceProps) => React.cloneElement(children, referenceProps)}
      </TooltipReference>
      <ReakitTooltip {...tooltip} {...props} id={slim ? "text-slim" : "text"}>
        <p>
            {text}
        </p>
      </ReakitTooltip>
    </>
  );
}

export default Tooltip;
```

### Propriedades

- **children**: Componente que ativará o tooltip ao passar com mouse por cima. A tag deverá envolver esse componente.

- **text**: Texto que aparecerá no conteúdo do tooltip. Ex: CAESI

- **slim**: Booleano que indica se o tooltip deve ter uma área menor, para receber apenas uma frase pequena ou palavra, como nos ícones do [Painel](https://elascomputacao.github.io#Painel).

- **position**: Indica a posição que ele deve aparecer em relação ao componente que o ativa. Os padrões são seguidos de acordo com o [Reakit](https://reakit.io/docs/tooltip/).

### Mais informações

Esse componente é escrito em cima do Tooltip do [Reakit](https://reakit.io/docs/tooltip/), adaptando-o apenas para facilitar nosso uso no contexto do site. 
