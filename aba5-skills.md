# Aba 5 — Skills

## O padrao aberto da industria de agentes em 2026

---

## INTRO (topo da aba)

### Eyebrow
> Padrao aberto adotado por Anthropic, OpenAI, Cursor e Aider

### Titulo principal
> # Skill nao e truque de uma ferramenta. E o oficio empacotado.

### Lead paragraph
Em 2026, skill virou **o padrao da industria** pra encapsular conhecimento e fluxo de trabalho de agentes de IA. Claude Code le `SKILL.md`. Codex le `SKILL.md`. Cursor le. Aider le. Voce escreve **uma vez** e funciona em qualquer harness. Isso muda tudo: aprender a criar e organizar skills nao e investir em uma plataforma — e investir em uma habilidade portavel que vai te servir nos proximos 5 anos, em qualquer agente que ainda vai aparecer.

---

## SECAO 1 — O que e uma skill (em 2 minutos)

Skill e uma **pasta com um arquivo `SKILL.md`** que ensina o agente a executar uma tarefa especifica.

```
minha-skill/
├── SKILL.md          ← descricao + instrucoes
├── scripts/          ← (opcional) codigo executavel
│   └── helper.py
└── references/       ← (opcional) docs/exemplos
    └── exemplo.json
```

O agente le o `SKILL.md` quando precisa, segue as instrucoes, executa scripts se houver, retorna ao fluxo principal.

### Por que skill funciona melhor que prompt direto

| | **Prompt direto** | **Skill** |
|---|---|---|
| Reusabilidade | Voce reescreve toda vez | Escreve uma vez, usa sempre |
| Consistencia | Varia conforme voce digita | Constante |
| Compartilhamento | Copia e cola entre pessoas | Versiona via Git |
| Curadoria | So voce sabe o que funciona | Time todo se beneficia |
| Evolucao | Voce esquece o que mudou | Versiona em commit |

### Dois tipos de skill

**Instructions-only (so texto):** o `SKILL.md` tem todas as instrucoes em prosa/bullets. O agente segue. **Maioria das skills e isso.**

**Com scripts:** o `SKILL.md` aponta pra codigo (`scripts/foo.py`) que o agente executa pra obter resultado deterministico. **Util quando precisa de logica complexa, conexao com API, ou comportamento garantido.**

---

## SECAO 2 — Anatomia do SKILL.md

### Estrutura minima (10 linhas)

```markdown
---
name: commit-padrao
description: Formata mensagens de commit no padrao do projeto (conventional commits)
---

# Commit Padrao

Quando o usuario pedir pra commitar, formate a mensagem assim:

- Tipo: feat | fix | docs | refactor | test | chore
- Escopo opcional entre parenteses
- Descricao curta no imperativo, sem ponto final
- Body opcional em paragrafos separados

Exemplo: `feat(auth): adiciona login via Google`
```

So isso. **Nome, descricao, instrucoes.** Funciona em Claude Code e Codex sem mudanca.

### Estrutura completa

```markdown
---
name: nome-da-skill              # obrigatorio
description: descricao curta     # obrigatorio (e o que dispara invocacao implicita)
allow_implicit_invocation: true  # opcional (default true)
---

# Titulo legivel

## Quando usar
- Cenario 1
- Cenario 2

## Como executar
1. Passo 1
2. Passo 2
3. Passo 3

## Inputs esperados
- input_a: tipo (descricao)
- input_b: tipo (descricao)

## Outputs garantidos
- Formato do output

## Pegadinhas
- Cuidado com X
- Sempre validar Y

## Scripts disponiveis
- `scripts/parse.py` — usa quando precisar de Z
- `scripts/format.sh` — usa pra W

## Referencias
- `references/exemplo-input.json`
- `references/exemplo-output.json`
```

### Frontmatter — os campos importantes

**`name`** (obrigatorio): identificador unico. Use kebab-case. Ex: `analise-csv`, `parser-pdf`, `commit-padrao`.

**`description`** (obrigatorio): **a parte mais critica**. E isso que faz o agente decidir se invoca a skill quando voce pede algo. Escreve com palavras-gatilho que voce realmente usaria.

**Ruim:** `"Skill que faz analise"`
**Bom:** `"Analisa arquivo CSV e gera resumo estatistico (media, mediana, outliers, valores faltantes). Uso: dados tabulares, planilhas, exports de banco."`

**`allow_implicit_invocation`** (opcional): se `true` (default), o agente pode invocar a skill sozinho quando matchear a descricao. Se `false`, so funciona quando voce chama explicitamente (`$nome-da-skill`).

---

## SECAO 3 — Como cada agente descobre skills

### Claude Code
Procura skills em camadas hierarquicas:

| Camada | Localizacao | Escopo |
|---|---|---|
| Sistema | `/usr/local/share/claude/skills/` | Toda maquina |
| Admin | `/etc/claude/skills/` | Politicas org |
| Usuario | `~/.claude/skills/` | Voce |
| Projeto | `<projeto>/.claude/skills/` | Esse projeto |
| Arvore | `<subpasta>/.claude/skills/` | Subdiretorios |

Mais especifico vence menos especifico (em conflito de nome).

### Codex
Procura skills em duas raizes:

| Localizacao | Escopo |
|---|---|
| `~/.codex/skills/` | Voce (global) |
| `.agents/skills/` em qualquer pasta da raiz do repo ate `pwd` | Local (per-repo) |

Codex **nao mescla** skills com mesmo nome — ambas aparecem no seletor.

### A regra portavel
A pasta muda (`.claude/skills` vs `.agents/skills`). O conteudo dentro **nao muda**. Voce pode manter os dois lados a lado no mesmo projeto:

```
meu-projeto/
├── .claude/
│   └── skills/         ← Claude Code le aqui
│       └── analise-csv/
│           └── SKILL.md
└── .agents/
    └── skills/         ← Codex le aqui
        └── analise-csv/   ← mesma skill, mesmo SKILL.md
            └── SKILL.md
```

Truque: faz uma pasta unica e usa **symlink**. Voce edita um arquivo, ambos os agentes leem.

---

## SECAO 4 — Crie sua primeira skill em 10 minutos

> Tutorial agnostico. Funciona em Claude Code OU Codex.

Vamos criar a skill `commit-padrao` (a do exemplo da Secao 2). Ela formata mensagens de commit no padrao conventional commits.

### Passo 1 — Cria a estrutura
```bash
# Pra Claude Code:
mkdir -p .claude/skills/commit-padrao

# Pra Codex:
mkdir -p .agents/skills/commit-padrao
```

### Passo 2 — Cria o SKILL.md
```bash
# Substitua .claude por .agents conforme seu agente
touch .claude/skills/commit-padrao/SKILL.md
```

Cole o conteudo:

```markdown
---
name: commit-padrao
description: Formata mensagens de commit no padrao conventional commits do projeto
---

# Commit Padrao

Quando o usuario pedir pra commitar, formate a mensagem assim:

## Estrutura
\`<tipo>(<escopo opcional>): <descricao>\`

## Tipos validos
- **feat**: nova feature
- **fix**: correcao de bug
- **docs**: mudanca de documentacao
- **refactor**: refactor sem mudanca de comportamento
- **test**: adicionar/modificar testes
- **chore**: mudancas de build/config/deps

## Regras
- Descricao no imperativo presente: "adiciona", nao "adicionado"
- Sem ponto final
- Maximo 72 caracteres na primeira linha
- Body opcional em paragrafos separados (com 2 newlines)

## Exemplos
- \`feat(auth): adiciona login via Google\`
- \`fix(api): corrige timeout em /users/sync\`
- \`docs: atualiza README com instrucoes de deploy\`
```

### Passo 3 — Reinicia o agente
```bash
# Sai e abre de novo
claude    # ou: codex
```

Pra Codex, pode tambem rodar `/skills` no chat pra ver as skills disponiveis.

### Passo 4 — Testa
No agente, manda:
```
Faz um commit dessas mudancas. Adicionei autenticacao via Google.
```

Se a skill foi descoberta, o agente vai usar o formato `feat(auth): adiciona login via Google` automaticamente. Se nao, voce pode invocar explicitamente:

```
$commit-padrao
```

### Passo 5 — Versiona
```bash
git add .claude/skills/commit-padrao/    # ou .agents/skills/...
git commit -m "feat: adiciona skill commit-padrao"
git push
```

Pronto. Time todo agora tem essa skill.

---

## SECAO 5 — As 4 ferramentas auxiliares

> Mantem formato problema/solucao do site atual. Cores: GSD roxo, Spec-Kit verde, Superpowers ambar, GSP rosa.

Agora que voce sabe o que e skill e como criar uma, vamos ver as 4 ferramentas auxiliares maduras que ja entregam dezenas de skills prontas.

### GSD — Get Shit Done
**Cor:** roxo
**Cobertura:** Claude Code (primariamente) — skills portaveis pra Codex com adaptacao
**Tipo:** repositorio de skills
**Quantos comandos:** 6 principais

**Problema que resolve:** voce abre o agente de manha e nao sabe por onde comecar. Tem 12 tarefas no backlog do cliente, 4 pendencias do dia anterior, 1 bug em producao. Sem rotina, voce gasta 1h so decidindo o que fazer.

**Solucao:** GSD adiciona **gerencia de tarefa nativa** dentro do agente. Voce conversa com o agente como se fosse seu PM:

**Comandos principais:**
1. `/task new <descricao>` — cria tarefa
2. `/task list` — lista tarefas pendentes
3. `/task done <id>` — marca como concluida
4. `/task focus <id>` — entra em modo foco numa tarefa
5. `/branch sync` — sincroniza branch com main
6. `/status` — relatorio do projeto

**Quando usar:**
- Projetos com mais de 3-4 tarefas paralelas
- Trabalho de freelancer com multiplos clientes
- Time pequeno sem ferramenta dedicada (Jira, Linear)

**Quando NAO usar:**
- Time ja com Linear/Jira maduro
- Projeto pessoal pequeno (overhead)

**[Link GitHub do GSD]**

---

### Spec-Kit
**Cor:** verde
**Cobertura:** Claude Code + Codex (skills portaveis)
**Tipo:** repositorio de skills (SDD framework)
**Quantos comandos:** 5 principais

**Problema que resolve:** voce pede "constroi sistema de notificacoes" e o agente entrega algo que nao bate com o que voce queria. **Razao:** sua especificacao mental nunca virou texto. Agente preencheu lacunas com suposicao.

**Solucao:** Spec-Kit forca um fluxo de spec antes do codigo. Voce escreve a spec primeiro. Agente le. Implementa de acordo. Resultado bate.

**Comandos principais:**
1. `/spec new <feature>` — gera spec a partir de ideia
2. `/spec review` — valida spec antes de implementar
3. `/spec expand` — expande RFs e RNFs
4. `/spec to-tasks` — quebra spec em tarefas executaveis
5. `/spec validate` — checa se implementacao bate com spec

**Quando usar:**
- Tarefas grandes (> 2h estimado)
- Trabalho pra cliente (precisa documentar decisao)
- Time colaborativo (spec vira contrato)

**Quando NAO usar:**
- Bug fix urgente (overhead atrapalha)
- Prototipo de 30 minutos

**[Link GitHub do Spec-Kit]**

---

### Superpowers
**Cor:** ambar
**Cobertura:** Claude Code (ecossistema mais maduro)
**Tipo:** plugin instalavel via marketplace
**Quantos comandos:** 7 + install

**Problema que resolve:** comandos comuns ficam verbosos. Voce digita "ajuda eu a debugar isso seguindo o padrao X..." de novo e de novo. Cada vez voce escreve diferente. Resultado varia.

**Solucao:** Superpowers e um pacote de slash commands prontos que encapsulam padroes comuns. Voce digita 2-3 caracteres, ele expande pro prompt completo (e otimizado).

**Comandos principais:**
1. `/debug` — fluxo de debug estruturado (pergunta sintoma, hipoteses, valida)
2. `/refactor` — refactor com criterios explicitos
3. `/explain` — explicacao em camadas (alto nivel → detalhe)
4. `/test` — gera testes pra codigo selecionado
5. `/review` — revisao critica de codigo
6. `/plan` — planejamento antes de codar
7. `/doc` — gera documentacao estruturada

**Install:**
```bash
# No marketplace de plugins do Claude Code
/plugin install superpowers
```

**Quando usar:**
- Voce ja tem fluxo definido e quer atalho
- Iniciante que ainda nao escreve prompts otimizados
- Quem cansou de redigitar mesma estrutura

**Quando NAO usar:**
- Voce precisa de prompts altamente customizados pra contexto especifico

**[Link GitHub do Superpowers]**

---

### GSP — Get Sheet Pretty (showcase)
**Cor:** rosa
**Cobertura:** Claude Code primariamente; algumas skills funcionam em Codex
**Tipo:** repositorio de skills (design system completo)
**Quantos comandos:** 20+ skills organizadas em pipeline

**Esse e o caso de skill madura mais completo do toolkit. Vale uma secao propria.**

**Vai pra Secao 6 ↓**

---

## SECAO 6 — GSP em detalhe (o caso de skill madura)

> Esta secao e a antiga Aba 12 (Design) reposicionada como showcase de skill avancada.

### O problema que GSP resolve

Designer freelancer brasileiro recebe brief de cliente: "preciso de logo, identidade, site, deck pra investidor, posts pra Instagram, e um e-mail de lancamento."

Sem GSP: voce iterar com IA item por item, gastando 80% do tempo em ajuste visual, perdendo coerencia entre as pecas, e entregando em 2-3 semanas.

Com GSP: voce roda o pipeline. Em **dias** tem entrega coerente, profissional, com identidade unica.

### Como funciona — Dual Diamond

GSP organiza o trabalho em **dois diamantes** sequenciais:

#### Diamante 1 — Descobrir
Convergencia → divergencia → convergencia. **O agente entende o cliente antes de produzir.**

1. **Brief inicial:** o agente faz 12-15 perguntas curtas (tom, publico, valores, referencias). Voce responde em conversacao.
2. **Sintese:** agente sintetiza em 1 paragrafo: "Estou entendendo que vc quer X pra publico Y com tom Z. Confirmar?"
3. **Refinamento:** voce ajusta. Agente atualiza sintese.
4. **Convergencia em direcao criativa:** 3 propostas de territorio criativo. Voce escolhe uma.

#### Diamante 2 — Entregar
Implementacao do territorio escolhido em **8 fases**:

1. **Naming** — gera nomes alinhados com territorio (se aplicavel)
2. **Logo** — concepcao + 5 variacoes + selecao + refinamento
3. **Identidade** — paleta, tipografia, voz, principios visuais
4. **Brand book** — documento PDF consolidado
5. **Aplicacoes web** — landing page, copy, hero, secoes
6. **Aplicacoes deck** — pitch deck (10-15 slides)
7. **Aplicacoes social** — kit de posts (5-10 templates)
8. **Aplicacoes email** — newsletter, transacionais, lancamento

**Cada fase e uma skill independente.** Voce pode rodar so a que precisa.

### Setup rapido vs setup completo

**Setup rapido (5 minutos):**
```bash
# Cria estrutura local
mkdir -p .claude/skills/gsp
# Copia o starter
curl -L https://github.com/[gsp-repo]/starter > .claude/skills/gsp/SKILL.md
```

Pronto. Voce tem uma skill `gsp` que dispara o pipeline.

**Setup completo (30 minutos):**
- Clona o repositorio inteiro do GSP
- Customiza o territorio criativo padrao pro seu cliente
- Adiciona skills pais (uma pra cada cliente recorrente)
- Configura templates personalizados
- Faz primeiro projeto teste

### Os 20+ comandos do GSP

> Em formato de tabela ou cards organizados por fase

**Fase 1 — Naming:**
- `gsp-name-generate` — gera 20 nomes alinhados
- `gsp-name-validate` — checa se nome ja existe (busca + dominio)
- `gsp-name-evolve` — ajusta nome escolhido

**Fase 2 — Logo:**
- `gsp-logo-concepts` — 5 conceitos visuais
- `gsp-logo-render` — renderiza concept em SVG
- `gsp-logo-variations` — variacoes (horizontal, vertical, simbolo, monocromatico)

**Fase 3 — Identidade:**
- `gsp-palette` — paleta primaria + secundaria + neutros
- `gsp-typography` — combinacao de fontes (display + body + mono)
- `gsp-voice` — tom de voz, exemplos do/dont
- `gsp-principles` — principios visuais documentados

**Fase 4 — Brand book:**
- `gsp-brandbook` — gera PDF consolidado
- `gsp-brandbook-export` — exporta assets em pasta organizada

**Fase 5 — Web:**
- `gsp-landing` — landing page completa
- `gsp-copy` — copy hero + secoes
- `gsp-hero` — hero section especifica

**Fase 6 — Deck:**
- `gsp-deck` — pitch deck completo
- `gsp-slide` — slide individual

**Fase 7 — Social:**
- `gsp-social-kit` — kit de templates
- `gsp-post` — post individual

**Fase 8 — Email:**
- `gsp-newsletter` — newsletter
- `gsp-transactional` — emails do app (welcome, reset, etc.)

### Quando usar GSP

- Trabalho de identidade visual completo (logo + identidade + aplicacoes)
- Cliente novo recorrente (vale investir no setup completo)
- Voce e designer/agencia que entrega "tudo"

### Quando NAO usar GSP

- Voce so precisa de uma peca isolada (overkill)
- Cliente ja tem identidade definida (use partes especificas, nao o pipeline todo)
- Projeto interno simples

### Antes de GSP / Depois de GSP

| | **Sem GSP** | **Com GSP** |
|---|---|---|
| Tempo medio identidade completa | 2-3 semanas | 3-5 dias |
| Coerencia entre pecas | Variavel | Alta |
| Documentacao gerada | Manual / nao gerada | Automatica (brand book) |
| Reusabilidade | Cada projeto comeca do zero | Setup customizado por cliente |
| Custo de revisao | Alto (cada peca em isolado) | Baixo (territorio ja validado) |

**[Link GitHub do GSP]**

---

## SECAO 7 — Combinacoes poderosas (workflows multi-skill)

Skills funcionam ainda melhor combinadas. Aqui os workflows mais usados:

### Workflow 1 — Projeto solo (GSD + Spec-Kit)
**Cenario:** voce e dev solo trabalhando em projeto medio.

**Fluxo:**
1. `/spec new <feature>` (Spec-Kit) — cria a spec
2. `/spec to-tasks` (Spec-Kit) — quebra em tarefas
3. `/task new <tarefa>` (GSD) — registra cada tarefa
4. `/task focus <id>` (GSD) — entra em foco
5. Implementa
6. `/task done <id>` (GSD)
7. Repete

**Resultado:** voce nao perde tarefa nem trabalha sem spec.

### Workflow 2 — Iniciante acelerado (Superpowers + Spec-Kit)
**Cenario:** voce esta aprendendo, ainda escreve prompt vago.

**Fluxo:**
1. `/plan` (Superpowers) — agente te ajuda a estruturar antes de codar
2. `/spec new <feature>` (Spec-Kit) — formaliza a ideia
3. `/explain` (Superpowers) — pra entender codigo existente
4. `/refactor` (Superpowers) — pra melhorar conforme aprende
5. `/test` (Superpowers) — gera testes
6. `/review` (Superpowers) — revisa antes de commitar

**Resultado:** voce escreve menos, aprende mais, codigo sai melhor.

### Workflow 3 — Designer freelancer (GSP + GSD)
**Cenario:** voce entrega identidade visual pra cliente novo.

**Fluxo:**
1. `/task new <projeto cliente X>` (GSD)
2. `gsp-name-generate` (GSP)
3. `gsp-logo-concepts` → `gsp-logo-render` (GSP)
4. `gsp-palette` + `gsp-typography` (GSP)
5. `gsp-brandbook` (GSP) — gera entregavel principal
6. `gsp-landing` ou `gsp-deck` conforme escopo
7. `/task done` (GSD)

**Resultado:** entrega completa em dias com coerencia.

### Workflow 4 — Time profissional (todas combinadas)
**Cenario:** time de 5-10 pessoas, projeto serio.

**Fluxo permanente:**
- Spec-Kit como base de toda feature
- GSD pra gerencia diaria
- Superpowers pra atalhos individuais
- GSP se time tem componente visual
- Skills proprias do time pra padroes especificos

**Resultado:** time alinhado, padroes consistentes, onboarding rapido pra novo membro.

---

## SECAO 8 — Como criar e distribuir suas proprias skills

### Nivel 1 — Skill local (so pro projeto)
Mora em `<projeto>/.claude/skills/` ou `<projeto>/.agents/skills/`. Versionada com o codigo. Time todo recebe via Git.

**Quando usar:** padrao especifico desse projeto.

### Nivel 2 — Skill pessoal (so pra voce)
Mora em `~/.claude/skills/` ou `~/.codex/skills/`. So existe na sua maquina.

**Quando usar:** padroes pessoais (tom de email, atalhos individuais).

### Nivel 3 — Skill de time (compartilhada via Git)
Repositorio dedicado com skills. Time clona local, faz symlink pro `.claude/skills/` ou `.agents/skills/`.

**Quando usar:** padroes que valem pra todos os projetos do time.

### Nivel 4 — Skill publica (plugin no marketplace)
Empacota skills em um plugin. Publica via `cloud code create-plugin` (Claude Code) ou no registry do Codex. Usuarios instalam via comando.

**Quando usar:** voce tem skill madura que serve a muita gente. (Detalhes na Aba 6 — Avancado, secao Plugins.)

---

## SECAO 9 — A regra de ouro pra criar skills

> Bloco final da aba. Sintese pratica.

Pergunta antes de criar uma skill nova:

### 1. Voce ja repetiu isso 3 vezes?
Se nao, ainda e tarefa pontual. Nao vira skill ainda.

### 2. A descricao seria reconhecivel pelo agente?
Se sua descricao e generica ("Skill que faz X"), nao funciona. **A descricao precisa ter palavras que voce usaria no prompt.**

### 3. O passo-a-passo cabe em 50-100 linhas?
Skill muito grande dilui o foco. Quebra em multiplas skills relacionadas.

### 4. Ela serve pra mais de um projeto?
Se sim → skill global. Se nao → skill local.

### 5. Voce conseguiria explicar em 30 segundos pro time?
Se nao consegue, ainda nao esta clara. Refina o `SKILL.md` ate conseguir.

**Skill boa = 1 trabalho, 1 descricao reconhecivel, instrucoes claras, 50-100 linhas, fim.**

---

## CTA FINAL DA ABA

Voce viu skills. Agora aplica:

- **Quer aprender a criar plugins (skills empacotadas)?** → Aba 6 (Avancado)
- **Quer setup pronto com skills?** → Aba 7 (Quiz personalizado)
- **Quer ver tudo na pratica?** → Aba 2 (O Metodo)
- **Quer atalhos pra dia a dia?** → Aba 8 (Cola & Dicas Pro)

---

# Notas pro Claude Code (instrucoes de implementacao)

### Estrutura geral
- Aba longa (similar a Aba 3 e 4 em densidade)
- 9 secoes claras
- Mistura conceito + tutorial + showcase

### Hero (Intro)
- Titulo forte que reposiciona skills (nao e truque do Claude Code)
- Lead enfatiza padrao aberto da industria
- Sem CTA primario (a aba ja e o conteudo)

### Tabela "Por que skill funciona melhor que prompt direto" (Secao 1)
- Tabela 2 colunas, 5 linhas
- Visual limpo, sem cor de fundo nas celulas

### Code blocks (varias secoes)
- Mantem styling de monospace + JetBrains Mono
- Botao copy em todos
- Syntax highlighting pra markdown e bash

### Estrutura completa do SKILL.md (Secao 2)
- Code block grande
- Cada campo do frontmatter explicado abaixo

### Tabelas de descoberta (Secao 3)
- 2 tabelas (Claude Code + Codex)
- Tabela final ilustrando as duas pastas lado a lado em estrutura de arvore

### Tutorial passo-a-passo (Secao 4)
- Steps numerados grandes
- Cada step com code block do comando + explicacao
- "Pronto" no final como momento de celebracao

### 4 ferramentas auxiliares (Secao 5)
- Cards padronizados (manter formato do site atual)
- Cores definidas (GSD roxo, Spec-Kit verde, Superpowers ambar, GSP rosa)
- Cada card com: tipo, cobertura, problema, solucao, comandos, quando usar / nao usar, link GitHub
- GSP virtualmente vazio (apenas teaser) com "Vai pra Secao 6 ↓"

### GSP em detalhe (Secao 6 — esta e a maior secao)
- Esta e a antiga Aba 12 (Design) reposicionada
- Layout pode usar padroes visuais especificos:
  - Dual Diamond: 2 diamantes em SVG horizontal lado a lado
  - 8 fases: timeline horizontal com 8 nodes (em mobile, vertical)
  - 20+ comandos: tabela ou grid organizado por fase
  - "Antes/Depois": tabela comparativa
- Investe mais aqui — e o "showcase"

### Workflows combinados (Secao 7)
- 4 workflows como cards ou accordions
- Cada um com fluxo numerado
- Em mobile: empilha verticalmente

### Niveis de distribuicao (Secao 8)
- 4 cards numerados (1 → 4) mostrando progressao
- "Quando usar" em destaque pra cada nivel

### Regra de ouro pra criar skills (Secao 9)
- 5 perguntas em formato Q&A
- Resposta abaixo de cada
- Frase final em destaque visual

### Acessibilidade
- Code blocks com aria-label "copyable"
- Tabelas com headers semanticos
- Tutorial com landmarks pra screen reader

### Performance
- GSP secao e pesada — considerar lazy load
- Imagens/diagramas (Dual Diamond, pipeline 8 fases) como SVG inline
