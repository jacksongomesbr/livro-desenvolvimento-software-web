
#Método GET
O método GET cria um **array** de chaves e valores *(exemplo, chave1=>valor1, chave2=>valor2, ..., chaven=>valorn)*, em que as chaves correspondem aos nomes dos controles dos formulários e os valores correspondem aos dados de entradas fornecidos pelo usuário. 

O atributo `method` define o método de envio dos dados do formulário, conforme exemplificação a seguir:

```html
<html>
<body>
    <form name="form1" method="GET">
        <input name="textNome" type="text">
        <input name="btnEnviar" type="submit" value="Enviar">
    </form>
</body>
</html>
```

Uma vez que o usuário informar algum valor no campo de texto do formulário e clicar no botão **Enviar**, um array de **chave=>valor** será criado e passado via URL. Este array é também chamado de **Query String**. 

Supondo que o usuário digite **John** no campo de texto e clique no botão **Enviar**, o seguinte array será criado e enviado pela URL: 
**?textNome=John&btnEnviar=Enviar**. O caracter **?** separa a URL base do array com os valores. Cada par *chave=>valor* é separado pelo caráter **&**. Por exemplo, se página carregada fosse *index.php*, e estivesse dentro da pasta exemplo, então a URL base poderia ser * http://localhost/exemplo/index.php* . 
##Acessando os dados do formulário em PHP
Quando os valores são enviados via *método GET*, automaticamente é criada um array chamado `$_GET` que contém todos os valores passados para o corrente *script* via URL. O array definido em `$_GET` é global para o script corrente e pode ser acessado a qualquer momento, independente do escopo (e.g. em uma função ou em uma classe), sem necessidade de nenhum tratamento especial. 

Vamos usar o código HTML definido anteriormente para acrescentar um script PHP que acessa os dados enviados via *método GET* e mostra-los no *browser*.

```php
<html>
<body>
    <?php
        if (isset($_GET["textNome"])){
            $nome = $_GET["textNome"];
            echo "Nome: ".$nome;
        }
    ?>
    <form name="form1" method="GET">
        <input name="textNome" type="text">
        <input name="btnEnviar" type="submit" value="Enviar">
    </form>
</body>
</html>
```
Na primeira vez que a página acima for carregada, um erro PHP será gerado porque o array `$_GET` e seus valores ainda **não** existem. Uma vez que o formulário for preenchido pelo usuário e o botão *Enviar* for acionado, o *array* será criado, os dados serão mostrados no *browser* e os erros deixarão de existir.

Para resolvermos o problema do erro gerado no primeiro acesso, pode ser realizada uma verificação com o intuito de identificarmos se os valores de `$_GET` não estão nulos, conforme código mostrado a seguir: 

```php
<?php
    if (isset($_GET["textNome"])){
        $nome = $_GET["textNome"];
        echo "Nome: ".$nome;
    }
?>
```
No código mostrado anteriormente foi realizada uma verificação com o auxílio da função `isset` para identificarmos se a chave `textNome` existe. Mais informações sobre a função `isset` estão disponíveis no capítulo de [Funções](../funcoes/README.md). 

As exemplificações mostradas anteriormente sempre enviam os dados para a página PHP corrente. Caso necessite enviar os dados para outra página (outro script PHP), pode ser utilizado o atributo `action` do formulário. Assim, deve ser atribuído ao atributo `action` o nome da página destino, por exemplo, `action="pagina_destino.php"` . A seguir você pode fazer [download](https://github.com/jacksongomesbr/livro-web-codigo-fonte/tree/master/php/formularios/metodo-get/projeto-1) de um projeto PHP que mostra a utilização do envio de dados para uma página diferente utilizado um formlário com método GET. 

>**DICA IMPORTANTE:**
> Caso necessite enviar parâmetros via URL é possível criar esse *array* manualmente e colocá-lo como parte do endereço. Assim, os dados também podem ser enviados via *GET* diretamente pela URL. 
```html
<a href="mostrar-dados.php?Cod=2&Nome='John'"> Passando CÓDIGO e NOME via link </a>
```
O código mostrado acima cria um link em HTML definindo o *array* de parâmetros que serão enviados para a página `mostrar-dados.php`. O projeto completo para que você possa testar está disponível para download [aqui](https://github.com/jacksongomesbr/livro-web-codigo-fonte/tree/master/php/formularios/metodo-get/projeto2). 
