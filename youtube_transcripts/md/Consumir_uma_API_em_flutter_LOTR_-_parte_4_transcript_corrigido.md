# Lord of the Rings Flutter - Base de Dados Local

Neste vídeo vamos continuar a melhorar o nosso Lord of the Rings para passar a ter uma base de dados local. Podemos ver aqui dois botões novos: um que permite obter os personagens a partir de uma base de dados local e outro que permite inserir personagens novos.

Ora bem, voltei ao início do último episódio onde tínhamos apenas isto - conseguia ter os personagens a partir da rede, a partir da API, para começarmos então a criar a partir desse ponto a nossa base de dados.

A base de dados que vamos usar é uma base de dados chamada SQLite que existe em todos os telemóveis, seja iOS seja Android, vem incluída. Não precisamos de instalar nada. No entanto, para aceder a ela vai nos dar jeito aqui uma biblioteca que é esta sqflite. Uma vez essa biblioteca, não se esqueçam de fazer pub get.

Vamos criar aqui um novo package chamado "data" e um ficheiro chamado "lotr_database" que lá dentro vamos criar um LotrDatabase. É aqui dentro que vamos usar uma classe do sqflite que é este Database. Cá está! Vamos colocar nullable ela no início vai estar a nulo e vamos criar um método init para inicializar.

Porque é que não inicializamos logo no construtor? Ou seja, neste caso no Dart não há new, mas podíamos logo criar uma instância de LotrDatabase e ele instanciava logo esta Database. Porque a inicialização desta base de dados vai ser assíncrona, ela vai demorar algum tempo porque nós não só temos que nos conectar a essa base de dados como temos que criar a própria base de dados da primeira vez. Isso pode demorar algum tempo e portanto vai ter que ser feito de forma assíncrona.

Uma vez que vai ser feito de forma assíncrona, vamos usar um esquema parecido com aquele que já tínhamos usado no repositório - não sei se se lembram - em que temos métodos, funções assíncronas que retornam futures. Então neste caso vou então criar aqui uma função que retorna um Future. Eu vou pôr Future void porque em princípio esta inicialização vai sempre correr bem, portanto não precisamos de retornar nada. E aqui dentro eu vou já colocar o código que vai inicializar a base de dados.

Pronto, copiei para aqui este código. Vou agora explicar. Ele é bastante simples. Temos aqui uma função que vem no package sqflite que permite abrir uma base de dados que começa por receber o sítio onde vamos guardar a base de dados. Neste caso é o ficheiro onde vamos guardar a base de dados. Reparem que este ficheiro é o nome que vocês quiserem dar e isto obtém o caminho dentro do file system do dispositivo para a base de dados apropriado. Isto é dependente do sistema operativo - no caso do iOS vai colocar num sítio, no caso do Android vai colocar no outro, mas ele trata disso automaticamente.

E depois temos aqui uma callback que é chamada após a base de dados ter sido criada. Ele chama esta callback que é o momento em que nós vamos aproveitar: "Olha, a base de dados foi criada, vou criar as tabelas todas." Eu aqui só tenho uma, mas posso criar várias tabelas onde vou querer guardar os meus dados.

Neste caso, isto é SQL puro: CREATE TABLE Character. OK, temos um ID que é o primary key, temos os outros atributos que já tínhamos visto antes no Character e o name é not null, mas os outros são null. Eu vou guardar o gender como integer - um no caso de ser homem e zero no caso de ser mulher. Temos também, é uma boa ideia ter esta versão aqui. Não vai, nós queremos mais tarde evoluir a base de dados. Imaginem que a aplicação já está instalada, quero manter os dados que lá estão, mas de alguma forma quero acrescentar novos campos, novas tabelas, etc. Esta versão vai dar jeito para isso.

E agora podemos chamar esta função init no main, ou seja, logo quando a aplicação arranca nós devíamos logo conectar-nos à base de dados, verificar se estão as tabelas criadas ou não. Se não tiverem, cria as tabelas. Isto só vai acontecer da primeira vez porque uma vez que a base esteja criada, o onCreate já não é chamado. Atenção, isto já só é chamado quando eu criar a base dados pela primeira vez.

E agora aqui nós vamos criar então esta base de dados. A primeira coisa que a gente vai fazer é vamos alterar este provider para passar a ser um MultiProvider. Nós vamos aqui querer ter vários objetos que vamos querer passar aos widgets, não é só já o CharacterRepository, e portanto convém ter aquilo que se chama MultiProvider.

No caso do MultiProvider eu já não tenho um create, tenho uma lista de providers e cada um deles vai ter um create. E eu vou criar um objeto provider e lá dentro passo isto que já aqui estava, mas agora posso ter vários. Esta é a grande vantagem.

Já agora convém aqui fazer isto. Isto poderá dar jeito nos testes se nós por alguma razão quisermos injetar aqui objetos fake, fake CharactersRepository. Então dá jeito eu ter aqui este tipo neste provider. Façam desta maneira mesmo que não dê erros de compilação.

Então vamos acrescentar aqui. Pronto, isto é como, digamos, exatamente o que já estava antes, mas agora já preparado para ter vários providers. Qual é o próximo provider que eu aqui quero? É precisamente o LotrDatabase. Eu podia ter feito isto como um singleton, mas uma vez que estamos nesta arquitetura de providers, eu não quero ter singletons, quero ter isto tudo com provider que é para eu depois nos testes poder injetar a minha própria base de dados.

Então vamos aqui mudar isto para LotrDatabase. OK, o que isto significa então é que eu agora dentro, a partir do contexto em qualquer widget da minha aplicação, posso obter quer um CharactersRepository quer um LotrDatabase.

E vai ser já aqui precisamente no MyApp que eu vou querer já aceder ao LotrDatabase. Para isso eu vou ter que fazer aqui uma coisa que é: uma vez que isto é assíncrono e pode demorar algum tempo, eu já não posso simplesmente abrir a aplicação e mostrar logo o CharactersListPage. Eu vou ter que chamar uma coisa que vai retornar um Future, eu vou ter que esperar que esse Future termine - estou a falar do init - ou vou esperar que isto termine. Imaginem que isto demora alguns segundos e só nessa altura é que eu vou poder mostrar então este CharactersListPage.

Então para isso vamos usar aquilo que já tínhamos usado no CharactersListPage que é um FutureBuilder em que eu vou basicamente - para quem não se lembra - registrar um Future e um builder. Este Future vai ser uma função que retorna um Future e este builder vai ser chamado à medida que esse Future vai evoluindo do ConnectionState.waiting para o ConnectionState.done.

Portanto a primeira coisa que eu vou ter que fazer, uma vez que este ecrã vai ter que mudar após acontecer alguma coisa - ou seja, ele vai começar por mostrar aqui uma rodinha e depois nessa altura mostra este ecrã que aqui está - então eu como vou ter que mudar o ecrã, eu vou transformar isto num StatefulWidget. Não pode ser um StatelessWidget porque senão eu vou ter que chamar o setState para que ele se refresque.

A seguir vou querer obter aqui logo a seguir aqui ao build, vou querer obter a minha database. Chamar assim, já sabem como é que eu obtenho a partir do contexto: faço um read e aqui coloco o que quero obter. Neste caso é um LotrDatabase. Pronto, isto vai ser exatamente o que foi passado aqui, mas no caso por exemplo de ser um teste, vai ser pode ser outra coisa que não esta que vem daqui do runApp.

Agora vou então encapsular este MaterialApp num FutureBuilder que já sabemos que não tem nada disto, tem um Future que neste caso vai ser o init do database e tem um builder. E tudo o resto que está lá dentro é aquilo que já estava, mas agora nós vamos olhar para este snapshot para perceber se já podemos mostrar isto ou não.

Ora, podemos fazer aqui um: verificar se o snapshot.connectionState do snapshot é done. Então vamos mostrar isto que era o que já estava. Caso contrário, vamos mostrar apenas uma CircularProgressIndicator aqui centrada e o MaterialApp apenas com isto, mais nada - nem título nem coisa nenhuma, apenas isto. Vai ser só durante um bocadinho enquanto ele está a carregar a base de dados. Das vezes seguintes até vai ser mais rápido já está a base de dados criada e portanto isto vai ser relativamente rápido. Mas assim temos a certeza que isto está a reagir bem ao assincronismo relacionado com este LotrDatabase.init.

Podemos já testar isto. OK, nem sequer conseguimos ver aqui nada. Eu vou fazer novamente. OK, isto é de tal maneira rápido de facto a ligação à base de dados e a criação que não vemos nada, mas mesmo assim é uma boa ideia fazer desta forma. Se tiverem várias tabelas e se tiverem de carregar muitos dados para a base de dados, é uma boa ideia terem este CircularProgressIndicator aqui enquanto ele está a pensar.

Então como é que eu sei que esta base de dados já foi criada? Na realidade o Android Studio permite ver o conteúdo da base de dados SQLite através deste App Inspection que está aqui. Se por acaso não vos aparecer isto, venham aqui ver se ele não estará por aqui. E quando carregam no App Inspection aparece-vos aqui o emulador. Vocês têm que vir aqui escolher a aplicação que não está... Ele demora um bocadinho, esperem um bocadinho e ele eventualmente vai então aparecer aqui este Database Inspector.

Conseguem ver que foi criado aqui um ficheiro lotr.db que lá dentro tem uma tabela Character com estas colunas. Portanto ela neste momento está vazia, mas tem o conteúdo que a gente quis para ele.

Então agora que temos a base de dados criada, podemos começar a implementar a inserção e a obtenção de dados a partir da base de dados. Vamos começar pela obtenção de dados.

Para isso vamos começar por olhar aqui para o modelo e lembrar que isto é aquilo que representa um personagem em memória. OK, isto é agnóstico daquilo de onde vem, ou seja, independentemente disto vir de uma API, de vir da base de dados, do que é que a gente tenha como fonte de informação, nós definimos que cada personagem tem estes campos. Isto até está fora de ordem, eu acho que isto prefiro isto aqui. OK, já agora pronto, reorganizei isto, mas basicamente isto é aquilo que me interessa a mim programador independentemente da fonte de informação.

Por acaso aqui tenho este fromMap que deu imenso jeito - não sei se se lembram - para obter a partir do JSON que vinha da API, criar um objeto do tipo Character com base no que vinha no JSON. Este map que aqui está era obtido a partir do JSON que era aqui no CharacterRepository. Eu obtinha uma lista por exemplo de characters e a seguir fazia este fromMap ou então aqui diretamente neste getCharacter também fazia aqui um fromMap.

Então este fromMap na altura fez sentido, mas agora eu vou querer obter o meu Character de dois sítios diferentes, duas fontes de informação diferentes. Ou ela vem da API e nesse caso vem a partir do JSON, ou ela vem a partir da base de dados e nesse caso o que a base dados me vai dar é um map. E portanto eu, para distinguir os dois - vez que o JSON também é map, também map - eu vou criar aqui, vou fazer aqui um refactor e mudar isto para fromJSON e vou criar uma coisa parecida chamada fromDB.

Ou seja, fromJSON vem da API, fromDB vem da base de dados. Aqui até vou mudar se calhar isto para ficar mais claro: para JSON e este para DB. Pronto, na DB por exemplo não há este underscore ID, isto era uma coisa que era do JSON, portanto eu vou deixar este assim.

Outra coisa que acontece é que o gender que a gente tem aqui é uma string que - não sei se se lembram - pode ser "male" ou "female", mas na base de dados nós resolvemos guardar isso - deixem-me recordar - como integer em que 1 era male e 0 era female. Ou seja, vamos fazer essa transformação aqui. Portanto se o que vem da base de dados é um 1, então nós vamos transformar isso em "male". Na base de dados está um 1, aqui vai estar "male". No caso contrário vai ser "female".

Feito isto, podemos vir aqui ao nosso LotrDatabase e criar uma nova função que também vai ter que ser um Future, mas agora vai ser uma List<Character> getCharacters(). Isto deve parecer familiar porque nós já fizemos uma função muito parecida com esta. Se nós formos aqui ao repositório, temos precisamente aqui um Future<List<Character>> getCharacters(). Vamos deixar assim.

E o que isto vai fazer é obter uma lista dos personagens que estão na base de dados, não na API. Para isso vamos usar o nosso database, a nossa variável database, mas temos aqui um problema: é que esta database pode estar a null. Nada me garante que alguém se lembrou de chamar este init. Começar por validar que o database é diferente de nulo, porque se for nulo a gente vai logo lançar uma exceção para indicar: "Atenção que te esqueceste de inicializar a database."

Temos um método dentro do database que nos permite correr queries, fazer selects neste caso. Ou seja, o que eu vou fazer é um SELECT * FROM Character. Para isso vou usar o rawQuery. Posso fazer este database ponto exclamação porque já verifiquei ali que ele não é null. E isto é assíncrono, logo devo fazer um await à espera do resultado.

O resultado vai ser uma lista de Map e por isso o que eu vou fazer é vou precisamente usar o map - agora para outra coisa - a função map que já usei no CharactersListPage para transformar cada uma das entradas desta lista que são Maps que vêm da base de dados nos Maps nos Characters. Para isso é que nós usamos aquele fromDB precisamente para isso.

Então basta fazer desta forma: ou seja, para cada entrada que está nesta lista eu vou obter uma entry que é um map que vai entrar dentro deste fromDB que foi aquele que a gente criou há pouco. Cá está! E ele vai-me criar uma lista de Characters.

Mesmo com isto eu já posso obter aqui, se calhar criar aqui o botão para obter os characters a partir da base de dados, que é isso que vamos fazer agora.

Então vamos começar aqui por transformar este botão que aqui está "Get characters from network" e agora vou mudar também aqui, fazer aqui um refactor para buildGetCharactersFromNetworkButton. Vou criar uma função parecida que vai ser o fromDB e aqui é "from database". Isto até é igual, o buttonPressed está igual a true, mas vamos ter que distinguir se eu carreguei num ou no outro.

Então para isso eu vou criar aqui uma nova variável que lhe vou chamar source que inicialmente vai estar a null, mas que nós vamos preenchê-la da forma correta. Como aqui vamos transformar isto em vez de ser uma expressão num bloco para podermos ter duas instruções, e agora vamos dizer que a source neste caso foi "network" e vamos fazer o mesmo aqui, mas agora a source é "db".

Portanto o que é que ganhamos com isto? Nós agora aqui vamos poder distinguir neste Future onde é que nós queremos ir buscar os characters. Se queremos ir buscar ao repositório ou à base de dados.

Mas antes disso eu tenho que mudar isto. Ele neste momento apenas mostra o getFromNetworkButton. Eu vou transformar isto numa Column de forma a que consiga colocar aqui o getCharactersFromDBButton. Já agora deixa-me só verificar aqui uma coisa. Eu acho que isto não é necessário, a gente não está a usar isto. Portanto vamos apagar, correr isto novamente.

OK, temos este problema aqui. Já sabemos como resolver, penso eu que já sabem. Isso é só chegar aqui à Column e dizer que o mainAxisAlignment é center.

Vamos então aqui usar: no Future, se o source for igual a "network", então nós vamos dar aquilo que já tínhamos que era "vai ao repositório obter o characters". Caso contrário vamos... ah, não temos a base de dados. Espera lá, precisamos aqui de obtê-la. Cá está, por injeção de dependências muito facilmente obtemos a base de dados. E está ela. E portanto vamos aqui chegar aqui e fazer database.getCharacters().

OK, tão simples como isto. Portanto se a source for "network", então obtém da rede. Se não, obtém da base de dados. Perfeito! Tudo o resto é igual porque reparem que a lista que nós passamos para aqui já é uma lista de Characters. Quer num caso quer noutro, nós estamos a obter uma lista de Characters. Portanto já temos objetos que já são independentes quer da rede quer da base de dados.

Então vamos ver se isto está a funcionar. Vamos obter os characters da base de dados. Não aparece nada.

Agora temos aqui um problema que eu também quero resolver que é: não temos maneira... como isto é a própria página, isto não foi um push, isto é a própria página que eu estou a mudar e agora não tenho maneira de fazer back. Portanto vamos alterar aqui esta lista para passar a ter aqui um botão back. Até ficam a saber como é que podem acrescentar o vosso próprio botão back neste AppBar.

Vamos aqui começar por colocar esta vista, esta lista, num widget chamado Expanded. Agora vamos colocar isto numa Column. Lá dentro vai estar este Expanded, mas antes disso vamos criar um ElevatedButton já lá vamos, cujo child vai ser um Text("Go back"). OK, vamos ver.

Portanto se eu agora fizer isto, eu já tenho um "go back". O go back ainda não faz nada, mas na realidade o que é que é o go back neste caso? Vamos olhar para aqui e reparar que se o buttonPressed tiver false, os botões para obter a lista. Caso esteja a true, então vai mostrar o resultado da source.

Ora, se a gente meter o buttonPressed a false, ele automaticamente - com setState claro - ele automaticamente vai passar a mostrar os botões novamente. É como se eu já não tivesse carregado no botão. Então novamente aqui, cá está ele a funcionar. E também podemos ver se... cá está, o Characters também tem um "go back" porque a gente colocou isto no buildList que é usado pelos dois. Portanto as duas listas são feitas exatamente da mesma forma.

Isto era expectável. Não temos nada na base de dados, portanto está na altura de criarmos aqui um character na base de dados. Para isso vamos acrescentar aqui um novo botão buildInsertCharacterButton que não tem nada a ver com isto e que basicamente vai chamar o database que nós ainda não temos aqui, vamos ter que lhe passar, e que a gente vai basicamente nesse botão fazer o insert. Nós ainda não temos isso lá.

Vamos começar por criar aqui uma forma de inserir um personagem. Começar por criar aqui uma função que tem que ser assíncrona mais uma vez, que recebe um Character - o tal modelo - e retorna um Future<void>. Neste caso o insert não retorna, não há grande coisa para retornar.

E agora vou voltar a fazer esta validação que aqui está. Isso tem que estar em todos. E só depois fazer esta validação é que eu vou então poder chamar o insert do database. Portanto o database tem uma função que me permite inserir na tabela Character um objeto desta forma. E eu aqui tenho que receber um map com os dados que eu quero inserir. E falta-me este toDB que ainda não existe.

Vamos criá-lo. Basicamente o que isto faz é converter a informação interna do Character num map que eu posso enviar para a base de dados. Vamos criar uma função toDB que retorna um Map em que a chave é String e o valor pode ser qualquer um - pode ser inteiro, string, o que quer que seja - e por isso é que pusemos aqui este dynamic.

Isto basicamente vai retornar um map em que por exemplo o ID é o ID desta classe. Este é fácil. O name é o name desta classe. Estes dois são os parâmetros obrigatórios, mas os outros podem ou não estar preenchidos. Então para evitar que eu tenha dados a mais neste... não é que fizesse mal estar lá nulo, eu podia pôr por exemplo "birth": null, mas para ficar melhor eu vou fazer isto: ou seja, se o birth for diferente de nulo, então eu preencho isto, senão nada, não acontece nada. É possível fazer isto em Dart. E vou fazer o mesmo para o death.

E finalmente para o gender que é um bocadinho diferente. Lembro que o gender na base de dados é um inteiro. Ou seja, este gender que aqui está é uma string, mas o que vai para a base de dados tem que ser um inteiro. E por isso eu tenho que verificar: se o gender for "male", então aquilo que vai para a base de dados é um 1. Caso contrário é zero.

Tenho o meu toDB concluído. Lembro que era aqui que eu queria usá-lo. Ou seja, ele vai pegar nos dados do Character que recebeu aqui, convertê-lo para tal map, inseri-lo nesta tabela Character através desta referência para a database.

Vou simplesmente chamar o database.insert e aqui vou inserir um Character aleatório. Para ele ter um ID sempre diferente, eu vou-lhe dar aqui um Random. Vou usar aqui isto: esta função Random().nextInt(100). Portanto um inteiro entre 0 e 100 aleatório. Vou-lhe também dar um name - pode ser "Pedro" - e um gender - neste caso pode ser "male" - e não vou preencher o nascimento nem a morte. E ele vai sempre inserir um Pedro male, mas com um ID diferente cada vez que carregamos no botão.

O que eu queria chamar atenção: este insert é assíncrono. O que quer dizer que este onPressed vai terminar e isto ainda não terminou, isto ainda vai ficar a correr lá atrás. Nós não estamos, não vou fazer um await disto para não prender o ecrã. Não, isto se calhar devia também ter aqui um FutureBuilder associado, mas para simplificar agora o código não vou me preocupar com isso. Isto na prática não vai ter grande efeito porque o tempo que demora ele a inserir é suficientemente rápido para que eu a seguir possa carregar no "Get characters from database" e ele funcionar bem sem qualquer problema. Portanto vou deixar isto assim.

Falta-me claro acrescentar isto à interface. Criei a função mas não criei a interface. Portanto falta-me aqui o buildInsertCharacterButton. Certo, agora sim, cá está.

E vamos inserir. Ele não dá feedback nenhum, mas provavelmente inseriu. Vamos ver... não inseriu. Vamos carregar agora... sim, cá está ele. Se eu inserir novamente... cá está ele.

E podemos também verificar que aqui no App Inspector, fizemos aqui um refresh... cá está! Foi gerado um ID 27, um aleatório, ID 63. O resto dos campos estão a null, mas de resto está tudo OK.