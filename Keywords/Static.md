## O que é ?
É utilizada `static` para metodos ou propriedades/variaveis  tornam acessiveis sem precisar de uma instanciação da classe, Ou seja, vc pode utilizar o metodo ou propriedade de uma classe sem instanciala.
```php
<?php

class Car 
{
	static $door = 4;
	static $name = "mustang";

	public static function getName() {
		return self::$name;
	}
}

var_dump(Car::$door); // return 4
var_dump(Car::getName()); // return mustang
```

Aqui, a propriedade acessada estaticamente prefere a propriedade da classe para a qual é chamada. Onde a palavra-chave as self impõe o uso apenas da classe atual. Consulte o exemplo abaixo:
```php
<?php

class a
{
	static protected $test = "class a";

	public function static_test() {
		echo static::$test; // Results class b
		echo self::$test; // Results class a
	}
}

class b extends a
{
	static protected $test = "class b";
}

$obj = new b();
$obj->static_test();
```