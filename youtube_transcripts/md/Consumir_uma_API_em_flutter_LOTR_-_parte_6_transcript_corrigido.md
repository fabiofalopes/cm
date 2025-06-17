# Consumir uma API em Flutter LOTR - Parte 6

Neste vídeo vou finalmente explicar como é que se implementa o modo offline. Isto vai tirar partir daquilo que temos vindo a construir até agora. Vou lembrar que ficamos neste ponto no último vídeo: temos uma classe abstrata repositório que hoje vamos perceber exatamente para que é que vai servir, que é estendida ou implementada pelo LOTR Services que trata da parte de ir à API, e a parte do LOTR Database trata de ir à base de dados local. Ambas falam a mesma linguagem no sentido em que transportam objetos do tipo Character.

E agora o que nós queremos é ter este comportamento: quando fazemos o get characters é o normal e vamos buscar ao servidor um JSON, nós vamos passar a guardar isso na base de dados de forma a que se a ligação se perder, nós passamos a obter essa informação a partir da base de dados.

A arquitetura perfeita para fazer isto é aquilo que se chama arquitetura do repositório ou padrão repositório, que eu passo a explicar. O repositório é uma classe que abstrai a fonte de dados. Temos aqui duas fontes de dados: uma que vem de uma API remota, outra que vem de uma base de dados local. E se nós implementarmos isto de tal forma que quem chama deste lado não sabe se está a ir ao lado remoto ou ao lado local, então temos o modo offline e o modo online muito facilmente implementados.

Senão vejamos: quando eu estou online, o que este repositório vai fazer é agulhar os pedidos que chegam aqui para o lado remoto. Mas se eu estou offline, ele passa a agulhar para o lado local da base de dados. E para implementarmos isto, nós vamos ter que criar então um Characters Repository - finalmente o nosso repositório que vai também ele estender esta classe abstrata. Reparem que tem cá as quatro funções que estas já tinham, mas agora estas funções vão ser inteligentes: elas vão tirar partir destas duas variáveis que aqui estão - uma aponta para o remoto que vai ser o LOTR Services, outra aponta para o local que vai ser o LOTR Database - e ela vai agulhar conforme eu estou online ou offline para um lado ou para o outro.

Antes de avançarmos para essa classe, só lembrar que nós já tínhamos aqui uma espécie de agulhamento implementado. Aqui esta linha, se repararem, ela já está a agulhar: se a source é Network, ela ia ao Services get characters; se não, ia ao Database get characters. E também aqui no detail tínhamos exatamente a mesma coisa.

O que nós agora vamos fazer é passar esta lógica para dentro da tal classe repositório, e aqui nós passamos a chamar o repositório e ele vai perceber onde ir buscar. Ou seja, fica escondido da interface gráfica se ele está a ir buscar à rede, à API, ou se está a ir buscar à base de dados.

A primeira coisa que nós vamos ter que fazer é perceber se estamos online ou offline. Para isso eu vou criar aqui uma classe nova - aliás, até vou criar uma pasta nova chamada Services - e aqui dentro vou criar um ConnectivityService que vai ser simplesmente uma classe ConnectivityService que vai ter uma função muito simples: retorna um bool e diz isOnline se neste momento estamos online ou não.

Para conseguirmos fazer isto, vamos ter que usar uma biblioteca que permite saber o estado da conectividade. Vamos acrescentá-la aqui ao pubspec, que é o connectivity_plus. Não esqueçam de fazer pub get.

E agora vou voltar aqui ao ConnectivityService. Vou tirar a partir dessa biblioteca para criar aqui este connectivity que vem do connectivity_plus. Este checkConnectivity vai-me dar uma variável que me diz qual é a conectividade que existe neste momento: ela pode ser... pode não existir, pode ser mobile ou pode ser Wi-Fi. Eu neste caso quero que ela retorne true se a conectividade for mobile ou Wi-Fi.

Temos aqui um problema, que é: o checkConnectivity ela não retorna uma conectividade, ela retorna um Future<Connectivity>. Porque isto é uma coisa que pode demorar algum tempo a perceber, esta conectividade é uma função assíncrona, portanto. E sendo isto uma função assíncrona, se calhar é uma boa ideia eu colocar aqui um await. Mas se eu colocar este await, já sabemos o que é que falta aqui, não é? A função tem que ser assíncrona. E se a função tem que ser assíncrona, então ela tem que retornar um Future<bool>.

Agora sim, temos criado o nosso serviço. Vamos usá-lo para identificar se estamos online ou offline.

Próximo passo é então implementar o CharactersRepository. Eu vou pegar nesta classe que já tem os cabeçalhos que eu tenho que implementar. Ela basicamente vai ter que estender isto, e portanto até o mais simples é fazer aqui um copy para CharactersRepository. Deixa de ser abstrato e para já vou meter corpo vazio em cada uma delas. Claro que elas estão a dar erro porque eu não estou a retornar nada. Elas vão ter que ser assíncronas todas.

E agora, o que é que esta classe vai ter que saber? Vai ter que saber qual é o local e qual é o remote. Vou ter que ter aqui uma variável ICharacterRepository que é local e uma que é remote. E também vou ter que ter... isto vai ser bom para garantir aqui uma boa injeção de dependências... aqui o ConnectivityService. Eu não quero instanciar dentro desta classe o ConnectivityService, eu quero recebê-lo, e por isso eu quero guardá-lo numa variável.

Vou criar aqui um construtor. Eu vou colocar este construtor como named, ou seja, vou poder pôr local igual a isto, remote igual a isto, e connectivityService igual a isto, para ficar mais claro o que é que está a acontecer. Ele está a dar erro porque faltam os required.

Primeira coisa que eu vou querer fazer é verificar o estado da conectividade logo no início. Sempre que eu vou chamar uma função destas, eu vou verificar se estou online ou se estou offline. E isso é tão simples como fazer isto: eu tenho que usar este await por causa disto ser assíncrono. Ou seja, eu tenho que ficar à espera que ele me diga se está online ou offline. Não há problema porque a própria função getCharacters já era assíncrona.

E agora, se estiver online, o que ele vai fazer é retornar o remote.getCharacters. Caso contrário, vai retornar o local.getCharacters. OK, super simples! Como eu vos disse, o difícil é preparar isto para este padrão, porque uma vez preparando é muito fácil implementar aqui a classe repositório.

Agora vou fazer o mesmo para esta classe aqui: vai ser ID, aqui a mesma coisa. Estão a ver? Super simples!

E agora estas duas funções têm aqui um problema. Lembrem-se que isto abstrai a fonte de dados que está por trás. Uma das fontes de dados permite inserir personagens, mas a outra não - a API não permite inserir personagens. Nós já tínhamos visto isso. Se nós formos aqui ao LOTR Services, quando eu vou aqui ao insert e ao delete, elas não funcionam porque a API é read-only, é só de leitura, e portanto eu não consigo lá alterar dados.

E é isso que a gente vai querer fazer aqui também. O que a gente vai fazer é ser mais drásticos e dizer simplesmente: não é possível chamar o insert e o deleteAll, tal como já acontecia no LOTR Services. Se calhar aqui eu vou pôr "Not implemented"... não, é bem... é "not available", ou seja, não está disponível este serviço no repositório genérico, se quiserem.

OK, agora que tenho o meu repositório, falta-me alterar a injeção de dependências. Enquanto que eu aqui estava a injetar diretamente o serviço remoto e o serviço local, eu agora vou querer injetar... eu até posso deixar estes à mesma, nunca se sabe se serão necessários ou não... eu agora até posso injetar aqui um CharactersRepository.

Mas antes disso, eu vou extrair isto para uma variável. Já vão perceber porquê. Eles extraíram, mas possivelmente errado... não é aqui que eu quero esta variável, é aqui mesmo fora do main. E vou dizer que é um final. Vou fazer o mesmo com o Database. E agora aqui vou usar a variável em vez da chamada à função. Isto já está como expressão, esta também vou colocar como expressão.

OK, isto é exatamente o que estava antes, mas agora guardei primeiro aqui as variáveis antes de providenciar aqui no MultiProvider. Vou criar então agora um novo provider chamado... para extrair um CharactersRepository. E que ele basicamente o que vai fazer é criar um CharactersRepository que ele agora recebe estes parâmetros: o que é que é o local? É o lotrDatabase. O remote? É o lotrServices. E o connectivityService? Não o temos, mas eu vou criá-lo agora. Aqui podia também usar uma variável para ele, mas essa não tem grande valor neste momento. Vou para já deixar assim; se for preciso depois crio uma variável.

E agora, ao alterar isto, eu tenho que agora refletir isso em todos os sítios onde eu usava o provider. Ou seja, eu agora aqui vou deixar de ter estes dois objetos diferentes, vou passar a ter um único com o qual interajo, que vai ser o repositório precisamente. E isto passa a ser... quero ter repositório, deixo de precisar da base de dados - ela está escondida, eu não sei o que é que está por trás.

Eu, para já, como deixei de querer interagir com a base de dados, eu vou retirar daqui estes botões - não me interessam, porque agora basicamente o que eu vou querer é ter sempre só o getCharacters. Do Network? Ele, se estiver online, obtém da rede; se estiver offline, vai obter da base de dados automaticamente. Ou seja, isto na realidade deixa de ser "From Network Button", é "Get Characters". Vou alterar também aqui: não interessa de onde é que é, eu quero apenas obter os personagens da fonte que estiver disponível nesse momento.

Tenho então o meu repositório, e agora esta linha desaparece. Eu deixo de fazer o agulhamento aqui: deixa de ser services para passar a ser repository. E isto desaparece também. Daqui no detail, aqui passa a ser o repositório, aqui também. E retiro daí porquê? Porque aquele agulhamento agora é feito aqui dentro.

Pronto, passei a ter aqui apenas um botão "Get" que vai tratar toda esta lógica: se está online vai à rede, se está offline vai à base de dados. Falta-me acrescentar aqui um await nisto, porque isto são funções assíncronas.

Vamos agora testar. Portanto, cá está: chamada API, obteve. OK, como estou online, ele basicamente está sempre a agulhar para o remote.

Agora vamos experimentar pôr isto offline. Estamos offline, estamos em modo avião. Vamos tentar chamar o getCharacters. Ele não tenta chamar o servidor, mas não aparece nada. Nós estamos... quando estamos online, ele obtém do remote data source; quando estamos offline, ele obtém do local data source. Mas é preciso que haja dados aqui na base de dados para retornar.

O que está a faltar é nós prepararmo-nos em online para o momento em que vamos estar offline. E o que é que é prepararmos? É pegar nos dados que vieram da API, enviá-los para a base de dados, de forma a que da próxima vez, se por acaso estivermos offline, possamos ir buscá-los à base de dados. Ou seja, está a faltar estes dados terem sido enviados para a base de dados.

Então é isso que vamos acrescentar aqui. Aqui o que vamos ter que fazer é basicamente meter isto numa variável - vou chamar characters - e no meio da obtenção dos personagens e antes de os retornarmos, nós vamos guardá-los na base de dados.

Como é que a gente os vai guardar? Nós podemos ter aqui um sistema inteligente em que vamos ver que personagens é que modificaram no servidor em relação aos que estão na base de dados. Nós aqui vamos ser mais simples: vamos simplesmente apagar tudo o que está na base de dados e voltar a colocar lá, cada vez que obtemos uma listagem do servidor.

Vamos começar por chamar local.deleteAll - já sabemos que tem que ser no local, né? Não pode ser no remote. E agora vamos fazer um ciclo em que basicamente percorremos os personagens que foram obtidos a partir da API e para cada um vamos chamar o local.insertCharacter. Tão simples como isto.

Há aqui só um pormenor, que é: estas funções, quer o deleteAll quer o insert, são funções assíncronas. O que quer dizer que ele não vai prender a execução aqui neste momento. O que quer dizer que ele pode começar a inserir personagens quando o deleteAll ainda não acabou.

Eu podia fazer aqui um await para eliminar esse problema, mas isso significava que eu ia prender também o próprio getCharacters. E na realidade eu não preciso de prender - eu não quero que a escrita na base de dados ou as operações com a base de dados interfiram no desempenho desta função. O que é que é? Esta função vai buscar ao servidor os dados, a seguir fica assincronamente a escrevê-los na base de dados, mas retorna logo o que tem sem ficar à espera que isso acabe.

Então, para isso, o que eu vou fazer é garantir apenas que isto é executado assincronamente e não interfere com isto, mas que isto é executado depois disto. As funções assíncronas que retornam futures têm uma função chamada then que recebem aqui um parâmetro que não me interessa - portanto posso pôr aqui um underscore - e agora passo aqui para dentro isto.

E portanto o que isto vai acontecer é: assincronamente ele vai fazer o deleteAll, depois quando o deleteAll acabar vai inserir para cada um dos personagens, mas isto vai correr já - isto retornou. Estão a ver? Ele vai basicamente não vai ficar preso aqui, não há aqui nenhum await. Ele retorna logo os personagens e ali em paralelo vai introduzindo na base de dados.

Eu poderia fazer o mesmo aqui, mas dado que esta listagem já me obtém os dados todos que eu preciso dos personagens, não faz sentido eu aqui estar preocupado com isto. Ou seja, eu já tenho a base de dados toda preenchida. Cada vez que faço um getCharacter de ID, eu já tenho isso na base de dados, portanto não vale a pena estar aqui a complicar isto. Eu vou deixar desta forma.

E agora podemos arrancar novamente. Agora vou fazer aqui uma coisa que é para vermos isto acontecer: vou abrir aqui a base de dados, vou só fazer aqui um refresh. OK, temos a base de dados vazia.

Agora reparem: vou aqui colocar... aqui para vermos... chamada API, OK, obteve. E agora vamos aqui fazer um refresh, e cá estão todos os dados que estavam no servidor, estão agora também na base de dados.

O que quer dizer que eu agora posso fazer... posso mudar isto para offline novamente. E reparem que eu estou a obter os dados, e até podemos aqui verificar que ele não está a ir ao servidor - ele não está a escrever aqui este "get" - ou seja, ele está a obter os dados localmente.

Portanto, temos basicamente o modo offline implementado.

Em resumo, o que é que é necessário para implementar o modo offline? Primeiro, criar uma classe abstrata que tenha as funções todas da API mais uma forma de inserir e apagar objetos na base de dados para o momento em que temos que sincronizar aquilo que vem da API com aquilo que está na base de dados - criar no fundo uma réplica local.

Depois, vamos ter que ter uma classe que estende esse repositório e que implementa a lógica da base de dados, outra que implementa a lógica dos web services com API. Finalmente, um CharactersRepository que, com base no estado da conectividade, ora vai ao remote, ora vai ao local, sendo que quando vai ao remote e consegue ter sucesso, deve apagar o que está na base de dados e inserir os valores que vêm da API.

Isto tudo pode vos parecer um bocado desnecessário. Vão ver que quando fizermos testes vai dar imenso jeito a gente podermos incluir aqui os nossos próprios serviços - a base de dados e o próprio ConnectivityService - a gente controlar o ConnectivityService. 