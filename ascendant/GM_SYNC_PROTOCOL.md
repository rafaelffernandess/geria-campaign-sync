# ASCENDANT — GM Campaign Sync Protocol

Campaign ID: `ascendant-main`
Feed: `ascendant/feed.json`

## Regra de ouro
Quando um turno da campanha alterar estado persistente — XP, Level, HP/Stamina, Mana/Aura/Prana/Força/Éter, Skills, Técnicas, Talentos, inventário, licença, efeitos, missões, relações, Codex, Torre, Dungeons, diário, títulos ou qualquer outro dado que o jogador deva continuar vendo — o GM deve gravar um novo evento no feed **naquele turno**.

Não basta dizer no texto “sincronizado”. Depois da escrita, o GM deve reler `ascendant/feed.json` e confirmar que:
1. `revision` aumentou;
2. o novo evento possui `seq` maior que o cursor anterior;
3. `campaign` continua exatamente `ascendant-main`.

Nunca escrever no `feed.json` da raiz, que pertence a Geria.

## Formas recomendadas

### Ganho de XP
```json
{"type":"patch","payload":{"operations":[{"op":"grantXp","value":25}]}}
```

### Estado direto
```json
{"type":"patch","payload":{"character":{"resources":{"mana":{"cur":52,"max":60}}}}}
```

### Skills / Técnicas
```json
{"type":"patch","payload":{"skills":[{"id":"skill-id","name":"Skill","rank":"F+","training":12}]}}
```

### Dados específicos de ASCENDANT
```json
{"type":"patch","payload":{"ascendant":{"license":"Bronze — Provisória","skillPoints":0}}}
```

## Idempotência
Use IDs estáveis para Codex, itens, efeitos, quests, journal, chronicle, Skills e Técnicas. Isso permite que o World Codex 6 reprocese o feed para reparar um cliente desatualizado sem multiplicar registros.

## Imagens
Não gerar nem sincronizar imagens automaticamente. O jogador gerencia a imagem principal de personagens, criaturas, locais, Bosses, Companhias, Dungeons e outros registros manualmente no World Codex.
