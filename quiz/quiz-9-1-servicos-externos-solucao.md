# Soluções - Quiz #9.1 - Serviços externos

### Pergunta 1

Os webservices são serviços na Internet que se comportam como:
- [x] funções
- [ ] aplicações
- [ ] páginas
...remotas.

Cada servidor pode fornecer vários serviços, também designados por:
- [ ] funções
- [x] endpoints
- [ ] tokens
...podendo o acesso ser feito através de um protocolo que estende o HTTP com cabeçalhos próprios chamado **SOAP** ou um protocolo:
- [x] mais leve
- [ ] mais pesado
...chamado **REST**. Se usarmos o segundo protocolo, as respostas poderão vir em **JSON** (formato baseado em pares nome-valor) ou em **XML** (formato baseado em tags).

Os dois principais verbos usados nestes pedidos são o **POST** para pedidos que escrevem no servidor e o **GET** para pedidos que lêem informação do servidor.

Para garantir que aplicações mal-comportadas não inundam o servidor de pedidos, alguns serviços requerem o envio de um **API token**. Por outro lado, para garantir a autenticação dos utilizadores, é necessário enviar:
- [ ] a sua password
- [ ] o seu api token
- [x] o seu access token

---
**Legenda:**
*   `[ ... ]`: Preencha com o texto correspondente.
*   `- [ ]`: Marque a opção correta. 