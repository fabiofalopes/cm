# Resumo: Aula 2 - Web, HTML5 e Híbrida-Web

## 1. Abordagens para Web Mobile

Existem três maneiras principais de oferecer uma experiência web otimizada para dispositivos móveis:

1.  **Responsive Web Design (RWD):** **(Recomendado)** A mesma página (URL e HTML) adapta o seu layout (CSS) ao tamanho do ecrã do dispositivo. É a abordagem mais comum e flexível.
2.  **Dynamic Serving:** O servidor deteta o tipo de dispositivo (e.g., mobile ou desktop) e serve uma versão diferente do HTML e CSS para o mesmo URL.
3.  **URLs Específicos (Separate URLs):** O servidor redireciona o utilizador para um URL diferente (e.g., de `www.site.com` para `m.site.com`) se detetar um acesso via dispositivo móvel.

Um site considerado "mobile-friendly" deve ter texto legível sem **zoom**, elementos clicáveis bem espaçados e não exigir **scroll horizontal**.

---

## 2. Aplicações Web com HTML5

- **Conceito:** Aplicações que correm diretamente no browser do dispositivo, usando tecnologias web padrão (HTML, CSS, JavaScript).
- **Capacidades:** Têm acesso a um número surpreendente de APIs de hardware e software através de JavaScript. O site [whatwebcando.today](https://whatwebcando.today/) demonstra as funcionalidades disponíveis no browser atual.
    - Acesso a: GPS, Acelerómetro, Câmara, Microfone, Bluetooth, Pagamentos, etc.
- **Problemas Principais:**
    - **Aparência de "Site":** O utilizador percebe que está dentro de um browser, quebrando a imersão de uma "app".
    - **Conectividade:** **Principal desvantagem.** Tradicionalmente, não funcionam offline, embora tecnologias como Service Workers (ver PWAs) possam mitigar isto.
- **Quando Usar:** Ideal para aplicações de uso pontual (e.g., consultar o cartaz de um festival), apps simples (conversores, calculadoras) ou conteúdos acedidos via motores de busca (e.g., Wikipedia).

---

## 3. Responsive Web Design (RWD) em Detalhe

RWD é a técnica de construir um site que se adapta a qualquer tamanho de ecrã. Baseia-se em três pilares e é a base de frameworks como o **Bootstrap**.

- **Técnicas Centrais:**
    1.  **Fluid Grid:** A grelha de layout usa unidades relativas (como percentagens) em vez de pixéis fixos, permitindo que a estrutura se estique ou encolha.
    2.  **Fluid Images:** As imagens são dimensionadas para nunca excederem o tamanho do seu contentor, evitando que "quebrem" o layout.
    3.  **Media Queries (CSS):** A "magia" do RWD. Permitem aplicar blocos de estilos CSS apenas quando certas condições são cumpridas (e.g., a largura do ecrã é inferior a 600px).

    ```css
    /* Exemplo: Se o ecrã tiver no máximo 600px, esconde o menu principal 
       e mostra um menu de hamburguer. */
    @media (max-width: 600px) {
      .menu-principal { display: none; }
      .menu-hamburguer { display: block; }
    }
    ```

---

## 4. Arquitetura Híbrida-Web

- **Conceito:** Uma aplicação HTML5 "empacotada" (`wrapped`) numa aplicação nativa, que pode ser distribuída pelas App Stores.
- **Componente Chave:** `WebView` — um componente nativo que funciona como um mini-browser, sem a barra de endereço, incorporado na app e que carrega o código web.
- **Conteúdo da WebView:** Pode carregar ficheiros de duas formas, sendo a combinação ideal:
    - **Locais:** Ficheiros (HTML, CSS, JS) guardados dentro da própria app. Garante o **funcionamento offline**.
    - **Remotos:** Ficheiros carregados de um servidor. Permite **atualizar a app** sem precisar de a submeter novamente à store.
- **Ponte (Bridge):** A "casca" nativa pode expor APIs do sistema operativo (e.g., acesso a contactos, calendário) ao JavaScript. Esta ponte permite que o código web invoque funcionalidades nativas que de outra forma não conseguiria aceder.
- **Frameworks Notáveis:** Apache Cordova, Ionic.

---

## 5. Progressive Web Apps (PWA)

- **Conceito:** Uma evolução das aplicações web que visa oferecer uma experiência semelhante à nativa. É um site que, através de tecnologias modernas, pode ser "instalado" no ecrã principal do dispositivo diretamente a partir do browser, sem passar por uma app store.
- **Componentes Chave:**
    - **Web App Manifest (`manifest.json`):** Um ficheiro JSON que descreve a aplicação (nome, ícone, cor do tema) e como se deve comportar quando "instalada".
    - **Service Worker:** Um script que o browser executa em segundo plano, separado da página web, e que permite funcionalidades como **funcionamento offline** (ao intercetar pedidos de rede e servir respostas de uma cache) e **push notifications**.
- **Limitações:** Embora o suporte esteja a crescer, a implementação de todas as funcionalidades de PWA, especialmente no **iOS**, ainda é limitada em comparação com o Android, o que afeta a sua adoção universal. 