<h3 align="center">
  Pipeline de Infraestrutura (AWS + Terraform + Github Actions)
</h3>

<p align="center">

  <img alt="License: MIT" src="https://img.shields.io/badge/license-MIT-%2304D361">
  <img alt="Version: 1.0" src="https://img.shields.io/badge/version-1.0-yellowgreen">

</p>

<hr>

# Overview

Este repositório tem como objetivo centralizar e padronizar a pipeline de infraestrutura como código (IaC), utilizando Terraform para o provisionamento de recursos na AWS, com execução automatizada por meio do GitHub Actions e autenticação segura via OIDC (OpenID Connect). A proposta é permitir que qualquer ambiente esteja apto a realizar deploys de infraestrutura de forma segura, automatizada, versionada e reprodutível, sem o uso de credenciais estáticas, utilizando boas práticas como:
  
- Integração nativa entre GitHub e AWS via Identity Provider
- Uso de IAM Roles com permissões mínimas (S3 e DynamoDB)
- Backend remoto com S3 (statefile + versionamento)
- Controle de concorrência com DynamoDB (lock de estado)
- Execução totalmente automatizada via pipeline
  
Ao final da configuração inicial (Identity Provider, IAM Role, S3, DynamoDB, workflows e repositório), o ambiente estará pronto para implantar infraestruturas na AWS com Terraform de forma automatizada via pipeline


<hr>

# Directory architecture

```html
Terraform_Pipeline/
	├── .github/
	│   └── workflows/
	│       ├── terraform.yml        
	│       ├── develop.yml          
	│       └── main.yml             
	│
	├── Infra/
	│   ├── backend.tf               
	│   ├── main.tf                  
	│   ├── variables.tf             
	│   ├── provider.tfvars          
	│   └── envs/
	│       ├── dev/
	│       │   └── terraform.tfvars 
	│       └── prod/
	│           └── terraform.tfvars 
	│
	├── Trash/
	│   ├── developOLD.yml            
	│   ├── mainOLD.yml
	│   └── terraformOLD.yml
```
<hr>

# Getting started

## 1 - Setup do projeto

Criar o repositorio de pipeline de Infra no github
- Criar o repositorio de pipeline de Infra no github
- Criação do Bucket S3 (Prod)
  

<hr>

## 2 - Configurar sua conta na AWS:

<p>Configurar sua conta AWS IAM Role que será usada pela nossa pipeline</p>
 <ul style="list-style-position: inside; padding: 0;">
  <li>Configurar a trust Relationship via OpenID</li>
  <li>Criar a Role</li>
  <li>Criar o bucket S3 que armazenará os Statesfiles do terraform.</li>
  <li>Criar a tabela do DynamoDB que irá realizar o lock para modificações</li>
</ul>

	
	
3 Criar o reusable workflow do terraform:
	Configurar os inputs do workflow
		-env
		-aws assume role arn
		-aws region
		-aws s3 bucket statefile
		-aws dynamodb table lock

	Configurar o setup do workflow
		-clonar o repositorio
		-configurar a AWS CLI
		-Configurar o terraform CLI
		
	Configurar o step terraform init
	Configurar o step terraform validate
	Configurar o step terraform Plan
	Configurar o step terraform Apply

OBS:O ideal seria ter configurada uma pipeline para o ambiente de Desenvolvimento também.

4 Vamos configurar a pipeline em Produção:
	- configurar o reusable workflow do terraform (main)
	- realizar a criação do bucket s3 no ambiente Prod


5 Praticas adicionais seria criarmos o suporte para o terraform destroy- mas isso não cheguei a realizar.
