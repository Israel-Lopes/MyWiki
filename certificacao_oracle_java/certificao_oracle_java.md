# ![certificao_banner](img/certificao_banner.png)

## Certificacao Oracle Java 8

<br />

### Sumario

1. [defina escopo de variaveis](#defina_escopo_de_variaveis)
1. [estrutura de uma classe](#estrutura_de_uma_classe)

<br />

### Defina escopo de variaveis <a name="defina_escopo_de_variaveis">

O escopo  e o que determina em que pontos do codigo uma variavel pode ser usada.

### Variaveis locais

Chamamso de locais as variaveis declaradas dentro de blocos, como dentro de metodos ou construtores.
  - O ciclo de vida de uma variavel vai do ponto onde ela foi delcarada ate o fim do bloco.
  - `{// Bloco}`

Parametro de metodos tambem sao considerados variaveis locais.

  - `public void correr( String passos ) {`

### Variaveis de Instancia

Variaveis de instancia ou variaveis de objeto sao os atributos dos objetos. Sao declaradas dentro da classe.

### Variaveis estaticas

Sao variveis que nao podem ter seu valor auterado. Sao precedidas pela palavra rezervada **static**.

  - `static valorDePI = 3,14`

<br />

### Estrutura de uma classe <a name="estrutura_de_uma_classe">

### Pacotes

Pacotes servem para separar e organizar diversas classes do sistema.

Para definir um pacote, se utiliza a palavra reservada **package**.

  - `package br.com.apinegocios.calculos`

### Classe 

A classe e onde definimos os atributos e comportamentos de um objeto.

  - `class Pessoa {}`

### Variaveis 

Variaveis sao bem simples de serem declaradas. Sempre se comeca pelo tipo seguido do nome dela.

  - `String nome`

### Metodos

Para declarar metodos precisamos do tipo do retorno, seguido do nome e fecha parenteses, podendo aver parametros ou nao de entrada.

### Construtores

Uma classe pode ter zero ou varios construtores. O construtor deve nao possuir retorno e seu nome ser igual da classe.

Construtor e usado para validar os dados de uma classe, mas em geral o compilador cria o construtor automaticamente.

```
classe Pessoa () {

  Pessoa () {// Cosntrutor}
  
  void Pessoa () {// Methodo}

}
```
### Interfaces

Alem de classes, tambem podemos declarar interfaces. Basta declarar palavra reservada **interface** antes. 

Interfaces possuem apenas methodos abstratos e nao podem ser estaticos, pois a interface e abstrata.

```
interface Autenticacao {

  final int tamanhoDaSenha = 8;
```
E possivel declarar mas de uma classe ou interface no mesmo arquivo, porem nao e uma boa pratica.
























