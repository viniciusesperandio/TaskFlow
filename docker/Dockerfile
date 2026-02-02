# ═══════════════════════════════════════════════════════════════════════════
# Stage 1: Base
# ═══════════════════════════════════════════════════════════════════════════
FROM mcr.microsoft.com/dotnet/aspnet:10.0 AS base
WORKDIR /app
EXPOSE 8080

# Criar usuário não-root para segurança
RUN addgroup --system --gid 1000 appgroup \
    && adduser --system --uid 1000 --ingroup appgroup appuser

# ═══════════════════════════════════════════════════════════════════════════
# Stage 2: Build
# ═══════════════════════════════════════════════════════════════════════════
FROM mcr.microsoft.com/dotnet/sdk:9.0 AS build
WORKDIR /src

# Copiar arquivos de projeto (cache de dependências)
COPY ["src/TaskFlow.API/TaskFlow.API.csproj", "TaskFlow.API/"]
COPY ["src/TaskFlow.Application/TaskFlow.Application.csproj", "TaskFlow.Application/"]
COPY ["src/TaskFlow.Domain/TaskFlow.Domain.csproj", "TaskFlow.Domain/"]
COPY ["src/TaskFlow.Infrastructure/TaskFlow.Infrastructure.csproj", "TaskFlow.Infrastructure/"]
COPY ["src/TaskFlow.CrossCutting/TaskFlow.CrossCutting.csproj", "TaskFlow.CrossCutting/"]
COPY ["Directory.Build.props", "./"]

# Restore
RUN dotnet restore "TaskFlow.API/TaskFlow.API.csproj"

# Copiar código fonte
COPY src/ .

# Build
RUN dotnet build "TaskFlow.API/TaskFlow.API.csproj" -c Release -o /app/build --no-restore

# ═══════════════════════════════════════════════════════════════════════════
# Stage 3: Publish
# ═══════════════════════════════════════════════════════════════════════════
FROM build AS publish
RUN dotnet publish "TaskFlow.API/TaskFlow.API.csproj" \
    -c Release \
    -o /app/publish \
    --no-restore \
    --no-build \
    /p:UseAppHost=false

# ═══════════════════════════════════════════════════════════════════════════
# Stage 4: Final
# ═══════════════════════════════════════════════════════════════════════════
FROM base AS final
WORKDIR /app

# Copiar artefatos publicados
COPY --from=publish /app/publish .

# Mudar para usuário não-root
USER appuser

# Health check
HEALTHCHECK --interval=30s --timeout=3s --start-period=10s --retries=3 \
    CMD curl --fail http://localhost:8080/health || exit 1

# Entry point
ENTRYPOINT ["dotnet", "TaskFlow.API.dll"]