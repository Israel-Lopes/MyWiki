# ![certificao_banner](img/certificao_banner.png)

## Certificacao Oracle Java 8

<br />

### Sumario

1. [Defina escopo de variaveis](#defina_escopo_de_variaveis)
2. [Estrutura de uma classe](#estrutura_de_uma_classe)
3. [Crie aplicacoes java com metodo main, rode na linha de comando](#rode_na_linha_de_comando)
4. [Importe outros pacotes](#importe_outros_pacotes_java)

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











