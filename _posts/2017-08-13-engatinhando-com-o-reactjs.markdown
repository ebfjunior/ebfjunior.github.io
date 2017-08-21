---
title:  "Engatinhando com o ReactJS"
date:   2017-08-13 14:50:00
categories: [frontend]
tags: [react, javascript]
excerpt_separator: <!--more-->
---

![ReactJS]({{ site.url }}/images/reactjs.jpg)

Fala pessoal! Como eu já falei pra vocês no meu [primeiro post][primeiro-post], atualmente estou na vibe do [ReactJS][reactjs], e pra ser sincero, foi **amor à primeira vista**! O React pode até ter virado uma modinha hoje em dia, mas é uma biblioteca tão incrível que eu acredito que ela veio para ficar, e é por isso que hoje vamos iniciar uma série sobre como criar uma aplicação em React do zero!

<!--more-->

Mas antes de entrarmos na nossa aplicação propriamente dita _<s>(já adianto que os amantes de música vão gostar!)</s>_, nesse artigo vamos falar sobre o que é o React e o básico da sua utilização.

## React... isso é de comer?

Mas afinal de contas, o que é esse tal React que todos tanto falam?

Bom, o React é uma **biblioteca** desenvolvida pelo pessoal do Instagram (e depois pelo Facebook) para a criação de **componentes reutilizáveis**. Resumindo, é uma forma de você desenvolver o seu site ou aplicação sem repetir um milhão de vezes aquela `div` que faz a mesma coisa pelo seu código.

Pode parecer pouco para uma biblioteca que é tão falada, mas lhes asseguro que não é. O React deixa o processo de desenvolvimento tão intuitivo que fez eu me perguntar como que antes eu criava minhas aplicações de outro jeito.

Além disso, a forma com que o React renderiza os nossos componentes é extremamente rápida com o **Virtual DOM**! Afinal, a galera do Facebook sabe como fazer as coisas, não é mesmo?

É importante frisar que, apesar de muitos o considerarem como tal, ele não é um concorrente direto do [AngularJS][angular]. Isso porque o Angular é um **framework** JS completo, que resolve vários tipos de problema, desde criação de componentes HTML até o gerenciamento do fluxo de dados da aplicação através do [Two-way Data Binding][data-binding], e o React serve *"apenas"* para a criação de componentes reutilizáveis.

Mas antes que você vá embora desse post por achar que o React é muito pouco para valer seu precioso tempo, eu gostaria de dizer que o fato dele se preocupar com apenas um problema não é exatamente uma coisa ruim. Na verdade, como ele foi desenvolvido para um único propósito, consequentemente temos um ganho maior de performance e praticidade. Além disso, existem outras bibliotecas que funcionam muito bem no ecossistema React e cuidam de todo o resto, como é o caso do [Redux][redux].

## Mais motivos para usar o React

Se você ainda não está convencido, posso citar mais alguns motivos para você dar uma chance para a nossa _"biblioteca modinha":_

### Tudo junto e misturado

O React utiliza uma forma diferente de renderizar o seu HTML. Ao invés de escrever markup e comportamento em lugares diferentes, você consegue escrever HTML diretamente no javascript através do [JSX][jsx].

Imagine só como seria lindo você poder gerar HTML sem concatenações caóticas de strings e sem a utilização de métodos _**write-only** (aquele código que você escreve uma vez e depois não consegue nunca mais ler e entender de novo)_ de alguma API do javascript.

_**Pois é, com o JSX isso é possível!**_

### ES6 por livre e espontânea pressão

Apesar de ser totalmente possível, é bem difícil você encontrar alguém que trabalhe com React sem usar a versão 6 do [EcmaScript][ecmascript] (ES2015 ou ES6). Isso porque os novos recursos da linguagem nos fornecem muito mais flexibilidade para escrevermos nossos códigos, principalmente com a implementação de classes e objetos (até que enfim, não é JavaScript?).

Aliás, se você ainda não teve experiência em conhecer o [ES6][es6], eu recomendo fortemente que você dê uma chance, afinal de contas o [ES8][es8] (ou ES2017) já está batendo na porta. A única parte chata é a necessidade de usar um [transpiler][transpiler] como o **Webpack+Babel** para suprir a falta de compatibilidade dos browsers.

Mas se você ainda assim preferir trabalhar com o **Javascript ES5**, basta adicionar uma biblioteca `create-react-class` e usar a sua API para criar os componentes, abrindo mão do nosso querido JSX.


### Muito mais que Web

Estamos falando de componentes reutilizáveis como se fossem um conceito inventado por alguém no ano de 2048, que utilizou uma máquina do tempo para trazer esta brilhante tecnologia até os dias atuais para revolucionar a forma com que criamos nossas aplicações, mas não é bem assim. 

A especificação e utilização de componentes reutilizáveis já existem à algum tempo, e não servem apenas para as páginas Web. Aliás, um outro meio que se beneficia muito desse conceito seria a plataforma mobile.

A equipe do Facebook também entendeu isso e criou o [React Native][react-native], uma biblioteca capaz de transpilar seu código JavaScript em apps nativas para **Android** e **IOS**. Ou seja, se você se dispor a aprender mais sobre o React, vai estar apenas à um passo para criar um aplicativo mobile para essas plataformas, sem ter que reescrever a mesma coisa em várias linguagens diferentes.

E o melhor de tudo isso? Sem aqueles apps híbridos que travam a cada clique que você dá<s>, assim como acontece com o Phonegap</s>.

---

## Renderização com o Virtual DOM

A estrela por trás do merecido sucesso do React e o principal responsável pela sua performance exemplar é o **Virtual DOM**. 

Todos sabem que fazer pesadas manipulações no **DOM** usando o famigerado [Vanilla JS][vanilla-js] pode não ser a tarefa mais rápida do mundo se você não tomar as devidas precauções ou se a sua página HTML é grande demais. Isso acontece porque o DOM foi implementado para ser uma maneira fácil de realizar a abstração de elementos HTML em uma estrutura de árvore, mas infelizmente esqueceram de considerar a performance ao fazer isso =(

Na verdade, esse problema vem ocorrendo com maior frequência nos últimos tempos, onde as **SPA (Single Page Applications)** vêm tomando cada vez mais espaço na Web, criando-se então, a necessidade de manipular elementos HTML o tempo todo, cada vez que usuário interage com a página.

E é aí que o Virtual DOM entra! O react guarda uma representação do DOM em memória. Quando você cria um componente, o método `render` é chamado e o mesmo é renderizado na tela. Se o estado do seu componente é alterado, o React é capaz de saber se o elemento precisa ser alterado ou não através do Virtual DOM, e se for o caso, aplicar a alteração apenas nos **nodes** necessários.

## Partindo para o que interessa

Agora chega de blá blá blá e mãos à obra! Como eu falei lá em cima, se queremos aproveitar todos os recursos do React, incluindo a engine JSX para a renderização de HTML dento do nosso JS, precisamos utilizar a implementação ES6 do Javascript. Com isso em mente, precisaríamos instalar e configurar o Webpack e o Babel para compilarem nosso código, já que os browsers hoje em dia ainda não suportam totalmente os recursos do ES6.

Para a nossa sorte, o pessoal do Facebook também criou uma ferramenta para que possamos inicializar e configurar nosso projeto sem termos que fazer todo esse trabalho manual.

E para usar é bem fácil. Para installar a biblioteca, rodamos a seguinte linha de comando:

{% highlight bash %}
npm install -g create-react-app
{% endhighlight %}

Note que utilizamos a opção `-g` para instalar globalmente a biblioteca, tornando-a disponível de qualquer lugar. 

Depois de instalada, basta que rodemos o comando `create-react-app meu-app-lindo`, sendo `meu-app-lindo` o nome do nosso app, para ter um aplicação totalmente instalada e configurada.

Se entrarmos na pasta `meu-app-lindo` que foi criada pelo script, vamos ver a seguinte estrutura de diretórios:

- `node_modules` : É a pasta onde ficam instaladas todas as bibliotecas necessárias <s>(ou nem tão necessárias assim)</s> para a nossa aplicação funcionar. 
- `public` : Como o próprio nome já diz, é a pasta pública da nossa aplicação, onde fica o index.html.
- `src` : É aqui que vai ficar toda a lógica do nosso app, e é onde a mágica acontece. Pode se preparar para colocar todos os seus componentes nessa pasta.
- `packages.json` : Um arquivo de configuração que o node utiliza na hora de iniciar a aplicação, para que possamos ter tudo rodando lindamente.

Para iniciarmos o nosso app, basta que rodemos o comando `npm start`, dentro do diretório `meu-app-lindo`. Uma página Web vai ser aberta, mostrando o nosso primeiro componente!

Pode não parecer grande coisa à princípio, afinal, é só um componente genérico qualquer. Mas é importante que entendamos como ele funciona.

Vamos dar uma olhada no arquivo `src/App.js`.


{% highlight javascript linenos %}

import React, { Component } from 'react';
import logo from './logo.svg';
import './App.css';

class App extends Component {
  render() {
    return (
      <div className="App">
        <div className="App-header">
          <img src={logo} className="App-logo" alt="logo" />
          <h2>Welcome to React</h2>
        </div>
        <p className="App-intro">
          To get started, edit <code>src/App.js</code> and save to reload.
        </p>
      </div>
    );
  }
}

export default App;

{% endhighlight %}

Esse arquivo representa o nosso componente propriamente dito. Por padrão, o script do Facebook cria um único componente chamado `App`.

Nas primeiras linhas estamos apenas importando alguns arquivos necessários para a criação do componente. Se você achou estranha a sintaxe de import, não se preocupe. Provavelmente você não está familiarizado com os recursos do ES6, mas eu vou abordar sobre esse assunto no próximo post.

Na linha 5, estamos criando o nosso componente utilizando a notação de classe, recurso também do ES6. Essa é apenas uma das maneiras de se criar um componente, e também a mais completa e flexível. Como você pode ver, estamos herdando da classe Componente (que acabamos de importar nas primeiras linhas do arquivo).

O método `render` da linha 6 é executado no momento que o componente é criado, e também toda vez que o React identifica que o seu estado mudou, através de um *diff* realizado no **Virtual DOM**. Esse método deve retorno o HTML do nosso componente, e é aí que o **JSX** entra. Note que estamos retornando diretamente o HTML, se a utilização de concatenações de strings, nem nada do tipo. Apenas o bom e velho HTML. 

Por último, mas não menos importante, temos a linha 21, responsável por exportar a nossa classe para que ela esteja acessível em outros arquivos.

Mas como utilizamos o componente que acabamos de criar? Simples! Confira agora o arquivo `src/index.js`:

{% highlight javascript linenos %}

import React from 'react';
import ReactDOM from 'react-dom';
import App from './App';
import './index.css';

ReactDOM.render(
  <App />,
  document.getElementById('root')
);

{% endhighlight %}

Note que além de importar a biblioteca `React`, estamos importando também o `ReactDOM`, que é o responsável por fazer a conexão e inserção do nosso componente com o DOM propriamente dito.

E olha só quem apareceu ali também nos imports. Isso mesmo, o componente `App`, que acabamos de criar! 

Então a única coisa que precisamos fazer é chamar o método `ReactDOM.render`, passando como parâmetros o componente `<App/>` e algum elemento HTML que funcionará como container. Nesse caso estamos utilizando uma `div` com id `root`, que está no arquivo `public/index.html`.

---

Então é isso galera. Esse foi apenas o primeiro artigo de uma série que estou fazendo sobre o React, e espero que vocês tenham gostado! Vocês podem conferir o [projeto][repositorio] gerado nesse artigo, e não esqueçam de deixar seus comentários com dúvidas, críticas, sugestões, etc.

**Até a próxima!**


[primeiro-post]:      {% post_url 2017-08-09-comecando-com-o-pe-direito %}
[reactjs]:            https://facebook.github.io/react/
[angular]:            https://angularjs.org/
[redux]:              http://redux.js.org/
[jsx]:                https://jsx.github.io/
[data-binding]:       https://docs.angularjs.org/guide/databinding
[ecmascript]:         https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Language_Resources
[react-native]:       https://facebook.github.io/react-native/
[transpiler]:         https://scotch.io/tutorials/javascript-transpilers-what-they-are-why-we-need-them
[vanilla-js]:         http://vanilla-js.com/
[es6]:                http://es6-features.org/#Constants
[es8]:                https://hackernoon.com/es8-was-released-and-here-are-its-main-new-features-ee9c394adf66
[repositorio]:        https://github.com/ebfjunior/blog-posts/tree/master/engatinhando-com-o-reactjs/meu-app-lindo