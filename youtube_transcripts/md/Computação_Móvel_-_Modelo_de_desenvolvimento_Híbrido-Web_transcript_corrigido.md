# Computação Móvel - Modelo de desenvolvimento Híbrido-Web

Olá, neste vídeo vou falar do modelo híbrido-web. Lembram-se que no vídeo anterior falámos do HTML5 e eu disse que tinha dois grandes problemas: um era o facto de aparecer a barra do browser, que não é muito profissional para uma aplicação, e o outro era o facto de não funcionar offline.

O modelo híbrido-web resolve estes dois problemas. Como é que resolve? Bem, basicamente o que acontece é que nós criamos uma aplicação nativa - portanto uma aplicação que vai ser instalada no telemóvel como qualquer outra aplicação - mas essa aplicação nativa não tem interface. Ou seja, ela não tem botões, não tem campos de texto, não tem nada disso. O que ela tem é apenas um componente que se chama WebView.

O WebView é basicamente um browser sem interface. Ou seja, é como se fosse o motor do browser - a parte que interpreta HTML, CSS, JavaScript - mas sem a barra de endereços, sem os botões de back, forward, bookmark, etc. É só a zona onde aparece o conteúdo.

Então o que acontece é: nós criamos uma aplicação nativa que tem apenas um WebView que ocupa todo o ecrã, e depois dentro desse WebView nós carregamos o nosso HTML, CSS e JavaScript. Desta forma, para o utilizador final, aquilo parece uma aplicação nativa normal - não aparece nenhuma barra de browser, não aparece nada disso - mas na realidade o que está a correr lá dentro é HTML, CSS e JavaScript.

E como é que isto resolve o problema do offline? Bem, quando nós criamos a aplicação nativa, nós podemos incluir os ficheiros HTML, CSS e JavaScript dentro da própria aplicação. Ou seja, em vez de irmos buscar esses ficheiros a um servidor na internet, eles já estão dentro da aplicação. Portanto, mesmo que não haja conectividade, a aplicação consegue funcionar porque os ficheiros já lá estão.

Obviamente que se a aplicação precisar de ir buscar dados a um servidor - por exemplo, para mostrar notícias atualizadas ou para fazer login - aí sim, vai precisar de conectividade. Mas a estrutura base da aplicação, o HTML, CSS e JavaScript, já está lá dentro e portanto pode funcionar offline.

Este modelo tem várias vantagens. Primeira vantagem: nós podemos reutilizar conhecimentos que já temos de desenvolvimento web. Se já sabemos HTML, CSS e JavaScript, não precisamos de aprender uma linguagem completamente nova para desenvolver aplicações móveis.

Segunda vantagem: podemos reutilizar código. Se já temos um site feito, podemos aproveitar muito desse código para criar a aplicação móvel.

Terceira vantagem: desenvolvimento multiplataforma. Com o mesmo código HTML, CSS e JavaScript, podemos criar aplicações para Android, iOS, Windows Phone, etc. Só temos que criar a parte nativa - que é basicamente só o WebView - para cada plataforma, mas o resto do código é partilhado.

Mas também tem desvantagens. A principal desvantagem é a performance. Como estamos a correr HTML, CSS e JavaScript dentro de um WebView, isso é sempre mais lento do que código nativo puro. Para aplicações simples pode não se notar, mas para aplicações mais complexas, com muitas animações ou que precisem de processar muitos dados, pode haver diferenças de performance notáveis.

Outra desvantagem é o acesso às funcionalidades do dispositivo. Embora o HTML5 já dê acesso a algumas funcionalidades como o acelerómetro, GPS, câmara, etc., há sempre algumas funcionalidades mais específicas de cada plataforma que podem não estar disponíveis através de HTML5.

Para resolver este problema, existem frameworks que fazem a ponte entre o JavaScript e as funcionalidades nativas do dispositivo. Por exemplo, o Apache Cordova (anteriormente conhecido como PhoneGap) permite que o nosso código JavaScript chame funções nativas do dispositivo. Desta forma, podemos aceder a praticamente todas as funcionalidades do telemóvel a partir do nosso código HTML/JavaScript.

Quando é que faz sentido usar este modelo? Eu diria que faz sentido quando:

1. Já temos conhecimentos sólidos de desenvolvimento web e queremos aproveitar esses conhecimentos para desenvolvimento móvel.

2. Queremos desenvolver para múltiplas plataformas com o mesmo código base.

3. A aplicação não é muito exigente em termos de performance - ou seja, não tem muitas animações complexas, não processa grandes quantidades de dados, etc.

4. Queremos um desenvolvimento mais rápido - geralmente é mais rápido desenvolver em HTML/CSS/JavaScript do que aprender uma linguagem nativa nova.

Exemplos de aplicações famosas que usam este modelo incluem o Instagram (pelo menos nas versões iniciais), o WhatsApp, e muitas outras aplicações que vocês usam no dia-a-dia sem se aperceberem que são híbridas.

Em resumo, o modelo híbrido-web é uma boa opção quando queremos combinar a facilidade de desenvolvimento web com a experiência de uma aplicação nativa, especialmente quando não temos requisitos muito exigentes de performance. 