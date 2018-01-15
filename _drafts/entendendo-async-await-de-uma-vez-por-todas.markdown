---
title:  "Entendendo Async/Await de uma vez por todas"
date:   2018-01-15 10:00:00
categories: [frontend]
tags: [javascript, ES2017]
excerpt_separator: <!--more-->
---

![ReactJS]({{ site.url }}/images/happy-new-year.jpg)

Salve, salve pessoal! Como foi dito na minha Retrospectiva 2017, esse ano eu pretendo postar muito mais contéudo pra vocês. Eu tentei criar algumas séries para falar sobre assuntos um pouco mais profundos, mas isso é uma coisa que toma muito tempo, e eu confesso que acabo protelando demais (Shame on me). Então decidi ir com calma, e falar sobre alguns assuntos menos extensos, mas que são muito importantes.

E hoje é a vez do `Async/Await` do **Javascript**! Depois de um ano quase sabático do **TC39** (afinal, a versão **ES2016** trouxe pouquíssimas mudanças para a linguagem), a versão ES2017 (ou ES8, como você ainda pode encontrar) vem com alguns recursos bastante interessantes. Umas delas é o _Async/Await_, que estava em processo de implantação já há algum tempo, e finalmente nos agraciou com a sua presença.

<!--more-->

## O que é Async/Await

Na verdade, o termo se trata de duas palavra-chaves que possibilitam a escrita de códigos que se comportam assíncronamente, de uma maneira que para ser síncrona.

_"Mas pra que eu vou querer isso?"_, você deve estar se perguntando.

Bom, quem aqui não se lembra da forma caótica que era escrever código assíncrono há alguns poucos anos atrás? Se você lembrou de uma porção de callbacks espalhados e aninhados em seu código, provavelmente sentiu um pavor gélido correndo em sua espinha nesse momento.

Se nós tivéssemos que fazer 3 chamadas consecutivas a uma determinada API, por exemplo, o código seria mais ou menos o seguinte:

{% gist 8860658c19c008f1dfecb4beb20db404 %}

Calma, não me matem por estar utilizando [Jquery][jquery] por livre e espontânea vontade nesse exemplo. A idéia é mostrar a utilização de callbacks no retorno de funções assíncronas, e nada melhor que o <s>bom</s> e velho `$.get` para isso.

[jquery]: http://jquery.com
