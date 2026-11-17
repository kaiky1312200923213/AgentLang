# AgentLang — Agente de Consultas SQL

**Autor:** Kaiky Yoshio Ono Marins  
**Categoria:** Python · Agentes de IA · SQL  
**Status:** Protótipo de estudo

## Visão geral

Experimento de agente conversacional que recebe perguntas em linguagem natural e consulta um banco SQLite de uma locadora. O projeto usa LangGraph para organizar o agente e uma ferramenta Python para executar consultas SQL.

## O que demonstra

- Integração de um modelo de linguagem com LangGraph.
- Leitura do esquema de tabelas do banco.
- Ferramenta de consulta SQL chamada pelo agente.
- Respostas em português com explicação dos resultados.

## Tecnologias

- Python
- LangGraph e LangChain
- SQLite
- SDK compatível com OpenAI
- NVIDIA NIM

## Banco de dados esperado

O exemplo referencia um arquivo local `locadora.db` com as tabelas `Cliente`, `Filme` e `ItemLocacao`. Esse banco não está incluído neste repositório; é necessário disponibilizá-lo localmente antes de executar.

## Material e segurança

O código original está em [MATERIAL-ORIGINAL.txt](./MATERIAL-ORIGINAL.txt). A instrução do agente orienta o uso de consultas `SELECT`; revise e valide as consultas antes de conectar o protótipo a dados reais. Configure `NVIDIA_API_KEY` no ambiente local e não publique credenciais.

© 2026 Kaiky Yoshio Ono Marins.