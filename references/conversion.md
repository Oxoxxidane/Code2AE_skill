# Code-to-AE conversion guide

## Research

Identify the requested entry point or scene, then trace every dependency that affects visible output. Check that fonts actually load, remote assets are stable, and random seeds and timing are reproducible. Capture or render the source at its original dimensions and pixel aspect ratio, recording the corresponding time. Do not infer fine detail from thumbnails.

For HTML, understand DOM stacking contexts, CSS layout, and transform-origin; z-index values are comparable only within the same stacking context. Inspect CSS animation, transition, WAAPI, and JavaScript-driven timing. For Remotion, trace compositions, nested Sequence offsets, the current frame, interpolate, spring, and asset durations. For Hyperframe, read the installed version and actual entry points rather than assuming it shares another framework's API.

If interaction, viewport size, or live data can produce multiple outputs, establish the state and time range to reproduce. Regular repetition, black frames, transparency, cropping, unusual colors, and depth of field in the source are part of its design. Do not inadvertently change them to follow generic authoring advice.

## Graphics and layers

Decompose objects according to their source geometry, preferring AE parametric shapes and built-in Fill, Stroke, Trim Paths, Repeater, and similar operators. Exact curves supplied by source SVGs may be converted directly into paths. For overly complex SVGs, consider an ArbiFX layer with the SVG embedded inline in author code and 24 adjustable parameters. Do not turn objects expressible with AE circles, rectangles, stars, or other built-in shapes into dense Bezier outlines.

Keep text as native editable AE text where possible. Check fonts, weights, tracking, leading, alignment, line breaks, and actual glyphs. Reference real images, videos, and textures as the source does; do not replace editable graphics with screenshots.

Layer stacking, parent transforms, masks, and precompositions are four distinct relationships and cannot substitute for one another. Define each order and inspect crossings and intersections. Organize precompositions around genuinely replaceable components, without prescribing a fixed number of levels. Applying effects inside or outside a precomposition changes blending, cropping, and color. Preserve the bounds needed by the source for blur, strokes, and glow.

## Motion

Understand the source motion functions and matrix multiplication order before choosing keyframes or analytic expressions. Nulls may separate layout, orbit, translation, self-rotation, and scale, but do not force every object into the same chain. Each Null handles one atomic motion; do not combine unrelated motions in a single controller.

CSS cubic-bezier describes time easing, not spatial path tangents. Inspect AE temporal interpolation and spatial interpolation separately. Use as few necessary keyframes as possible for ordinary segmented motion; retain continuous spring, periodic, and deterministic-noise functions with mathematical expressions. Do not write sampled values as per-frame keyframes or expression lookup tables.

Check local time offsets, loop boundaries, first and last frames, holds, extrema, and transitions, not just the two endpoints. Use only language features and interfaces supported by the target AE version.

## ArbiFX

Use the source to divide procedural ArbiFX work from native motion graphics. Image inputs, named layer inputs, transparent output, cameras, lights, and time must correspond to the original effect. Keep intersecting subjects or complex depth relationships in the same rendering unit; arbitrary splitting into independent planes cannot preserve their occlusion.

Retrieve authoring materials through Render CLI. Read all seven rules, notes, the API allowlist, and the selected complete template before writing code. Design 24 controls for the actual effect, with defaults matching the source. Apply hundredfold display conversion only once: the host already converts percent parameters. Explicitly convert other manually scaled display values back to internal units in author code.

Check the real correspondence among shaders, uniforms, geometry attributes, handles, and APIs. Fix Render errors locally at the reported positions; do not replace APIs based on guesses. Confirm that camera and light changes visibly affect the subject instead of being declarations only. Inspect the output PNG's actual alpha rather than inferring transparency from a JPEG on a background.

For fullscreen shaders, follow the closest template when deciding whether NoBlending is appropriate and interpreting output alpha. Composite exported images over a background to detect double multiplication by alpha, dark edges, or disappearing glow; a transparent-background preview alone is insufficient. Choose blending for multi-object 3D scenes according to their actual occlusion relationships, rather than universally switching to NoBlending.

## Verification

Compare source and AE at matching dimensions, times, and inputs. Inspect speed, rhythm, trajectories, and occlusion throughout the animation, using difference images or frame-by-frame checks as needed. Confirm that parametric shapes, text, parent chains, precompositions, and all 24 controls remain editable and effective.

Inspect 3D structure and occlusion from multiple directions, especially openings, glass, internal structures, z-fighting, and incorrect normals. Auxiliary views test structure; their composition need not match the default delivery view.

After saving, confirm that project assets and effects can be restored. Explicitly report differences that remain despite attempted fixes, and checks prevented by missing environment capabilities. Do not substitute a universal visual score or arbitrary tolerance for actual judgment.
