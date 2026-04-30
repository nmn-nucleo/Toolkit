# Aba 2 — O Metodo

## Contexto Global vs Local: a virgula que separa amador de profissional

---

### A virgula que muda tudo

Tem uma coisa que ninguem te ensina nos tutoriais de Claude Code, Codex ou Cursor. Nao esta na documentacao oficial, nao aparece nos cursos do YouTube, nao esta nos posts virais do Twitter.

E essa coisa, sozinha, e a diferenca entre seu agente "funcionar mais ou menos" e seu agente "ler sua mente".

E entender que **o agente le seu sistema de arquivos como contexto** — e que existe um global e um local, e que voce decide o que vai onde.

Quem nao entende isso fica preso no que a gente chama de "Globalzao": uma pasta inchada com 30+ skills carregadas em todo projeto, IA lenta, contexto confuso, alucinacao constante. Ela "se perde". Voce reclama. Tenta de novo. Continua bagunçado.

Quem entende isso resolve em uma tarde.

---

### O principio (em uma frase)

> **Global e leve. Local e especifico. Os dois se combinam quando voce roda no projeto.**

Memoriza. Tatua. E o coracao do metodo.

---

### O modelo mental: cozinha + mochila

Pensa em duas coisas:

**Sua cozinha (global).** Aquilo que voce sempre tem disponivel, todo dia, em todo prato: sal, pimenta, azeite, panela basica, faca afiada. E pequeno, e fundamental, e voce nao quer ficar sem.

**Sua mochila (local).** O que voce leva pra uma situacao especifica: piquenique no parque, viagem de fim de semana, reuniao no cliente. Cada mochila tem coisa diferente. Voce nao leva a cozinha inteira pro piquenique — leva o que faz sentido naquele dia.

**O erro classico:** transformar a cozinha em mochila. Coloca tudo no global "porque pode precisar". Resultado: a cada projeto novo, o agente carrega panela de pressao, espremedor de laranja, processador, liquidificador, batedeira... e nem comecou a fazer o sanduiche.

**O metodo certo:** cozinha tem o basico universal. Mochila tem o especifico do dia. Quando voce esta cozinhando, os dois se combinam — voce usa o sal da cozinha junto com o pao da mochila.

---

### Onde cada coisa mora (caminhos reais)

Esse e o ponto onde a maioria dos tutoriais falha em explicar. Aqui vai o mapa:

#### Claude Code

| Escopo | Caminho | Conteudo tipico |
|--------|---------|-----------------|
| Global | `~/.claude/` (Mac/Linux) | Skills universais, MCP servers globais, settings.json global, CLAUDE.md global (preferencias pessoais) |
| Global | `C:\Users\<voce>\.claude\` (Windows) | Mesmo que acima |
| Local | `<seu-projeto>/.claude/` | Skills especificas do projeto, CLAUDE.md do projeto, agentes customizados, hooks |

#### Codex

| Escopo | Caminho | Conteudo tipico |
|--------|---------|-----------------|
| Global | `~/.codex/config.toml` | Configuracao global (modelo padrao, sandbox, agentes, MCP) |
| Global | `~/.codex/AGENTS.md` | Instrucoes universais ao agente |
| Local | `<seu-projeto>/AGENTS.md` | Instrucoes especificas do projeto |
| Local | `<seu-projeto>/.agents/skills/` | Skills especificas do projeto |

**Repara em uma coisa importante:** o **conceito** e identico nos dois. O nome do arquivo muda. A logica nao. Quem aprende a pensar em camadas global/local domina **qualquer** agente atual e futuro.

---

### O que vai onde (a regra pratica)

#### Vai no GLOBAL (sua cozinha)

- Skills que voce usa **em todo ou quase todo projeto** (ex: formatacao consistente de commits, organizacao de README, lint basico)
- **Preferencias pessoais** (idioma de resposta, tom, estilo de codigo)
- **MCP servers universais** (Filesystem, Memory, GitHub se voce usa em tudo)
- **Configuracoes de modelo padrao** (qual versao usar, reasoning level, etc)

Regra de ouro: se voce nao usa em **pelo menos 80% dos projetos**, nao vai no global.

#### Vai no LOCAL (sua mochila)

- **Instrucoes do projeto** (CLAUDE.md ou AGENTS.md descrevendo o stack, convencoes, decisoes arquiteturais)
- **Skills especificas** (analise de planilha pra projeto de dados; design system pra projeto de site; parser de log pra projeto de DevOps)
- **MCP servers relevantes** (banco de dados desse projeto, API especifica desse cliente)
- **Agentes customizados** que so fazem sentido aqui
- **Hooks de projeto** (validacao antes de commit no padrao desse repo)

Regra de ouro: tudo que e contexto, regra ou ferramenta especifica desse projeto vai aqui — nao no global.

---

### Como os dois se combinam

Quando voce abre um agente dentro de um projeto, ele:

1. Le primeiro o **global** (sua cozinha) — carrega o basico universal
2. Le depois o **local** (sua mochila) — carrega o especifico do projeto
3. **Combina os dois** num contexto unificado pra essa sessao

Em caso de conflito (uma instrucao global diz X, uma local diz Y): **local ganha**. O projeto sempre sobrescreve o global. Faz sentido — o local e mais especifico, mais informado, mais recente sobre o que voce esta fazendo agora.

Isso significa que voce pode ter um padrao global de "responda em portugues" e um projeto especifico que sobrescreve com "responda em ingles porque a documentacao e internacional". Os dois convivem em paz.

---

### O anti-padrao: o "Globalzao"

Aqui esta o erro mais comum, que voce provavelmente esta cometendo agora se nunca pensou nisso:

```
~/.claude/
├── skills/
│   ├── analise-csv/
│   ├── design-system-cliente-A/
│   ├── parser-log-projeto-B/
│   ├── prompts-marketing/
│   ├── tributario-brasileiro/
│   ├── automacao-blockchain/
│   ├── revisor-juridico/
│   ├── ... (mais 23 skills)
└── CLAUDE.md (com 800 linhas)
```

**Sintomas que voce esta no Globalzao:**

- O agente demora pra comecar a responder
- Voce sente que ele "se perde" no meio de uma tarefa
- Ele faz coisa que voce nao pediu (puxando contexto de outro projeto que nem e relevante)
- Ele esquece o que estavam fazendo no meio da sessao
- Voce acha que e "alucinacao do modelo" — na verdade e contexto inchado

**O custo real:** cada token de contexto carregado e token gasto antes do trabalho comecar. Se seu global tem 30 skills carregadas, voce comeca cada sessao com talvez 50 mil tokens consumidos so de "se preparar". Multiplica isso por todas as sessoes do mes.

E pior — agente com contexto inchado **toma decisao pior**. Ele tem que escolher dentre muito mais possibilidades, distrai com conteudo irrelevante, mistura padroes de projeto A com projeto B.

---

### O padrao certo: enxuto + especifico

Compara com isso:

```
~/.claude/                          ← cozinha enxuta
├── skills/
│   ├── git-workflow/               (uso em todo projeto)
│   ├── commit-message/             (uso em todo projeto)
│   └── code-review-basico/         (uso em todo projeto)
└── CLAUDE.md                       (40 linhas: idioma, tom, principios gerais)

projeto-blue-analytics/.claude/     ← mochila do dia
├── skills/
│   ├── duckdb-query/
│   ├── analise-cnpj/
│   └── dashboard-html/
├── agents/
│   └── analista-comercial/
└── CLAUDE.md                       (decisoes arquiteturais desse projeto)
```

3 skills no global. 3 skills no local. Total: 6 skills no contexto dessa sessao — todas relevantes.

**Comparado com o Globalzao de 30 skills carregadas, isso e:**

- ~5x menos tokens consumidos antes do trabalho comecar
- Agente foca melhor (menos opcoes pra confundir)
- Trocar de projeto = trocar de contexto automaticamente
- Onboarding de outra pessoa no projeto e trivial (a pasta `.claude/` ou `.agents/` ja tem tudo)

---

### Aplicado: criando um novo projeto do zero

Aqui o passo a passo concreto, valendo pra Claude Code **e** Codex:

```bash
# 1. Cria a pasta do projeto
mkdir meu-projeto-novo
cd meu-projeto-novo

# 2. Abre o agente nessa pasta
claude              # ou: codex

# 3. O agente ja le seu global automaticamente.
#    Voce nao precisa fazer nada — a cozinha sempre esta disponivel.

# 4. Cria a estrutura local do projeto
mkdir -p .claude/skills    # pra Claude Code
# ou
mkdir -p .agents/skills    # pra Codex

# 5. Adiciona o arquivo de instrucoes do projeto
touch CLAUDE.md            # pra Claude Code
# ou
touch AGENTS.md            # pra Codex

# 6. Comeca a trabalhar. O agente combina global + local automaticamente.
```

E so isso. Nao tem ritual magico, nao tem configuracao escondida. A "virgula" toda esta em entender que esses dois lugares existem e que voce decide o que vai em cada um.

---

### Por que isso vale pra qualquer ferramenta

Voce reparou que tudo que esta acima vale igual pra Claude Code e Codex? Nao e coincidencia.

O modelo de **camadas de contexto (global no usuario + local no projeto)** virou padrao da industria de agentes em 2026. Cursor segue. Aider segue. Codex segue. Claude Code segue. As proximas ferramentas vao seguir tambem — porque e o jeito que faz sentido pra IA operar em codigo.

Quando voce aprende **esse modelo**, voce nao esta aprendendo um truque de uma ferramenta especifica. Voce esta aprendendo a operar agentes — e essa habilidade e portavel.

E o que torna o metodo eterno enquanto as ferramentas sao temporarias.

---

### Os tres testes (voce esta na rota certa?)

Faz esses tres testes agora no seu setup atual:

#### Teste 1: o peso da cozinha
Abre seu agente em uma pasta vazia (sem nada no local). Quanto tempo ele leva pra responder a primeira mensagem? Se demora notavelmente — sua cozinha esta entupida. Tem skill global que devia ser local.

#### Teste 2: a troca de mochila
Vai pro projeto A. Pergunta: "qual o stack desse projeto?" Vai pro projeto B. Mesma pergunta. As respostas sao **diferentes e especificas**? Se nao — voce nao tem mochila por projeto. Esta tudo no global.

#### Teste 3: o teste do explicador
Em 30 segundos, sem olhar arquivo, voce consegue dizer:
- O que tem no seu global?
- O que tem no local desse projeto?
- O que vc colocou em qual e por que?

Se nao consegue — esta na hora de organizar.

---

### Resumo (cole na parede)

> Trate o agente como um sistema de arquivos.
>
> **Pasta global = mochila do dia a dia.** Esta sempre com voce. Pequena, essencial, basica.
>
> **Pasta do projeto = mesa de trabalho.** So aparece quando voce senta pra trabalhar nesse projeto. Tem tudo desse trabalho ali.
>
> **Os dois somam quando voce senta pra trabalhar.** Local sobrescreve global em conflito. Cozinha + mochila = refeicao.
>
> Aprende esse modelo. Aplica. Voce vira profissional.

---

### O que vem depois

Agora que voce entendeu **onde** o contexto vive, as proximas ideias do metodo se encaixam naturalmente:

- **SDD (Spec-Driven Development)** — como escrever a spec que vai no CLAUDE.md/AGENTS.md local
- **Subagents** — como dividir tarefas grandes em sub-sessoes com contexto proprio
- **Commits atomicos** — como manter o local limpo e o historico legivel
- **TDD com IA** — como o teste local virou parte do contexto

Cada um desses se sustenta no que voce acabou de aprender. Sem entender global vs local, eles nao funcionam direito. Com isso entendido, todos eles funcionam melhor.

E sempre, em qualquer ferramenta.
