# Quiz #2 - Modelos de Desenvolvimento (Parte 1) - Solução

### Pergunta 1

Dentro da abordagem Web, temos duas sub-abordagens: **HTML5** e **Híbrida-Web**. A primeira consiste simplesmente em aceder a um site com o **browser** que está instalado no dispositivo móvel. A segunda encapsula uma **WebView** numa app que parece nativa pois arranca-se diretamente a partir do home screen.

Para um site ser mobile-friendly, tem que obedecer a certas regras como o texto ser legível sem necessidade de fazermos **zoom** e evitar usar scroll **horizontal**.

Existem basicamente 3 abordagens para preparar um site de forma a que seja visualizável em smartphones. Uma delas é atribuir um **URL** específico para mobile. Com essa abordagem conseguimos aceder à versão mobile mesmo que estejamos num PC. Outra opção é ter uma única página que se adapta automaticamente ao tamanho do **écran**, usando uma técnica de css chamada **media queries**. A principal framework css que adopta esta técnica chama-se **Bootstrap**. Esta abordagem é boa pois desenvolvemos uma única vez para múltiplos dispositivos. No entanto, se quisermos adaptar o écran consoante o sistema operativo, temos que usar a abordagem **Dynamic serving** que controla, no servidor, qual a página que vai ser mostrada ao utilizador.

Na abordagem Híbrida-Web, temos uma Webview incorporada numa aplicação. Essa Webview pode ser carregada com conteúdos **locais** ou **remotos**. O primeiro caso é bom quando a aplicação está **offline**. O segundo é bom pois permite manter a app atualizada. Ou seja, o ideal é combinar os dois tipos de conteúdo.

Uma das frameworks Híbrida-Web mais conhecidas é o **Ionic**, que usa tecnologias web como angular e o bootstrap para desenvolver aplicações móveis. O desenvolvimento nesta framework é muito **rápido**, graças ao live reload.

Finalmente, surge uma outra opção parecida com a Híbrida-Web mas que pode ser instalada diretamente a partir de um **browser**, sem passar pela store. Essa opção chama-se **Progressive Web App** e consiste num site ao qual se adicionou na raiz o ficheiro **manifest.json**. Infelizmente, estima-se que apenas **85**% dos utilizadores consigam correr essas aplicações, nomeadamente devido a limitações no sistema operativo **iOS**. 