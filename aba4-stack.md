# Aba 4 — Stack

## As ferramentas que fazem o trabalho (sem fanatismo)

---

## INTRO (topo da aba)

### Eyebrow
> Stack 2026 — atualizado mensalmente

### Titulo
> # A stack certa nao tem time. Tem objetivo.

### Lead
A guerra Claude Code vs Codex e besteira. Os dois sao bons. Eles convergem release a release. A pergunta certa nao e "qual e melhor" — e **"qual ferramenta resolve o que voce precisa fazer hoje"**. Essa aba mapeia a stack inteira por objetivo, mostra como cada ferramenta se posiciona, e te dá um guia de decisao adulto. Sem fanboyice.

---

## SECAO 1 — O panorama 2026

Em 2026, a stack de agentes de IA pra desenvolvimento se organiza em tres camadas:

**Camada 1 — Os harnesses principais.** Sao os "corpos" que executam a IA na sua maquina. Os dois dominantes: **Claude Code** (Anthropic) e **Codex** (OpenAI). Ambos sao multi-surface (terminal, IDE, desktop, nuvem). Ambos suportam skills, MCP, AGENTS.md/CLAUDE.md, subagents. **Sao mais parecidos do que diferentes.**

**Camada 2 — As ferramentas auxiliares.** Sao add-ons que rodam em cima dos harnesses, ampliando capacidade. Aqui mora **GSD** (gerencia de projeto), **Spec-Kit** (spec-driven dev), **Superpowers** (plugin de wrappers), **GSP** (design system), **OpenCode** (CLI alternativo open-source).

**Camada 3 — Os surfaces.** Como voce interage com tudo: terminal, VS Code, JetBrains, desktop apps, web. Cada harness aparece em multiplas surfaces.

Voce **nao precisa escolher uma ferramenta e casar com ela.** O metodo aqui ensina a usar a stack certa pra cada tarefa.

---

## SECAO 2 — Os dois harnesses principais (lado a lado)

> Visualmente: dois cards grandes, cor propria pra cada um, mesma estrutura. Sem hierarquia visual entre eles. Codex nao e "secundario."

### Card — Claude Code
**Quem faz:** Anthropic
**Lancamento:** maio 2025 (GA)
**Modelo padrao:** Claude Opus 4.7 (Max), Claude Sonnet 4.6 (Pro)
**Janela de contexto:** 1M tokens (Opus 4.7)

**Surfaces disponiveis:**
- CLI no terminal (principal)
- Extensao VS Code
- Extensao JetBrains (beta)
- Cowork — desktop app (gerenciamento por pasta)

**Filosofia:** local-first, customizacao granular. Tudo roda na sua maquina. **26 hooks programaveis** dao controle fino sobre o que o agente pode/nao pode fazer. Curva de aprendizado maior, teto de organizacao mais alto.

**Brilha em:**
- Codigo frontend (React, UI)
- Refactor complexo com dependencias
- Workflows com regras organizacionais (hooks)
- Computer Use (controlar browser, interagir com GUI)
- Output minucioso e bem estruturado (vence 67% das avaliacoes cegas)

**Custo:** consome 3-4x mais tokens que Codex em tarefas equivalentes — output mais detalhado, mas mais caro por tarefa.

**Configuracao:** `CLAUDE.md` no projeto + `~/.claude/` global

### Card — Codex
**Quem faz:** OpenAI
**Lancamento:** maio 2025 (preview), out 2025 (GA)
**Modelo padrao:** GPT-5.4 (~1M context, 128K output)
**Janela de contexto:** 1.05M tokens

**Surfaces disponiveis:**
- CLI no terminal (open source, Rust)
- Extensao IDE (VS Code, Cursor, Windsurf)
- Codex desktop app (macOS/Windows — UI muito polida)
- Codex Cloud (sandboxes paralelos via ChatGPT)

**Filosofia:** sandbox kernel-level, configuracao simples. **Tres modos de aprovacao** (untrusted, on-request, never) cobrem a maioria dos casos. Curva menor, "out of the box" forte. Cloud-native pra paralelismo.

**Brilha em:**
- Tarefas terminal-nativas (DevOps, scripts, sysadmin)
- Tarefas paralelas (Codex Cloud roda multiplas em containers separados)
- Eficiencia de tokens (2-4x menos token que Claude pra resultado comparavel)
- Onboarding rapido — equipe nova produz no mesmo dia
- Code review — o reviewer agent automatico pega bugs sutis bem

**Custo:** mais barato por tarefa. Plano ChatGPT Plus ($20/mo) ja inclui uso decente.

**Configuracao:** `AGENTS.md` no projeto + `~/.codex/config.toml` global

---

## SECAO 3 — Comparativo arquitetural honesto

> Tabela comparativa, sem ganhador. Mostra que sao filosofias diferentes, ambas validas.

| Dimensao | Claude Code | Codex |
|---|---|---|
| **Modelo de seguranca** | Hooks programaveis (26 eventos lifecycle) | Sandbox kernel-level (Seatbelt/Landlock/seccomp) |
| **Configuracao** | Camadas hierarquicas (5 niveis: system → user → project → directory → flag) | Profiles explicitos via `--profile` |
| **Granularidade** | Alta (cada hook customizavel) | Baixa (3 modos cobrem tudo) |
| **Padrao de instrucao** | `CLAUDE.md` (especifico Anthropic) | `AGENTS.md` (padrao aberto, lido por Codex/Cursor/Aider) |
| **Skills** | `.claude/skills/SKILL.md` | `.agents/skills/SKILL.md` (mesmo formato) |
| **Multi-agente** | Agent Teams (compartilham task list, coordenam) | Cloud workers (isolados, paralelos) |
| **Computer Use** | Maduro (browser, GUI, fluxo completo) | Limitado (foco em codigo + terminal) |
| **Open source** | Nao (proprietario) | Sim (Rust, github.com/openai/codex) |
| **Nuvem nativa** | Limitada (Cowork e desktop) | Forte (Codex Cloud, sandboxes paralelos) |

**Traducao em linguagem humana:**
- **Claude Code** te da limites mais flexiveis com controle mais detalhado. Bom pra time que vai investir em customizar.
- **Codex** te da limites mais rigidos com controle mais simples. Bom pra time que quer sair produzindo rapido.

**Nenhum e melhor universalmente.** Depende do que voce esta fazendo.

---

## SECAO 4 — Stack organizada por objetivo

> Esta e a secao central da aba. Sai do formato "ferramenta-por-ferramenta" e organiza por **o que voce quer fazer**.

### "Quero um agente base rodando no terminal"
**Opcoes:** Claude Code **ou** Codex CLI
**Recomendacao:** comeca com Codex se valor zero curva de aprendizado; Claude Code se quer customizar de saida. Voce pode usar os dois — eles nao se atrapalham.

### "Quero gerenciar projeto e tarefas dentro do agente"
**Ferramenta:** GSD
**Cobertura atual:** Claude Code (nao tem equivalente direto pra Codex ainda — voce pode portar manualmente as skills)

### "Quero rigor de Spec-Driven Development"
**Ferramenta:** Spec-Kit
**Cobertura:** funciona em Claude Code e Codex (skills sao portaveis)

### "Quero atalhos e wrappers pra agilizar tudo"
**Ferramenta:** Superpowers (plugin)
**Cobertura atual:** Claude Code (e o ecossistema mais maduro)

### "Quero design system pronto pra UI/branding"
**Ferramenta:** GSP (Get Sheet Pretty)
**Cobertura:** Claude Code primariamente; algumas skills funcionam em Codex

### "Quero CLI alternativo open-source"
**Ferramenta:** OpenCode
**Quando faz sentido:** voce quer rodar modelo proprio (LLaMA, Qwen, DeepSeek) ou tem requisitos de auditoria total do codigo

### "Quero revisar codigo antes de commitar"
**Opcoes:**
- Codex tem reviewer agent automatico (auto-review mode) — roda em segundo plano, pega bugs antes de aprovar
- Claude Code permite hooks `PreToolUse` que invocam revisao customizada
- **Combo poderoso:** usar um agente pra escrever, outro pra revisar (Claude escreve + Codex revisa, ou vice-versa). Pega 53-80% mais bugs que solo.

### "Quero rodar tarefas em paralelo na nuvem"
**Opcoes:**
- **Codex Cloud:** containers isolados, agentes nao se falam, tarefas independentes em paralelo. Ideal pra greenfield (novas features sem dependencia entre si).
- **Claude Agent Teams:** sub-agentes coordenados, compartilham task list, dependencias rastreadas. Ideal pra refactor grande com sub-tarefas dependentes.

### "Quero economizar token e tempo"
**Caminho:** Codex CLI + skills bem organizadas + global enxuto. Em benchmarks reais (clonagem de Figma): Codex usou 1.5M tokens, Claude usou 6.2M na mesma tarefa.

### "Quero output mais minucioso e bem estruturado"
**Caminho:** Claude Code (Sonnet 4.6 ou Opus 4.7) com CLAUDE.md detalhado.

### "Quero entender o que ferramentas fazem por baixo dos panos"
**Caminho:** OpenCode + estudar o codigo Rust do Codex (open source).

---

## SECAO 5 — Cada ferramenta auxiliar, em detalhe

> Mantem o formato problema/solucao + badges + links GitHub do site atual.
> Cada ferramenta com sua cor (GSD roxo, GSP rosa, Spec-Kit verde, Superpowers ambar, OpenCode azul).

### GSD — Get Shit Done
**Tipo:** Repositorio de skills
**Cobertura:** Claude Code (primariamente)
**Cor:** roxo

**Problema que resolve:** projetos sem rotina ficam caoticos. Voce abre o agente, esquece o que estava fazendo, perde contexto entre sessoes, nao tem padrao de tarefa.

**Solucao:** GSD adiciona skills de gerencia de tarefa (criar, listar, mover, concluir), branch sync, status do projeto, daily review. Vira o "scrum interno" do agente.

**6 comandos principais:** ver Aba 5 — Skills.

**[Link GitHub do GSD]**

### Spec-Kit
**Tipo:** Repositorio de skills
**Cobertura:** Claude Code + Codex (skills portaveis)
**Cor:** verde

**Problema que resolve:** voce pede "constroi X" e o agente entrega Y, porque a especificacao mental nunca virou texto.

**Solucao:** Spec-Kit forca um fluxo de spec antes do codigo. Skills pra: gerar spec a partir de ideia, validar spec, expandir em RFs/RNFs, transformar em tarefas. Reduz drasticamente retrabalho.

**5 comandos principais:** ver Aba 5.

**[Link GitHub do Spec-Kit]**

### Superpowers
**Tipo:** Plugin (instalavel via marketplace)
**Cobertura:** Claude Code
**Cor:** ambar

**Problema que resolve:** comandos comuns ficam verbosos. Voce digita "ajuda eu a debugar isso seguindo o padrao X..." de novo e de novo.

**Solucao:** Superpowers e um pacote de slash commands prontos (`/debug`, `/refactor`, `/explain`, `/test`, etc.) que encapsulam padroes comuns. Voce digita 2 caracteres, ele expande pro prompt completo.

**7 comandos + install:** ver Aba 5.

**[Link GitHub do Superpowers]**

### GSP — Get Sheet Pretty
**Tipo:** Repositorio de skills (design system)
**Cobertura:** Claude Code primariamente
**Cor:** rosa

**Problema que resolve:** designer brasileiro freelancer + cliente que pede "logo, identidade, site, deck, tudo" e voce gasta 80% do tempo em iteracao visual com a IA, perdendo o foco.

**Solucao:** GSP e um pipeline de design completo: dual-diamond (descobrir + entregar), 8 fases padronizadas, 20+ comandos especificos (logo, brand, landing, deck, social media, etc). Saida consistente, profissional, em horas em vez de dias.

**Como usar:** ver Aba 5 (sub-secao GSP completa, com setup rapido vs completo).

**[Link GitHub do GSP]**

### OpenCode
**Tipo:** Ferramenta CLI (agente alternativo)
**Cobertura:** Stand-alone (concorrente direto de Claude Code/Codex)
**Cor:** azul

**Problema que resolve:** dependencia de empresa unica. Voce quer auditar o codigo do agente, rodar modelo proprio, ou nao confiar dados sensiveis a API externa.

**Solucao:** OpenCode e CLI 100% open source que aceita qualquer modelo (Claude API, GPT API, modelos locais via Ollama). Ideal pra ambientes regulados, equipes de seguranca, ou quem so quer entender por baixo dos panos.

**[Link GitHub do OpenCode]**

---

## SECAO 6 — O guia de decisao

> Bloco de destaque visual. Tipo flowchart simples ou cards numerados.

### Voce esta comecando do zero?
→ **Comeca com Codex.** Barreira menor, desktop app polido, ChatGPT Plus que voce talvez ja tenha cobre uso decente. Quando dominar, experimenta Claude Code pra comparar.

### Voce ja usa um agente e quer subir o nivel?
→ **Aprende o que voce nao usa.** Se ja usa Codex → testa Claude Code pra Computer Use e refactor frontend. Se ja usa Claude Code → testa Codex Cloud pra paralelismo e o reviewer automatico.

### Voce trabalha com codigo critico (financeiro, saude, governamental)?
→ **Claude Code com hooks programados.** A granularidade (26 eventos) permite enforcar policies que sandbox simples nao cobre. Configura `PreToolUse` pra bloquear comandos perigosos.

### Voce trabalha em time pequeno com tarefas independentes?
→ **Codex Cloud.** Containers paralelos, cada dev delega uma tarefa, todas rodam simultaneamente, voce revisa os PRs no fim do dia.

### Voce trabalha em refactor grande de codebase legado?
→ **Claude Agent Teams.** Sub-agentes coordenados, cada um pega uma camada do refactor, compartilham task list, dependencias rastreadas.

### Voce quer maximizar qualidade do output a qualquer custo?
→ **Combo Claude + Codex em revisao cruzada.** Um escreve, outro revisa. Pega ate 80% mais bugs que solo. Custo dobra, qualidade tambem.

### Voce e estudante / hobbyista com orcamento apertado?
→ **Codex CLI no plano ChatGPT Plus ($20/mo).** Eficiente, paga conta, da conta da maioria das tarefas pessoais.

### Voce vai investir tempo em customizar profundamente?
→ **Claude Code.** O teto de customizacao e mais alto. 26 hooks, MCP rico, Cowork pra organizar. Voce sente o investimento depois de 1-2 meses.

### Voce nao quer depender de empresa unica?
→ **OpenCode + AGENTS.md.** Padrao aberto, codigo auditavel, modelo trocavel. Migra de provider quando quiser sem refazer setup.

---

## SECAO 7 — O combo recomendado (pelo Get It Easy)

Se voce so vai instalar uma coisa: **Codex** (curva menor, custo menor, da conta da maioria).

Se voce vai investir tempo: **Claude Code** (teto mais alto, melhor pra workflow customizado).

Se voce pode investir nos dois: **os dois em revisao cruzada** (qualidade subiu, custo dobrou — vale pra projetos pagos).

Em qualquer caso: **GSD + Spec-Kit + GSP** como skills auxiliares portaveis (funcionam em qualquer harness com adaptacao).

---

## SECAO 8 — O que NAO esta na stack (e por que)

Pra ser honesto sobre escopo:

**Cursor** — IDE com agente embutido. Funciona bem, mas e outro paradigma (IDE-first em vez de CLI-first). Se voce ja usa Cursor e gosta, fica. Se esta comecando, recomendamos CLI-first porque o controle e maior.

**Aider** — CLI open source pioneiro. Bom historicamente, mas Codex CLI capturou esse espaco com mais polimento. Mantemos no radar.

**Replit Agent / Lovable / Bolt** — agentes web pra prototipo rapido. Otimo pra ideia inicial, ruim pra producao. Nao concorre com Claude Code/Codex — concorre com WordPress.

**Devin** — agente autonomo de longa duracao. Promessa grande, execucao ainda inconsistente em 2026. No radar, nao recomendamos como stack principal.

**GitHub Copilot** — autocomplete sofisticado. Categoria diferente — voce ainda escreve a maior parte do codigo. Nao e agentic.

---

## CTA FINAL DA ABA

Voce viu a stack. Agora:

- **Quer setup automatico?** → Aba 7 (Quiz monta sua stack baseada em quem voce e)
- **Quer entender as skills em detalhe?** → Aba 5 (Skills, padrao aberto)
- **Quer comparar custos em R$?** → Aba 9 (Custos & Planos)
- **Quer ver tudo na pratica?** → Aba 2 (O Metodo)

---

# Notas pro Claude Code (instrucoes de implementacao)

Quando for converter pra HTML:

1. **Hero da aba** mantem padrao das outras abas. Eyebrow + H1 + lead + sem CTA primario (a aba ja e o conteudo).

2. **Cards Claude Code vs Codex (Secao 2)** — visualmente, dois cards LADO A LADO em desktop, mesmo tamanho, mesma estrutura interna. Cada um com cor de acento propria:
   - Claude Code: sugiro tom **laranja queimado / ambar profundo** (associacao Anthropic)
   - Codex: sugiro tom **teal / cyan-esverdeado** (associacao OpenAI / contraste)
   - Importante: **mesma hierarquia visual**. Nao pode parecer que um e principal e o outro secundario.
   - Em mobile: empilhados verticalmente, na ordem alfabetica (Claude primeiro).

3. **Tabela comparativa (Secao 3)** — tabela limpa, primeira coluna negrito, sem cor de fundo nas celulas. Ultimas duas linhas (linguagem humana) com fundo levemente destacado.

4. **Stack organizada por objetivo (Secao 4)** — cada bloco "Quero X" vira card clicavel ou item de acordeao. O texto da pergunta e o titulo. Em mobile: lista vertical com expand. **Esta e a secao mais importante da aba.** Investir em UX aqui.

5. **Cards das ferramentas auxiliares (Secao 5)** — mantem o formato atual do site (badges, problema/solucao, links GitHub). Apenas reordena pra ordem que escrevi acima e mantem cores definidas.

6. **Guia de decisao (Secao 6)** — sugiro flowchart visual ou cards numerados. Cada cenario com icone tematico (lampada, escudo, equipe, etc). Em mobile: lista com setas.

7. **Combo recomendado (Secao 7)** — bloco em destaque, fundo levemente diferente (talvez ouro suave). Tipografia maior. E um momento de "te indico isso aqui."

8. **Secao 8 (o que nao esta)** — texto menor, fonte menor, talvez em accordion fechado por padrao com label "Por que outras ferramentas nao estao na stack". Quem quer ver, abre.

9. **Atualizacao mensal:** essa aba envelhece rapido (releases mensais de Claude/Codex). Sugiro adicionar uma data "Ultima atualizacao: <mes/ano>" no eyebrow e um pequeno aviso "Stack revisada mensalmente" pra setar expectativa.

10. **Cor convention check:** se ja tem documentacao das 5 cores existentes (GSD roxo, GSP rosa, Spec-Kit verde, Superpowers ambar, OpenCode azul), os tokens das duas cores novas (Claude Code + Codex) precisam ser adicionados na paleta principal. Anthropic costuma usar laranja-coral; OpenAI verde-petroleo. Confere com sua paleta atual antes de finalizar.
