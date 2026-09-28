# Geria Campaign Sync

Feed público da campanha de **Geria**.

Este repositório contém somente informações que o personagem já descobriu. Nunca coloque aqui o banco secreto do GM, spoilers, eventos futuros, tokens ou chaves.

## Feed usado pelo Codex

`feed.json`

URL RAW:

`https://raw.githubusercontent.com/rafaelffernandess/geria-campaign-sync/main/feed.json`

No Geria Codex 4.0:
- Campaign ID: `geria-main`
- Sync automático: ativado
- Intervalo recomendado: 30 segundos

A pasta `media/` é reservada a imagens, GIFs, mapas e outros conteúdos visuais já desbloqueados pelo personagem.


## Visual Journey 4.2

O Campaign Sync também pode liberar mídia e mapa progressivamente, sem publicar o mapa mestre ou conteúdo ainda desconhecido.

Operações suportadas pelo Geria Codex 4.2:
- `setEntryImage`: arte principal de personagem, criatura, local, organização etc.
- `addEntryMedia`: galeria adicional (imagem/GIF/vídeo).
- `setItemImage`: arte principal de item conhecido.
- `setLoadoutVisual`: ilustração de corpo inteiro do equipamento atual.
- `revealMapTile`: fragmento cartográfico revelado, com `src`, `x`, `y`, `w`, `h`.
- `revealArea`: área circular descoberta sobre um mapa-base já conhecido.

A pasta `media/` deve conter apenas conteúdo visual que o personagem já pode ver.
