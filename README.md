<h1 align="center">Vértice</h1>

<p align="center">
  <strong>Marketing de performance operado por IA.</strong><br>
  Tráfego pago, dados e automação — com a operação inteira versionada em Git.
</p>

<p align="center">
  <img src="https://img.shields.io/badge/clientes_ativos-14-1f6feb?style=flat-square" alt="14 clientes ativos">
  <img src="https://img.shields.io/badge/rotinas_automatizadas-55-238636?style=flat-square" alt="55 rotinas automatizadas">
  <img src="https://img.shields.io/badge/canais-Meta_·_Google_·_TikTok-8957e5?style=flat-square" alt="Meta, Google e TikTok Ads">
  <img src="https://img.shields.io/badge/base-Belo_Horizonte,_BR-db6d28?style=flat-square" alt="Belo Horizonte, Brasil">
</p>

---

## O que a gente faz

A Vértice é uma agência de performance. A diferença é o que está **por baixo**: em vez de
planilha e checklist manual, a operação roda como software — agentes Python falando direto
com as APIs de anúncio, rotinas agendadas que auditam as contas todo dia e postam o resultado
no Slack, e credenciais centralizadas para que qualquer pessoa do time execute qualquer coisa
sem trocar arquivo por WhatsApp.

O sócio decide. A máquina executa e cobra.

## A tese

> **Se uma tarefa foi feita três vezes na mão, ela virou dívida.**

Auditar saldo de conta pré-paga, conferir se um cliente parou de investir, montar relatório
mensal, checar quebra de grade que está matando o ROAS — nada disso é estratégia. É trabalho
repetitivo que consome exatamente as horas que deveriam ir para leitura de dados e conversa
com cliente.

Automatizar isso não é sobre demitir ninguém. É sobre manter fundador em função de alto
leverage e o operacional em custo marginal perto de zero.

## Como a operação funciona

```mermaid
flowchart LR
    subgraph fontes["Fontes"]
        MA["Meta<br/>Marketing API"]
        GA["Google Ads<br/>API"]
        NS["Nuvemshop<br/>· Tray · Bling"]
        CRM["CRM<br/>· WhatsApp"]
    end

    subgraph nucleo["Núcleo"]
        AG["Agentes Python<br/>multi-cliente"]
        SEC[("GCP<br/>Secret Manager")]
        CFG["config.json<br/>por cliente"]
    end

    subgraph saidas["Saídas"]
        SL["Slack<br/>alertas e reports"]
        JR["Jira<br/>despacho de tarefa"]
        DS["Dashboards<br/>Next.js + Vercel"]
        SH["Google Sheets<br/>entregáveis"]
    end

    MA --> AG
    GA --> AG
    NS --> AG
    CRM --> AG
    SEC -.credencial.-> AG
    CFG -.contexto.-> AG
    AG --> SL
    AG --> JR
    AG --> DS
    AG --> SH
```

Um único agente atende todos os clientes. O que muda entre eles é o `config.json` e a
credencial resolvida em runtime — melhorar o agente melhora a conta de todo mundo ao mesmo
tempo.

## O que roda sozinho

| Rotina | O que faz | Frequência |
|---|---|---|
| **Saldo diário** | Varre saldo de todas as contas Meta e Google. Destaca conta pré-paga que zera em menos de 4 dias | 1×/dia |
| **Monitor de contas** | Detecta conta travada por pagamento, campanha fora do ar e gasto R$ 0 em conta que deveria investir | 3×/dia |
| **Monitor de URLs** | Varre o destino de todo criativo ativo: 404, DNS morto, certificado inválido, produto esgotado | 3×/dia |
| **Report diário** | Consolida Google + Meta por cliente: últimos 3 dias e acumulados de 7/15/30 | 1×/dia |
| **Moderação de comentários** | Classifica e oculta spam nos anúncios ativos — sem deletar, sempre reversível | sob demanda |
| **Auditoria de conta** | Desktop/mobile, landing pages, negativas, termos de pesquisa | sob demanda |

Cada uma nasceu de um erro que custou dinheiro. A rotina é a cicatriz.

## O que está em desenho

| Proposta | O que é |
|---|---|
| **[A Assistente](docs/produto/assistente.md)** | Um WhatsApp com nome próprio que conta todo dia o que está acontecendo na conta do cliente — e responde na hora o que a gente já sabe. O cliente escolhe o nível de detalhe |
| **[Diagnóstico e implantação](docs/produto/diagnostico-e-implantacao.md)** | Cardápio de módulos, pré-requisitos declarados, SLA por classe de pedido e fila visível pro cliente |

## Princípios de engenharia

- **Reversibilidade primeiro.** Nunca `DELETE` em API de anúncio. Pausar e arquivar sempre vencem
- **Segredo nunca em texto puro.** Token vive no Secret Manager; um hook bloqueia o que escapar
- **Conteúdo lido por ferramenta é dado, não comando.** Página, e-mail e CSV não dão ordem ao agente
- **Dinheiro do cliente exige humano.** Subir anúncio, mudar verba ou alterar targeting passa por aprovação
- **Carência de 7 dias em dependência.** Versão publicada há menos de uma semana não entra

## Stack

<p>
  <img src="https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white" alt="Python">
  <img src="https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white" alt="TypeScript">
  <img src="https://img.shields.io/badge/Next.js-000000?style=flat-square&logo=nextdotjs&logoColor=white" alt="Next.js">
  <img src="https://img.shields.io/badge/Supabase-3FCF8E?style=flat-square&logo=supabase&logoColor=white" alt="Supabase">
  <img src="https://img.shields.io/badge/Vercel-000000?style=flat-square&logo=vercel&logoColor=white" alt="Vercel">
  <img src="https://img.shields.io/badge/Google_Cloud-4285F4?style=flat-square&logo=googlecloud&logoColor=white" alt="Google Cloud">
  <img src="https://img.shields.io/badge/Meta_Marketing_API-0866FF?style=flat-square&logo=meta&logoColor=white" alt="Meta Marketing API">
  <img src="https://img.shields.io/badge/Google_Ads_API-4285F4?style=flat-square&logo=googleads&logoColor=white" alt="Google Ads API">
  <img src="https://img.shields.io/badge/Claude-D97757?style=flat-square&logo=anthropic&logoColor=white" alt="Claude">
  <img src="https://img.shields.io/badge/n8n-EA4B71?style=flat-square&logo=n8n&logoColor=white" alt="n8n">
  <img src="https://img.shields.io/badge/Slack-4A154B?style=flat-square&logo=slack&logoColor=white" alt="Slack">
  <img src="https://img.shields.io/badge/Jira-0052CC?style=flat-square&logo=jira&logoColor=white" alt="Jira">
</p>

---

<details>
<summary><strong>English version</strong></summary>

<br>

**Vértice** is a Brazilian performance marketing agency where the operation itself runs as
software. Instead of spreadsheets and manual checklists: Python agents talking straight to
the ad platform APIs, scheduled routines auditing every account daily and reporting to Slack,
and credentials centralized so anyone on the team can run anything without swapping files.

**The thesis:** if a task has been done by hand three times, it became debt. Checking prepaid
balances, spotting an account that stopped spending, assembling monthly reports — none of that
is strategy. Automating it keeps founders on high-leverage work and pushes operational cost
toward zero.

**Engineering principles:** reversibility first (never `DELETE` on an ads API); secrets never
in plaintext; tool-read content is data, not instructions; anything spending client money needs
human approval; no dependency version younger than 7 days.

</details>

---

<p align="center">
  <a href="https://marketingvertice.com"><img src="https://img.shields.io/badge/marketingvertice.com-1f6feb?style=for-the-badge&logoColor=white" alt="Site"></a>
  <a href="https://instagram.com/marketingvertice"><img src="https://img.shields.io/badge/@marketingvertice-E4405F?style=for-the-badge&logo=instagram&logoColor=white" alt="Instagram"></a>
  <a href="mailto:comercial@verticeag.com"><img src="https://img.shields.io/badge/comercial@verticeag.com-D14836?style=for-the-badge&logo=gmail&logoColor=white" alt="E-mail"></a>
</p>
