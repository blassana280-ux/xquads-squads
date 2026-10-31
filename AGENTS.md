# Xquads — instruções para agentes

Este repositório é uma coleção de **squads de agentes de IA** distribuídos como
[Agent Skills](https://agentskills.io), o padrão aberto de extensão de agentes.
Cada pasta de primeiro nível com um `SKILL.md` é uma skill independente.

## O que ler primeiro

Se o usuário descreveu uma demanda mas não disse qual squad quer, leia
`xquads/SKILL.md`. Ele é o chefe geral: diagnostica o domínio e ativa o squad
certo. Se o usuário nomeou o squad, vá direto ao `SKILL.md` dele.

## Como um squad funciona

```
squad/
├── SKILL.md        Ponto de entrada. Diz como ativar e o que existe dentro.
├── agents/         Personas autocontidas. Ler o arquivo = adotar o agente.
├── tasks/          Roteiros executáveis, com entradas, passos e saída definida.
├── workflows/      Sequências multi-agente já encadeadas.
├── checklists/     Validação de qualidade antes de entregar.
├── data/           Catálogos de roteamento e frameworks de referência.
└── config/         Tiers, ícones e metadados do squad.
```

Os squads têm um **chefe** (`entry_agent` no `squad.yaml`) que diagnostica e
delega, e **especialistas** que executam. O chefe não faz o trabalho do
especialista — nem rascunho.

## Regras de ativação

1. Todos os caminhos dentro de um `SKILL.md` são relativos à raiz daquela skill.
2. Ler o arquivo de um agente significa **assumir aquela persona por completo**:
   principios, estilo, limites e o `greeting`.
3. Um agente por vez. Trocar de agente encerra a persona anterior.
4. Comandos do agente usam prefixo `*` (`*help`, `*exit`, e os da persona).
5. Responda em português (pt-BR), salvo pedido explícito em contrário.
6. Tasks com `elicit: true` exigem resposta do usuário em cada ponto de
   elicitação. Não presuma respostas nem pule etapas.

## Fora do escopo

Os squads do Xquads cobrem marketing, copy, marca, tráfego, narrativa, design,
dados, estratégia, segurança e movimento. **Desenvolvimento de software não é
escopo deste repositório** — código vai para o fluxo de desenvolvimento do
usuário.

O squad `cybersecurity` cobre técnicas ofensivas e só deve ser ativado em
contexto autorizado: pentest contratado, CTF, pesquisa de segurança ou defesa de
infraestrutura própria.

## Manutenção do repositório

- `SKILL.md` é **gerado**, não editado à mão. A fonte é
  `scripts/gerar-skills.py`, que lê `squad.yaml` e `config/config.yaml`. Para
  mudar um `SKILL.md`, mude o gerador ou a description curada dentro dele e
  rode `python3 scripts/gerar-skills.py`.
- `python3 scripts/validar-skills.py` valida os 15 `SKILL.md` contra a spec.
  Rode antes de qualquer commit que toque em squads.
- Não introduza caminhos absolutos de cliente (`~/.claude/...`, `~/.codex/...`)
  nas instruções de ativação. Isso quebra a portabilidade, que é a razão de o
  repositório estar neste formato.

<!-- omnibrain-overlay:v2 -->

---

<!--
  Section locale du réseau blassana280-ux — ajoutée par OmniBrain.
  Les instructions upstream ci-dessus restent la seule autorité pour ce dépôt :
  cette section ajoute des règles de travail locales, elle n'en remplace aucune.
  Supprimez ce bloc avant toute contribution upstream si le dépôt ne l'accepte pas.
-->

# Couche locale — réseau OmniBrain

## Source de vérité de l'orchestrateur

> **blassana280-ux/omni-agents-framework** → `OMNIBRAIN.md`, `registry/`, `omni/orchestrator.py`, `tests/`

La référence historique `blassana280-ux/optimiser-mes-agents-IA` **n'a pas pu être vérifiée** (l'API GitHub
répond `403`, aucun accès en lecture) : elle ne doit plus être citée comme
existante.

## Règles de travail

1. **Classer avant d'agir** — simple → 1 agent ; moyenne → 1 à 3 ; complexe →
   escouade, dispatch dans une seule vague parallèle.
2. **Preuve fraîche obligatoire** — aucune affirmation sans sortie de commande,
   ligne de fichier ou réponse d'API. Verdict par défaut : « NEEDS WORK ».
3. **Réutiliser avant de créer** — chercher dans `registry/skills.json`
   (`python3 -m omni skills <termes>`) avant d'inventer un agent.
4. **Aucun secret dans le dépôt** — providers et tokens par variables
   d'environnement uniquement.
5. **Jamais d'écriture directe sur `main`** — branche + Pull Request.
6. **Respect de l'upstream** — `CONTRIBUTING.md` du dépôt prévaut, y compris
   pour la déclaration d'assistance IA.
