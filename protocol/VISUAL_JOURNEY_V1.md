# Geria Visual Journey Protocol v1

Versão do Codex: 4.2+

## Princípio
O app do jogador recebe somente o que já foi descoberto. O mapa mestre e artes de conteúdo secreto ficam fora do repositório público.

## Exemplos de operações

### Arte de Codex
```json
{"op":"setEntryImage","id":"npc-001","src":"https://.../media/characters/npc-001.webp"}
```

### Arte de item
```json
{"op":"setItemImage","id":"item-001","src":"https://.../media/items/item-001.webp"}
```

### Visual equipado
```json
{"op":"setLoadoutVisual","src":"https://.../media/loadouts/current.webp","caption":"Equipamento atual"}
```

### Névoa de guerra por fragmentos
```json
{"op":"revealMapTile","id":"tile-001","value":{"src":"https://.../media/maps/tile-001.webp","x":38,"y":42,"w":16,"h":16,"name":"Região explorada"}}
```
