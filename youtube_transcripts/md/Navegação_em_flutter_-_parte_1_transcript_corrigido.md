# Flutter Navigation Bottom Bar - Transcrição Corrigida

Neste vídeo vou mostrar como implementar navegação entre várias páginas numa aplicação em Flutter utilizando uma Bottom Navigation Bar. Como podem ver aqui, o comportamento que se pretende é este que estão aqui a ver.

Antes de avançar para a implementação, vou vos mostrar em termos de diagrama como é que isto vai funcionar. Vamos ter um widget chamado Main Page que vai ser responsável por gerir a Navigation Bar, ou seja, ele aqui no meio não vai ter nada. Ele vai trocando o que está aqui no meio à medida que a gente vai carregando aqui. Portanto, a responsabilidade dele é apenas criar esta Navigation Bar e garantir que quando nós trocamos, quando carregamos aqui no Page 1 ou no Page 2, o que está aqui no meio é trocado.

E o que é que está aqui no meio são widgets. Neste caso, por exemplo, o Page 1 que inclusivamente inclui uma App Bar, porque a gente quer que o título mude consoante a gente carrega no Page 1 ou no Page 2. Portanto, toda esta zona a verde será responsabilidade do widget interior, se quiserem. E a Main Page, a única coisa que faz é ir trocando o Page 1 com o Page 2 consoante se vai clicando num e noutro.

Dito isto, vamos então avançar para a implementação.

Vou começar por alterar aqui este `analysis_options` só para ele não chatear muito com warnings que nesta fase não são muito importantes e atrasam um bocadinho o desenvolvimento. Pronto, vamos então ao código propriamente dito.

Este Main é o Main que é gerado automaticamente quando criamos um projeto Flutter, e eu vou já começar por eliminar aqui esta parte. Isto já lavamos. Vou criar aqui uma pasta para isto ficar mais organizado, chamada "pages", e vou já criar aqui três widgets que vão ser a Main Page. Vou criar aqui com o `stls` Main Page, OK, importar, e vou duplicar isto: Page 1, Page 2. E vamos aqui mudar isto: P1 e pronto, temos então os nossos três widgets aqui criados.

Agora, para facilitar a futura manutenção desta aplicação no sentido de que poderão vir a ser necessárias mais páginas - nós neste momento temos só duas, mas imaginem que mais tarde é necessário criar uma terceira ou uma quarta, ou queremos facilmente mudar o nome da página ou o ícone que está associado - vamos criar aqui um quarto ficheiro chamado "pages". E lá dentro vamos criar uma estrutura, neste caso é uma lista de tuplos que vão representar a informação de cada página.

O que é que é um tuplo? Um tuplo é o equivalente a uma classe, se quiserem, no sentido em que agrega várias informações num único objeto, mas que eu não preciso criar uma classe só para isso. Eu uso os parênteses e lá dentro posso ir criando atributos que acrescenta ao tuplo, e depois mais tarde posso aceder como se fosse uma classe.

Neste caso, quais são os atributos que eu quero para cada página? Obviamente quero um title - neste caso vai ser "Page 1" - quero um icon que vai ser neste caso `Icons.` - vou por isto - `thumb_up`, e finalmente quero um widget que representa qual é o widget que vai ser responsável por desenhar essa página. Neste caso é o Page1(), importar, que foi o widget que a gente já criou. Agora vamos fazer o mesmo para a página 2.

E agora vamos então começar a alterar isto. Vou já aqui corrigir o meu Main - isto agora é Main Page, não tem título já que aqui estamos - vou só mudar aqui o title e importar isto. Pronto, para já isto ainda não faz nada, nem vale a pena correr.

Vamos então olhar aqui, se calhar, primeiro para o Page 1 e para o Page 2 antes de olharmos para o Main Page. Na realidade, eu basta-me construir o Page 1 e depois é quase um copy-paste para o Page 2, porque eles neste momento são iguais.

Então eu vou querer, em vez deste placeholder, vou criar aqui... vou querer usar um Scaffold para ter um App Bar. Um App Bar é este título que estamos aqui... que temos aqui, OK? Vamos colocar aqui este App Bar, vamos dizer que o title é Text. E agora podíamos criar aqui apenas "Page 1", mas já que temos essa informação nesta estrutura, devemos usá-la, porque assim temos um único sítio onde alteramos e fica refletido logo em toda a aplicação.

Então isto vai passar a ser `pages` - que é a minha variável global, vamos importá-la - na posição zero, portanto aquela lista na posição zero, ponto title. Assim eu tenho a certeza que se mudar aqui, depois vai mudar ali também. Se eu mudar este título, ela vai mudar logo, vai mudar aqui, vai mudar aqui, portanto fica tudo refletido.

Continuando, no body vamos começar pelo texto com a mesma situação, que é este title. Vamos copiá-lo para aqui. Claro que isto apenas vai mostrar o título. Portanto, o que a gente quer é basicamente criar aqui um widget do tipo Column, que é para organizar isto de forma vertical, com um ícone e um texto.

Então vamos fazer um wrap disto numa Column e vamos colocar aqui um Icon. E agora `pages[0].icon`. Para já fica assim, e eu ainda não vou copiar isto para o Page 2 porque ainda quero afinar isto. Isto provavelmente ainda não está com o aspeto que eu quero, portanto não vamos para já nos preocupar com isto.

Agora vou voltar aqui ao Main Page então para começar a implementar aqui a Bottom Navigation Bar. Também aqui vou criar um Scaffold, só que este Scaffold não vai ter App Bar. Isto é muito importante! Eu já mostrei há bocado o que que acontece na Main Page: ele apenas é responsável por criar esta parte. Esta parte fica a responsabilidade de cada uma das páginas interiores, precisamente porque o App Bar vai mudar consoante a gente seleciona um ou outro. Portanto, ela não vai ter App Bar, vai ter diretamente um body que neste momento a gente vai dizer que é igual ao Page1(). OK, vamos aqui importar.

E acho que podemos já correr isto para começar a afinar aqui a nossa aplicação. Cá está! Não está com aspeto espetacular.

Vamos agora melhorar aqui o Page 1. Para já, isto deve estar centrado. Portanto, vamos fazer um wrap com Center. E o que ele faz é centrar apenas horizontalmente. Para centrar verticalmente esta Column, a gente vai usar aqui o `mainAxisAlignment` e dizer que é `Center`. OK, já está centrado.

E agora vamos aumentar, se calhar, um bocadinho o tamanho do ícone e do texto. Aqui no ícone é só fazer `size` igual a... vou pôr 100, tamanho relativamente grande. Aqui no texto temos que usar o `style` e depois criar um `TextStyle` com um `fontSize`, por exemplo, de 30. OK.

Vou só tirar aqui... tirar esta vírgula e esta vírgula. E desta forma, se eu agora formatar, isto fica assim mais compacto. Gosto mais assim.

E agora falta-nos só aqui este App Bar, que eu não estou a gostar muito por ele não ter uma cor de fundo. Nós podíamos alterar isso aqui diretamente, mas a forma mais correta de fazer é através do tema. Todas as aplicações Flutter têm um tema associado - aqui está ele - e nós podemos diretamente neste tema mudar logo a cor de todos os App Bars que aparecerem na nossa aplicação, e essa é a forma mais correta.

Então, para o fazer, vou começar por extrair este `ColorScheme` para uma variável. Vou-lhe chamar `colorScheme`. E a seguir vou preencher uma propriedade chamada `appBarTheme`, em que eu, a partir do App Bar que existe neste momento, eu copio e coloco o `backgroundColor` igual à cor primária deste `colorScheme`, e o `foregroundColor` igual ao `backgroundColor` deste `colorScheme`. Tenho aqui também o `centerTitle: true`, mas eu até vou tirar isso.

E agora já temos o nosso App Bar na cor correta. Temos então, digamos, a nossa aplicação em termos da página feita. Eu agora até podia copiar isto já para a página 2, tudo isto. Importar, isto aqui passa a ser um... Obviamente, notem que não é nada bom eu ter código duplicado, ou seja, este Page 1 e Page 2, da forma como estão neste momento, até deveriam ser um único widget para o qual eu, por exemplo, passava através do construtor qual era a posição dentro do pages. No entanto, no mundo real, eu raramente tenho duas páginas iguais na Navigation Bar. Não é? Feito esta ressalva.

Vamos então implementar o nosso Bottom Navigation Bar. O Scaffold tem uma propriedade chamada `bottomNavigationBar`, e a gente pode logo preencher isto com um objeto do tipo `NavigationBar` que agora vamos ter que inicializar. OK.

Para já, ele diz-me que precisa de um `destinations`, que é basicamente quais são os destinos possíveis de navegação. Neste caso, quais são as páginas que vão aparecer na Navigation Bar. O que ela recebe é uma lista de `NavigationDestination`.

E agora eu tenho que converter basicamente as minhas páginas que aqui estão para `NavigationDestination`. Para isso, eu vou usar o `map`. E como alguns de vocês poderão não estar familiarizados com essa instrução, eu vou só aqui muito rapidamente mostrar como é que ela funciona.

A instrução de que vos quero falar é o `map`. Esta instrução existe em Dart, mas também existe numa série de linguagens, e o objetivo dela é transformar os elementos de uma lista noutros elementos, ou seja, aplicar uma transformação a cada elemento de uma lista de forma que a lista resultante tenha o mesmo número de elementos da lista original, mas com alguma transformação aplicada.

Vamos ver um exemplo concreto muito simples. Se eu quiser transformar esta lista de inteiros numa outra lista em que cada inteiro é o inteiro original mais um, então eu aplico este lambda que estão aqui a ver, ou seja, para cada inteiro eu somo mais um.

Não é obrigatório a lista destino ter o mesmo tipo de elementos da lista origem. Neste caso, uma lista de inteiros deu origem a uma lista de inteiros, mas pode dar origem a uma lista de outros objetos quaisquer. Por exemplo, eu estou a transformar quadrados em círculos para indicar que estou a transformar mesmo o tipo dos elementos da lista. E neste caso, eu estou a transformar uma lista de inteiros numa lista de Strings, em que me limito no lambda a converter um inteiro na sua representação sobre formato string.

Isto é o que nos interessa mais para o caso concreto que temos aqui nesta aplicação, que é: nós queremos transformar uma lista de tuplos com esta estrutura - widget, icon, label - numa lista de objetos do tipo `NavigationDestination` que, por sua vez, vão ter um icon e uma label. Obviamente tem que haver uma relação entre isto e isto.

Como é que eu vou fazer isso? Com este lambda muito simples: eu recebo um `p` que neste caso é uma entrada, uma page, se quiserem, é um tuplo. Para cada tuplo que aqui está, ele vai parar ao `p`, e depois eu vou criar um `NavigationDestination` baseado nesse `p`. Como? O icon é o `p.icon` - ou seja, este icon que está aqui - e a label é o `p.title` - ou seja, esta label que está aqui. E portanto, através deste `map`, eu consigo fazer esta transformação com uma única linha.

Vamos então aplicar esse `map` aqui, precisamente neste `destinations`. Em vez de começarmos a criar uma lista à mão, vamos simplesmente pegar no `pages` - que é aquela variável global que criámos aqui neste ficheiro, importá-la - e vamos aplicar o `map` precisamente a essa variável. Vai ser aquele que já tínhamos visto. Eu aqui usei `page` em vez de `p`, mas é a mesma coisa. E temos que no final fazer um `toList()` porque aquilo que é devolvido pelo `map` não é aceito diretamente aqui pelo `destinations`.

Isto já nos vai aparecer uma Bottom Bar, mas ela ainda não vai estar a funcionar. Reparem que ela não funciona ainda.

A seguir, temos outro parâmetro muito importante na Navigation Bar, que é o `selectedIndex`. Isto é um inteiro que indica qual é a posição na Bottom Bar que deve estar selecionada quando nós arrancamos a aplicação. Neste caso, que seria o zero, OK? Mas a gente quer que isto vá mudando consoante ele clica aqui ou aqui. Isto deve mudar o `selectedIndex`. Portanto, nós vamos criar aqui uma variável `selectedIndex` que vamos inicializar a zero, e é aqui que a gente vai colocar esta variável. Isto não pode ser `const`.

Agora que temos isto... ah, falta aqui agora tirar também daqui o `const`. E agora, com esta alteração, continua a não funcionar. O que é que falta ainda? Alterar aqui é preciso à mudança de página aqui neste click, se quiserem, aqui na Bottom Navigation Bar.

Para isso, eu vou preencher este `onDestinationSelected`, que é basicamente uma função que é chamada cada vez que eu carrego aqui numa destas opções, e ela passa qual é o índice - neste caso, ou zero ou 1 - que foi selecionado, digamos assim. E com isso, eu vou alterar o `selectedIndex`.

Isto continua a não funcionar, e os mais atentos de vocês já saberão porquê: porque este widget é Stateless, ou seja, ele é desenhado uma vez e depois nunca mais é desenhado. E eu tenho que o desenhar novamente de cada vez que carrego no Page 1 ou no Page 2, ou seja, este `selectedIndex` tem que provocar um novo build deste widget.

Então, a primeira coisa que eu tenho que fazer é convertê-lo para Stateful Widget. Para isso, basta-me fazer aqui Alt+Enter e ele converte para Stateful Widget. Mas ainda não é suficiente! Eu vou ter que encapsular esta alteração dentro de um `setState` para que ele perceba que tem que refrescar o ecrã e chamar novamente o build.

Vamos tirar isto aqui, vamos converter isto para uma expressão. E agora sim! Agora sim, isto devia funcionar.

Porque é que não funciona? Porque nós estamos a esquecer aqui de uma coisa: nós deixámos aqui no body fixo o Page1. Agora o body tem que partir do `selectedIndex` para mostrar o widget correto, ou seja, vamos novamente recolher a nossa variável `pages` no `selectedIndex` - ou seja, a página que neste momento está selecionada - e vamos buscar o widget.

E agora sim, isto passa a funcionar!