<td style="width: 20%;"><img src="/img/Logo_CEFET-MG.png" width="20%" /></td>

# Introdução ao Shell Script no Linux
<p><strong><span style="color: #0000ff;">Internet das Coisas - Kit de desenvolvimento SBC com Linux</span></strong></p>
<p><strong><span style="color: #0000ff;">Prof Epaminondas Lage</span></strong></p>
<a href="http://lattes.cnpq.br/7787341723868111"> Currículo Lattes LAGE, E. S.</a> 

# Índice deste Repositório

* [Shell Script no Linux com OrangePi One](#Shell-Script-no-Linux-com-OrangePi-One)
* [Introdução ao Scripts em Shell](#Introdução-ao-Scripts-em-Shell)
* [Criação do shell script](#Criação-do-shell-script)
* [Comandos básicos do editor vim](#Comandos-básicos-do-editor-vim)
* [Comandos básicos do editor joe](#Comandos-básicos-do-editor-joe)
* [Concedendo permissões ao arquivo](#Concedendo-permissões-ao-arquivo)
* [Edição e execução do arquivo](#Edição-e-execução-do-arquivo)
* [Inserindo comentários](#Inserindo-comentários)
* [Declarando e utilizando variáveis](#Declarando-e-utilizando-variáveis)
* [Atribuindo saídas de comandos a variáveis](#Atribuindo-saídas-de-comandos-a-variáveis)
* [Capturando a entrada de dados do usuário](#Capturando-a-entrada-de-dados-do-usuário)
* [Comandos de seleção ou de tomada de decisão](#Comandos-de-seleção-ou-de-tomada-de-decisão)
* [O comando if](#o-comando-if)
* [O comando else](#o-comando-else)
* [O comando elif](#O-comando-elif)
* [O comando case](#O-comando-case)
* [Loops condicionais](#Loops-condicionais)
* [Loop while](#Loop-while)
* [Operadores Aritméticos em Shell Script](#Operadores-Aritméticos-em-Shell-Script)
* [Operadores Relacionais em Shell Script](#Operadores-Relacionais-em-Shell-Script)
* [Operadores Lógicos em Shell Script](#Operadores-Lógicos-em-Shell-Script)
* [Funções](#Funções)
* [Gerenciando a execução de um script](#Gerenciando-a-execução-de-um-script)
* [Lendo um pino de I/O por interrupção no Linux](#Lendo-um-pino-de-IO-por-interrupção-no-Linux)
* [Status do Projeto](#Status-do-Projeto)
* [Bibliografia](#Bibliografia)

# Shell Script no Linux com OrangePi One

Orange Pi One is an open-source single-board computer. It is highly compact with a dimension of 69X48mm. It can run Android 4.4, Ubuntu, Debian Image. 
          	
Podemos utilizar a criação de arquivos de scripts para tornar mais simples as execuções de tarefas repetitivas no dia a dia. Muito tempo do programador é empregado em ações desse tipo, como abrir os mesmos programas todos os dias; esvaziar a lixeira e diretórios temp para economizar espaço em disco; etc.

Um script nada mais é do que um algoritmo projetado para realizar uma determinada tarefa, utilizando os comandos específicos do bash e os executáveis do sistema operacional.

Lembre-se de executar os comandos como usuário comum e não como root, visto que, como root tudo será aceito e, dependendo do que você fizer, isto pode gerar danos ao sistema operacional. Uma maneira fácil de verificar é abrir o terminal e se o símbolo antes do cursor é o "˜", você está como usuário comum, mas se é o "#", você está como root. Para sair do modo root, digite exit.

Para executar estes shell scripts vamos usar o Kit GPIO SBC Linux conforme Figura 1 , um ponto de acesso à rede ethernet na mesma faixa de rede dos microcomputadores que serão utilizados para acesso remoto às OrangePi One conforme a Figura 2.

<table style="border-collapse: collapse; height: 321px;">
<tbody>
<tr >
<td style="width: 50%;"><img src="/img/kit2.jpg" width="50%" /></td>
<td style="width: 50%;"><img src="/img/rede_iot.png" width="100%" /></td>
</tr>
<tr style="width: 100%;">
<td style="width: 50%;">Figura 1. Kit GPIO SBC Linux.</td>
<td style="width: 50%;">Figura 2. Rede Local IoT.</td>
</tr>
</tbody>
</table>

# Introdução ao Scripts em Shell

Podemos utilizar a criação de arquivos de scripts para tornar mais simples as execuções de tarefas repetitivas no dia a dia. Muito tempo do programador é empregado em ações desse tipo, como abrir os mesmos programas todos os dias; esvaziar a lixeira e diretórios temp para economizar espaço em disco; etc.
Um script nada mais é do que um algoritmo projetado para realizar uma determinada tarefa, utilizando os comandos específicos do bash e os executáveis do sistema operacional.

    Lembre-se de executar os comandos como usuário comum e não como root, visto que, como root tudo será aceito e, dependendo do que você fizer, isto pode gerar danos ao sistema operacional. Uma maneira fácil de verificar é abrir o terminal e se o símbolo antes do cursor é o $, você está como usuário comum, mas se é o #, você está como root. Para sair do modo root, digite exit
    
    Devemos portando criar um usuário para que possamos trabalhar com segurança. O comando "adduser" serve para adicionar um usuário ou um grupo ao sistema, onde será criado um diretório com o nome do usuário, com uma entrada para o usuário no arquivo /etc/passwd (senhas). A utilização do comando adduser necessita do uso do comando sudo (deve estar com previlégio de root).
    
Além disso, quando é adicionado um novo usuário, é criado, por padrão, um grupo com o nome do mesmo usuário. Caso seja criado um novo grupo, o comando adduser cria uma entrada para o grupo no arquivo /etc/group. 
    
    root@orangepione:~# adduser aluno
	Adding user `aluno' ...
	Adding new group `aluno' (1002) ...
	Adding new user `aluno' (1002) with group `aluno' ...
	Creating home directory `/home/aluno' ...
	Copying files from `/etc/skel' ...
	Enter new UNIX password: 
	Retype new UNIX password: 
	passwd: password updated successfully
	Changing the user information for aluno
	Enter the new value, or press ENTER for the default
		Full Name []: 
		Room Number []: 
		Work Phone []: 
		Home Phone []: 
		Other []: 
	Is the information correct? [Y/n] Y
	root@orangepione:~# 

Portanto pode-se sair da sessão e fazer ssh com o usuário "aluno"  e senha "cefet" recém criado.

	ssh aluno@ip_orangepi
	senha:cefet

<table border="0">
<tbody>
<tr>
<td><img style="display: block; margin-left: auto; margin-right: auto;" src="/img/epaminondaslage_ssh_aluno.png" width="50%" /></td>
</tr>
<tr>
<td style="text-align: center;">Figura 3. Tela de login via ssh.</td>
</tr>
</tbody>
</table>

# Criação do shell script

Em primeiro lugar precisaremos de um arquivo para escrever o nosso script. Podemos fazer isso via terminal ou via modo gráfico, sendo que, no último caso, basta apenas clicar com o botão direito do mouse em um diretório desejado e escolher criar novo arquivo de texto ou criar novo documento.

Para criar um arquivo via terminal, basta abrir o mesmo e digitar vi exemplo1.sh, também podemos digitar touch exemplo1.sh

O comando vi cria e abre um arquivo para leitura/escrita no terminal, enquanto o comando touch cria um arquivo, mas não o abre. Posteriormente é possível abri-lo com um editor de sua preferência.

# Comandos básicos do editor vim

<table border="0">
<tbody>
<tr>
<td><img style="display: block; margin-left: auto; margin-right: auto;" src="/img/vi_comandos-1.png" width="80%" /></td>
</tr>
<tr>
<td style="text-align: center;">Figura 4. Comandos Básicos do Vim.</td>
</tr>
</tbody>
</table>
 
<table border="0">
<tbody>
<tr>
<td><img style="display: block; margin-left: auto; margin-right: auto;" src="/img/vim.png" width="50%" /></td>
</tr>
<tr>
<td style="text-align: center;">Figura 5. Tela de help do Vim.</td>
</tr>
</tbody>
</table>
 
# Comandos básicos do editor joe

Caso o SO Linux não tenha o  joe instalado, é necessário dar o comando abaixo para instalar o editor de textos. 

	apt install joe

<table border="0">
<tbody>
<tr>
<td><img style="display: block; margin-left: auto; margin-right: auto;" src="/img/editor Joe.png" width="50%" /></td>
</tr>
<tr>
<td style="text-align: center;">Figura 6. Tela do Editor Joe.</td>
</tr>
</tbody>
</table>

# Concedendo permissões ao arquivo

Para editar o arquivo, precisamos dar permissão de escrita a ele.

Para a primeira alternativa, em que o vi abriu direto o arquivo, precisamos pressionar ESC para editá-lo, assim, ao se fazer isso, o caractere : aparece, então digite 

	!chmod777%

Para a segunda alternativa, em que o touch não abriu o arquivo criado, basta digitar: 
	
	chmod 777 exemplo1.sh.

O chmod é utilizado para setar permissões em arquivos e diretórios. O valor 777 concede todos os direitos (read, write, execute) para o usuário, o grupo e os outros. Ao invés de 777, outro modo de fazer isso é digitando +rwx.

O caractere ! força o vi a executar o que está sendo pedido (no caso, executar o chmod). 
O caractere % faz referência ao arquivo atual. Pode-se também, ao invés de utilizá-lo, fornecer o nome do arquivo.

# Edição e execução do arquivo

Utilizaremos o vi, no terminal, mas você pode escolher qualquer outro editor, gráfico ou não.

Abra o arquivo com o comando vi exemplo1.sh, com o vi você precisa digitar i para colocá-lo no modo de inserção.

Um shell script começa (mas não necessariamente) definindo qual o interpretador de comandos que será utilizado para interpretar e executar o script. Existem outros além do bash, como o sh, o ksh e o csh. 

	#!/bin/SHELL_ATUAL


<table border="0">
<tbody>
<tr>
<td><img style="display: block; margin-left: auto; margin-right: auto;" src="/img/bash.png" width="50%" /></td>
</tr>
<tr>
<td style="text-align: center;">Figura 7. Execução do código bash.</td>
</tr>
</tbody>
</table>

Como vemos na Figura 7, a primeira linha de um shell script define qual o interpretador de comandos será utilizado.

Note que utilizamos o path completo de onde se encontra o shell, no caso, no diretório /bin/.

Após isso, é hora de iniciarmos o nosso script. O exemplo imprimirá na tela algumas informações sobre o usuário e o computador, conforme o código da Listagem 1.

	#!/bin/bash
	echo "Seu nome de usuário é:"
	whoami
	echo "Info de hora atual e tempo que o computador está ligado:"
	uptime
	echo "O script está executando do diretório:"
	pwd 

Listagem 1. Código do exemplo1.sh

Este código nos fornece algumas informações sobre o usuário, algumas informações da máquina e sobre o local de armazenamento do nosso script.

Para salvarmos o arquivo digitamos ESC e depois “:wq” para gravar as alterações e sair.

Para executar o script, há alguns pontos a considerar:

* Se você tiver salvo o seu arquivo no diretório atual, basta executá-lo digitando no prompt: ./exemplo1.sh
* Se você tiver salvo o seu arquivo em outro diretório qualquer, você precisará informar o path completo até ele. Considerando que ele esteja em /tmp/scripts: /tmp/scripts/exemplo1.sh
* O comando echo exibe na tela a string entre aspas duplas. Caso você não queira que ela fique entre aspas duplas, simplesmente não as forneça no comando echo; 
* O comando whoami exibe o usuário logado no sistema;
* O comando uptime exibe a hora atual, o tempo decorrido desde que o computador foi ligado, o número de usuários logados e uma média do número de processos carregados nos últimos um, cinco e 15 minutos;
* O comando pwd exibe o diretório no qual o arquivo está rodando.
* Toda string que contiver espaços deve estar entre aspas duplas.

# Inserindo comentários

Comentários em códigos são muito importantes. Explicar o que está sendo feito e dar informações sobre o funcionamento do código permite ao desenvolvedor economizar tempo para entendê-lo. 

Para inserir comentários no seu script, basta iniciar a linha com o caractere #, como no código da Listagem 2 e execução na Figura 8.

	#!/bin/bash
	#Este é um comentário
	#Este é outro comentário
 	echo "Este script contém comentários."

Listagem 2. Shell script com comentários


<table border="0">
<tbody>
<tr>
<td><img style="display: block; margin-left: auto; margin-right: auto;" src="/img/listagem2.jpg" width="50%" /></td>
</tr>
<tr>
<td style="text-align: center;">Figura 8. Saída da execução do código da Listagem 2.</td>
</tr>
</tbody>
</table>

Como pode ser observado, os comentários não são processados, portanto, não aparecem para o usuário.

# Declarando e utilizando variáveis

Uma variável é um label (nome) que armazena um valor para ser utilizado posteriormente no código. Seu uso evita repetições de valores por parte do programador e torna o código mais informativo e limpo. 

A linguagem do shell não é tipada, ou seja, pode-se armazenar qualquer tipo de valor em uma variável, desde strings a números.

Para declará-las basta seguir a sintaxe nome_da_variavel=valor onde:
	* nome_da_variavel: sequência de caracteres que deve começar por qualquer letra maiúscula ou minúscula ou underscore (_);
	* valor: qualquer dado que deva ser valorado à variável.

Nota: Observe que não deve haver espaços entre o sinal de igual e o nome e o valor da variável.

Para utilizarmos o valor da variável coloca-se o $ (cifrão) na frente de seu nome, como mostra o exemplo da Listagem 3.

	#!/bin/bash
	site=www.devmedia.com.br
	meu_numero_favorito=22
	_cidade=”Belo Horizonte”
	echo “Um ótimo site para você aprender a programar e se manter atualizado é: $site”
	echo “Meu número favorito é: $meu_numero_favorito”
	echo “Minha cidade natal é: $_cidade”

Listagem 3. Declarando e utilizando variáveis

Agora, se você deseja printar o nome da própria variável, basta colocar uma barra invertida \ antes do $, assim, ela nega o caractere seguinte e normalmente é utilizada para caracteres de scape (ou seja, caracteres que já tem uma função específica, mas que você deseja somente utilizar em um nome ou valor, sem executá-los). 
Vejamos um exemplo na Listagem 4.

	#!/bin/bash
	nome=fernanda
	echo “O nome da variável é \$nome”

Listagem 4. Printando o nome de uma variável ao invés de seu conteúdo

# Atribuindo saídas de comandos a variáveis

É possível armazenar o resultado de um comando em uma variável. Isso é muito útil em situações em que se usará este resultado em mais de um lugar ao longo do script.
Há duas sintaxes para isso:

	* nome_da_variavel=$(comando)
	* nome_da_variavel=`comando`

Você pode escolher a que melhor lhe agrada ou empregar as duas nos seus scripts.

O próximo exemplo lista as informações relativas a todos os discos e partições do sistema:

	#!/bin/bash
	system_info=`df -h` # Também poderia ser system_info=$(df -h)
	echo “$system_info”

Veja que o comando df-h executará e a sua saída (resultado dessa execução) será armazenada na variável system_info.

# Capturando a entrada de dados do usuário

Pode ser que o seu script precise interagir com o usuário, pedindo para ele fornecer algum dado de entrada para processamento. Neste caso, é necessário que se leia o que o usuário digitou e isso é feito através do seguinte comando readnome_da_variavel_para_armazenar_o_valor_a_ser_lido
Vejamos o exemplo da Listagem 5.

	#!/bin/bash
	echo “Qual o nome de uma de suas músicas favoritas?”
	read nome_musica;
	echo “Você gosta de ouvir $nome_musica!”

Listagem 5. Utilizando o comando read para ler entrada do usuário

# Comandos de seleção ou de tomada de decisão

## O comando if

Na maioria das vezes precisamos seguir um determinado fluxo de execução baseado em alguma decisão tomada pelo usuário ou outro sistema que esteja utilizando o nosso. O comando mais simples que permite isso é o condicional, que tem a seguinte sintaxe:

	if [ CONDICAO ];
	then
	  AÇÕES
	Fi

Listagem 1. NOME

Onde: 

* CONDICAO: teste que, se verdadeiro, passará o controle para o bloco dentro do then;
* AÇÕES: comandos a serem executados se o resultado de CONDICAO for verdadeiro.

Nota: É muito comum o desenvolvedor esquecer de fechar o if. Lembre-se sempre que, para cada if aberto, você precisa fechá-lo com o fi.
Nota: Lembre-se que, se utilizar o [, você deve fechá-lo com o ], e deixando sempre espaços ao redor. Isso é muito importante, pois eles são um “atalho” para o comando 'test'. Isso significa que, alternativamente, você poderia querer não utilizar os colchetes: 

	if test CONDICAO;
	then
	     AÇÕES
	Fi

Mas normalmente se utiliza os colchetes por ser mais compacto e para ficar mais semelhante ao formato em outras linguagens. De qualquer forma, a escolha é sua.
Nota: Em outras linguagens de programação o if testa uma condição, mas em shell script o if testa a saída de um comando.

Vamos a um exemplo em que o usuário deverá digitar um número e verificaremos se ele está em um determinado intervalo, como mostra a Listagem 6. 

	#!/bin/bash
	echo “Digite um número qualquer:”
	read numero;
	if [ “$numero” -gt 20 ];
	then
	  echo “Este número é maior que 20!”
	fi

Listagem 6. Utilizando o condicional if...then

Veja a seguir os parâmetros mais comuns utilizados com o comando test:

* n string1: o comprimento de string1 é diferente de 0;
* z string1: o comprimento de string1 é zero; 
  * string1 = string2: string1 e string2 são idênticas; 
  * string1 != string2: string1 e string2 são diferentes; 
  * inteiro1 -eq inteiro2: inteiro1 possui o mesmo valor que inteiro2; 
  * inteiro1 -ne inteiro2: inteiro1 não possui o mesmo valor que inteiro2; 
  * inteiro1 -gt inteiro2: inteiro1 é maior que inteiro2; 
  * inteiro1 -ge inteiro2: inteiro1 é maior ou igual a inteiro2; 
  * inteiro1 -lt inteiro2: inteiro1 é menor que inteiro2; 
  * inteiro1 -le inteiro2: inteiro1 é menor ou igual a inteiro2; 
* e nome_do_arquivo: verifica se nome_do_arquivo existe;
* d nome_do_arquivo: verifica se nome_do_arquivo é um diretório;
* f nome_do_arquivo: verifica se nome_do_arquivo é um arquivo regular (texto, imagem, programa, docs, planilhas).

# O comando else

Existe a possibilidade de também tratar o caso em que o nosso teste falha. Para isso temos o comando else, cuja sintaxe é:

	if [ CONDICAO ];
	   then
	       AÇÕES_1
	  else
	      AÇÕES_2
	fi

Onde:

* CONDICAO: teste que, se verdadeiro, passará o controle para o bloco dentro do then;
* AÇÕES_1: comandos a serem executados se o resultado de CONDICAO for verdadeiro;
* AÇÕES_2: comandos a serem executados se o resultado de CONDICAO for falso.

Vejamos um exemplo na Listagem 7 que verifica se um número digitado pelo usuário é positivo ou negativo.

	#!/bin/bash
	  echo “Digite um número qualquer:”
	  read numero;
	  if [ “$numero” -ge 0 ];
   	then
   	 echo “O número $numero é positivo!”
  	else
 	  echo “O número $numero é negativo!”
	fi

Listagem 7. Utilizando o condicional if...then...else

# O comando elif

Há casos em que temos mais de uma condição a ser testada, todas correlacionadas. Para isso temos o comando elif, cuja sintaxe é:

	if [ CONDICAO_1 ];
	 then
	  AÇÕES_1
	 elif [ CONDICAO_2 ];
	 then
	   AÇÕES_2
	 elif [ CONDICAO_3 ];
	 then
	   AÇÕES_3
   	           .
   	           .
   	           .
   	           .
	 elif [ CONDICAO_N ];
 	then
 	 AÇÕES_N
	Fi

Onde:

* CONDICAO_1 … CONDICAO_N: teste que, se verdadeiro, passará o controle para o bloco dentro do respectivo then;
* AÇÕES_1 … AÇÕES_N: comandos a serem executados se os resultados de CONDICAO_1 … CONDICAO_N forem verdadeiros.

A seguir temos um exemplo que apresenta um menu para o usuário escolher uma opção. Baseado nesta escolha, a hora e a data serão exibidas; uma divisão será efetuada e seu resultado será exibido, e uma mensagem será exibida com o nome que o usuário fornecer, como mostra a Listagem 8.

	#!/bin/bash
	echo "Selecione uma opção:"
	echo "1 - Exibir data e hora do sistema"
	echo "2 - Exibir o resultado da divisão 10/2"
	echo "3 - Exibir uma mensagem”
	read opcao;
	if [ $opcao == "1" ];
	then
	  data=$(date +"%T, %d/%m/%y, %A")
 	 echo "$data"
	elif [ $opcao == "2" ];
	then
	   result=$((10/2))
	   echo "divisao de 10/2 = $result"
	elif [ $opcao == "3" ];
	 then
	 echo "Informe o seu nome:"
	 read nome;
	 echo "Bem-vindo ao mundo do shell script, $nome!"
	fi

Listagem 8. Utilizando o comando elif

Nota: O bash não tem suporte nativo a divisões em ponto flutuante, apenas divisões inteiras. Caso queira efetuar este tipo de operação, precisará de um comando externo, como dc ou bc

Nota: Observe a linha: result=$((10/2))
Veja que utilizamos dois conjuntos de parênteses para encapsular a operação de divisão. Em shell script precisamos realizar operações matemáticas entre parênteses.

# O comando case

O comando case tem a mesma funcionalidade do if...then...elif, com a diferença de sua sintaxe ser mais compacta e enxuta:

	case VARIAVEL in
  	CASO_1)
      	   AÇÕES_1
 	 ;;
 	 CASO_2)
  	   AÇÕES_2
 	 ;;
  	 CASO_N)
  	   AÇÕES_N
	 ;;
	esac
	
Onde:

* VARIAVEL: variável que terá seu valor verificado;
* CASO_1 … CASO_N: possíveis estados da variável;
* AÇÕES_1 … AÇÕES_N: ações a serem tomadas caso a variável combine com CASO_1 … CASO_N, respectivamente.

Por exemplo, modificando o exemplo anterior temos o código da Listagem 9.

	#!/bin/bash
	  echo "Selecione uma opção:"
	  echo "1 - Exibir data e hora do sistema"
	  echo "2 - Exibir o resultado da divisão 10/2"
	  echo "3 - Exibir uma mensagem”
	 read opcao;
 	 case $opcao in
 	  “1”)
 	     data=$(date +"%T, %d/%m/%y, %A")
	      echo "$data"
	      ;;
	   “2”)
	     result=$((10/2))
	     echo "divisao de 10/2 = $result"
 	  ;;
 	   “3”)
	    echo "Informe o seu nome:"
	    read nome;
 	   echo "Bem-vindo ao mundo do shell script, $nome!"
	  ;;
	Esac

Listagem 9. Utilizando o comando case

# LOOPS Condicionais

Loops são muito úteis para ficar iterando sobre determinadas ações até que uma condição seja satisfeita e interrompa o laço.
O primeiro deles é o for, cuja sintaxe é:

	for VARIAVEL in VALOR_1, VALOR_2 … VALOR_N;
	  do
	       AÇÕES
	  done

Onde:

* VARIAVEL: variável cujo valor será inicializado e incrementado, respeitando os limites dos valores do conjunto fornecido;
* VALOR_1, VALOR_2 … VALOR_N: valores que VARIAVEL poderá assumir durante o loop;
* AÇÕES: ações a serem tomadas repetidamente até que o valor de VARIAVEL ultrapasse o último valor informado no conjunto de valores fornecido.

Nota: A sequência VALOR_1, VALOR_2 … VALOR_N; na sintaxe pode ser substituída por: {VALOR_1..VALOR_N};

Observe que são apenas duas reticências.

Quando o loop for começar, a variável é inicializada com o primeiro valor do conjunto, e ocorre a primeira iteração (entrada no laço e execução dos comandos). Para as iterações seguintes, os valores do conjunto serão atribuídos à variável, sucessivamente, até que se alcance o último e o loop termine a execução.
Veja o exemplo da Listagem 10, que conta decrescendo de 10 a 0.

	#!/bin/bash
	 echo “Testando o loop for”
	 for i in {10..0};
 	 do
 	  echo “$i”
	 done

Listagem 10. Exemplo de uso do loop for

Outra forma de criarmos sequências de valores é com o comando seq, como mostra a Listagem 11.

	#!/bin/bash
	 echo “Testando o comando seq”
	 for i in $(seq 1 5 100);
	 do
	  echo “$i”
	done

Listagem 11. Exemplo de uso do loop for com o comando seq com intervalo

Observe que foi criada uma sequência de 1 até 100, com intervalo de 5.

Agora, na Listagem 12 temos um exemplo de loop sem intervalo.

	#!/bin/bash
	 echo “Testando o comando seq”
	 for i in $(seq 1 100);
	 do
	  echo “$i”
	done

Listagem 12. Exemplo de uso do loop for com o comando seq sem intervalo

Observe que foi criada uma sequência de 1 até 100, de 1 em 1.

# Loop while

Enquanto o loop for é mais ideal para quando sabemos até quanto contar, o loop while é bom para quando não temos essa noção, mas sabemos de uma condição que deverá ser atendida para que o laço termine. Sua sintaxe é:

	while [ CONDICAO ];
 	    do
 	       AÇÕES
	  done

Onde:

* CONDICAO: condição cuja veracidade determina a permanência no laço;
* AÇÕES: ações a serem tomadas enquanto CONDICAO for verdadeira.

Vamos na Listagem 13 um exemplo que exibe ao usuário o que ele digitou, enquanto ele não informar -1.

	#!/bin/bash
 	 echo “Informe o que você quiser, -1 para sair”
 	 read dado;
 	 while [ $dado != “-1” ];
 	 do
	    echo “Você digitou $dado”
	  read dado;
	done

Listagem 13. Exemplo de uso do loop while

Vejamos um outro exemplo com contador na Listagem 14.

	#!/bin/bash
	echo “Informe até que valor positivo e maior que zero contar:”
	read valor;
	i=1
	while [ $i -le $valor ];
 	do
	  echo “$i”
 	 ((i=$i+1))
	done

Listagem 14. Exemplo de uso do loop while com contador

# Operadores Aritméticos em Shell Script

O shell possui os principais operadores utilizados em linguagem de programação semelhantes ao shell como C, Perl, Php com exceção dos operadores de incremento (++ e – -). Abaixo seguem os operadores aritméticos, comparação, lógicos e bit-a-bit usados pelo shell para a criação de variáveis, operações aritméticas, comparações e teste lógicos.
Operadores aritméticos

*img operadores_aritiméticos.png

Para usar o operador de multiplicação, é necessário usar uma barra invertida antes do sinal de multiplicação \*, usando o comando de expressão aritméticas expr ou a expansão aritimética $( ( expressão ) ).
Exemplos:

	echo `expr 3 + 2`
	echo $( (3+2) )
	echo `expr 3 + 2 \* 3`
	echo $( (3+2*3) )
	echo `expr $( (3 +2) ) \* 3`
	echo $( (3+2*3) )

	echo `expr 3 % 2`
	echo $((3 % 2))

	VL=5
	echo $(($VL**2))

# Operadores Relacionais em Shell Script



# Operadores Lógicos em Shell Script

Uma condição lógica é criada, quando dois ou mais condicionados produzem um único resultado baseado neles. Aqui um resultado de condição também pode inverter o resultado de outra condição.

As operações lógicas OR & AND são muito úteis quando várias condições são usadas em nossos scripts.

	* OR é usado entre duas ou várias condições. Retorna verdadeiro se qualquer uma das condições retornar como verdadeiro. A primeira condição é sempre verificada, mas a segunda condição é verificada apenas se a primeira condição for retornada como false
    
	* AND é usado entre duas ou várias condições. Ele retorna true somente se todas as condições retornarem como true. A primeira condição é sempre verificada, mas a segunda condição é verificada apenas se a primeira condição for retornada como verdadeira

* Usando OR lógico (||) em scripts de shell

O OR lógico no script bash é usado com o operador -o. Segue um pequeno script de shell que mostrará como usar o operador lógico OR (||) entre duas condições.

	#!/bin/bash
	
	# Um shell script que solicita dois números
	# Verifica se o primeiro número é menor que 10 e o segundo é maior que 20
	
	read -p "Entre o Primeiro número: " first
	read -p "Entre o Segundo número: " second
	if [ $first -le 10 ] || [ $second -gt 20 ]
	  then
    		echo "Apenas uma condição é verdadeira"
	  else
    		echo "Ambas condições são falsas"
	fi
* Usando o AND lógico (&&) em scripts de shell

O AND lógico no script bash é usado com o operador -a. Abaixo, o script de shell mostrará como usar o AND lógico ( && ) entre duas condições.

	#!/bin/bash
 
	# Um shell script que solicita dois número
	# Verifica se o primeiro número é menor que 10 e o segundo é maior que 20

	read -p "Entre o Primeiro número: " first
	read -p "Entre o Segundo número: " second
         
	if [ $first -le 10 ]  && [ $second -gt 20 ]
	   then
    		echo "As duas condições são verdadeiras"
	   else
    		echo "Ao menos uma condição é falsa"
	fi

* Usando múltiplos OR & AND lógicos

Agora, use os vários operadores lógicos em uma única instrução. O exemplo abaixo o ajudará a entender como usar vários operadores lógicos em uma única instrução.

	#!/bin/bash
 
	# Um Script que solicita um número
	# Verifica se o número está entre 10 - 20 ou se o número está entre 100 - 200
 
	read -p "Entre um número: " num
 
	if ([ $num -ge 10 ] && [ $num -le 20 ]) || ([ $num -ge 100 ] && [ $num -le 200 ])
	   then
		echo "O número ($num) está entre 10-20 ou 100-200"
	   else
	   	echo "O número ($num) não está entre 10-20 nem entre 100-200"
	fi

# Funções

O uso de funções é imprescindível para separar, organizar e estruturar a lógica de qualquer algoritmo, seja em shell script ou qualquer outra linguagem de programação. Sua sintaxe é muito simples:

	nome_funcao()
	  {
	      AÇÕES
	   }

Funções podem chamar outras funções existentes no script, simplesmente escrevendo-se o nome dela, como vemos no exemplo da Listagem 15.

	#!/bin/bash	
	 main()
	 {
	   echo "Escolha uma opção:"
	   echo "1 - Esvaziar a lixeira"
	   echo "2 - Calcular fatorial"
	   read opcao;
	   case $opcao in
	   "1")
	    esvaziar_lixeira
	    ;;
	   "2")
	    calcular_fatorial	
	    ;;
	 esac
	}
	esvaziar_lixeira()
	{
	  echo "Esvaziando a lixeira..."
	  path="${HOME}/.local/share/Trash/files"
	  cd "$path"
	  for file in *
 	 do
	  rm -rf "$file"
	  done
 	 echo "Done!"
	}
	calcular_fatorial()
	{
	  echo "Informe um número:"
	  read numero;
	  i=1
	  fat=1
	  while [ $i -le $numero ]
	  do
	  fat=$(($fat*$i))
	  i=$(($i+1))
	  done
	  echo "fatorial de $numero é $fat"
	}
	main

Listagem 15. Exemplo de uso de funções

Nota: Lembre-se sempre de chamar a função principal (no nosso caso, main) no final do seu script, do contrário, nada acontecerá quando você o executar.
Argumentos

Normalmente um programa recebe argumentos como entrada, ou seja, dados fornecidos pelo usuário ou por outro programa, os quais devem ser “consumidos” para produzir as saídas desejadas.
Em shell script não poderia ser diferente: temos nomes especiais para designar os argumentos recebidos por um script:

* $0 – contém o nome do script que foi executado;
* $1 … $n – contêm os argumentos na ordem em que foram passados (1º argumento em $1, 2º argumento em $2, etc.).
* $# - contém o número de argumentos que foi passado (ou seja, não considera o nome do script em $0);
* $* - retorna todos os argumentos de uma vez só.

Vamos ao exemplo da Listagem 16 e sua execução é exibida na Figura 9.

	#!/bin/bash
 	 if [ $# -lt 1 ];
	  then
	   echo "Precisa fornecer pelo menos 1 argumento!"
	   exit 1
	 fi
	 echo "Número de argumentos passados: $#"
	i=0
	for argumento in $*
	 do
	 i=$(($i+1))
	  echo "Argumento $i passado: $argumento"
	 done

Listagem 16. Exemplo de uso de argumentos em scripts

<table border="0">
<tbody>
<tr>
<td><img style="display: block; margin-left: auto; margin-right: auto;" src="/img/listagem16.jpg" alt="" width="50%" /></td>
</tr>
<tr>
<td style="text-align: center;">Figura 9. Sa&iacute;da da execu&ccedil;&atilde;o do c&oacute;digo da Listagem 16</td>
</tr>
</tbody>
</table>

# Gerenciando a execução de um script

* Executando um Script Bash

Existem várias maneiras de executar um script Bash. Alguns deles são dados a seguir:

* Usando bash ou sh.
* Usando a fonte.
* Executando diretamente em um ambiente bash.
    
Para fazer alguns desses métodos funcionarem, o script deve ter um shebang como cabeçalho para indicar que é um script de shell ou script bash neste caso. Portanto, certifique-se de incluir o comando abaixo na parte superior do arquivo.

	#!/bin/bash

Este comando fará o script rodar sob o interpretador bash. Recomenda-se escrever o cabeçalho shebang mesmo que funcione sem eles.

* Usando bash ou sh

Esta é a maneira mais padrão de executar o script bash. Para Linux e macOS, o bash é instalado por padrão. Neste método, digitamos bash seguido do nome do arquivo com extensão, ou seja, sh neste caso. Em um terminal, execute o seguinte código substituindo o nome do arquivo pelo nome do arquivo do seu script bash.

	bash filename.sh

Também podemos usar sh para executar o script, pois ele direcionará para o shell padrão no ambiente de configuração. 

	sh filename.sh
	
Se você não estiver na mesma pasta / diretório que o script, certifique-se de especificar o caminho relativo para o script.

* Usando a fonte

Este método é bastante fácil de executar um script bash, e todos eles são bastante simples. Precisamos apenas digitar “source” antes do nome do arquivo / script com uma extensão. Em um terminal, execute o seguinte código substituindo o nome do arquivo pelo nome do arquivo do seu script bash.

	source filename.sh
	
* Especificando o caminho para o script e chmod

Este é um método independente para executar um script bash. Temos que executar o script como um executável, podemos executar o script em qualquer lugar, desde que tenhamos um shell bash em algum lugar do ambiente. Para torná-lo executável, precisamos ter certeza de que temos os direitos para executar o arquivo como um executável. Usaremos chmod para alterar os direitos no arquivo / script. Em um terminal, execute o seguinte código substituindo o nome do arquivo pelo nome do arquivo do seu script bash.

	chmod +x filename.sh  

O comando acima nos permitirá executar o arquivo. Portanto, ele muda o modo do arquivo, o arquivo deve ser somente leitura, executável ou qualquer outro modo para arquivos. Se você estiver usando Linux e não for o usuário root, simplesmente use sudo antes do comando chmod. O comando + x garantirá que o arquivo seja executável por todos no ambiente.

Depois de verificar a permissão do arquivo, podemos simplesmente executar o arquivo da seguinte maneira. O comando abaixo leva em consideração que você está no mesmo diretório que o arquivo / script bash.

	./filename.sh
	
* Executando um script em background

Os processos podem ser executados de duas formas: em foreground (primeiro plano) ou background (segundo plano). Os processos executado em foreground são aqueles que necessitam de interação direta com o usuário, incluindo troca de informações. Os processo em background não necessitam desta interação com o usuário.

* Enviando um comando para segundo plano

Existem várias maneiras para enviar um comando para segundo plano, porém, a mais simples é colocando um & (E comercial) ao final do comando. Por exemplo:

	root@orangepione:/home/aluno# ./pisca.sh &
	[1] 1287

Perceba também que existe um sinal de – ou + na frente do número do processo, isso simplesmente indica que o processo com sinal de + foi iniciado por último e ele será trazido para o primeiro plano caso você digite apenas “fg”. O processo com um sinal de menos apenas indica que ele foi iniciado antes do processo com sinal de +. Se você iniciar mais tarefas, a próxima terá um sinal de +, a que estava com sinal de + ficará com um sinal de – e a primeira tarefa iniciada não terá nenhum sinal.

Se você quiser trazer uma tarefa para primeiro plano, digite fg %N (onde N é o número do processo que deseja). Você pode parar temporariamente a aplicação pressionando as teclas “CTRL” + “Z” do seu teclado. E o shell está livre para que eu possa digitar novamente. Verifique que se você digitar “jobs” novamente, verá que a tarefa não está executando. Utilize o comando “bg” para continuar executando a tarefa em segundo plano. Veja:

	root@orangepione:/home/aluno# 
	root@orangepione:/home/aluno# ./pisca.sh &
	[1] 1287
	root@orangepione:/home/aluno# fg
	./pisca.sh
	^Z
	[1]+  Stopped                 ./pisca.sh
	root@orangepione:/home/aluno# 
	root@orangepione:/home/aluno# bg
        [1]+ ./pisca.sh &

* Listando os processos em execução - Comando "ps" 

	root@orangepione:/home/aluno# ps
  	PID TTY          TIME CMD
 	1215 pts/0    00:00:00 bash
 	1287 pts/0    00:00:00 testa.sh
 	1497 pts/0    00:00:00 sleep
 	1498 pts/0    00:00:00 ps
	root@orangepione:/home/aluno# 

        root@orangepione:/home/aluno# ps aux|grep testa.sh
        root      1287  0.0  0.1   3720   672 pts/0    S+   09:28   0:00 grep --color=auto testa.sh
        root@orangepione:/home/aluno# 
	
* Encerrando um processo

Dentro do Linux, as tarefas são chamadas de processos, e cada um deles possui um número de identificação (ID) único. Para encerrar (matar) um processo utilizamos o comando kill. Para encerramos um processo é necessário apenas digitar Kill PID onde PID é o numero do processo. o Parametro -9 força sua inte

	root@orangepione:/home/aluno# ./pisca.sh
	^Z
	[1]+  Stopped                 ./pisca.sh
	root@orangepione:/home/aluno# ps 
	  PID TTY          TIME CMD
 	1582 pts/0    00:00:00 bash
	 1871 pts/0    00:00:00 pisca.sh
 	1897 pts/0    00:00:00 sleep
 	1898 pts/0    00:00:00 ps
	root@orangepione:/home/aluno# kill -9 1871
	root@orangepione:/home/aluno# ps
 	 PID TTY          TIME CMD
	 1582 pts/0    00:00:00 bash
	 1910 pts/0    00:00:00 ps
	[1]+  Killed                  ./pisca.sh
	root@orangepione:/home/aluno#


Shell scripts são a melhor maneira de automatizar tarefas diárias em sistemas Linux/Unix-like. Além de práticos, nos poupam muito tempo, além de possuírem uma sintaxe simples e permitir processar desde pequenas quantidades de dados até executar tarefas mais robustas.

# Lendo um pino de IO por interrupção no Linux

O acesso a pinos de I/O (GPIO) no Linux é feito através de arquivos exportados no diretório /sys/class/gpio/. Para acessar um pino de I/O, o primeiro passo é exportá-lo escrevendo o número do pino de I/O no arquivo export. Depois é necessário configurar a direção do pino de I/O no arquivo direction e por fim ler ou alterar o estado do pino de I/O no arquivo value.

Por exemplo, para acionar o GPIO 53:

	# echo 53 > /sys/class/gpio/export		
	# echo out > /sys/class/gpio/gpio53/direction
	# echo 1 > /sys/class/gpio/gpio53/value


* Exemplo básico da utilização de shell script no OrangePi

Pisca_led - Fica alternando o nível logico do pino PA12 a cada 1 segundo
Botao - Ao ser pressionado o botão (PA11) o led (PA06) desliga. A leitura do valor de entrada do pino PA11 é realizada por Poll, num intervalo de 500 ms, evitando assim que seja consumido 100% do processador.

No primeiro exemplo, temos o pino PA12 configurado como saída e nele temos um led vermelho conectado para ilustrar melhor o funcionamento do script.


<table border="0">
<tbody>
<tr>
<td><img style="display: block; margin-left: auto; margin-right: auto;" src="/img/gpio_orangepione.png" alt="" width="50%" /></td>
</tr>
<tr>
<td style="text-align: center;">Figura 10: Distribuição das GPIOs na barra de pinos da Orange Pi One.</td>
</tr>
</tbody>
</table>

Um detalhe importante, que merece ser ressaltado, é o funcionamento do export das GPIO. Como não temos um mapeamento interno no kernel delas, o export deve ser realizado como base no port e pino. Eis que, desta forma, teremos uma conta que deve ser realizada para descobrirmos o valor correto da GPIO.
 
xx corresponde à conta abaixo:
(Posição da letra no alfabeto – 1) * 32 + número do pino

	Ex: PA12
	( 1 – 1 ) * 32 + 12 = (0 * 32) + 12 = 12
 
	Ex: PD14
	( 4 – 1 ) * 32 + 12 = 3 * 32 + 14 = 110
 
Outro detalhe que precisamos prestar atenção é na corrente máxima de saída que o pino consegue fornecer. Neste caso, o datasheet nos informa que a corrente máxima é de 40 mA, página 607 Allwinner H3. Neste caso, foi utilizado um resistor de 330 Ohms em série com o Led, a fim de limitar sua corrente em 10 mA.

No segundo exemplo, teremos o pino PA06 configurado como saída e o PA11 como entrada. O funcionamento do código consiste em verificar via Poll se o botão (PA11) foi pressionado, e caso seja, o Led amarelo (PA06) será apagado.

No código do exemplo 2, é necessário realizar duas ressalvas: a primeira é que no caso do pino de entrada (PA11) foi adicionado um resistor de pull-up externamente, com a finalidade de limitar a corrente de entrada.

A segunda, consiste no aspecto que a adição do comando sleep 0.5, que nos traz um atraso de, aproximadamente, 500 ms na leitura do pino. Entretanto, caso não seja inserido, o processador terá seu uso em 100%. Isso porque o código estando num loop infinito, as operações descritas no script serão realizas de forma ininterrupta, ocasionando o uso excessivo do processador. 

Destaca-se que outra maneira de executar esse código será a análise da troca de estado do pino por interrupção. Nesse caso, não teríamos atraso na leitura e nem usaríamos em excesso o processador.

	#!/bin/sh
	# Inicializa a gpio12 (PA12) - (1 - 1)*32 + 12 = 12
	echo 12 > /sys/class/gpio/export
	# Declara a gpio12 como saida
	echo "out" > /sys/class/gpio/gpio12/direction
	# Inicializa a saida com nivel logico 0 (led desligado)
	echo 0 > /sys/class/gpio/gpio12/value
	trap "echo 12 > /sys/class/gpio/unexport; exit 0" 1 2 15
	# 1 - SIGUP
	# 2 - SIGINT
	# 3 - SIGTERM
	#loop infinito
	while true
	do
	#Liga o led (gpio12)
	echo 1 > /sys/class/gpio/gpio12/value
	#Aguarda 1 segundo
	sleep 1
	#Desliga o led
	echo 0 > /sys/class/gpio/gpio12/value
		sleep 1
	done

Listagem 17. Exemplo em script pisca_led.sh

* Acrescentado comando trtrap para remover a exportação dos pinos

	#!/bin/sh
	echo 11 > /sys/class/gpio/export
	echo in > /sys/class/gpio/gpio11/direction
	echo 6 > /sys/class/gpio/export
	echo out > /sys/class/gpio/gpio6/direction
	echo 0 > /sys/class/gpio/gpio6/value
	trap "echo 11 > /sys/class/gpio/unexport; echo 6 > /sys/class/gpio/unexport; exit 0" 1 2 15
	#1 - HANGUP
	#2 - INTERRUPT
	#15 - TERMINATE
	while true
	do
		botao=$( cat /sys/class/gpio/gpio11/value)
		if [ "$botao" -eq 1 ];
			then
				echo 1 > /sys/class/gpio/gpio6/value
			else
				echo 0 > /sys/class/gpio/gpio6/value
		fi
	sleep 0.5
	done

Listagem 18. Exemplo de uso script botão.sh

# Pull-up

O esquema de ligação padrão para esta configuração é ilustrado pela Figura 11. Quando o botão estiver solto, o Vcc fluirá pelo resistor R1 chegando na porta digital. Quando o botão for pressionado, o Gnd fluirá pelo contato da chave — sem maiores resistências — alcançando o pino do microcontrolador.

Na prática, quando o botão estiver solto, o microcontrolador reconhecerá nível lógico 1, por isso a nomenclatura pull-up (puxar para cima): normalmente para cima/nível lógico High. Todavia, enquanto a chave for pressionada, o microcontrolador reconhecerá nível lógico 0.

<table border="0">
<tbody>
<tr>
<td><img style="display: block; margin-left: auto; margin-right: auto;" src="/img/pull-up.jpg" alt="" width="80%" /></td>
</tr>
<tr>
<td style="text-align: center;">Figura 11: Resistor de Pull-Up.</td>
</tr>
</tbody>
</table>

# Pull-down

A Figura 12 ilustra o esquema de ligação padrão para esta configuração. Quando o botão estiver solto, o Gnd fluirá pelo resistor R1 chegando na porta digital. Quando o botão for pressionado, o Vcc fluirá pelo contato da chave — sem maiores resistências — alcançando o pino do microcontrolador. 

Na prática, quando o botão estiver solto, o microcontrolador reconhecerá nível lógico 0 (Gnd), por essa razão a nomenclatura pull-down (puxar para baixo): normalmente para baixo/nível lógico 0. Contudo, enquanto a chave for pressionada, o microcontrolador identificará nível lógico 1 .

<table border="0">
<tbody>
<tr>
<td><img style="display: block; margin-left: auto; margin-right: auto;" src="/img/Pull-down.jpg" alt="" width="80%" /></td>
</tr>
<tr>
<td style="text-align: center;">Figura 11: Resistor de Pull-down.</td>
</tr>
</tbody>
</table>



# Status do Projeto
![Badge em Desenvolvimento](http://img.shields.io/static/v1?label=STATUS&message=EM%20DESENVOLVIMENTO&color=GREEN&style=for-the-badge)
Atualizado em Julho de 2022

# Bibliografia
- http://www.orangepi.org/html/hardWare/computerAndMicrocontrollers/details/Orange-Pi-One.html
- https://www.devmedia.com.br/introducao-ao-shell-script-no-linux/25778 
- https://embarcados.com.br/orange-pi-one-gpios-shell-script/
- https://sergioprado.org/lendo-um-pino-de-io-por-interrupcao-no-linux/
- https://sergioprado.org/interface-gpio-kernel-linux/
- https://git.kernel.org/pub/scm/linux/kernel/git/linusw/linux-gpio.git/
- https://linux-sunxi.org/GPIO
- https://olimex.wordpress.com/2012/10/23/a13-olinuxino-playing-with-gpios/a
- https://m.youtube.com/watch?v=WCOHCHmrxaA
- https://forum.armbian.com/topic/7067-orange-pi-pc-how-to-use-gpio-for-push-buttons-tutorial/
- https://stackoverflow.com/questions/46463724/accessing-gpio-on-orangepi-pc-plus-h3-on-armbian-3-4-113-and-newer
- https://opi-gpio.readthedocs.io/en/latest/api-documentation.html
- https://www.mhavila.com.br/topicos/unix/shscript.html 
- https://pypi.org/project/OPi.GPIO/
- https://learn.adafruit.com/circuitpython-on-orangepi-linux
- https://www.instructables.com/Orange-Pi-One-Python-GPIO-basic/
- http://www.orangepi.org/orangepibbsen/forum.php?mod=viewthread&tid=4996
- https://www.armbian.com/orange-pi-one/
- https://github.com/armbian/build 
- https://www.dobitaobyte.com.br/varios-modos-de-interagir-com-o-gpio-do-raspberry-pi/
- https://tecadmin.net/use-logical-or-and-in-shell-script/
- https://acervolima.com/como-executar-o-script-bash-no-linux/
- https://gnulinuxbr.wordpress.com/2010/04/07/operadores-shell-script/

