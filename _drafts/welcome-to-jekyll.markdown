---
title:  "Welcome to Jekyll!"
date:   2017-08-08 15:04:23
categories: [frontend]
tags: [react, frontend, js]
---

Como eu já falei pra vocês no meu [primeiro post][primeiro-post], atualmente estou na vibe do [ReactJS][reactjs]. E pra ser sincero, foi **amor à primeira vista**! O React pode até ter virado uma modinha hoje em dia, mas é uma biblioteca tão incrível que eu acredito que ele veio para ficar, e é por isso que hoje vamos iniciar uma série sobre como criar uma aplicação em React do zero!

Mas antes de entrarmos na nossa aplicação propriamente dita _<s>(já adianto que os amantes de música como eu vão gostar!)</s>_, nesse artigo vamos falar sobre o que é o React e o básico da sua utilização.

## React... isso é de comer?

Mas afinal de contas, o que é esse tal React que todos tanto falam?

Bom, o React é uma **biblioteca** desenvolvida pelo pessoal do Instagram (e depois pelo Facebook) para a criação de **componentes reutilizáveis**. Resumindo, é uma forma de você desenvolver o seu site ou aplicação sem repetir um milhão de vezes aquela sua `div` que faz a mesma coisa pelo seu código.

Pode parecer pouco para uma biblioteca que é tão falada, mas lhes asseguro que não é. O React deixa o processo de desenvolvimento tão intuitivo que fez eu me perguntar como que antes eu criava minhas aplicações de outro jeito.

Além disso, a forma com que o React renderiza os nossos componentes é extremamente rápida com o **Virtual DOM**! Afinal, a galera do Facebook sabe como fazer as coisas, não é mesmo?

É importante frisar que, apesar de muitos o considerarem como tal, ele não é um concorrente direto do [AngularJS][angular]. Isso porque o Angular é um **framework** JS completo, que resolve vários tipos de problema, desde criação de componentes HTML até o gerenciamento do fluxo de dados da aplicação através do **Two-way Data Binding**.

Mas antes que você vá embora desse post por achar que o React é muito pouco para valer seu precioso tempo, eu gostaria de dizer que o fato dele se preocupar com apenas um problema não é necessariamente uma coisa ruim. Na verdade, como ele foi desenvolvido para um único propósito, consequentemente temos um ganho maior na performance. E além disso, existem outras bibliotecas que funcionam muito bem no ecossistema React e cuida de todo o resto, como o [Redux][redux]

## Mais motivos para usar o React

Se você ainda não está convencido, posso citar mais alguns motivos para você dar uma chance para a nossa _"biblioteca modinha"_:

### Tudo junto e misturado

O React utiliza uma forma diferente de renderizar o seu HTML. Ao invés de escrever seu markup e comportamento em lugares diferentes, você consegue escrever HTML diretamente no seu javascript através do [JSX][jsx].

Imagine só como seria lindo você poder gerar HTML sem concatenações caóticas de strings ou sem utilizar métodos _write-only (dúvido que você consiga ler e entender seu HTML depois de algumas semanas)_ de alguma API do javascript.

_**Pois é, com o JSX isso é possível!**_

<!-- 
O seu componente dicaria mais ou menos assim:

{% highlight javascript %}
import React, { Component } from 'react';

class DivBolada extends Component {
  render() {
    return (
      <div>
        <span>
          Cat Demo View
        </span>

        <img src="http://i.imgur.com/QbA1W4Z.jpg">

        <span>
          Some random cats picture.
        </span>
      </div>
    );
  }
}
{% endhighlight %} -->

[primeiro-post]:      {% post_url 2017-08-09-comecando-com-o-pe-direito %}
[reactjs]:            https://facebook.github.io/react/
[angular]:            https://angularjs.org/
[redux]:              http://redux.js.org/
[jsx]:                https://jsx.github.io/