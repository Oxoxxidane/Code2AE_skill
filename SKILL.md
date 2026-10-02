---
name: code2ae
description: Faithfully rebuild HTML, Remotion, Hyperframe, and other code projects as editable After Effects projects. Understand the source and observe its output, then reconstruct motion graphics with AE parametric shapes, precompositions, sparse keyframes, and Nulls that each handle one atomic motion. For procedural effects that AE cannot faithfully reproduce natively, validate them with the same-source ArbiFX Render CLI before applying them through HTTP apply_code.
---

# Code2AE

Match the source program's visuals and animation while keeping the AE project editable and easy to modify. Do not change the source design for aesthetic improvement.

## Check the environment first

Locate this SKILL.md, then invoke `bin/<platform>/code2ae-http` and `bin/<platform>/arbifx-render` using absolute paths (add `.exe` on Windows). `<platform>` combines the operating system, windows/darwin/linux, with amd64/arm64 (x64 and x86_64 map to amd64; aarch64 maps to arm64), for example `windows-amd64`. The entire directory is movable and does not depend on a fixed drive, working directory, source checkout, or build tools. Keep the selected platform's entire bin directory, including its fonts and runtime libraries. See [Runtime requirements](references/runtime.md).

ArbiFX provides a complete AE control HTTP interface wrapped by the CLI. Prefer CLI operations; use computer interaction only when necessary.

Read the [HTTP CLI](references/cli.md), [complete HTTP protocol](references/http-api.md), and [Render CLI](references/render-cli.md), then observe the following:

AE's HTTP service starts only after at least one ArbiFX effect has been loaded in the current AE session. Starting AE alone is insufficient. If the connection fails, explain this prerequisite to the user; an unavailable HTTP service cannot create its own first instance.

The HTTP interface uses two ports: AE 28154 and Start 28153. Applying an AFX instance without opening Start may leave the Start port unavailable. Before sending Start commands, use the AE interface on port 28154 to locate the intended AFX instance and request that instance's Start window.

Local HTTP requires no token. Backend API key verification uses the user's ArbiFX configuration. Never print plaintext keys in output or logs.

If ArbiFX reports insufficient credits, remind the user to visit [www.arbifx.com](https://www.arbifx.com) to top up their credits.

The After Effects project must use 8 bits per channel (8 bpc).

## Execute AE tasks serially

Run AE modification and rendering tasks one at a time. Wait for the current task to finish before starting another. If a request times out, check whether the original task has completed or is still running before retrying or submitting another task.

If AE appears to be stalled, first determine whether it is computing, saving, or waiting for a modal dialog to be dismissed. When a dialog is present, stop sending AE commands and first try to resolve or dismiss it yourself through the UI. If you cannot dismiss it, wait for the user to close it before resuming AE commands.

## Understand the complete source project

Follow the [Conversion guide](references/conversion.md): read entry points, dependencies, components, styles, animation helpers, shaders, and assets, and run the source to observe still frames and the complete animation. Establish dimensions, frame rate, duration, timeline, randomness, typography, clipping, transparency and occlusion, transform order, anchors, and easing. Follow dependencies to the actual implementation of every visible element; do not infer the implementation from an entry file or screenshot alone.

Analyze HTML, Remotion, and Hyperframe according to the versions actually used by the project. If interaction, viewport dimensions, or dynamic data produce multiple possible outputs, first select the scene within the user's requested scope. Record the relationship between each visible element, its source implementation and motion, and its planned AE implementation in whatever form the task needs.

## Build the composition tree from the leaves upward

Organize the entire scene as a tree of nested compositions, with the final composition at the root. Build and verify the leaf nodes first. Assemble each parent only after its child nodes are correct, then verify that parent before moving up to the next level.

Use precompositions thoughtfully to organize the project, and aim to keep each composition at no more than 100 layers whenever practical.

Reuse suitable effects, precompositions, and assets wherever possible. Before reusing or duplicating an item, verify that it is usable, its content is correct, and all of its exposed control parameters work as intended. Duplicate or reference it only after these checks pass.

## Rebuild native motion graphics

- Prefer AE's built-in parametric rectangles, rounded rectangles, ellipses, polygons, stars, and shape operators. Use Bezier paths only for custom outlines that parametric shapes genuinely cannot express. Encapsulate complex SVGs as ArbiFX layers, embedding the original SVG inline in the ArbiFX code.
- Define composition order, layer order, masks, blending modes, and parenting clearly. Parenting does not determine occlusion order. Preserve the source matrix multiplication order when combining transforms.
- Use precompositions to encapsulate replaceable components. Preserve their dimensions, anchors, and time origins, and leave enough effect bounds to avoid clipping glows, strokes, or blur.
- For glows and halos, prefer shape layers with Gaussian Blur. Do not approximate a soft halo by assembling many shapes.
- Encapsulate filters without a faithful native AE implementation, complex procedural effects, complex 3D effects, complex SVG animations, complex spatial arrangements of repeated objects, large particle systems, and large numbers of instances as ArbiFX (AFX) effects. Do not build these effects by assembling hundreds or thousands of AE layers.
- Split complex motion across parented Nulls, with each Null responsible for one atomic motion. Derive their hierarchy and order from the source instead of applying a fixed chain template.
- Reproduce motion with as few keyframes as practical and accurate interpolation. Use analytic expressions based on absolute composition time when needed. Do not create per-frame keyframes or expression lookup tables, or replace editable motion graphics with baked video or image sequences.
- Do not insert the source video's final rendered output, in whole or in part, into the AE project as a substitute for rebuilding its content, or present such footage as an implemented reconstruction.

## Procedural effects with ArbiFX

See [Procedural effects with ArbiFX](references/arbifx-effects.md).

## Inspect and correct

Use `ae preview-frame` (or a raw `preview_frame` request to select a composition or time) to export actual AE composition frames. Inspect project structure using returned properties and keyframes. Compare the complete animation against the source, especially transitions, extrema, loop seams, trajectories, occlusion, and parameters. Frame-by-frame comparison is allowed as verification; it does not justify frame-by-frame animation.

Check all expressions throughout the AE project, including nested precompositions, and fix every expression error before delivery.

Check AE preview performance and thoroughly optimize the project to minimize redundant computation while preserving the intended visuals, animation, and editability.

Code inspection, Render output inspection, and actual AE composition inspection are all required. Recheck affected portions after correcting differences. Do not introduce a universal SSIM threshold, fixed repair count, or scoring system. Deliver the editable project, required assets, and author code. Report what was actually verified and any remaining differences; never present unverified work as successful.

Save the AE project after every major stage. Before delivery, confirm that the final save has completed and check the saved project's modification time and file size to ensure that the delivered file contains the latest corrections.
