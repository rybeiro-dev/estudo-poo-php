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

### StdClass
StdClass é um objeto dinâmico do PHP. No StdClass criamos apenas propriedades públicas.

```php
$dinamicObject = new StdClass();
$dinamicObject->name = "Fabio";
$dinamicObject->gender = 44;

dump($dinamicObject);
```

Convertendo um array em um _StdClass_
```php
$arr = ['name' => 'Fabio', 'gender' => 44];
gettype($arr);
# a conversão é um simples casting
$arr = (object) ['name' => 'Fabio', 'gender' => 44];
gettype($arr);
```

### DTO - Data Transfer Object
Quando se trabalha com APIs de terceiros é uma boa prática criar um diretório _DataTransferObject_ e implementar a classe para trabalhar com os dados.

```php
use stdclass;

class PersonDTO
{
	public function __construct(private stdclass $properties, private string $name = '', private string $gender = '')
	{
		$this->name = $properties->name;
		$this->gender = $properties->gender;
	}

	public function getName():string
	{
		return $this->name;
	}

	public function getGender(): string
	{
		return $this->gender;
	}
}

$json = '{"name":"Fabio", "gender":"male"}';

$person = PersonDTO(json_decode($json));

dump($person->getName());
dump($person->getGender());
```

### Classes Anônimas
Uma classe anônima é útil para criar uma classe para criar propriedades e métodos. Também é possível extender de outras classe, usar implementações.

```php
$person = new class(){
	public function __construct(private stdclass $properties, private string $name = '', private string $gender = '')
	{
		$this->name = $properties->name;
		$this->gender = $properties->gender;
	}

	public function getName():string
	{
		return $this->name;
	}

	public function getGender(): string
	{
		return $this->gender;
	}
}

$json = '{"name":"Fabio", "gender":"male"}';

$person = PersonDTO(json_decode($json));

dump($person->getName());
dump($person->getGender());

```

### InstanceOf
Para verificar se uma instância é de uma classe pode utilizar o _instanceOf_
Verificando uma classe com _instanceOf_

```php
$person = new Person();

if ($person instanceOf Person) echo "yes";

```

### Métodos estáticos
Para definir um método estático usar a palavra reservada _static_ no cabeçalho.

```php
class ViaCepService
{
	public static function handle(string $cep): array
	{
		return Http::get("viacep.com.br/ws/{$cep}/json/")->json();
	}
}

dump( ViaCepService::handle('06810040') );
```

### ENUM
Em PHP, ENUM é uma estrutura de dados que representa um conjunto fixo de valores nomeados. Enum pode ser usado para definir estados.

Enum é uma instância de _Sington_


##### Conceito com PHP

```php

enum Naipe{
	case Copas;
	case Ouros;
	case Paus;
	case Espadas;
}

Naipe::Copas->name
```

_BackedEnum_ aceita string ou integer

```php
enum Naipe: string
{
	case Copas = 'C';
	case Ouros = 'O';
	case Paus = 'P';
	case Espadas = 'E';
}

Naipe::Espadas->value;
```

É possível utlizar _implements_ para Enums.

```php
interface Colorido
{
	public function cor(): string;
}


enum Naipe: string implements Colorido
{
	case Copas = 'C';
	case Ouros = 'O';
	case Paus = 'P';
	case Espadas = 'E';

	public function cor(): string
	{
		return match($this){
			Naipe::Copas, Naipe::Ouros => 'Vermelho',
			Naipe::Paus, Naipe::Espadas => 'Preto',
		}
	}
}

function pintar(ColoridoInterface $colorido)
{
	echo "Cor do Naipe: {$colorido->cor()}";
}

pintar(Naipe::Ouro);

```

Para retornar todos os casos de uma _Enum_, tem o método _cases()_
```php
enum Colors
{
	case Red;
	case Blue;
	case Green;
}

print_r(Colors::cases());
```

##### Conceito com Laravel
Organizar as _Enums_ no diretório. Usar _Enums_ ao invés de uma tabela de banco de dados.

```php

enum StateEnum: string
{
	case Ativo = 'ativo';
	case Inativo = 'inativo';
}

```

Suponha que temos uma classe Post; Fazer o _casting_ no _Model_.

```php
class Post extends Model
{
	protected $casts = ['state' => StateEnum::Class]
}


echo Post::first()->state->name . PHP_EOL;
echo Post::first()->state->value . PHP_EOL;

```

> IMPORTANTE: Na _Migration_ de _Post_ pode utilizar o tipo _string_ se utilizar o tipo _enum_ todos os valores deve ser definidos na tabela.

```php
# usando string
$table->string('state')->default('ativo');

# usando enum
$table->enum('state', ['ativo', 'inativo']);
```

> *Pode acessar um _Enum_ direto no _Route_* através 


###  Namespaces e Autoload no padrão PSR-4
Namespace é uma maneira de encapsular itens, como classes, interfaces, funções e constantes, em grupos distintos, evitando conflitos de nomes e fornecendo uma forma de organizar e estruturar o código de uma aplicação.

O padrão PSR-4 (PHP Standards Recommendation 4) é um conjunto de diretrizes estabelecidas pela PHP-FIG (PHP Framework Interop Group) para padronizar a autoloading de classes em PHP. O objetivo principal do PSR-4 é facilitar a inclusão automática de classes (autoloading) em um projeto PHP, eliminando a necessidade de incluir manualmente arquivos de classe.

Em projetos crie o seu pacote do composer para encapsular (empacotar) o seu projeto e suas dependências.

```php
composer init # Algumas perguntas serão feitas para o projeto
```

Para ter um namespace simplificado altere no composer.json para App. E execute o comando ```composer dumpautoload -o``` para recarregar as classes do projeto. É necessário alterar manualmente nas classes.

```json
"autoload":{
	"psr-4":{
		"App\\": "src/"
	}
}
```

### Exceptions


## Métodos Mágicos

### \__construct() e \__destruct()

Todos os métodos no PHP que começam com duplo underline é considerado um método mágico.
```php
# construtor com Property Promotion
public function __construct(public string $name, public int $age = 0)
{
	parent::__construct(); # passar parametro para a classe pai
}

# Utilizado em caso que precisa forçar a destruição de algum objeto para liberar memória.
public function __destruct()
{
	echo "Chamou o destruct";
}
```

### \__get() e \__set()
O método _\__get()_ é utilizado para ler propriedades inacessíveis são _protected_, _private_ e inexistentes.

Com o método mágico \__get() conseguimos evitar erros de acesso a propriedades.

```php
public function __get(string $name): string
{
	if(property_exists($this, $name)){
		return $this->$name;
	}

	return null;
}
```

Com o método mágico \__set() conseguimos criar a propriedade e valor caso ela não exista.

```php
public function __set(string $name, mixed $value): void
{
	$this->$name = $value;
}
```

### \__call() e \__callStatic()
\__call() é chamado ao acessar métodos inacessiveis protegidos ou privados ou inexistente em um contexto de objeto.

Podemos utilizar esse método para muitas coisas, entre elas direcionar mensagens de erro/falhas e utilizar como método dinâmico.

```php
# sintaxe
class Invoice
{
	public function __call(string $method, array $parameters): mixed
	{
		dd($method, $parameters);
	}
}

$invoice = new Invoice;

$invoice->process();
```

Exemplo de sobreescrita

```php
class Invoice
{
	protected function process(float $amount, string $description)
	{
		dump('Chamaou', $amount, $description);
	}

	public function __call(string $method, array $parameters): mixed
	{
		if(method_exists($this, $method)){
			call_user_func_array([$this, $method], $parameters)
		}

		return $this;
	}
}

$invoice = new Invoice;

$invoice->process();
```

\__callStatic() é invocado em contexto estático de métodos inacessíveis protegidos ou privados ou inexistente.

```php
class Invoice
{
	public function __callStatic(string $method, array $parameters): mixed
	{
		# dd($method, $parameters);
		return (new static)->$method(...$parameters);
	}
}

Invoice::process(4,'faturamento');
```

### \__isset() e \__unset()

Esses métodos mágicos são invocados quando usamos o método isset() ou unset() em um contexto de objeto ao acessar métodos inacessiveis protegidos, privados ou inexistente.

```php
class Invoice
{
	# sintaxe __isset()
	$properties = [];

	public function __isset(string $key): bool
	{
		return array_key_exists($key, $properties);
	}


	# sintaxe __unset()
	public function __unset(string $key): void
	{
		unset($this->properties[$key]);
	}
}
```

### \__toString()

```php
```

### \__invoke()

O método invoke() é chamado quando usamos um objeto como função.

```php
class User 
{
	public function __invoke(): mixed
	{
		dump('Chamada do método __invoke');
	}
}

$user = new User;

# chamada de objeto como função
dd( $user());
```

## PHP Readonly
Trata-se um classe somente leitura que garante que as propriedades não sejam manipuladas.

```php
readonly class PaymentService
{
	# utilizando a técnica Constructor Property Promotion.
	public function __construct(public string $token)
	{}
}

$pay = new PaymentService;
echo $pay->token;
```

## Value Object - email
_Value Object_ é um padrão de projeto para criar objetos que representam valores específicos do seu domínio, como email, dinheiro, endereços etc. Esses objetos tem por caracteristicas serem imutáveis, sem identidade, representam um conceito especifico.

```php
class Email
{
	public function __construct(protected string $email)
	{
		$this->validate();
	}

	private function validate(): void
	{
		if(!filter_var($this->email, FILTER_VALIDATE_EMAIL)){
			throw new \DomainException('Formato de email inválido!');
		}
	}
}
```

## Reflexion Api
É a api do PHP que da acesso mais profundo aos métodos e propriedades independentemente do encapsulamento.

A _Reflexion Api_ tem vários métodos para acesso aos dados.

```php
class Cliente
{
	public function __construct(private string $telefone){}

	private function telefone(): string
	{
		return $this->telefone;
	}
}

$reflection = new \ReflectionClass(Cliente::class);
```

Nas versões igual ou maior que o PHP 8.2 conseguimos evitar o _hacke_ de acesso utilizando _readonly_

```php
class Pessoa
{
	# Simplimente criamos uma variável somente leitura
	public function __construct(private readonly $nome){}
}
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