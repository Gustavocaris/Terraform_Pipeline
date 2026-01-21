<h3 align="center">
  Pipeline de Infraestrutura (AWS + Terraform + Github Actions + Multi Env)
</h3>

<p align="center">

  <img alt="License: MIT" src="https://img.shields.io/badge/license-MIT-%2304D361">
  <img alt="Version: 1.0" src="https://img.shields.io/badge/version-1.0-yellowgreen">

</p>


Crie o Identity Provider do Github em sua conta AWS
Crie uma IAM Role em sua conta AWS (Permissão mínimia de S3 e DynamoDB)
Crie um Bucket S3 em sua conta AWS (Habilite o Bucket Versioning)
Crie uma tabela no DynamoDB na sua conta AWS (PartitionKey com o nome "LockID")
Clone esse repositório
Configure os arquivos workflow
Pronto! Você já está habilitado para implantar infras na AWS com Terraform via pipeline

```html
Terraform_Pipeline/
├── Infra/
├── envs/
│       ├── dev/
│       │       └── terraform.tfvars
│       └── prod/
│             └── terraform.tfvars
|     ├── main.tf
│     ├── backend.tf
|     ├── main.tf
|     ├── variables.tf
|     ├── provider.tfvars
├── envs/
│     ├── dev/
│     │     └── terraform.tfvars
│     └── prod/
│           └── terraform.tfvars
└── .github/
      └── workflows/
            ├── terraform.yml # Workflow reutilizável
            ├── develop.yml # Pipeline DEV
            └── main.yml # Pipeline PROD
```
