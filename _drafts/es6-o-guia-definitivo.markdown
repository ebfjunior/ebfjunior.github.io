---
title:  "ES6: O Guia Definitivo"
date:   2017-08-17 11:11:23
categories: [frontend]
tags: [javascript, es6, guia]
excerpt_separator: <!--more-->
---

![ES6](/images/es6.jpg)


Ok, Ok... Eu sei que eu disse no meu [último post][ultimo-post] que eu estava iniciando uma série sobre como criar uma aplicação em **ReactJS** do zero. Mas como o meu objetivo é utilizar vários recursos do **ES6**, enquanto escrevia o próximo artigo da série eu vi que estava parando demais para explicar os novos recursos da linguagem. Por isso preferi dar uma breve pausa na série para fazer um **Guia Definitivo** sobre o ES6!

<!--more-->

O **EcmaScript 6** _(ou **ES2015**)_ não é exatamente novo, mas muitos desenvolvedores ainda têm uma certa dificuldade em utilizá-lo em seus projetos, seja por falta de conhecimento ou por _**Bocardia Mental**_ mesmo. Como são muitas as novidades vindas com a versão, vou tentar conter minha mão nervosa e ser o mais breve possivel<s>, mas me perdoem se eu não conseguir</s>.

# Por que tanta mudança?

Quem trabalha com desenvolvimento Web à um pouco mais de 5 anos, deve se lembrar bem o quão penoso era fazer um site que funcionasse bem em todos os navegadores. Isso por que, desde a chamada [Guerra dos Navegadores][guerra-dos-navegadores], criou-se a cultura de que cada browser deveria criar suas próprias implementações e padrões para a utilização de recursos frontend e obrigar todos os desenvolvedores a seguirem suas diretivas "soberanas". Com isso, quando saia uma nova versão do Javascript, cada browser implementava sua própria versão das especificações e _**BUM!!**_ Explosão de `IF/ELSE` por todo lado para tratar as peculiaridades dos navegadores.

Esse foi o principal motivo para o Javascript não ter evoluido como se esperava por um longo período de tempo. Afinal, como iriam liberar uma nova versão se os browsers ainda estavam brigando para ver quem implementava os recursos da versão atual da maneira mais _bizarra_ possível?

Para resolver o problema foi criado o [TC39][tc39], um comitê formado principalmente por membros das principais desenvolvedoras de browsers, que ficaria responsável pela implementação das novas versão do Javascript, que a partir de então seria anualmente. Com isso, foi adotada uma nova nomenclatura baseada no ano da versão _(como ES2017)_, ao invés de números _(como ES6)_. Porém, quando esta nova abordagem foi anunciada, muitos já conheciam a nova versão do Javascript como ES6.

# Como usar?

O **TC39** pode estar ajudando bastante no crescimento padronizado do Javascript, facilitando a implementação de suas especificações por parte das desenvovledoras, mas ainda assim, o ES6 trouxe um conjunto um conjunto gigantesco de mudanças, fazendo com que o **ES2015** ainda não tenha suporte total em todos os browsers. Hoje, as maiorias das especificações já foram implementadas nos browsers (a lista completa e atualizada de compatibilidade pode ser vista [aqui][compatibilidade-es6]), mas infelizmente ainda temos que considerar os browsers mais antigos que ainda são bem utilizados (como o **Internet Explorer 11**).

Mas calma, nem tudo está perdido. Existem várias bibliotecas que prometem implementar _"na mão"_ as funcionalidades do ES6, mas a maneira mais interessante de se trabalhar é com a utilização de um [transpiler][transpiler] como o [Babel][babel], em conjunto com o [Webpack][webpack]. Podemos abordar como configurar o **Webpack+Babel** em um próximo post, mas para testar os recursos abordados neste artigo, você poderão utilizar o [Babel Online][babel-online].

# Recursos da nova versão

Eu prometi que não iria me estender muito, então vamos finalmente partir para as novidades do ES6.

## Let e Const

Para entender os benefícios de se declarar variáveis utilizando `let` e `const`, precisamos primeiro entender como funciona a forma original, com o uso de `var`.

Primeiramente, as variáveis declaradas com `var` possuem um **escopo** de função ao invés de um escopo de bloco. Para entender, vejamos esse exemplo:

{% highlight javascript linenos %}
function xpto(){ //cria um escopo de função
    var a = 1;
    console.log(a); //exibe o número 1

    if(true){
        var a = 2;
        console.log(a); //exibe o número 2
    }

    console.log(a); //exibe o número 2
}
{% endhighlight %}

Talvez o comportamento esperado era que todas as variáveis criadas dentro de blocos (como `if`, `for` ou `while`) estivessem disponíveis apenas dentro de seus respectivos blocos. Mas com o Javascript não é tão simples assim. Como no Javascript os escopos pertencem às funções, qualquer variável declarada dentro da função irá ser _"içada"_ para o topo de seu escopo, graças ao conceito de [Hoisting][hoisting].

No **ES5**, quando queríamos criar uma variável pertencente apenas à um escopo restrito, precisávamos utilizar [IIFEs][iife] (**Immediately Invoked Function Expression** ou **Funções Imediatas**), como no exemplo a seguir:

{% highlight javascript linenos %}
function xpto(){ //cria um escopo de função
    var a = 1;
    console.log(a); //exibe o número 1

    if(true){
        (function(){ //cria um escopo de função
            var a = 2;
            console.log(a); //exibe o número 2
        })();
    }

    console.log(a); //agora sim exibe o número 1 =D
}
{% endhighlight %}

Mas no **ES6** podemos utilizar as diretivas `let` e `const` para declarar variáveis com escopo de bloco, onde `const` declara uma constante e `let` declara uma variável propriamente dita. Então o código acima ficaria assim em ES6:

{% highlight javascript linenos %}
function xpto(){ //cria um escopo de bloco
    const a = 1;
    console.log(a); //exibe o número 1

    if(true){ //cria um escopo de bloco
        const a = 2;
        console.log(a); //exibe o número 2
    }

    console.log(a); //exibe o número 1
}
{% endhighlight %}

Mas existe um pequeno problema ao se declarar constantes com `const`. Naturalmente, você imagina que o valor nunca vai poder ser alterado posteriormente, como toda boa constante deveria ser. E isso pode ser verdade quando estamos trabalhando com tipos simples de constantes, como números e strings, mas não podemos dizer o mesmo sobre os objetos. Veja o exemplo a seguir:

{% highlight javascript linenos %}
const pessoa = {
  nome: "John",
  sobrenome: "Doe"
}

console.log(pessoa.sobrenome); //exibe Doe

pessoa.sobrenome = "Smith";

console.log(pessoa.sobrenome); //exibe Smith
{% endhighlight %}

Como você viu, podemos alterar livremente as propriedades de um objeto, mesmo tendo sido declarado como constante. Mas antes de você se desesperar, existem alternativas para lidar com o problema, como o [Object.freeze][object-freeze] e o [Immutable.js][immutable].

## Default parameters

Nas versões anteriores ao ES6, quando queríamos tratar um parâmetro opcional, precisávamos fazer isso manualmente, como no exemplo à seguir:

{% highlight javascript linenos %}
function incrementar(numero, incremento){
  incremento = incremento || 1;
  return numero + incremento;
}


console.log(incrementar(10)); //exibe o número 11
{% endhighlight %}

Agora, conseguimos especificar o valor padrão de um parâmetro já na declaração da função, reduzindo a quantidade de código escrito:

{% highlight javascript linenos %}
function incrementar(numero, incremento=1){
  return numero + incremento;
}


console.log(incrementar(10)); //exibe o número 11
{% endhighlight %}

## Rest parameters

Para criar uma função que pode receber um quantidade indeterminada de parâmetros, podíamos usar a variável `arguments` e fazer o seguinte:

{% highlight javascript linenos %}
function adicionaDependentes(pessoa){
  var i = 1;
  var count = arguments.length;
  while(i < count){
    pessoa.dependentes.push(arguments[i]);
    
    i++;
  }
  
  
  return pessoa;
}

var pessoa = {nome: "John Doe",  dependentes: []};
adicionaDependentes(pessoa, "Jack", "Mary", "James");
{% endhighlight %}

Note que precisamos fazer muita coisa manual, como controlar a posição inicial do array `arguments`, incrementar o contador dentro do loop (ou utilizar o loop `for`), além de o resultado não ser um código bonito de se ver. Com o ES^, podemos especificar um **rest parameter** através do uso de `...` antes do nome do parâmetro. Veja a seguir:

{% highlight javascript linenos %}
function adicionaDependentes(pessoa, ...dependentes){
  for(const dependente of dependentes){
    pessoa.dependentes.push(dependente);
  }

  return pessoa;
}

var pessoa = {nome: "John Doe",  dependentes: []};
adicionaDependentes(pessoa, "Jack", "Mary", "James");
{% endhighlight %}

Bem melhor, não?

**BÔNUS:** Reparem que no código acima foi utilizado o loop `for...of`, que é bem parecido com o `for...in`, porém o resultado da iteração é o objeto propriamente dito dentro do array, e não o seu índice. Assim, no exemplo, nós não precisamos acessar um dependente como `dependente[i]`, e sim acessando diretamente a variável.






[ultimo-post]:                  {% post_url 2017-08-13-engatinhando-com-o-reactjs %}
[guerra-dos-navegadores]:       http://docente.ifrn.edu.br/moisessouto/disciplinas/autoria-web/a-verdadeira-historia-da-internet-guerra-dos-navegadores
[tc39]:                         http://www.ecma-international.org/memento/TC39.htm
[compatibilidade-es6]:          https://kangax.github.io/compat-table/es6/
[transpiler]:                   https://scotch.io/tutorials/javascript-transpilers-what-they-are-why-we-need-them
[babel]:                        https://babeljs.io/
[webpack]:                      https://webpack.js.org/
[babel-online]:                 http://babeljs.io/repl/#?babili=false&evaluate=true&lineWrap=false&presets=es2015%2Creact%2Cstage-2&targets=&browsers=&builtIns=false&debug=false&code_lz=Q
[hoisting]:                     http://loopinfinito.com.br/2014/10/29/hoisting-e-escopo-em-javascript/
[iife]:                         https://developer.mozilla.org/pt-BR/docs/Glossario/IIFE
[object-freeze]:                https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/freeze
[immutable]:                    https://facebook.github.io/immutable-js/