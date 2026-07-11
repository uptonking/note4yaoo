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

# superdoc-arch-v2

- 🤔 superdoc editor is built with a extensible editing architecture that is modular, headless, and agent-friendly.
  - there is a v1 editor at `packages/super-editor/src/editors/v1`. please analyze superdoc editor core architecture/data-flow/logic, then explain to me whether it is possible to implement a v2 editor using the Document API and without using prosemirror ? Is the Document API or  adapter API able to help to implement a v2 editor ?
  - is there a editing Document API / adapter API in begonia like superdoc Document API / adapter API ?
  - begonia should implement a modular/extensible/headless architecture just like superdoc, but in functional programming style. if begonia's architecture is extensible/flexible enough now, is it possible to refactor/improve the begonia architecture to implement a v2 functional edtior without prosemirror?

- Superdoc can support a v2 editor without ProseMirror, but not by reusing the current v1 internals unchanged. Its DocumentApi is genuinely adapter-driven at the API boundary
  - The encouraging part is that Superdoc’s headless toolbar/UI already depend on a narrow host contract plus doc access, and the UI controller also uses a structural editor-like contract
  - But v1 itself is still ProseMirror-centric and its adapter assembly is tightly wired to that runtime 
  - ProseMirror is still the actual v1 editor state, not just a thin compatibility backend. It maps XML to a ProseMirror schema.

- Begonia is using ProseMirror even more centrally than just the browser editor layer. The headless mutable document port is typed as ProseMirrorNode. Engine normalization is PM-node based. The browser selection adapter is also PM-state driven.
  - Begonia already has a strong Document API, but it does not yet have a full editing adapter API like the role Superdoc’s adapter bag plays. But editor-adapters is still mostly layout/ projection oriented, and the browser selection bridge is still explicitly ProseMirror-based.
  - Begonia can be refactored into a modular, headless, functional v2 editor without ProseMirror, but only as a staged migration. 
  - The biggest blocker is deeper than the browser layer: Begonia’s engine normalization, document service, and headless mutable document port still use ProseMirrorNode as the canonical document type.

- 
- 
- 
- 

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
- both projects have a real paginated layout engine, both support multi-column sections, and both support page-DOM virtualization for large documents. 
- The big difference is architectural shape: docx-editor is a simpler dual-DOM editor centered on one hidden ProseMirror state plus one visible page painter, while superdoc is a more layered system with a PM adapter, measurement subsystem, layout engine, resolved-layout stage, painter adapter, and extra orchestration around notes/header-footer/collaboration/history.
- docx-editor is explicit about its model: hidden ProseMirror is the editing truth, visible pages are a separate static DOM rebuilt from PM state 
  - The layout engine itself is linear and page/column oriented: it collects section configs, paginates blocks, and uses a relatively small paginator abstraction
  - Multi-column support is real, but the visible path is comparatively simple: toFlowBlocks emits section column metadata, and the paginator mostly works with count/gap/current column plus a “column region top” for continuous section breaks
  - Virtualization exists, but only at paint time: after layout is computed, page shells are observed with IntersectionObserver, rendered near viewport, and depopulated when far away
- superdoc is more layered. 
  - That extra resolveLayout stage is important: painting, hit-testing, selection rectangles, notes, and navigation consume the same resolved output instead of painting directly from raw layout fragments. 
  - Its column engine is also more advanced, and the engine can start new mid-page column regions and balance them
  - Virtualization is materially stronger: default window: 5, overscan: 1, explicit top/bottom spacers, gap spacers, prefix offsets, binary-search anchor, pinned pages, zoom-aware scroll math, and external scroll-container support 

## Layout Engine / Pipeline

- docx-editor — Simpler, functional pipeline
  - PM → toFlowBlocks → measureBlocks → layoutDocument → renderPage
  - The pipeline is orchestrated by useLayoutPipeline.ts which calls four functions sequentially: toFlowBlocks, measureBlocks, layoutDocument, renderPages. Each function is stateless
  - Strengths
    - Easy to reason about — 4 functions, each < 400 lines
    - rAF coalescing in useLayoutPipeline.ts prevents layout thrashing during fast typing
    - Fingerprint-based incremental updates (buildSourceIdentityForFragment) avoid full re-renders
  - Weaknesses
    - measureBlock.ts dispatches by FlowBlock kind — each new block type needs manual wiring in React AND Vue
    - Floating image exclusion zone calculation lives in the measurement layer, not the paginator — the paginator doesn't know about floats, making it harder to handle float-column interactions
    - Column balancing is not implemented
    - No ColumnRegion concept — can't track mid-page column configuration changes
    - No vertical alignment, no drop caps, no drawing blocks

- superdoc — Heavier, more modular
  - PM → pm-adapter → FlowBlocks → measureBlock → layoutEngine → ResolvedLayout → DomPainter
  - Strengths
    - Full column support: unequal widths, ColumnRegion for mid-page column changes, column-balancing.ts with binary-search algorithm and orphan/widow control
    - SectionState in section-breaks.ts tracks active/pending for ALL section properties 
    - DrawingBlock support — vector shapes, charts, WordArt, SVG geometry, clip paths
    - Strict package boundaries: painter must not import pm-adapter/style-engine/layout-bridge
  - Weaknesses
    - Significantly more code — measureParagraphBlock() alone is ~1800 lines (vs docx-editor's ~980)
    - More complex cache invalidation: DirtyTracker, DebouncedPassManager, ParagraphLineCache, FontMetricsCache, measurementCache — 5 cache layers vs docx-editor's 3
    - ColumnRegion adds complexity to every fragment rendering path

- SuperDoc's layout engine is more robust and extensible — it handles the full OOXML section/column/drawing model. The extra complexity IS worth it for production DOCX fidelity (column balancing, vertical alignment, unequal columns, drawings). 
  - For a simpler WYSIWYG editor targeting core Word features, docx-editor's approach is cleaner and easier to maintain.

- Both projects use Canvas measureText()
  - Key difference — font metrics accuracy: 
    - docx-editor's singleLineRatio comes from a hardcoded lookup table of OS/2 metrics for known fonts (matching Word's behavior for those fonts). This is clever but limited to fonts in the table.
    - SuperDoc's FontMetricsCache uses actualBoundingBoxAscent/Descent from Canvas directly, which gives real per-font metrics without needing a lookup table — more accurate for arbitrary/custom fonts.
  - docx-editor uses a singleton canvas context, caches resolved font fallback/single-line ratio, and is very explicitly tuned around Word/OOXML line-height behavior
  - superdoc also uses canvas, but has a broader measurement subsystem: configurable browser vs deterministic mode, LRU text-width cache, separate font-metrics cache, and more infrastructure for tables/lists/drawings
  - docx-editor looks more directly tuned for Word pagination fidelity; superdoc looks more extensible and probably better cached for repeated large-doc measurement.

- line breaking: 
  - docx-editor uses binary search (findMaxFittingLength) for long words that exceed line width. This finds the exact split point in O(log n) calls to measureText. 
  - SuperDoc uses greedy character-by-character accumulation for the same case. 
  - Binary search is ~O(log n) vs O(n), but both are fast enough for real-world text.
  - SuperDoc's measurement is more extensible (deterministic mode, wider test string, configurable fallback stack, Canvas actualBoundingBox for all fonts). 
  - docx-editor's paragraph-level cache is a nice optimization but the binary search for line breaks and simpler cache structure make it slightly more performant for large documents. The 20k text width cache (vs 5k) is the bigger performance win for docx-editor.

- ProseMirror Integration — Architecture Comparison
- docx-editor — Extension-based schema
  - PM is the hidden source of truth and the visible editor is not PM DOM at all
  - StarterKit.ts bundles ~40 extensions (marks, nodes, features) into a composable set
  - ExtensionManager collects all extensions, builds the PM schema from their schema properties, then initializes plugins post-EditorState creation
  - Schema has 3 FlowBlock variants mapped to PM node types: paragraph → paragraph, table → table, image → image
  - PM doc is always hidden (left: -9999px) — never shown to user
  - Body has ONE hidden EditorView. Each header/footer rId gets its own hidden EditorView (via HiddenHeaderFooterPMs.tsx)
- superdoc — Class-based editor + pm-adapter
  - PM is wrapped behind Editor, PresentationEditor, Document API, collaboration/Yjs, history coordination, and multiple story/header-footer sessions 
    - superdoc also still has a ProseMirrorRenderer path for non-layout-engine/fallback rendering
  - SuperConverter (OOXML→PM) → Editor (PM state) → pm-adapter (PM→FlowBlocks) → layout/paint
  - Editor class (in editors/v1/core/Editor.ts) extends EventEmitter, wraps a PM EditorState
  - Extensions loaded via PM's native extension system (not a custom ExtensionManager)
  - PM schema is separate from the layout schema — the pm-adapter reads PM state and resolves styles at render time. 
    - style resolution is deferred to render time, not baked during import. The converter stores raw OOXML. This preserves document intent for round-trip fidelity.
  - PM doc is also hidden — PresentationEditor bridges PM events into layout/paint state
- SuperDoc's pm-adapter + deferred style resolution is architecturally superior for round-trip fidelity — baking styles during import loses document intent (e.g., a paragraph inheriting style from its parent vs. having inline formatting). 
  - docx-editor's approach is simpler but risks overwriting style references with resolved values. 
  - SuperDoc's document-api contract-first pattern for export operations is also more maintainable than docx-editor's direct fromProseDoc.

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
- SuperDoc: DomPainter class with feature-flagged virtualization option. Configurable: window (default 5 pages), overscan (default 0), gap (default 72px), paddingTop. 
  - Uses scroll event listeners + spacer-based approach.
  - Spacer-based: top spacer + virtualPagesEl container + bottom spacer
  - explicit virtual window, binary search over page offsets, pinned pages, and zoom-aware scroll conversion are more compatible with complex editor behavior 
    - If the requirement is “virtualization must coexist with selection, dragging, notes, zoom, and nested scroll containers,” superdoc is better.
  - Spacer heights = total offscreen content height (maintains correct scroll range)
  - Only virtualWindow (default 5) pages mounted at any time + overscan (default 0)
  - Pages are fully mounted or unmounted (not just content — the entire page element)
  - updateVirtualWindow() called on scroll events — binary search to find anchor page, then mount/unmount
  - scroll
    - Manual calculation — potential for jitter during fast scroll
    - Scroll container	Supports external scroll containers (scrollContainer option)
  - superdoc's spacer approach is more flexible — supports external scroll containers, zoom without re-layout, pinned pages for selection, and multiple layout modes (horizontal/book). 
    - The spacer approach is harder to get right (feedback loops, offset caching, zoom coordination) but more production-ready for complex scenarios. 
    - For a straightforward vertical paginated editor, IntersectionObserver is better. 
    - For a feature-rich editor with zoom, spread view, and external containers, the spacer approach is necessary.
- Zoom
  - No re-layout — zoom is CSS transform: scale(zoomFactor) on the mount element. Pages are not re-painted or re-measured.
  - No re-layout, no re-measurement, no re-rendering — zoom is purely a CSS transform
  - Computation cost: Essentially zero — just a CSS transform change + one scroll recalculation. The browser handles the visual scaling via GPU compositing. The only JS work is the scroll position recalculation on the next scroll event, which is O(log N) binary search.
  - If the user zooms and then scrolls, spacer heights may need recalculation if the mount layout changes
  - Zoom + virtual window shift = the most expensive case (new pages mount/unmount at scaled positions)
  - DomPainter.setZoom() itself mainly updates the zoom factor and recalculates virtualization window math instead of re-measuring text on every zoom change
    - zoom should usually feel fast enough, especially relative to full repagination, but it still triggers repaint work and the code explicitly warns that very high zoom may degrade performance.

- Docx-Editor: renderPages() function with `IntersectionObserver`. Fixed: VIRTUALIZATION_THRESHOLD = 8, VIRTUALIZATION_BUFFER = 2.
  - All page shells are always mounted (correct dimensions for scroll position)
    - memory: O(N) shells + O(window) content
  - `IntersectionObserver` approach is elegant and small, but it depends more on browser observer timing, assumes viewport-root observation, and gives less direct control over selection/drag/zoom/scroll-container edge cases
  - Content is lazy-loaded via IntersectionObserver with rootMargin: '1500px 0px 1500px 0px'
  - Populated/depopulated dynamically — shells always exist for scroll stability
  - Natural scroll — browser handles scroll position via DOM height
    - No manual scroll calculation needed — IntersectionObserver fires automatically
    - Scroll container	Window only
  - Incremental updates:
    - Fingerprint-based: each page gets a hash of (size, margins, fragments, block IDs)
    - Only pages whose fingerprint changed get re-rendered
  - docx-editor's IntersectionObserver approach is simpler and more performant for scroll — the browser handles all scroll math natively, no manual calculation needed.

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
