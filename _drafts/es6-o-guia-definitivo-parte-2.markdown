---
title:  "ES6: O Guia Definitivo - Parte 2"
date:   2017-08-21 11:11:23
categories: [frontend]
tags: [javascript, es6, guia]
excerpt_separator: <!--more-->
---

![ES6](/images/es6.jpg)

Fala galera! Já deu pra ver que a pancada de funcionalidades que vieram junto com o **ES6**, não é? São tantos os novos recursos da linguagem, que eu não consegui falar nem sobre a metade deles no post [ES6: O Guia Definitivo - Parte 1][ultimo-post]. Então antes de me estender muito, vamos seguir com as novidades do ES6!

<!--more-->

## Orientação a objetos

Um dos recursos mais aguardados _(e polêmicos)_ do *ES6* é o suporte à **Classes** de objetos. A verdade é que o nosso querido **Javascript** sempre foi uma linguagem extremamente flexível, e por isso existem muitas formas de você representar um objeto, desde a declaração de um simples **JSON** até uma [função de primeira classe][primeira-classe].

Isso acontece porque, até o **ES5**, o Javascript se utilizava apenas da [prototipação][prototipacao] para implementar a **Orientação a Objetos**. Com isso, temos a possibilidade de instanciar uma simples função, e o próprio Javascript faz o **binding** da variável `this` de acordo com o seu escopo, ganhando então o comportamento esperado de um objeto.

Vamos exemplificar como funciona a Orientação a Objetos por prototipação:

{% highlight javascript linenos %}
function Monstro(){
  this.descricao = function(){
    console.log("Eu tenho "+this.altura+"m de altura e peso "+this.peso+"kg");
  }
}

var lobisomen = new Monstro();
lobisomen.altura = 2.2;
lobisomen.peso = 110;
lobisomen.uivar = function(){
  console.log("Auuuuuuuuuuuuuuuuu!");
}

var vampiro = new Monstro(1.9, 78);
vampiro.altura = 1.9;
vampiro.peso = 78;
vampiro.morder = function(){
  console.log("Estou chupando seu sangue!");
}

lobisomen.descricao(); //Eu tenho 2.2m de altura e peso 110kg
lobisomen.uivar(); //Auuuuuuuuuuuuuuuuu!

vampiro.descricao(); //Eu tenho 1.9m de altura e peso 78kg
vampiro.morder(); //Estou chupando seu sangue!

{% endhighlight %}


Note que estamos definindo um _"rascunho"_ de como todo monstro deve ser, mesmo que possam ter métodos e atributos diferentes. E esses métodos diferenciados são definidos diretamente no objeto criado, ou seja, podemos ter uma infinidade de monstros diferentes usando apenas um único _"protótipo"_ inicial.

No nosso exemplo, onde temos apenas um tipo de cada monstro, a prototipação nos serve perfeitamente, mas se quisermos instanciar vários lobisomens por exemplo, teríamos que repetir o nosso código algumas vezes, ou utilizar a propriedade `prototype` para termos um comportamento parecido com a **Herança** que estamos acostumados.

Veja o seguinte exemplo, com o uso de `prototypes`:

{% highlight javascript linenos %}

function Monstro(altura, peso){
  this.altura = altura;
  this.peso = peso;
  
  this.descricao = function(){
    console.log("Eu tenho "+this.altura+"m de altura e peso "+this.peso+"kg");
  }
}

function Lobisomen(altura, peso){
  Monstro.call(this, altura, peso);
  this.uivar = function(){
    console.log("Auuuuuuuuuuuuuuuuu!");
  }
}
Lobisomen.prototype = new Monstro();

function Vampiro(altura, peso){
  Monstro.call(this, altura, peso);
  this.morder = function(){
    console.log("Estou chupando seu sangue!");
  }
}
Vampiro.prototype = new Monstro();

var lobisomen1 = new Lobisomen(2.2, 110);
var lobisomen2 = new Lobisomen(2.23, 105);
var vampiro1 = new Vampiro(1.85, 78);
var vampiro2 = new Vampiro(1.80, 71);

lobisomen1.descricao(); //Eu tenho 2.2m de altura e peso 110kg
lobisomen1.uivar(); //Auuuuuuuuuuuuuuuuu!

lobisomen2.descricao(); //Eu tenho 2.23m de altura e peso 105kg
lobisomen2.uivar(); //Auuuuuuuuuuuuuuuuu!

vampiro1.descricao(); //Eu tenho 1.85m de altura e peso 78kg
vampiro1.morder(); //Estou chupando seu sangue!

vampiro2.descricao(); //Eu tenho 1.8m de altura e peso 71kg
vampiro2.morder(); //Estou chupando seu sangue!

{% endhighlight %}

Como vocês podem ver, além de chamar o construtor do "objeto pai", precisamos substituir a propriedade **prototype** para termos acesso à todos os métodos do protótipo Monstro. 

Se você não está familiarizado com o uso do prototype, ele nada mais é que uma propriedade que contém uma cópia do seu objeto pai. Por exemplo, quando instanciamos uma data com `new Date()`, automaticamente a sua propriedade **prototype** é setada com `Date.prototype`, fazendo com que nosso objeto "herde" os métodos e propriedades de `Date` _(para mais informações sobre o **prototype**, confira esse [post][prototype-alura] no blog da [Alura][alura])_.


---

[ultimo-post]:                  {% post_url 2017-08-17-es6-o-guia-definitivo-parte-1 %}
[primeira-classe]:              https://medium.com/@angelorubin/javascript-first-class-function-fun%C3%A7%C3%B5es-de-primeira-classe-7ebf63d2c83a
[prototipacao]:                 https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Introduction_to_Object-Oriented_JavaScript
[prototype-alura]:              http://blog.alura.com.br/heranca-em-javascript/
[alura]:                        https://www.alura.com.br/