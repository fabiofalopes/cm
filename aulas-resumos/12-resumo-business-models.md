# Resumo Aprofundado: Aula 12 - Modelos de Negócio

Um modelo de negócio define como uma aplicação gera receita. A escolha do modelo depende do problema que a app resolve, do público-alvo e do valor que oferece. Todas as transações e a distribuição são mediadas pela **App Store (iOS)** e **Google Play (Android)**.

---

## 1. Custos da Plataforma e Comissões

Antes de gerar receita, é preciso considerar os custos de entrada e as comissões das lojas, que são um detalhe prático fundamental.

- **Taxa de Developer:**
    - **Apple App Store:** **$99 por ano**.
    - **Google Play Store:** **$25 (pagamento único)**.
- **Comissão sobre Vendas:** As lojas cobram uma comissão sobre todas as transações (apps pagas, in-app purchases, subscrições).
    - **Comissão Padrão:** Varia entre **15% e 30%**. Tipicamente, é 30% para a maioria dos developers e baixa para 15% para developers com menos de $1 milhão de receita anual ou para subscrições com mais de um ano.

---

## 2. Modelos de Monetização Principais

### A) Grátis com Publicidade (Free with Ads)
- **Como Funciona:** A app é gratuita. A receita vem de anúncios. A plataforma **Google AdMob** é uma solução popular que funciona em iOS e Android.
- **Tipos de Anúncios:** Banners, intersticiais (ecrã inteiro), vídeos recompensados (o utilizador vê um anúncio em troca de um benefício).
- **Vantagens:** Baixa barreira à entrada, ideal para atrair o máximo de downloads.
- **Desvantagens:** Requer uma **grande base de utilizadores ativos** para ser rentável e pode prejudicar a experiência do utilizador (UX).
- **Ideal para:** Apps onde os utilizadores passam **muito tempo**, como jogos casuais, apps de notícias e redes sociais.

### B) Paga (Paid / Pay-to-Download)
- **Como Funciona:** O utilizador paga um valor único para descarregar a app.
- **Vantagens:** Receita direta e previsível por download.
- **Desvantagens:** **Elevada barreira à entrada**. É difícil convencer utilizadores a pagar sem experimentar, especialmente com forte concorrência gratuita.
- **Ideal para:** Apps de nicho, ferramentas profissionais ou apps que **já têm uma reputação estabelecida** e um público que reconhece o seu valor.

### C) Freemium e Compras In-App (In-App Purchases)
- **Como Funciona:** O download é gratuito com funcionalidades básicas. O utilizador pode pagar para desbloquear funcionalidades "premium", remover anúncios ou comprar itens.
- **Sub-modelos:**
    - **Funcionalidades Premium:** Desbloquear capacidades avançadas (ex: exportar em alta resolução).
    - **Bens Virtuais:** Comprar itens ou moeda virtual em jogos (ex: skins, power-ups). É a base da economia de muitos jogos gratuitos.
- **Vantagens:** **O melhor de dois mundos**. Permite que o utilizador perceba o valor da app antes de pagar ("testar antes de comprar").
- **Desvantagens:** Exige um equilíbrio cuidadoso: as funcionalidades gratuitas têm de ser úteis, mas as pagas têm de ser desejáveis.
- **Ideal para:** A grande maioria das apps, de jogos a ferramentas de produtividade.

### D) Subscrição (Subscription)
- **Como Funciona:** Pagamento recorrente (mensal/anual) para acesso contínuo ao conteúdo ou serviço.
- **Vantagens:** **Receita recorrente e previsível (MRR/ARR)**, o modelo mais valorizado por investidores. Fomenta uma relação de longo prazo.
- **Desvantagens:** A app tem de **oferecer valor contínuo** (novos conteúdos, funcionalidades, atualizações) para justificar o pagamento e combater a "fadiga de subscrições".
- **Ideal para:** Serviços com **custos de manutenção contínuos**, como streaming (Netflix), SaaS (Notion), notícias (jornais) e apps de bem-estar.

---

## 3. Tabela Comparativa

| Modelo | Vantagem Principal | Desvantagem Principal | Tipo de App Comum | Detalhe-Chave do Quiz |
|:---|:---|:---|:---|:---|
| **Publicidade** | Máximo alcance | Requer escala massiva | Jogos casuais, Notícias | Ideal se o utilizador passa **muito tempo** na app. |
| **Paga** | Receita garantida por download | Elevada barreira à entrada | Ferramentas Profissionais | Funciona melhor para apps **já conhecidas**. |
| **Freemium** | Permite "testar antes de comprar" | Difícil de equilibrar | Produtividade, Jogos | Oferece **algumas** funcionalidades grátis. |
| **Subscrição** | **Receita recorrente e previsível** | Exige valor contínuo | Conteúdo, Serviços (SaaS) | Justifica-se quando há **custos de manutenção**. | 