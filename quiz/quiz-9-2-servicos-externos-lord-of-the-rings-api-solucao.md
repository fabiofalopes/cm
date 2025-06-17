# Solução - Quiz #9.2 - Serviços externos (Lord of the rings API)

### Pergunta 1

Começa por aceder a [https://the-one-api.dev/](https://the-one-api.dev/) e regista-te de forma a te ser atribuída uma API key.

1.  Através da documentação disponível nesse site, quando endpoints diferentes são oferecidos por esse serviço? **8**
2.  Quantos desses endpoints requerem uma API key? **7** (todos exceto `/book`)
3.  Desses, quantos devem ser acedidos por POST? **0** (são todos acedidos via GET para leitura)
4.  Qual o endereço completo do endpoint que permite obter todos os livros da série "Senhor dos Anéis"? https://**the-one-api.dev/v2/book**
5.  Usando os HTTP requests do Intellij (ver último slide da aula), faz um pedido a esse endpoint (que permite obter todos os livros). No json de resposta, qual o id associado ao primeiro livro ("Irmandade do anel") **5cf5805fb53e011a64671582**
6.  Qual o endereço completo do endpoint que permite obter todos os personagens da série "Senhor dos Anéis"? https://**the-one-api.dev/v2/character**
7.  Quando tentas aceder a esse endpoint sem lhe passares a API key, obténs uma mensagem de erro em json. Qual o conteúdo do atributo "message", nessa resposta? **Unauthorized.**
8.  Tenta agora aceder a esse endpoint com a API key que te foi atribuída (inclui o header Authorization tal como descrito na documentação). A partir do JSON obtido:
    
    *(Nota: As respostas abaixo requerem a execução do pedido com uma chave de API válida. O resultado pode ser obtido executando `curl -H "Authorization: Bearer <SUA_CHAVE_API>" -s "https://the-one-api.dev/v2/character" | jq` e inspecionando o JSON)*
    
    1.  Em que ano nasceu Belegorn? TA **2029**
    2.  Como quem é casado Milo Burrows? **Prisca Baggins**
    3.  Qual o id do Gandalf? **5cf5cdbf3cf0513c6b84d8b Gandalf**

9.  (Todas as respostas são válidas) Já leste os livros desta série?
    - [ ] Todos
    - [ ] Alguns
    - [x] Nenhum

---
**Legenda:**
*   `[ ... ]`: Preencha com o texto correspondente.
*   `- [ ]`: Marque a opção correta. 