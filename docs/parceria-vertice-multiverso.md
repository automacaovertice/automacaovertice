# Vértice × Multiverso — tese, oferta e precificação

> Documento de trabalho. Registrado em 08/09/2026, véspera da reunião com César e Luís.
> Peças de apresentação:
> - Pitch: https://claude.ai/code/artifact/b3ec1d5f-2fd2-4102-a75b-f59d8c44eda4
> - Calculadora de cenários: https://claude.ai/code/artifact/b86a2b41-f1d7-4f47-888d-224f9fc989d9

## A tese

O gargalo não é entender automação — é atravessar da compreensão até estar no ar.
Curso resolve a primeira metade e abandona a pessoa na segunda, que é exatamente
onde ela fica quente para comprar caro.

Cada casa já resolveu isso de um lado. A Vértice pela operação de performance
rodando como software; a Multiverso pela engenharia de produto. Junto, isso deixa
de ser competência interna e vira produto.

## O que cada casa põe na mesa

| Vértice | Multiverso |
|---|---|
| Operação de performance como software: agentes Python, 55 rotinas, credencial centralizada | Engenharia de produto que se sustenta depois de entregue |
| A cicatriz — cada rotina nasceu de um erro que custou dinheiro | Modelos mentais de arquitetura: o que vale código, o que vale IA, o que não vale construir |
| Relacionamento e atendimento, onde o problema real aparece | O perfil implantador, que coloca no ar e some do caminho |
| Distribuição: base que já compra e já pediu isso | Sistematização de contratação e onboarding ponta a ponta |

**Onde se encontram:** a Vértice sabe o que precisa existir porque apanha disso todo
dia; a Multiverso sabe construir de um jeito que sobrevive. O produto não é o software
nem o curso — é a travessia.

## A oferta

A Mesa custa **R$ 20 mil por pessoa, por semestre**, com Rodrigo e César presentes.
Ela é o piso da conta, nunca o brinde — é isso que está sendo comprado.

| Produto | 6 meses | Para quem |
|---|---|---|
| Mesa | R$ 20.000 / pessoa | Já tem time técnico, quer o acesso e a leitura |
| Mesa + Método | R$ 44.000 / empresa | Tem quem execute, não sabe o que mandar executar |
| Mesa + Implantação | R$ 72.000 / empresa | Quer no ar sem montar time para isso |

Outras condições: Mesa avulsa mensal R$ 4.200 (cara de propósito, existe para virar
semestral); Mesa 12 meses R$ 34.000; Implantação 12 meses R$ 120.000.

## Como o preço se calcula

A venda de ticket alto trava quando o cliente não sabe por que custa isso. A saída é
abrir a conta e mostrar a margem como margem, em vez de escondê-la numa hora inflada.

```
piso = mesa + implantação + (infra + IA + acompanhamento) × meses
```

| Componente | Cálculo | 6 meses |
|---|---|---|
| Mesa | preço de tabela, entra inteiro | R$ 20.000 |
| Implantação | ~100 h-código × R$ 150 | R$ 15.000 |
| Infra | Vercel, Supabase, GCP · R$ 250/mês | R$ 1.500 |
| IA | tokens em uso real · R$ 400/mês | R$ 2.400 |
| Acompanhamento | 4 h/mês de sênior | R$ 3.600 |
| **Piso** | o que custa existir | **R$ 42.500** |
| **Preço** | piso × 1,7 | **R$ 72.000** |

**O teto vem do outro lado.** Se a implantação devolve 15 h/semana do fundador, são
~390 h no semestre. A R$ 300/hora de custo de oportunidade, o cliente recupera ~R$ 116
mil. Vender a R$ 72 mil deixa a conta favorável para ele e com 41% de margem para nós.
É esse número que se apresenta na venda, não a tabela de horas.

> Só os R$ 20 mil da Mesa estão confirmados. Hora-código a R$ 150, infra a R$ 250/mês,
> IA a R$ 400/mês e o múltiplo de 1,7 são hipóteses a validar com custo real.

## A esteira

Quem compra R$ 72 mil já comprou R$ 97 antes. O curso, que a maioria trata como
destino, aqui é meio de funil.

| # | Degrau | Preço | O que prova |
|---|---|---|---|
| 1 | Diagnóstico automatizado | grátis | Que entendemos a operação dele melhor que ele |
| 2 | Diagnóstico com leitura humana | R$ 97 | Separa curioso de quem tira o cartão do bolso |
| 3 | Playbook das rotinas | R$ 297 | Mostra o tamanho real do trabalho |
| 4 | Curso de metodologia | R$ 1.997 | Revela quem não vai andar sozinho |
| 5 | Sprint de 30 dias | R$ 8.000 | Uma integração no ar — amostra cara que fecha o topo |
| 6 | Mesa + Implantação | R$ 72.000 | A travessia inteira, com nós dois dentro |

## Cenário de faturamento

Mix hipotético de um semestre: 8 × Implantação, 10 × Método, 15 × Mesa pura.

| | 10 × 38k | 10 × 44k |
|---|---|---|
| 8 × Mesa + Implantação | R$ 576.000 | R$ 576.000 |
| 10 × Mesa + Método | R$ 380.000 | R$ 440.000 |
| 15 × Mesa pura | R$ 300.000 | R$ 300.000 |
| **Total** | **R$ 1.256.000** | **R$ 1.316.000** |

Subir o Método de 38 para 44 põe R$ 60 mil a mais no semestre.

Custos de caixa somam R$ 306 mil (implantação R$ 120k, produção das mesas R$ 90k,
revisões R$ 36k, acompanhamento R$ 29k, IA R$ 19k, infra R$ 12k). **Sobra R$ 1.010.000
— margem de 77%.**

### Quanto a Vértice leva

Modelo proposto: **20% originação / 50% entrega / 30% marca e presença na Mesa**
(este último dividido igual entre as casas).

| Papel da Vértice | Fatia | Semestre |
|---|---|---|
| Origina tudo, entrega 50% | 60% | R$ 606.000 |
| Origina tudo, entrega 30% | 50% | R$ 505.000 |
| Origina 70%, entrega 40% | 49% | R$ 494.900 |
| Origina metade, entrega 30% | 40% | R$ 404.000 |

**Faixa de R$ 400 a 600 mil no semestre, com R$ 505 mil como caso central.**

Observação: no modelo atual, originar vale menos que entregar. Se a base de clientes
for da Vértice e isso deve pesar mais, o 20/50/30 precisa virar algo como 30/40/30.

### O alerta de capacidade

**33 pessoas não cabem numa mesa.** Com 8 vagas por turma isso vira 5 turmas — 30
encontros no semestre, mais de um por semana, com os dois sócios presentes. Somando
acompanhamento e revisões: **612 h de sócio no semestre, ~12 h/semana para cada um.**

Isso colide com o objetivo de ficar mais disponível. Três saídas, em ordem de preferência:

1. **Menos vagas, preço maior.** 2 turmas (16 pessoas), Mesa a R$ 28k. Escassez é o
   que sustenta o preço — 33 vagas destroem a premissa do produto de qualquer forma.
2. **Só o topo tem os dois sócios.** Os 8 de Implantação têm a mesa com Rodrigo e
   César; os 15 de Mesa pura vão para um formato maior e mensal, com convidado.
   Vira produto diferente, com nome diferente.
3. **Delegar as revisões.** As 240 h de revisão quinzenal do Método são trabalho de
   implantador, não de sócio. Só isso derruba de 12 h para 7,5 h por semana.

## Decisões da reunião

1. **O que é a Mesa, contratualmente** — proposta: encontros mensais presenciais,
   8 vagas por turma, os dois sócios em todos, vaga nominal e intransferível.
2. **Software próprio agora?** — proposta: não. Cria obrigação de suporte e roadmap
   antes de haver demanda comprovada. Vender método e implantação sobre a stack do
   cliente; o produto emerge do que se repetir.
3. **O que vira produto primeiro** — proposta: a interface de WhatsApp (voz e arquivo
   entram, viram atividade no Jira). É o que mais se repete e menos existe pronto.
4. **Repartição de receita** — proposta: 20/50/30, revisando se originação deve pesar mais.
5. **De quem é a metodologia** — proposta: marca conjunta, cada casa livre para usar em
   cliente próprio, sem exclusividade nesta primeira temporada.
6. **Entram outras empresas?** — proposta: não na v1. Terceiros como fornecedor
   pontual, nunca sócio de contrato.
7. **Primeiro cliente-teste** — proposta: um Sprint de 30 dias com alguém da base
   antes de anunciar. Preço cheio, escopo pequeno, tudo cronometrado — é assim que a
   fórmula vira número real.

## Validação de demanda já existente

João Vitor Pinheiro, sem que nada tivesse sido oferecido: *"eu queria muito ter um
Musso no meu time"*. Isso é demanda antes da oferta existir. O que ele pede não é um
desenvolvedor — é quem coloca no ar, valida com o CEO e garante o operacional sem
precisar de gestão.

Desdobra em duas frentes:
- **Como produto:** alocação de implantador, R$ 12–18 mil/mês, com metodologia e as
  duas casas como retaguarda técnica.
- **Como formação:** a trilha que forma esse perfil vira o degrau mais caro da esteira
  educacional e alimenta nosso próprio banco de implantadores.

## Pendências

- Nome exato do repositório `marketing-vertice` para migrar estes documentos.
- Link da DNIA (dn.ia) para comparar o modelo deles — busca não encontrou com confiança.
- Custos reais de hora-código, infra e IA para substituir as hipóteses.
