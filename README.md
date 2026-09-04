# Static website with S3

## Visao Geral do Projeto

Desenvolvi este projeto para automatizar a hospedagem e o deploy de um site estatico no Amazon S3. Utilizei com sucesso o AWS Systems Manager Session Manager para acessar o servidor de forma segura via linha de comando sem expor portas SSH.

## Tecnologias e Ferramentas

* Amazon S3 para hospedagem dos arquivos estaticos do site
* AWS Systems Manager SSM para acesso remoto seguro via CLI
* AWS IAM para gestao de usuarios e politicas de acesso
* AWS CLI e Bash Scripting para automacao e sincronizacao do deploy

## O que Aprendi e Pratiquei

* Criei e configurei buckets no Amazon S3 totalmente pela linha de comando
* Implementei regras de acesso seguro com o AWS Systems Manager
* Estruturei politicas de acesso granular no AWS IAM
* Automatizei processos repetitivos criando scripts em Bash
* Otimizei o envio de arquivos utilizando o comando sync para transferir apenas o delta de alteracoes

## Passo a Passo da Execucao

### 1. Acesso Seguro e Configuracao Inicial

Acessei a instancia pelo SSM e criei o bucket S3 configurando a hospedagem estatica:

```bash
sudo su - ec2-user
aws configure
aws s3api create-bucket --bucket pedrocarvsec --region us-west-2 --create-bucket-configuration LocationConstraint=us-west-2
aws s3 website s3://pedrocarvsec/ --index-document index.html
2. Automacao do Deploy com Script Bash
Criei o script update_website.sh para automatizar a sincronizacao dos arquivos do site com o bucket:

Bash
#!/bin/bash
aws s3 sync /home/ec2user/sysops/static_website/ s3://pedrocarvsec/ --acl public-read
Concedi permissao de execucao ao arquivo e rodei a automacao:

Bash
chmod +x update_website.sh
./update_website.sh
Evidencias do Projeto
Automacao e CLI via SSM: docs/01_automation_ssm.png

Configuracao no Console S3: docs/02_s3_configuration.png

Site Publicado e Online: docs/03_website_live.png

URL publica do site: http://pedrocarvsec.s3-website-us-west-2.amazonaws.com
