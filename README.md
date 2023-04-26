# Entrega-04---Lab-de-Redes
# Paulina Kayse de Andrade Santos
# Empresa: salvedicasedinheiro.com.br

## Docker
A partir da pasta docker-pyserver criado no servidor ELAN, iremos adicionar a nossa página index.html referente a empresa.
Após isso, é criado o Dockerfile para obter a imagem que ao rodar o comando "run", executará via container. Para que o index.html rode no servidor HTTP simples, disponibilizado pelo próprio python3, é configurada as seguintes instruções dentro do arquivo Dockerfile:
````
FROM python3
ADD index.html
EXPOSE 8000
CMD python3 -m http.server 8000
````

Criado e configurado o Dockerfile, basta executar o comando abaixo para criar a imagem via Dockerfile.:
````
docker build -f Dockerfile . -t simplehttp
````
E este comando para criar e rodar o container a partir da imagem, execuntando como servidor (ou seja, em background "-d").
````
docker run -d -p 8000:80 -it --rm --name simplehttp simplehttp
````

Portanto, criamos então um servidor HTTP por comando python com porta externa 8000 para a porta interna 80, esta útlima a porta referente ao serviço TCP HTTP.

## Teste
Para verfificar se está mesmo rodando, pode ser utilizado o comando docker ps, que mostrará os containers em execução:
````
docker ps
````
Ou então, via comando wget com IP localhost para poder resgastar o arquivo index.html que está dentro do nosso conteiner:
````
wget http://127.0.0.1:80
cat index.html
````
