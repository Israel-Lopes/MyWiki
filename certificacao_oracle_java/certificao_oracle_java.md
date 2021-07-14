# ![certificao_banner](img/certificao_banner.png)

## Certificacao Oracle Java 8

<br />

### Sumario

1. [Defina escopo de variaveis](#defina_escopo_de_variaveis)
2. [Estrutura de uma classe](#estrutura_de_uma_classe)
3. [Crie aplicacoes java com metodo main, rode na linha de comando](#rode_na_linha_de_comando)
4. [Importe outros pacotes](#importe_outros_pacotes_java)
5. [Declarar e inicializar variaveis](#declarar_e_inicializar_variaves)

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

  - `static double valorDePI = 3,14`

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

<br />

### Rode na linha de comando <a name="rode_na_linha_de_comando">

Uma classe executavel possui metodo inicial para execucao do programa o metodo main.
Metodo main e metodo principal da aplicao, onde ela e inicilizada.
Metodo main precisa seguir algumas regras para ele pode ser executado.
  - Ser publico(public).
  - Ser estatico(static).
  - Nao ter retorno(void).
  - Ter nome main.
  - Receber como parametro um array ou varargs de String(String[] ou String...).

Para executar uma classe por linha de comando, usa javac.

´$ javac nomeDoArquivoComMetodoMain.java´

### Compilacao e execucao

Para criar um programa java, e preciso escrever um codigo-fonte e, atraves de um  compilador, gerar um executavel(bytecode). o compilador do jdk e o javac.

A execucao do bytecode e feita pela **JVM**.

### Propriedades na linha de comando

Proprie sao edentificadas pelo -D antes. Este -D nao faz parte da chave.

`java -key1=abc -Dkey2=def Foo xpto bar`

-key1=abc e key2=def sao parametros/propriedades e xptop e bar sao arguemntos recebidos pelo metodo main.

### Classpath

Para compilar ou executar, e necessario que os comandos javac e java possam encontrar as classes referenciadas pela aplicacao java.

As classes feita pelo programador sao encontradas atraves do class-path(caminho das classes).

### Configurando o classpath

Ha duas maneiras de configurar o classpath:

 - Configurando a variavel de ambiente CLASSPATH no sistema operacional.
   Basta seguir as opcoes do SO em questao a definir a variavel. Isso e considerado uma má pratica no dia a dia porque e um classpath global, que vai valer para qualquer programa java executando na maquina.

- Com as opcoes -cp ou -classpath dos comandos javac ou java.

E a forma mas usada. Imagine que queremos usar alguma biblioteca junto com nosso programa:

`$ java -cp /path/to/library.jar Test.java`

`$ java -cp /path/to/library.jar Test`

E podemos passar tanto caminhos de outras pastas como de JARs ou zips.

<br />

### Importe outros pacotes java e deixe os acessiveis <a name="importe_outros_pacotes_java">

Se duas classes estao no mesmo pacote, elas se "enxergam" entre si, sem a necessidade de colocar o nome do pacote.

Para usar uma classe que esta em outro pacote, temos duas opcoes: podemos referencia-la usando o que chamamos de Full **Qualified Name**, ou seja, o nome do pacote seguido do nome da classe

### importanto classes com mesmo nome 

Quando precisamos usar classes com o mesmo nome mas  de pacotes diferentes, so podemos importar uma delas. A outra deve ser referenciada pelo **Full Qulified Name**. Tentativas de importar as classes irao resultar em erros de compilacao.

### Pacotes

Pacotes servem para organizar suas  classes e interfaces. Eles permitem agrupar componetes que tenham alguma relacao entre si, alem de garantir algum nivel de controle de acesso a menbros. Alem de serem uma divisao logica para suas classes.

### Subpacotes e estrutura de diretorios

Pacotes sao usados pela JVM como uma maneira de encontrar as classes so sistema de arquivos, logo a estrututra de diretorios do projeto deve ser a mesma da estrututra de pacotes.

### Convencoes de nomes para pacotes

Existem algumas convecoes para nomes de pacotes. Elas nao sao obrigatorias, mas gerealmente sao seguidas para facilitar o entendimento e organizacao do codigo:

  - O nome do pacote deve ser todo em letras minusculas;
  - um pacote deve comecar com site da empresa, ao contrario;
  - Apos o site,deve vir o projeto;
  - Apos o projeto, a estrutura e livre.

### Import usando classes de outros pacotes

Existem diversas maneiras de referenciar uma classe de pacotes diferente.

### Full Qualifield Name

Podemos refernciar uma classe em nosso codigo usandoo que chamamos de Full Qualifield Name, ou FQN. Ele e composto pelo pacote completo mais o nome da classe:

```
class Pessoa {
  // Full Qualifield Name
  java.util.Calendar aniversario;
}
```

Usar o FQN nem sempre deixa o codigo legivel, em vez de usar o nome completo da classe, podemos importa-la e usar apenas o nome simples da classe:

```
java.util.Calendar aniversario;

class Pessoa {
  Calendar aniversario;
}
```
E permitido importar todas as classes de um pacote usando *.


```
java.util.*;

class Pessoa {
  Calendar aniversario;
}
```

Caso importemos dois ou mas pacotes que contenham classes com o mesmo nome, sera obrigatorio usar FQN. Caso nao faca isso, tera erro.

### import static

Desde o Java 5, e possivel importar apenas metodos e atributos estaticos de uma classe, usando a palavra-chave **static**.

<br />

### Declarar e inicializar variaveis <a name="declarar_e_inicializar_variaveis">

Nem todas linguagens exige que as variaveis sejam inicializadas antes de serem utilizadas. Mas, no java, a inicializacao e obrigatoria, ode ser inplicita ou explicita.

### Tipos primitivos

Todos os tipos primitivos do java  ja estao definidos e nao e possivel criar novos tipos primitivos. Sao oito tipos primitivos:

  - byte 1 byte (8bits, de -128 a 127); 
  - short 2 bytes (16 bits, de -32.768 a 32.767);
  - char 2 bytes (so positivo), (16 bits, de 0 a 65.535);
  - int 4 bytes (32 bits, de -2.147.483.648 a 2.147.483.647);
  - long 8 bytes (64 bits, de -9.223.372.036.854.775.808 a 9.223.372.036.854.775.807);
  - float 4 bytes (32 bits, de +/-1.4*10^45a +/-3.4028235*10^38);
  - double 8 bytes (64 bits, de +/-4.9*10^324 a +/-1.7976931348623157*10^308);
    - Todos os numeros de ponto flutuante, tambem podem assumir os seguintes valores.
    - +/- infinit
    - +/- o
    - NAN (not a Number)
  - boolean

Nao ha necessidade de decorar o intervalo e tamanho de todos os tipos primitivos. O unico intervalo que e cobrado na prova e o do byte.

### Bases diferentes

No caso dos numeros inteiros, podemos declarar usando bases diferentes.

O Java suporta a base decimal e mais as bases octal, hexadecimal e binaria.

um numero na base octal tem comecar com um zero a esquerda, usa algarimos de  0 ate 7.

```
int i = 0761; // octal

System.out.println(i); // 497
```

Hexadecimal, comeca com 0x ou 0X e usa os algarismos de 0 ate 15.

```
int i = 0xAB3400; // hexadecimal

System.out.println(i); // 11219968
```

Na base binaria, comecamos com 0b, e so podemos usar 0 e 1

```
int i = 0b100001011; // binary

System.out.println(i); // 267
```

### Notacao cientifica

Ao declarar doubles ou floats, podemos usar a notacao cientifica

```
double d = 3.1E2;
System.out.println(d); // 310.0;
```

```
float e = 2e3f;
System.out.println(d); // 2000.0;
```

```
float f = 1E4F;
System.out.println(f); // 10000.0;
```

### Usando underlines em literais

A partir do java 7, existe a possibilidade de usarmos underlines (_) quanmdo estamos declarando literais para facilitar a leitura do codigo:

``int a = 123_456_789;``

A mesma regra se aplica a numeros de ponto flutuante.

### Iniciando chars

Os chars sao iniciados colocando o caractere desejado entre aspas simples.

``char c = 'A';``

Mas podemos iniciar numeros tambem. Neste caso, o numero representa a posicao do caracter na tabela unicode:

```
char c = 65;
System.out.println(c); // A
```

### Identificadores

Quando escrevemos nossos programas, usamos basicamente dois tipos de termos para compor nosso codigo: identificadores e palavras reservadas.

Chamamos de identificadores as palavras definidas pelo programador para nomear variaveis, metodos, contrutores, classes, interfaces etc.

Ja as palavras reservadas ou palavras-chave sao termos predefinidos da linguagem que podemos usar para definir comandos(if, for, class, entre outros).

Palavras chaves:
  - abstract
  - assert
  - boolean
  - break
  - byte
  - case
  - catch
  - char
  - class
  - const
  - continue
  - default
  - do
  - double
  - else
  - enum
  - extends
  - false
  - final
  - finally
  - float
  - for
  - goto
  - if
  - implements
  - import
  - instanceof
  - int
  - interface
  - long
  - native
  - new
  - null
  - package
  - private
  - protected
  - public
  - return
  - short
  - static
  - strictfp
  - super
  - switch
  - synchronized
  - this
  - throw
  - trows
  - transient
  - true
  - try
  - void
  - volatile
  - while

### NULL, FALSE E TRUE

Outras tres palavras reservadas que nao aparecem na lista sao **true**, **false** e **null**.

Mas segundo a especificacao da linguagem Java, esses tres termos sao considerados literais e nao palavras reservadas(embora tambem sejam reservadas), totalizando 53 palavras reservadas.

























