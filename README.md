# Claude Code Laravel Template

Template de configuração do Claude Code para projetos Laravel. Inclui regras, hooks e agents especializados.

## Instalação

### Opção 1: Clonar em projeto existente

```bash
# Na raiz do seu projeto Laravel
git clone https://github.com/SEU_USUARIO/claude-code-laravel.git temp-claude
cp -r temp-claude/.claude .
cp temp-claude/CLAUDE.md .
rm -rf temp-claude

# Configurar settings local
cp .claude/settings.local.json.example .claude/settings.local.json
```

### Opção 2: Usar como template Git

```bash
# Clonar como template
git clone --depth 1 https://github.com/SEU_USUARIO/claude-code-laravel.git
rm -rf claude-code-laravel/.git
```

### Opção 3: Download direto

Baixe os arquivos `.claude/` e `CLAUDE.md` e copie para seu projeto.

## Estrutura

```
.claude/
├── agents/           # Agents especializados
│   ├── api-documenter.md
│   ├── code-reviewer.md
│   ├── livewire-builder.md
│   ├── migration-validator.md
│   ├── performance-auditor.md
│   ├── refactor-analyzer.md
│   └── test-generator.md
├── hooks/            # Scripts executados antes/depois de tools
│   ├── format-php.sh
│   ├── protect-files.sh
│   └── validate-bash.sh
├── rules/            # Diretrizes por tecnologia
│   ├── alpine.md
│   ├── flux-ui.md
│   ├── fortify.md
│   ├── git.md
│   ├── herd.md
│   ├── laravel-12.md
│   ├── laravel-boost.md
│   ├── laravel-core.md
│   ├── livewire.md
│   ├── migrations.md
│   ├── php.md
│   ├── pint.md
│   ├── security.md
│   ├── tailwind.md
│   └── test.md
├── settings.json     # Configuração de hooks e agents
└── settings.local.json.example
CLAUDE.md             # Instruções principais do projeto
```

## Configuração

### 1. Settings Local

Copie o exemplo e ajuste conforme necessário:

```bash
cp .claude/settings.local.json.example .claude/settings.local.json
```

### 2. MCP Servers

O template usa os seguintes MCP servers:

- **Laravel Boost**: Database, logs, tinker, docs
- **Herd**: Ambiente de desenvolvimento PHP

Instale-os conforme a documentação de cada um.

### 3. Permissões

Edite `.claude/settings.local.json` para adicionar permissões específicas:

```json
{
  "permissions": {
    "allow": [
      "Bash(php artisan:*)",
      "Bash(npm run:*)",
      "Bash(vendor/bin/pint:*)"
    ]
  }
}
```

## Agents Disponíveis

| Agent | Descrição |
|-------|-----------|
| `code-reviewer` | Revisa código verificando segurança e padrões |
| `test-generator` | Gera testes Pest automaticamente |
| `migration-validator` | Valida migrations antes de executar |
| `livewire-builder` | Cria componentes Livewire com Flux UI |
| `refactor-analyzer` | Sugere refatorações (Services, Actions) |
| `performance-auditor` | Identifica N+1 queries e problemas de performance |
| `api-documenter` | Gera documentação OpenAPI/Swagger |

### Usando Agents

```
Use o agent code-reviewer para revisar app/Http/Controllers/
```

## Hooks

### PreToolUse

- **protect-files.sh**: Bloqueia edição de arquivos sensíveis
- **validate-bash.sh**: Valida comandos Bash antes de executar

### PostToolUse

- **format-php.sh**: Formata PHP com Pint após edição

## Customização

### Adicionar Nova Rule

Crie um arquivo em `.claude/rules/sua-rule.md` e referencie no `CLAUDE.md`.

### Adicionar Novo Agent

1. Crie o prompt em `.claude/agents/seu-agent.md`
2. Registre em `.claude/settings.json`:

```json
{
  "agents": {
    "seu-agent": {
      "description": "Descrição do agent",
      "promptFile": ".claude/agents/seu-agent.md",
      "tools": ["Read", "Write", "Glob"]
    }
  }
}
```

### Adicionar Novo Hook

1. Crie o script em `.claude/hooks/seu-hook.sh`
2. Torne executável: `chmod +x .claude/hooks/seu-hook.sh`
3. Registre em `.claude/settings.json`

## Requisitos

- Claude Code CLI
- Laravel Herd (opcional, para MCP herd)
- Laravel Boost MCP Server (opcional)

## Licença

MIT
