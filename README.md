# Descrição do Sistema de Encurtamento de URLs

Este projeto é uma aplicação web desenvolvida em ASP.NET Core com a finalidade de encurtar URLs. A seguir, é apresentada uma visão geral do sistema, destacando suas funcionalidades e as tecnologias utilizadas.

## Funcionalidades

- **Encurtamento de URL:**  
  O sistema recebe uma URL completa e retorna uma URL reduzida. Esta operação é realizada pela API definida em [`Program.cs`](csharp:///c:/Users/dev_r/Downloads/source-code-aws-lambda/UrlShorter/before/UrlShortener/UrlShortener/Program.cs).

- **Redirecionamento:**  
  Ao acessar a URL encurtada, o sistema redireciona para a URL original cadastrada, utilizando rotas definidas na API.

- **Persistência dos Dados:**  
  As informações relacionadas às URLs (como código gerado, URL original e data de criação) são armazenadas utilizando o Entity Framework Core com banco de dados PostgreSQL, conforme configurado em [`ApplicationDbContext.cs`](csharp:///c:/Users/dev_r/Downloads/source-code-aws-lambda/UrlShorter/before/UrlShortener/UrlShortener/ApplicationDbContext.cs) e nas migrations ([`20240620155953_Create-Database.cs`](csharp:///c:/Users/dev_r/Downloads/source-code-aws-lambda/UrlShorter/before/UrlShortener/UrlShortener/Migrations/20240620155953_Create-Database.cs)).

- **Geração de Código Único:**  
  O serviço responsável por gerar o código único para cada URL encurtada é implementado em [`UrlShorteningService.cs`](csharp:///c:/Users/dev_r/Downloads/source-code-aws-lambda/UrlShorter/before/UrlShortener/UrlShortener/Services/UrlShorteningService.cs).

- **Documentação da API:**  
  Utiliza o Swashbuckle para geração de documentação Swagger, facilitando a interação e o teste da API.

## Tecnologias Utilizadas

- **.NET 8.0 (ASP.NET Core):**  
  O backend da aplicação é desenvolvido utilizando o .NET 8.0 com foco em APIs REST.

- **Entity Framework Core:**  
  Responsável pela camada de persistência e mapeamento objeto-relacional (ORM) para o PostgreSQL, possibilitando operações CRUD.

- **PostgreSQL:**  
  Banco de dados relacional utilizado para armazenar as informações das URLs, gerenciado através do container configurado no Docker.

- **Docker & Docker Compose:**  
  A aplicação e seus serviços (como o banco de dados) são empacotados em containers, permitindo um ambiente de desenvolvimento e produção isolado. As configurações podem ser consultadas em arquivos como [`docker-compose.yml`](yml:///c:/Users/dev_r/Downloads/source-code-aws-lambda/UrlShorter/before/UrlShortener/docker-compose.yml) e [`Dockerfile`](//c:/Users/dev_r/Downloads/source-code-aws-lambda/UrlShorter/before/UrlShortener/UrlShortener/Dockerfile).

- **AWS Lambda (Integração opcional):**  
  Na versão "after" do projeto, há integração com o AWS Lambda utilizando o pacote `Amazon.Lambda.AspNetCoreServer.Hosting` para hospedar a API em ambiente serverless. Verifique a referência em [`UrlShortener.csproj`](csharp:///c:/Users/dev_r/Downloads/source-code-aws-lambda/UrlShorter/after/UrlShortener/UrlShortener/UrlShortener.csproj).

- **Swagger / OpenAPI:**  
  Permite a exploração interativa da API e testes de endpoints através do Swagger UI.

- **User Secrets e Configurações de Ambiente:**  
  A aplicação utiliza arquivos de configuração (como [`appsettings.Development.json`](json:///c:/Users/dev_r/Downloads/source-code-aws-lambda/UrlShorter/before/UrlShortener/UrlShortener/appsettings.Development.json)) para gerenciar as strings de conexão e variáveis de ambiente em diferentes cenários (desenvolvimento e produção).

## Estrutura do Projeto

- **Pasta `UrlShortener`:**  
  Contém o código fonte da aplicação, incluindo controllers, serviços, models, entities, contextos do EF Core e extensões.  

- **Pasta `Migrations`:**  
  Armazena as migrations do Entity Framework Core que gerenciam a evolução do schema do banco de dados ([`ApplicationDbContextModelSnapshot.cs`](csharp:///c:/Users/dev_r/Downloads/source-code-aws-lambda/UrlShorter/before/UrlShortener/UrlShortener/Migrations/ApplicationDbContextModelSnapshot.cs)).

- **Arquivos de Configuração:**  
  Os arquivos `appsettings.json` e `appsettings.Development.json` contêm as configurações do ambiente, conectando a aplicação com o banco de dados e definindo níveis de logging.

- **Docker:**  
  Os arquivos `Dockerfile`, `docker-compose.yml` e `docker-compose.override.yml` definem o ambiente de containers utilizado para executar tanto a aplicação quanto o serviço de banco de dados.

## Conclusão

Este sistema de encurtamento de URLs, desenvolvido em ASP.NET Core com suporte a Docker e integração com AWS Lambda, é uma aplicação robusta que demonstra a integração entre uma API RESTful, persistência com Entity Framework Core e PostgreSQL, documentos interativos com Swagger e orquestração de containers usando Docker Compose.