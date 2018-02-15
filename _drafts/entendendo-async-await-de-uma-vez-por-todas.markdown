---
title:  "Entendendo Async/Await de uma vez por todas"
date:   2018-01-15 10:00:00
categories: [frontend]
tags: [javascript, ES2017]
excerpt_separator: <!--more-->
---

![ReactJS]({{ site.url }}/images/happy-new-year.jpg)

Salve, salve pessoal! Como foi dito na minha Retrospectiva 2017, esse ano eu pretendo postar muito mais contéudo pra vocês. Eu tentei criar algumas séries para falar sobre assuntos um pouco mais profundos, mas isso é uma coisa que toma muito tempo, e eu confesso que acabo protelando demais (Shame on me). Então decidi ir com calma, e falar sobre alguns assuntos menos extensos, mas que são muito importantes.

E hoje é a vez do `Async/Await` do **Javascript**! Depois de um ano quase sabático do **TC39** (afinal, a versão **ES2016** trouxe pouquíssimas mudanças para a linguagem), a versão ES2017 (ou ES8, como você ainda pode encontrar em alguns lugares) vem com alguns recursos bastante interessantes. Umas delas é o _Async/Await_, que estava em processo de implantação já há algum tempo, e finalmente nos agraciou com a sua presença nesse release.

<!--more-->

## O que é Async/Await?

Na verdade, o termo se trata de duas palavra-chaves que possibilitam a escrita de códigos que se comportam assíncronamente, de uma maneira que parece ser síncrona.

_"Mas pra que eu vou querer isso?"_, você deve estar se perguntando.

Bom, quem aqui não se lembra da forma caótica que era escrever código assíncrono há alguns poucos anos atrás? Se você lembrou de uma porção de callbacks espalhados e aninhados em seu código, provavelmente sentiu um pavor gélido correndo em sua espinha nesse momento.

Se nós tivéssemos que fazer 3 chamadas consecutivas a uma determinada API, por exemplo, o código seria mais ou menos o seguinte:

{% gist 8860658c19c008f1dfecb4beb20db404 %}

Calma, não me matem por estar utilizando [Jquery][jquery] por livre e espontânea vontade nesse exemplo. A idéia é mostrar a utilização de callbacks no retorno de funções assíncronas, e nada <s>pior</s> melhor que o bom e velho `$.ajax` para isso. A questão é que, mesmo que esse seja um exemplo bem simples, você já consegue perceber como um código um pouco mais complexo poderia ficar com essa abordagem.


## The Promise Way

Em 2015, com o lançamento do **ES6**, nós ganhamos oficialmente a implementação das [Promises][promises] para facilitar a escrita de códigos assíncronos, podendo inclusive encadeá-los de uma maneira mais elegante do que com os callbacks.

Para que você possa acompanhar os exemplos em seu computador, considere a seguinte API fictícia.

{% gist fb20862afbdc13df7ccee03d4ab0054c %}

Note que estamos utilizando `Promises` nas nossas APIs fictícias para poder retardar suas execuções em 500ms. Para quem não está muito familiarizado com o conceito de Promises, basta entender que nós estamos retornando uma "promessa" de que algo vai ser executado (ou não) em algum momento. E quando isso acontecer, chamamos o método `resolve` para realizar a ação.

Antes de conseguir convencer você de que as promises vieram para ficar, dê apenas mais uma olhada em como ficaria o consumo dessas APIs com a abordagem dosz callbacks (mesmo que estejamos trabalhando com promises nos nossos _"endpoints"_).

{% gist 8f01ac8df04ede69e2eeba2192eaa5e3 %}

Veja a seguir, como nós poderíamos consumir essas 3 APIs de forma consecutiva.

{% gist a63c2188b2e182079e5e37f2f8d47d3c %}



[jquery]: http://jquery.com
[promises]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise
