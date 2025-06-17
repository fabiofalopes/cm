# Consumir uma API em Flutter LOTR - parte 1

Nesta série de vídeos vou-vos mostrar como implementar esta aplicação que obtém todos os personagens da trilogia do Senhor dos Anéis a partir de um servidor. Por isso é que isto demora algum tempo. Para cada personagem indica se é um homem ou uma mulher através deste ícone, e eu posso clicar em qualquer personagem para saber em que ano nasceu e morreu e mais informação se quiser.

Neste primeiro vídeo ainda não vou ligar isto ao servidor, vou mostrar isto apenas mas com uma lista fixa de personagens. Como é que vamos implementar este componente que é uma ListView e como é que ele navega para o respectivo detalhe e volta à ListView.

Ora bem, já criei um projeto Flutter vazio. Neste momento apenas tem aquilo que vem por omissão quando criamos um projeto. A única coisa que fiz foi acrescentar aqui neste ficheiro analysis_options estas rules para ele não chatear muito com os warnings nesta fase.

Portanto temos o nosso main default com que ele normalmente é criado. Eu vou já apagar aqui isto e vou também apagar esta classe HomePage. Vou deixar só mesmo aqui esta parte. Este HomePage vai mudar depois, já lá vamos.

Vamos começar por criar então uma pasta pages no qual vamos criar a nossa página que vai mostrar a lista de personagens. Vou chamar CharactersListPage. Ela vai ser um widget. Vou começar por criar um widget CharactersListPage. Vamos importar isto que aqui está. Enganei-me aqui a escrever isto aqui um ref e vou já mudar aqui isto para CharactersListPage. Não tem um title, portanto vamos apagar e vamos então arrancar isto como está neste momento.

OK, temos um placeholder. Não é o que queremos. Vamos já começar por mudar isto para um Scaffold. Vai ter uma AppBar, neste caso vou lhe dar um título "Lord of the Rings" e vou também colocar aqui um body que para já vai ser um botão com o texto "Get Characters" e falta-me o onPressed. Para já não vai fazer nada. Vamos ver como é que isto fica.

OK, o botão vamos centrá-lo. Vamos colocá-lo no Center e aqui está ele. Temos o nosso ecrã inicial.

OK, o próximo passo seria mostrar a lista dos personagens, mas antes disso temos que criar os objetos que vão guardar essa informação. Lembrem-se que deve haver uma separação clara entre interface gráfica e lógica de negócio. Neste caso a lógica de negócio são os objetos que representam cada um dos personagens.

Vamos colocá-los numa pasta Model e aqui dentro vamos criar um ficheiro Character que lá dentro vai ter uma classe Character que vai ter alguns dos atributos que estão normalmente associados às personagens: um identificador, uma data de nascimento, uma data de morte, o género masculino ou feminino, e um nome.

Reparem que estes três atributos estão opcionais, ou seja, eles podem ser null. Este o identificador e o nome são obrigatórios. Ele agora está-se a queixar porque eles têm que ser inicializados, mas isso vai ser já resolvido aqui com o construtor.

E agora quero chamar a atenção - eu não gosto muito destes construtores - quero chamar a atenção para a diferença entre este construtor e o construtor que eu vou querer usar. Vou aqui criar uma função main só para perceberem a diferença.

Eu posso criar um personagem chamando o construtor obviamente, mas reparem que eu tenho que preencher os cinco atributos mesmo eles não existindo. Por exemplo, o ID tem que existir, mas por exemplo isto pode estar a null, isto pode estar a null, isto pode estar a null e este tem que existir. Ou seja, eu tenho que estar a passar estes nulls. Portanto atributos opcionais eu sou obrigado à mesma a preenchê-los neste construtor.

Além disso, assim de repente eu não consigo lembrar-me se este null é a data de nascimento ou a data de morte, se este é o género ou é outra coisa. Então o ideal era que conseguisse por um lado só passar os atributos que me interessam e por outro que os conseguisse distinguir facilmente, perceber facilmente o que é que representa cada atributo.

E para isso nós vamos colocar aqui umas chavetas. Basta fazer isso aqui à volta dos atributos. Ao fazermos isso ele vai-se queixar que este atributo tem que ter aqui um required porque é um atributo obrigatório. Este é opcional, este é opcional, este também tem aqui um atributo e a gente faz o que ele diz - tem que ter aqui um required porque é um atributo obrigatório.

E agora vamos voltar a fazer a mesma coisa e reparem como agora ele para já mostra só - mostra já por nome, diz-nos que o primeiro atributo é o id e o segundo é o nome com aqueles dois pontos e mostra-nos apenas os atributos obrigatórios. Portanto eu apenas preciso de preencher os atributos obrigatórios. Eventualmente se quiser preencher os outros atributos tenho que dizer qual é o nome desse atributo, posso passá-los por qualquer ordem, não tem que ser pela mesma ordem que está no construtor, passar assim desta forma.

Ou seja, eu gosto bastante mais destes construtores com argumentos com nome em vez de argumentos posicionais e por isso recomendo que façam o mesmo.

Feita esta explicação, vamos então avançar. Agora que temos a nossa classe Character, quando nós carregarmos neste botão o que nós queremos é que ele nos retorne uma lista de objetos deste tipo. Para isso nós vamos criar aqui uma nova pasta chamada repository, porque normalmente é boa prática nós criarmos uma classe à qual chamamos repository que indica quais são as funções que estão disponíveis na API para obtermos ou enviarmos informação.

Então vou chamar esta classe CharactersRepository e vai ser também uma classe CharactersRepository. E esta classe vai ter apenas duas funções. Vamos importar. Portanto vai ter uma função que retorna uma lista de personagens e uma função que dado um ID retorna informação sobre esse personagem.

Neste momento como nós não estamos a ir ao servidor, estas funções vão retornar a informação fixa. Ou seja, eu vou retornar aqui - com esta anotação isto representa uma lista em Dart - e aqui dentro eu vou criar Pedro e vou também dizer que o gender é male. Vou criar outro.

Já agora, esta representação do gender talvez não seja a mais apropriada como string, mas vai ser a forma como a API nos vai retornar. Então isto facilita já aqui a tradução depois daquilo que vem da API para o programa.

Aqui neste caso eu vou retornar sempre o mesmo personagem e agora criar aqui uma classe CharactersRepository. Depois no onPressed vou chamar repository.getCharacters.

OK, nós agora vamos querer guardar isto aqui numa variável. Vamos guardá-lo numa variável aqui da classe porque isto vai dar jeito estar cá fora. Uma variável characters que vamos inicializar a vazio. Isto deixa de ser const e agora vamos atribuir a essa variável o valor retornado por esta função.

Agora o que é que nós queremos? Queremos que quando essa variável for vazia ele mostra o botão, mas quando estiver preenchida mostro uma lista. Para isso acontecer, isso significa que este widget vai ter que mudar após a gente carregar no botão. Para ele mudar ele tem que deixar de ser StatelessWidget porque os StatelessWidget nunca mudam depois de ser criados.

Portanto vamos converter isto para StatefulWidget. Agora uma vez que ele está criado já podemos chamar aqui o setState porque nós queremos que após ele atualizar o characters que ele refresque o widget, que ele volta a chamar o build.

Claro que agora quando voltar a chamar o build nós não queremos voltar a mostrar o botão, nós queremos mostrar a lista. E portanto vamos ter que ter aqui uma separação. Aqui dentro deste body vamos ter que ter basicamente um que indica se a lista de personagens está vazia então mostra o que está agora, se tem personagens então mostra uma lista.

Criar aqui usar o operador ternário para indicar aqui com o ponto de interrogação: ou estamos perante uma situação em que a lista está vazia, nesse caso mostra isso, ou caso contrário estamos numa situação em que vai mostrar a lista. Por agora eu vou criar um Text "lista" só para exemplificar.

Vamos então correr novamente e cá está. Quando carregamos no botão ele transforma em lista. Agora só temos que em vez deste texto com uma lista colocar aqui uma lista verdadeira.

Antes de mais quero - eu estou a achar já este código um bocado complicado demais. Eu vou fazer o seguinte: eu vou extrair daqui um método que vou lhe chamar buildGetCharactersButton. OK, já ficou bastante mais simples. E agora neste TextList vou fazer a mesma coisa que vou chamar buildList. Para já vamos fazer aqui uma coisa. Isto vai passar a ser um widget e este também vai passar a ser um widget.

Vamos então converter isto para uma lista. Vamos começar por transformar isto num bloco e agora vamos em vez do Text usar um componente chamado ListView que é o componente que é usado para criar uma lista. E vamos chamar um construtor chamado separated porque nós queremos que os items apareçam separados com uma linha entre eles.

Para já vou deixar isto assim, vou só dar aqui um formato e vou aqui preencher já algumas coisas. Isto na realidade é um index para alguma coisa, este a mesma coisa. Antes de explicar então o que é que isto significa: ele recebe três parâmetros. Um deles é bastante - o itemCount que é quantos elementos tem a lista. O itemBuilder vai ser responsável por construir para aquele index indicado qual é o componente que vai representar essa linha. E o separatorBuilder vai ser responsável por dizer qual é a divisão que deve ser aplicada para aquele index.

Vamos começar pelo itemCount. Muito simples, não é? Se nós temos já uma variável characters está preenchida com o tamanho, então é só usar o length para obter o itemCount.

O itemBuilder vamos usar aqui um componente chamado ListTile que é um item de uma lista. E o ListTile tem um title que nós para já vamos dizer que é igual ao index.

Finalmente aqui vamos colocar este Divider que basicamente é uma linha com esta largura, com esta espessura e de cor cinzenta que vai separar cada um dos items.

Vamos então ver como é que isto fica neste momento. Ora bem, temos então neste momento 0 e 1 porque o que nós estamos a fazer é cada ListTile mostra o index no qual está, ou seja, ele começa por chamar com o zero e a seguir com o um.

Nós vamos querer agora alterar isto para passar a ter o nome do personagem. Como é que vamos fazer isso? Em vez do index vamos outra vez ao characters mas na posição index, porque o characters é uma lista, portanto nessa posição nós vamos querer obter o name. E passamos a ter então aqui os nomes.

Outra coisa que queremos melhorar é acrescentar aqui um ícone no início para indicar se é um homem ou uma mulher. Para isso vamos usar aqui uma propriedade que é o leading. O leading permite atribuir um widget ao início do ListTile aqui encostado à esquerda.

Nós vamos querer que isso seja um Icon e temos aqui Icons.man. OK, para já vou pôr todos como se fosse é um homem, mas na realidade nós queremos distinguir consoante a personagem é homem ou mulher. E para isso nós vamos criar aqui outra vez uma condição com o operador ternário em que basicamente vamos questionar o gender: se for igual a "male" então é este, caso contrário vamos voltar a verificar se é feminino porque pode não ser nenhum deles. Deixa aqui ajustar isto.

Finalmente vamos dizer que no caso não seja nenhum deles vamos... Vamos formatar isto para perceber melhor. Portanto vamos lá então: se o gender é "male" então vai colocar um Icons.man, caso contrário se for "female" vai colocar um Icons.woman, caso contrário não é nem male nem female então vai colocar... Vamos ver.

E já cá está então o ícone diferente em cada um deles. Quase a terminar a nossa aplicação, mas falta ainda quando se clica em cada uma destas items ele abrir o detalhe correspondente a este personagem.

Para isso vamos criar uma nova página, novo widget ao qual vamos chamar CharacterDetailPage. Este widget tem aqui algumas características que quero chamar atenção. Uma delas é que recebe no construtor o characterId, ou seja, nós quando criamos este widget temos que indicar qual é o identificador do personagem para o qual queremos o detalhe.

Depois no build obtemos o CharactersRepository tal e qual já acontecia no CharactersList, mas a seguir chamamos a função getCharacter com o characterId de forma a obter o objeto com os seus dados. Uma vez obtidos os seus dados eu posso criar aqui um AppBar com o texto com o ID que era o identificador e por exemplo no body colocar Text character.name.

Finalmente eu vou querer aqui neste ListTile apanhar o evento de clicar lá, de selecionar ou de fazer tap para então saltar para a página respectiva. Como é que eu vou fazer isso? Há aqui um atributo chamado onTap que basicamente recebe uma função que é chamada quando carregamos neste item. E o que eu quero fazer é fazer um Navigator.push, passo-lhe o context e passo este objeto MaterialPageRoute que recebe um builder que eu vou preencher desta forma.

Falta-me aqui o characterId. Como é que eu obtenho o characterId? É simples, é só pegar aqui no characters[index] e colocar o id dele.

Esta é a forma que temos de navegar fazendo um push de um novo ecrã em cima do que já está. Quando usamos este push o que significa é que ele permite que a gente faça back automaticamente do ecrã para o qual fomos. Se nós fizermos - quisermos que ele faça back - quisemos que ele substitua mesmo, nós podemos fazer um pushReplacement. Neste caso queremos um push porque eu quero que após ver o detalhe ele volta atrás, possa voltar atrás e voltar à lista.

Vamos testar isto. Aparentemente não aconteceu nada, mas eu agora quando clico aqui ele já me salta para o detalhe. E reparem que ele aparece sempre aqui Pedro. Isto é uma razão - para se já não se lembram - tem a ver com a forma como nós criamos o repository. Nós dissemos que independentemente do id que aqui aparece a gente vai sempre retornar Pedro. É por essa razão que neste momento isto está errado. Quando nós ligamos isto, isto vai passar a funcionar corretamente.

Vamos só aqui afinar um bocadinho este ecrã. Isto devia estar centrado. Vamos fazer um wrap com Center e vamos também aumentar um bocado o tamanho dele. Vou meter aqui um style TextStyle e dizer que o fontSize é 40.

E vamos também colocar aqui uma imagem em cima de um anel até porque é interessante - pode ser interessante saberem usar imagens. Esta imagem neste caso ela vem de um endereço, vem da net, não está incluída na aplicação.

Temos que fazer um wrap com um Column para poder ter aqui vários items alinhados na vertical. E agora em cima deste nós vamos colocar uma Image. Vamos dizer que tem tamanho 150 e que a image em si é uma NetworkImage e vamos lhe passar este endereço.

Vamos refrescar. Ah, ele ao colocar uma Column nós temos que alterar aqui o mainAxisAlignment para passar a ser Center. E vamos meter aqui mais - já que estamos aqui a alterar isto muito rapidamente - aqui duas informações. Vamos colocar aqui duas informações: da data de nascimento e a data da morte.

Vou só dar aqui também um style a estes dois componentes. Neste caso eles estão a null porque nós não temos essa informação aqui no nosso repository. Vamos preencher.

Pronto, temos então a nossa aplicação terminada. Mostra sempre a mesma coisa. Vamos melhorá-la agora ligando a API no próximo vídeo. 