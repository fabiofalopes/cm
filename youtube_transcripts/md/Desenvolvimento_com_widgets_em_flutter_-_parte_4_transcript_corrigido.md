# Transcrição Corrigida - Melhoramento do Controlador

Neste vídeo vamos melhorar um bocadinho o nosso controlador. Ele neste momento já funciona perfeitamente, isto reage aqui a estes botões. Isto é atualizado automaticamente, já vimos que isto é apenas refrescado apenas estes widgets sem afetar os outros, portanto está tudo direitinho.

O que é que se pode ainda melhorar nesta aplicação? Bem, voltando aqui a este estado da aplicação, já tínhamos visto que este 25 na realidade deve ser uma variável e essa variável deve afetar, deve ser afetada por estes botões e ela constitui o estado da aplicação. No entanto, o sítio onde nós estamos a gerir esse estado ainda não está bem - nós estamos a gerir o estado da aplicação dentro do próprio widget, ou seja, estamos a misturar um bocadinho a interface gráfica com aquilo que se chama a lógica de negócio ou a lógica da aplicação.

Então idealmente o que a gente gostaria era de isolar este comportamento numa classe própria. Podia ser por exemplo "controlador AC" que lá dentro tem uma variável temperatura e até inclusivamente tem métodos para aumentar e diminuir essa temperatura e todo o resto que nos lembramos mais tarde, mas no fundo tornar isto numa classe digamos independente da interface gráfica.

Então é isso que vamos fazer agora. Vamos criar então aqui um novo ficheiro no qual vamos criar uma classe "controlador AC". Vamos dizer que ela tem uma temperatura e agora podemos criar já um construtor com isso. E vamos dizer também que tem um bool "aumenta" - porque é boolean? Porque eventualmente nós não vamos conseguir aumentar a temperatura para sempre, né? É um controlador, a certa altura quando nós tentamos aumentar mais a temperatura ele vai parar de aumentar. Então este boolean pode ser usado para retornar true ou false - nós conseguimos aumentar ou não a temperatura.

Para já não vamos preocupar-nos com isso, vamos simplesmente fazer "temperatura++" e return - conseguimos aumentar a temperatura. Vamos fazer o mesmo para o "diminui".

Agora que temos esta classe, podemos chegar aqui ao nosso controlador e acabar com este "temperatura" que aqui está para passar a ter um "controladorAC" que é o nosso... falta em português... é o nosso "controladorAC" e agora é inicializado desta forma, ou seja, através de um construtor.

Pronto, claro que uma vez que alteramos isto, muda, não é? Portanto isto passa a ser "controladorAC.temperatura". Está aqui as chavetas, ele não está a fazer auto-complete porque isto tem que estar dentro de chavetas. OK, e aqui o setState já passa a ser "controladorAC.aumenta" - não, "diminui", claro neste caso - e ".aumenta".

Finalmente aqui outra vez... cá vamos ver se está tudo a funcionar. OK, continua tudo a funcionar lindamente, mas agora isolado numa classe.

Bem, o que é que nós ganhamos com isto? Ganhamos para já que agora é relativamente fácil eu começar a acrescentar validações, limitações, constrangimentos que não deviam estar misturados dentro desta lógica que está neste setState que é apenas de interface gráfica, mas sim dentro disto.

Ou seja, eu agora posso fazer uma coisa deste género: "se a temperatura é menor que 40" - já 40 é o máximo que o ar condicionado aguenta - então vamos permitir que aumente, mas fora disso vamos retornar falso e não vamos aumentar. Automaticamente não vamos conseguir aumentar para lá de 40.

Estão a ver? Nós agora inclusivamente, como estamos a retornar um boolean, eventualmente nós podíamos apanhar esse retorno e dar um alerta ao utilizador a dizer "atingiu o máximo da temperatura" ou "não é possível fazer essa operação", qualquer coisa deste género.

Finalmente, além de termos... podemos meter aqui esta lógica, podemos testar através de testes unitários facilmente esta classe, ao contrário das classes de interface gráfica que são difíceis de testar. Não são impossíveis, há maneira de testar, mas aí que temos que simular cliques, simular que eu clique naquele botão, agora verificar como é que ficou. Isto é bastante mais complicado de testar.

Aqui nós podemos simplesmente testar, por exemplo, que esta classe não deixa que a temperatura suba para cima de 40 graus. Como é que vamos fazer isso? Temos aqui um teste - eu vou apagar este teste então, está aqui a fazer nada - e vou criar um teste novo chamado "controladorAC_teste" porque eu vou testar o controlador AC.

E vou já criar aqui o nosso teste. Um dos testes... vou explicar muito rapidamente: temos uma função main que lá dentro tem esta função "test" que recebe uma explicação do que é que o teste vai fazer, o que é que este cenário vai testar, e depois dentro deste bloco recebe aquilo que é o teste propriamente dito. Isto é parecido com aquilo que vocês já sabem do JUnit.

Neste caso eu estou simplesmente a instanciar um objeto "controladorAC" com a temperatura 20 e a seguir verificar que a temperatura é realmente 20. Esta "expect" é equivalente ao "assert" e companhia do JUnit.

Vamos ver como é que podemos correr este teste. É só fazer isto assim, ele corre todos os testes. OK, passou. Temos a certeza que ele não passou por acaso? Vamos correr novamente agora com um erro. OK, falhou - estava à espera 19 e foi 20. Este é o output standard a que vocês estão habituados do JUnit, aqui também se aplica.

Então se quisermos fazer um novo teste para a função "aumenta" do controlador, nós poderíamos fazer desta forma: mais uma vez vamos criar aqui um controlador, agora vamos aumentá-lo e vamos verificar que a temperatura passou a 21. Podemos correr os testes... OK.

Temos também... vamos fazer um outro teste que é "não aumenta para sempre". E vamos fazer aqui um ciclo - vamos pôr aqui "for" cem vezes, não interessa - em que ele vai tentar aumentar a temperatura 100 vezes e vamos verificar que no final ele vai ter 40.

Pronto, agora sim temos a aplicação bem desenhada. A lógica de negócio está isolada da interface gráfica, estamos a testar este contexto, os widgets unitários apenas se refrescam aquilo que são necessários, ou seja, este widget refresca sozinho e estes dois em conjunto manipulam este objeto "controladorAC", esta classe "controladorAC", para produzir este efeito.

E com isto termina este curso, este mini curso sobre widgets.