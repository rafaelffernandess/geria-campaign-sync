# ASCENDANT — GM Sync Protocol 6.0

Use somente o feed `ascendant/feed.json` para a campanha ASCENDANT. **Nunca escreva no `feed.json` da campanha de Geria.**

## Identidade da campanha
- Campaign ID: `ascendant-main`
- Feed: `ascendant/feed.json`
- Schema aceito pelo World Codex 6: `world-codex-campaign-feed-v1` e feeds 5.x compatíveis.

## Regra por turno
Quando o turno alterar estado persistente, acrescente evento com `seq` crescente e ID único, aumente `revision` e atualize `generated_at`.

Registre o que realmente mudou: XP, recursos, Skills, técnicas, Talentos, inventário, efeitos, missões, relações, Codex, Torre, Dungeons, títulos, licença e reputação.

## XP — obrigatório no feed
Para XP incremental prefira:
```json
{"op":"grantXp","value":25,"reason":"Combate / treino / missão"}
```
O World Codex 6 também aceita `grantXP`, `awardXp`, `addXp` e valores absolutos em `character.xp`.

**Não escreva apenas “+25 XP” na narração.** Se o feed não conceder XP, o aplicativo não deve inventá-lo.

## Coleções
Pode enviar no topo do payload ou dentro de `character`; o World Codex 6 normaliza ambos:
- `inventory`
- `effects`
- `skills`
- `techniques`
- `spells`
- `talents`
- `titles`
- `identifiers`

Para Skills/técnicas específicas também existem:
```json
{"op":"upsertSkill","value":{"id":"skill-id","name":"..."}}
{"op":"upsertTechnique","value":{"id":"tech-id","name":"..."}}
```

## Codex
Prefira:
```json
{"codex":{"entries":[{"id":"...","name":"...","category":"...","state":"discovered"}]}}
```
ou:
```json
{"op":"upsertCodex","value":{"id":"...","name":"..."}}
```
O World Codex 6 transforma até `set codex.entries` em upsert para compatibilidade, mas não use esse formato em novos eventos.

## ASCENDANT
Campos como `ascendant`, `tower`, `dungeons` e `reputation` podem ser enviados diretamente no payload. Eles são mesclados sem apagar os demais dados.

## Imagens
Não gere nem sincronize imagens automaticamente. O jogador escolhe manualmente as artes principais no World Codex.

## Segurança entre campanhas
- ASCENDANT: `ascendant/feed.json`, `ascendant-main`
- Geria: `feed.json`, `geria-main`

Nunca misture os feeds.

## Exemplo
```json
{
  "seq": 16,
  "id": "ascendant-session-000-training-reward",
  "type": "patch",
  "payload": {
    "operations": [
      {"op":"grantXp","value":25,"reason":"Autotreino noturno"}
    ],
    "skills": [
      {"id":"skill-force-nudge","training":14}
    ],
    "journal": [
      {"id":"journal-training-16","title":"Treino","body":"...","date":"Sessão 0"}
    ]
  }
}
```
