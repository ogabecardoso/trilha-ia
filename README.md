# Trilha Claude Code (beta)

Trilha de 24 semanas, 1 hora por dia útil, para sair de iniciante e virar **especialista em soluções com IA**: sites, apps, SaaS e ERP, sabendo planejar, desenvolver, entregar e vender projetos para clientes. Tudo é feito com o Claude Code, que também é o seu tutor.

> **Beta.** A semana 1 foi conferida na documentação oficial do Claude Code (versão 2.1.295), mas ainda está sendo testada pelos primeiros alunos. As semanas seguintes são escritas por etapas e chegam pelas atualizações do plugin. Achou um problema? Avise no grupo.

## O que vem no plugin

- **`/trilha:iniciar`**: uma entrevista curta (nível, objetivo, calendário, nichos que você atende) e a criação do seu laboratório personalizado.
- **`/trilha:aula`**: o tutor diário. Ele conduz a aula, confere a prática, faz a pergunta de fixação e registra o seu progresso.
- **Página da trilha**: um artefato no claude.ai com a régua das 24 semanas, o mapa, as aulas, a referência rápida e o seu progresso.

## A trilha

| Semanas | Fase | Ao final, você vende |
|---|---|---|
| 1–3 | Fundamentos: Claude Code, Markdown/JSON/YAML, lógica e Git do zero | — |
| 4–5 | Customizador: CLAUDE.md, skills, hooks, subagentes, MCP e plugins | — |
| 6–7 | Projeto 1: site para um cliente piloto real | Sites e landing pages |
| 8–11 | Projeto 2: app interno sob medida, com PWA | Apps internos sob medida |
| 12–17 | Projeto 3: SaaS com assinatura | Produtos com assinatura |
| 18–23 | Projeto 4: mini-ERP com NF-e em homologação | Sistemas de gestão |
| 24 | Prova final: um cliente que você nunca viu | — |

Cada aula tem 10 minutos de conceito, 40 de prática e 10 de checklist e fixação. Os segmentos dos projetos se adaptam aos nichos que você atende. A stack é Next.js, TypeScript, Tailwind, Supabase e Vercel.

## Requisitos

- Claude Code atualizado e um plano do Claude (o Pro serve; a trilha ensina a economizar).
- Git instalado. Node.js a partir da semana 2.
- Para a página da trilha: login no claude.ai. Sem ela, a trilha funciona só com a `/trilha:aula`.

## Instalar

Numa sessão do Claude Code:

```
/plugin marketplace add ogabecardoso/trilha-ia
/plugin install trilha@trilha-ia
```

## Começar

1. Abra o Claude Code em qualquer pasta e rode `/trilha:iniciar`.
2. Responda à entrevista. O laboratório é criado na pasta que você escolher.
3. Entre na pasta do laboratório, rode `claude` e depois `/trilha:aula`.

## Receber as semanas novas

```
/plugin marketplace update trilha-ia
```

Ou ative a atualização automática em `/plugin`, na aba **Marketplaces**. Depois, `/trilha:aula preparar` traz a semana nova para o seu laboratório, adaptada ao seu progresso.

## Comandos do tutor

| Comando | O que faz |
|---|---|
| `/trilha:aula` | Dá a próxima aula |
| `/trilha:aula S01A3` | Abre uma aula específica |
| `/trilha:aula S01A3 passo 7` | Retoma do passo 7, depois de um `/clear` |
| `/trilha:aula status` | Resumo do seu progresso |
| `/trilha:aula desafio` | Desafio do fim de semana |
| `/trilha:aula prova` | Prova da fase |
| `/trilha:aula preparar` | Escreve a próxima semana, ajustada às suas dificuldades |

## Como o repositório está organizado

```
.claude-plugin/marketplace.json     catálogo (marketplace trilha-ia)
plugins/trilha/
├── .claude-plugin/plugin.json      manifesto do plugin
├── skills/iniciar/                 entrevista e criação do laboratório
├── skills/aula/                    tutor diário
└── modelos/                        mapa, aulas base, página e modelos de arquivos
```

Criada por Gabriel, com o Claude Code.
