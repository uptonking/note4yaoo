---
title: lib-editor-superdoc-codebase
tags: [codebase, superdoc]
created: 2026-04-20T00:35:54.175Z
modified: 2026-04-20T00:36:02.064Z
---

# lib-editor-superdoc-codebase

# guide

# architecture
- packages
  - layout-engine/contracts — shared type definitions (FlowBlock, Measure, Fragment, Page, ColumnLayout, TrackedChangeMeta, etc.)
  - layout-engine/pm-adapter — bridges ProseMirror state to FlowBlocks, resolves styles, converts tracked-change marks
  - layout-engine/layout-engine — core paginator with column balancing, section-break scheduling, floating objects, keepNext chains
  - layout-engine/style-engine — cascade resolution (defaults, styles, conditional formatting, inline overrides)
  - layout-engine/measuring — text measurement (via layout-bridge/ font metrics + character measurement)
  - layout-engine/painters/dom — DomPainter class that renders layout to DOM, handles virtualization, headers/footers, incremental updates

- SuperDoc uses a modular, package-separated pipeline with clear boundaries between each stage:
  - DOCX → super-converter (OOXML parser) → PM doc (hidden, never shown) → pm-adapter (reads PM state + resolved styles) → FlowBlock[] → layout-engine (paginates) → ResolvedLayout → DomPainter (painters/dom/) → visible DOM pages
- SuperDoc has a `DrawingBlock` (vector shapes, shape groups, WordArt) and `ListBlock` (separate from ParagraphBlock) — these don't exist in docx-editor.

- Measurement
  - Uses a FontMetricsCache + ParagraphLineCache system in layout-bridge
  - Canvas-based text measurement (measureCharacterX, text-measurement.ts)
  - Paragraph hash-based caching for unchanged content

- DomPainter
  - A class-based renderer (vs docx-editor's functional renderPage())
  - Supports vertical, horizontal, and book layout modes
  - Has a ResolvedLayout concept (pre-processed layout with identity tracking)
  - Incremental rendering via patchLayout() — only re-renders changed pages
  - Paint snapshot system for structured content observatio

- 
- 
- 
- 
- 
- 
- 
- 

# prompts
- deep into related code/docs/architecture/data-flow in project docx-editor(in current folder) and project superdoc(at `../superdoc` folder), compare the deeper differences in core features like pagination, virtualized render, multi-column layout, track-change...(or any other major features that are important).
- after your code/architecture exploring, please explain to me more architecture/data-flow differences between the two projects:
1. for the core layout engine/pipeline that supports pagination and multi-column, which one is more robust/extensible/performant and compatible with other major features ? is the complexity worth it?
2. for text measuremen in layout engine, are 2 projects both use Canvas-based text measurement? compare the logic and explain which one is more robust/extensible/performant?
3. prosemirror is used in both projects, how is prosemirror used in each, compare the architectre and differences.
4. for virtualized rendering, superdoc uses scroll event listeners + spacer-based approach. docx-editor uses IntersectionObserver approach. which one is more robust/extensible/performant and compatible with other major features ? compare the implementation logic and explain.
5. when zooming in/out the superdoc editor/page, is the computation heavy, is it fast?

- 
- 
- 
- 
- 

# state/data-model

# view

# more

# 📌 docx-editor

## architecture

- Paginated Layout Engine — 4-Stage Pipeline
  - PM State → FlowBlocks (toFlowBlocks.ts) — ProseMirror nodes converted to typed block objects (paragraph, table, image, textBox, sectionBreak, etc.)
  - FlowBlocks → Measures (measureBlock.ts) — Canvas-based text measurement (not DOM), producing MeasuredLine[] with per-line width/ascent/descent. Floating images create exclusion zones that reduce paragraph line widths.
  - Measures → Pages (layoutDocument in layout-engine/index.ts) — The Paginator places fragments onto pages, splitting content across page/column boundaries. Handles keepNext/keepLines chains, section breaks (active/pending pattern), and two-pass footnote layout.
  - Pages → DOM (renderPage.ts + virtualization) — Multi-pass rendering with floating image layers, fragment painting, and column separator lines.
  - Orchestrated by useLayoutPipeline.ts (rAF-coalesced) and useLayoutTriggers.ts (web font loads, header/footer changes). Three scroll-restore strategies preserve position across re-layouts.

- Multi-Column Layout — Partially Supported
  - Working: Column count, column spacing, equal-width columns, column separator lines (w:sep), multi-column pagination with content flowing across columns, column breaks
  - roadmap
    - Non-equal-width columns
    - nextColumn section start: Defined and parsed but ignored by the layout engine 

- Virtualized Rendering
  - Documents < 8 pages render eagerly; 8+ pages use an `IntersectionObserver` approach
  - All page shells (empty containers with correct dimensions) are always mounted for scroll stability
  - Content populated lazily as pages enter the viewport (1500px rootMargin pre-loading)
  - ±2 page buffer kept rendered for smooth scrolling
  - Incremental updates: fingerprint-based — only changed pages get re-rendered
  - Three scroll-restore strategies survive re-layouts

- 
- 
- 
- 
- 
- 
- 

## state

## view

# 🆚 Comparison: SuperDoc vs. Docx-Editor

## Pagination

- Aspect: Package structure
  - SuperDoc: 7+ packages (contracts, pm-adapter, layout-engine, style-engine, measuring, painters, layout-bridge) with strict import boundaries
  - Docx-Editor: Single packages/core with layout-engine/, layout-bridge/, layout-painter/ inside

- Aspect: Paginator
  - SuperDoc: createPaginator() class-like factory; PageState tracks constraintBoundaries, maxCursorY, lastParagraphBorderHash, lastParagraphContextualSpacing
  - Docx-Editor: createPaginator() simpler; PageState tracks columnIndex, cursorY, trailingSpacing

- Aspect: Section breaks
  - SuperDoc: Full scheduleSectionBreak() with nextPage, continuous, evenPage, oddPage, plus requirePageBoundary override. 
  Active/pending pattern for all section properties (margins, size, columns, orientation).
  forceMidPageRegion for mid-page column changes.

  - Docx-Editor: Active/pending pattern for margins/size/columns. Handles nextPage and continuous. nextColumn section type is ignored (falls through to default = nextPage).

- Aspect: KeepNext chains
  - SuperDoc: Pre-computed KeepNextChain type with startIndex, endIndex, memberIndices, anchorIndex. Phase 1: sum member heights; Phase 2: add anchor first-line height only.
  - Docx-Editor: computeKeepNextChains() simpler; no anchor first-line optimization.

- Aspect: Contextual spacing
  - SuperDoc: Per-paragraph contextualSpacing with shouldSuppressOwnSpacing() for each side independently
  - Docx-Editor: shouldSuppressSpacingForEmpty checks but simpler spacing logic

- Aspect: Vertical alignment
  - SuperDoc: vAlign on sections: top, center, bottom, both (justified) — post-layout fragment Y adjustment
  - Docx-Editor: Not present

- Aspect: Drop caps
  - SuperDoc: dropCapDescriptor with full metadata, rendered by layout engine
  - Docx-Editor: Not present

- Aspect: Footnotes
  - SuperDoc: footnoteReservedByPageIndex — per-page footnote height reservation
  - Docx-Editor: Two-pass footnote layout approach

## Multi-Column Layout

- Aspect: Column types
  - SuperDoc: ColumnLayout = { count, gap, withSeparator?, widths?: number[], equalWidth? } — supports unequal column widths via widths[] array
  - Docx-Editor: ColumnLayout = { count, gap, equalWidth?, separator? } — widths[] parsed but not used in rendering

- 🆚 Aspect: Column normalization 
  - SuperDoc: normalizeColumnLayout() — scales explicit widths proportionally, fills missing widths with equal fallback, validates epsilon. Unequal widths are fully supported and rendered. 
  - Docx-Editor: Always computes equal-width: (contentWidth - (count-1)*gap) / count

- Aspect: Column regions
  - SuperDoc: ColumnRegion = { yStart, yEnd, columns } — pages can have multiple vertical column regions when continuous section breaks change columns mid-page. Renderer uses columnRegions for per-region separator lines.

  - Docx-Editor: No ColumnRegion concept — columns on SectionBreakBlock only, no mid-page region tracking

- Aspect: Column balancing
  - SuperDoc: Full column-balancing.ts module: binary-search algorithm for balanced column heights, orphan/widow control, table splitting at row boundaries, shouldBalanceColumns() with explicit balanceColumns flag, shouldSkipBalancing() guards. Matches Word's observed behavior.

  - Docx-Editor: No column balancing implementation

- Aspect: Column X computation
  - SuperDoc: columnX() in paginator uses per-column widths array: x += widths[index] + gap for unequal columns
  - Docx-Editor: getColumnX() uses equal-width formula: margins.left + columnIndex * (width + gap)

- Aspect: nextColumn section start
  - SuperDoc: Not handled — SectionBreakBlock.type only allows continuous, nextPage, evenPage, oddPage. nextColumn not in the enum.

  - Docx-Editor: Defined as valid SectionStart but ignored by layout engine (falls through to nextPage)

- Aspect: Column separator rendering
  - SuperDoc: renderer-column-separators.test.ts — full separator line rendering with per-region boundaries
  - Docx-Editor: Column separator lines rendered in renderPage.ts — simpler, only page-level columns

## Virtualized Rendering

- 🆚 Aspect: Implementation
  - SuperDoc: DomPainter class with feature-flagged virtualization option. Configurable: window (default 5 pages), overscan (default 0), gap (default 72px), paddingTop. Uses scroll event listeners + spacer-based approach.

  - Docx-Editor: renderPages() function with `IntersectionObserver`. Fixed: VIRTUALIZATION_THRESHOLD = 8, VIRTUALIZATION_BUFFER = 2.

- Aspect: Activation
  - SuperDoc: Opt-in via options.virtualization.enabled = true (feature flag). Only vertical mode.
  - Docx-Editor: Automatic for documents ≥ 8 pages

- Aspect: DOM structure
  - SuperDoc: Top spacer + virtualPagesEl container + bottom spacer. Spacer heights = total offscreen content height. Pages mounted/unmounted based on scroll position.

  - Docx-Editor: All page shells always mounted (for scroll stability). IntersectionObserver
    populates/depopulates content.

- Aspect: Scroll handling
  - SuperDoc: scrollContainer support (wrapper div with overflow-y: auto). scrollContainerMountOffset cached to prevent feedback loops. overflowAnchor: none on pages container to prevent browser anchor-induced scroll drift.

  - Docx-Editor: Three scroll-restore strategies (snapshot, DOM anchor, ratio fallback)

- Aspect: Pinned pages
  - SuperDoc: setVirtualizationPins() — selection/drag logic can pin specific page indices to remain mounted even outside the viewport window
  - Docx-Editor: No pin mechanism

- 🆚 Aspect: Zoom support
  - SuperDoc: setZoom() — CSS zoom/scale factor for converting between screen-space and layout-space during virtualization
  - Docx-Editor: No zoom support

- Aspect: Incremental updates
  - SuperDoc: patchLayout() + changedBlocks set — only changed pages re-rendered. Paint snapshot system
    (PaintSnapshotBuilder) for structured content observation.

  - Docx-Editor: Fingerprint-based incremental — only pages whose fingerprint (hash of size, margins, fragments) changed get re-rendered

- 🆚 Aspect: Layout modes
  - SuperDoc: vertical, horizontal, book (spread view). Semantic flow mode (flowMode: 'semantic') with
    SEMANTIC_PAGE_HEIGHT_PX = 1_000_000 — no pagination clipping during measurement.

  - Docx-Editor: Vertical only. No horizontal/book/semantic modes.

## Track Changes

- Aspect: Mark types
  - SuperDoc: trackInsert, trackDelete, trackFormat — 3 PM mark types. Format changes track before/after state(bold, italic, strike, underline, textStyle, highlight, link).
  - Docx-Editor: No trackFormat mark — only tracked-insert and tracked-delete in the contract types 

- Aspect: TrackedChangeMeta
  - SuperDoc: { kind, id, overlapParentId, relationship, storyKey, author, authorEmail, authorImage, date, before?: RunMark[], after?: RunMark[] } — rich metadata with overlap tracking and format change before/after state

  - Docx-Editor: { kind, author, date } on data-change-author/data-change-date/data-revision-id dataset attrs. Simpler.

- Aspect: Rendering modes
  - SuperDoc: TrackedChangesMode = 'review' | 'original' | 'final' | 'off' — 4 modes. 
    - Review: insert highlighted, delete highlighted+strikethrough. 
    - Original: shows document before changes. 
    - Final: shows document after changes. 
    - Off: no decorations.

  - Docx-Editor: No mode switching — tracked insertions/deletions are always rendered with visual decorations(color, strikethrough). No original/final/off toggle.

- Aspect: Overlap handling
  - SuperDoc: resolveInsertDeleteOverlap() — when a deletion overlaps an insertion, both marks are rendered with track-overlap-insert-delete-dec class and trackChangePreferredTargetId dataset for accept/reject targeting. review-model/overlap-compiler.js compiles nested edits.
  - Docx-Editor: No overlap handling

- Aspect: Accept/reject
  - SuperDoc: Full decision engine: decideTrackedChanges() with makeTextInsertIntent, makeTextDeleteIntent, makeTextReplaceIntent. replacements mode (paired/independent). Toolbar commands for accept/reject selection. Permission system (isTrackedChangeActionAllowed).

  - Docx-Editor: Accept/reject API exists in DocxEditorRef but simpler implementation

- 🆚 Aspect: Collaboration
  - SuperDoc: Yjs-based CRDT (packages/collaboration-yjs) for real-time multiplayer editing with conflict resolution. Track changes integrated with collaborative editing.

  - Docx-Editor: No real-time collaboration layer

- Aspect: PM integration
  - SuperDoc: Dedicated TrackChangesExtension with plugins (TrackChangesBasePlugin), mark definitions, and editing hooks. Cursor position adjustments via TrackChangesHandler (deletions subtracted from visual position).

  - Docx-Editor: Track changes parsed and rendered, but no dedicated editing extension for cursor offset adjustments
