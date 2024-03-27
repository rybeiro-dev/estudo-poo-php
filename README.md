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

### Encapsulamento
Encapsular os dados de uma aplicação significa evitar que estes sofram acessos indevidos. Trata-se da visibilidade de propriedades e métodos da classe.
```php
public # permite o acesso através da instância filha
private # Não permite o acesso através da instância filha
protected # permite o acesso através da instância filha
```

### Interface
Uma interface assemelha-se a um contrato, podemos definir métodos que as classes que implementam esta interface serão obrigados a implementar.

```php
# Criando a interface
interface PessoafisicaInterface
{
	public function getCpf(): string;
}

# utilizando a inteface

class PessoaFisica implements PessoafisicaInterface
{
	public function getCpf(): string
	{
		return $this->cpf;
	}
}
```

### Abstração
Com métodos abstrados e obrigatórios de implementação.

```php
abstract class Pessoa
{
	public string $name;

	abstract public function getName(): string;
}
```

### Type hinting

O _type hinting_ é um dos novos recurso da nova versão do PHP. Com o uso da linguaguem fortemente tipada podemos sugerir na entrada do método para um parâmetro um ou mais tipo de dado. Também temos a opção do _callable_ que é a declaração de um método como parâmetro.

```php
class Person
{
	# aqui o uso de typehighing
	public function greetings(string $name, int $age, int|float $weight, int|float $height, callable imc): string|null
	{
		return "Olá {$name}, você possui {$age} de idade e o seu peso é {$weight}. Muito bom!";
	}
}

$person = new Person();

echo $person->grettings('Fabio', 44, 82.7, 1.74, function(int|float $weight, int|float $height){
	$imcCalculated = $weight / ($height * $height);

	return "O seu IMC: {$imcCalculated}";
}) . PHP_EOL;
```
	
Também tem o tipo de dado _never_ que declara que uma função não retorna nada.

```php
function showSystemInfo(): never
{
	echo shell_exec("uptime");
	exit;
}
```

###  Final Class
É utilizado quando se tem uma classe bem definida e coeza e não queremos que seja extendida por ninguém. Quem tentar extender vai receber uma exception. A partir o PHP 8.2 ao invés de usar o _final_ usa-se _readonly_

```php
final class PessoaFisica
{
	#métodos e propriedades
}
```

### Polimorfismo
Polimorfismo  é a capacidade de diferentes classes implementarem métodos com o mesmo nome, mas com comportamentos específicos para cada classe.

Exemplo:
```php

<?php

// Definição da classe Animal
class Animal {
    public function emitirSom() {
        echo "Som genérico de animal\n";
    }
}

// Definição da classe Cachorro, que herda de Animal
class Cachorro extends Animal {
    public function emitirSom() {
        echo "Au au!\n";
    }
}

// Definição da classe Gato, que herda de Animal
class Gato extends Animal {
    public function emitirSom() {
        echo "Miau!\n";
    }
}

// Função que recebe um animal e faz ele emitir som
function fazerAnimalEmitirSom(Animal $animal) {
    $animal->emitirSom();
}

// Criando instâncias das classes
$cachorro = new Cachorro();
$gato = new Gato();
$animalGenerico = new Animal();

// Chamando o método emitirSom de cada objeto
fazerAnimalEmitirSom($cachorro); // Saída: Au au!
fazerAnimalEmitirSom($gato);     // Saída: Miau!
fazerAnimalEmitirSom($animalGenerico); // Saída: Som genérico de animal
?>

```

### Contructor Property Promotion
E a técnica que possibilita a criação das propriedades da classe visibilidade diretamente no parâmetro do contrutor. O Construtor já faz todo o processo na instância para permitir o acesso às propriedades.

```php
public function __construct(protected string $name, protected string $documento){}
```

### Trait
Trait é uma coleção de métodos que podem ser incluídos em qualquer classe em PHP.

```php
# exemplo:
<?php

// Definindo um Trait chamado Mensagens
trait Mensagens {
    public function mensagemBoasVindas() {
        echo "Bem-vindo!\n";
    }

    public function mensagemDespedida() {
        echo "Até logo!\n";
    }
}

// Definindo uma classe que usa o Trait Mensagens
class MinhaClasse {
    use Mensagens;

    public function outroMetodo() {
        echo "Este é outro método da classe.\n";
    }
}

// Criando uma instância da classe MinhaClasse
$objeto = new MinhaClasse();

// Chamando métodos da classe MinhaClasse e do Trait Mensagens
$objeto->mensagemBoasVindas(); // Saída: Bem-vindo!
$objeto->mensagemDespedida(); // Saída: Até logo!
$objeto->outroMetodo(); // Saída: Este é outro método da classe.
?>

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