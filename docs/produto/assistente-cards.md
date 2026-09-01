# Assistente — cards de implantação

Backlog da [Assistente](./assistente.md), quebrado no tamanho de card de Jira. Cada linha tem o
que entrega, como se sabe que está pronto e do que depende.

As fases aqui detalham as do §10 do documento principal, com uma diferença: o que lá é a fase 0
("piloto") vira duas aqui — **canal de pé** e **sobreviver a um ban** — porque o failover é
infraestrutura, não refinamento. Sem ele, o piloto funciona até o primeiro número cair.

**Como ler a prioridade:** `P0` é caminho crítico — sem ele nada roda. `P1` entra assim que o P0
da mesma fase fecha. `P2` é o que dá pra viver sem por algumas semanas, mas cobra juros depois.

---

## Fase 0 — Canal de pé

Objetivo da fase: uma mensagem sai da nossa infra e chega no grupo de um cliente, com o número
certo, sem ninguém apertar nada.

| # | Card | Entrega | Pronto quando | Depende de |
|---|---|---|---|---|
| **A1** | Provisionar os três números | Ouvido, boca e reserva ativos na Z-API, com o ouvido como admin do grupo piloto | Os três respondem a um teste de conexão e o ouvido consegue adicionar/remover participante | — |
| **A2** | Webhook de entrada | O ouvido recebe evento de mensagem de grupo e normaliza pra um formato interno | Mensagem enviada no grupo piloto aparece na fila interna em < 5s | A1 |
| **A3** | Registro de grupos | Mapa `grupo ↔ cliente ↔ config`, com o bloco `atendimento` no `config.json` | Um grupo desconhecido é rejeitado com log claro, nunca respondido | A2 |
| **A4** | Envio pela boca | Envio de texto assinado pelo número marcado como ativo | Mensagem chega no grupo com a assinatura do §7; o reserva **não** consegue enviar | A1, A3 |
| **A5** | Trava de envio único | Lease que garante uma boca falando por vez | Teste que promove o reserva no meio de um envio não gera mensagem duplicada | A4 |

**P0:** A1 · A2 · A3 · A4 — **P1:** A5

## Fase 1 — Sobreviver a um ban

Objetivo: a queda de um número é um incidente de minutos, sem ação do cliente.

| # | Card | Entrega | Pronto quando | Depende de |
|---|---|---|---|---|
| **B1** | Heartbeat dos números | Ping periódico de cada instância, com estado publicado | Instância derrubada na mão vira alerta no Slack em < 10 min | A1 |
| **B2** | Failover automático | Promoção do reserva a boca ao detectar queda | Simulação de queda: próxima mensagem sai pelo reserva sem intervenção | B1, A5 |
| **B3** | Reposição do reserva | O ouvido, como admin, adiciona o próximo número ao grupo | Após um failover, o grupo volta a ter boca + reserva sem ninguém pedir nada ao cliente | B2 |
| **B4** | Aquecimento | Rotina de tráfego baixo e constante no número reserva | O reserva tem histórico contínuo de atividade antes de qualquer promoção | A1 |
| **B5** | Reapresentação | Mensagem de troca de número do §7, disparada uma vez por grupo após failover | Cliente recebe o aviso; a mensagem não repete se o failover se repetir no mesmo dia | B2 |

**P0:** B1 · B2 — **P1:** B3 · B4 · B5

> Risco aceito e registrado: conectar cliente não-oficial já viola os termos, mesmo sem enviar.
> B1–B3 reduzem o tempo de recuperação; não eliminam a chance de perder o ouvido. O plano B
> continua sendo a API oficial em grupo dedicado (§5).

## Fase 2 — Notificação (níveis 0 a 2)

Objetivo: o cliente recebe todo dia, sozinho, e para de perguntar "quanto gastou ontem".

| # | Card | Entrega | Pronto quando | Depende de |
|---|---|---|---|---|
| **C1** | Agendador de janela | Respeita horário, dias e feriado por cliente | Nada sai fora da janela, exceto crítico | A3 |
| **C2** | Mensagem diária níveis 1 e 2 | Consolida as rotinas existentes no formato do §7 | Mensagem sai com recorte completo e comparação com a média do período | C1, A4 |
| **C3** | Alerta crítico (nível 0) | Conta travada, saldo zerando, site fora do ar — em qualquer nível | Alerta chega fora da janela e traz o que já foi feito, não só o problema | C1 |
| **C4** | Silêncio em dia sem gasto | Suprime o bom-dia quando a conta não rodou | Conta parada não gera mensagem repetida por dias | C2 |
| **C5** | Mudança de nível por texto | "me manda menos" / "quero acompanhar o dia todo" altera a config | Frase em linguagem natural muda o nível e a assistente confirma o que mudou | C2 |

**P0:** C1 · C2 · C3 — **P1:** C4 · C5

## Fase 3 — Pergunta livre

Objetivo: cobertura de 50% das perguntas sem humano.

| # | Card | Entrega | Pronto quando | Depende de |
|---|---|---|---|---|
| **D1** | Roteador de intenção | Classifica a mensagem contra o catálogo do §4, com fallback explícito | Pergunta fora do catálogo devolve "não tenho esse dado" e vira linha de backlog | A2, A3 |
| **D2** | Camada de consulta | Reuso dos agentes: investimento, saldo, resultado, criativo, saúde | Cada família do catálogo responde com dado real de pelo menos 3 clientes | D1 |
| **D3** | Formatador com recorte | Todo número sai com período, conta e hora da coleta | Nenhuma resposta com número passa sem os quatro campos | D2 |
| **D4** | Guardas de resposta | Sem consulta não há número; nada que gaste dinheiro é executado | Teste adversarial: mensagem pedindo pra subir verba é recusada e escalada | D1 |
| **D5** | Isolamento + canário | Config por cliente, e grupo-canário que valida antes de qualquer deploy | Deploy que tentasse cruzar dado de dois clientes falha no canário | A3 |
| **D6** | Filtro de privacidade | Só processa o que é dirigido à assistente; o resto não é persistido | Conversa entre pessoas do cliente não aparece em log nem em contexto | A2 |
| **D7** | Aviso e consentimento | Texto de onboarding informando que existe um assistente no grupo | Todo grupo ativo tem o aviso registrado com data | C2 |

**P0:** D1 · D2 · D3 · D4 · D5 — **P1:** D6 · D7

> D5 é o card que não pode ser cortado por prazo. Vazamento entre clientes é o único bug do §9
> que encerra o produto.

## Fase 4 — Medir e ajustar

Objetivo: saber se está funcionando antes do cliente avisar que não está.

| # | Card | Entrega | Pronto quando | Depende de |
|---|---|---|---|---|
| **E1** | Métricas do §2 | Razão reativo/proativo, cobertura, taxa de fallback, TTFR | Painel semanal por cliente, sem ninguém abrir planilha | D1, C2 |
| **E2** | Alerta de silêncio anômalo | Cliente que parou de interagir vira alerta interno | Dispara em 2× a média histórica do próprio cliente | E1 |
| **E3** | CSAT pontual | 👍/👎 depois de resposta relevante, no máximo 1×/semana | Nunca dispara depois de má notícia | D3 |
| **E4** | Fila visível | Status de pedido e SLA respondidos dentro do grupo | "em que pé está o que eu pedi" responde com posição e prazo reais | D2 |

**P0:** E1 — **P1:** E2 · E3 — **P2:** E4

---

## O que fica de fora nesta rodada

- **Níveis 3 e 4** — só depois que o nível 2 estiver rodando sem ninguém reclamar de ruído. E,
  quando entrarem, em grupo dedicado, não no grupo do cliente.
- **API oficial** — contingência declarada, não trabalho agendado. Vira card quando um dos
  gatilhos do §5 acontecer.
- **Conversa 1:1** — o grupo cobre o caso de uso; abrir um segundo canal antes da hora dobra a
  superfície de manutenção.
