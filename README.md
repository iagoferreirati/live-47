-- O que é o Docker Compose?

O Docker Compose é usado para executar aplicações que possuem vários contêineres usando um arquivo YAML.
Pode haver vários casos em que o aplicações docker deve executar vários contêineres para diferentes tecnologias (Mysql, Redis ...)

Agora, criar, executar e conectar arquivos docker separados para cada contêiner pode ser uma tarefa difícil; é aqui que o docker-compose ajuda você. Usando um único arquivo docker-compose.yml , você pode criar e iniciar todos os contêineres executando um único comando

Isso é muito útil para aplicações corporativas em produção, onde diversas aplicações rodam dentro de containers.


-- O arquivo docker-compose.yml

Nesse arquivo, precisamos especificar pelo menos um service e opcionalmente, volumes e redes.

services:
...
volumes:
...
networks:
...

1. services (Serviços)
Em primeiro lugar, os serviços referem-se à configuração dos contêineres.

Por exemplo, vamos pegar um aplicação Web dockerizado que consiste em um front-end, um back-end e um banco de dados: provavelmente dividiríamos esses componentes em três imagens e os definiríamos como três serviços diferentes na configuração:


services:
  frontend:
    image: nginx
    ...
  backend:
    image: node
    ...
  db:
    image: postgres
    ...


Nos podemos usar uma imgem publica ou personalizada

publica
services:
  my-service:
    image: ubuntu:latest
    ...

Personalizada
services:
  my-custom-app:
    build: /path/to/dockerfile/
    ...


2. Configurando os Volumes:

Os volumes são o mecanismo preferencial para dados persistentes gerados e usados ​​pelos contêineres do Docker. Embora as montagens de ligação dependam da estrutura de diretório e do sistema operacional da máquina host, os volumes são totalmente gerenciados pelo Docker

services:
  volumes-example-service:
    image: alpine:latest
    volumes:
      - /tmp/banco:/var/mysql/db

2. Configurando a Rede:
Os contêineres do Docker se comunicam entre si em redes criadas, implicitamente ou por meio de configuração, pelo Docker Compose. Um serviço pode se comunicar com outro serviço na mesma rede simplesmente referenciando-o pelo nome do contêiner e porta (por exemplo , network-example-service:80 ), desde que tenhamos tornado a porta acessível por meio da palavra-chave de exposição :    

networks:
  network-db:
    driver: bridge

services:
  mysql:
    container_name: mysql
    image: mysql:8.0.28
    networks:
      - network-db


Repositorio com templates dos sites
git clone git@github.com:learning-zone/website-templates.git   


Github actins
  packer + ansible >
    role do ansible -> instalar o docker
    role do ansible -> Executar docker compose
  terraform
    Subir um ec2 com a imagem gerada pelo packer

  Exemplo:
    https://github.com/iagoferreirati/stack-zabbix-server/blob/main/.github/workflows/main.yml



Para quem esta começando
  -> Linux
  -> Ansible
  -> Docker
  -> Cloud (AWS)
  -> Terraform
  -> CI/CD