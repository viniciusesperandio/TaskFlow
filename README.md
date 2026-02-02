# 🚀 TaskFlow - Sistema de Gestão de Tarefas Empresarial

[![.NET](https://img.shields.io/badge/.NET-9.0-512BD4?logo=dotnet)](https://dotnet.microsoft.com/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-16-336791?logo=postgresql)](https://www.postgresql.org/)
[![RabbitMQ](https://img.shields.io/badge/RabbitMQ-3.13-FF6600?logo=rabbitmq)](https://www.rabbitmq.com/)
[![Redis](https://img.shields.io/badge/Redis-7-DC382D?logo=redis)](https://redis.io/)
[![Docker](https://img.shields.io/badge/Docker-ready-2496ED?logo=docker)](https://www.docker.com/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

Sistema B2B de gestão de tarefas e projetos com foco em **rastreabilidade, performance e observabilidade**. Arquitetura em camadas seguindo princípios de **Clean Architecture** e **Domain-Driven Design (DDD)**.

---

## 📋 Índice

- [Sobre o Projeto](#-sobre-o-projeto)
- [Tecnologias Utilizadas](#-tecnologias-utilizadas)
- [Arquitetura](#-arquitetura)
- [Pré-requisitos](#-pré-requisitos)
- [Instalação e Configuração](#-instalação-e-configuração)
- [Como Executar](#-como-executar)
- [Acessos aos Serviços](#-acessos-aos-serviços)
- [Estrutura do Projeto](#-estrutura-do-projeto)
- [Funcionalidades](#-funcionalidades)
- [Variáveis de Ambiente](#-variáveis-de-ambiente)
- [Testes](#-testes)
- [Monitoramento](#-monitoramento)
- [Contribuindo](#-contribuindo)
- [Licença](#-licença)
- [Contato](#-contato)

---

## 📖 Sobre o Projeto

TaskFlow é um sistema completo de gerenciamento de tarefas desenvolvido para ambientes corporativos, oferecendo:

- ✅ Gestão completa de tarefas e projetos
- ✅ Autenticação e autorização com JWT
- ✅ Mensageria assíncrona para notificações
- ✅ Cache distribuído para alta performance
- ✅ Observabilidade com métricas e dashboards
- ✅ Análise de qualidade de código automatizada
- ✅ CI/CD com GitHub Actions

**Objetivo**: Demonstrar boas práticas de desenvolvimento .NET em um projeto real e escalável.

---

## 🛠️ Tecnologias Utilizadas

### **Backend**
- **.NET 9.0** - Framework principal
- **C# 13** - Linguagem de programação
- **ASP.NET Core** - Web API
- **Entity Framework Core 9.0** - ORM
- **Dapper** - Micro-ORM para queries otimizadas

### **Banco de Dados**
- **PostgreSQL 16** - Banco de dados relacional
- **Redis 7** - Cache distribuído

### **Mensageria**
- **RabbitMQ 3.13** - Message broker
- **MassTransit 8.2** - Framework de mensageria

### **Observabilidade**
- **Prometheus** - Coleta de métricas
- **Grafana** - Visualização de dados
- **Serilog** - Logging estruturado

### **Qualidade de Código**
- **SonarQube** - Análise estática
- **xUnit** - Framework de testes
- **FluentAssertions** - Assertions legíveis
- **Moq** - Mock de dependências

### **DevOps**
- **Docker & Docker Compose** - Containerização
- **GitHub Actions** - CI/CD
- **Azure DevOps** - Pipelines alternativos

### **Documentação**
- **Swagger/OpenAPI** - Documentação interativa da API

---

## 🏗️ Arquitetura

O projeto segue os princípios de **Clean Architecture** com separação clara de responsabilidades:

```
┌─────────────────────────────────────────────────────────────┐
│                        TaskFlow.API                          │
│                  (Controllers, Middlewares)                  │
└─────────────────────────┬───────────────────────────────────┘
                          │
┌─────────────────────────▼───────────────────────────────────┐
│                   TaskFlow.Application                       │
│              (Use Cases, DTOs, Validators)                   │
└─────────────────────────┬───────────────────────────────────┘
                          │
┌─────────────────────────▼───────────────────────────────────┐
│                     TaskFlow.Domain                          │
│           (Entities, Value Objects, Interfaces)              │
└─────────────────────────┬───────────────────────────────────┘
                          │
┌─────────────────────────▼───────────────────────────────────┐
│                 TaskFlow.Infrastructure                      │
│      (Repositories, EF Core, RabbitMQ, Services)             │
└──────────────────────────────────────────────────────────────┘
```

### **Princípios Aplicados:**
- ✅ **SOLID** - Princípios de design orientado a objetos
- ✅ **DDD** - Domain-Driven Design
- ✅ **CQRS** - Command Query Responsibility Segregation
- ✅ **Repository Pattern** - Abstração de acesso a dados
- ✅ **Dependency Injection** - Inversão de controle

---

## 📦 Pré-requisitos

Antes de começar, certifique-se de ter instalado:

- [.NET 9 SDK](https://dotnet.microsoft.com/download/dotnet/9.0) - Framework .NET
- [Docker Desktop](https://www.docker.com/products/docker-desktop) - Para executar os serviços
- [Git](https://git-scm.com/) - Controle de versão
- **Editor de código**: [Visual Studio 2022](https://visualstudio.microsoft.com/), [VS Code](https://code.visualstudio.com/) ou [Rider](https://www.jetbrains.com/rider/)

### **Verificar Instalações:**

```bash
# Verificar .NET
dotnet --version
# Deve retornar: 9.0.x

# Verificar Docker
docker --version
docker-compose --version

# Verificar Git
git --version
```

---

## 🚀 Instalação e Configuração

### **1. Clonar o Repositório**

```bash
git clone https://github.com/seu-usuario/TaskFlow.git
cd TaskFlow
```

### **2. Configurar Variáveis de Ambiente**

```bash
# Copiar o arquivo de exemplo
cp .env.example .env

# Editar o arquivo .env com suas configurações (opcional)
# As configurações padrão já funcionam para desenvolvimento
```

### **3. Criar Estrutura de Pastas para Monitoramento**

```bash
# Windows (PowerShell)
mkdir -p monitoring\prometheus, monitoring\grafana\provisioning\datasources, monitoring\grafana\provisioning\dashboards, monitoring\grafana\dashboards

# Linux/Mac
mkdir -p monitoring/prometheus monitoring/grafana/provisioning/{datasources,dashboards} monitoring/grafana/dashboards
```

### **4. Copiar Arquivos de Configuração**

Certifique-se de que os arquivos de configuração estão nos locais corretos:

```
monitoring/
├── prometheus/
│   ├── prometheus.yml
│   └── alerts.yml
└── grafana/
    └── provisioning/
        ├── datasources/
        │   └── datasource.yml
        └── dashboards/
            └── dashboard.yml
```

---

## ▶️ Como Executar

### **Opção 1: Desenvolvimento Local (Recomendado)**

Ideal para desenvolvimento ativo com hot reload.

#### **Passo 1: Subir a Infraestrutura (Docker)**

```bash
# Subir PostgreSQL, RabbitMQ, Redis, Prometheus, Grafana e SonarQube
docker-compose up -d

# Verificar se os containers estão rodando
docker-compose ps

# Ver logs (opcional)
docker-compose logs -f
```

#### **Passo 2: Executar a API (.NET)**

```bash
# Navegar até a pasta da API
cd src/TaskFlow.API

# Restaurar dependências (primeira vez)
dotnet restore

# Executar a API
dotnet run --launch-profile http
```

A API estará disponível em: **http://localhost:5000**

#### **Passo 3: Acessar o Swagger**

Abra o navegador em: **http://localhost:5000/swagger**

---

### **Opção 2: Tudo no Docker**

Útil para testar o ambiente completo em containers.

```bash
# Subir TUDO (infraestrutura + API)
docker-compose up -d

# Verificar status
docker-compose ps

# Ver logs da API
docker-compose logs -f taskflow-api
```

> **Nota**: A API no Docker só funcionará após implementar todos os projetos da solution.

---

### **Comandos Úteis**

```bash
# Parar todos os containers
docker-compose stop

# Parar e remover containers
docker-compose down

# Remover containers E volumes (⚠️ apaga dados!)
docker-compose down -v

# Rebuildar a API após mudanças
docker-compose build taskflow-api
docker-compose restart taskflow-api

# Ver logs de um serviço específico
docker-compose logs -f postgres
docker-compose logs -f rabbitmq
docker-compose logs -f redis
```

---

## 🔗 Acessos aos Serviços

| Serviço | URL | Credenciais | Descrição |
|---------|-----|-------------|-----------|
| **TaskFlow API** | http://localhost:5000/swagger | - | Documentação interativa da API |
| **PostgreSQL** | localhost:5432 | postgres / postgres123 | Banco de dados |
| **RabbitMQ Management** | http://localhost:15672 | admin / admin123 | Gerenciamento de filas |
| **Redis** | localhost:6379 | password: redis123 | Cache (use Redis CLI ou GUI) |
| **Grafana** | http://localhost:3000 | admin / admin123 | Dashboards de métricas |
| **Prometheus** | http://localhost:9090 | - | Coleta de métricas |
| **SonarQube** | http://localhost:9000 | admin / admin | Análise de código |

### **Conectar ao PostgreSQL via Client (DBeaver, pgAdmin, etc):**

```
Host:     localhost
Port:     5432
Database: taskflow
Username: postgres
Password: postgres123
```

---

## 📁 Estrutura do Projeto

```
TaskFlow/
│
├── src/
│   ├── TaskFlow.API/              # Camada de apresentação (Controllers, Middlewares)
│   ├── TaskFlow.Application/       # Casos de uso, DTOs, Validações
│   ├── TaskFlow.Domain/            # Entidades, Value Objects, Regras de negócio
│   ├── TaskFlow.Infrastructure/    # Repositórios, EF Core, RabbitMQ
│   └── TaskFlow.CrossCutting/      # IoC, Logging, Configurações
│
├── tests/
│   ├── TaskFlow.UnitTests/         # Testes unitários
│   └── TaskFlow.IntegrationTests/  # Testes de integração
│
├── monitoring/
│   ├── prometheus/                 # Configuração do Prometheus
│   └── grafana/                    # Dashboards do Grafana
│
├── docker/
│   ├── Dockerfile                  # Dockerfile da API
│   └── .dockerignore
│
├── .github/
│   └── workflows/                  # GitHub Actions (CI/CD)
│
├── docker-compose.yml              # Orquestração dos serviços
├── .env.example                    # Template de variáveis de ambiente
└── README.md                       # Este arquivo
```

---

## ✨ Funcionalidades

### **Implementadas:**
- ✅ API RESTful com Swagger
- ✅ Health checks
- ✅ Infraestrutura Docker completa
- ✅ Configurações por ambiente (Dev, Staging, Production)

### **Em Desenvolvimento:**
- 🔄 Autenticação e autorização JWT
- 🔄 CRUD de tarefas
- 🔄 Atribuição de tarefas a usuários
- 🔄 Comentários e anexos
- 🔄 Notificações via RabbitMQ
- 🔄 Relatórios e dashboards
- 🔄 Histórico de alterações (audit log)

### **Planejadas:**
- 📋 Webhooks para integrações
- 📋 API de relatórios
- 📋 Suporte a múltiplos projetos
- 📋 Gestão de equipes

---

## 🔧 Variáveis de Ambiente

As configurações podem ser feitas via arquivo `.env` ou diretamente nos `appsettings.{Environment}.json`.

### **Principais Variáveis:**

```bash
# Database
DB_HOST=localhost
DB_PORT=5432
DB_NAME=taskflow
DB_USER=postgres
DB_PASSWORD=postgres123

# RabbitMQ
RABBITMQ_HOST=localhost
RABBITMQ_PORT=5672
RABBITMQ_USER=admin
RABBITMQ_PASSWORD=admin123

# Redis
REDIS_CONNECTION=localhost:6379,password=redis123

# JWT
JWT_SECRET=super-secret-key-min-32-chars
JWT_EXPIRATION_MINUTES=60

# Email (SendGrid - Produção)
SENDGRID_API_KEY=your-api-key-here

# SonarQube
SONAR_HOST_URL=http://localhost:9000
SONAR_TOKEN=your-token-here
```

---

## 🧪 Testes

### **Executar Testes Unitários:**

```bash
# Todos os testes
dotnet test

# Com cobertura de código
dotnet test --collect:"XPlat Code Coverage"

# Apenas testes unitários
dotnet test tests/TaskFlow.UnitTests

# Apenas testes de integração
dotnet test tests/TaskFlow.IntegrationTests
```

### **Relatório de Cobertura:**

```bash
# Gerar relatório HTML
dotnet tool install --global dotnet-reportgenerator-globaltool
reportgenerator -reports:**/coverage.cobertura.xml -targetdir:coveragereport
```

---

## 📊 Monitoramento

### **Métricas Disponíveis:**

- Requisições HTTP (total, taxa, latência)
- Taxa de erros (4xx, 5xx)
- Uso de memória e CPU
- Tamanho de filas do RabbitMQ
- Conexões ativas do PostgreSQL
- Hit rate do Redis

### **Acessar Dashboards:**

1. **Grafana**: http://localhost:3000
   - Login: admin / admin123
   - Dashboards pré-configurados estarão disponíveis

2. **Prometheus**: http://localhost:9090
   - Explorar métricas em: Status → Targets

### **Alertas Configurados:**

- API indisponível (> 1 minuto)
- Taxa alta de erros (> 5%)
- Tempo de resposta alto (p95 > 1s)
- Banco de dados indisponível
- RabbitMQ indisponível
- Filas com muitas mensagens (> 1000)

---

## 🤝 Contribuindo

Contribuições são bem-vindas! Para contribuir:

1. Fork o projeto
2. Crie uma branch para sua feature (`git checkout -b feature/MinhaFeature`)
3. Commit suas mudanças (`git commit -m 'Adiciona MinhaFeature'`)
4. Push para a branch (`git push origin feature/MinhaFeature`)
5. Abra um Pull Request

### **Padrões de Código:**

- Siga os princípios SOLID
- Escreva testes para novas funcionalidades
- Use conventional commits
- Documente APIs públicas
- Mantenha cobertura de testes > 80%

---

## 📄 Licença

Este projeto está sob a licença MIT. Veja o arquivo [LICENSE](LICENSE) para mais detalhes.

---

## 📧 Contato

**Vinicius Esperandio**

- LinkedIn: [linkedin.com/in/viniciusesperandio](https://www.linkedin.com/in/viniciusesperandio)
- Email: viniciusesperandio@hotmail.com
- GitHub: [@viniciusesperandio](https://github.com/viniciusesperandio)

---

## 🎯 Roadmap

### **Versão 1.0 (MVP)**
- [x] Setup inicial do projeto
- [x] Configuração Docker
- [x] API básica com Swagger
- [ ] Autenticação JWT
- [ ] CRUD de tarefas
- [ ] Testes unitários básicos

### **Versão 1.1**
- [ ] Notificações via RabbitMQ
- [ ] Cache com Redis
- [ ] Dashboards Grafana
- [ ] CI/CD com GitHub Actions

### **Versão 2.0**
- [ ] Suporte a projetos
- [ ] Gestão de equipes
- [ ] Webhooks
- [ ] API de relatórios

---

## 🙏 Agradecimentos

- [Anthropic](https://www.anthropic.com/) - Claude AI
- [.NET Foundation](https://dotnetfoundation.org/)
- Comunidade open-source

---

<div align="center">

**⭐ Se este projeto te ajudou, considere dar uma estrela!**

Feito com ❤️ por [Vinicius Esperandio](https://github.com/viniciusesperandio)

</div>