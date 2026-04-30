# Aba 8 — Cola & Dicas Pro

## A pagina que voce abre todo dia

---

## INTRO (topo da aba)

### Eyebrow
> Referencia rapida — atalhos, comandos, fluxos

### Titulo principal
> # Tudo que voce esquece, num lugar so.

### Lead paragraph
Esta aba e **referencia, nao tutorial**. Voce nao le do inicio ao fim — voce procura. Comandos em grid, fluxos de referencia, regras em uma linha, e 18 dicas pro testadas em projeto real. Tudo com equivalente Claude Code **e** Codex lado a lado, porque o oficio e o mesmo.

### Atalho rapido (botao no topo)
> **[ Imprimir / salvar PDF ]** — pra colar na parede ou caderno

---

## SECAO 1 — Setup completo (do zero a primeiro projeto)

### Pre-requisitos universais

```bash
# Node.js (LTS)
node --version    # esperado: v20+ ou v22+

# Python 3.11+
python --version  # ou: python3 --version

# Git
git --version     # esperado: 2.40+
```

Se algum faltar:

| | macOS | Windows | Linux (Debian/Ubuntu) |
|---|---|---|---|
| **Node.js** | `brew install node` | `winget install OpenJS.NodeJS` | `sudo apt install nodejs npm` |
| **Python** | `brew install python` | `winget install Python.Python.3` | `sudo apt install python3 python3-pip` |
| **Git** | `brew install git` | `winget install Git.Git` | `sudo apt install git` |

### Instalar agente

```bash
# Claude Code
npm install -g @anthropic-ai/claude-code

# OU Codex
npm install -g @openai/codex
```

### Configurar Git (uma vez so)

```bash
git config --global user.name "Seu Nome"
git config --global user.email "voce@email.com"
git config --global init.defaultBranch main

# SSH pra GitHub (recomendado)
ssh-keygen -t ed25519 -C "voce@email.com"
# Adiciona ~/.ssh/id_ed25519.pub no github.com/settings/keys
```

### Primeiro projeto (template universal)

```bash
mkdir meu-projeto && cd meu-projeto
git init
git remote add origin git@github.com:voce/meu-projeto.git

# Estrutura local pro agente
mkdir -p .claude/skills    # ou .agents/skills pra Codex
touch CLAUDE.md            # ou AGENTS.md

# Abre o agente
claude                     # ou: codex

# Primeiro commit
git add .
git commit -m "feat: estrutura inicial"
git push -u origin main
```

**Pronto.** Voce tem ambiente funcional em ~5 minutos.

---

## SECAO 2 — Comandos essenciais (grid Claude / Codex)

> Tabela mestre — funcao a funcao, comando equivalente nos dois.

### Sessao

| Funcao | Claude Code | Codex |
|---|---|---|
| Abrir agente | `claude` | `codex` |
| Abrir com instrucao | `claude --instructions <arquivo>` | `codex --profile <perfil>` |
| Sair | Ctrl+D ou `/exit` | Ctrl+D ou `/exit` |
| Limpar tela | Ctrl+L | Ctrl+L |
| Limpar contexto | `/clear` | `/clear` |
| Ver historico | `/history` | `/history` |
| Continuar sessao anterior | `claude --resume` | `codex --resume` |

### Aprovacao e seguranca

| Funcao | Claude Code | Codex |
|---|---|---|
| Pular permissoes (cuidado) | `--dangerously-skip-permissions` | `--full-auto` |
| Modo planejamento | Plan Mode (toggle) | `--profile plan` |
| Sandbox restrito | Hooks `PreToolUse` | `--sandbox untrusted` |
| Sandbox liberado | (default) | `--sandbox never` |

### Skills e plugins

| Funcao | Claude Code | Codex |
|---|---|---|
| Listar skills carregadas | (em tempo real) | `/skills` |
| Invocar skill explicitamente | `$nome-skill` | `$nome-skill` |
| Instalar plugin | `cloud code install <nome>` | `codex install <nome>` |
| Listar plugins | `cloud code list-plugins` | `codex list-plugins` |
| Atualizar plugins | `cloud code reload-plugins` | `codex update-plugins` |

### Subagents

| Funcao | Claude Code | Codex |
|---|---|---|
| Criar subagent | (Agent Teams via CLAUDE.md) | `codex cloud delegate "tarefa"` |
| Status de subagents | (em sessao) | `codex cloud status` |
| Revisar resultado | (em sessao) | `codex cloud review <branch>` |

### Modos de profundidade

| Funcao | Claude Code | Codex |
|---|---|---|
| Pensar pouco | `/effort low` | `reasoning = "low"` (config) |
| Pensar medio | `/effort medium` | `reasoning = "medium"` |
| Pensar muito | `/effort high` ou "think hard" | `reasoning = "high"` |
| Pensar profundamente | "think harder" / "ultrathink" | (max ja e high) |

### Atalhos de teclado (universais nos dois)

| Tecla | Acao |
|---|---|
| Ctrl+L | Limpa a tela |
| Ctrl+D | Sai do agente |
| Ctrl+C | Cancela operacao atual |
| Esc Esc | Cancela tool em execucao |
| Setas ↑↓ | Historico de prompts |
| Tab | Auto-complete em paths |

---

## SECAO 3 — 3 fluxos de referencia (acesso rapido)

> Voce esta no meio de uma tarefa e quer lembrar como executa um fluxo. Estes 3 cobrem 80% dos casos.

### Fluxo A — Bug fix urgente

```
1. /clear  (limpa contexto)
2. Le CLAUDE.md/AGENTS.md (mental)
3. Prompt: contexto + sintoma + reproducao + restricoes (nao expandir escopo)
4. Recebe diagnostico → questiona (nao aceita primeira hipotese)
5. Aplica fix minimo
6. Roda teste manual + automatico
7. Commit atomico: "fix: <descricao curta>"
8. Push + deploy
9. Documenta no PR/issue: causa raiz + fix + teste
```

**Tempo medio:** 30-90 min. Mais que isso, suspeita de causa raiz mais profunda.

### Fluxo B — Feature nova (pequena ou media)

```
1. Define escopo em 2-3 linhas
2. Se > 2h: cria spec curta (Spec-Kit `/spec new`)
3. Le CLAUDE.md/AGENTS.md (atualizou recentemente?)
4. Prompt com 4 pilares: contexto + objetivo + restricoes + formato
5. Pede plano antes de codigo
6. Aprova plano (ou ajusta)
7. Implementa em commits pequenos
8. Roda testes apos cada commit
9. Push + abre PR
10. Auto-review (se configurado em CI)
```

**Tempo medio:** 1-4h.

### Fluxo C — Onboarding em projeto desconhecido

```
1. Clone do repo
2. Le README.md
3. Abre agente na pasta
4. Prompt: "gere mapa mental do projeto"
   - Pontos de entrada
   - Modulos principais e responsabilidades
   - Fluxos principais
   - Top-10 arquivos pra ler primeiro
5. Le os top-10 (na ordem)
6. Roda projeto local (npm install, configurar .env, etc.)
7. Faz pequena alteracao "hello world" pra validar setup
8. Commit + push pra branch propria
```

**Tempo medio:** 1-2h. Depois disso, voce esta produtivo.

---

## SECAO 4 — 8 regras em uma linha (cola na parede)

> Bloco em destaque visual. Lista de 8, numeradas, em 1 linha cada.

1. **Contexto primeiro, prompt depois.**
2. **Pequeno antes de grande.**
3. **Local sobrescreve global.**
4. **Testar antes de confiar.**
5. **Commit atomico (uma mudanca = um commit).**
6. **Re-spec antes de re-codar.**
7. **Skill repete; prompt nao.**
8. **Quando suspeitar de alucinacao, valida.**

---

## SECAO 5 — 18 dicas pro

> Bloco organizado por tema. Cada dica = nome + 1 paragrafo de explicacao + (se aplicavel) comando.

### Categoria 1 — Velocidade

#### 1. Pular permissoes em ambientes confiaveis
Quando voce trabalha em sandbox/Docker isolado, repetir aprovacao a cada comando vira atrito desnecessario.
- Claude Code: `--dangerously-skip-permissions`
- Codex: `--full-auto`

**Cuidado:** **nunca** use em maquina pessoal com dados sensiveis.

#### 2. Esc Esc pra cancelar tool em execucao
Agente comecou a fazer algo errado e voce quer parar **sem matar a sessao**? Aperta Esc duas vezes — cancela so a tool atual, mantem o contexto.

#### 3. Bash inline em prompt
Voce nao precisa explicar "roda isso e me diz o resultado." Cola o comando entre crases:
```
Roda `npm test` e analisa as falhas.
```
Agente entende que e pra executar.

#### 4. Feedback loops (uma mudanca → testa → ajusta)
Em vez de "implementa tudo", peca: "implementa passo 1, mostra resultado, espera meu OK, segue pro 2."
- Reduz retrabalho
- Voce mantem controle
- Bug aparece cedo, custa pouco pra corrigir

### Categoria 2 — Qualidade

#### 5. Plan Mode antes de execucao (Claude Code)
Pra qualquer tarefa nao-trivial, ativa Plan Mode primeiro.
- Custo: 1 prompt extra (planejamento)
- Beneficio: voce pega abordagem errada antes de gastar token implementando

#### 6. Think modes pra problemas complexos
Quando o problema e dificil de verdade, sinaliza profundidade:
- "think" — pensamento basico
- "think hard" — pensamento estruturado
- "think harder" / "ultrathink" — analise profunda

Custo: mais token. Beneficio: melhor solucao em problemas complicados.

#### 7. Auto-review com agente diferente
Combo poderoso: **Claude escreve, Codex revisa** (ou vice-versa). Custo dobra, mas pega 53-80% mais bugs que solo. Vale pra projeto pago/critico.

#### 8. /effort pra controlar profundidade (Claude Code)
- `/effort low` — tarefa simples, otimiza pra rapido/barato
- `/effort medium` — default, equilibrado
- `/effort high` — problema dificil, otimiza pra qualidade

### Categoria 3 — Contexto

#### 9. /clear entre tarefas independentes
Sessao acumula contexto. Tarefa 1 polui contexto da Tarefa 2 (que nao tem nada a ver). `/clear` ou Ctrl+L resolve.

**Regra pratica:** terminou tarefa? Limpa antes da proxima.

#### 10. CLAUDE.md/AGENTS.md curto e direto
Maximo 300 linhas. Mais que isso, voce esta colocando documentacao no lugar de briefing. Documentacao vai em `/docs/`.

#### 11. Limpar global periodicamente
Toda 2-3 meses, audita seu `~/.claude/skills/` ou `~/.codex/skills/`. Skill que voce nao usou em 3 meses vai pro cemiterio.

#### 12. Subagent pra pesquisa pesada
Em vez de o agente principal ler 50 arquivos (e poluir contexto), delega: "Subagent: leia /docs e me retorne resumo das decisoes arquiteturais." Volta com 200 tokens em vez de 50k.

### Categoria 4 — Integracao

#### 13. LSP plugins (Claude Code)
Conecta o agente ao Language Server do seu editor. Vantagem: agente "ve" os mesmos erros e sugestoes que voce ve no VS Code/JetBrains. Reduz alucinacao em codigo tipado.

#### 14. GitHub App (Claude Code)
Em vez de PAT (Personal Access Token), instala GitHub App da Anthropic. Vantagens:
- Permissoes granulares por repo
- Audit trail de acoes do agente
- Token rotativo automatico

#### 15. Docker pra ambientes de risco
Quando experimenta com codigo nao-confiavel ou pacote novo, **roda o agente dentro de Docker**. Isolamento completo, "blast radius" zero.

```bash
docker run -it --rm -v $(pwd):/workspace node:22 bash
# Dentro do container:
npm install -g @anthropic-ai/claude-code
claude
```

#### 16. Worktrees pra trabalhar em paralelo
Voce pode ter **multiplas branches checkout simultaneamente** com `git worktree`. Cada worktree e uma pasta separada, com agente proprio.

```bash
git worktree add ../meu-projeto-feature feature-branch
cd ../meu-projeto-feature
claude  # agente nessa branch sem afetar a principal
```

Codex tem isso nativo (Codex Cloud trabalha em worktrees automaticos).

### Categoria 5 — Experimentos avancados

#### 17. Browser interno (Codex desktop)
Codex desktop tem **browser embarcado**. Voce nao precisa alt-tab pra checar resultado de uma URL — agente abre internamente, le, retorna. Reduz contexto e fricao.

#### 18. Cloud workers pra refactor paralelo
Tem 30 endpoints pra atualizar do mesmo jeito? Em vez de fazer um por um, delega 10 ao mesmo tempo no Codex Cloud. Containers paralelos, voce revisa todos os PRs no fim do dia.

```bash
codex cloud delegate "atualiza endpoint /users com novo padrao" --branch users
codex cloud delegate "atualiza endpoint /posts com novo padrao" --branch posts
codex cloud delegate "atualiza endpoint /comments com novo padrao" --branch comments
# ... 7 mais
```

---

## CTA FINAL DA ABA

Voce viu a cola. Aplica:

- **Quer dominar o metodo completo?** → Aba 2 (O Metodo)
- **Quer ferramentas avancadas?** → Aba 6 (Avancado)
- **Quer ver custos?** → Aba 9 (Custos & Planos)
- **Quer setup automatico?** → Aba 7 (Quiz personalizado)

---

# Notas pro Claude Code (instrucoes de implementacao Aba 8)

### Estrutura geral
- Aba de referencia — UX foca em **busca e localizacao rapida**
- Botao "Imprimir/PDF" no topo (CSS @media print otimizado)
- Sticky table of contents pra navegacao rapida

### Setup completo (Secao 1)
- Code blocks numerados com botao copy
- Tabela responsiva pra "Por sistema operacional"

### Comandos essenciais (Secao 2)
- 6 tabelas (Sessao, Aprovacao, Skills, Subagents, Profundidade, Atalhos)
- Tabela responsiva — em mobile: cada linha vira card
- Funcao "buscar comando" no topo (input que filtra todas as tabelas)

### 3 fluxos (Secao 3)
- 3 cards/accordions
- Listas numeradas grandes, legiveis
- "Tempo medio" em destaque visual

### 8 regras em uma linha (Secao 4)
- Bloco com fundo destacado (talvez ouro suave)
- Numeros gigantes
- Layout: 2 colunas em desktop, 1 em mobile

### 18 dicas pro (Secao 5)
- Organizado em 5 categorias (cards/accordions)
- Cada dica como sub-card com numero, titulo, paragrafo, (opcional) code block
- Em mobile: stack vertical

### Print/PDF
- @media print: oculta navegacao, expande todos accordions, formato A4
- Pessoa salva o PDF e imprime pra ter referencia fisica

### Acessibilidade
- Tabelas com headers semanticos
- Code blocks aria-label "copyable"
- Atalho de teclado: `8` ou `R` (referencia) volta pra essa aba
