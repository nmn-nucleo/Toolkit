# Aba 6 — Avancado

## A camada profunda da stack — onde voce realmente customiza

---

## INTRO (topo da aba)

### Eyebrow
> Conteudo tecnico — para quem ja domina o basico

### Titulo principal
> # O nivel raso e tutorial. O nivel profundo e oficio.

### Lead paragraph
Essa aba e pra quem ja passou pelas Abas 1 a 5 e quer ir alem: configurar com precisao, expandir capacidades via MCP, dividir trabalho com subagents, programar limites com hooks, criar skills proprias, otimizar performance, integrar com CI/CD, debuggar problemas, gerir memoria semantica, e empacotar tudo em plugins distribuiveis. **Cada sub-aba e independente — entra pelo que precisa.**

### Indice da aba (11 sub-abas, navegacao por anchors)
1. CLAUDE.md / AGENTS.md avancado
2. settings.json / config.toml
3. MCP — Model Context Protocol
4. Subagents
5. Hooks
6. Custom skills
7. Performance
8. CI/CD
9. Troubleshooting
10. **Memoria** (novo — direto da reuniao)
11. **Plugins & Marketplace** (novo — direto da reuniao)

---

## SUB-ABA 1 — CLAUDE.md / AGENTS.md avancado

> Aprofunda o que foi visto nas Abas 2 e 3.

### A hierarquia em camadas (Claude Code)

Claude Code le `CLAUDE.md` em **5 niveis hierarquicos** (mais especifico vence):

```
1. System    → /etc/claude/CLAUDE.md             (admin maquina)
2. User      → ~/.claude/CLAUDE.md               (suas preferencias)
3. Project   → <projeto>/CLAUDE.md               (esse projeto)
4. Directory → <subpasta>/CLAUDE.md              (subdiretorio)
5. Flag      → claude --instructions <arquivo>   (sessao especifica)
```

**Em conflito:** o nivel mais profundo vence. Ex: instrucao de projeto sobrescreve user, que sobrescreve system.

### A hierarquia em Codex

Codex usa `AGENTS.md` em **2 niveis principais**:

```
1. Global    → ~/.codex/AGENTS.md          (suas preferencias)
2. Project   → <projeto>/AGENTS.md         (esse projeto)
```

Mais simples, mas equivalente em poder. **Project vence global.**

### O que vai em cada nivel

| Nivel | Conteudo tipico | Tamanho |
|---|---|---|
| System / Admin | Politicas org (Claude Code only) | Curto, raramente muda |
| User / Global | Preferencias pessoais (idioma, tom, estilo) | 20-50 linhas |
| Project | Stack, convencoes, decisoes, restricoes do projeto | 100-300 linhas |
| Directory | Especifico de uma subpasta (Claude Code only) | Raro, casos especiais |
| Flag | Instrucao temporaria pra sessao especifica | Inline ou arquivo |

### Padroes avancados pra projeto

**Padrao 1 — Sections com headers fortes:**
```markdown
# Project: [Nome]

## CRITICAL RULES (read first)
- NUNCA fazer X
- NUNCA modificar Y
- SEMPRE verificar Z antes de commit

## Stack
...

## Conventions
...

## Architecture decisions
...

## Common patterns to follow
...

## Anti-patterns to avoid
...
```

**Padrao 2 — Inclusao de outros arquivos:**
```markdown
## Importantes referencias
- Ver `/docs/architecture.md` pra decisoes
- Ver `/docs/api-conventions.md` pra padroes de endpoint
- Ver `/scripts/check-commit.sh` pra validacoes pre-commit
```

**Padrao 3 — Comandos rapidos no topo:**
```markdown
## Quick commands
- Setup: `npm install && npm run setup`
- Run: `npm run dev`
- Test: `npm test`
- Build: `npm run build`
- Deploy: `./scripts/deploy.sh`
```

### O que NAO colocar
- Documentacao pesada de API (use README.md ou /docs/)
- Historico de mudanca (use CHANGELOG.md)
- Onboarding completo (use ONBOARDING.md ou Notion)

CLAUDE.md/AGENTS.md e **briefing operacional** — curto, direto, alto-impacto.

---

## SUB-ABA 2 — settings.json / config.toml

### Claude Code — settings.json

Localizacao: `~/.claude/settings.json` (global) ou `<projeto>/.claude/settings.json` (local).

Estrutura tipica:

```json
{
  "model": "claude-opus-4-7",
  "max_tokens": 8192,
  "temperature": 0.7,
  "tools": {
    "filesystem": { "enabled": true },
    "shell": { "enabled": true, "allowed_commands": ["npm", "git", "python"] },
    "web": { "enabled": false }
  },
  "hooks": {
    "PreToolUse": ".claude/hooks/validate.sh",
    "PostToolUse": ".claude/hooks/log.sh"
  },
  "skills": {
    "auto_load": true,
    "search_paths": [
      "~/.claude/skills",
      ".claude/skills"
    ]
  }
}
```

### Codex — config.toml

Localizacao: `~/.codex/config.toml`.

Estrutura tipica:

```toml
[model]
default = "gpt-5.4"
reasoning = "medium"

[sandbox]
mode = "on-request"  # untrusted | on-request | never

[agents]
max_threads = 4

[mcp]
enabled = true
servers = ["filesystem", "github", "memory"]

[profiles.work]
model = "gpt-5.4"
sandbox = "on-request"

[profiles.research]
model = "gpt-5.4"
reasoning = "high"
sandbox = "never"
```

**Profiles em Codex:** voce pode ter perfis nomeados e ativar via `codex --profile work`. Util pra alternar entre contextos (trabalho serio vs experimentacao livre).

---

## SUB-ABA 3 — MCP (Model Context Protocol)

### O que e MCP

**Padrao aberto** que conecta agentes a ferramentas externas (bancos, APIs, filesystem, GitHub) via protocolo unificado. Em vez do agente "achar" dados na internet, ele consulta direto a fonte autenticada.

**Suportado nativamente** por Claude Code, Codex, Cursor, Aider.

### Como funciona

```
Agente → MCP Client → MCP Server → Servico externo
                                   (DB, API, filesystem)
```

Voce roda um **MCP server** local (ou conecta a um remoto). O agente conversa com o server. O server faz o trabalho.

### Servers populares (que valem instalar)

| Server | Pra que | Quando usar |
|---|---|---|
| **filesystem** | Acesso a arquivos locais | Sempre (basico) |
| **github** | API do GitHub | Quem usa GitHub |
| **gitlab** | API do GitLab | Quem usa GitLab |
| **memory** | Memoria persistente entre sessoes | Projetos longos (ver Sub-aba 10) |
| **slack** | Integracao Slack | Time que vive no Slack |
| **postgresql** | Query em Postgres | Projetos com banco |
| **duckdb** | Analise local de dados | Analise de planilhas/CSVs |
| **notion** | Notion como context source | Quem usa Notion |
| **obsidian** | Vault do Obsidian | Quem versiona conhecimento ali |
| **playwright** | Controle de browser | Automacao web, testes E2E |

### Setup em Claude Code

Edita `~/.claude/settings.json`:

```json
{
  "mcp_servers": {
    "filesystem": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-filesystem", "/path/to/allowed"]
    },
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": { "GITHUB_TOKEN": "ghp_..." }
    }
  }
}
```

### Setup em Codex

Edita `~/.codex/config.toml`:

```toml
[mcp.servers.filesystem]
command = "npx"
args = ["-y", "@modelcontextprotocol/server-filesystem", "/path/to/allowed"]

[mcp.servers.github]
command = "npx"
args = ["-y", "@modelcontextprotocol/server-github"]
env = { GITHUB_TOKEN = "ghp_..." }
```

### Cuidados de seguranca

- **Filesystem:** sempre limita o path (nao da acesso a `/`)
- **GitHub/GitLab:** use token com escopo minimo necessario
- **Postgres:** usuario read-only se possivel
- **Servers desconhecidos:** roda em sandbox antes de habilitar

---

## SUB-ABA 4 — Subagents

### O que e

Subagent e uma **sub-sessao** que o agente principal abre pra resolver tarefa especifica sem poluir o contexto principal. Pensa nele como **estagiario focado**: voce delega, ele trabalha em paralelo, retorna resumo.

### Quando usar

- Tarefa pesada que vai consumir muito contexto (ex: ler 50 arquivos)
- Tarefa que pode rodar em paralelo (ex: pesquisar 3 abordagens diferentes)
- Tarefa especifica com contexto proprio (ex: revisor de seguranca)

### Claude Code — Agent Teams

Claude Code permite **subagents coordenados** que compartilham task list. Voce pode:

- Definir agentes com **roles especificas** (frontend specialist, backend specialist, reviewer)
- Compartilhar contexto via task list comum
- Coordenar dependencias entre subagents

```markdown
# Em CLAUDE.md
## Agents

### frontend-specialist
- Foco em React, CSS, UX
- Le apenas /src/components, /src/pages
- Output: codigo + screenshot mental do resultado

### backend-specialist
- Foco em API, banco, performance
- Le apenas /src/api, /src/db
- Output: codigo + endpoints documentados

### reviewer
- Le tudo, nao escreve nada
- Foco: bugs, seguranca, padroes
```

### Codex — Cloud Workers

Codex Cloud roda **containers paralelos isolados**. Voce delega N tarefas, todas rodam ao mesmo tempo em ambientes separados, voce revisa os PRs no fim.

```bash
# Delegar 3 tarefas em paralelo
codex cloud delegate "implementa endpoint /users" --branch users
codex cloud delegate "implementa endpoint /posts" --branch posts
codex cloud delegate "implementa endpoint /comments" --branch comments

# Voltar mais tarde e revisar
codex cloud status
codex cloud review users
```

### Trade-offs entre as duas abordagens

| | **Claude Code (Agent Teams)** | **Codex (Cloud Workers)** |
|---|---|---|
| Agentes se comunicam? | Sim, via task list compartilhada | Nao, isolados |
| Roda em paralelo? | Limitado (multi-thread local) | Sim, totalmente |
| Coordenacao | Forte (dependencies rastreadas) | Fraca (cada um sozinho) |
| Ideal pra | Refactor grande com sub-tarefas dependentes | Features independentes em paralelo |

---

## SUB-ABA 5 — Hooks (Claude Code primariamente)

### O que e

Hooks sao **scripts disparados em eventos do lifecycle do agente**. Voce define o que roda antes/depois de cada acao do agente.

### Os 26 eventos do Claude Code

> Lista resumida — os principais.

| Evento | Quando dispara | Uso tipico |
|---|---|---|
| `PreToolUse` | Antes de qualquer tool ser usada | Validacao, bloqueio |
| `PostToolUse` | Depois de tool ser usada | Logging, auditoria |
| `PreFileWrite` | Antes de escrever arquivo | Lint, format check |
| `PostFileWrite` | Depois de escrever arquivo | Auto-format, test runner |
| `PreShellCommand` | Antes de comando shell | Bloquear comandos perigosos |
| `PostShellCommand` | Depois de comando shell | Logging |
| `PreSessionStart` | Antes da sessao comecar | Setup ambiente |
| `PostSessionEnd` | Quando sessao termina | Cleanup, sync |
| `OnError` | Quando ha erro | Notificacao, retry |
| ... | ... | ... |

(Lista completa em [Anthropic docs])

### Exemplo: hook que bloqueia comandos perigosos

`.claude/hooks/pre-shell.sh`:
```bash
#!/bin/bash
COMMAND="$1"

# Bloqueia rm -rf /
if echo "$COMMAND" | grep -qE 'rm -rf /(\s|$)'; then
  echo "BLOQUEADO: rm -rf / detectado" >&2
  exit 1
fi

# Bloqueia delecao em producao
if echo "$COMMAND" | grep -q 'DROP TABLE'; then
  echo "BLOQUEADO: DROP TABLE detectado em ambiente production" >&2
  exit 1
fi

exit 0
```

Em `~/.claude/settings.json`:
```json
{
  "hooks": {
    "PreShellCommand": ".claude/hooks/pre-shell.sh"
  }
}
```

### Codex — equivalente: sandbox kernel-level

Codex **nao tem** sistema granular de hooks. Em vez disso, usa **sandbox em nivel de kernel** (Seatbelt no macOS, Landlock + seccomp no Linux):

- **untrusted:** nada permitido alem de leitura
- **on-request:** pede permissao pra cada acao critica
- **never:** sem sandbox (so use em ambiente isolado)

**Trade-off:** menos flexivel que hooks programaveis, mas mais simples e seguro por default.

---

## SUB-ABA 6 — Custom skills

> Aprofunda o que foi visto na Aba 5.

### Quando criar custom skill (vs usar prompt direto)

Criterio: voce **ja repetiu 3 vezes**? Se sim, vira skill. Se nao, fica prompt.

### Skill com scripts (poder maximo)

Quando logica complexa entra em jogo, skill aponta pra script:

`.claude/skills/parse-receita-cnpj/SKILL.md`:
```markdown
---
name: parse-receita-cnpj
description: Parseia arquivo de CNPJ da Receita Federal e gera resumo estatistico
---

# Parse Receita CNPJ

Quando o usuario pedir analise de arquivo CNPJ:

1. Confirma com usuario o caminho do arquivo
2. Roda `scripts/parse.py <arquivo>`
3. Apresenta o resumo gerado em `output.md`
4. Pergunta se quer aprofundar alguma area

## Inputs esperados
- Arquivo CSV ou TXT da Receita Federal

## Outputs garantidos
- Resumo estatistico em markdown
- Top 10 maiores empresas por capital
- Distribuicao por CNAE
- Distribuicao por estado
```

`.claude/skills/parse-receita-cnpj/scripts/parse.py`:
```python
import sys
import duckdb

def parse(filepath):
    conn = duckdb.connect()
    conn.execute(f"CREATE TABLE cnpjs AS SELECT * FROM read_csv_auto('{filepath}')")
    
    # Top 10 por capital
    top_capital = conn.execute("""
        SELECT razao_social, capital_social
        FROM cnpjs
        ORDER BY capital_social DESC
        LIMIT 10
    """).fetchall()
    
    # Por CNAE
    por_cnae = conn.execute("""
        SELECT cnae_principal, COUNT(*) as count
        FROM cnpjs
        GROUP BY cnae_principal
        ORDER BY count DESC
        LIMIT 20
    """).fetchall()
    
    # ... gera output.md
    
if __name__ == "__main__":
    parse(sys.argv[1])
```

### Boas praticas pra skills com scripts

1. **Descricao clara** do que o script faz (input/output)
2. **Caminho relativo** (`scripts/foo.py`, nao `/Users/.../foo.py`)
3. **Trate erros** no script — agente vai ler stderr
4. **Output estruturado** (JSON ou markdown bem formado)
5. **Idempotente** — rodar 2x nao quebra
6. **Documenta dependencias** no SKILL.md (ex: "requer Python 3.11+ e duckdb")

---

## SUB-ABA 7 — Performance

### Eficiencia de tokens — comparativo

| Cenario | Claude Code | Codex |
|---|---|---|
| Tarefa simples (~30 min) | 50-100k tokens | 15-40k tokens |
| Tarefa media (~2h) | 300-600k tokens | 80-200k tokens |
| Refactor grande (~1 dia) | 2-4M tokens | 500k-1.5M tokens |

**Codex consome 2-4x menos tokens** em tarefas equivalentes. **Claude Code produz output mais minucioso** (vence 67% das avaliacoes cegas em qualidade).

### 7 tecnicas pra economizar tokens

#### 1. Global enxuto (regra de ouro da Aba 2)
Skills no global so se voce usa em 80% dos projetos. O resto e local.

#### 2. CLAUDE.md/AGENTS.md curto e potente
Maximo 300 linhas. Mais que isso, voce esta colocando documentacao no lugar de briefing.

#### 3. Use referencias em vez de duplicar contexto
Em vez de colar 200 linhas de codigo no prompt, escreve "Le `src/foo.ts`" e deixa o agente puxar.

#### 4. Limpa contexto entre tarefas grandes
`/clear` ou Ctrl+L entre tarefas independentes. Sessao acumula contexto que nao serve.

#### 5. Use subagents pra tarefas pesadas
Subagent tem contexto proprio. Roda pesquisa, retorna resumo, principal nao polui.

#### 6. Quebra tarefas grandes em pequenas
Tarefa de 4h em 8 sub-tarefas de 30 min. Cada uma com prompt focado.

#### 7. Skills em vez de prompts longos
Padrao repetido vira skill. 1500 tokens de prompt viram 50 tokens de invocacao.

### Tecnicas exclusivas de cada agente

**Claude Code:**
- `/effort` flag pra controlar profundidade
- Plan Mode antes de execucao (mais barato planejar do que refazer)
- Think modes (`think`, `think hard`, `think harder`) — escolhe profundidade

**Codex:**
- Reasoning levels (`low`, `medium`, `high`) na config
- Auto-review mode (revisao em segundo plano nao consome contexto principal)
- Cloud workers (delega pra container, nao consome contexto local)

---

## SUB-ABA 8 — CI/CD

### Integracao com pipelines

Tanto Claude Code quanto Codex podem rodar em **modo headless** (nao-interativo) dentro de pipelines.

### Claude Code em CI

`.github/workflows/claude-review.yml`:
```yaml
name: Claude Code Review

on: [pull_request]

jobs:
  review:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Run Claude review
        run: |
          npx @anthropic-ai/claude-code \
            --headless \
            --instructions "Revise o diff. Foco: bugs, seguranca, performance." \
            --output review.md
        env:
          ANTHROPIC_API_KEY: ${{ secrets.ANTHROPIC_API_KEY }}
      - name: Comment on PR
        uses: marocchino/sticky-pull-request-comment@v2
        with:
          path: review.md
```

### Codex em CI

```yaml
name: Codex Review

on: [pull_request]

jobs:
  review:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Run Codex review
        run: |
          npx @openai/codex \
            --non-interactive \
            --profile review \
            --output review.md
        env:
          OPENAI_API_KEY: ${{ secrets.OPENAI_API_KEY }}
```

### Casos de uso em CI/CD

1. **Auto-review em PRs** — agente revisa diff, comenta no PR
2. **Geracao automatica de changelog** — gera CHANGELOG.md a partir de commits
3. **Documentacao automatica** — atualiza /docs quando codigo muda
4. **Testes generativos** — gera testes pra codigo sem cobertura
5. **Triagem de issues** — categoriza issues novas, sugere labels

### Cuidados

- **Custo escalavel:** cada PR consome tokens. Define orcamento mensal.
- **Falsos positivos:** agente pode reclamar de coisa que e proposital. Nao bloqueia merge sem revisao humana.
- **Secrets:** nunca passa secret real no prompt. Usa env vars.

---

## SUB-ABA 9 — Troubleshooting

### Problema 1 — Agente "se perde" no meio da tarefa

**Sintomas:** comeca bem, depois esquece o que estava fazendo, refaz coisas, contradiz decisao anterior.

**Causa mais provavel:** contexto inchado (Globalzao). Agente esta carregando tanto contexto que nao consegue manter foco.

**Diagnostico:**
1. Quantas skills no global? (mais que 10? ja e demais)
2. CLAUDE.md/AGENTS.md tem mais que 300 linhas? (se sim, corta)
3. Sessao tem mais que 4h sem `/clear`? (se sim, limpa)

**Solucao:** ver Aba 2 (Metodo) — global enxuto, local especifico.

### Problema 2 — Agente faz coisa que voce nao pediu

**Sintomas:** voce pediu A, ele entregou A + B + C. Adicionou dependencia, mudou arquivos nao relacionados, etc.

**Causa:** restricoes nao explicitas no prompt OU CLAUDE.md/AGENTS.md.

**Solucao:**
- Adiciona secao "O que NAO fazer" no CLAUDE.md/AGENTS.md
- No prompt, explicita escopo: "Nao toque em outros arquivos. Nao adicione dep nova."

### Problema 3 — Skills nao sao invocadas automaticamente

**Sintomas:** voce criou skill, mas agente nao usa quando relevante.

**Causa:** descricao da skill esta vaga.

**Diagnostico:**
1. A descricao tem palavras que voce **realmente usaria** no prompt?
2. Voce roda `/skills list` (Codex) ou ve skills carregadas (Claude Code)? Aparece?
3. O `allow_implicit_invocation` esta `true` (default)?

**Solucao:** reescreve descricao com palavras-gatilho. Veja Aba 5.

### Problema 4 — MCP server nao conecta

**Sintomas:** agente nao consegue acessar GitHub/banco/filesystem via MCP.

**Diagnostico:**
1. Server esta no settings.json/config.toml? Path correto?
2. Token/credencial valida?
3. Permissao de filesystem inclui o path requisitado?
4. Roda `npx <server>` standalone — funciona?

**Solucao:** rodar o MCP server isoladamente pra ver erro real. Logs ajudam.

### Problema 5 — Performance degradada (lento)

**Sintomas:** agente demora pra responder. Sessoes ficaram pesadas.

**Causa:** acumulo de contexto + skills demais.

**Solucao:**
- `/clear` entre tarefas
- Reinicia agente
- Audita skills globais
- Ve se ha hooks pesados rodando em todo PreToolUse

### Problema 6 — Agente "alucinou" (inventou API/funcao)

**Sintomas:** agente sugere `lodash.deepClone` (nao existe) ou metodo inventado.

**Causa:** modelo preencheu lacuna sem verificar.

**Prevencao:**
- Em prompts: "Se nao tiver certeza que API existe, verifica primeiro"
- Use MCP filesystem pra confirmar imports
- Sempre roda o codigo antes de aceitar diff

---

## SUB-ABA 10 — Memoria (NOVO)

> Sub-aba inteira nova, vinda da reuniao 04-29.

### O problema

Agente perde contexto entre sessoes. Voce trabalha 3 dias num projeto, no quarto dia abre o agente, e ele "esqueceu" decisoes do dia anterior. Voce explica de novo. E de novo.

**Solucao:** sistema de memoria persistente.

### CloudMem — a solucao validada

**O que e:** servidor MCP que armazena observacoes do agente em um banco vetorial. Agente consulta antes de cada tarefa, recupera memorias relevantes, mantem continuidade.

**Status:** **validado em producao**, recomendado pelo Get It Easy.

**Como funciona:**
1. Durante o trabalho, agente registra observacoes ("decidimos usar Postgres", "padrao de API e camelCase", "cliente prefere copy curto")
2. Observacoes sao indexadas com embeddings semanticos
3. Em nova sessao, agente busca memorias relevantes pra contexto atual
4. Continuidade preservada **sem precisar reler tudo**

**Setup:**

```json
// Em ~/.claude/settings.json (ou ~/.codex/config.toml equivalente)
{
  "mcp_servers": {
    "memory": {
      "command": "npx",
      "args": ["-y", "@cloudmem/server"],
      "env": {
        "MEMORY_STORE": "~/cloudmem-data"
      }
    }
  }
}
```

**Skill complementar pra invocar:**
```markdown
---
name: memoria
description: Salva ou consulta memorias persistentes do projeto via CloudMem
---

# Memoria

## Quando salvar
- Apos decisao arquitetural importante
- Apos descoberta de padrao do cliente
- Apos resolver bug nao-trivial

## Quando consultar
- Inicio de cada sessao em projeto longo
- Ao retomar projeto apos pausa
- Quando perdido sobre decisao anterior
```

### MemPalace — a solucao em observacao

**O que e:** ferramenta nova (lancada 14 abril 2026) que tenta ir alem de memoria simples — usa **semantica + grafos de conhecimento** pra mapear relacoes entre conceitos do projeto.

**Status:** **em observacao** — promissor, mas ainda nao validado pra producao.

**Por que esta no radar:**
- Promete capturar relacoes (X depende de Y, Y é instancia de Z)
- Pode reduzir "alucinacao por falta de contexto" em projetos complexos
- Comunidade ativa, evolucao rapida

**Por que nao recomendamos ainda:**
- Pouca documentacao
- Casos de borda nao mapeados
- Performance varia em projetos grandes
- Quebra de compat entre versoes recentes

**Recomendacao:** **continue usando CloudMem em producao. Acompanhe MemPalace pra validar quando estabilizar.**

### CloudMemSemantic Inject (avancado)

**O que e:** opcao do CloudMem que **injeta automaticamente** observacoes com similaridade semantica no contexto, sem voce pedir.

**Por padrao:** desativado (pra nao inflar contexto).

**Quando ativar:** projetos longos onde voce quer que o agente puxe memoria relevante automaticamente.

**Como ativar:**
```json
{
  "mcp_servers": {
    "memory": {
      "command": "npx",
      "args": ["-y", "@cloudmem/server", "--semantic-inject"],
      "env": {
        "MEMORY_STORE": "~/cloudmem-data",
        "SEMANTIC_THRESHOLD": "0.85"
      }
    }
  }
}
```

**Cuidado:** com threshold baixo, pode injetar muito ruido. Comeca com 0.85 e ajusta.

---

## SUB-ABA 11 — Plugins & Marketplace (NOVO)

> Sub-aba inteira nova, vinda da reuniao 04-29.

### O que e plugin

**Plugin** e uma **skill (ou conjunto de skills) empacotada** pra instalacao via comando, com versioning, atualizacao e dependencias resolvidas automaticamente.

**Vantagem sobre skill solta:**
- Voce instala com 1 comando
- Atualizacao via "reload plugins"
- Versionado (semver)
- Pode ter dependencias declaradas
- Distribuido publicamente ou privadamente

### Anatomia de um plugin

```
meu-plugin/
├── plugin.json          ← metadata
├── skills/              ← skills empacotadas
│   ├── skill-1/
│   │   └── SKILL.md
│   └── skill-2/
│       └── SKILL.md
├── agents/              ← (opcional) agentes
├── hooks/               ← (opcional) hooks
└── README.md
```

### plugin.json — metadata

```json
{
  "name": "blueworld-toolkit",
  "version": "1.0.0",
  "description": "Toolkit pra projetos de comercial intelligence (Blue World pattern)",
  "author": "Otavio / Nucleo Mundial",
  "license": "MIT",
  "homepage": "https://github.com/...",
  "skills": [
    "lead-scoring",
    "cnpj-enrichment",
    "dashboard-html"
  ],
  "dependencies": {
    "duckdb": "^0.9.0",
    "python": ">=3.11"
  },
  "compatibility": {
    "claude-code": ">=2.1.0",
    "codex": ">=1.5.0"
  }
}
```

### Como criar plugin (Claude Code)

```bash
# Cria estrutura
cloud code create-plugin meu-plugin
cd meu-plugin

# Edita plugin.json e adiciona skills
# ...

# Publica no marketplace publico
cloud code publish

# Ou empacota local pra distribuicao manual
cloud code pack
# Gera meu-plugin-1.0.0.tar.gz
```

### Como instalar plugin

```bash
# Plugin publico do marketplace
cloud code install figma-toolkit

# Plugin de URL (privado/customizado)
cloud code install https://github.com/empresa/plugin-privado

# Plugin local (tarball)
cloud code install ./meu-plugin-1.0.0.tar.gz

# Listar instalados
cloud code list-plugins

# Atualizar todos
cloud code reload-plugins
```

### Marketplace proprio (caso de uso avancado)

**Cenario:** voce quer **um marketplace especifico** (ex: marketplace do Get It Easy) que aponta pra repositorios de plugins seus.

**Estrutura:** voce mantem **um repositorio central** que contem indice + apontamentos pra repositorios dos plugins individuais.

```
get-it-easy-marketplace/
├── marketplace.json     ← indice
└── plugins/             ← apontamentos (nao codigo)
    ├── gsp.json
    ├── gsd.json
    └── lead-scoring.json
```

`marketplace.json`:
```json
{
  "name": "Get It Easy Marketplace",
  "version": "1.0.0",
  "plugins_dir": "./plugins"
}
```

`plugins/gsp.json`:
```json
{
  "name": "gsp",
  "repository": "https://github.com/get-it-easy/gsp-plugin",
  "version_constraint": "^1.0.0"
}
```

**Usuario instala o marketplace:**
```bash
cloud code add-marketplace https://github.com/get-it-easy/marketplace
cloud code install gsp  # agora encontra
```

### Plugins privados (caso enterprise)

**Cenario:** cliente corporativo (ex: Carlos da Shift) precisa de plugin com codigo proprietario que nao pode ser publico.

**Solucao:** repositorio Git privado + marketplace privado da empresa.

```bash
# Cliente configura SSH key pra repo privado
cloud code add-marketplace git@github.com:empresa/marketplace-privado.git

# Instala plugin do marketplace privado
cloud code install plugin-cliente-x
```

**Vantagens:**
- Codigo proprietario protegido
- Atualizacoes controladas pela empresa
- Acesso por chave SSH (nao public link)
- Audit trail de quem instalou o que

### Boas praticas pra plugins

1. **Semver rigoroso** — quebra de API → major version
2. **CHANGELOG.md** — usuarios precisam saber o que mudou
3. **Testes** — skills do plugin devem ter testes basicos
4. **Documentacao no README** — quando usar, como configurar, exemplos
5. **Compatibilidade declarada** — qual Claude Code/Codex minimo
6. **Sem segredos no codigo** — nada de token/key hardcoded

### Codex — equivalente

Codex **tambem suporta plugins**, com estrutura ligeiramente diferente (`.codex-plugin.toml` em vez de `plugin.json`). Conceito identico, sintaxe diferente.

```bash
# Codex
codex install plugin-name
codex list-plugins
codex update-plugins
```

---

## CTA FINAL DA ABA

Voce viu o avancado. Aplica:

- **Quer setup automatico com tudo?** → Aba 7 (Quiz personalizado)
- **Quer organizar dia a dia?** → Aba 8 (Cola & Dicas Pro)
- **Quer ver custos?** → Aba 9 (Custos & Planos)
- **Quer recapitular?** → Aba 2 (O Metodo)

---

# Notas pro Claude Code (instrucoes de implementacao)

### Estrutura geral
- Aba MAIS DENSA do site — 11 sub-abas
- Cada sub-aba e independente, navegavel via TOC ou anchors
- TOC fixo a esquerda em desktop (sticky), mobile vira accordion no topo

### Hero (Intro)
- Titulo + lead + lista numerada das 11 sub-abas
- Lista clicavel — leva direto pro anchor

### Cada sub-aba
- Header H2 forte (ex: "Sub-aba 10 — Memoria")
- Indicar quando e nova: badge "NOVO" pra Memoria e Plugins
- Code blocks com botao copy
- Tabelas comparativas mantem padrao das outras abas

### Sub-aba 1 — CLAUDE.md/AGENTS.md
- Diagrama visual da hierarquia 5 niveis (talvez piramide invertida)
- Comparativo lado a lado Claude/Codex

### Sub-aba 2 — settings.json/config.toml
- 2 code blocks lado a lado (em desktop) ou stack (mobile)
- Cores diferentes pra json e toml (highlight)

### Sub-aba 3 — MCP
- Diagrama do fluxo (Agente → MCP Client → MCP Server → Servico)
- Tabela de servers populares
- 2 setups lado a lado

### Sub-aba 4 — Subagents
- Tabela comparativa Agent Teams vs Cloud Workers
- Pode ter diagrama mostrando coordenacao vs paralelismo

### Sub-aba 5 — Hooks
- Tabela dos eventos principais
- Code block do exemplo pre-shell hook
- Bloco em destaque pra trade-off Codex (sandbox em vez de hooks)

### Sub-aba 6 — Custom skills
- Code block grande do exemplo parse-receita-cnpj (real, vindo do contexto BlueAnalytics)
- Lista de boas praticas

### Sub-aba 7 — Performance
- Tabela comparativa de eficiencia em token
- 7 tecnicas em accordion ou cards
- Tecnicas exclusivas separadas por agente

### Sub-aba 8 — CI/CD
- 2 YAMLs lado a lado (GitHub Actions Claude vs Codex)
- Lista de casos de uso
- Cuidados em destaque

### Sub-aba 9 — Troubleshooting
- 6 problemas em accordion
- Cada um com sintomas, diagnostico, solucao
- Links pras outras abas onde resolve

### Sub-aba 10 — Memoria (NOVO)
- Badge "NOVO" no titulo
- 2 cards lado a lado: CloudMem (validado, fundo verde sutil) vs MemPalace (em observacao, fundo amarelo sutil)
- Code block do setup
- Aviso explicito sobre recomendacao

### Sub-aba 11 — Plugins (NOVO)
- Badge "NOVO" no titulo
- Maior sub-aba (e a mais conceitualmente densa)
- Diagrama da estrutura de plugin
- Code blocks de plugin.json, comandos de instalar, marketplace proprio
- Caso enterprise (privados) em destaque

### Performance
- Aba pesada — lazy load por sub-aba
- TOC sticky pra navegacao rapida
- Anchors com smooth scroll

### Acessibilidade
- TOC navegavel por teclado
- Cada sub-aba como landmark `<section>` com aria-label
- Code blocks: aria-label "copyable"
