# Native HTML FAQ

A small, responsive FAQ example built with `details`, `summary` and CSS. The browser handles disclosure state; there is no JavaScript, framework, build step, analytics or external asset request.

This is the source companion to [A native HTML FAQ that leaves room for real answers](https://stormystudios.hashnode.dev/a-native-html-faq-that-leaves-room-for-real-answers). It demonstrates a practical starting point, with the decisions and testing limits documented below.

## Open the example

Download `index.html` and open it in a browser. Its CSS is embedded in the document, so it also works offline. GitHub's file view displays the source; it does not run the page.

The example contains four questions. The first starts open, and opening another question leaves the earlier answer available. Use Tab to reach a question, then Enter or Space to toggle it in browsers that support the native disclosure interaction.

## Why these choices?

### Native state and a clear label

Each question is the first `summary` child of its `details` element. The answer follows it in ordinary HTML. No custom button role, click handler or manually maintained `aria-expanded` value is needed for this native pattern.

```html
<details class="faq-item">
  <summary>
    <span>Does this need JavaScript?</span>
    <span class="faq-icon" aria-hidden="true"></span>
  </summary>
  <div class="answer">
    <p>The browser manages the disclosure state.</p>
  </div>
</details>
```

The plus/minus icon is decorative and hidden from assistive technology. The question text supplies the label. The `open` attribute on the first item controls its initial state: remove it to start closed. Setting `open="false"` still opens an item because this attribute is Boolean.

### Several answers can remain open

The items have no shared `name` attribute. A shared name creates an exclusive group in supporting browsers, where opening one item closes another. Independent items suit readers who want to compare answers; the trade-off is a longer page when several are expanded.

Essential information such as opening hours, prices or contact details should also appear where people need it elsewhere on the website.

### Space for real content

The wrapper is limited to `46rem`, with space at either side on smaller screens. Answers have no fixed height, maximum height or separate scrolling region. They expand the normal document flow. Inherited `overflow-wrap: anywhere` allows long unbroken strings to wrap.

This does not prevent a parent page from imposing its own constraints. A fixed-height section, clipped container or scroll-snapping layout still needs testing with the actual content.

### Focus and motion

The whole summary is interactive, with padding and a minimum height. A three-pixel `:focus-visible` outline identifies keyboard focus. Avoid removing it or placing the component inside a container that clips it.

Only the icon has a short transition; the answer does not animate its height. `prefers-reduced-motion: reduce` removes that transition while preserving the immediate state change. A forced-colours rule uses `CanvasText` for the icon.

## Check it in context

Use real content and the browsers your audience uses:

1. Open the final question and read its answer to the end on a narrow screen.
2. Try a long question, several answer paragraphs and an unbroken URL.
3. Increase text size or browser zoom and check for clipping and horizontal scrolling.
4. Navigate with Tab, activate with Enter and Space, then move forward and backwards without a mouse.
5. Keep multiple answers open and verify that the surrounding page still lets you read them.
6. Enable reduced motion and forced colours, then check the focus indicator and icon.
7. Test with relevant screen readers and platform combinations before relying on the component in a production accessibility assessment.

The original CodePen version has recorded Chrome keyboard/Enter checks and a signed-out browser check at a 390px viewport, where the final answer was readable. This standalone packaging has received static HTML/CSS checks; it has not received a new browser or screen-reader audit. Neither those checks nor the native elements establish WCAG conformance or universal usability.

## References

- [HTML Standard: the details element](https://html.spec.whatwg.org/multipage/interactive-elements.html#the-details-element)
- [MDN: details and the open/name attributes](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/details)
- [MDN: summary accessibility differences](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/summary#accessibility)
- [MDN: focus-visible](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Selectors/:focus-visible)
- [MDN: prefers-reduced-motion](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/At-rules/@media/prefers-reduced-motion)

Prepared with AI assistance from the original demo and its published tutorial. No open-source licence has been selected or added.

An interface example by [Stormy Studios](https://stormystudios.com/), Cornwall.
