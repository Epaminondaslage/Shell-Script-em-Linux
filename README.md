# Shell-Script-no-Linux


# Introdução ao Scripts em Shell

Podemos utilizar a criação de arquivos de scripts para tornar mais simples as execuções de tarefas repetitivas no dia a dia. Muito tempo do programador é empregado em ações desse tipo, como abrir os mesmos programas todos os dias; esvaziar a lixeira e diretórios temp para economizar espaço em disco; etc.
Um script nada mais é do que um algoritmo projetado para realizar uma determinada tarefa, utilizando os comandos específicos do bash e os executáveis do sistema operacional.

    Lembre-se de executar os comandos como usuário comum e não como root, visto que, como root tudo será aceito e, dependendo do que você fizer, isto pode gerar danos ao sistema operacional. Uma maneira fácil de verificar é abrir o terminal e se o símbolo antes do cursor é o $, você está como usuário comum, mas se é o #, você está como root. Para sair do modo root, digite exit
    
    Devemos portando criar um usuário para que possamos trabalhar com segurança. O comando "adduser" serve para adicionar um usuário ou um grupo ao sistema, onde será criado um diretório com o nome do usuário, com uma entrada para o usuário no arquivo /etc/passwd (senhas). A utilização do comando adduser necessita do uso do comando sudo (deve estar com previlégio de root).
Além disso, quando é adicionado um novo usuário, é criado, por padrão, um grupo com o nome do mesmo usuário. Caso seja criado um novo grupo, o comando adduser cria uma entrada para o grupo no arquivo /etc/group. 
    

    root@orangepione:/home# adduser epaminondas
    Adding user `epaminondas' ...
    Adding new group `epaminondas' (1001) ...
    Adding new user `epaminondas' (1001) with group `epaminondas' ...
    Creating home directory `/home/epaminondas' ...
    Copying files from `/etc/skel' ...
    Enter new UNIX password: 
    Retype new UNIX password: 
    passwd: password updated successfully
    Changing the user information for epaminondas
    Enter the new value, or press ENTER for the default
	Full Name []: Epaminondas Lage
	Room Number []: 
	Work Phone []: 
	Home Phone []: 
	Other []: 
    Is the information correct? [Y/n] Y
    root@orangepione:/home# 
Portanto pode-se sair da sessão e fazer ssh com o usuário recém criado.

