# TaskFlow
Sistema de Gestão de Tarefas Empresarial - B2B

# Rodar a API
dotnet run --project src/TaskFlow.API

# Rodar testes unitários
dotnet test tests/TaskFlow.UnitTests

# Rodar testes de integração
dotnet test tests/TaskFlow.IntegrationTests

# Build da API
dotnet build src/TaskFlow.API

# Build de tudo (precisa especificar cada projeto ou usar loop)
for proj in src/**/*.csproj; do dotnet build "$proj"; done

# Restore de todos os projetos
dotnet restore src/TaskFlow.API  # Vai restaurar dependências transitivas

# Adicionar pacote NuGet
dotnet add src/TaskFlow.Infrastructure package Npgsql.EntityFrameworkCore.PostgreSQL

# Criar migration
dotnet ef migrations add InitialCreate \
  --project src/TaskFlow.Infrastructure \
  --startup-project src/TaskFlow.API

# Aplicar migrations
dotnet ef database update \
  --project src/TaskFlow.Infrastructure \
  --startup-project src/TaskFlow.API
