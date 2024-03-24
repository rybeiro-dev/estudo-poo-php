# POO - PHP Orientado a Objetos

### CLASSE
Uma classe é um tipo complexo de dado para a definição de objetos. Para criar uma classe utilizamos a palavra reservada _class_.

```php
class PessoaFisica
{
    # aqui podemos escrever as propriedades e métodos
}
```

### OBJETO
Um objeto é a representação (instância) de uma classe. Para criar objetos utilizamos a palavra reservada _new_.

```php
$pessoa = new PessoaFisica
```

### TIPAGEM
Uma camada importe de segurança é trabalhar com tipagem. É recomendado o uso de tipagem forte para aumentar a segurança
do projeto e deve ser declarado nas Models e Controllers.

```php
# Isso é suficiente para deixar o arquivo seguro
declare(strict_types=1)
```

### PROPRIEDADE
São caracteristicas da classe para criação do objeto, no caso de uma pessoa física: Nome, idade, email e outros.

```php
class PessoaFisica
{
    private string $nome;
    private string $idade;
    private string $email;
}
```

### MÉTODO
São ações que utilizamos na classe, como por exemplo obter o nome.

```php
class PessoaFisica
{
    public function getNome(): string
    {
        return $this->nome;
    }
}
```


### SELF e THIS - diferença
_this_ é utilizado para acesso a métodos e propriedades da classe, enquanto, _self_ é utilizado para acesso a constantes e conceitos estáticos.


### HERANÇA
Herança é quando temos propriedades e métodos que são comuns em outras classes. Para usar herança utliza-se a palavra reservada _extends_.

```php
class PessoaFisica
{
    public string $name = 'Teste';
}

class PessoaJuridica extends PessoaFisica
{
    public function proprietario(): string
    {
        echo $this->nome . EOF_PHP;
    }
}

$pj = new PessoaJuridica();

print_r($pj->proprietario());
```

### CLASSE ABSTRATA
Classes abstratas são declaradas com o propósito de representar uma espécie de esqueleto para suas subclasses, sem permitir instâncias..

Métodos também podem ser declarados como abstract e, com isso, não possuem implementação. As classes que estendem uma classes abstratas devem implementar os métodos de modo específico.

```php
abstract class Pessoa
{
    public string $name;    
}

class PessoaFisica extends Pessoa
{
    public string $cpf;
}

class PessoaJuridica extends Pessoa
{
    public string $cnpj;
}

$pf = new PessoaFisica();

$pj = new PessoaJuridica();

dump($pf);
dump($pj);

```





## Iniciando
Dentro da raiz do projeto vamos criar nosso pacote com o _Composer_

```shell
composer init

```

# IMPORTANTE:
Para melhorar a depuração do código instalar o pacote __var-dumper_ do _symfony_ apenas no ambiente de desenvolvimento.

```shell
composer require --dev symfony/var-dumper
```