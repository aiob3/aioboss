# Context Engineer — Simulation & Calibration (Examples)

This file contains sample tasks and the expected agent outputs to be used for calibration and testing.

## Example 1: Update `CONTEXT.md` for `packages/editor` with ShapeUtil summary

**Task**: "Summarize the `ShapeUtil` architecture and add a `getStarted` snippet to `packages/editor/CONTEXT.md`"

**Agent actions (expected)**:
1. `grep_search "class .* extends ShapeUtil" packages -r`
2. `read_file` each found ShapeUtil file to extract responsibilities
3. `semantic_search` to locate any docs about ShapeUtil usage and creation
4. Identify gaps; prepare `chunks` mapping (id, file, summary)
5. Produce a plan (Markdown) to add a brief summary to `packages/editor/CONTEXT.md` and prepare `apply_patch` diff
6. Provide a list of tests (e.g., `cd packages/editor && npm run test -- --grep shape`) and include `typecheck` and `lint`

**Expected Output (JSON):**
{
  "objective": "Update packages/editor/CONTEXT.md with ShapeUtil summary",
  "chunks": [
    {"id":"c1","summary":"Base ShapeUtil class and geometry responsibilities","source":"packages/editor/src/lib/editor/shapes/ShapeUtil.ts"},
    {"id":"c2","summary":"Text shape util details and component","source":"packages/tldraw/src/lib/shapes/text/"}
  ],
  "plan": [
    {"step":1, "description":"Collect all ShapeUtil files with grep_search","tool":"grep_search"},
    {"step":2, "description":"Read files to extract responsibilities","tool":"read_file"},
    {"step":3, "description":"Edit CONTEXT.md adding ShapeUtil summary","tool":"apply_patch"}
  ],
  "tests":["cd packages/editor && npm run test -- --grep shape"],
  "prChecklist":["typecheck","lint","tests"]
}

**Simulated `apply_patch` diff (example)**:
@@
*** Begin Patch
*** Update File: packages/editor/CONTEXT.md
@@
+### Shape utilities (ShapeUtil)
+Each shape type in the editor is implemented via a `ShapeUtil` class. A `ShapeUtil` handles the shape's geometry, rendering component, hit-testing, and interactions such as resize and rotate. To add a new shape:
+
+1. Create a new `ShapeUtil` extending `ShapeUtil<T>` in `packages/tldraw/src/lib/shapes/<your-shape>`.
+2. Implement `getGeometry()`, `component()`, and `indicator()`.
+3. Add a tool and register the shape util in `defaultShapeUtils`.
+
*** End Patch

---

## Example 2: Chunking and RAG for Design Docs
**Task**: "Chunk `docs/design` directory and create a basic RAG index map"

**Expected agent steps**:
- `file_search` list `docs/design` files
- `semantic_search` to generate summaries, then produce chunk map
- Save `chunks` to `docs/agent-chunks/context-chunks.json` (or suggested destination)

**Simulated Output**: file `docs/agent-chunks/context-chunks.json` with structure of chunk ids and small summaries.

---

## Calibration guide
- When running the Context Engineer on a task, evaluate the outputs against acceptance criteria: chunk size, plan atomicity, tests listed, and the `apply_patch` diff correctness.
- If needed, iterate with the agent by requesting specific clarifications (e.g., "Provide more precise test command for the editor shape tests").
