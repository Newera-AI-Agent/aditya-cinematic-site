---
name: phone-first-cinematic-3d-scroll
description: Build and verify a maintainable single-file index.html for a phone-first cinematic mythical 3D scroll experience using procedural Canvas/WebGL-style effects, particles, touch interaction, reduced-motion support, and no external assets or dependencies.
---

# When to use

Use this skill when the project requires a public static single-page experience with:

- Only `index.html` as the implementation artifact.
- Phone-first responsive behavior.
- Cinematic 3D-style scrolling and scene transitions.
- Procedural visuals instead of external images, models, fonts, libraries, or services.
- Many particles, atmospheric effects, touch interaction, and reduced-motion support.
- Only `Aditya` as visible text.
- Local VM verification before public deployment.
- A user-selected public subdomain named `aditya`.
- No secrets or exposed personal details.

# Rules

1. The implementation MUST be contained in `index.html`; do not add JavaScript libraries, CSS frameworks, external fonts, image files, model files, CDN imports, analytics, trackers, or runtime dependencies.

2. The final page MUST contain no visible human-readable text other than `Aditya`. This includes navigation labels, buttons, instructions, fallback messages, loading labels, tooltips, accessibility text rendered visually, and error messages.

3. `Aditya` MAY be rendered as the primary visual title, but all other UI controls MUST use non-textual affordances such as icons, gestures, visual states, or semantic attributes that do not create visible words.

4. The page MUST be usable on a narrow phone viewport beginning at approximately `320px` CSS width without horizontal scrolling, clipped controls, unreadable content, or interaction requiring hover.

5. The page MUST use a progressive rendering strategy:
   - Prefer WebGL when available.
   - Provide a Canvas 2D fallback.
   - Provide a static CSS/HTML visual fallback if both rendering contexts fail.
   - Never display a visible error message containing text other than `Aditya`.

6. Procedural visuals MUST be generated at runtime from deterministic or seeded mathematics. Do not load or embed external assets through URLs, base64 data, blobs, local files, or remote APIs.

7. The visual system MUST establish a premium mythical look through a restrained palette, layered depth, volumetric-looking light, atmospheric haze, luminous particles, silhouettes, and controlled contrast rather than uncontrolled color or particle noise.

8. The rendering architecture MUST separate:
   - DOM shell and accessibility semantics.
   - Full-screen visual renderer.
   - Procedural scene generation.
   - Scroll and touch input state.
   - Animation scheduling.
   - Reduced-motion and quality adaptation.
   - Resize and device-pixel-ratio management.

9. The scroll experience MUST be represented by normalized progress, not by directly coupling scene state to arbitrary pixel values. Use a clamped progress value in the range `[0, 1]` and derive scene parameters from it.

10. Scene transitions MUST be continuous and reversible. Scrolling forward and backward MUST interpolate the same scene state without accumulating transforms, particles, listeners, or DOM nodes.

11. The implementation MUST use a finite scene model with explicit boundaries. A recommended structure is:
    - Scene 0: dark atmospheric initialization and distant points of light.
    - Scene 1: rising celestial field and central mythic silhouette.
    - Scene 2: orbital energy, parallax layers, and intensified particles.
    - Scene 3: convergence into the `Aditya` title mark.
    - Scene 4: quiet final state with persistent ambient motion.
    
    Scene names and identifiers MUST NOT be rendered as visible text.

12. Each scene MUST define interpolatable parameters rather than imperative one-off effects. Parameters SHOULD include opacity, scale, rotation, camera offset, particle density, particle speed, glow radius, haze strength, and color intensity.

13. The renderer MUST avoid per-frame allocations in hot loops where practical. Reuse typed arrays, particle objects, buffers, gradients, and reusable paths instead of creating large numbers of objects every animation frame.

14. Particle count MUST adapt to device capability. At minimum, support a lower-quality mode based on viewport size, device pixel ratio, frame timing, and `prefers-reduced-motion`.

15. The page MUST cap effective rendering resolution on high-density displays. Do not multiply canvas width and height by unbounded `devicePixelRatio`.

16. The renderer MUST use a single `requestAnimationFrame` loop or an equivalent single scheduler. It MUST stop or reduce work when the document is hidden.

17. Scroll listeners MUST be passive where appropriate and MUST not perform expensive drawing synchronously. Input handlers SHOULD only update state; rendering MUST occur in the animation scheduler.

18. Touch interaction MUST support at least one meaningful gesture, such as swipe-driven scene progress, drag-based parallax, or touch tilt. It MUST not block native page scrolling or trap the user in a gesture-only interface.

19. Pointer and touch effects MUST be bounded and gracefully absent when unavailable. Mouse hover MUST not be required for understanding or completing the experience.

20. `prefers-reduced-motion: reduce` MUST materially reduce motion:
    - Disable or substantially slow camera movement.
    - Remove rapid particle trajectories and oscillation.
    - Preserve a readable, visually complete composition.
    - Keep transitions short and opacity-based where possible.
    
    This behavior MUST be implemented in JavaScript and CSS as appropriate.

21. The page MUST respect safe areas using environment variables such as `env(safe-area-inset-top)` and `env(safe-area-inset-bottom)` where fixed or edge-aligned UI is used.

22. The visible title `Aditya` MUST remain legible over the strongest background state, including on small screens and during transitions. Use contrast, glow control, and a stable text layer rather than relying solely on particle brightness.

23. The page MUST expose meaningful semantics without adding visible text. Use appropriate landmark structure, a descriptive document title only if it does not render as page content, canvas labeling through non-visible semantics, focus states, and keyboard-operable controls where controls exist.

24. Do not place personal information, repository credentials, deployment tokens, API keys, email addresses, local paths, VM details, or private metadata in source, comments, commit messages, or deployment configuration.

25. The public repository MUST contain only intended project files and MUST be checked for secrets before publication.

26. The implementation MUST be maintainable despite being single-file. Organize the file into clearly marked sections:
    1. document shell,
    2. CSS tokens and layout,
    3. renderer constants,
    4. seeded procedural generation,
    5. input state,
    6. scene interpolation,
    7. rendering backends,
    8. animation loop,
    9. capability and motion handling,
    10. initialization.

27. Do not duplicate independent render loops for WebGL, Canvas 2D, particles, and transitions. The active backend MUST consume the same scene state and timing model.

28. WebGL shaders, if used, MUST be embedded directly in `index.html`, must not fetch source files, and MUST have a Canvas 2D fallback that preserves the intended composition rather than showing a blank page.

29. The implementation MUST handle:
    - missing WebGL,
    - context creation failure,
    - context loss,
    - zero-size or hidden canvas,
    - orientation changes,
    - resize storms,
    - unsupported pointer APIs,
    - unavailable `matchMedia`,
    - disabled JavaScript as a noninteractive but non-broken fallback.

30. The experience MUST not depend on an exact browser, GPU, viewport, refresh rate, or scroll speed. It MUST remain coherent at 30 FPS, 60 FPS, and during rapid reverse scrolling.

31. Any visual complexity added for atmosphere MUST be justified by the phone performance budget. Prefer fewer well-layered particles and gradients over unbounded particle counts.

32. Before claiming completion, verify the actual rendered result in the target VM and at phone-sized viewport dimensions. Do not infer visual quality from source inspection alone.

# Steps

1. **Inspect the project contract**
   - Read `TASK_CONTRACT.json`, `TASK_CONTRACT.md`, and `TODO.md`.
   - Extract explicit acceptance criteria, deployment constraints, and prohibited content.
   - Record conflicts before implementation; do not silently override the contract.

2. **Define the single-file architecture**
   - Create `index.html`.
   - Add the document shell, a full-screen visual canvas, the `Aditya` title layer, and a scroll-progress source.
   - Keep all code in the section order required by Rule 26.
   - Verify that no external URLs or dependencies are present.

3. **Establish the visual system**
   - Define CSS custom properties for background, dusk tones, celestial gold, cool shadow, bloom intensity, spacing, and safe-area offsets.
   - Use layered radial and linear gradients for depth.
   - Keep the palette limited and high contrast.
   - Verify that the title remains legible at initial, middle, and final progress.

4. **Implement the scene state**
   - Define normalized progress and explicit scene parameter ranges.
   - Use clamped interpolation and smooth easing functions.
   - Ensure every parameter can be evaluated from current progress without relying on previous frames.
   - Verify forward and reverse scrolling produce identical states at equivalent progress.

5. **Implement deterministic procedural generation**
   - Seed particle positions and properties.
   - Create multiple depth bands with different scale, speed, blur, opacity, and parallax behavior.
   - Add procedural motifs such as arcs, rings, dust, rays, haze, and a central silhouette using paths, gradients, noise-like functions, or shader math.
   - Verify that reloading produces the same composition unless intentional randomization is explicitly required.

6. **Implement the rendering backends**
   - Implement a WebGL backend only if it improves the visual result within the single-file constraint.
   - Implement a Canvas 2D backend with equivalent scene parameters.
   - Add a CSS/DOM fallback that preserves the title and basic atmospheric composition.
   - Verify each backend can initialize independently or fail over without a blank page.

7. **Implement input and scroll behavior**
   - Read scroll position through a passive listener or an equivalent lightweight mechanism.
   - Normalize it against the document’s scrollable range.
   - Add touch or pointer input for bounded parallax or gesture influence without preventing native scrolling.
   - Verify rapid scrolling, reverse scrolling, dragging, and orientation changes.

8. **Implement quality adaptation**
   - Choose a particle and resolution budget from viewport dimensions, device pixel ratio, and frame performance.
   - Reduce quality after sustained frame degradation and optionally restore it after stable performance.
   - Pause or simplify rendering when the document is hidden.
   - Verify that low-end or narrow devices do not receive the desktop particle budget.

9. **Implement reduced-motion support**
   - Add CSS media-query handling for `prefers-reduced-motion`.
   - Add a JavaScript media-query listener where supported.
   - Replace rapid motion with stable composition, restrained opacity changes, and minimal ambient animation.
   - Verify the preference before and after page initialization.

10. **Implement accessibility and non-textual controls**
    - Ensure the canvas has a meaningful non-visible semantic label without adding visible text.
    - Ensure any icon-only control has an accessible name through an appropriate attribute.
    - Provide visible keyboard focus styling for interactive elements.
    - Verify no visible string other than `Aditya` appears in the page viewport.

11. **Run static source checks**
    - Search for external imports, remote URLs, asset fetches, analytics, trackers, credentials, tokens, email addresses, and personal metadata.
    - Search visible DOM content and generated UI for text other than `Aditya`.
    - Confirm there is exactly one `index.html` implementation entry point.
    - Confirm no dependency installation is required.

12. **Run browser verification in the VM**
    - Serve the directory through a local static HTTP server.
    - Test phone viewport widths, at least one larger viewport, portrait and landscape orientation, and device-pixel-ratio variation.
    - Test WebGL enabled, WebGL unavailable, JavaScript errors, rapid scroll, reverse scroll, touch or pointer input, hidden-tab behavior, and reduced motion.
    - Capture screenshots or recordings at initial, intermediate, and final progress.
    - Inspect the browser console for errors, warnings caused by the implementation, and unhandled promise rejections.

13. **Measure performance**
    - Record frame behavior during scrolling on a phone-sized viewport.
    - Check long-task behavior, memory growth, canvas resolution, and particle count.
    - Confirm particles and buffers do not grow after repeated scrolling or resizing.
    - Confirm the page remains interactive under degraded GPU conditions.

14. **Verify the five highest-risk pitfalls**
    - **Rendering overload:** Prove adaptive quality, bounded canvas resolution, reusable particle data, and one scheduler prevent severe phone slowdown.
    - **Scroll/scene desynchronization:** Prove normalized progress and pure interpolation keep transitions reversible and coherent during fast direction changes.
    - **WebGL or platform failure:** Prove Canvas 2D and CSS fallbacks render a complete composition without external assets.
    - **Touch and reduced-motion failure:** Prove touch does not block native scrolling and reduced-motion removes disallowed movement while retaining the intended experience.
    - **Single-file/deployment regressions:** Prove there are no hidden dependencies, external requests, secrets, personal details, or assumptions that fail on a clean static host.

15. **Prepare the public repository**
    - Review the final diff and remove generated files, logs, screenshots containing private information, local paths, and credentials.
    - Confirm the repository contains the intended public source only.
    - Use a public repository only after the source and secret scan pass.

16. **Deploy the selected subdomain**
    - Configure the chosen static hosting provider for the user-selected subdomain `aditya`.
    - Use the provider’s documented DNS and custom-domain process; do not hardcode provider assumptions into the application.
    - Verify HTTPS, the canonical public URL, root-path loading, direct navigation, refresh behavior, and static asset independence.
    - Confirm the deployed page still shows no visible text other than `Aditya`.

17. **Perform public verification**
    - Test the public URL from a clean browser session and a phone-sized viewport.
    - Verify DNS resolution, certificate validity, no mixed-content requests, no unexpected external requests, and no console errors.
    - Recheck the final deployment against the local VM screenshots and interaction checklist.
    - Report only verified outcomes; distinguish unverified hosting or DNS steps from completed implementation work.

# Definition of done

- `index.html` is present and contains the complete implementation.
- No external assets, libraries, dependencies, APIs, secrets, or personal details are used.
- The only visible text is `Aditya`.
- The layout is phone-first, responsive, and free of horizontal overflow.
- The experience contains coherent, reversible, scroll-driven cinematic scenes.
- Procedural particles, depth, atmospheric effects, and mythic visual motifs render without external assets.
- WebGL, Canvas 2D, and CSS fallback behavior has been tested or the unavailable path has been explicitly verified.
- Touch interaction works without blocking native scrolling.
- `prefers-reduced-motion` materially reduces motion while preserving a complete visual experience.
- Rendering uses bounded resolution, adaptive quality, reusable data, and one animation scheduler.
- Fast scrolling, reverse scrolling, resizing, orientation changes, hidden-tab behavior, and degraded rendering conditions have been tested.
- The five highest-risk pitfalls have explicit verification evidence.
- The source has passed dependency, URL, secret, and visible-text checks.
- The project has been run and visually inspected in the VM.
- The public repository contains no unintended private information.
- The selected public subdomain `aditya` resolves over HTTPS and serves the verified experience, if deployment was requested and credentials/DNS control were available.
- Any unavailable deployment or DNS step is reported honestly rather than marked complete.