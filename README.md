# 🧠 Segundo Cérebro — Telegram · Hermes · NotebookLM · n8n

Guia passo a passo para construir um assistente pessoal que vive no Telegram, usa o NotebookLM como memória persistente e automatiza tarefas com n8n — do zero, em WSL2 ou na nuvem.

👉 **[Acessar o guia](https://erbacellar.github.io/hnotebooklm-rag/index.html)**

---

## O que você vai construir

- Assistente no **Telegram** que responde por texto, voz e foto
- **Memória persistente** com NotebookLM (respostas citadas, baseadas nas suas fontes)
- **Automação** com n8n conectado via MCP (Model Context Protocol)
- **Pipeline diário autônomo**: feed de notícias → limpeza → briefing no Telegram
- **Diário pessoal** pesquisável por linguagem natural
- Infraestrutura que **sobe sozinha** no boot (systemd) — local ou na nuvem

---

## Estrutura do guia

| Fase | Etapas | O que cobre |
|------|--------|-------------|
| I — Fundamentos | 01–05 | Pré-requisitos, Hermes, NotebookLM, SOUL.md |
| II — No dia a dia | 06–08 | Telegram, voz, foto, TTS, persistência |
| III — Automação | 09–13 | n8n + MCP, workflows, crons, roteamento, diário |
| IV — Alcance & Escala | 14–17 | Múltiplos usuários, Cloudflare Tunnel, nuvem, Oracle Cloud |
| V — Referência | 18–19 | Lições aprendidas, fontes |

---

## Stack

| Peça | Papel |
|------|-------|
| [Hermes Agent](https://hermes-agent.nousresearch.com) | Agente executor — pensa, age, chama ferramentas |
| [NotebookLM](https://notebooklm.google.com) + [notebooklm-py](https://github.com/teng-lin/notebooklm-py) | Memória/contexto persistente via CLI |
| [n8n](https://n8n.io) (self-hosted) | Automação e servidor MCP |
| [Telegram](https://telegram.org) | Porta de entrada (texto, voz, foto) |
| [Cloudflare Tunnel](https://developers.cloudflare.com/cloudflare-one/connections/connect-networks/) | Acesso externo seguro (opcional) |
| [Oracle Cloud Free Tier](https://www.oracle.com/cloud/free/) | Hospedagem gratuita na nuvem (opcional) |

---

## Custo

**≈ R$ 0** usando free tiers:
- Hermes: gratuito (Nous Portal)
- NotebookLM: gratuito (conta Google)
- n8n: self-hosted gratuito
- Telegram: gratuito
- Oracle Cloud: Always Free (4 OCPUs / 24 GB RAM)

---

## Lições principais documentadas

- `SOUL.md` é case-sensitive (`SOUL.md` ≠ `soul.md`) e relido a cada mensagem
- Skills e servidores MCP carregam no boot do gateway → `hermes gateway restart` após mudar
- PATH em serviço systemd é mínimo → sempre usar caminho absoluto do `notebooklm`
- Em modelos gratuitos: **tool dedicada com nome distinto > diretriz no SOUL.md**
- Tools são por plataforma (`hermes tools --summary`) — CLI ≠ Telegram
- `notebooklm ask` sintetiza; para texto literal usar `source fulltext`
- `source clean -y` só em fontes assentadas (nunca logo após adicionar)
- Audio WAV > 50 MB → converter para MP3 antes de enviar no Telegram
- TTS natural: configurar Gemini API key no `.env` do Hermes
- Heredoc no terminal quebra indentação Python → usar `base64 -d`

---

## Contribuindo

PR é bem-vindo. Para mudanças grandes, abra uma issue antes para discutir.

---
