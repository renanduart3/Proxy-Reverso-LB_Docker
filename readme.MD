###Serviços

docker-compose
	version: '3'

	services:

		nginx:
			image: nginx:1.17.6-alpine
			container_name: nginx
			ports:
				- "8000:80"
		node1:
			image: nginx:1.17.6-alpine
			container_name: node1
			ports:
				- "80"
		node2:
			image: nginx:1.17.6-alpine
			container_name: node2
			ports:
				- "80"

nginx
/usr/share/nginx/html/index.html > proxy-load-balancer
/etc/nginx/nginx.conf
/etc/nginx/conf.d/default.conf

node1
/usr/share/nginx/html/index.html > node1
/etc/nginx/nginx.conf
/etc/nginx/conf.d/default.conf
tail -f /var/log/nginx/nginx-access.log

node2
/usr/share/nginx/html/index.html > node2


##Comandos auxiliares

docker-compose up -d  : Sobe os containers com as definições do docker-compose.yml
docker-compose ps : Ver os processos rodando dentro do orquestrador de container

nginx -s reload : Reinicia o servidor nginx
nginx -t : Verifica a sintaxe dos arquivos de configuracao do nginx


##Operações no Docker

As imagens do Nginx vem sem pacotes auxiliares, logo vc precisa do bash e vim para configura-los

###Inatalação dos pacotes auxiliares
docker-compose exec nginx apk add bash vim
docker-compose exec node1 apk add bash vim
docker-compose exec node2 apk add bash vim

###Executar o bash no terminal e avaliar os serviços
docker-compose exec nginx bash
docker-compose exec node1 bash
docker-compose exec node2 bash