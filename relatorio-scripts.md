# Relatório: Scripts Bash do SpecKit

## Visão Geral

Os scripts bash em [.specify/scripts/bash/](.specify/scripts/bash/) fornecem utilitários de automação que suportam o workflow dos agentes SpecKit. Eles gerenciam a criação de branches, validação de estruturas, atualização de contextos de AI agents e preparação de ambientes.

## Arquivos de Script (5 Total)

### 1. common.sh - Utilitários Compartilhados

**Localização**: [.specify/scripts/bash/common.sh](.specify/scripts/bash/common.sh)

**Funções Principais**:

#### `get_repo_root()`
- Encontra a raiz do repositório
- Busca por `.git` ou marcador `.specify`
- Suporta repositórios git e não-git

#### `get_current_branch()`
- Obtém branch atual do git
- Fallback para variável de ambiente `SPECIFY_FEATURE`
- Retorna nome da branch de feature

#### `get_feature_dir()`
- Constrói caminho do diretório da feature
- Formato: `specs/###-feature-name/`
- Base para todos os artifacts

#### `find_feature_dir_by_prefix()`
- Localiza spec por prefixo numérico (###)
- Suporta múltiplas branches por spec
- Útil para busca flexível

#### `get_feature_paths()`
- Retorna todos os caminhos importantes:
  - `REPO_ROOT`: Raiz do repositório
  - `FEATURE_DIR`: Diretório da feature
  - `SPEC`: spec.md
  - `PLAN`: plan.md
  - `TASKS`: tasks.md
  - E mais...

#### `check_feature_branch()`
- Valida formato da branch: `###-name`
- Verifica padrão de nomenclatura
- Retorna erro se inválido

#### `check_file()` / `check_dir()`
- Utilitários de validação de status
- Verifica existência de arquivos/diretórios
- Usado por outros scripts

**Uso**: Importado por todos os outros scripts via `source common.sh`

---

### 2. create-new-feature.sh - Criação de Features

**Localização**: [.specify/scripts/bash/create-new-feature.sh](.specify/scripts/bash/create-new-feature.sh)

**Propósito**: Cria novas branches de feature e diretórios estruturados

**Funcionalidades**:
- **Auto-incremento**: Busca último número em remotes + local + specs/
- **Nome inteligente**: Gera `###-short-name` a partir da descrição
  - Filtra stop words (the, a, an, of, for, to, with)
  - Preserva acrônimos (API, UI, DB)
  - Converte para lowercase com hífens
- **Truncamento**: Respeita limite de 244 bytes do GitHub
- **Estrutura**: Cria `specs/###-name/` e copia spec-template.md
- **Ambiente**: Define variável `SPECIFY_FEATURE`

**Flags**:
- `--json`: Saída em formato JSON
- `--short-name <name>`: Nome customizado
- `--number <num>`: Número específico

**Exemplo de Uso**:
```bash
./create-new-feature.sh "Add user authentication with JWT"
# Cria: 001-add-user-authentication/
# Branch: 001-user-auth
```

---

### 3. setup-plan.sh - Preparação de Planejamento

**Localização**: [.specify/scripts/bash/setup-plan.sh](.specify/scripts/bash/setup-plan.sh)

**Propósito**: Prepara ambiente para fase de planejamento técnico

**Processo**:
1. Valida feature branch (formato `###-name`)
2. Verifica existência do diretório da feature
3. Copia [plan-template.md](.specify/templates/plan-template.md) para feature directory
4. Retorna paths em JSON ou texto

**Quando Executar**: Antes de rodar `speckit.plan`

**Saída**:
- Arquivo `plan.md` vazio na feature directory
- Paths relevantes para o agent

---

### 4. update-agent-context.sh - Atualização de Contextos AI

**Localização**: [.specify/scripts/bash/update-agent-context.sh](.specify/scripts/bash/update-agent-context.sh)

**Propósito**: Atualiza automaticamente arquivos de contexto de AI agents com tech stack do projeto

**Funcionalidades**:
- **Parser de plan.md**: Extrai informações de tech stack
- **Multi-agent**: Suporta 15+ AI agents:
  - claude, gemini, copilot, cursor-agent
  - qwen, windsurf, aider, roo-cline
  - chatgpt, bolt, v0, github-spark
  - replit, lovable, pythagora
- **Modo de Atualização**:
  - Cria novos arquivos a partir de [agent-file-template.md](.specify/templates/agent-file-template.md)
  - Atualiza seções existentes preservando adições manuais
- **Seções Gerenciadas**:
  - "Active Technologies"
  - "Recent Changes" (últimas 3 features)

**Uso**:
```bash
# Atualizar agent específico
./update-agent-context.sh claude

# Atualizar todos os agents existentes
./update-agent-context.sh --all
```

**Quando Executar**: Automaticamente chamado por `speckit.plan`

---

### 5. check-prerequisites.sh - Validação de Requisitos

**Localização**: [.specify/scripts/bash/check-prerequisites.sh](.specify/scripts/bash/check-prerequisites.sh)

**Propósito**: Validação consolidada de pré-requisitos para execução de agents

**Funcionalidades**:
- Valida existência do diretório da feature
- Verifica arquivos obrigatórios (spec.md, plan.md)
- Lista documentos disponíveis:
  - research.md
  - data-model.md
  - contracts/
  - quickstart.md
  - checklists/
- Suporte a múltiplos formatos de saída

**Flags**:
- `--json`: Saída em formato JSON
- `--require-tasks`: Exige tasks.md
- `--include-tasks`: Inclui tasks.md se existir
- `--paths-only`: Retorna apenas paths

**Usado Por**: Todos os agents antes de executar para validar contexto

**Exemplo de Saída (JSON)**:
```json
{
  "status": "ok",
  "feature_dir": "specs/001-user-auth/",
  "available_docs": {
    "spec": true,
    "plan": true,
    "research": true,
    "data_model": false,
    "tasks": false
  }
}
```

---

## Fluxo de Uso Típico

### Ciclo de Vida de uma Feature

```
1. CRIAR NOVA FEATURE
   └─> ./create-new-feature.sh "Feature description"
       ├─> Cria branch: 001-feature-name
       ├─> Cria diretório: specs/001-feature-name/
       └─> Copia spec-template.md

2. PREPARAR PLANEJAMENTO
   └─> ./setup-plan.sh
       └─> Copia plan-template.md para feature dir

3. ATUALIZAR CONTEXTOS (automático via speckit.plan)
   └─> ./update-agent-context.sh --all
       └─> Atualiza .claude, .cursorrules, etc.

4. VALIDAR PRÉ-REQUISITOS (chamado por agents)
   └─> ./check-prerequisites.sh --json
       └─> Verifica estrutura e documentos disponíveis

5. DURANTE TODO O PROCESSO
   └─> common.sh fornece utilitários
       └─> Resolução de paths, validação de branches
```

## Integração com Agentes

### Agents que Utilizam Scripts

| Agent | Scripts Utilizados | Propósito |
|-------|-------------------|-----------|
| **speckit.specify** | create-new-feature.sh, common.sh | Criar branch e estrutura inicial |
| **speckit.plan** | setup-plan.sh, update-agent-context.sh | Preparar planning e atualizar contextos |
| **speckit.tasks** | check-prerequisites.sh, common.sh | Validar documentos disponíveis |
| **speckit.implement** | check-prerequisites.sh, common.sh | Validar estrutura antes de implementar |
| **speckit.analyze** | check-prerequisites.sh, common.sh | Verificar artifacts para análise |

### Comunicação Agent ↔ Script

**Formato**: Os scripts suportam saída JSON para fácil parsing pelos agents

**Exemplo**:
```bash
# Agent chama script
./check-prerequisites.sh --json

# Script retorna JSON
{
  "status": "ok",
  "feature_dir": "specs/001-auth/",
  "spec_path": "specs/001-auth/spec.md",
  "plan_path": "specs/001-auth/plan.md"
}
```

## Características Técnicas

### Compatibilidade
- **Git**: Funciona com repositórios git
- **Não-Git**: Suporta projetos sem git usando marcador `.specify`
- **Cross-platform**: Bash puro, compatível com Linux/Mac/WSL

### Robustez
- **Validação**: Checks extensivos de erros
- **Fallbacks**: Múltiplas estratégias de resolução
- **Mensagens**: Erros claros e acionáveis

### Modularidade
- **common.sh**: Base compartilhada
- **Função única**: Cada script tem responsabilidade clara
- **Composição**: Scripts podem chamar uns aos outros

## Variáveis de Ambiente

### SPECIFY_FEATURE
- Define feature atual quando não há git
- Formato: `###-feature-name`
- Usado como fallback por `get_current_branch()`

### REPO_ROOT (calculado)
- Raiz do repositório
- Determinado por `get_repo_root()`

## Boas Práticas

### Para Desenvolvedores
1. **Clone**: Scripts esperam ser executados da raiz do repo
2. **Branch**: Sempre trabalhe em branch de feature (`###-name`)
3. **Validação**: Use `check-prerequisites.sh` antes de rodar agents

### Para Extensões
1. **common.sh**: Sempre importe para funcionalidades base
2. **JSON**: Use flag `--json` para processamento programático
3. **Error handling**: Scripts retornam exit codes apropriados

## Referências Cruzadas

- Código dos scripts: [.specify/scripts/bash/](.specify/scripts/bash/)
- Templates usados: [.specify/templates/](.specify/templates/)
- Agentes que os utilizam: [.github/agents/](.github/agents/)
- Fluxo de agentes completo: [relatorio-fluxo-agentes.md](relatorio-fluxo-agentes.md)
