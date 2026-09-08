# Estrutura interna da Vértice — delegação, acesso e contexto

> Documento de trabalho. Registrado em 08/09/2026.
> Esta é a conversa que dá credibilidade ao pitch da parceria, mas não é pauta dele.
> O objetivo declarado: reduzir a dependência do Rodrigo para que ele esteja mais
> disponível — e para que a operação sobreviva a trinta dias de férias.

## O KPI que importa

> **Percentual de entregas que rodaram sem escalar para o Rodrigo.**

Todo o resto (atividades por semana, PRs, horas) é instrumentação. Esse é o número
que mede a tese. Se ele não sobe, nada mais importa.

Medida sugerida para as atividades: classificar por dificuldade numa escala curta
(1, 2, 3, 5, 8) no momento do despacho, não no fim. Acompanhar duas séries ao longo
do tempo: volume entregue por pessoa e a fatia que precisou do Rodrigo. Hora não
serve como medida — hora de código e hora de reunião não são a mesma moeda.

## Divisão de trabalho

O critério de corte é uma matriz de duas perguntas: **é replicável?** e **mexe em
dinheiro do cliente?**

| | Replicável | Novo |
|---|---|---|
| **Não mexe em dinheiro** | João Vitor Moreira | João, com revisão |
| **Mexe em dinheiro** | João, com aprovação | Rodrigo |

- **João Vitor Moreira** — operacional e implantação replicável. Trabalha sobre a
  estrutura que já existe (Vercel, agentes, config por cliente). O que ele não pode
  errar precisa estar em trilho, não em julgamento.
- **Letícia** — relacionamento e atendimento. Decide o que é do atendimento dela e
  despacha o resto como atividade. Não precisa de código para isso.
- **Rodrigo** — o que é novo, o que é complexo, o que mexe em dinheiro do cliente.
  Prazo maior, por design: se escala para ele, o cliente já sabe que demora mais.

O gatilho de despacho é a demanda do cliente. Letícia atende, vira atividade, João
executa sobre solução que já existe. O que não tem solução pronta sobe.

## Proteção de código sem limitar a pessoa

O problema declarado: hoje a Letícia poderia baixar o código. O objetivo é *controlar
dado sem limitar a pessoa* — as coisas precisam funcionar para ela como funcionam
para o Rodrigo, com nível de acesso diferente e sem travas que a impeçam de trabalhar.

**A estrutura:** ela não recebe repositório, recebe **ações**. Um bot no Slack expõe
comandos que rodam na infra da Vértice (`/relatorio <cliente>`, `/status`,
`/pausar <campanha>`), e o Claude que ela usa tem um MCP restrito a **ferramentas**,
não a arquivos. O código nunca chega na máquina dela porque nunca precisa chegar.

Isso tem um efeito colateral bom: toda ação passa a ser registrada. O que hoje é
conversa de WhatsApp vira log.

Princípio a manter: o que mexe em dinheiro de cliente continua exigindo aprovação
humana, como já está nos princípios de engenharia da casa.

## Contexto acessível: GitHub → MCP

A pergunta era o quanto custaria migrar o contexto do GitHub para um MCP. **A resposta
é que não é migração — é envelopar.**

O Git continua sendo a fonte da verdade: é versionado, auditável, e já funciona. O que
falta é a camada de acesso. Por cima dele:

1. **Ingestão** — reunião vira transcrição, vira markdown estruturado, commitado no
   repo. Sem isso, nada mais adianta: o contexto precisa existir em texto.
2. **Índice** — embeddings no Supabase (pgvector), reindexado a cada commit.
3. **Servidor MCP com escopos** — `cliente:*`, `interno:financeiro`, `time:*`.
   O acesso se concede por pessoa e por escopo.
4. **Cliente** — Claude no Slack ou no Claude Code com o MCP plugado.

**Estimativa: 60–100 h para a v1**, sendo que a fase 1 sozinha já entrega a maior
parte do valor e pode ir ao ar em duas semanas.

O modelo mental é exatamente o do Mélius que você descreveu: existe um conjunto de
coisas consultáveis; o que você não tem acesso, você simplesmente não vê; alguém acima
tem; e quando aquele dado passa a ser importante para você, você recebe permissão.
Isso mapeia direto para escopos por diretório e tag no servidor MCP.

Consequência organizacional: isso cria demanda por alguém responsável por dados —
uma contratação futura, não imediata.

## Grupos de relatório

A ideia é boa e é barata: um grupo onde chega o relatório diário de que está tudo
rodando. *"Bom dia, todas as 14 contas investindo"* é uma mensagem leve. *"Atenção,
esta conta parou"* é a mesma estrutura, e todo mundo já sabe ler.

O ganho real não é o relatório — é a **autorresponsabilidade**. Se todo mundo vê que
a empresa está rodando, todo mundo repara quando para. Quando o Rodrigo tirar férias,
são quatro pessoas olhando, não zero.

Separação sugerida de canais: um por cliente, um para conversas de IA, um para
alinhamento de time. O que já está sendo tratado vira prioridade automaticamente,
sem passar por reunião.

## Contratações que destravam

Em ordem de retorno:

1. **Um implantador (perfil "Musso")** — a peça que falta. Coloca código no ar, valida
   com o time, garante o operacional. É a mesma vaga que vira produto na parceria
   com a Multiverso, o que significa que formar essa pessoa tem retorno duplo.
2. **Mais um perfil João** — operacional replicável. Times pequenos com poucas pessoas
   bem treinadas resolvem mais do que times grandes mal instrumentados.
3. **Responsável de dados** — só depois que o contexto em MCP existir e a demanda for real.

## Caminho para as férias de 30 dias

O teste final da estrutura. O que precisa estar de pé antes:

- Reuniões com cliente migradas de semanal para quinzenal, negociado com antecedência.
- Uma pessoa do time conduzindo a reunião de acompanhamento.
- Relatório diário no grupo, para que a ausência seja visível e não silenciosa.
- Fila de escalação com prazo declarado: o que sobe para o Rodrigo demora mais, e o
  cliente sabe disso desde o começo.
- A Mesa coberta ou pausada no período — hoje ela é a atividade mais insubstituível
  da agenda, e é justamente por isso que ela vale R$ 20 mil.

## Princípio que atravessa tudo

> Quanto menos decisões uma pessoa precisa tomar, mais fácil é delegar o trabalho dela.

Cada decisão que vira trilho é uma decisão que não precisa mais do Rodrigo. É esse o
trabalho: transformar julgamento em estrutura, um pedaço por vez.
