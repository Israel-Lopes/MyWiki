# Curso de JUnit e Mockito

## Assertivas

### AssertTrue

AssertTrue, recebe como parametro um booleano. Essa e a mais simples de toda.

Ele verifica se a expressao e verdadeira, ***true***.

Recomendase utilizar o minimo de espressoes negativas.

```
Assert.assertTrue(true);
```

### AssertFalse

Valida se a expressao e ***false***.

```
assertFalse(false);
```

### AssertEquals

O funcionamento dele e bem simples, ele valida se o valor esperado e iqual ao atual.

```
assertEquals(esperado, atual);
```

Para utilizar Equals para comparar casas decimais, se utiliza o delta de comparação. 

O delta seria uma margem de erro para comparação.

```
assertEquals(esperado, atual, delta);
```

Exemplo:

```
assertEquals(0.51, 0.51, 0.01);
```

### AssertThat

Basicamente AssethThat significa, verifique que.

No assertThat e o inverso do assertEqual, o primeiro valor
e o atual, o segundo eo match.

Aqui esta verificando se o valor esperado e igual a 5.0
```
asserthThat(locacao.getValor(), CoreMatchers.is(5.0));
```

Outra forma de fazer

```
assethThat(locacao.getValor(), is(equalsTo(5.0)));
```

Negação. Verifique que valor da negação, nao e 6.

```
assethThat(locacao.getValor(), is(not(6.0)));
```

Com Data. Verifica se a data e verdadeira.

```
assethThat(locacao.getValor(), new Date(), is(true));
```

O ideal e que para cada teste tenha uma assertiva.

### Rule

Com rule voce pode fazer varios testes e um so, perdendo assim a necessidade de dividir os testes.

Exemplo:

```
@Rule
public ErrorCollector erro = new ErrorCollector();

erro.checkThat(locacao.getValor(), is(equalsTo(6.0)));
erro.checkThat(isMesmaData(locacao.getDataLocacao(), new Date()), is(true));
```

Nesse exemplo acima, diferente de um AssethThat, ele ira chegar um a um mesmo que ocorra falhas.

### Garantindo que nao a falhas

```
@Rule
public ErroCollector error = new ErroCollector();


@Test
public void testeLocacao() {

    // cenario 
    LocacaoService service = new LocacaoService();
    Usuario usuario = new Usuario("Usuario !");
    Filme filme = new Filme("Filme 1", 2, 5.0);

    //Acao
    try {
        service.alugarFilme(usuario, filme);
        Assert.fail("Deveria ter lancado uma execao");

    } cathc (Exception e) {
        assertThat(e.getMessage(), is("Filme sem estoque"));
    }

}
```

Para garantir que um teste passe e nao tenha falhas, podera ser criado um try catch  com ***Assert.fail***.

A maneira mais segura de se trabalhar com execoes e com try catch.

Outra forma de trabalhar com execoes.

```
@Rule
public ExpectedException execption = ExpectedException.none();



@Test
public void testeLocacao() {

    // cenario 
    LocacaoService service = new LocacaoService();
    Usuario usuario = new Usuario("Usuario !");
    Filme filme = new Filme("Filme 1", 2, 5.0);

    //Acao
    service.alugarFilme(usuario, filme);

    exception.expect(Excption.class);
    exception.expectMessage("Filme sem estoque");

}
```

Outra forma tambem e com expected. No cabecalho do metodo, dentro da anotacao @Test. Assim ele ira capturar a excption descrita la.

```
@Test(expected = FilmeSemEstoqueException.class)
public void testeLocacao() throws Exception {
```

Outra forma de testar e verificando as mensagens lancadas.

```
if (filme == null) {
    throw new LocadoraException("Usuario vazio");
}
```

Aqui ira capturar a mensagem quando execao for lancada:

```
exception.expect(LocadoraException.class);
exception.expectMessage("Usuario vazio");
```

### Before e After

Existem duas anotaçoes que me permiter por blocos de codigos para serem executadas antes e apois cada teste.

Primeira delas e ***@Before***. Com ele e possivel que ele seja executado primeiro, antes do teste. Segue o exemplo a baixo.

```
@Before
public void setup() {
    System.out.println("before");
}
```

Outro e o ***@After***, ele e executado apos cada teste.

```
@After
public void setup() {
    System.out.println("after");
}
```

O @Before e @After e executado um a um para cada teste, repeditas vezes.

Um exemplo de utilizacao do @Before, seria para inicializar classes comuns entre os teste. Exemplo a abaixo.

```
private LocacaoService service;

@Before
public void setup() {
    service = new LocacaoService();
}

```

Outra maneira tambem de inicializar e com ***BeforeClass*** e ***AfterClass***, que e inicializado depois e antes da classe ser inicializada ou finalizada. A implentacao deles e semelhante ao ***Before***, porem metodo contendo essa anotacao tem que ser static.

```
@BeforeClass
public static void setup() {
    System.out.println("before class");
}
```
OBS: Variaveis do tipo estatica no escopo da classe o JUnit nao reinicializa.

### Executando testes em ordem

Para executar os testes em ordem, deve ser criar os metodos sem a anotacao @Test. Com isso criase um teste geral para rodar. Segue exemplo abaixo.

```
public static contador = 0;

public void inicia() {
    contador = 1;
}

public void verifica() {
    Assert.assertEqual(1, contador);
}

@Test
public void testGeral() {
    inicia();
    verifca();
}
```

Dessa forma e garantido que metodo inicia() sera executado primeiro e depois verifica().

Existe uma outra forma de se fazer isso, que e a maneira mais adequada que e com anotacao @FixMethodOrder(), que e utilizada no cabecalho da classe.

```
@FixMethodOrder(MethodSorters.NAME_ASCENDING)
public class OrdemTest() {

public static contador = 0;

@Test
public void t1_inicia() {
    contador = 1;
}

@Test
public void t2_verifica() {
    Assert.assertEqual(1, contador);
}
```

Nesse exemplo os metodos de teste foram executados em ordem alfabetica, porem existem outras maneiras de definir essa rodem de execução.

### @Ignore e Assumptions

Com @Ignore, poderomso ignorar testes indesejados.

```
@Test
@Ignorer
public void deveriaTestar() {

    }
```

Outra forma e utilizando o Assumptions, exemplo de sua utilizacao e definir que o teste so seria executado em um sabado.

```
@Test
public void deveriaTestar() {
    Assume.assumeTrue(DataUtils.verifcarDiaSemana(new Date(), Calendar.SATURDAY));
    }
```

### Testes parametrizados

O Junit fornece uma forma de paremitrizar os teste, que se chama parametrizer, com ele e possivel reduzir a quantidade de linha de codigo repetido dos testes.

Para inicializarmos o parameteride, devemos colocalo do topo da classe sendo ele ***@RunWith(Parameterized.class)***. Dessa forma o JUnit ja sabe que o teste dessa classe sera parametrizado.

Proximo passo agora e definir o conjunto de dados que sera testado. No metodo ***getParametros***, que sera a fonte de dados, devemos informar isso para JUnit. Para isso devemos utilizar a anotacao ***@Parameters***, nao se esquesa que e no plural.

OBS: O metodo do parameters sempre deve ser ***statci***.

Proximo passo agora e definir o link das variaves que sao usadas no metodo getParametros, sao elas ***filmes*** e ***valorLocacao***.

OBS: Essas variaveis devem ser publicas, caso contrario dara erro de acesso.

```
@RunWith(Parameterized.class)
public class CalculoValorLocacaoTest {

    private LocacaoService service;

    @Parameter
    public List<Filme> filmes;

    @Parameter(value=1)
    public Double valorLocacao;

    @Before
    public void setup() {
        service = new LocacaoService();
    }

    private static Filme filme1 = new Filme("Filme 1", 2, 4.0);
    private static Filme filme2 = new Filme("Filme 2", 2, 4.0);
    private static Filme filme3 = new Filme("Filme 3", 2, 4.0);
    private static Filme filme4 = new Filme("Filme 4", 2, 4.0);
    private static Filme filme5 = new Filme("Filme 5", 2, 4.0);
    private static Filme filme6 = new Filme("Filme 6", 2, 4.0);

    @Parameters
    public static Collection<Object[]> getParametros() {
        return Arrays.asList(new Object[][] {
            {Arrays.asList(filme1, filme2, filme3), 11.0},
            {Arrays.asList(filme1, filme2, filme3, filme4), 13.0},
            {Arrays.asList(filme1, filme2, filme3, filme4, filme5), 14.0},
            {Arrays.asList(filme1, filme2, filme3, filme4, filme5, filme6), 14.0}
        });
    }

    @Test
    public void deveCalcularValorLocacaoConsiderandoDescontos() throws FilmeSemEstoqueException, LocadoraException {

        //Cenario
        Usuario usuario = new Usuario("Usuario 1");

        //Acao
        Locacao resultado = service.alugarFilme(usuario, filmes);

        //Verificacao
        assertThat(resultado.getValor(), is(valorLocacao));
    }
}
```



18