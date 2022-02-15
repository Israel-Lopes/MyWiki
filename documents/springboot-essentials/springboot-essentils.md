# Spring Boot Essentils

O que e Spring boot

SpringBoot e um frameworke que criar aplicaçoes stand alone que voce pode inicializar praticamente sem nenhuma dependencia com uma inicializacao muito rapida em que ele vai tomar conta de quase toda configuracao, com minimo de configuracao possivel.

Ele ja vem com servelet container enbutido, que por padrao e o tomCat. A vantagem de utilizar spring e que ele possui uma integracao muito forte com resto da familia spring, por exemplo: spring Data e spring Cloud, para trabalhar com banco de dados e cloud.

## Gerenciando dependencias sozinho

Para springBoot gerencia as dependencias sozinho, dentro do arquivo pom.xml adicione:

```
<parent>
    <artifactId>spring-boot-stater-parent</artifactId>
    <groupId>org.springframework.boot</groupId>
    <version>2.3.4.RELEASE</version>
</parent>
```

## Criando starter da aplicação

Dentro da pasta principal do projeto, crie a pasta ***start***.

Dentro de start crie o arquivo ***ApplicationStart***, sera isso que ira inicializar nossa aplicação spring.

```
public class ApplicationStart {
    @EnableAutoConfiguration
    @ComponentScan(basePackeges = "academy.dev.springboot")
    public static void main(String[] args) {
        SpringApplication.run(ApplicationStart.class, args);
    }
}
```
 - @EnableAutoConfiguration autoconfigura nossa aplicação criando um bean, apenas com isso ja e possivel inicializar a aplicação.
 - ComponentScan, faz o springboot fazer scaner em outros pacotes. Essa anotação so e utilizada caso o ***AplicationStart*** nao esteja no diretorio padrao do spring.

Outra forma de fazer autoconfiguration e utilizando apenas essa anotação:
```
@SpringBootApplication(exclude = {DataSourceAutoConfiguration.class })
```

## Criando Controller com endpoint

Crie a pasta controller, dentro dela crie o arquivo animeController

```
@RestController
@RequestMapping("animes")
public class AnimeController {

    @GetMapping(path = "list")
    public List<Anime> list() {
        return List.of(new Anime( "DBZ"), new Anime( ""Berserk));
    }
}
```

 - @RestController diz que nosso controller e de uma REST API, que retornara um json.
 - @RequestMapping("anime"), com isso aplicação sera acessado por /anime
 - @GetMapping, faz um GET em /anime/list

## Instancia e Injeção de dependencia

Sequindo o exemplo de uma classe.

```
public class DateUtil {
    public String formatLocalDatetimeDatabaseStyle(LocalDateTime localDateTime) {
        return DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss").format(localDateTime);
    }
}
```

Agora queremos instanciar essa classe. A forma natural de fazer isso seria:

```
private DateUtil dateUtil = new DateUtil();
```

Essa seria a forma tradicional de instancia a classe, porem com a injeção de dependencia, existe uma forma melhor de se fazer e mais segura.

Segue exemplo abaixo:

```
@Autowired
private DateUtil dateUtil;
```

Na classe agora deve se por a anotação ***@Component***, ***@Service*** ou ***@Repository***.

## Hot Swap

Hot Swap faz a atulização da aplicação em tempo real, não precisando reiniciar ela.

Dependencia:

```
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-devtools</artifactId>
</dependency>
```

## Classes service

Classes services sao resposanveis pela regra de negocio, diferente dos controlles que nao recebem regras de negocio. Pode tambem se basear nisso com as anotaçoes, @Service ou @Controller.

## Controller

Basicamente ele dever simples, e tambem onde fica os end-Points

## Como retornar status da requisição

O status da requisição pode ser retornado com ***ResponseEntity();***

```
return new ResponseEntity<>(animeService.listAll(), HttpStatus.OK);
```

## Fazendo POST

```
@PostMapping
@ResponseStatus(HttpStatus.CREATED)
public ResponseEntity<anime> save(@RequestBody Anime anime) {
    return  new ResponseEntity<>(animeService.save(anime));
}
```

## Fazendo GET

```
@GetMapping(path = "/{id}")
public ResponseEntity<Anime> findById(@Pathvariable long id) {
    return ResponseEntity.ok(animeService.findById(id));
}
```

## Fazendo DELETE

```
@DeleteMapping(path = "/{id}")
public ResponseEntity<Void> delete(@Pathvariable long id) {
    animeService.delete(id);
    return new ResponseEntity<>(HttpStatus.NO_CONTENT));
}
```

## Fazendo PUT

```
@PutMapping
public ResponseEntity<Void> replace(@RequestBody Anime anime) {
    animeService.replace(anime);
    return new ResponseEntity<>(HttpStatus.NO_CONTENT));
}
```

## Instalando Docker na aplicação

A primeira etapa e criar um arquivo dentro da aplicação do projeto no diretorio raiz, arquivo chamara ***docker-compose.yml***.

Dentro do arquivo, escreva:

```
version: '3.1'
services:
  db:
    image: mysql
    container_name: mysql
    environment:
      MYSQL_ROOT_PASSWORD: root
    ports:
    - "3306:3306"
    volumes:
    - devdojo_data:/var/lib/mysql

volumes:
  devdojo_data:
```

Agora basta executar: ``docker-compose up ``

Dependencias necessarias do JPA:

```
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-data-jpa</artifactId>
</dependency>

<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
</dependency>
```

Proximo passo agora e configurar a aplicação no aplication. Dentro da pasta resource, crie o arquivo ***application.yml***, dentro dele digite:

```
server:
  error:
    include-stacktrace: on_param

spring:
  datasource:
    url: jdbc:mysql://localhost:3306/anime?createDatabaseIfNotExist=true
    username: root
    password: root
  jpa:
    hibernate:
      ddl-auto: update
```

Caso nao funcione, pode ser feito dessa forma tambem, crie o arquivo aplication.properties e colo que dentro:

```
spring.datasource.url=jdbc:mysql://localhost:3306/news?createDatabaseIfNotExist=true
spring.datasource.username=root
spring.datasource.password=root
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
spring.jpa.database-platform = org.hibernate.dialect.MySQL5Dialect
spring.jpa.generate-ddl=true
```

Agora devemos transformar nosso dominio em uma entidade do banco. 

Para isso ulizaremos as sequintes anotaçoes:

 - @Entity
   - Quando colocada avera erro pois necessitara de fazer um construcor, para isso utilizase @NoArgsConstructor 
 - @NoArgsConstructor
 - @Id
 - @GeneratedValue

```
@Data
@AllArgsConstructor
@NoArgsConstructor
@Entity
public class Anime {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String name;
}
```

## Conectando as classes ao JPA

Na interface do repository vamos extender de ***JpaRepository<Anime, Long>***

```
public interface AnimeRepository extends JpaRepository<Anime, Long> {
}
```

Na classe de service, AnimeService, vamos adiconar:

``private final AnimeRepository animeRepository;``

Vamos tambem colocar a anotaçao ***@RequiredArgsConstructor***, para spring fazer a injeção de dependencia do ***AnimeRepository***.

```
@Service
@RequiredArgsConstructor
public class AnimeService {

    private final AnimeRepository animeRepository;
```

## Request Params

Agora vamos adicionar parametros na request. Para isso adicione em ***AnimeRepository***:

``List<>Anime findByName(String name);``

Ficando assim.

```
public interface AnimeRepository extends JpaRepository<Anime, Long> {
    List<>Anime findByName(String name);
}
```

findByName e uma referencia ao atributos ***name*** que tem na classe ***Anime***.

```
@Data
@AllArgsConstructor
@NoArgsConstructor
@Entity
public class Anime {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String name;
}
```

Agora em Anime Service deve colocar:

```
public List<Anime> findByName(String name) {
    return animeRepository.findByName(name);
}
```

Para terminar agora iremos em ***AnimeController*** e adicionaremos:

```
@GetMapping(path = "/find")
public ResponseEntity<List<Anime>> findByName(@RequestParam String name) {
    return ResponseEntity.ok(animeService.findByName(name));
}
```
 - @ResquestParam e obrigatorio. Com ele podemos passar nome como parametro e nao um id, como antes demostrado.

Forma correta do parametro na URL:

``http://localhost:8080/animes/find?name=steins gate``

## Execeções Customizadas

Para criar uma exeção customizadas, crei dentro do projeto crie pasta ***execption***.

Agora crie a classe ***BadRequestExcption***.

```
@ResponseStatus(HttpStatus.BAD_REQUEST)
public class BadRequestExcption extends RuntimeException {
    public BadRequestExcption(String message) {
        super(message);
    }
}
```

Com essa anotação, ele sempre ira retornar o status HTTP da bad request.

Dentro da classe ***AnimeService***, vamos usar nossa exeção. Onde avia retorno de ***ResponseStatusException***, sera trocado pela nova exeção, ficando assim:

Antes

```
new ResponseStatusException(HttpStatus.BAD_REQUEST, "Anime not found"));
```

para

```
new BadRequestException("Anime not found"));
```

19




























