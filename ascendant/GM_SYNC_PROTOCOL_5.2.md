# ASCENDANT — GM Sync Protocol 5.2

Use somente o feed `ascendant/feed.json` para a campanha ASCENDANT. Nunca escreva no `feed.json` da campanha de Geria.

## Regras obrigatórias por turno

Quando o turno alterar estado persistente, acrescente um novo evento com `seq` crescente e ID único, aumente `revision`, e atualize `generated_at`.

O feed deve registrar o que realmente mudou: XP, recursos, Skills, Talentos, inventário, efeitos, missões, relações, Codex, Torre, Dungeons, títulos, licença e progresso.

### XP
Para conceder XP, use uma operação aditiva:

```json
{
  "op": "grantXp",
  "value": 25,
  "reason": "Treino / combate / missão"
}
```

Não escreva apenas "+25 XP" na narração. Se o XP não estiver no feed, o World Codex não tem como recebê-lo.

Para ressincronização absoluta, `character.xp` pode ser enviado explicitamente.

### Codex
Use `payload.codex.entries` para entradas novas ou atualizações. Nunca use `set` em `codex.entries`, porque isso pode substituir a coleção inteira em clientes antigos.

### Coleções
Prefira os campos de topo:
- `inventory`
- `skills`
- `techniques`
- `effects`
- `quests`
- `relations`
- `journal`
- `chronicle`

O World Codex 5.2 também normaliza versões antigas que vierem dentro de `character`.

### Exemplo

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
    ]
  }
}
```

## Imagens
Não gere nem sincronize imagens automaticamente. O jogador administra imagens principais manualmente dentro do World Codex.

## Segurança entre campanhas
- ASCENDANT: `ascendant/feed.json`, campaign `ascendant-main`
- Geria: `feed.json`, campaign `geria-main`

Nunca misture os feeds.
