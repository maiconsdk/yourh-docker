## Como instalar

Baixe e instale o mkcert acessando a sua documentação em https://github.com/FiloSottile/mkcert para criarmos um certificado autoassinado local

### OBS

Para usuários de WLS2, os certificados criados não irão funcionar nos navegadores do Windows, por isso, você deverá instalar o mkcert, criar os certificados diretamente pelo Windows seguindo o guia de instalação usando o chocolatey pelo powershell e movê-los para o WLS2 na pasta docker/apache/ssl.

### Criando certificados

No diretório docker/apache/ssl, crie os certificados. Após criados, mude o nome deles para o padrão abaixo

```bash
mkcert umentor.test

mv umentor.test.pem umentor.test.crt
mv umentor.test-key.pem umentor.test.key
```

### Executando containers docker

No seu terminal, realize o docker build para executar o dockerfile (Caso utilize Docker desktop, você pode não ter disponível o docker-compose, por isso, use docker compose)

```bash
docker-compose build
```

Após o build, crie os containers necessários usando o docker compose up

```bash
docker-compose up -d
```

Com os containers criados e os certificados criados, você deverá acessar a pasta src/ do projeto e nela baixar o repositório do projeto YouRH

```bash
git clone git@github.com:umentorbr/umentor.git
```

Após isso, você deverá acessar o container para instalar as dependências do composer

```bash
docker exec -it server bash

composer install

exit
```

Após isso, você pode seguir com a configuração padrão do projeto, configurando o .env, restaurando o banco de dados e o filemanager.
OBS: Para acessar o DB seu gerenciador de DB, confira as portas e acessos no docker-compose.
