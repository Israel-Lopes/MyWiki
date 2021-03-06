# ![certificao_banner](img/certificao_banner.png)

## Certificacao Oracle Java 8

<br />

### Sumario

1. [Defina escopo de variaveis](#defina_escopo_de_variaveis)
2. [Estrutura de uma classe](#estrutura_de_uma_classe)
3. [Crie aplicacoes java com metodo main, rode na linha de comando](#rode_na_linha_de_comando)
4. [Importe outros pacotes](#importe_outros_pacotes_java)
5. [Declarar e inicializar variaveis](#declarar_e_inicializar_variaves)
6. [Diferenca entre variaveis de referencia a objetos e tipos primitivos](#diferenca_entre_variaveis)
7. [Usando operadores e construcoes de decisao e Arrys](#operadores_construcoes)
8. [Usando lacos](#usando_lacos)

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

??$ javac nomeDoArquivoComMetodoMain.java??

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
   Basta seguir as opcoes do SO em questao a definir a variavel. Isso e considerado uma m?? pratica no dia a dia porque e um classpath global, que vai valer para qualquer programa java executando na maquina.

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

<br />

### Diferenca entre variaveis de referencia a objetos e tipos primitivos <a name="diferenca_entre_variaveis">

As variaveis de tipos primitivos de fato armazenam os valores (e nao ponteiros/referencias). Ao se atribuir o valor de uma variavel primitiva a uma outra variavel, o valor de uma variavel primitiva a uma outra variavel, o valor e copiado, e o roiginal nao e alterado.

```
int a = 10;
int b = a;
b++;
System.out.println(a); // Continua com 10.
```

Os programas contruidos com o modelo orientado a objetos utilizam evidentemente, objetos. Para acessar um atributo ou invocar um metodo de qualquer objeto, e necessario que tenhamos armazenar uma referencia para o mesmo.

Uma variavel de referencia e um ponteiro para o endreco de memoria onde o objeto se encontra. Ao atribuirmos uma variavel de  referencia a outra, estamos copiando a referencia, ou seja, fazendo com que as duas variaveis apontem para o mesmo objeto, e nao criando um novo objeto:

```
class Carro {
  int ano;
}

class Test {
  public static void main(String[] args){
    Carro a = new Carro();
    Carro b = a; // Agora (b) aponta para o mesmo objeto de (a)
    
    a.ano = 5;
    
    System.out.println(b.age); // Imprime 5
  }
}
```

Duas referencias sao consideradas iguais somente se elas estao apontando para o mesmo objeto. Mesmo que os objetos que elas apontem sejam iguais, ainda sao referencias para objetos diferentes:

```
Carro a = new Carro();
a.ano = 5;

Carro b = new Carro();
b.ano = 5;

Object c = a;

System.out.println(a == b); // false
System.out.println(a == c); // true
```

### Leia ou escreva para Campos de objetos

Ler e escrever propriedades em objetos e uma das tarefas mais comuns em um programa java. Para acessar um atributo, usamos o operador .(ponto), junto a uma varivel de referncia para um objeto:

```
class Carro {
  String model;
  int year;
  
  public Carro() { year = 2014; }
  
  public String getData() {
    return model + " - " + year;
  }
  
  public void setModel(String m) {
    this.model = m;
  }
}
```

### Explique o ciclo de vida de um objeto (criacao, "de referencia" e garbage collection)

O ciclo de vida dos objetos java esta dividido em tres fases distintas.

#### Criacao de objetos

Toda vez que usamos o operador new, estamos criando uma nova instancia de um objeto na memoria:

```
class Pessoa {
  String nome;
}

class Test {
  public static void main(String[] args) {
    Pessoa p = new Pessoa(); // Criando objeto do tipo Pessoa.
  }
}
```

Repare que ha uma grande diferenca entre criar um objeto e declarar uma variavel. A variavel e apenas uma referencia, um ponteiro, nao contem um objeto de verdade.

```
// Apenas declarando a variavel, nenhum objeto foi criado.
Pessoa p;

// Agora um objeto foi criado e atribuido a variavel.
p = new Pessoa();
```

#### Objeto acessivel

A partir do momento em que um objeto foi criado e atribuido a uma variavel, dizemos que o objeto esta acessivel, ou seja, podemos usa-lo em nosso programa:

```
Pessoa p = new Pessoa(); // Criando.
p.nome = "Joao"; // inserindo.
```

#### Objeto inacessivel

Um objeto e acessivel enquanto for possivel "alcancar-lo" atraves de alguma referencia direta ou indireta. Caso nao exista nenhuma caminho direto ou indireto para acessar esse objeto, ele se torna inacessivel:

```
Pessoa p = new Pessoa();
p.nome = "Joao";

// Atribuimos a (p) o valor null, agora objeto nao esta mais acessivel.
p = null; // A

// Criando objeto sem variavel.
new Pessoa(); // B
```

Nesse codigo, criamos um objeto do tipo **Pessoa** e o atribuimos a variavel (p). Na linha **A** atribuimos (null) a (p). O que acontece com objeto anterior? Ele simplismente nao pode mais ser acessado por nosso programa, pois nao temos nenhum ponteiro para ele. O mesmo pode ser dito do objeto criado na linha **B**. Apos essa linha, nao conseguimos mais acessar esse objeto.

Tome cuidado: se a prova perguntar quantos objetos foram criados no codigo acima, temos a criacao de duas pessoas em uma  String, totalizando tres objetos

Outra maneira de ter um objeto  inacessivel e quando o escopo da variavel que aponta para ele terminar.

#### Garbage Collection

Todo objeto inacessivel e considerado elegivel para o garbage collector. Algumas questoes da prova perguntam quantos objetos sao elegiveis ao garbage collector ao final de algum trecho de codigo.

```
public class Bla {
  int b;
  public static void main(String[] args) {
    Bla b;
    for (int i = 0; i < 10; i++) {
      b = new Bla();
      b.b = 10;
    }
    System.out.println("end"); // A
  }
}
```

Ao chegar na linha A, temos 9 objetos elegiveis do tipo Bla para o Garbage Collector.

### Objetos elegiveis X Objetos coletados

O garbage collector roda em segundo plano juntamente com sua aplica????o java. Nao e possivel prever quando ele sera executado, portanto nao se pode dizer com certeza quantos objetos foram efetivamente coletados em um certo ponto da aplica????o. O que podemos determinar e quantos objetos sao elegiveis para a coleta. A prova pode tentar se aproveitar do descuido do desenvolvedor aqui numca temos certeza de quantos objetos sao elegiveis para a coleta. A prova pode tentar se aproveitar do descuido do desenvolvedor aqui: numca temos certeza de quantos objetos passaram pelo garbage collector, logo, somente indique quantos estao passiveis de serem coletados.

```
import java.util.*

class Car {

}
class Cars {
  List<Car> all = new ArrayList<Car>();
}

class Test{
  public static void main(String args[]){
    Cars cars = new Cars();
    for (int i = 0; i < 100; i++ ){
      cars.all.add(new Car());
      // ate essa linha todos ainda podem ser alcan??ados
    }
  }
}
```
Nesse codigo, por mais que tenhamos criado 100 carros e um objeto do tipo Cars, nenhum dels pode ser garbage coletado pois todos podem ser alcan??ados direta ou indiretamente atraves de nossa ***thread*** principal.

### Argumentos variaveis: varargs

A partir do Java5, varargs possibilitam um metodo que recebe um numero variavel(nao fixo) de parametros. E a maneira de receber um array de objetos e possibilitar uma chamada mais facil do metodo.
Podemos chamalo com qualquer numero de argumentos:

```
class Calculator {
 public int sum(int... nums) {
  int total = 0;
  for (int a : nums) {
    total += a;
  }
  return total;
 }
}
```

### Manipule dados usando a classe String-Builder e seus metodos

Para suportar Strings mutaveis, o Java possui as classes StringBuffer e StringBuilder. A operacao mais basica e o append que permite concatenar ao mesmo objeto:

```
StringBuffer sb = new StringBuffer();
sb.append("Certificacao");
sb.append(" - ");
sb.append("Oracle");

System.out.println(sb); // Certificacao - Oracle
```

Repare que o ***append*** nao devolve novos objetos como em ***String***, mas altera o proprio StringBuffer, que e mutavel.

Quando fazemos concatenacao de String usando o +, por de baixo dos panos, e usado um StringBuilder. Nao existe a operacao + na classe String. O compilador troca todas as chamadas de concatenacao por StringBuilders(podemos ver isso no bytecode compilado).

### Principais metodos de StringBuffer e StringBuilder

Ha a familia de metodos append com overloads para receber cada um dos primitivos, String, arrays de chars, outros StringBuffer etc. Todos eles devolvem o proprio StringBuffer/Builder o que permite chamadas encadeadas:

```
StringBuffer sb = new StringBuffer();
sb.append("certificacao").append(" - ").append("Oracle");
system.out.println(sb);
```

O metodo append possui umja versao que recebe Object e chama o meotodo toString de seu objeto.

Ha ainda os metodos ***insert*** para inserir coisas no meio. Ha versoes que recebem primitivos, String, arrays de char etc. Mas todos tem o primeiro argumento recebendo o indice onde queremos inserir:

```
Stringbuffer sb = new StringBuffer();
sb.append("certificacao - Oracle");
sb.insert(9, "Ensino");

System.out.println(sb); // Certificacao - Ensino
```

Para converter um ***StringBuffer/Bui8lder*** em ***String***, basta chamar o ***toString*** mesmo. O metodo ***reverse*** inverte seu conteudo:

```System.out.println(new StringBuffer("guilherme").reverse());```

Fora esses, tambem ha o ***trim***, ***charAt***, ***length()***, ***equals***, ***indexOf***, ***lastIndexOf***, ***substring*** nao altera o valor do seu ***StringBuilder*** ou ***StringBuffer***, mas retorna a ***String*** que voce deseja. Existe tambem o metodo ***subSequence*** que recebe o inicio e o fim e funciona da mesma maneira que o ***substring*** com dois argumentos.

### Criando e manipulando Strings

Existem duas maneiras tradicionais de criar uma ***Strings***, uma implicita e outra explicita:

```
String implicit = "Java";
String explicit = new String("Java"); 
```

A comparacao entre esses dois tipos de criacao de ***Strings*** e feita na seccao ***Test quality between strings and other object using == and equals() 5.3***

Existem outras maneiras nao comuns, como atravez de uma array:

```
char[] name = new char[] {'J', 'a', 'v', 'a'};
String fromArray = new String(name);
```

Ou ainda podemos criar uma ***String*** baseada em um ***StringBuilder*** ou ***StringBuffer***:

```
StringBuilder sb1 = new StringBuilder("Java");
String name Builder = new String(sb1);

StringBuffer sb2 = new StringBuffer("Java");
String nameBuffer = new String(sb2);
```

Como uma String nao e um tipo primitivo, ela pode ter valor ***null***, lembre se disso:

```
String name = null; // explicit null
```

Podemos concatenar ***Strings*** com o +;

```
String name = "Java" + "Exam";
```

Caso tente concatenar ***null*** com uma ***String***, temos a conversao de ***null*** para ***String***:

```
String nulled = null;
System.out.println("value:" + nulled); // value: null
```

E o contrario tambem tem o mesmo resultado:

```
String nulled = null;
System.out.println(nulled + "value"); // null value
```

O java faz conversao de tipos primitivos para ***Strings*** automaticamente:

```
String name = "Java" + ' ' + "Certification" + ' ' + 1500;
System.out.println(name); // Certification java 1500
``` 

Lembre se da precedencia de operadores. O exemplo a seguir mostra o codigo sendo interpretado da esquerda pra direita(primeiro a soma);

```
String value = 15 + 00 + "certification";
System.out.println(value); // 15 certification
```

### Strings sao imutaveis

O principal ponto sobre Strings e que elas sao imutaveis:

```
String s = "java";
s.toUpperCase();
System.out.println(s);
```

Esse codigo imprime ***java*** em minusculo. Isso porque o metodo ***toUpperCase*** nao altera a ***String***  original. Na verdade, se olharmos o javadoc da classe ***String*** vamos perceber que todos os metodos que parecem modificar uma String na verdade devolvem uma nova.

```
String s = "java";
String s2 = s.toUpperCase();
system.out.println(s2);
```

Agora sim imprimira ***JAVA***, uma nova ***String***. Ou, usando a mesma referencia:

```
String s = "java";
s = s.toUpperCase();
system.out.println(s);
```

Para tratarmos de "strings mutaveis", usamos as classes ***StringBuffer*** e ***StringBuilder***.

Lembre se que a ***String*** possui um array por tras e, seguindo o padrao do Java, suas posicoes comecam em 0;

```
// 0=g, devolve 'g'
char caracter0 = "guilherme".charAt(0);

// 0=g 1=u, devolver 'u'
char caracter1 = "guilherme".charAt(1);

// 0=g 1=u 2=i, devolve 'i'
char character2 = "guilherme".charAt(2);
```

Cuidado ao acessar uma posicao indevida, voce pode levar um ***StringIndexOutOfBoundsException*** (atencao ao nome da ***Exception***, nao e ***ArrayindexOutofBoundsException***).

### Principais metodos de String 

O metodo ***length*** imprime o tamanho da ***String***:

```
String s = "Java";
System.out.println(s.length()); // 4
```

Ja o metodo ***isEmpty*** diz se a ***String*** tem tamanho zero:

```
System.out.println("".isEmpty()); // true
System.out.println("Java".isEmpty()); // false
System.out.println(" ".isEmpty()); // false
```

Devolve uma nova String:

 - ***String toUpperCase()*** tudo em maisculo;
 - ***String toLowerCase()*** tudo em minusculo;
 - ***String trim()*** retira espacos em branco no comeco e no fim;
 - ***String substring(int beginIndex, int endIndex)*** devolvera substring a partir do indice passado ate o final da String;
 - ***String concat(String)*** concatene o parametro ao fim da String atual e devolve o resultado;
 - ***String replace(char oldChar, char newchar)*** substitui todas as ocorrencias de determinado ***char*** por outro;
 - ***String replace(CharSequence target, charSequence replacement)*** substitui todas as ocorrencias de determinada ***CharSequence*** (como String) por outra.
 
 O metodo ***trim*** limpa caracteres em branco nas duas pontas da ***String***.
 
 O metodo ***replace*** substituira todas as ocorrencias de um texto por outro.
 
 Para extrair peda??os de uma ***String***, usamos o metodo ***substring***. Cuidado ao usar o metodo ***substring*** com valores invalidos, pois eles jogam uma ***Exception***. O segredo do metodo ***substring*** e que ele nao inclui o caracter da posicao final, mas inclui o caractere da posicao inicial.

<br />

### Usando operadores e construcoes de decisao e Arrys<a name="operadores_construcoes">

Para manipular os valores armazenados das variaveis, tanto as primitivas quanto as nao primitivas, a linguagem de programacao deve oferecer operadores. Um dos operadores mais importantes e o que permite guardar um valor em uma variavel. Esse operador e denominado **operados de atribuicao**.

### Pool de Strings

O Java mantem um pool de objetos do tipo ***String***. Antes de criar uma nova String, primeiro o java verifica neste pool se uma String com mesmo conteudo ja existe; caso sim, ele a reutiliza, evitando criar dois objetos exatamente iguais na memoria. Como as duas referencias estao apontando para o mesmo objeto do pool, o == retorna ***true***.

### Unreachable Code e Missing return

Um codigo Java nao compila se o compilador perceber que aquele codigo nao sera executado sob hipotese alguma.

### Declare, instancie, inicialize e use um array multidimencional

Podemos generalizar a ideia de array para construir array de duas dimensoes, em outras palavras, array de arrays. Analogicamente, podemos definir arrays de quantas dimensoes quisermos.

```
// Array de duas dimencoes.
int [][] table;

// Array de tres dimensoes
int [][] cube[];

// Array de quatro dimensoes
int[] [][]hipercube[];
```

Perceba que as dimensoes podem ser definidas do lado esquerdo ou direito da variavel.

**Inicializacao**

Podemos inicializar as arrays com dimensoes diferentes, como no caso a seguir onde inicializarmos a primeira dimensao com 10 e a segunda com 15:

```
int [][] table = new int[10][15];
```

Podemos tambem inicializar somente a primeira dimensao, deixando as outras para depois:

```
int [][][] cube = new int [10][][];
```

Podemos inicializar diretamente com valores que conhecemos, e nesse caso colocamos todas as dimensoes:

```
int [][] test = new int [][]{{1,2,3}, {3,2,1}, {1,1,1}};
```

### Interator e o enhanced for

A interface ***Interator*** define uma maneira de percorrer colecoes. Isso e necessario porque, em colecoes diferentes de ***List***, nao possuimos metodos para pegar o enesimo elemento. Como, entao, percorrer todos os elementos de uma colecao?

 - ***hasNext***: retorna um booleano indicando se ainda ha elementos a serem percorridos por esse iterator;
 - ***next***: pula para o proximo elemento, devolvendo-o;
 - ***remove***: remove o elemento atual da colecao.
 
 Normalmente o codigo que costuma aparecer para percorrer uma colecao e o seguinte:
 
 ```
 Collection<String> strings = new ArrayList<String>();
 Interator<String> interator = string.iterator();
 while (iterator.hasNext()) {
  String current = interator.next();
  System.out.println(current);
 }
 ```
 
 O ***enhanced-for*** tambem pode ser usado nesse caso:
 
 ```
 Collection<String> strings = new ArrayList<String>();
 for (String current : strings) {
  System.out.println(current);
 }
 ```
 
 ### O metodo equals em colecoes
 
 A maoria absoluta das colecoes usa metodo ***equls*** na hora de buscar por elementos, como nos metodos ***contains*** e ***remove***. Se voce deseja ser capaz de remover ou buscar elementos, tera que provavelmente sobrescrever o metodo ***equals*** para refletir o conceito de iqualdade em que esta interrassado, e nao  somente  a igualdade de referencia(implementacao padrao do metodo). Cuidado  ao tentar sobrescrever o metodo ***equals***, se voce escrever lo recebendo um tipo especifico em vez de ***Objeto***, nao o estara sobrescrevendo, a o ***ArrayList*** continuara invocando o codigo antigo, a implementacao padrao de ***equals***.
 
 <br />

### Usando lacos<a name="usando_lacos">















