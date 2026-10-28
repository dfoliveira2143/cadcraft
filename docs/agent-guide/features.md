# CADCraft — funcionalidades e módulos

Última atualização: 2026-10-28.

## Fluxo principal

| Etapa | Entradas | Responsabilidade e dependências | Saídas |
|---|---|---|---|
| Abrir e editar | DXF/DWG e comandos de desenho | [geom](../../crates/geom/), [dxf](../../crates/dxf/), [doc](../../crates/doc/), [constraints](../../crates/constraints/), [engine](../../crates/engine/) | Drawing editável com histórico |
| Avaliar e produzir saída | Estado editado e parâmetros de saída | [io](../../crates/io/), [render](../../crates/render/), [dwg](../../crates/dwg/) | DXF/DWG, plotagem PDF e imagens |
| Acesso pelo usuário ou agente | Gestos, argumentos CLI ou chamadas estruturadas | [apps](../../apps/), [engine](../../crates/engine/) e interfaces descritas abaixo | Estado atualizado, resposta ou erro; comportamento detalhado nos contratos |

A tabela mostra o caminho conceitual, não uma garantia de suporte a todos os formatos. APIs, estruturas, unidades, efeitos colaterais e limites ficam na [arquitetura](../architecture.md), nos documentos de assunto e nos módulos indicados.

## Contratos e exemplos de uso

- [geometry-parity.md](../geometry-parity.md)
- [autolisp.md](../autolisp.md)
- [customization.md](../customization.md)
- [plot-styles.md](../plot-styles.md)
- [plotters.md](../plotters.md)
- [control-protocol.md](../control-protocol.md)
- [mcp.md](../mcp.md)

## Inventário de bibliotecas

Responsabilidades resumidas a partir dos manifestos e comentários de módulo do checkout. As dependências listadas são as internas diretas declaradas em `dependencies` (incluindo condicionais); não incluem dependências de teste/build nem expansão de features. O manifesto de cada linha é a fonte exata.

| Módulo / manifesto | Responsabilidade declarada | Dependências internas diretas |
|---|---|---|
| [color](../../crates/color/Cargo.toml) | CADCraft colour: AutoCAD Color Index palette, true colour, ByLayer/ByBlock | Nenhuma declarada nesta categoria |
| [constraints](../../crates/constraints/Cargo.toml) | CADCraft parametric solver: geometric and dimensional constraints (own damped Gauss-Newton solver), expressions | `cadcraft-doc`, `cadcraft-geom` |
| [doc](../../crates/doc/Cargo.toml) | CADCraft drawing database: entities, symbol tables, blocks, layouts, copy-on-write store | `cadcraft-color`, `cadcraft-geom` |
| [dwg](../../crates/dwg/Cargo.toml) | CADCraft DWG bridge: converts DWG to and from DXF bytes using the acadrust crate (MPL-2.0, used unmodified) | Nenhuma declarada nesta categoria |
| [dxf](../../crates/dxf/Cargo.toml) | Standalone DXF tag reader/writer (ASCII and binary, pre-2007 code pages), from the published DXF reference | Nenhuma declarada nesta categoria |
| [engine](../../crates/engine/Cargo.toml) | CADCraft engine: sessions, commands, the command line and prompts, snaps, selection, undo | `cadcraft-color`, `cadcraft-constraints`, `cadcraft-doc`, `cadcraft-dxf`, `cadcraft-fonts`, `cadcraft-geom`, `cadcraft-render` |
| [fonts](../../crates/fonts/Cargo.toml) | CADCraft text: the built-in single-stroke drafting font and TEXT/MTEXT layout | `cadcraft-geom` |
| [geom](../../crates/geom/Cargo.toml) | CADCraft geometry: f64 vectors, curves, arcs, splines, intersections, offsets, snaps | Nenhuma declarada nesta categoria |
| [io](../../crates/io/Cargo.toml) | CADCraft file formats: DXF read/write mapping, SVG, PNG and PDF export | `cadcraft-color`, `cadcraft-doc`, `cadcraft-dwg`, `cadcraft-dxf`, `cadcraft-fonts`, `cadcraft-geom`, `cadcraft-render` |
| [mcp](../../crates/mcp/Cargo.toml) | CADCraft MCP server: JSON-RPC 2.0 over stdio, driving a running app or a headless session | `cadcraft-engine`, `cadcraft-io`, `cadcraft-render` |
| [render](../../crates/render/Cargo.toml) | CADCraft rendering: display lists (linetypes, hatches, text, blocks, dimensions) and a CPU rasteriser | `cadcraft-color`, `cadcraft-doc`, `cadcraft-fonts`, `cadcraft-geom` |
| [ui-egui](../../crates/ui-egui/Cargo.toml) | CADCraft user interface (egui): the swappable front end | `cadcraft-color`, `cadcraft-doc`, `cadcraft-engine`, `cadcraft-fonts`, `cadcraft-geom`, `cadcraft-render` |

Ao mudar uma entrada, saída ou dependência, atualize primeiro o contrato do módulo e depois esta navegação. [Voltar ao índice](../INDEX.md).
