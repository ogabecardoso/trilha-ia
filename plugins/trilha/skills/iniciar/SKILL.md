---
name: iniciar
description: Monta o laboratório da Trilha Claude Code para um novo aluno. Faz uma entrevista curta (perfil, nível, objetivo, calendário, segmentos dos projetos) e cria a pasta com mapa, aulas, progresso, CLAUDE.md e a página do artefato. Use quando o usuário digitar /trilha:iniciar ou pedir para começar a trilha, criar o laboratório ou personalizar a trilha.
argument-hint: "[pasta do laboratório]"
---

# Iniciar a Trilha Claude Code (beta)

Fale em português do Brasil, com tom didático e direto. Avise logo no início que a trilha está em **beta**: a semana 1 foi conferida na documentação oficial, mas ainda está sendo testada pelos primeiros alunos, e as semanas seguintes são escritas por etapas.

Modelos do plugin: `${CLAUDE_PLUGIN_ROOT}/modelos`
Argumento (pasta desejada, opcional): `$ARGUMENTS`

## 1. Descubra os fatos antes de perguntar

Rode e anote, sem perguntar ao aluno: `claude --version`, `git --version`, `node --version`, o sistema operacional e o shell, e `git config --global user.name`. O que você conseguir descobrir sozinho não vira pergunta.

## 2. Entrevista em duas rodadas

Em cada rodada, numere as perguntas e dê a sua recomendação para cada uma, de modo que "sim" aceite a recomendação. Faça uma rodada, espere as respostas e só então faça a próxima.

**Rodada 1 · perfil**
1. Nome e como prefere ser chamado.
2. Objetivo. Recomendação: virar especialista em soluções com IA (sites, apps, SaaS, ERP) para vender projetos sabendo planejar, desenvolver e entregar.
3. Nível em cada fundamento: terminal, Claude Code, Git, Markdown, JSON, YAML, lógica de programação (nunca usei / uso o básico / domino).
4. Plano do Claude: Pro, Max, Team ou Enterprise. No Pro, a trilha reforça a economia de uso.
5. Interfaces que usa: terminal, app Desktop, VS Code.
6. Data de início. Recomendação: a próxima segunda-feira, com 1 hora por dia útil e o desafio no fim de semana.

**Rodada 2 · projetos e laboratório**
7. Segmentos dos quatro projetos. Mostre os padrões e recomende trocar pelos nichos que o aluno atende ou quer atender:
   - P1, site: estúdio de depilação e estética
   - P2, app: controle de colheita num pomar de maçã
   - P3, SaaS: estúdios de pilates e academias pequenas
   - P4, mini-ERP: distribuidora de materiais de construção, com NF-e em homologação
8. Cliente piloto real para o P1: alguém próximo com um pequeno negócio que aceite dar entrevista e validar o site. Se não houver, o Claude faz o papel do cliente.
9. Restrições de dados: empresa onde trabalha, clientes cujos dados nunca podem entrar no laboratório.
10. Pasta do laboratório. Recomendação: o argumento recebido ou `Documentos/Claude/Trilha Claude Code` dentro da pasta do usuário.

Depois das respostas, mostre um resumo do que vai ser criado e peça confirmação antes de criar qualquer arquivo.

## 3. Monte o laboratório

1. Crie a pasta e as subpastas `kit/`, `exercicios/`, `projetos/` e `manual/aulas/`.
2. Copie de `${CLAUDE_PLUGIN_ROOT}/modelos`:
   - `index.html` → `manual/index.html`
   - `trilha.json` → `manual/trilha.json`
   - `aulas/*.md` → `manual/aulas/`
   - `gitignore.txt` → `.gitignore`
   - `progresso.json` → `progresso.json`
   - `CLAUDE.md.modelo` → `CLAUDE.md`
3. Personalize `manual/trilha.json`:
   - `inicio`: a data de início (AAAA-MM-DD, sempre uma segunda-feira).
   - `laboratorio.pasta`: o caminho que o aluno vai digitar no `cd`, na sintaxe do shell dele. Em `regras`, troque `{{REGRA_DADOS}}` pelas restrições da pergunta 9 (ou apague o marcador).
   - `mudancas`: troque `AAAA-MM-DD` pela data de hoje e `{{VERSAO}}` pela versão do Claude Code.
   - Fases F3 a F6: `segmento`, `cliente` e `resumo` conforme as respostas. Se o segmento mudou, reescreva os títulos, objetivos, desafios e provas dessas fases para o novo domínio, **mantendo a mesma estrutura de semanas e os mesmos objetivos técnicos e comerciais**. Exemplo: no P2, a semana 8 continua sendo descoberta do negócio, requisitos, modelagem, SQL e proposta, só que no domínio novo. Se o app do P2 não tiver uso em campo sem internet, troque o tema de offline (S11A1 a S11A3) por notificações e integrações (e-mail, WhatsApp), com dificuldade parecida.
   - Dispensas: marque `"dispensada": true` nas aulas que cobrem o que o aluno disse que **domina** (Markdown: S02A1; JSON: S02A2; YAML: S02A3; lógica: S02A4 e S02A5; Git: S03A1 a S03A3; Claude Code: S01A1 e S01A5). Na dúvida, não dispense. Nunca dispense aulas de projeto nem provas.
4. Nas aulas em `manual/aulas/`, troque `{{PASTA_LAB}}` pelo caminho da pasta.
5. Preencha `progresso.json`: `aluno`, `inicio` e `aulaAtual` com a primeira aula não dispensada.
6. Preencha os marcadores do `CLAUDE.md`: `{{NOME}}`, `{{INICIO_BR}}` e `{{FIM_BR}}` (início + 23 semanas + 4 dias, no formato DD/MM/AAAA), `{{PERFIL}}` (lista curta com nível, plano e interfaces), `{{REGRA_DADOS}}`, `{{REGRA_ECONOMIA}}` (no Pro: "Plano Pro: economize, com respostas diretas e sem leituras desnecessárias."; nos outros planos, uma regra mais leve) e `{{PROJETOS}}` (os quatro projetos, com segmento e cliente piloto). Deixe `{{URL_ARTEFATO}}` para o passo 8.
7. Rode `git init -b main` na pasta, sem fazer commit: o primeiro commit é exercício da semana 3. Se o aluno dispensou Git, ofereça fazer o commit inicial.
8. **Artefato (página com mapa e progresso):** se a ferramenta Artifact estiver disponível, publique `manual/index.html` com o ícone `map` e com `files` contendo `trilha.json` (de `manual/trilha.json`), `progresso.json` e cada aula como `aulas/<id>.md` com `contentType` `text/markdown`. Grave a URL em `progresso.json` (`artefato`) e no `CLAUDE.md` e republique o `progresso.json`. Se a ferramenta não estiver disponível, explique que a trilha funciona do mesmo jeito com a `/trilha:aula` e os arquivos em `manual/aulas/`, e escreva "não publicado" no lugar da URL.
9. Confira que não sobrou nenhum `{{` nem `AAAA-MM-DD` nos arquivos do laboratório.

## 4. Fechamento

Diga em poucas linhas o que foi criado e como começar:

```
cd "<pasta do laboratório>"
claude
/trilha:aula
```

Lembre que a trilha é beta e que problemas e sugestões devem ir para quem compartilhou o plugin. Para receber as semanas novas: `/plugin marketplace update trilha-ia`.
