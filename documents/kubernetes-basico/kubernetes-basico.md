![banner](img/banner-kunbernetes.png)

[Material de referencia](https://www.youtube.com/watch?v=5unI7VPnASM&t=6138s)

O kubernetes e um orquestrador de container. Vendo a necessidade de alta escalabilidade, o kubernetes se ve necessario, imagine a situação de ter que gerenciar muitos containers docker, o kubernetes faz isso por voce.

## Configmap

Configmap e um arquivo que injeta dados de configuração no container.

Basicamente o configmap e um unico arquivo de configuração para mais de um container, facilitando para que nao tenha a necessidade de configurar os containers de um a um.

## Secrets

A secret salva senha no kubernetes e recupera ela dentro do container.

## Load Balancer

Load balancer e um balanceador de carga. Ele equilibra o nivel de carga entre os containers para que nao fiquem sobrecarregados.

## Service Discovery

O service discovery tem um registro de todos os containers e junto com o load balance ele delega para qual container ira a massa de dados, sua prioridade e o container que estiver mais saudavel.

## POD

POD e uma unidade, um envolucro que sela um container, ou seja o POD ele envolve um container e sela ele. Por padrao um POD sempre tera um container dentro, mas pode aver casos exepcionais em que se tem mais de um container dentro de uma POD, mas isso nao e aconselhavel fazer.

O POD ele verifica se o container esta com qualidade o sulficiente para rodar o container.

```
    POD           
    .________________.
    |                |
    |    Container   |
    |________________|                                                
```

## ReplicaSet

O replicaset monitora a todo tempo a quantidade de POds que estao no ar.

O replicaSet pode ser configurado por exemplo para o tempo todo esta rodando dois PODs, caso um POD morra, o replicaSet ira replicar esse POD novamente do zero.

O replicaSet tambem quarda a versao do container. 

```
ReplicaSet
._____________________________________________________.
|   POD                          POD                  |
|   .________________.           .________________.   |
|   |                |           |                |   |
|   |  |Container|   |           |   |Container|  |   |
|   |________________|           |________________|   |
|                                                     |
|_____________________________________________________|
```
## Deployment

Por de cima do replicaSet temos o deployment. O deployment ele garante qe consiga gerar uma nova versao, garante tambem o replicaSet, ele tem por de dentro o replicaSet que garante a quantidade de replica de PODs.

```
Deployment
._________________________________________________________________.
|    ReplicaSet                                                   |
|    ._______________________________________________________.    |
|    |                                                       |    |
|    |   POD                          POD                    |    |
|    |   .________________.           .________________.     |    |
|    |   |                |           |                |     |    |
|    |   |   |Container|  |           |   |Container|  |     |    |
|    |   |________________|           |________________|     |    |
|    |                                                       |    |
|    |                                                       |    |
|    |_______________________________________________________|    |
|_________________________________________________________________|
```

## Service

```
Deployment
._____________________________________________________.
| ReplicaSet                                          |
| ._________________________________________________. |
| |                                                 | |
| |  POD                         POD                | |
| |  .________________.          .________________. | |     ._________.
| |  |                |          |                | | |     |         |
| |  |   |Container|  |          |   |Container|  | | | --> | Service |
| |  |________________|          |________________| | |     |_________|
| |                                                 | |
| |                                                 | |
| |_________________________________________________| |
|_____________________________________________________|
```

O service ele possibilita que outras pessoas ou sistemas acessem o deployment, conseguentemente acesso aos PODs. Ele fica de forma externa em relação a o deployment.

No service e feito uma configuração apartir de uma label chamda ***selector***.

Exemplo disso e que a selector pode ser chamda de ***app:front*** ou ***app:back***. Dessa forma podemos diversificar o selector para uma aplicação front end ou back end por exemplo.

OBS: Cada deployment tera o seu service.

Utilizando o service, existe algumas possibilidades:

 - Gerar um ip interno.
 - Gerar um ip externo, para acesso externo.
 - Disponibilizar uma porta.

***Round-robin*** e um algoritimo de randomização que trabalha em conjunto com service.

## Rodando kubernetes local com kind

O kind simula um cluster kubernetes utilizando o docker da maquina local.

Para criar cluster com klind:

``klind create cluster --name=meuprimeirocluster``

Mostra os nodes:

``kubectl get nodes``

Mostra os pods:

``kubectl get pods``

Mostra os services:

``kubectl get services``

Crie agora o arquivo ***server.go***, dentro dele digite:

```
package main

func main() {

    http.HandleFunc("/", Home)
    http.ListenAndServe(":3000", nil)
}

func Home(w http.ResponseWriter, r *http.Request) {
    w.Write([]byte("<h1>Ola mundo!</h1>"))
}
```

Agora para rodar:

``go run server.go``

Fazendo curl na porta 3000 podera ver que retorna um "Ola mundo!".

``curl localhost:3000``

Agora que testamos temos que ir para proximo passo que e criar docker file. Para isso crie um arquivo docker chamado ***Dockerfile*** e insira dentro dele o seguinte:

```
FROM golang:1.15
WORKDIR /go/src/testekubernetes
COPY . .
RUN GOOS=linux go build ldflags="-s -w"
CMD ["./testekubernetes"]
```

Nesse script esta criando uma imagem docker, esta tambem copiando os arquivos que estao para dentro do container, esta gerando build do executavel server.go e rodando o executavel Go para rodar o servidor.

Proximo passo agora e gerar um docker build dessa imagem:

``docker build -t <caminho-do-diretorio-do-projeto>``

Agora vamos subir:

``docker run -p 3000:3000 <caminho-do-diretorio-do-projeto:latest>``

## Como fazer deploy de uma aplicacao

Para fazer deploy de uma aplicacao para docker-hub basta fazer:

``docker push <nome-da-imagem>``

Dessa forma a sua imagem ira subir para docker-hub.

## Criando Deployment

Para criar o nosso deployment, crie um arquivo chamado ***deployment.yaml*** dentro de uma pasta chamada k8s. 

Agora insira as seguintes linhas:

```
apiVersion: apps/v1
kind: Deployment
metadata:
    name: goserver
spec:
    replicas: 1
    selector:
        matchLabels:
            app: server
    template:
        metadata:
            labels:
                app: server
        spec:
            containers:
                - name: goserver
                  image: <nome-da-imagem>
                  ports:
                    - containerPort: 3000
```

Agora vamos rodar:

``kubectl apply -f deployment.yml``

Agora se voce fizer kubectl get pods, podera ver que ele criou um pod.

``kubectl get pods``

Agora vamos criar o service, basta criar arquivo service.yaml e por dentro dele:

```
apiVersion: v1
kind: Service
metadata:
    name: goserve-service
spec:
    type: ClusterIP
    ports:
        - protocol: TCP
          name: http-svc
          port: 3000
    selector:
        app: serve
```

Agora vamos iniciar ele para criar o service:

``kubectl apply -f service.yaml``

## Apontamento de porta

``kubectl port-foward service/goserver-service 3000:3000``

Dessa forma estamos dizendo que quando for acessada a port 3000 da maquina redirecione para port 3000 do goserver.