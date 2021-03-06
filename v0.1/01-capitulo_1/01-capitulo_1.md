
Capítulo 1
==========

O que é o PHP?
--------------

Essa linguagem foi concebida durante o outono de 1994 por Rasmus
Lerdorf. As primeiras versões não foram disponibilizadas, tendo sido
utilizadas em sua home-page apenas para que ele pudesse ter informações
sobre as visitas que estavam sendo feitas. A primeira versão utilizada
por outras pessoas foi disponibilizada em 1995, e ficou conhecida como
“Personal Home Page Tools” (ferramentas para página pessoal). Era
composta por um sistema bastante simples que interpretava algumas macros
e alguns utilitários que rodavam “por trás” das home-pages: um livro de
visitas, um contador e algumas outras coisas.

Diferentemente de algumas linguagens para web, o PHP permite criar sites
web dinâmicos, possibilitando uma interação do usuário com o site,
através de formulários feitos em HTML, parâmetros da URL, links e também
serve para criar aplicações embarcadas, aplicações mobile, de linha de
comando. A diferença entre ela com relação ao JavaScript padrão, por
exemplo, é que o código PHP é executado no servidor, sendo enviado para
o cliente apenas HTML puro e o próprio código JavaScript. Hoje em dia
existe NodeJS rodando JavaScript no servidor. Desta maneira é possível
interagir com bancos de dados e aplicações existentes no servidor, com a
vantagem de não expor o código fonte para o cliente. Outra diferença do
PHP com um script CGI escrito em C ou Perl é que o código PHP fica
embutido no próprio HTML, enquanto no outro caso é necessário que o
script CGI gere todo o código HTML, ou leia de um outro arquivo.

Com o PHP podemos fazer tudo, qualquer coisa feita por algum programa
CGI pode ser feita com PHP, como coletar dados de um formulário, gerar
páginas dinamicamente ou enviar e receber cookies. O PHP também tem como
uma das características mais importantes o suporte a um grande número de
bancos de dados, como dBase, Interbase, Firebird, mSQL, mySQL, Oracle,
Sybase, PostgreSQL e vários outros. Construir uma página baseada em um
banco de dados torna-se uma tarefa extremamente simples com PHP. Além
disso, PHP tem suporte a protocolos como IMAP, SNMP, NNTP, POP3 e,
logicamente, HTTP. Também é possível abrir sockets e interagir com
outros protocolos.

Como funciona o PHP
-------------------

![Esquema de uma requisição a uma página PHP](img/image2.jpg)

Requisitos do Sistema Operacional
---------------------------------

-   **SO:** Linux, Solaris, MAC OS

-   **Servidores web:** Apache 2, Nginx e o Próprio PHP. Pacotes como
    LAMP, XAMP e alguns outros também podem ser utilizados.

-   **Banco de Dados:** mSQL, SQL Server, MySql/MariaDB, Sybase, Oracle,
    PostgreSQL

**Nota:** Pode-se usar o comando php -S 0.0.0.0:8001 -t caminho/do/site

Instalação e configuração do PHP
--------------------------------

Para instalar o PHP é necessário o PHP, Apache, MySQL e phpMyAdmin. Abra
o terminal (CTRL+T) e rode os comandos abaixo para instalar os pacotes.

**Apache:** \~\$ sudo apt-get install apache2

**MySQL:** \~\$ sudo apt-get install mysql-server e sudo apt-get install
php5-mysqlnd

**PHP:** \~\$ sudo apt-get install php5 php5-curl php5-mcrypt php5-mysql
libapache2-mod-php5

**phpMyAdmin:** \~\$ Apache: sudo apt-get install phpMyAdmin

### Testando o Apache

Abra o browser e digite [http://localhost](http://localhost/).

![Figura 2: A imagem indica que o Apache está rodando.](img/image3.jpg)

###  Configurando o Apache

Para podermos criar nossos projetos de uma forma mais fácil e sem
precisar virar root no sistema, vamos cria um diretório em
*/home/seu\_usuario/www.* Todos os seus sites e projetos devem ser
colocados nesse diretório. Finalizando nosso processo, precisamos
modificar o arquivo de configuração do apache apontando para o novo
diretório criado. Abra um terminal (CRTL+T) e rode comando.

\~\$ sudo gedit /etc/apache2/sites-available/000-default.conf

Procure por *DocumentRoot /var/www/html* e comente a linha colocando o
sinal tralha na frente da linha. Adicione *DocumentRoot
/home/seu\_usuario/www/*

### Testando o PHP

Crie um arquivo chamado *info.php.*

```
<?php phpinfo();

```

Salve em */home/seu\_usuario/www/*, no browser digite
[*http://localhost/info.php*](http://localhost/info.php).

**Nota:** É recomendado por questões de segurança que arquivos que sejam
somente PHP, não tenha a tag de fechamento e que contenha a última linha
em branco.

![Figura 3: Essa tela indica que o PHP está rodando perfeitamente](img/image4.jpg)

### \
Testando o phpMyAdmin

Abra o browser e digite
[*http://localhost/phpMyAdmin*](http://localhost/phpmyadmin) e acesse-o
com o login e senha definidos na instalação do MySQL.

###  Configurando PHP

Localizar e modificar o arquivo *php.ini*. Esse arquivo pode estar em
local diferente dependendo da distribuição GNU/Linux que está usando. No
Ubuntu e nas distribuições “Debian like”, esse arquivo encontra-se em
*/etc/php5/apache2/php.ini*. Após as modificações é necessário reiniciar
seu servidor PHP como por exemplo o Apache, para reiniciar o Apache pode
se usar o comando *sudo service apache2 restart*.

Para o ambiente de desenvolvimento é altamente recomendado habilitar as
seguintes diretrizes:

-   error\_reporting = E\_ALL
-   display\_errors = On
-   log\_errors = On
-   track\_errors = On
-   html\_errors = On

As diretrizes acima fazem que quais quer tipo de erro seja exibido,
logado, rastreado e exibido de uma forma mais organizada. Essas
configurações devem ser diferentes no ambiente de produção (onde o site
é de fato hospedado), isso por que os usuários devem receber mensagens
de erros amigáveis, e na tentativa de algum craker ou algum script kid
querer explorar alguma falha no site, o erro não de para ele de bandeja
uma mensagem de erro com o nome e campos de alguma tabela do seu banco
de dados.

**Nota:** Se usar uma distribuição diferente do Ubuntu nada que uma
pesquisada na internet para descobrir o comando certo.

Entendendo o PHP
----------------

### Sintaxe

O código do PHP pode ficar embutido no contexto do HTML, porém em muitos
casos perceberá que esses códigos são bem simples e não contém regras de
negócios ou estruturas muito complexas, ou seja, se limita somente a
exibição de dados, estruturas de laços e condições simples.

Para estruturas complexas e longas usa-se <?php algum código;
?>*, para exibir conteúdo na tela utilizar <?= \$variavel;
?>.

**ATENÇÃO:** Em códigos legados e/ou em código cujo a versão do PHP seja
inferior a 5.4.x ou que não seguem as recomendações de padronização é
comum encontrar a sintaxe sendo usada da seguinte forma:

  ---------------------------------------------------------------------------
  <? comandos ?>              Não recomendado
  --------------------------------- -----------------------------------------
  <script language=“php”>     Não recomendado
  comandos                     
  </script>                   

  <% comandos %>              Não recomendado

  <?php echo \$variavel; ?>   Ainda utilizado, mas não é recomendado.
  ---------------------------------------------------------------------------

É altamente recomendado o não fechamento da tag PHP e deixar uma linha
em branco no fim do arquivo sem espaços[^1]

### Finalização de comando

Entre cada instrução em PHP é preciso utilizar o ponto e vírgula, assim
como em Pascal, C, Perl e outras linguagens mais conhecidas.

### Variáveis

Toda variável em PHP tem seu nome composto pelo caracter \$ e o nome da
variável, que deve iniciar sempre por uma letra ou o caracter “\_”. PHP
é case sensitive, ou seja, as variáveis *\$quantidade* e *\$Quantidade*
são diferentes. Por isso é preciso ter muito cuidado ao definir os nomes
das variáveis. É bom evitar os nomes em maiúsculas, pois como veremos
mais adiante, o PHP já possui alguma variável pré-definidas cujos nomes
são formados por letras maiúsculas.

Não há um padrão para nomes de variáveis podemos criar algo como
\$teste\_valor ou \$testeValor desde que a aplicação inteira use o mesmo
padrão. Particurlamente em caso de nome composto eué recomendado o
padrão camelCase. *\$matriculaUsuario*, *\$valorTotal*, etc, pois esse é
o padrão adotado nos argumentos de funções e métodos de classes.

### Tipos de variáveis

-   Inteiro
-   Array
-   Objeto
-   String
-   Ponto flutuante
-   Boolean

### Constantes

Constantes são um tipo especial para armazenar valores fixos, diferentes
de variáveis que podem ter seus valores alterados ao decorrer do script.
No PHP uma constante é definida com caracteres em maiúsculo.

*define('FILE\_READ\_MODE', 0644);*

Primeiros passos com PHP
------------------------

Crie um diretório chamado */home/seu\_usuario/www/cap1*.
```
<!DOCTYPE html>
<html>
    <head>
       <meta charset="UTF-8">
       <title>Curso PHP Básico do Jeito Certo</title>
    </head>
    <body>
        <?= "Bem-vindo ao PHP"; ?>
    </body>
</html>
```
Salve em */home/seu\_usuario/www/PHPBasico/Cap1/exemplo1.php*, no
browser digite
[*http://localhost/*](http://localhost/PHPBasico/Cap1/exemplo1.php)[*PHPBasico*](http://localhost/PHPBasico/Cap1/exemplo1.php)[*/*](http://localhost/PHPBasico/Cap1/exemplo1.php)[*Cap1*](http://localhost/PHPBasico/Cap1/exemplo1.php)[*/*](http://localhost/PHPBasico/Cap1/exemplo1.php)[*exemplo1*](http://localhost/PHPBasico/Cap1/exemplo1.php)[*.php*](http://localhost/PHPBasico/Cap1/exemplo1.php).

Vimos agora um exemplo prático de um script PHP rodando no navegador com
TAGs HTML 5. Iremos agora modificar o arquivo criado acima e implementar
os conceitos aprendidos nos tópicos já aprendidos.

**Nota:** Nos arquivos PHP que forem usados para exibição do HTML como
no exemplo acima é recomendado o uso da tag, `<`?= ?`>` ao invés da
tag `<`?php echo ?`>`;

```
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>Curso Básico - PHP do Jeito Certo</title>
    </head>
    
    <body>
    <?= '<h1>Bem-vindo ao PHP</h1>';
    echo '<h2>Variáveis e Constantes</h2>';
    //Isso é um comentário de uma linha

    //vamos estudar agora as variáveis
    $nome = 'Anna Clara'; //Variável tipo string

    $sobrenome = 'Da Fonseca'; //Variável tipo string

    $idade = 33; //Variável tipo integer

    $altura = 1.69; //Variável tipo float

    $genteFina = true; //Variável tipo boolean

    \* Comentário em bloco muito usado para grandes descrições
    * Exibindo o resultado no navegador
    */

    echo $nome . '<br />';
    echo $sobrenome . '<br />';
    echo $idade . "<br />";
    echo $altura . '<br />';
    echo $genteFina . '<br /><br />'; //Esse 1 representa um true (verdadeiro)

    //Agrupando as variáveis em um texto
    echo 'Olá meu nome é ' . $nome . ' ' . $sobrenome . '. <br/>';

    echo 'Tenho ' . $idade . ' anos e minha altura é ' . $altura . 'm<br /><hr />';

    //Constantes
    define('SO', 'GNU/Linux Ubuntu'); //definindo uma constante
    define('FERRAMENTAS_ESCRITORIO', 'LibreOffice');

    echo 'Eu uso ' . SO . ' com ' . FERRAMENTAS_ESCRITORIO;

    '<br /> O Valor de PI é: ' . M_PI //Constante Interna do PHP

    ?>
    </body>
</html>
```

Salve o arquivo e atualize o browser para ver o resultado.

Dando continuidade à sintaxe básica do PHP, veremos agora como trabalhar
com os arrays. Eles são de suma importância para os desenvolvedores de
qualquer linguagem. Com ele podemos agrupar várias informações em uma
única variável. Também muito útil para agrupar valores de um mesmo
contexto.

```
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>Curso Básico - PHP do Jeito Certo</title>
    </head>
    
    <body>
    <?php
    echo '<h1>Exemplo 2</h2>

    <h2>Arrays Simples</h2>';

    //Array simples com indice automático
    $frutas = array('Goiaba', 'Jaca', 'Uva', 'Cacau');

    echo '<pre>';
    print_r($frutas);
    echo '</pre>';

    //Array simples com indice manual
    $frutas = array(3 => 'Goiaba', 6 => 'Jaca', 1 => 'Uva', 4 => 'Cacau');

    echo '<pre>';
    print_r($frutas);
    echo '</pre>';

    echo 'Exibindo um elemento do array $frutas ' . $frutas[6] . '<br />';

    //Outra forma de se montar um array
    $marcaCarro[0] = 'BMW';
    $marcaCarro[1] = 'Mercedes';
    $marcaCarro[2] = 'Porche';

    echo '<pre>';
    print_r($marcaCarro);
    echo '</pre>';

    echo 'Exibindo um elemento do array $marcaCarro ' . $marcaCarro[0] . '<br />';
    ?>
    </body>
</html>
```

<span id="__DdeLink__1832_1532099292" class="anchor"></span>Salve em
*/home/seu\_usuario/www/PHPBasico/Cap1/exemplo2.php*, no browser digite
[*http://localhost/*](http://localhost/PHPBasico/Cap1/exemplo2.php)[*PHPBasico*](http://localhost/PHPBasico/Cap1/exemplo2.php)[*/*](http://localhost/PHPBasico/Cap1/exemplo2.php)[*Cap1*](http://localhost/PHPBasico/Cap1/exemplo2.php)[*/exemplo*](http://localhost/PHPBasico/Cap1/exemplo2.php)[*2*](http://localhost/PHPBasico/Cap1/exemplo2.php)[*.php*](http://localhost/PHPBasico/Cap1/exemplo2.php).

```
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>Curso Básico - PHP do Jeito Certo</title>
    </head>
    
    <body>
    <?php
    echo '<h1>Exemplo 3</h2>

    <h2>Arrays Matriz</h2>';

    $compras = array(
        'semana1' => array(
            'item1' => array(
                'produto' => 'Maça',
                'valor' => 5.87,
                'peso' => '1kg',
            ),
            'item2' => array(
                'produto' => 'Feijão',
                'valor' => 3.77,
                'peso' => '1kg',
            ),
        ),
        'semana2' => array(
            'item1' => array(
                'produto' => 'Arroz',
                'valor' => 7.27,
                'peso' => '5kg',
             ),
             'item2' => array(
                'produto' => 'Feijão',
                'valor' => 3.77,
                'peso' => '1kg',
             ),
             'item3' => array(
                'produto' => 'Farinha',
                'valor' => 2.01,
                'peso' => '1kg',
             ),
        ),
    );

    //Exibindo todos os elementos do Array
    echo '<pre>';
    print_r($compras);
    echo '</pre>';

    //exibindo semana1
    echo '<pre>';
    print_r($compras['semana1']);
    echo '</pre>';

    //exibindo semana1 e o item2
    echo '<pre>';
    print_r($compras['semana1']['item2']);
    echo '</pre>';

    //exibindo individualmente o produto farinha
    echo 'Hoje eu comprei ' . $compras['semana2']['item3']['produto'];
    ?>
    </body>
</html>
```

Salve em */home/seu\_usuario/www/PHPBasico/Cap1/exemplo3.php*, no
browser digite
[*http://localhost/*](http://localhost/PHPBasico/Cap1/exemplo3.php)[*PHPBasico*](http://localhost/PHPBasico/Cap1/exemplo3.php)[*/*](http://localhost/PHPBasico/Cap1/exemplo3.php)[*Cap1*](http://localhost/PHPBasico/Cap1/exemplo3.php)[*/exemplo*](http://localhost/PHPBasico/Cap1/exemplo3.php)[*3*](http://localhost/PHPBasico/Cap1/exemplo3.php)[*.php*](http://localhost/PHPBasico/Cap1/exemplo3.php).

```
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>Curso Básico - PHP do Jeito Certo</title>
    </head>
    
    <body>
    <?php
    echo '<h1>Exemplo 4</h2>

    <h2>Arrays Matriz</h2>';

    $compras = [
        'semana1' => [
            'item1' => [
                'produto' => 'Maça',
                'valor' => 5.87,
                'peso' => '1kg',
            ],
            'item2' => [
                'produto' => 'Feijão',
                'valor' => 3.77,
                'peso' => '1kg',
            ],
        ],
        'semana2' => [
            'item1' => [
                'produto' => 'Arroz',
                'valor' => 7.27,
                'peso' => '5kg',
            ],
            'item2' => [
                'produto' => 'Feijão',
                'valor' => 3.77,
                'peso' => '1kg',
            ],
            'item3' => [
                'produto' => 'Farinha',
                'valor' => 2.01,
                'peso' => '1kg',
            ],
        ],
    ];

    //Exibindo todos os elementos do Array
    echo '<pre>';
    print_r($compras);
    echo '</pre>';

    //exibindo semana1
    echo '<pre>';
    print_r($compras['semana1']);
    echo '</pre>';

    //exibindo semana1 e o item2
    echo '<pre>';
    print_r($compras['semana1']['item2']);
    echo '</pre>';

    //exibindo individualmente o produto farinha
    echo 'Hoje eu comprei ' . $compras['semana2']['item3']['produto'];
    ?>
    </body>
</html>
```

Salve em */home/seu\_usuario/www/PHPBasico/Cap1/exemplo4.php*, no
browser digite
[*http://localhost/*](http://localhost/PHPBasico/Cap1/exemplo4.php)[*PHPBasico*](http://localhost/PHPBasico/Cap1/exemplo4.php)[*/*](http://localhost/PHPBasico/Cap1/exemplo4.php)[*Cap1*](http://localhost/PHPBasico/Cap1/exemplo4.php)[*/exemplo*](http://localhost/PHPBasico/Cap1/exemplo4.php)[*4*](http://localhost/PHPBasico/Cap1/exemplo4.php)[*.php*](http://localhost/PHPBasico/Cap1/exemplo4.php).

**Nota:** Esse último exemplo mostra como os arrays estão sendo
utilizados principalmente nas versões mais novas do PHP e também é um
tipo de notação que vem sendo adotadas em frameworks.

Referências
-----------

Arrays em php é um assunto muito vasto, existem muitas funções internas
do php só para tratamento de arrays. Conheça essas funções do php em:
**http://php.net/manual/pt\_BR/book.array.php**

Resumo do capítulo
------------------

Nesse capítulo aprendemos o básico do básico no PHP. Como criar e
manipular variáveis do tipo string, boolean, integer e arrays, criar e
usar constantes, comentários simples e em blocos, concatenamos o texto
com variáveis com o operador '.' (ponto).

Exercícios
----------

1.  Crie um array simples contendo 7 animais selvagem e exiba na tela
    cada item com seu respectivo índice;

2.  Crie um array simples contendo 5 animais domésticos e exiba na tela
    cada item com seu respectivo índice;

3.  Crie uma matriz chamado animais dividindo em animais domésticos e
    selvagens, para facilitar pode atribuir os dois arrays simples
    criados nos itens anteriores. Exiba na tela um texto contendo, “meu
    animal selvagem favorito é: ” e “meu animal doméstico favorito é: ”
    e escolha um de sua preferência.
