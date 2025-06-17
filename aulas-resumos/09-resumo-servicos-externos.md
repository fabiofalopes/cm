# Resumo: Aula 9 - Serviços Externos e Firebase

## 1. O Modelo Cliente-Servidor e os Webservices

Aplicações móveis (clientes) comunicam com um servidor (backend) para tarefas centrais como partilhar dados, autenticar utilizadores e enviar notificações. Esta comunicação é feita através de **Webservices**.

- **Web App vs. App Móvel (com Webservices):**
    - Uma **Web App** tradicional devolve ao browser uma mistura de dados e apresentação (**HTML**, CSS). O servidor dita a aparência.
    - Uma **App Móvel** comunica com **Webservices** (ou APIs) que se comportam como "funções remotas". Estes devolvem apenas **dados brutos**, geralmente em formato **JSON**, e a app nativa é totalmente responsável por os renderizar e apresentar ao utilizador.

- **Terminologia Essencial de Webservices:**
    - **Endpoint:** Cada "função" ou serviço específico que um servidor oferece. Ex: `https://api.exemplo.com/users/1`.
    - **Protocolos:**
        - **REST (Representational State Transfer):** A abordagem mais comum e leve. Usa os verbos HTTP padrão para interagir com os recursos.
        - **SOAP (Simple Object Access Protocol):** Um protocolo mais antigo e pesado, com um formato XML estrito e os seus próprios cabeçalhos.
    - **Formatos de Dados:**
        - **JSON (JavaScript Object Notation):** O mais popular. Leve, legível e fácil de converter para objetos Dart (Mapas).
        - **XML (eXtensible Markup Language):** Baseado em tags, mais verboso que o JSON.
    - **Verbos HTTP:**
        - **`GET`**: Para **ler** ou obter dados de um endpoint.
        - **`POST`**: Para **escrever**, criar ou submeter novos dados para um endpoint.

- **Segurança e Acesso:**
    - **API Token (ou API Key):** Uma chave usada para **autorizar a aplicação** a aceder à API. Serve para identificar e controlar o acesso da app cliente (e.g., limitar o número de pedidos), mas não identifica o utilizador.
    - **Access Token (e.g., Bearer Token):** Uma chave usada para **autenticar o utilizador**. Prova que o utilizador fez login com sucesso e tem permissão para aceder ou modificar os seus próprios dados.

---

## 2. Backend-as-a-Service (BaaS) e Firebase

- **Conceito:** Em vez de construir e gerir um servidor próprio (o que é complexo e caro), utiliza-se um fornecedor de "Backend como um Serviço". Este oferece funcionalidades prontas a usar (autenticação, base de dados, etc.) através de um SDK que se integra na app móvel.
- **Principal Exemplo:** **Firebase** (da Google).

### Serviços Essenciais do Firebase

#### A) Firebase Authentication
- **Função:** Gere todo o ciclo de vida de autenticação de utilizadores.
- **Funcionalidades:** Registo, login, recuperação de password, etc.
- **Providers:** Suporta múltiplos métodos de login prontos a usar: Email/Password, Google, Facebook, Apple, Anónimo, etc.

#### B) Cloud Firestore (Base de Dados)
- **Tipo:** Base de dados **NoSQL**, orientada a documentos, que organiza dados em coleções e documentos.
- **Estrutura:**
    - Os dados são guardados em **`Documentos`** (essencialmente, mapas de `chave: valor`).
    - Os documentos vivem dentro de **`Coleções`**.
    - Um documento pode conter dados primitivos, mapas, listas e até **sub-coleções**.
- **Funcionalidade Chave: Tempo Real (Real-time)**
    - O Firestore permite "ouvir" (`listen`) as alterações num documento ou numa coleção através de **`Streams`** em Dart.
    - Quando os dados mudam no servidor, o `Stream` na app emite os novos dados automaticamente. Isto permite que a UI se atualize em tempo real sem necessidade de fazer *polling* (pedidos repetidos ao servidor).

#### C) Cloud Storage
- **Função:** Armazenar ficheiros grandes e não estruturados (imagens, vídeos, PDFs).
- **Uso Comum:** A app faz o upload de uma imagem para o Storage. O Storage devolve um URL público ou privado para esse ficheiro. Esse **URL é depois guardado num campo de um documento no Firestore**, associando o ficheiro ao respetivo dado (e.g., ao perfil do utilizador).

#### D) Cloud Functions
- **Função:** Executar código backend sem gerir servidores (arquitetura *serverless*).
- **Triggers (Gatilhos):** As funções são despoletadas por eventos que ocorrem noutras partes do ecossistema Firebase.
    - Ex: Enviar um email de boas-vindas quando um novo utilizador se regista (gatilho: `on new user creation` no Authentication).
    - Ex: Redimensionar uma imagem ou extrair metadados quando um novo ficheiro é carregado (gatilho: `on file upload` no Storage).

---

## 3. Integração com SDKs Nativos (Platform Channels)

- **O Problema:** Muitos serviços de terceiros (ex: Google Maps, HealthKit da Apple, SDKs de pagamento) só existem como bibliotecas nativas para iOS (Swift/ObjC) e Android (Kotlin/Java).
- **A Solução:** Os **plugins** de Flutter usam um mecanismo chamado **Platform Channels** para comunicar com o código nativo.
- **Como Funciona:**
    1.  O código **Dart** (na app Flutter) envia uma mensagem através de um canal com um nome específico.
    2.  O código **Nativo** (no lado do iOS ou Android do projeto Flutter) tem um "ouvinte" para esse mesmo canal.
    3.  Ao receber a mensagem, o código nativo executa a tarefa necessária usando o SDK nativo da plataforma.
    4.  O resultado (sucesso ou erro) é devolvido ao Dart através do mesmo canal.
- **Para o Developer:** Toda esta complexidade é **abstraída pelo plugin**. Apenas se importa e usa a API em Dart do plugin (e.g., `google_maps_flutter` ou `stripe_flutter`), mas é fundamental saber que por baixo está a ocorrer esta comunicação com o código nativo da plataforma. 