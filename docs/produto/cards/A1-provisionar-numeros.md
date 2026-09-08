# A1 — Provisionar os três números (ouvido, boca, reserva)

**Fase:** 0 — Canal de pé · **Prioridade:** P0 · **Depende de:** nada · **Bloqueia:** A2, A4, B1, B4
**Referência:** `docs/produto/assistente.md` §5 · **Estimativa:** 1 dia de trabalho + prazo de ativação dos chips

---

## Objetivo

Ter a base física do canal de pé: três linhas de WhatsApp ativas, três instâncias conectadas na
Z-API, e o número orquestrador como **admin** do grupo do cliente piloto.

Nenhuma mensagem automática sai neste card. O que ele entrega é a fundação sobre a qual A2
(webhook) e A4 (envio) são trabalho de horas em vez de trabalho de semanas.

## Por que três números

| Papel | Função | Risco que carrega |
|---|---|---|
| **Ouvido** | Recebe tudo, é admin do grupo, **nunca envia** | Baixo — comportamento só de leitura |
| **Boca** | É a assistente: manda notificação e resposta | Alto — concentra o risco de ban, e é descartável |
| **Reserva** | Fica no grupo, calado e aquecido, até ser promovido | Baixo até ser promovido |

O ouvido ser admin é o ponto que torna o failover automático: quando a boca cai, é ele que
coloca o substituto no grupo, sem pedir nada ao cliente.

Os três números atendem **todos os grupos** — não é um conjunto por cliente. O custo é fixo.

## Escopo

1. **Escolher o cliente piloto.** Critério: grupo ativo, relação boa, e alguém do lado de lá que
   topa ser cobaia e dar retorno honesto. Piloto com cliente frágil não testa nada, só arrisca.
2. **Contratar 3 linhas.** Chip de operadora, em CNPJ da Vértice.
3. **Criar 3 instâncias na Z-API**, uma por número.
4. **Guardar as credenciais no Secret Manager.** Token e instance-id nunca em texto puro, nunca
   em `.env` commitado — vale o mesmo hook que já protege o resto da operação.
5. **Conectar cada número** e registrar como reconectar a sessão quando cair.
6. **Nomear os perfis.** A boca e o reserva usam **o mesmo nome e a mesma foto** — é o que faz a
   troca de número passar despercebida. O ouvido usa nome neutro (ex.: "Vértice · Sistema").
7. **Colocar os três no grupo piloto** e promover o ouvido a admin.
8. **Health check único**: um comando mostra o estado das três instâncias.

## Critérios de aceite

- [ ] As 3 instâncias aparecem online num único health check.
- [ ] Nenhuma credencial em texto puro no repositório.
- [ ] O ouvido é admin do grupo piloto e **conseguiu adicionar e remover** um número de teste.
- [ ] Boca e reserva estão no grupo, com nome e foto idênticos.
- [ ] Existe um registro de operação com: qual número é qual papel, onde estão os chips, quem
      paga a fatura e como reconectar cada sessão.

## Atenções

- **Nenhum número pode ser de pessoa física do time.** Se a pessoa sair, o canal vai junto.
- **Nada de número virtual/VoIP.** É o perfil que o WhatsApp bane mais rápido — exatamente o que
  este desenho existe pra evitar.
- **Não reaproveitar o número que o time já usa pro atendimento humano.** Se ele cair, some o
  canal automático e o humano na mesma tacada.
- **Avisar o cliente piloto antes** de colocar três números desconhecidos no grupo dele. Além de
  ser o começo do consentimento formal (card D7), três entradas silenciosas são um péssimo
  primeiro contato.
- **Aquecimento começa aqui.** Os números não vão de zero a produção no mesmo dia — uso leve por
  alguns dias antes de qualquer automação. A rotina formal é o card B4.

## Fora de escopo

Webhook de entrada (A2) · envio de mensagem (A4) · trava de envio único (A5) · failover (B2).

## Decisão que trava este card

**O nome da assistente** — Vera, Vic, Nina ou outro. O passo 6 não roda sem ele, porque nome e
foto de perfil dependem da escolha. É a única coisa que precisa ser decidida antes de começar.
