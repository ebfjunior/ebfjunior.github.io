---
title:  "ES6: O Guia Definitivo - Parte 2"
date:   2017-08-21 11:11:23
categories: [frontend]
tags: [javascript, es6, guia]
excerpt_separator: <!--more-->
---

![ES6](/images/es6.jpg)

Fala galera! Já deu pra ver a pancada de funcionalidades que vieram junto com o **ES6**, não é? São tantos os novos recursos da linguagem, que eu não consegui falar nem sobre a metade deles no post [ES6: O Guia Definitivo - Parte 1][ultimo-post]. Então antes de me estender muito, vamos seguir com as novidades do ES6!

<!--more-->

## Destructuring assignments

Não é incomum precisarmos criar variáveis intermediárias para dados que vêm de uma estrutura como `Arrays` ou `Hashs`, quando o objetivo é o reaproveitamento de código.

Você com certeza já fez muitos códigos como os que seguem:

{% gist a38a7bfab9f897bb7095a1cc0b27f309 %}

Não é lá muito elegante, mas ainda é melhor do que repetir toda a estrutura do seu Array/Objeto várias vezes para usar algum determinado valor. Mas com a chegada do ES6 nós ganhamos o versátil e poderoso recurso de **Destructuring**.

Destructuring é exatamente você desestruturar o seu elemento e automaticamente criar variáveis com seus respectitivos valores. É como se estivéssemos extraindo os valores de Arrays e Objetos!

Então vejamos o exemplo acima, já com o uso do **Destructuring**:

{% gist 063770077fdaa86340061ab86c909d6d %}


## Orientação a objetos

Um dos recursos mais aguardados _(e polêmicos)_ do *ES6* é o suporte à **Classes** de objetos. A verdade é que o nosso querido **Javascript** sempre foi uma linguagem extremamente flexível, e por isso existem muitas formas de você representar um objeto, desde a declaração de um simples **JSON** até uma [função de primeira classe][primeira-classe].

Isso acontece porque, até o **ES5**, o Javascript se utilizava apenas da [prototipação][prototipacao] para implementar a **Orientação a Objetos**. Com isso, temos a possibilidade de instanciar uma simples função, e o próprio Javascript faz o **binding** da variável `this` de acordo com o seu escopo, ganhando então o comportamento esperado de um objeto.

Vamos exemplificar como funciona a Orientação a Objetos por prototipação:

{% gist 510d98a3fd9a5c63841e6f11c7b2c792 %}

Note que estamos definindo um _"rascunho"_ de como todo monstro deve ser, mesmo que possam ter métodos e atributos diferentes. E esses métodos diferenciados são definidos diretamente no objeto criado, ou seja, podemos ter uma infinidade de monstros diferentes usando apenas um único **protótipo** inicial.

No nosso exemplo, onde temos apenas um tipo de cada monstro, a **prototipação** nos serve perfeitamente, mas se quisermos instanciar vários lobisomens por exemplo, teríamos que repetir o nosso código algumas vezes, ou utilizar a propriedade `prototype` para termos um comportamento parecido com a **Herança** que estamos acostumados.

Veja o seguinte exemplo, com o uso de `prototypes`:

{% gist a5624eb381766bf90e62eca564dbb553 %}

Como vocês podem ver, além de chamar o construtor do "objeto pai", precisamos substituir a propriedade **prototype** para termos acesso à todos os métodos do protótipo Monstro. 

Se você não está familiarizado com o uso do prototype, ele nada mais é que uma propriedade que contém uma cópia do seu objeto pai. Por exemplo, quando instanciamos uma data com `new Date()`, automaticamente a sua propriedade **prototype** é setada com `Date.prototype`, fazendo com que nosso objeto "herde" os métodos e propriedades de `Date` _(para mais informações sobre o **prototype**, confira esse [post][prototype-alura] no blog da [Alura][alura])_.

### Suporte a Classes do ES6

O exemplo acima ficaria assim se for escrito na especificação do ES6, utilizando o suporte à Classes de objetos:

{% gist c88bb6cd2de52a2bb62869ee89c61def %}

Tudo bem, o código pode não ter ficado menor, mas com certeza ficou mais legível.

O método `constructor` é executado toda vez que um novo objeto é instanciado, e quando estamos instanciando uma classe “filha”, podemos usar o método `super` para chamar o construtor do pai.

Note que estamos utilizando o prefixo `_` antes dos nomes de atributos da nossa classe `Monstro`. Essa é apenas uma **convenção** para a definição de atributos privados da nossa classe, e por se tratar apenas de uma convenção, entende-se que a linguagem não vai fazer nenhum esforço para bloquear o acesso desses atributos de fora da nossa classe. Mas é um bom padrão para identificarmos se um atributo é privado toda vez que batemos o olho nele.

E a parte boa é que ganhamos [sugar syntax][sugar-syntax] para os nossos **Getters and Setters**. Veja um exemplo:

{% gist fc3c08353006c6eaf305f9020a4865b2 %}

Mesmo a classe não possuindo um atributo `raio`, nós podemos utilizar códigos como `circunferencia.raio` ou `circunferencia.raio = x` graças às diretivas `get` e `set` na definição da nossa classe.

E se você está se perguntando _"Mas onde estão os métodos estáticos?"_, pode ficar tranquilo que o pessoal do **TC39** não se esqueceu deles. Basta utilizar a diretiva `static` antes da definição do método:

{% gist 72eac6ae9a6506adb625f33d683a62a9 %}

E vale lembrar duas últimas coisas sobre o **Suporte a Classes** do **ES6**: 

- A Declaração de classes não são **hoisted** como acontece com as funções. Ou seja, primeiro precisamos declarar nossa classe para só depois utilizá-la.

- Todos os itens que foram abordardos nesse tópico não passam de **sugar syntaxes** para a **prototipação** padrão do **ES5**. Com isso temos uma maneira mais semântica de aplicar a orientação à objetos em nossos projetos através da declaração de classes, mas para o Javascript, tudo continua sendo a boa e velha prototipação. E isso não é necessariamente uma coisa ruim, porque nos dá a possibilidade de fazer um _"mix"_ das duas abordagens =) 

---

[ultimo-post]:                  {% post_url 2017-08-17-es6-o-guia-definitivo-parte-1 %}
[primeira-classe]:              https://medium.com/@angelorubin/javascript-first-class-function-fun%C3%A7%C3%B5es-de-primeira-classe-7ebf63d2c83a
[prototipacao]:                 https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Introduction_to_Object-Oriented_JavaScript
[prototype-alura]:              http://blog.alura.com.br/heranca-em-javascript/
[alura]:                        https://www.alura.com.br/
[sugar-syntax]:                 https://www.quora.com/What-is-syntactic-sugar-in-programming-languages