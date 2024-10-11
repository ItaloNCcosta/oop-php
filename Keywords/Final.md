## Entendendo a palavra-chave `final` no PHP

### O que é a palavra-chave `final`?

No PHP, a palavra-chave **`final`** é usada para indicar que uma classe ou um método não pode ser estendido ou sobrescrito. Ou seja, uma classe declarada como `final` não pode ser herdada, e um método marcado como `final` não pode ser redefinido em classes filhas. Isso é útil quando você quer garantir que a implementação de uma classe ou método permaneça inalterada em subclasses.

### Conceitos importantes

Antes de explorar exemplos de uso da palavra-chave `final`, é importante ter um entendimento básico de dois conceitos de Programação Orientada a Objetos:

- **Herança**: A herança permite que uma classe (chamada de classe filha) herde métodos e propriedades de outra classe (classe pai). Isso permite o reaproveitamento de código e a especialização de comportamento.
- **Encapsulamento**: O encapsulamento se refere à prática de esconder detalhes internos de uma classe, permitindo que o acesso e a manipulação de seus dados sejam feitos apenas através de métodos específicos (getters e setters).

Agora que esses conceitos estão claros, vamos ver como `final` funciona na prática.

### Exemplo prático

Vamos criar uma classe abstrata chamada `Carro`, que serve como base para outros tipos de carros. Dentro dessa classe, temos métodos abstratos e concretos, e deixaremos para as subclasses a responsabilidade de implementar as particularidades de cada carro.

```php
<?php

// Classe abstrata Carro, que força as subclasses a implementar a descrição.
abstract class Carro
{
	protected string $motor;

	// Construtor que inicializa o motor do carro
	public function __construct(string $motor){
		$this->motor = $motor;
	}
	
	// Método abstrato que obriga subclasses a fornecer uma descrição do carro
	abstract public function getDescricao(): string;

	// Método para obter o tipo de motor do carro
	public function getMotor(): string
	{
		return $this->motor;
	}
}
```

Aqui, criamos uma classe abstrata `Carro` que define um motor e exige que qualquer classe filha implemente o método `getDescricao()`. Agora vamos criar duas classes que representam carros específicos: o Fusca e o Uno.

### Classe Fusca com `final`

O Fusca será uma classe `final`, o que significa que nenhuma outra classe poderá herdar dela, garantindo que a implementação do Fusca permaneça inalterada.

```php
// Classe Fusca, marcada como final para impedir herança
final class Fusca extends Carro 
{ 
	public function __construct(string $motor = 'boxer')
	{
		parent::__construct($motor);
	}

	// Implementação do método abstrato para descrever o Fusca
	public function getDescricao(): string {
		return "Fusca é um carro clássico feito pela Volkswagen no final da Segunda Guerra Mundial.";
	}
}
```

### Classe Uno

Agora, vamos criar a classe `Uno`. A princípio, tentaremos herdar do Fusca, mas isso resultará em um erro.

```php
// Tentativa de herdar da classe Fusca, que é final
class Uno extends Fusca
{
	public function __construct(string $motor = 'sevel')
	{
		parent::__construct($motor);
	}
	
	// Implementação do método abstrato para descrever o Uno
	public function getDescricao(): string {
		return "Uno é um carro popular brasileiro feito pela Fiat. Um carro simples, leve e robusto.";
	}
}
```

Ao tentar executar esse código, receberemos o seguinte erro:

```shell
PHP Fatal error:  Class Uno cannot extend final class Fusca in /index.php on line 16
```

Isso ocorre porque `Fusca` foi declarada como uma classe `final`, e a classe `Uno` não pode herdar dela.

### Corrigindo o erro

Para corrigir esse erro, precisamos fazer o `Uno` herdar diretamente da classe `Carro`, ao invés de herdar do Fusca. Veja o código corrigido abaixo:

```php
// Classe Uno herdando corretamente de Carro
class Uno extends Carro
{
	public function __construct(string $motor = 'sevel')
	{
		parent::__construct($motor);
	}
	
	// Implementação do método abstrato para descrever o Uno
	public function getDescricao(): string {
		return "Uno é um carro popular brasileiro feito pela Fiat. Um carro simples, leve e robusto.";
	}
}
```

Agora, com essa correção, o código funcionará conforme esperado. Podemos criar instâncias das duas classes e obter suas descrições e motores:

```php
// Criando instâncias e exibindo os resultados
$fusca = new Fusca();
echo "Motor do Fusca: " . $fusca->getMotor() . PHP_EOL;
echo "Descrição: " . $fusca->getDescricao() . PHP_EOL;

$uno = new Uno();
echo "Motor do Uno: " . $uno->getMotor() . PHP_EOL;
echo "Descrição: " . $uno->getDescricao() . PHP_EOL;
```

### Conclusão

A palavra-chave **`final`** no PHP é uma ferramenta poderosa para garantir que uma classe ou método específico não seja sobrescrito ou herdado. Isso é útil em casos onde você quer evitar modificações em implementações sensíveis ou específicas, como vimos no exemplo do Fusca. Ao usar `final`, você garante que as subclasses respeitem as regras e limites que você definiu no design da aplicação.