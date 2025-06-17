# Desenvolvimento Baseado em Widgets com Flutter

Olá! Neste vídeo vou falar um bocadinho de desenvolvimento baseado em widgets usando especificamente o Flutter, embora eu ache que estes princípios se aplicam a todas as tecnologias que se baseiam em widgets.

Para isso eu vou usar aqui um exemplo: um controlador de ar condicionado com este aspecto. Isto em termos do widget é tem basicamente quatro componentes, quatro itens que é um texto onde está a temperatura aqui, um botão menos e mais que controlam esta temperatura que aqui está, e aqui um texto que vai se atualizando automaticamente segundo vamos esperar a hora atual.

Lembrar que em Flutter pelo menos, ah, nós precisamos ainda de incluir isto num widget que é ele próprio é o ecrã principal. Ah, vamos chamar controlador a ser pets, repasse que esta tem aqui um título e tem um conjunto componentes. Isto vai ser feito através de um scaffold é que temos aqui uma bar e aqui um body.

Vamos então avançar para implementação disto. Vou criar um novo projeto Flutter, vou te chamar controlador ar condicionado. Vou retirar aqui estas opções e o resto deixar tudo por omissão. Para ele quando cria um projeto queria logo este Counter, nós não queremos isto. Podemos aproveitar eventualmente só tirar daqui este comentário que temos, aproveitar este material à época aqui está, mas estas duas classes eu vou apagá-las porque vou criar aqui através do stateless.

Vou criar aqui um STF, vou criar um controlador a serpentes que é o tal que vai ser um scaffold que vai ter uma se vai chamar controlador. Vou mudar aqui também aqui no title da aplicação e vai ter um body que vai ter então os quatro componentes. Nós o body recebem, nós neste caso queremos um widget que a grupo vários vídeos, nesse caso vamos usar o column me permite a vários.

Ok, então vou organizar aqui os quatro widgets. Vou começar por criar aqui um text com a temperatura atual que neste momento vai ser fixa. Vou criar um que vai ser o menos, botão com menos e que vai ter também um pressed, ele é obrigatório tem que ter isto. Agora vou fazer o mesmo para o mais e copiar daqui o outro text que vai ser a hora e que vai ser 16 faz com que 30 e 46. Vou deixar agora fixo tudo isto e depois mais à frente vamos nos preocupar com a parte dinâmica. Neste momento quero apenas preocupar-me com o layout.

Ele está-se a queixar aqui de uma série de coisas que ele diz que prefere constante, constantes isto no início. Enquanto estamos a digamos a prototipar torna-se um bocado chato, por isso eu vou fazer aqui uma coisa que é vou chegar aqui ao analysis options e vou acrescentar esta propriedade prefer_is que é para ele não me chatear com isso e depois mais tarde eu eventualmente posso retirar aquela flag e para os conceitos.

Ok, então vamos lá ver como é que isto fica. Primeiro ainda tem que vir aqui dizer que isto afinal é o controlador a serpentes. Ok e vamos então arrancar isto. Ok, temos aqui o nosso primeiro aspeto, não tá espetacular mas é bom para começar. Temos então os quatro itens organizados numa coluna.

Uma coisa que eu posso fazer já é centralizar. E para isso vou chegar aqui à coluna e dizer que main é que seja align é center. Podemos centrar isto fazendo o wrap com um center. Ok, já está mais direitinho.

Agora vamos aumentar aqui a fonte destes, destes de estudo né, está muito pequenino. Para isso vamos usar aqui o style dentro do test e dá-lhe um textStyle com um fontSize neste caso assim bastante generoso 40. Vamos fazer o mesmo para que e também para os botões.

Vou fazer aqui uma coisa que é: vou antes que isto começa a ficar muito complicado, vou já extrair este botão para um método. Isto é uma boa prática quando vocês começam a ter aqui muito, digamos, muita configuração do widget, só para criar um componente. Vocês têm basicamente duas hipóteses: selecionam isto e ele vai-vos dar duas hipóteses interessantes que é ou é um extract method ou é um extract widget. Eu acho que não se justifica para já para criar todo um widget novo apenas para o botão menos e mais, por isso vamos começar por extrair um método.

Ele normalmente diz que o método começa por build de qualquer coisa, tá ótimo. Ah, eu neste caso vou dizer que isto é o buildMinus que é o botão menos, não é? Pronto. E para já vou eliminar isto, vou colocar dois botões menos depois logo se ajusta isso. Ok, e reparem que ele tem aqui então ele até criou desta forma.

Eu vou também fazer uma coisa que é: quando eu queria este método, ele basicamente queria isto, podia não ser feito assim. Ok, eu vou fazer assim para perceber é melhor o que é que ele está a fazer. Ok, retornar a widget. Ok, mas é uma boa prática eu dizer que isto é um widget. Eu não preciso dizer question de TextButton porque mais tarde eu posso criar é mudar aqui coisas, mas ele continua a ser um widget. Portanto vamos deixar assim por agora e pronto.

Agora temos dois menos, nada, nada, nenhum nenhum funciona. Ok, eu posso só para termos a certeza que isto tá a funcionar, posso fazer aqui um print "cliquei ou para mim menos". Pronto, e assim quando eu carregar ele parece ali para mim menos.

Ora bem, o que que eu quero? Porque que eu estou a fazer isto desta forma? Porque agora quero organizar estes dois botões ao lado um do outro, não quero que estejam por cima do outro. E para isso vou - quando eu organizo as coisas numa coluna elas chegam na vertical, mas existe um componente permitido organizar na horizontal que é o Row.

Por isso vou criar aqui um Row coisa vai ser estas duas coisas que aqui estão. Pronto, falta aqui uma vírgula e passamos a ter isto. Ele tá alinhado à esquerda mas a gente resolve já isso porque o Row também tem aqui uma mainAxisAlignment que nós podemos dizer que está ao centro. Ok, também temos então ali os dois botões.

E agora quero trabalhar esses botões para eles terem um bordo à volta. Ok, isso implica eu mudar aqui isto para estar contido num Container que tem uma decoration do tipo BoxDecoration. Ok, já temos ali, graças a este BoxDecoration, isto já começa a ter o aspecto que eu queria.

No entanto eu estou muito juntos, portanto aliás todos os componentes estão muito juntos. Portanto eu vou acrescentar aqui um bocadinho de espaço entre eles entre o text. Ou isto vai criar aqui um espaço e agora vou fazer o mesmo aqui. Vamos ver como é que isto fica. Ok, já estou a ganhar ali espaço.

E agora vou também criar aqui um espaço entre os dois botões, mas agora em vez de ser um height é um width. Ok, pronto, isto já tá com aspecto bastante parecido com o que eu queria.

E por isso agora vou fazer aqui um string label. Ok, e isto passa a ser uma label e agora aqui passo a string que eu queria aqui ao menos e aqui é um mais. Pronto, eles vão ter que ter um comportamento diferente aqui no no onPressed. Neste momento ainda consigo safar-me com a label, mas depois eles vão ter que ter um comportamento diferente e por isso vamos ter que depois preocupados com isso.

Isto já não é um buildMinus é apenas um buildButton de forma ficar genérico. Ok, temos para mim mais, para mim menos. No entanto isto tá tudo fixo. No entanto temos o nosso layout terminado para já. No próximo vídeo vou começar a dinamizar este ecrã.