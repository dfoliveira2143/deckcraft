# DeckCraft — funcionalidades e módulos

Última atualização: 2026-10-28.

## Fluxo principal

| Etapa | Entradas | Responsabilidade e dependências | Saídas |
|---|---|---|---|
| Abrir e editar | PPTX, apresentação nativa e ações de edição | [model](../../crates/model/), [pptx](../../crates/pptx/), [format](../../crates/format/), [engine](../../crates/engine/) | Presentation com slides, mestres e histórico |
| Avaliar e produzir saída | Estado editado e parâmetros de saída | [text](../../crates/text/), [anim](../../crates/anim/), [media](../../crates/media/), [render](../../crates/render/), [pdf](../../crates/pdf/) | Slides renderizados, apresentação em tela e arquivos exportados |
| Acesso pelo usuário ou agente | Gestos, argumentos CLI ou chamadas estruturadas | [apps](../../apps/), [engine](../../crates/engine/) e interfaces descritas abaixo | Estado atualizado, resposta ou erro; comportamento detalhado nos contratos |

A tabela mostra o caminho conceitual, não uma garantia de suporte a todos os formatos. APIs, estruturas, unidades, efeitos colaterais e limites ficam na [arquitetura](../architecture.md), nos documentos de assunto e nos módulos indicados.

## Contratos e exemplos de uso

- [animation-parity.md](../animation-parity.md)
- [slideshow-parity.md](../slideshow-parity.md)
- [control-protocol.md](../control-protocol.md)
- [mcp.md](../mcp.md)

## Inventário de bibliotecas

Responsabilidades resumidas a partir dos manifestos e comentários de módulo do checkout. As dependências listadas são as internas diretas declaradas em `dependencies` (incluindo condicionais); não incluem dependências de teste/build nem expansão de features. O manifesto de cada linha é a fonte exata.

| Módulo / manifesto | Responsabilidade declarada | Dependências internas diretas |
|---|---|---|
| [anim](../../crates/anim/Cargo.toml) | DeckCraft slide show timing: animation sequences, per-shape animation state over time, and transition frame layouts | `deckcraft-geom`, `deckcraft-model` |
| [av1](../../crates/av1/Cargo.toml) | Clean-room AV1 decoder (AV1 Bitstream & Decoding Process Specification v1.0.0 with Errata 1) | `deckcraft-bitstream` |
| [bitstream](../../crates/bitstream/Cargo.toml) | Bit-level reading and writing for DeckCraft's codec crates: a re-export of `craft_media::bitstream` from craft-libs, plus `budget`. | Nenhuma declarada nesta categoria |
| [color](../../crates/color/Cargo.toml) | DeckCraft colour: RGB/HSL, theme colour slots, DrawingML-style colour transforms | Nenhuma declarada nesta categoria |
| [engine](../../crates/engine/Cargo.toml) | DeckCraft engine: sessions, undo history, selection, the command registry every frontend dispatches through, and pointer tools | `deckcraft-color`, `deckcraft-fonts`, `deckcraft-format`, `deckcraft-geom`, `deckcraft-media`, `deckcraft-model`, `deckcraft-pdf`, `deckcraft-pptx`, `deckcraft-render`, `deckcraft-text` |
| [fonts](../../crates/fonts/Cargo.toml) | DeckCraft fonts: font database (craft-fonts + system), substitutes for Office fonts, metrics, outlines, shaping | Nenhuma declarada nesta categoria |
| [format](../../crates/format/Cargo.toml) | DeckCraft native file format (.deckcraft: zip of a JSON manifest plus media) and outline text import/export | `deckcraft-model` |
| [geom](../../crates/geom/Cargo.toml) | DeckCraft geometry: units (EMU/pt), transforms, preset shape generators, adjust handles, hit testing | Nenhuma declarada nesta categoria |
| [h264](../../crates/h264/Cargo.toml) | Clean-room pure-Rust H.264/AVC decoder (ITU-T H.264) | `deckcraft-bitstream` |
| [hevc](../../crates/hevc/Cargo.toml) | Clean-room pure-Rust H.265/HEVC decoder (ITU-T H.265) | `deckcraft-bitstream` |
| [isobmff](../../crates/isobmff/Cargo.toml) | Clean-room ISO BMFF (MP4) and QuickTime (MOV) demuxer and muxer | Nenhuma declarada nesta categoria |
| [matroska](../../crates/matroska/Cargo.toml) | Clean-room Matroska (MKV) and WebM demuxer and muxer | Nenhuma declarada nesta categoria |
| [mcp](../../crates/mcp/Cargo.toml) | DeckCraft MCP server: JSON-RPC 2.0 over stdio, driving a running app or a headless session | `deckcraft-engine`, `deckcraft-render` |
| [media](../../crates/media/Cargo.toml) | DeckCraft media: probing, audio decoding (MP3, AAC/M4A, WAV, AIFF, FLAC, ALAC, Vorbis, Opus) to f32 PCM, H.264/HEVC/VP9/AV1 video decoding, poster frames, trim/fade/volume and the playback mixer and clock | `deckcraft-av1`, `deckcraft-h264`, `deckcraft-hevc`, `deckcraft-isobmff`, `deckcraft-matroska`, `deckcraft-ogg`, `deckcraft-opus`, `deckcraft-vp9` |
| [metafile](../../crates/metafile/Cargo.toml) | DeckCraft metafiles (ported from WordCraft): parses Windows WMF and EMF records into a neutral vector model (paths and bitmaps) | Nenhuma declarada nesta categoria |
| [model](../../crates/model/Cargo.toml) | DeckCraft document model: presentations, masters, layouts, slides, shapes, text, themes, transitions, animations | `deckcraft-color`, `deckcraft-geom` |
| [ogg](../../crates/ogg/Cargo.toml) | Clean-room Ogg (RFC 3533) demuxer with Ogg Opus (RFC 7845) and Ogg Vorbis stream mapping | Nenhuma declarada nesta categoria |
| [opus](../../crates/opus/Cargo.toml) | Clean-room pure-Rust Opus decoder (RFC 6716 / RFC 8251; OpusHead, multistream surround) | Nenhuma declarada nesta categoria |
| [pdf](../../crates/pdf/Cargo.toml) | DeckCraft PDF export (craft-pdf/Krilla): slides, notes pages and handouts with a selectable text layer, links and bookmarks | `deckcraft-fonts`, `deckcraft-model`, `deckcraft-render`, `deckcraft-text` |
| [pptx](../../crates/pptx/Cargo.toml) | DeckCraft PPTX: Office Open XML (PresentationML/DrawingML) import and export, written from the public ECMA-376 standard | `deckcraft-color`, `deckcraft-geom`, `deckcraft-model` |
| [render](../../crates/render/Cargo.toml) | DeckCraft renderer: slides, layouts and masters to pixels (vello_cpu): fills, outlines, effects, pictures, text, tables, charts | `deckcraft-anim`, `deckcraft-color`, `deckcraft-fonts`, `deckcraft-geom`, `deckcraft-metafile`, `deckcraft-model`, `deckcraft-text` |
| [text](../../crates/text/Cargo.toml) | DeckCraft text layout: runs to shaped glyph lines with bullets, indents, spacing, alignment, anchoring, autofit and caret hit testing | `deckcraft-color`, `deckcraft-fonts`, `deckcraft-geom`, `deckcraft-model` |
| [ui-egui](../../crates/ui-egui/Cargo.toml) | DeckCraft egui frontend (PowerPoint-style UI); swappable — nothing below depends on it | `deckcraft-anim`, `deckcraft-color`, `deckcraft-engine`, `deckcraft-fonts`, `deckcraft-geom`, `deckcraft-media`, `deckcraft-model`, `deckcraft-render`, `deckcraft-text` |
| [vp9](../../crates/vp9/Cargo.toml) | Clean-room pure-Rust VP9 decoder (VP9 Bitstream & Decoding Process Specification) | `deckcraft-bitstream` |

Ao mudar uma entrada, saída ou dependência, atualize primeiro o contrato do módulo e depois esta navegação. [Voltar ao índice](../INDEX.md).
