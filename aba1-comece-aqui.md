# Aba 1 — Comece aqui

## A porta de entrada do toolkit

---

## HERO (topo da pagina)

### Eyebrow (linha pequena acima do titulo)
> Metodo + comunidade + personalizacao em portugues

### Titulo principal (H1)
> # Pare de aprender ferramentas. Aprenda o oficio.

### Subtitulo (lead paragraph)
Em 2026 o problema nao e mais escolher entre Claude Code, Codex ou Cursor. Eles convergem semana a semana. O problema e que ninguem te ensinou a **pensar** com agentes de IA — e e isso que separa quem perde tempo de quem entrega resultado.

### CTAs primarios (dois botoes lado a lado)
- **[ Faco o quiz ]** (link pra Aba 7 — Setup personalizado)
- **[ Quero entender o metodo ]** (link pra Aba 2 — O Metodo)

### Linha de prova social (abaixo dos CTAs)
> Construido em portugues, testado com clientes reais, agnostico de ferramenta. Funciona com Claude Code, Codex, Cursor, e o que vier depois.

---

## SECAO 1 — Bifurcacao: voce e iniciante ou ja programa?

> Duas portas. Mesmo metodo. Linguagem diferente.

### Card A — Iniciante curioso
**"Nunca abri um terminal na vida"**

Voce ouviu falar de vibe coding, viu gente fazendo site sozinho com IA, ficou curioso. Nao sabe nem o que e Node.js. Tudo bem.

**O que voce ganha:**
- Em 2 horas, primeiro projeto rodando
- Manual personalizado pra sua area de atuacao
- Setup automatico (sem voce ter que entender Git agora)
- Zero jargao desnecessario

**[ Comeco por aqui → ]** (leva pra rota iniciante: O que e + quiz simplificado + Do Zero)

### Card B — Dev experiente
**"Programo ha anos, quero parar de queimar token"**

Voce ja usa Claude Code ou Codex no dia a dia. Ja brigou com contexto inchado, ja viu agente "se perder" no meio da tarefa. Quer organizacao profissional, nao tutorial basico.

**O que voce ganha:**
- Metodo completo de organizacao global vs local
- Comparativo Claude Code vs Codex sem fanboyice
- Skills, hooks, MCP, plugins, marketplace
- Anti-patterns que custam token e produtividade

**[ Vou direto ao ponto → ]** (leva pra rota avancada: O Metodo + Stack + Avancado)

---

## SECAO 2 — O que e isso aqui (em uma frase)

> **Get It Easy e o metodo de operar agentes de IA. As ferramentas sao intercambiaveis. Voce fica com o que importa: saber operar.**

Tres camadas:

1. **Fundacao (o metodo)** — mindset, contexto global vs local, organizacao, workflow. Vale pra qualquer agente.
2. **Stack (as ferramentas)** — Claude Code, Codex, Cursor, skills, MCP, plugins. Lado a lado, sem fanatismo.
3. **Personalizacao (o seu caminho)** — quiz que monta seu manual, suas skills, seus projetos. Sob medida.

---

## SECAO 3 — Pre-requisitos (o que voce precisa instalar antes)

Vale tanto pra Claude Code quanto pra Codex. Sao a mesma base.

### Os tres essenciais
| Ferramenta | Pra que serve | Como verificar |
|---|---|---|
| **Node.js** | Instalar e rodar agentes via npm/npx | `node --version` no terminal |
| **Python** | Rodar scripts e skills baseadas em Python | `python --version` ou `python3 --version` |
| **Git** | Versionar projetos e backup no GitHub | `git --version` |

### Os agentes (escolhe um pra comecar, ou os dois)

**Claude Code (Anthropic)**
```bash
npm install -g @anthropic-ai/claude-code
```
Depois: `claude` no terminal pra abrir.

**Codex CLI (OpenAI)**
```bash
npm install -g @openai/codex
```
Depois: `codex` no terminal pra abrir.

### A conta no GitHub (essencial)
Sem GitHub voce perde projeto se o computador queimar. Cria conta gratis em github.com, configura SSH ou login no terminal, e versiona tudo. **Toda pasta de projeto vira um repositorio.** Nao tem desculpa.

> **Se voce nao tem nada disso instalado:** vai na Aba 15 (Do Zero) ou faz o quiz que ele monta o setup pra voce.

---

## SECAO 4 — Os conceitos fundamentais (FAQ adaptado)

8 perguntas que voce **precisa** entender antes de tocar em qualquer agente. Resposta curta, sem enrolacao. Depois aprofunda nas outras abas.

### 1. O que e uma "skill"?
Skill e uma pasta com um arquivo `SKILL.md` (e opcionalmente scripts) que ensina o agente a fazer uma tarefa especifica. Tipo: "como fazer um logo", "como analisar uma planilha de CNPJs", "como revisar codigo Python". O agente le a skill quando precisa, executa, retorna ao fluxo. **E padrao aberto adotado por Claude Code, Codex, Cursor e Aider** — nao e exclusivo de uma ferramenta. Veja Aba 5.

### 2. O que e um "subagent"?
E uma sub-sessao que o agente principal abre pra resolver uma tarefa especifica sem poluir o contexto principal. Tipo um "estagiario" focado: voce pede "pesquisa X", ele pesquisa em paralelo, retorna resumo, libera o agente principal pra continuar. Reduz contexto, acelera trabalho. Veja Aba 2 (Workflow) e Aba 6 (Avancado).

### 3. O que e CLAUDE.md / AGENTS.md?
E o "briefing" do projeto. Um markdown na raiz do projeto que diz pro agente: como esse projeto e organizado, qual o stack, quais convencoes seguir, o que NUNCA fazer. **Claude Code chama de CLAUDE.md. Codex chama de AGENTS.md. O conteudo e quase identico.** Veja Aba 3 (Oficio) e Aba 6 (Avancado).

### 4. O que e MCP (Model Context Protocol)?
Padrao aberto que conecta agentes a ferramentas externas: bancos de dados, APIs, GitHub, Filesystem, Notion. Em vez de o agente "achar" dados na internet, ele consulta direto a fonte autenticada. **Suportado nativamente por Claude Code e Codex.** Veja Aba 6.

### 5. O que e janela de contexto?
E quanta informacao o agente consegue manter na cabeca em uma sessao. Em 2026, Claude Opus tem 1 milhao de tokens (~750 mil palavras), Codex (GPT-5.4) tem 1.05 milhao. Mas **mais contexto nao e melhor automaticamente** — contexto inchado distrai o agente. Por isso o metodo de global vs local importa tanto. Veja Aba 2.

### 6. Como e a primeira sessao com um agente?
Voce abre o terminal, vai na pasta do projeto, digita `claude` ou `codex`, e simplesmente conversa. O agente le os arquivos da pasta, le seu CLAUDE.md/AGENTS.md, le suas skills, e fica pronto. Voce diz o que quer ("crie uma landing page sobre X", "analise esse CSV"), ele planeja, executa, mostra o resultado. **Voce continua no controle** — pode pedir mudanca, voltar passo, mudar abordagem.

### 7. Claude Code ou Codex — qual escolher?
Resposta honesta: **os dois funcionam bem em 2026 e convergem em features**. Codex tem barreira de entrada menor (mais "out of the box"), desktop app polido, consome menos tokens. Claude Code tem mais granularidade pra customizar (26 hooks vs 3 modos), Computer Use mais maduro, output mais minucioso em avaliacoes cegas. **Se voce esta comecando, qualquer um serve. Se quer o melhor de cada, use os dois pra revisao cruzada.** Veja Aba 4 (Stack).

### 8. Vou estar refem de uma empresa?
Nao se voce aprender o metodo aqui. Skills sao padrao aberto. AGENTS.md e padrao aberto. MCP e padrao aberto. Os conceitos de global vs local funcionam em qualquer agente. Voce aprende o oficio uma vez, e migra de ferramenta quando quiser. **Esse e o ponto inteiro do toolkit.**

---

## SECAO 5 — Os numeros (stats em destaque)

> Pequeno bloco visual, tipo cards, com numeros redondos e fontes confiaveis.

- **107+** skills documentadas no toolkit
- **5** ferramentas principais cobertas (Claude Code, Codex, GSD, Spec-Kit, GSP)
- **24+** agentes de exemplo
- **2** padroes interoperaveis (SKILL.md + AGENTS.md/CLAUDE.md)
- **9** abas no toolkit completo
- **4M** desenvolvedores usando Codex semanalmente (fonte: OpenAI, abr/2026)
- **~4%** dos commits publicos no GitHub vem de Claude Code (fonte: SemiAnalysis, fev/2026)

---

## SECAO 6 — Como navegar o toolkit (mapa do site)

Em vez de listar 9 abas em ordem, organiza por **objetivo do usuario**:

### "Quero entender o que e isso tudo"
→ Aba 1 (voce esta aqui) → Aba 2 (O Metodo) → Aba 3 (Oficio)

### "Quero comecar a usar agora"
→ Aba 7 (Setup personalizado — quiz) → Aba 1 (pre-requisitos) → Volta pro quiz

### "Ja uso agente, quero organizar melhor"
→ Aba 2 (O Metodo) → Aba 6 (Avancado) → Aba 8 (Cola & Dicas Pro)

### "Quero comparar Claude Code vs Codex"
→ Aba 4 (Stack) → Aba 9 (Custos & Planos)

### "Quero criar minhas proprias skills"
→ Aba 5 (Skills) → Aba 6 (sub-aba Custom skills)

### "Estou perdido, me ajuda"
→ Aba 7 (faca o quiz, ele resolve)

---

## SECAO 7 — A primeira pergunta que voce devia se fazer

> Bloco em destaque, fundo levemente diferente, voz do toolkit falando direto.

Antes de instalar qualquer coisa, antes de assistir tutorial, antes de gastar token: pergunta isso.

**"O que eu quero que esse agente faca por mim, repetidamente, no proximo ano?"**

Se a resposta e "site pra cliente" — voce vai em uma direcao.

Se e "analise de planilhas grandes" — outra direcao.

Se e "automacao de tarefas chatas no escritorio" — outra direcao.

Se e "aprender a programar do zero" — outra direcao ainda.

**O agente e a ferramenta. Voce e o oficio.** O quiz na Aba 7 ajuda voce a responder essa pergunta com clareza, e te entrega um manual personalizado em cima da resposta.

**[ Faco o quiz agora → ]**

---

## SECAO 8 — Comeco agora (CTA final)

Tres caminhos, dependendo do seu perfil:

**Sou iniciante completo →** Aba 15 (Do Zero) ou quiz na Aba 7
**Tenho alguma experiencia →** Aba 2 (O Metodo) e depois Aba 4 (Stack)
**Sou dev experiente →** Aba 6 (Avancado) e depois Aba 8 (Cola)

Ou, se voce confia na gente: **[ Faz o quiz e a gente te encaminha → ]**

---

## NOTA DE FECHAMENTO (rodape da aba, opcional)

> O metodo aqui foi construido testando com clientes reais, em portugues, no Brasil. Nao e traducao de tutorial gringo. As ferramentas que cobrimos sao as que efetivamente funcionam — testadas, nao teoricas. Se algo aqui te economizou uma tarde de trabalho, considera entrar pra comunidade ou pegar o pacote customizado. E assim que isso aqui sustenta.

---

# Notas pro Claude Code (instrucoes de implementacao)

Quando for converter pra HTML:

1. **Hero** ocupa fold inteiro (acima da dobra). Tipografia grande, espaco respiravel, dois CTAs claros. Usa Syne pro H1.

2. **Cards de bifurcacao (iniciante vs avancado)** sao dois cards lado a lado em desktop, empilhados em mobile. Cada um com cor sutil diferente (talvez tons de ouro mais ou menos saturados — sem inventar paleta nova). Hover destaca. Click navega.

3. **Tabela de pre-requisitos** mantem estilo das outras tabelas do site. Code blocks pros comandos npm install com botao copy.

4. **Os 8 FAQs** podem ser accordion (click expande), em linha vertical. Numero do FAQ em destaque, pergunta como titulo, resposta como paragrafo. Links cruzados pras outras abas em estilo discreto.

5. **Os "numeros em destaque"** sao 7 cards horizontais (carrossel em mobile, grid em desktop). Numero gigante em ouro, label embaixo em DM Sans. Fonte da estatistica como tooltip ou linha pequena.

6. **Mapa do site (objetivo do usuario)** funciona melhor como lista vertical com setas/breadcrumbs visuais — nao cards. Cada linha mostra a sequencia logica.

7. **CTA final tres caminhos** vira tres botoes verticais empilhados ou tres mini-cards clicaveis.

8. Mantem o ticker/marquee no topo da pagina como ja existe.

9. Atalho de teclado: tecla `1` ou `H` (home) sempre volta pra essa aba. Documentar em outro lugar.
