## Classes
Classe é o "esqueleto" de um objeto. Dentro temos varias caracteristica que sao chamadas de atributos e algumas funçoes que esse objeto tem que sao chamados de metodos. Uma classe nada mais é que a representaçao de um objeto.
## Objeto
Objeto é a representaçao de algo, seja de forma final, abstrata ou qualquer outra representaçao de objeto fisico. O objeto é representado por uma classe.
## Instância
É quando transforma a classe em objeto. Quando criando um arquivo e dentro nos colocamos `class Car {}` nos estamos criando uma classe que é a representaçao de um objeto (mas para o codigo, ainda nao é um objeto). 

	Entao quando ele se torna um objeto ?
Uma classe passa a ser um objeto quando nos instânciamos a classe. por exemplo:
```php
class Car {}

$car = new Car(); //instanciando a classe Car
var_dump($car);
```

Depois de instânciarmos, e imprimimos/mostramos a variavel `$car`, irar nos mostrar que a variavel tem o valor do objeto.