Onde está "ola mundo"?

<div style="display: inline-block; height: 10000px"></div><span style="display: inline-block; position:relative; top: -9985.92px;"><span class="goog-inline-block kix-lineview-text-block" style="width: 72px; padding-left: 0px;"><span class="kix-wordhtmlgenerator-word-node" style="font-size:14.666666666666666px;font-family:Arial;color:#000000;background-color:transparent;font-weight:400;font-style:normal;font-variant:normal;text-decoration:none;vertical-align:baseline;white-space:pre;">ola mundo<span class="goog-inline-block" style="width:7.875px;height:17.599999999999998px"> </span></span></span></span>


---
# Conectividade

Algumas razões para as aplicações móveis precisarem de conectividade:

- Precisam de informação que não está armazenada no telemóvel porque ocuparia demasiado espaço (ex: lista de restaurantes, músicas em streaming)

- Precisam de informação que é atualizada fora da aplicação (ex: estado do tempo, saldo bancário, comentários a uma foto)

- Precisam de atualizar informação que reside fora da aplicação (ex: foto de perfil)

- Precisam de partilhar informação com outros utilizadores (ex: chat)


---
# Conectividade

Há aplicações que começam por funcionar em offline mas acabam por evoluir para tirar partido da conectividade

```
[Smartphone screen showing an app interface]
2:28 PM                                81%

Me

Erin Glabets
Active since Oct 2016
RUN

TIME SPENT
2:05:53  1:08:53
THIS WEEK   LAST WEEK

ACTIVITIES                    All Time Totals
178
Run/Walk

GOALS                         Run a total of 60 mi
0 / 60 m
---
# Conectividade

Há aplicações que começam por funcionar em offline mas acabam por evoluir para tirar partido da conectividade

Minhas
corridas

Corridas dos
meus amigos
---
# Conectividade

João

```mermaid
graph LR
    A[Smartphone] -->|1| B[Servidor]
```

1. O João envia para o servidor os resultados da sua corrida


---
# Conectividade

João

```mermaid
graph LR
    A[Smartphone] -->|1| B[Servidor]
    B --> |2| C[(Base de Dados)]
```

1. O João envia para o servidor os resultados da sua corrida
2. O Servidor guarda na sua Base de Dados os resultados das corridas de toda a gente


---
# Conectividade

```mermaid
graph LR
    A[João] -->|1| B[Servidor]
    B -->|3| C[António]
    B -->|2| D[(Base de Dados)]
```

1. O João envia para o servidor os resultados da sua corrida
2. O Servidor guarda na sua Base de Dados os resultados das corridas de toda a gente
3. O António vai buscar ao servidor os resultados dos seus amigos (incluindo o João)


---
# Serviços externos

```mermaid
graph LR
    A[Smartphone] <--> B[Servidor]
```

A comunicação entre aplicações móveis e o servidor é normalmente efetuada através de **Webservices**


---
# Web vs Webservices

```mermaid
graph LR
    A[User] <--> B[HTML]
    B <--> C[Web]
    C <--> D[Servidor]
    D <--> E[(Database)]
    
    style A fill:#000000,stroke:#000000,color:#ffffff
    style B fill:#ffffff,stroke:#0000ff,color:#000000
    style C fill:#4682b4,stroke:#0000ff,color:#ffffff
    style D fill:#4682b4,stroke:#0000ff,color:#ffffff
    style E fill:#ffffff,stroke:#000000,color:#000000
```

The diagram illustrates the comparison between Web and Webservices:

1. On the left side, a user is represented interacting with an HTML interface, which shows a Google search results page for "android".

2. The HTML interface connects to a "Web" component, which in turn connects to a "Servidor" (Server in Portuguese).

3. The server is then connected to a database, represented by a cylinder shape.

This visualization demonstrates the basic structure of how web services operate, with the user interacting through an HTML interface, which communicates with a web server, which in turn interacts with a database to retrieve or store information.


---
# Web vs Webservices

```mermaid
graph LR
    User((User)) <--> |HTML| Web
    Web --> Servidor((Servidor))
```


---
# Web vs Webservices

```mermaid
graph LR
    A[User] -->|HTML| B[Web]
    C[Mobile Devices] -->|XML/JSON| D[Webservices]
    B --> E[Servidor]
    D --> E
    E <--> F[(Database)]
```

The diagram illustrates the difference between Web and Webservices:

1. Web:
   - A user (represented by a person icon) interacts with the Web through HTML.
   - The example shows a Google search results page for "android".

2. Webservices:
   - Mobile devices (represented by tablet and smartphone icons) interact with Webservices using XML/JSON.
   - An example of JSON structure is shown:

```json
{
 "kind": "customsearch#search",
 "url": {
  "type": "application/json"
 },
 "items": [
  {
   "title": "Android",
   "link": "https://www.android.com/",
   ...
  }
 ]
}
```

Both Web and Webservices connect to the same Server, which in turn interacts with a database.


---
# Web vs Webservices

| HTML                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         | JSON                                                            |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------- |
| \<div class="kix-appview-editor-container">\<div class="kix-appview-editor" style="overflow-x: auto; height: 356.562px;">\<div>\<div class="kix-zoomdocumentplugin-outer" aria-hidden="true" style="width: 826px; height: 1066px; left: 313px; top: 4px;">\<div class="kix- zoomdocumentplugin-inner" style="">\<div>\<div class="kix-paginateddocumentplugin">\<div class="kix-paginateddocumentplugin-background docs-ui-unprintable" style="height: 1066px; width: 816px;">\</div>\<div>\<div class="kix-page docs-page kix-page-paginated" guidedhelpid="docs\_editing\_area" style="background-color: rgb(255, 255, 255); width: 816px; height: 1056px;">\<div class="docs-print- block kix-page-header" style="min-height: 96px; max-height: 422.4px; width: 816px;">\</div>\<div class="kix-page-content-wrapper" style="background-color: rgb(255, 255, 255); height: 960px;">\<div>\<div style="height: 864px;">\<div class="kix-page-column" style="height: 864px; left: 0px; width: 816px;">\<div style="margin-left: 96px; margin-right: 96px;">\<div>\<div>\<div class="kix- paragraphrenderer" id="">\<div class="kix-lineview" style="height: 20px; direction: ltr; text-align: left;">\<div class="kix-lineview- decorations" style="left: 0px; top: 14.08px;">\</div>\<div class="kix-lineview-content" style="user-select: none; margin-left: 0px; padding-top: 0px;">\<span style="display: inline-block; height: 10000px">\</span>\<span style="display: inline-block; position:relative; top: -9985.92px;">\<span class="goog-inline-block kix-lineview-text-block" style="width: 72px; padding-left: 0px;">\<span class="kix- wordhtmlgenerator-word-node" style="font-size:14.666666666666666px;font-family:Arial;color:#000000;background-color:transparent;font- weight:400;font-style:normal;font-variant:normal;text-decoration:none;vertical-align:baseline;white-space:pre;">ola mundo\<span class="goog-inline-block" style="width:7.875px;height:17.599999999999998px">\ \</span>\</span>\</span>\</span>\</div>\</div>\</div>\</ div>\</div>\</div>\<div class="kix-page-column-bottom">\<div class="docs-print-block" style="margin-left: 96px; margin-right: 96px;">\<div class="kix-page-column-footnotes-separator kix-page-column-footnotes-separator-hidden" style="width: 192px;">\</div>\</div>\</div>\</ div>\</div>\</div>\<div class="docs-print-block kix-page-bottom" style="min-height: 96px; max-height: 422.4px; width: 816px;">\</div>\</ div>\<div class="kix-page-relative-entity-container" style="top: 0px; height: 1056px;">\</div>\</div>\</div>\<div class="docs-ui- unprintable" style="height: 0px; background-color: rgb(255, 255, 255); display: none; width: 816px;">\</div>\</div>\</div>\</div>\</ div>\<div class="docs-ui-unprintable">\</div>\<div class="docs-ui-unprintable">\</div>\<div class="docs-ui-unprintable">\</div>\<div class="docs-ui-unprintable">\</div>\<div class="docs-ui-unprintable">\</div>\<div class="kix-discussion-plugin docs-ui-unprintable" style="left: 1135px; top: 8px; text-align: left;" dir="ltr">\<div class="docos docos-stream-view docos-stream-view-legacy docos-stream- view-height-legacy docs-gm docos-layout-anchored docos-layout-vertical" role="list">\</div>\<div id="docs-instant-button-bubble" class="docs-material docs-instant-button-bubble-transformation-ltr" role="button" tabindex="-1" aria-hidden="true" aria-label="Add a comment" data-tooltip="Add a comment" data-tooltip-suspended="true" style="top: 113.8px; opacity: 0;">\<div class="docs-instant-button- bubble-icon-container">\<span class="docs-instant-button-bubble-icon docos-icon-img docos-icon-img-hdpi docos-instant-icon-img docos- icon-instant-docos-ltr docos-instant-button-bubble-icon">\</span>\</div>\</div>\</div>\<div class="docs-ui-unprintable">\</div>\</div>\<div class="kix-cursor docs-ui-unprintable" style="opacity: 0; left: 414px; top: 105px;">\<div class="kix-cursor-caret" style="border-color: rgb(0, 0, 0); height: 17.6px;">\</div>\<div class="kix-cursor-top" style="opacity: 0; display: none;">\</div>\<div class="kix-cursor-name" style="opacity: 0; display: none;">\</div>\</div>\<div class="kix-scrollbararea">\<div class="jfk-tooltip kix-scrollbarwidget" role="tooltip" aria-live="polite" style="display: none; right: 0px; top: 0px;">\<div class="jfk-tooltip-contentId" style="direction: ltr;">\</div>\<div class="jfk-tooltip-arrow jfk-tooltip-arrowright" style="top: 15px;">\<div class="jfk-tooltip-arrowimplbefore">\</ div>\<div class="jfk-tooltip-arrowimplafter">\</div>\</div>\</div>\</div>\<div>\<div class="kix-embeddedobjectdragger kix- embeddedobjectdragger-embeddedentity">\</div>\</div>\<div>\<div class="kix-embeddedobjectdragger kix-embeddedobjectdragger-cropmode docs- ui-unprintable" style="display: none;">\</div>\<div class="kix-embeddedobjectdragger-cropwrapper" style="display: none;">\</div>\</ div>\<div>\</div>\</div>\</div> | {<br/>  "document": {<br/>    "body": "ola mundo"<br/>  }<br/>} |



---
# Web vs Webservices

The image illustrates the difference between web and webservices in mobile applications.

## Browser mobile

The top left of the image shows a mobile browser interface resembling LinkedIn:

- Search bar for people, jobs, posts
- A post with an image of a group of people
- Like, Comment, and Share buttons
- User interaction details

## App nativa (Native App)

The bottom left shows a native app interface, also resembling LinkedIn:

- Search bar
- A post with the same group image
- Like, Comment, and Share buttons
- User interaction details
- Navigation icons at the bottom

## Diagram

The right side of the image contains a diagram showing the relationship between web/webservices and the server:

```mermaid
graph LR
    A[Browser mobile] <--> B[Web]
    C[App nativa] <--> D[Webservices]
    B --> E[Servidor]
    D --> E
    E <--> F[(Database)]
```

The diagram illustrates that both the web interface (accessed through a mobile browser) and webservices (used by native apps) communicate with the same server, which in turn interacts with a database.


---
# Web vs Webservices

```mermaid
graph LR
    A[http://yesno.wtf] <--> B[Web]
    C[http://yesno.wtf/api] <--> D[Webservices]
    B --> E[Servidor]
    D --> E
    E <--> F[(Database)]
```

The diagram illustrates the difference between Web and Webservices:

1. Web:
   - Represented by the URL: http://yesno.wtf
   - Connects directly to the "Web" interface of the server

2. Webservices:
   - Represented by the URL: http://yesno.wtf/api
   - Connects to the "Webservices" interface of the server

Both Web and Webservices interfaces are part of the same "Servidor" (Server), which is connected to a database.


---
# Web vs Webservices

YES                   NO

http://yesno.wtf

http://yesno.wtf/api

```mermaid
graph LR
    A[Web] --> B[Servidor]
    C[Webservices] --> B
    B <--> D[(Database)]
```

```json
{"answer":"yes","forced":false,"image":"https://yesno.wtf/assets/yes/1-af11222d8d4af90bdab8fc447c8cfebf.gif"}
```

```json
{"answer":"no","forced":false,"image":"https://yesno.wtf/assets/no/21-05540164de4e3229609f106e468fa8e7.gif"}
```


---
# Serviços externos

Um Webservice é um serviço disponibilizado por um servidor na Internet, que pode ou não receber um conjunto de inputs e responde sempre com um conjunto de outputs


---
# Serviços externos

Um Webservice é um serviço disponibilizado por um servidor na Internet, que pode ou não receber um conjunto de inputs e responde sempre com um conjunto de outputs

<div style="background-color: #d9534f; color: white; padding: 10px;">
É como se chamássemos uma função mas em vez de estar local (ex: na mesma classe), está num servidor
</div>

Por isso se costuma referir aos webservices como API do Servidor


---
# Serviços externos

Um Webservice tem 4 características fundamentais:

- Endereço do servidor
  (ex: api.spotify.com)

- Nome do serviço
  (ex: artist top tracks)

- Inputs
  (ex: identificador do artista)

- Outputs
  (ex: lista das músicas mais tocadas desse artista)


---
# Serviços externos

Tipicamente, um servidor disponibiliza vários serviços, também designados por endpoints

| **Spotify for Developers** Documentation                                                                                                                                                                                                                                                                                                                                                                                                       |                                                                                                                                                                                                                                                                                                                                                           |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **How-Tos**<br/>**REFERENCE**<br/>AlbumsGet Album<br/>Get Several Albums<br/>Get Album Tracks<br/>Get User's Saved Albums<br/>Save Albums for Current User<br/>Remove Users' Saved Albums<br/>Check User's Saved Albums<br/>Get New ReleasesArtistsGet Artist<br/>Get Several Artists<br/>Get Artist's Albums<br/>Get Artist's Top Tracks<br/>Get Artist's Related Artists **Audiobooks**<br/>**Categories**<br/>**Chapters**<br/>**Episodes** | **Web API - References / Artists / Get Artist**## Get Artist OAuth 2.0Get Spotify catalog information for a single artist identified by their unique Spotify ID.**Important policy notes**- Spotify content may not be downloaded
- Keep visual content in its original form
- Ensure content attribution### Request`GET /artists/{id}`id	string	Required |

      <p>The Spotify ID of the artist.</p>
      <p>Example value: "0TnOYISbd1XYRBk9myaseg"</p>
      <h3>Response</h3>
      <code>200 401 403 429</code>
      <p>An artist</p>
      <details>
        <summary>external_urls object</summary>
      </details>
    </td>
  </tr>
</table>

To the left of the Spotify documentation screenshot, there's an annotation pointing to various items in the "Albums" section, labeled "endpoints".


---
# webservices

Os webservices podem ser acedidos de diversas formas, sendo as duas mais conhecidas:

- SOAP
- REST


---
# webservices

## SOAP

• Quer os inputs quer os outputs estão no formato XML


---
# webservices

## SOAP

- Quer os inputs quer os outputs estão no formato XML
- Permite definir formalmente quais os inputs e outputs através de um ficheiro WSDL


---
# webservices

## SOAP

- Quer os inputs quer os outputs estão no formato XML
- Permite definir formalmente quais os inputs e outputs através de um ficheiro WSDL
- Estende o protocolo HTTP com atributos próprios, tornando-o inviável de ser utilizado por browsers e bibliotecas HTTP. Por essa razão, obriga a utilizar uma biblioteca de terceiros (ou seja, não incluída no SDK iOS ou Android)


---
# webservices

## SOAP

- Quer os inputs quer os outputs estão no formato XML
- Permite definir formalmente quais os inputs e outputs através de um ficheiro WSDL
- Estende o protocolo HTTP com atributos próprios, tornando-o inviável de ser utilizado por browsers e bibliotecas HTTP. Por essa razão, obriga a utilizar uma biblioteca de terceiros (ou seja, não incluída no SDK iOS ou Android)
- Não recomendado para aplicações móveis
  - Demasiado "pesado" quer no processamento quer na largura de banda ocupada
  - Obriga a utilizar bibliotecas de terceiros


---
# webservices

## REST

- Os inputs estão no formato standard do protocolo HTTP (pares nome-valor), tal como se fosse a submissão de um formulário HTML


---
# webservices

## REST

- Os inputs estão no formato standard do protocolo HTTP (pares nome-valor), tal como se fosse a submissão de um formulário HTML
- Os outputs podem estar no formato XML ou JSON (preferencialmente JSON)


---
# webservices

## REST

- Os inputs estão no formato standard do protocolo HTTP (pares nome-valor), tal como se fosse a submissão de um formulário HTML
- Os outputs podem estar no formato XML ou JSON (preferencialmente JSON)
- Utiliza o protocolo HTTP sem extensões, ou seja, funciona em browsers e a maioria das linguagens inclui suporte nativo para estes webservices


---
# webservices

## REST

- Os inputs estão no formato standard do protocolo HTTP (pares nome-valor), tal como se fosse a submissão de um formulário HTML
- Os outputs podem estar no formato XML ou JSON (preferencialmente JSON)
- Utiliza o protocolo HTTP sem extensões, ou seja, funciona em browsers e a maioria das linguagens inclui suporte nativo para estes webservices
- Recomendado para aplicações móveis
  - Pouco processamento e largura de banda
  - Suporte nativo dos SDKs de iOS e Android


---
# XML

- Constituído por tags, organizadas de forma hierárquica
  (isto é, podem haver tags dentro de tags)
- As tags podem ter atributos
- Parecido com o HTML

```xml
<tracks>
    <track name="Can't Help Falling in Love"
           popularity="73"
           duration_ms="179773" />
    <track name="Hound Dog"
           popularity="65"
           duration_ms="136026" />
    <track name="A Little Less Conversation"
           popularity="65"
           duration_ms="211173" />
</tracks>
```


---
# JSON

- Formato associado à linguagem Javascript
- Pares "nome" : valor separados por vírgula
- Os valores podem ser strings (entre aspas), inteiros, listas (entre parêntesis rectos) ou sub-pares nome-valor.
- Os pares nome-valor devem estar entre chavetas

```json
{ "tracks" : [
    {
      "name" : "Can't Help Falling in Love",
      "popularity" : 73,
      "duration_ms" : 179773
    },
    {
      "name" : "Hound Dog",
      "popularity" : 65,
      "duration_ms" : 136026
    },
    {
      "name" : "A Little Less Conversation",
      "popularity" : 65,
      "duration_ms" : 211173
    }
  ]
}
```


---
# Exercício

Transformar esta mensagem em XML para JSON

```xml
<response>
   <message>Olá, mundo</message>
   <item id="1234567" name="abc" />
   <item id="999999" name="kil" />
   <user>
      <name>Pedro</name>
      <phone number="213456789" />
      <phone number="914565675" />
   </user>
</response>
```


---
# Exercício

Transformar esta mensagem em XML para JSON

<response>
    <message>Olá, mundo</message>
    <item id="1234567" name="abc" />
    <item id="999999" name="kil" />
    <user>
        <name>Pedro</name>
        <phone number="213456789" />
        <phone number="914565675" />
    </user>
</response>

JSON?

(regra)
Os valores podem ser strings (entre aspas), inteiros, listas
(entre parêntesis rectos) ou sub-pares nome-valor

(usem como exemplo)
```json
{
  "tracks": [
    {
      "name": "Can't Help Falling in Love",
      "popularity": 73,
      "duration_ms": 179773
    },
    {
      "name": "Hound Dog",
      "popularity": 65,
      "duration_ms": 136026
    },
    {
      "name": "A Little Less Conversation",
      "popularity": 65,
      "duration_ms": 211173
    }
  ]
}
```


---
# Resolução

```json
{
  "response": {
    "message": "Olá, mundo",
    "items": [
      {
        "id": 1234567,
        "name": "abc"
      },
      {
        "id": 999999,
        "name": "kil"
      }
    ],
    "user": {
      "name": "Pedro",
      "phones": [
        {
          "number": 213456789
        },
        {
          "number": 914565675
        }
      ]
    }
  }
}
```


---
# REST

Para invocarmos um webservice REST, precisamos de saber (pelo menos) 3 coisas:

- URL do serviço
  exemplo: https://www.googleapis.com/customsearch/v1


---
# REST

Para invocarmos um webservice REST, precisamos de saber (pelo menos) 3 coisas:

- URL do serviço
  exemplo: https://www.googleapis.com/customsearch/v1
- Método - GET, POST, PUT, DELETE
  - GET - para obter informação (leitura)
  - PUT - para inserir informação (escrita)
  - POST - para atualizar informação (escrita)
  - DELETE - para apagar informação (escrita)


---
# REST

Para invocarmos um webservice REST, precisamos de saber (pelo menos) 3 coisas:

- URL do serviço
  exemplo: https://www.googleapis.com/customsearch/v1
- Método - GET, POST, PUT, DELETE
  - GET - para obter informação (leitura)
  - PUT - para inserir informação (escrita)
  - POST - para atualizar informação (escrita)
  - DELETE - para apagar informação (escrita)
- Inputs (parâmetros)
  - Se for por GET vão no próprio url
    exemplo: https://www.googleapis.com/customsearch/v1?q=android
  - Se for pelos outros métodos, vão no corpo do pedido, como se fosse um formulário


---
# GET vs POST

## GET
- Obter informação do servidor (read)

## POST
- Atualizar informação no servidor (write)


---
# GET vs POST

## GET
- Obter informação do servidor (read)
- Parâmetros são acrescentados ao url:
  http://localhost/do?param1=3&param2=5

## POST
- Atualizar informação no servidor (write)
- Parâmetros vão no corpo do pedido


---
# GET vs POST

## GET
- Obter informação do servidor (read)
- Parâmetros são acrescentados ao url:
  http://localhost/do?param1=3&param2=5
- Pode ser chamado múltiplas vezes sem causar efeitos secundários
  (reload)

## POST
- Atualizar informação no servidor (write)
- Parâmetros vão no corpo do pedido
- Se fôr chamado várias vezes pode causar efeitos indesejáveis (ex:
  transferir 2x)


---
# GET vs POST

## GET

- Obter informação do servidor (read)
- Parâmetros são acrescentados ao url:
  http://localhost/do?param1=3&param2=5
- Pode ser chamado múltiplas vezes sem causar efeitos secundários (reload)
- Exemplos: pesquisas em geral, página de perfil, boletim meteorológico, lista de restaurantes

## POST

- Atualizar informação no servidor (write)
- Parâmetros vão no corpo do pedido
- Se for chamado várias vezes pode causar efeitos indesejáveis (ex: transferir 2x)
- Exemplos: mudar password, pagar, adicionar comentário


---
# Exemplo REST

https://www.googleapis.com/customsearch/v1?q=android&key=AIzaSyDfhpqYkH0WGUzDgd3HdSjWmM-Zs8968EA

```json
{
  "kind": "customsearch#search",
  "url": {
    "type": "application/json"
  },
  "items": [
    {
      "title": "Android",
      "link": "https://www.android.com/",
      "displayLink": "www.android.com",
      "snippet": "See what's new with Android - from phones to watches and more. Visit the official \nsite to explore and learn."
    },
    {
      "title": "Android (operating system) - Wikipedia",
      "link": "https://en.wikipedia.org/wiki/Android_(operating_system)",
      "displayLink": "en.wikipedia.org",
      "snippet": "Android is a mobile operating system developed by Google, based on the Linux \nkernel and designed primarily for touchscreen mobile devices such as …"
    }
  ]
}
```


---
# REST

https://www.googleapis.com/customsearch/v1?q=android&key=AIzaSyDfhpqYkH0WGUzDgd3HdSjWmM-Zs8968EA

Que parâmetro "key" é este?


---
# API Token

A maioria das APIs públicas (autenticadas ou não) obrigam os programadores a enviar um API token ou API key

- O token é um identificador único de cada programador/aplicação


---
# API Token

A maioria das APIs públicas (autenticadas ou não) obrigam os programadores a enviar um API token ou API key

- O token é um identificador único de cada programador/aplicação
- É normalmente uma string bastante grande


---
# API Token

A maioria das APIs públicas (autenticadas ou não) obrigam os programadores a enviar um API token ou API key

- O token é um identificador único de cada programador/aplicação
- É normalmente uma string bastante grande
- É obtida manualmente, após login no site associado à API


---
# API Token

A maioria das APIs públicas (autenticadas ou não) obrigam os programadores a enviar um API token ou API key

- O token é um identificador único de cada programador/aplicação
- É normalmente uma string bastante grande
- É obtida manualmente, após login no site associado à API
- Tem que ser enviado em todos os pedidos


---
# API Token

A maioria das APIs públicas (autenticadas ou não) obrigam os programadores a enviar um API token ou API key

- O token é um identificador único de cada programador/aplicação
- É normalmente uma string bastante grande
- É obtida manualmente, após login no site associado à API
- Tem que ser enviado em todos os pedidos
- Tem como objectivo prevenir abusos (ex: inundar o servidor com pedidos) e assegurar modelos de pagamento (ex: o serviço é gratuito até 1000 pedidos por dia)


---
# API Token

A maioria das APIs públicas (autenticadas ou não) obrigam os programadores a enviar um API token ou API key

- O token é um identificador único de cada programador/aplicação
- É normalmente uma string bastante grande
- É obtida manualmente, após login no site associado à API
- Tem que ser enviado em todos os pedidos
- Tem como objectivo prevenir abusos (ex: inundar o servidor com pedidos) e assegurar modelos de pagamento (ex: o serviço é gratuito até 1000 pedidos por dia)
- Importante: O token não tem nada a ver com as credenciais do utilizador mas sim da aplicação


---
# API Key

https://developers.google.com/places/web-service/

```html
<div style="background-color: #4285F4; color: white; padding: 10px;">
  <span style="font-size: 18px;">🏷️ Google Places API</span>
  <span style="float: right;">
    Home    Documentation    Pric >   
    <input type="text" placeholder="Search" style="padding: 5px;">
  </span>
</div>

<div style="background-color: #4285F4; color: white; padding: 20px;">
  <h2>Places API Web Service</h2>
  <p>Add up-to-date information about millions of locations.</p>
  <div>
    OVERVIEW    GUIDES    SUPPORT
    <span style="float: right;">
      <button style="background-color: white; color: #4285F4; border: none; padding: 10px;">GET A KEY</button>
      <button style="background-color: white; color: #4285F4; border: none; padding: 10px;">VIEW PRICING AND PLANS</button>
    </span>
  </div>
</div>
```

## Local data around the world

Get data from the same database used by Google Maps and Google+ Local. Places features more than 100 million businesses and points of interest

[An arrow points to the "GET A KEY" button]


---
# Parâmetros

Os parâmetros enviados para um webservice podem ter dois formatos:

- Query parameters - enviados após o símbolo '?' colocado no final do url e separados pelo símbolo '&'
  Exemplo: http://api.xyz.com/service?p1=34&p2=67

- Path parameters - incluídos no próprio caminho para o serviço
  Exemplo: http://api.xyz.com/service/34/67


---
# Autenticação

Tal como os sites exigem autenticação prévia, também os webservices podem exigir autenticação

## Exemplo sem autenticação - Obter previsão meteorológica para Lisboa
GET http://api.openweathermap.org/data/2.5/weather?q=Lisbon&appid=f1c1bd57ded364f65fc7546dc3a702b8

## Exemplo com autenticação - Obter as minhas playlists
GET https://api.spotify.com/v1/me/playlists

Precisa de saber quem é o utilizador


---
# Autenticação

Os webservices nunca devem enviar a password do utilizador mas antes um access token obtido previamente

Esse token é enviado em cada pedido ao servidor, através do header HTTP "Authorization"

| GET https\://api.spotify.com/v1/me/playlists        |
| --------------------------------------------------- |
| Headers:                                            |
| - Cache-Control: max-age=0                          |
| - User-Agent: Mozilla/5.0 …                         |
| - Authorization: Bearer QB0zg...eF9U (access token) |



---
# Token

```
GET https://api.spotify.com/v1/me/playlists
Headers:
- Cache-Control: max-age=0
- User-Agent: Mozilla/5.0 …
- Authorization: Bearer QB0zg...eF9U
```

Não existe um standard para o formato dos tokens

Recentemente, tem-se vindo a popularizar o JWT (JSON Web Token):

```json
{
  "sub": "1234567890",
  "name": "John Doe",
  "iat": 1516239022
}
```

Mais info: https://jwt.io/


---
# API Token vs Access Token

**API Token** - Um por aplicação, usado para controlar o número de acessos. Obtido após registo do programador no serviço.

**Access Token** - Um por sessão, usado para autenticar o utilizador. Obtido após login do utilizador


---
# API Token vs Access Token

```mermaid
graph LR
    A1[Apollo] --> S((Servidor<br>Reddit))
    A2[Antenna] --> S
    A3[Apollo] --> S
    S --> A1
    S --> A2
    
    style S fill:#4a86e8,stroke:#000,stroke-width:2px
    
    subgraph User1
        U1((User))
        A1
    end
    
    subgraph User2
        U2((User))
        A2
    end
    
    subgraph User3
        U3((User))
        A3
    end
```

This diagram illustrates the interaction between different Reddit client applications (Apollo and Antenna) and the Reddit server. Three users are shown, each using either Apollo or Antenna to access Reddit's services. The bidirectional arrows indicate that data flows both ways between the clients and the server.


---
# API Token vs Access Token

Apollo

api token: apollo84953
access token: sara325657

Antenna

api token: antenna42068
access token: cris106567

Apollo

api token: apollo84953
access token: pedro23467

Servidor
(Reddit)


---
# Autenticação

Mas como é que se obtém o access token?

A maioria dos webservices usa o protocolo OAuth 2.0, um protocolo aberto que permite autorizar, de forma segura, o acesso a recursos autenticados

Pode ser usado na web, desktop e mobile


---
# OAuth 2.0 flow

## Exemplo

Uma app para editar fotos (Photogram)

- Fotos locais (no telemóvel)
- Fotos no google drive

<div style="text-align: right;">
    <img src="arrow.png" alt="Arrow pointing to 'Fotos no google drive'" style="width: 100px; height: auto;">
</div>

<div style="text-align: right; margin-top: 10px;">
    <div style="display: inline-block; border: 1px solid blue; padding: 10px; background-color: lightblue;">
        Vou usar a API do google para<br>
        aceder à minha google drive
    </div>
</div>

<div style="text-align: right; margin-top: 20px; font-size: 0.8em;">
    
</div>
---
# OAuth 2.0 flow

Photogram                    Google Drive

```mermaid
graph LR
    A[Photogram] --- B[Google Drive]
    C[Phone] --- A
    
    subgraph Phone
    D[Photogram]
    E["Ligar ao Google Drive"]
    end
```


---
# OAuth 2.0 flow

```mermaid
sequenceDiagram
    participant P as Photogram
    participant G as Google Drive
    
    P->>G: pedido de autorização<br>(app = photogram;scope = file_access)
    
    note over P: Mobile App<br>with "Ligar ao<br>Google Drive" button
```

The diagram illustrates the OAuth 2.0 flow between Photogram and Google Drive. On the left side, there's a representation of a mobile device showing the Photogram app interface with a button labeled "Ligar ao Google Drive" (Connect to Google Drive).

The flow shows an authorization request from Photogram to Google Drive, with the following parameters:
- app = photogram
- scope = file_access


---
# OAuth 2.0 flow

```mermaid
sequenceDiagram
    participant Photogram
    participant Google Drive
    Photogram->>Google Drive: pedido de autorização (app = photogram;scope = file_access)
    Google Drive->>Photogram: login no Google Drive
```

![A smartphone showing Google sign-in screen with email and password fields]


---
# OAuth 2.0 flow

```mermaid
sequenceDiagram
    participant Photogram
    participant Google Drive

    Photogram->>Google Drive: pedido de autorização (app = photogram;scope = file_access)
    Google Drive->>Google Drive: login no Google Drive
    Google Drive->>Google Drive: autorização
```

Photogram

Google Drive

pedido de autorização
(app = photogram;scope = file_access)

login no Google Drive

autorização


---
```mermaid
sequenceDiagram
    participant Photogram
    participant Google Drive
    
    Photogram->>Google Drive: pedido de autorização (app = photogram;scope = file_access)
    Google Drive->>Google Drive: login no Google Drive
    Google Drive->>Google Drive: autorização
    Google Drive->>Photogram: access_token (token=xsuhasdsias; expires=xxx)
    Photogram->>Photogram: guarda o token
```

Photogram | Google Drive
--- | ---

```
   Photogram

    ✅

 Ligado ao
Google Drive
```


---
# OAuth 2.0 flow

```mermaid
sequenceDiagram
    participant Photogram
    participant Google Drive
    
    Photogram->>Google Drive: pedido de autorização (app = photogram;scope = file_access)
    Google Drive->>Google Drive: login no Google Drive
    Google Drive->>Google Drive: autorização
    Google Drive->>Photogram: access_token (token=xsuhasdsias; expires=xxx)
    Note over Photogram: guarda o token
    Photogram->>Google Drive: pedido à API - /getFiles (token=xsuhasdsias)
    Google Drive->>Photogram: resposta ({"files": ["img1.png","img2.png"]})
```

[An image of a smartphone showing the Photogram app interface with multiple photos]


---
```mermaid
sequenceDiagram
    participant P as Photogram
    participant GD as Google Drive

    P->>GD: pedido de autorização (app = photogram;scope = file_access)
    GD->>GD: login no Google Drive
    GD->>GD: autorização
    GD->>P: access_token (token=xsuhasdsias; expires=xxx)
    Note over P: guarda o token
    P->>GD: pedido à API - /getFiles (token=xsuhasdsias)
    GD->>P: resposta ({"files": ["img1.png","img2.png"]})
    Note over P,GD: Pode continuar a usar o mesmo token para<br>fazer pedidos à API até que expire
```

# OAuth 2.0 flow

The diagram illustrates the OAuth 2.0 flow between Photogram and Google Drive.

1. Photogram sends an authorization request to Google Drive with the parameters:
   - app = photogram
   - scope = file_access

2. Google Drive prompts for login.

3. Google Drive performs authorization.

4. Google Drive sends an access token back to Photogram:
   - token=xsuhasdsias
   - expires=xxx

5. Photogram stores the token.

6. Photogram makes an API request to Google Drive:
   - Endpoint: /getFiles
   - Using the token: xsuhasdsias

7. Google Drive responds with:
   ```json
   {"files": ["img1.png","img2.png"]}
   ```

Note: Photogram can continue using the same token to make API requests until it expires.


---
# OAuth 2.0

Uma vez que o protocolo OAuth é relativamente complexo de implementar, a maioria dos servidores fornece um SDK ou biblioteca para facilitar a integração

| Facebook SDK for Android                                                                                                                                                                                                                                                                                                                                                                                  | Start Integrating Google Sign-In into Your Android App                                                                                                                                                                                                                                                                                                                                                                                    | Twitter Kit                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Helps you build engaging social apps and get more installs.<br/><br/>**Download the SDK**<br/><br/>Includes Account Kit, Audience Network, and Facebook packages. Requires Android API 15.<br/><br/>v4.22.0 See Change Log or Upgrade Guide.<br/><br/>- Get Started<br/>Basic guide for Android
- SDK Reference Docs<br/>Reference Docs and sample code
- View Source<br/>View code and samples on Github | **Contents**- Prerequisites
- Get a configuration file
- Add the configuration file to your project
- Add the Google Services plugin
- Add Google Play Services
- Get your backend server's OAuth 2.0 client ID
- Next stepsBefore you can start integrating Google Sign-In in your configure a Google API Console project and set up you The steps on this page do just that. The next steps the integrate Google Sign-In into your app. | Twitter content, live and lightweight in your app.<br/><br/>Twitter Kit is designed to make interacting with Twitter- whether it's logging someone in, displaying Tweets, or Tweeting from your app- seamless and efficient. Twitter Kit offers pre-built views for single Tweets or live timelines, and a composer that makes sharing from your app a matter of adding just a few lines of code.<br/><br/>The Android SDK is a collection of individual feature modules, called Kits. The SDK provides the following Kits: |



---
# Google SDK

https://developers.google.com/identity/sign-in/android/sign-in

```java
GoogleSignInOptions gso = 
    new GoogleSignInOptions.Builder(GoogleSignInOptions.DEFAULT_SIGN_IN)
    .requestScopes(new Scope(PeopleScopes.CONTACTS_READONLY))
    .build();
```

Importante definir bem as permissões que precisamos, no momento em que fazemos o pedido de autorização

<div style="text-align: right;">
    <img src="smartphone_screen.png" alt="Smartphone screen" style="width: 200px;">
    <p>3:07</p>
    <p>Pedro Alves<br>pedro.h.alves@gmail.com</p>
    <p>GoogleFriendsList would like to:</p>
    <p>[G] View your contacts</p>
    <p>By continuing, you allow this app and Google to<br>use your information in accordance with their<br>respective terms of service and privacy policies.</p>
    <p>[DENY]    [ALLOW]</p>
</div>
---
# Tratamento de erros

Os webservices não retornam páginas de erro, retornam códigos de erro

![An image showing a comparison between a website error page and an error code]

On the left side of the image, there's a representation of a typical website error page with the following content:

```
Site Not Found
Well, this is awkward. The site you're looking for is not here.
Is this your site? Get more info or contact support

DreamHost
```

On the right side, it simply states:

vs    Error Code: 404

This comparison illustrates the difference between how errors are presented in web pages versus web services.


---
# Tratamento de erros

Os códigos de erro são universais, fazem parte do protocolo HTTP

| STATUS CODE | DESCRIPTION                                                                                                                                                                                                            |
| ----------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 200         | OK - The request has succeeded. The client can read the result of the request in the body and the headers of the response.                                                                                             |
| 201         | Created - The request has been fulfilled and resulted in a new resource being created.                                                                                                                                 |
| 202         | Accepted - The request has been accepted for processing, but the processing has not been completed.                                                                                                                    |
| 204         | No Content - The request has succeeded but returns no message body.                                                                                                                                                    |
| 304         | Not Modified. See Conditional requests.                                                                                                                                                                                |
| 400         | Bad Request - The request could not be understood by the server due to malformed syntax. The message body will contain more information; see Response Schema.                                                          |
| 401         | Unauthorized - The request requires user authentication or, if the request included authorization credentials, authorization has been refused for those credentials.                                                   |
| 403         | Forbidden - The server understood the request, but is refusing to fulfill it.                                                                                                                                          |
| 404         | Not Found - The requested resource could not be found. This error can be due to a temporary or permanent condition.                                                                                                    |
| 429         | Too Many Requests - Rate limiting has been applied.                                                                                                                                                                    |
| 500         | Internal Server Error. You should never receive this error because our clever coders catch them all ... but if you are unlucky enough to get one, please report it to us through a comment at the bottom of this page. |



---
# Exemplos (Spotify)

## Get an Artist

Get Spotify catalog information for a single artist identified by their unique Spotify ID.

### Request

| HEADER                                                                    | TYPE   | REQUIRED |
| ------------------------------------------------------------------------- | ------ | -------- |
| Authorization<br/>*A valid user access token or your client credentials.* | String | Required |


| PATH PARAMETER                           | TYPE   | REQUIRED |
| ---------------------------------------- | ------ | -------- |
| {id}<br/>*The Spotify ID of the artist.* | String | Required |


### Response

On success, the HTTP status code in the response header is 200 OK and the response body contains an artist object in JSON format. On error, the header status code is an error code and the response body contains an error object.

```
GET https://api.spotify.com/v1/artists/{id}

// json response
{
  "external_urls" : {
    "spotify" : "https://open.spotify.com/artist/00dUWJ0sBjI"
  },
  "followers" : {
    "href" : null,
    "total" : 306565
  },
  "genres" : [ "indie folk", "indie pop" ],
  "href" : "https://api.spotify.com/v1/artists/00dUWJ0sBjDri",
  "id" : "00dUWJ0sBjDrqHygGUXeCF",
  "images" : [ {
    "height" : 816,
    "url" : "https://i.scdn.co/image/eb266625dab075341e8c43",
    "width" : 1000
  }
```

(https://developer.spotify.com/documentation/web-api/reference-beta/#category-artists)

| Operação   | Endpoint                                 | Verbo | API Token? | Access Token? | Query/Path? | Inputs       | Output |
| ---------- | ---------------------------------------- | ----- | ---------- | ------------- | ----------- | ------------ | ------ |
| Get Artist | https\://api.spotify.com/v1/artists/{id} | GET   | Não        | Sim           | Path        | id (artista) | JSON   |



---
# Exemplos (Weatherstack)

## Current Weather
Available on: All plans

To query the weatherstack API for real-time weather data in a location of your choice, simply attach your preferred location to the API's `current` endpoint as seen in the example request below. Depending on your subscription, you can also make a bulk location request by passing multiple semicolon-separated locations to the API URL.

### Example API Request:

```
http://api.weatherstack.com/current
    ? access_key = YOUR_ACCESS_KEY
    & query = New York
```

Run API Request

### HTTP GET Request Parameters:

| Object       | Description                                                                                                                                                     |
| ------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `access_key` | \[Required] Your API access key, which can be found in your account dashboard.                                                                                  |
| `query`      | \[Required] Use this parameter to pass a single location or multiple semicolon-separated location identifiers to the API. Learn more about the Query Parameter. |


(https://weatherstack.com/documentation)

| Operação        | Endpoint                              | Verbo | API Token? | Access Token? | Query/Path? | Inputs              | Output |
| --------------- | ------------------------------------- | ----- | ---------- | ------------- | ----------- | ------------------- | ------ |
| Current Weather | https\://api.weatherstack.com/current | GET   | Sim        | Não           | Query       | query (localização) | JSON   |



---
# Exemplos (bit.ly)

## Create a Bitlink

Convert a long url to a Bitlink and set additional parameters

REQUEST BODY SCHEMA: application/json

| Field | Type | Description |
|-------|------|-------------|
| domain | string | Default: "bit.ly" |
| title | string | |
| group_guid | string | Enterprise users: Always verify your default group is set properly in the Bitly app. Otherwise, you will likely connect to your free account instance and quickly hit those link limits. You can do this in your settings, and we have more details in this help article. |
| tags | Array of string | |
| deeplinks | Array of object | |
| long_url | string (required) | |

(https://dev.bitly.com/v4/#operation/createFullBitlink)

```json
POST /bitlinks

https://api-ssl.bitly.com/v4/bitlinks

Payload

application/json

{
  "domain": "bit.ly",
  "title": "string",
  "group_guid": "string",
  "tags": [
    "string"
  ],
  "deeplinks": [
    { ... }
  ],
  "long_url": "string"
}
```

| Operação       | Endpoint                               | Verbo | API Token? | Access Token? | Query/Path? | Inputs         | Output |
| -------------- | -------------------------------------- | ----- | ---------- | ------------- | ----------- | -------------- | ------ |
| Create Bitlink | https\://api-ssl.bitly.com/v4/bitlinks | POST  | Sim        | Sim           | N/A         | long\_url, ... | JSON   |



---
# Como descobrir webservices?

https://www.programmableweb.com/apis/directory

https://github.com/public-apis/public-apis


---
# Como experimentar rapidamente webservices REST?

## Usando o Intellij (Ultimate edition apenas)

A imagem demonstra como usar o IntelliJ IDEA Ultimate Edition para experimentar rapidamente webservices REST. Aqui estão os passos principais:

1. No menu de criação de novos arquivos do IntelliJ, selecione "HTTP Request" sob a categoria "Other".

2. Uma vez criado o arquivo de requisição HTTP, você verá opções para adicionar diferentes tipos de requisições:
   - GET Request
   - POST Text Body
   - POST Parameters Body
   - POST Form with a Text Field
   - POST Form with a File Field

3. Um exemplo de requisição GET é mostrado:

   ```
   GET https://blabla-api/things
   Accept: application/json
   Authorization: Bearer qwertyui
   ```

4. Você pode executar todas as requisições no arquivo usando o botão "Run All Requests in File".

5. Há opções para adicionar novas requisições e ambientes usando os botões "Add Request" e "Add Environment".

Esta funcionalidade permite testar e experimentar com webservices REST diretamente no ambiente de desenvolvimento, sem a necessidade de ferramentas externas.

