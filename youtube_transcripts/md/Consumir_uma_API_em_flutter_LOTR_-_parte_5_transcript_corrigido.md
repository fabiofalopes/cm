# Consumir uma API em Flutter LOTR - Parte 5

Neste vídeo vamos começar a preparar o Lord of the Rings para o modo offline, em que se nós perdermos a conectividade continuamos a poder obter os personagens e informação sobre os personagens. No caminho para fazer essa preparação, vamos aproveitar para resolver um erro que já vem de trás e que se calhar não deram por ele.

Mas antes disso, quero só lembrar o que é que está feito: temos um botão para obter os personagens a partir da API e depois podemos obter o detalhe. Temos um então para obter personagens que estão na base de dados que foram inseridas através do insert Character.

E agora o erro que eu estava a falar é este: quando eu agora carrego aqui ele dá um erro. OK, qualquer um deles dá um erro e olhando para aqui para o log não se percebe o que é que poderá estar a acontecer.

Para facilitar este diagnóstico, eu vou acrescentar aqui uma ferramenta que me dá muito jeito, gosto muito dela, que é o pretty http logger. Vamos acrescentar aqui esta biblioteca que basicamente o que ela vai fazer é permitir logar todos os pedidos HTTP API de uma forma simples. Eles passam a aparecer aqui sem a gente ter praticamente trabalho nenhum.

Basta modificarmos aqui uma linha: em vez deste client ser simplesmente este client, vamos substituir por uma classe do pretty http logger desta forma: http with middleware é uma classe do pretty http logger. Importamos e agora dizemos aqui que todos os pedidos são feitos através deste http logger e que o nível de log é o Basic. Isto significa que ele apenas mostra informação básica: qual é o pedido e qual é a resposta, não mostra o conteúdo da resposta.

Se por alguma razão nos der jeito de ver o conteúdo da resposta, basta alterar aqui o nível de log para body. Aqui não queremos isso porque a resposta, o JSON que vem deste pedido é bastante extenso e não queremos encher aqui a consola com isso. Portanto vamos deixar o Basic.

Vamos aqui dar um restart. Vamos começar a ver aqui os pedidos a aparecer e quando eu venho aqui, cá está, apareceu este pedido. Tão a ver, portanto cada vez que eu vou ao servidor ele mostra-me aqui o pedido. Isto dá bastante jeito para diagnosticar problemas.

E agora vamos ver o que é que acontece aqui quando eu carrego aqui. Ops, ele está a ir ao servidor buscar a personagem 74. Não existe a personagem 74. Porquê? Porque esta personagem foi criada por nós através do insert Character na base de dados, ela na realidade não existe.

Então há aqui um problema que é: eu para obter os detalhes, os dados desta personagem, eu tenho que perceber que ela foi criada na base de dados e tem que usar a base de dados para isso.

Vamos corrigir este erro começando por acrescentar aqui neste ficheiro que neste momento só tem uma forma de obter os personagens todos da base de dados e inserir um personagem. Precisamos ter aqui uma função que nos permita obter os dados de um personagem em concreto, à semelhança do que já está a ser feito aqui no repositório. Tão a ver, portanto eu vou precisar de uma coisa deste género.

Vou copiá-la para aqui, vou colocá-la aqui debaixo para ficar mais organizado. Vou manter esta minha regra aqui no início e agora vou aqui, em vez de obter todos os personagens que era o que estava a acontecer aqui - uma lista de personagens - eu quero apenas obter um personagem.

Para isso vou usar exatamente a mesma forma que aqui está, mas vou-lhe acrescentar aqui um WHERE. Reparem que coloquei aqui um ponto de interrogação e ele vai ser substituído pelo que eu colocar aqui dentro desta lista. Se puser aqui vários pontos de interrogação, posso colocar aqui vários elementos nesta lista. É assim que devem construir as vossas queries à base de dados.

E isto vai retornar-me uma lista. Reparem que esta lista agora só vai ter uma entrada à partida, porque só existe um Character com aquele ID, se tudo tiver bem. Isto é uma primary key, logo eu pelo sim pelo não - não vai - eu ter pedido um ID que não existe na base de dados, eu vou começar por verificar se o result não é vazio. Então eu vou retornar um from DB result first, porque à partida ele só vai ter um resultado.

Tem que colocar aqui um else porque caso não, caso seja vazio, tenho que fazer alguma coisa. A forma mais simples neste caso é de lançar uma exceção. E temos o nosso get Character feito.

Aproveito já, já que estou aqui a mexer neste Database, vou aproveitar também para criar já uma nova função que me vai dar jeito. Esta pode ir aqui para baixo, que é uma função que permite apagar todos os personagens que estão na base de dados aqui do telemóvel. Vai ser parecida com o insert no sentido em que não retorna nada, ela limita-se a se executar, mas é assíncrona. Portanto tem que ser um Future void.

Vamos manter à mesma, até vou copiar isto tudo porque aqui em vez de ser insert vai ser um raw delete. E aqui dentro é tão simples como fazer isto.

Vamos alterar a isto para que quando eu carrego aqui ele perceba que essa informação está na base de dados e não no servidor, e por isso uso esta função nova que a gente criou aqui. Então vamos aqui ao Character detail page. Precisar de obter também aqui a base de dados como fiz no characters list page. Estão a ver, ou seja, até vou copiar daqui.

E tal como no characters list page, eu preciso da source, eu preciso saber se a source é o network ou o Database. Lembram-se disso? Source até pode ser assim. Aqui já não tem ponto de interrogação, tenho a certeza qual é a source e vou acrescentar aqui ao meu construtor.

E agora o que é que eu vou fazer com essa source? Tal como no Character list page, vou aproveitar para chamar uma função diferente consoante a source é network ou é Database. Portanto se a source for Network vai retornar isto, caso contrário vai retornar isto. Simples, apenas com esta alteração deve ser o suficiente para isto funcionar.

Vamos só aqui ver que ele agora está a dar um erro de compilação porque isto agora precisa de dois parâmetros. Não basta o ID, não basta eu passar no construtor qual é a personagem, qual é o ID da personagem que quer mostrar. Também tenho que passar qual é a source à qual ele deve ir buscar esse personagem, que basicamente é o source que já aqui temos.

OK, vamos testar isto. Vamos só aqui abrir aqui isto só para ter a certeza que se houver pedidos ao servidor a gente os apanha. Cá está, nós não estamos a meter informação de nascimento nem de morte, por isso é que aparece a null, mas de resto parece estar tudo a funcionar bem. Reparem que agora já não aparece aqui nenhum pedido ao servidor.

Para testar o delete, vamos só acrescentar aqui um botão para apagar. Muito simples, eu vou só duplicar aqui, criar aqui um delete All Button. Vou também embaixo copiar isto. OK, e aqui em vez de ser insert é delete All. Podemos simplificar isto e colocar numa expressão para ficar mais simples. E vamos ver se... ah, falta aqui alterar isto. OK, vamos ver se apagou. Apagou.

O próximo passo para preparar isto para o modo offline: vamos olhar aqui para esta figura para percebermos melhor é eliminar, ou melhor, melhorar um bocadinho aqui esta arquitetura.

Reparem, temos aqui um characters repositório que neste momento é responsável por gerir a ligação à API. Todos os pedidos que são feitos à API passam por aqui e constroem um Character que pertence ao modelo através deste from JSON que aqui está.

Por outro lado, temos um lotr Database que obtém a partir da base de dados local do telemóvel através dessas quatro funções que aqui estão, interage com essa base de dados e também usa este Character que faz parte do modelo e em particular usa o from DB e o to DB.

Uma das coisas que podemos observar aqui é que há aqui uma certa duplicação. Se quiserem, quer um quer outro tem um get Character, se quer um quer outro tem o get Character a partir do string ID. Este não tem o insert e o delete apenas porque esta API é apenas só de leitura, porque se fosse uma API de escrita também até fazia sentido ter também aqui um insert e um delete de forma a que a gente pudesse apagar remotamente os personagens que estavam no servidor e inserir novos personagens no servidor.

Então o que a gente vai fazer para esta arquitetura é começar por criar uma classe abstrata que se chama ICharactersRepositório. O I vem de interface. Em Dart não há interfaces, mas a classe abstrata faz o mesmo efeito, em que temos estas quatro funções abstratas.

E a seguir vamos alterar isto para isto deixar de ser um repositório, porque na realidade o repositório é uma representação genérica de uma fonte de informação. Eu vou especificar que isto na realidade, o que vem através da API é através do lotr Services, o que vem da base de dados através do lotr Database, e ambos implementam esta classe abstrata.

Vamos então implementar isto. Eu vou começar por... uma vez que este Characters repositório na realidade é o lotr Services, eu vou copiar isto para a pasta data e vou-lhe chamar lotr Services. A seguir vou mudar aqui o nome da classe para lotr Services.

E esta classe vai passar a ser... e characters repository vai ser abstrata. Vamos retirar daqui o construtor que não é necessário para nada. Vamos retirar isto porque a gente deve apenas colocar aqui as assinaturas das funções. Vamos também copiar para aqui estas funções. Vamos mudar só aqui o nome para refletir o ICharacters repository.

E agora claro que ele se está a queixar porque se isto é abstrato eu não posso instanciar isto e nem sequer existe este construtor. Portanto na realidade o que eu agora quero aqui é um lotr Services. Aqui a mesma coisa. E agora aqui no... só verificar aqui isto. Deixa de ser a Characters repositório para passar a ser lotr Services. E isto vamos chamar Services.

E vamos copiar esta linha para o Character detail page. Falta importar e aqui vamos chamar Services. Ou seja, fica bastante mais claro: se a source é Network vai ao Services, caso contrário vai à Database.

Vamos só verificar que continua tudo a funcionar. OK, cá está os pedidos a aparecerem. E se for através do Database... OK, não tenho cá nada, vou inserir aqui um personagem. Já cá tenho um e continua tudo a funcionar.

Falta-me só aqui um pormenor que é: eu criei aqui esta classe abstrata, mas estas classes não estendem essa classe abstrata. Portanto vamos alterar isso. Está aqui, ele dá um erro porque falta o delete All e o insert. É verdade, e para já eles não vão fazer nada. E pronto, esta estrutura implementada.

Notem aqui que este insert e este delete estão mais cinzentos precisamente porque eles não estão a fazer nada. No entanto, ambos estendem o ICharacters repositório.

Então no próximo vídeo vamos mostrar para que é que isto serve, como é que a gente vai usar o modo offline desta forma com esta arquitetura. 