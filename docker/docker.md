# ![docker_banner](img/docker_banner.png)

`root@terminal:~# docker container run hello-world`

Existem duas formas de executar container.
  - Modo daimon, que roda em background.
  - Modo interativo.

`root@terminal:~# docker container run debian`

  - Baixando imagem debian e executando.

`root@terminal:~# docker container ps`

  - Lista quais sao containers ativos.
  - A opcao "-a" lista todos os containers, mesmo a queles que estao parados.

`root@terminal:~# docker container run --rm debian`

 - Executa o container e ao final da execucao ele deleta o container da lista.
 
 `root@terminal:~# docker container run -it debian bash`
 
  - Executa o container e entra no modo interativo do bash.
  
Containers devem ter nomes unicos.

`root@terminal:~# docker container run --name mydebian -it debian bash`

  - Cria um novo container nomeado por mydebian apartir da imagem debian.

`root@terminal:~# docker container start -ai mydebian`

  - Reutilizacao de container
  - "-ai", atocha um terminal de forma interativa
  
<br />

O docker engine tem diversos mecanismos para conseguir fazer isolamento de uma forma segura do seu container com a maquina host. 

Entretanto nao faz sentido termos um container completamente isolado, o que queromos na verdade e termos um isolamento controlado.

Por isso e importante que compartilhermos algumas coisas.

  Comunicao dos containers ex:
  
  - Uma porta, para que alguem consiga acessar um servico.
  - Compartilha uma pasta entre a maquina host e o seu container.
  - Copiar arquivos para o container, ou da maquina host para container.
  - Outra forma de comunicao seria entre os proprios containes. Uma aplicacao sendo configurada em multiplos containers.
  
### Como mapear as portas dos containers

Vamos instalar um servidor chamdo **nginx**, mapeando a porta 8080

`root@terminal:~# docker container run -p 8080:80 nginx`

  - A opcao "-p" e para fazer o mapeamento.
  - A primeira porta 8080, e a porta que vai ser exposta para fora do container.
  - Porta 80 e porta interna do container a qual ele sera startado por padrao.
  - nginx e a imagem a qual sera baixada.
  
`root@terminal:~# curl http://localhost:8080`
  
![retorna_pagina_nginx](img/retorna_pagina_nginx.png)

   - Aqui ira retornar a pagina.



Como mapear um volume

