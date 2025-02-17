# **JavaScript - IV - Requisições**
## Instruções Iniciais:

1. Instalem o Node.js na máquina de vocês, na ultima versão disponível do programa: https://nodejs.org/en/
2. Instalem também o Postman na máquina de vocês: https://www.postman.com/downloads/
3. Forkem o repositório para a conta pessoal de vocês.
4. Clonem no computador de vocês o repositório forkado em suas contas particulares.

**_ATENÇÃO_: Não modifiquem o conteúdo do projeto original forkado, apenas a que você copiou e renomeou!**

### Façam suas perguntas através do DontPad

[http://dontpad.com/On13-JSIV](http://dontpad.com/On13-JSIV)

----

## **1. APIs**

Bom, para começar, precisamos primeiro definir o que são APIs. Porque se fala tanto sobre APIs e endpoints dentro do mundo da programação?

Nós, humanos, desenvolvemos formas intermediárias para nos comunicarmos - através da fala, da escrita ou de gestos. Da mesma forma, também foi desenvolvida uma forma para que uma aplicação consiga se comunicar com os seus servidores e com outras aplicações.

![api-diagram](assets/api-diagram.png)

**APIs** - ou Application Programming Interface - **são uma série de métodos e funções que permitem que aplicações acessem dados e interajam com componentes de softwares externos, sistemas operacionais ou microsserviços**. Uma API disponibiliza uma interface de comunicação e de integração entre aplicações.

**Simplificando: uma API entrega uma requisição de um usuário (user request) para um sistema e retorna ao usuário a resposta do sistema (response)**.

APIs são muito utilizadas porque elas são práticas e facilitam o desenvolvimento de uma aplicação. Exemplo: você está criando uma página de formulário de cadastro ao seu sistema. No campo de endereço, você precisa que ele seja automaticamente encontrado e preenchido a depender do CEP inserido pelo usuário na tela.

Ao invés de criar do zero uma aplicação que faça essa busca e preenchimento, você pode utilizar uma API já pronta que realiza essa função que você precisa - no caso, a [ViaCEP](https://viacep.com.br/), [ApiCEP](https://apicep.com/api-de-consulta/), dentre outras.

É possível classificar APIs de diversas formas, mas para fins do nosso estudo, cabe trazer as SOAP APIs e as REST APIs.

**1. SOAP APIs:** SOAP - ou Simple Object Access Protocol - APIs são protocolos de comunicação web e são usados para transmitir informações e dados via HTTP/HTTPS. Aqui, os dados são retornados no formato xml (uma estrutura semelhante a do HTML, mas que não possui as tags pré-definidas).

**2. REST APIs:** A arquitetura REST - ou Representational State Transfer - é amplamente utilizada dentro do desenvolvimento de APIs. Isso porque, ao contrário da arquitetura SOAP, as REST APIs tem um modelo mais simples de requisição. O nosso estudo será concentrado nelas.

**IMPORTANTE:** Cada REST API possui uma documentação, dispondo sobre o modo que deve ser feita essa requisição, e quais os tipos de requisições que são aceitas pela API. Lembrem-se sempre de ler a documentação.

O processo de requisição de uma REST API envolve quatro passos específicos:

### **1) Método ou o verbo da requisição HTTP e URL:**

De modo geral, a requisição de uma REST API é feita se utilizando de dois requisitos: **a URL disponibilizada para utilização da API (HTTP protocol) e o método HTTP que você precisa**.  

Existem muitos métodos HTTP, mas os mais usados são os seguintes:

| Método   |      Função      |  Status de Retorno |
|----------|:-------------:|------:|
| GET |  Traz informações | 200 |
| POST |    Cria um novo item   |   201 |
| PUT | Atualiza um item |    200 |
| DELETE | Remove um item |    200 |

**IMPORTANTE:** É preciso saber quais métodos são aceitos pela API. A descrição dos métodos que são aceitos normalmente é feita na documentação da API em específico.

### **2) Input (opcional):**

A API pode pedir que informações específicas constem dentro do *header* e do *body* da requisição e, de forma geral, essas especificidades estão dispostas dentro da documentação de uma API.

Essas informações específicas podem ser um parâmetro de pesquisa, ou um token de autenticação, dentre outras informações.

### **3) Processamento no back-end:**

Com o envio da requisição, ela é processada dentro da API. A depender da requisição pedida, cabe ao sistema do back-end encontrar informações, atualizar dados, criar um dado novo, ou até mesmo deleta-lo.

### **4) Resposta:**

Com o processamento da requisição, a API retorna uma resposta ao usuário. Essa resposta é composta por um **código de status do retorno numérico e textual**, **um conjunto de cabeçalhos da resposta**, e do **próprio dado retornado no formato JSON**.

Relação dos códigos de status de retorno: https://developer.mozilla.org/pt-BR/docs/Web/HTTP/Status.

---

## **2. JSON**

JSON é a abreviação de *JavaScript Object Notation* ou Notação de Objeto Javascript. É uma sintaxe para armazenar e transferir dados. Trata-se de uma string que se parece bastante com um objeto JavaScript.

```Javascript
[
  {
    "nome": "Iza",
    "idade": 1,
    "castrado": true,
    "cor": ["branco", "preto"],
    "caracteristicas": ["fofinha", "sociável"]
  },
  {
    "nome": "Beyoncé",
    "idade": 1,
    "castrado": true,
    "cor": ["amarelo", "branco", "marrom", "dourado"],
    "caracteristicas": ["brincalhão", "dengoso"]
  },
]
```

O formato JSON é amplamente utilizado na resposta de requisições por ele ser leve e fácil de ler e escrever. Nota-se que as propriedades necessariamente tem que estar entre aspas duplas.

Na sua forma original, o JSON tem esse formato:

```Javascript
{["\"id"\:"\"10001"\"\"name"\:"\"ABC"\]}
```

Para que possamos utiliza-lo dentro do JavaScript, nos servimos do método JSON.parse(data), que transforma a data string do JSON em um objeto JavaScript para ser manipulado e o retorna.

---

## **3. Tipos de Requisição a APIs**

### **a. Ok, mas o que é uma requisição assíncrona?**

![sync-async](assets/sync-async.gif)

As requisições podem ser tanto síncronas quanto assíncronas.

No JavaScript, tradicionalmente, a execução do código é feita de forma síncrona.

Encadeamento único significa que um comando está sendo executado por vez. Síncrono significa um de cada vez, ou seja, uma linha de código está sendo executada ao mesmo tempo para que o código apareça. Então, em JavaScript, uma coisa está acontecendo de cada vez.

Só que lá em 1999, surgiu o AJAX - em síntese *Asynchronous JavaScript and XML* (ou XML e JavaScript Assíncrono) - que possibilitou a realização de chamadas assíncronas.

As chamadas assíncronas rompem com a regra da sincronia, permitindo a ocorrência de mais de um evento de cada vez dentro do JavaScript. Com ela, eu consigo uma requisição em um trecho de código, receba um aviso quando os dados forem recebidos (o famoso callback) e permitindo que o navegador siga no seu trabalho enquanto a sua requisição estiver sendo processada. 

Ou seja, com a chamada assíncrona não é necessário recarregar a página após uma requisição.

### **b. XMLHttpRequest**

Depois de entender sobre APIs, a gente pensa: tá, mas como eu faço uma requisição em uma API?

Existem alguns métodos e objetos que foram criados para realizar essas requisições.

Um dos pioneiros foi o XMLHttpRequest (XHR) - que é um objeto utilizado para interagir com servidores. São usados para receber dados de uma URL sem ter que atualizar de novo a página - assim, é criado uma requisição assíncrona.

Apesar de ter "XML" no seu nome, a requisição de XMLHttpRequest pode receber qualquer tipo de dado.

### **Como é uma requisição XMLHttpRequest**

```Javascript
// cria um novo construtor XMLHttpRequest
const request = new XMLHttpRequest();
const metodo = "GET";
const url = "https://exemplo.com";

// inicializa a requisição
request.open(metodo, url, true);

// adiciona um evento para ser ativado quando o readyState mudar
request.addEventListener("readystatechange", function () {
  // verifica se a conexão foi bem sucedida
  if (request.readyState == 4 && request.status == 200) {
    // atribui a uma nova variável o JSON já transformado em objeto Javascript (através do parse())
    const data = JSON.parse(request.response);
  }
})

// envia a requisição para o servidor
request.send();
```
### **c. *Fetch***

Atualmente, a maioria das requisições efetuadas no JavaScript se utilizam da **API Fetch**. Trata-se de uma interface JavaScript para acessar e manipular partes de uma requisição HTTP - como o pedido e as respostas obtidas.

Como isso é efetuado? Através do método `fetch()`.

``` JavaScript
var myHeaders = new Headers();

var myInit = { method: 'GET',
               headers: myHeaders,
               mode: 'cors',
               cache: 'default' };

var myRequest = new Request('flowers.jpg', myInit);

fetch(myRequest)
.then(function(response) {
  return response.blob();
})
.then(function(myBlob) {
  var objectURL = URL.createObjectURL(myBlob);
  myImage.src = objectURL;
})
.catch((error) => {
  return error;
});

```

### **d. Qual a diferença entre eles?**

O método XMLHttpRequest foi revolucionário por possibilitar uma requisição assíncrona - onde é possível obter dados de uma API sem congelar a tela e também sem precisar de uma atualização total da página.

A API Fetch é uma alternativa mais moderna ao XMLHttpRequest. As interfaces  marcadas de Headers, Request e Response possibilitam maior consistência nas requisições, menos chances de erros na escrita do código, com uma escrita mais simples e permitindo o uso das Promises.

`fetch()` é um método mais moderno, simples e compreensível, o que explica a sua grande usabilidade nos dias de hoje.

## **4. Introdução às Promises**

### **a. Sobre as *promises***

Deu para perceber no tópico acima que o método `fetch()` inicia um processo para "pegar" um recurso em uma rede ou em uma API, retornando algo dentro do `then()/catch()`. 

O que esse `.then()` nos trás é a resolução de uma Promise - que representa um valor que eventualmente retornará após uma operação ser integralmente realizada.

**Promise é um objeto que representa o sucesso ou o fracasso de uma operação assíncrona, e o seu eventual valor de retorno**.

Logo, a promise tem três estados:

a) **pending:** status inicial, ainda pendente de completude ou rejeição.

b) **fulfilled:** operação com sucesso.

c) **rejected:** operação rejeitada.

A Promise serve como um proxy para um valor que ainda não se conhece no momento em que a promessa é criada. Ao invés de retorna-lo de forma síncrona, ele o retorna o valor num determinado momento no futuro.

### **b. Anatomia das *promises***

Para criar uma nova Promise, é necessário usar a palavra-chave `new`. Existe um construtor nativo e ele retorna o objeto `Promise`.

O callback (executor) da `Promise` recebe dois parâmetros: `resolve` e `reject`. Esses parâmetros são funções geradas pelo construtor

Depois disso, é possível usar os métodos:

1.  `then()` (para quando há sucesso na execução da `promise`); e 

![.then()](assets/.then().gif)

2. `catch()` (para quando a `promise` é rejeitada).

![.catch()](assets/.catch().gif)

3. `finally()` (que é acionado em qualquer hipótese - de sucesso ou rejeição da Promise)

**Anatomia do código:**

```JavaScript

const promise = new Promise((resolve, reject) => {
  if (condicao) {
    resolve("resolvido!"); // dado é retornado para o then
  } else {
    reject("aaahh errooou"); // entra no catch
  }
});

promise
  .then((data) => {
    console.log(data);
  })
  .catch((err) => {
    console.log(err);
  });

```
### **c. async/await**

A palavra-chave `async` é usada em declarações ou expressões de funções. Assim, elas se tornam funções assíncronas e permitem o uso do `await` dentro delas.

Elas normalmente são usadas quando é necessário esperar a resolução desta para dar continuidade às operações seguintes.

Ou seja, o `async` faz com que uma função automaticamente retorne uma Promise.

Ao se usar o `async`, você deve marcar com o `await` as funções e métodos que retornarão uma Promise.

```JavaScript
function resolveDoisSegundos(x) {
  return new Promise(resolve => {
    setTimeout(() => {
      resolve(x);
    }, 2000);
  });
};

const expFuncaoAsync = async x => {
  const a = await resolveDoisSegundos(20); // aguarda essa promise ser resolvida antes de continuar
  return x + a;
};
```

O `await` pausa a função `expFuncaoAsync()`, marcada com o `async`, até que a Promise dentro da função `resolveDoisSegundos()` seja resolvida. Então o valor retornado é atribuído à variável e o código de `expFuncaoAsync()` continua de onde parou.

### **async/await ou then()?**

Percebam que o `async/await` podem ser utilizados para criar uma requisição assíncrona ao invés de uma `Promise`. Mas, aí fica a dúvida: qual eu devo utilizar?

Primeiramente, é preciso dizer que a chegada do `async/await` não excluiu o uso de Promises - já que quando uma função assíncrona é retornar uma Promise. O que o `async/await` faz é simplificar o uso das Promises.   

```JavaScript

async function getDados(url) {
    const response = await fetch(url);
    const json = await response.json();
    return json;
}
getDados(url)
      .then(res => console.log(res))
      .catch(err => console.error(err));

```

Pessoalmente, eu entendo que `async/await` deixa o código mais legível e fácil de entender ao invés de concatenar vários `then()`.

Por outro lado, o comando `await` só funciona dentro de uma função `async` - que precisa ser criado apenas para poder executar o comando `await`, enquanto as Promises com o `then()` podem ser usadas em qualquer lugar.

Há também questões mais técnicas de performance, tratamento de erros e memória - mas, considerando que essa aula é mais inicial, deixo esse artigo para quem quiser se aprofundar sobre o tema: https://blog.pusher.com/promises-async-await/

---

## **Links Úteis:**

### **Requisição a APIs**

https://developer.mozilla.org/pt-BR/docs/Glossary/API

https://developer.mozilla.org/pt-BR/docs/Web/HTTP/Status

https://pt.wikipedia.org/wiki/Interface_de_programa%C3%A7%C3%A3o_de_aplica%C3%A7%C3%B5es

https://developer.mozilla.org/en-US/docs/Web/API

https://rockcontent.com/br/blog/rest-api/

https://www.webscrapingapi.com/beginners-guide-apis/

https://searchapparchitecture.techtarget.com/definition/RESTful-API

### **JSON**

https://www.json.org/json-en.html

https://www.devmedia.com.br/o-que-e-json/23166

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON/parse

### **CORS**

https://medium.com/@baphemot/understanding-cors-18ad6b478e2b

https://geekflare.com/cors-basics/

https://medium.com/@alexandremjacques/entendendo-o-cors-parte-8331d0a777e1

https://pt.wikipedia.org/wiki/Cross-origin_resource_sharing

### **XMLHttpRequest**

https://www.sitepoint.com/xmlhttprequest-vs-the-fetch-api-whats-best-for-ajax-in-2019/

https://pt.wikipedia.org/wiki/XMLHttpRequest

https://developer.mozilla.org/pt-BR/docs/Web/API/XMLHTTPRequest


### **Requisições síncronas e assíncronas**

https://code.tutsplus.com/tutorials/event-based-programming-what-async-has-over-sync--net-30027

https://developer.mozilla.org/pt-BR/docs/Web/API/XMLHttpRequest/Synchronous_and_Asynchronous_Requests

https://en.wikipedia.org/wiki/Asynchrony_(computer_programming)


### **Fetch**

https://developer.mozilla.org/pt-BR/docs/Web/API/Fetch_API/Using_Fetch

https://developer.mozilla.org/en-US/docs/Web/API/fetch

### **Promises**

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/Promise

https://www.freecodecamp.org/news/javascript-promises-explained/

https://dev.to/lydiahallie/javascript-visualized-promises-async-await-5gke

### **Async/Await**

https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Operators/async_function

https://www.alura.com.br/artigos/async-await-no-javascript-o-que-e-e-quando-usar

https://blog.pusher.com/promises-async-await/




