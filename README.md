# Conhecendo e utilizando o terminal

## Comando básicos úteis

- whoami: Revela sua credencial (usuário que esta logado).

```console
user_name@vm1:~$ whoami
user_name
```

- pwd: Revela diretório atual.

```console
user_name@vm1:~$ pwd
/home/user
```
- ls: Releva arquivos do diretório.

```console
user_name@vm1:~$ ls
Desktop Downloads ...
```

- echo: "falar" no console, é possivel redirecionar para um txt usando ">" ou concatenar várias chamadas de echo com ">>".

```console
user_name@vm1:~$ echo "bem vindo">bemvindo.txt
```
```console
user_name@vm1:~$ echo "bem vindo 2">>bemvindo.txt
```

- cat: ler um arquivo txt no terminal.

```console
user_name@vm1:~$ cat bemvindo.txt
bem vindo
bem vindo 2
```

- man: "manual", help de comando, mostra diversos argumentos que podemos utilizar.

```console
user_name@vm1:~$ man ls
```

- cd: _change directory_, usado para navegar entre as pastas, "." significa pasta atual e ".." pasta anterior

```console
user_name@vm1:~$ cd <path>
```

- mkdir: Cria diretório

```console
user_name@vm1:~$ mkdir <dir_name>
```

- rm: remove arquivos ou diretórios (usando -r flag).  `-r` significa _recurssive_.

```console
user_name@vm1:~$ rm <path-or-file> 
```

- locate: Localizar um arquivo

```console
user_name@vm1:~$ locate <file>
```

- which: Revela qual o arquivo executa se chamar algum comando existente.

```console
user_name@vm1:~$ which R
```
- sudo: executar comando como sudo
```console
user_name@vm1:~$ sudo <command>
```
- passwd: Alterar ou criar senha

```console
user_name@vm1:~$ passwd
```
para alterar a senha do usuário root

```console
user_name@vm1:~$ sudo passwd
```

- su: Alterar o usuário

```console
user_name@vm1:~$ su <user>
```

OBSERVAÇÃO: Todos arquvios no _path_ `/usr/bin/` por padrão, é procurado na hora da execução.

## Caracteres coringas no bash

```console
user_name@vm1:~$ echo "bem vindo"> bemvindo.txt
user_name@vm1:~$ echo "teste 1"> file1.txt
user_name@vm1:~$ echo "teste 2"> file2.txt
user_name@vm1:~$ echo "teste 3"> file3.txt
```
- \*: substitui qualquer cadeia caracter.

```console
user_name@vm1:~$ cat file*.txt
teste 1
teste 2
teste 3
```
```console
user_name@vm1:~$ cat *.txt
bem vindo
teste 1
teste 2
teste 3
```
## Manipuland, copiando, movendo e renomeando arquivos

-cp: _copy_, usando em arquvios, caso queria usar em diretórios devemos usar a flag `-r`

```console
user_name@vm1:~$ cp bemvindo.txt <novo-nome.txt>
```
- mv: _move_ 

```console
user_name@vm1:~$ mv <file> <path/new-file-name>
```

OBSERVAÇÃO: não esquecer de colocar a extensão do arquivo corretamente.

## Compactando diretórios (.zip . tar.gz)

-zip: compacta um diretório em zip.

```console
user_name@vm1:~$ zip -r <name>.zip <dir_name>
```
-unzip: Descompacta um arquivo .zip, a flag `-q` significa _quiet_, isto é, não solta nenhuma notificação. 

```console
user_name@vm1:~$ unzip -q <name>.zip
```

- tar: Compacta um diretório,a flag `-c` significa _create_ e `-z` para também zipar e deixar ainda mais compacto. 

```console
user_name@vm1:~$ tar -cz <dir> > <name2>.tar.gz
```
para descompatar, basta usar a flag `-x` de _exctract_ ao invês de `-c`.

```console
user_name@vm1:~$ tar -xz < <name2>.tar.gz
```

podemos substituir o redirecionametos "<" ou ">" usando a flag `-f` (_filename_).

```console
user_name@vm1:~$ tar -czf <name2>.tar.gz <dir>
```
```console
user_name@vm1:~$ tar -xzf <name2>.tar.gz
```
## Edição de arquivos com vi

É possivel usar o terminal para editar arquivos direto do terminal. Como essa função não é muito utilizada no meu caso, veja melhor o help desse comando com

```console
user_name@vm1:~$ man vi
```

# Programas, processos e pacotes

- ps: Revela os processos que estão em execução. A flag `-e` indica para mostrar de toda a máquina. 

```console
user_name@vm1:~$ ps -e
```

- kill: Acaba com a execução de um processo, o <id_process> pode ser visto com o `ps`. A flag `-9` mata sem "pedir para parar". 

```console
user_name@vm1:~$ kill -9 <id_process>
```
- grep: programa filtra linhas segundo um padrão de string. O comando abaixo lista os processos em execução (`-f` para mais informaçoes), o caracter `|` redireciona a saida para outro programa, e grep filtra as linhas que possues "firefox" nelas.

```console
user_name@vm1:~$ ps -ef | grep firefox
```

- top: mostra a situação dos processos(uso de CPU, RAM, ...)

```console
user_name@vm1:~$ top
```

- killall: Funciona como o kill, mas é possivel indicar para acabar com todos processos com um nome em comum. O comando abaixo fecha todas as abas de firefox abertas.

```console
user_name@vm1:~$ killall -9 firefox
```

## Permissoes

Todo arquivo em linux podem ter 3 tipos de permissão `r-w-x` (_read_,_write_,_execute_).

- chmod: dar tipos de permissões para os três possíveis grupos do linux (Dono, grupo de arquivo, outros usuários). Em <grupo\> podemos colocar u (_user_), g(_group of dir_) ou o(_others_);

```console
user_name@vm1:~$ chmod <grupo>+x <file>
```

## Variáveis de ambiente e PATH

- env: Revela as variáveis de ambiente

```console
user_name@vm1:~$ env
```
podemos adicionar mais um endereço na variável de ambiente PATH de maneira, abrindo o arquivo .bashrc (no ubuntu), e adicionando a seguinte linha

```console
PATH=$PATH:<dir>
```

## Instalação de programas

O ubuntu oferece o apt, um sistema de gerenciamento de pacotes.
alguns exemplos são

```console
user_name@vm1:~$ sudo apt-get update
```

```console
user_name@vm1:~$ apt-cache search <package>
```

```console
user_name@vm1:~$ sudo apt-install <package>
```

```console
user_name@vm1:~$ sudo apt-get remove <package>
```

Podemos também instalar pacotes de um repositório não central, isto é, fazendo o download e posteriormente instalando na máquina. Após realizar o download de \<pacote>.deb 

```console
user_name@vm1:~$ dpkg -i <pacote>
```
a flag `-i` significa install, para remover basta substituir a flag para `-r` de remove .

## Acesso remoto com ssh e scp

```console
user_name@vm1:~$ sudo apt-install ssh
```
```console
user_name@vm1:~$ ssh user@<ip>
```
e para copiar um arquivo da máquina local para a máquina remota

```console
user_name@vm1:~$ scp -r <file> user@<ip>:/<path>
```