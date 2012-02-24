## Progressive disclosure

Only show what is relevant, making the interface simpler for the user.
Simply put, you may consider a *relevant* element to be *visible* (“perceivable” as [they say in WCAG][WCAG-P1]), whilst *irrelevant* elements are *hidden*.

[WCAG-P1]: http://www.w3.org/TR/WCAG/#perceivable "Principle 1: Perceivable - Information and user interface components must be presentable to users in ways they can perceive."

### Accessibility

As noted in the HTML5 spec, do not flag elements as irrelevant if you want to temporarily hide them (e.g. tabbed interfaces).
Use `.hide()` from jquery core in those situations. Use this library when elements are irrelevant.
Tabbed interfaces still use *progressive disclosure* techniques, but **should not** use this script.

## Related concepts

* `relevant`, XForms
* `@hidden`, html5
* `@aria-hidden`, ARIA

# API

## `.forcesRelevance( 'relevant', true )`

indicates an element should be made relevant (shown). No change for relevant elements, irrelevant elements will trigger a `relevant` event.

## `.forcesRelevance( 'relevant', false )`

indicates an element should be made irrelevant (hidden). No change for irrelevant elements, relevant elements will trigger an `irrelevant` event.

## `.forcesRelevance( 'show' )`

# enables descendent form elements and self
# removes `@hidden` attribute
# removes `aria-hidden`
# shows the element (uses a `slideDown` transition)
# fires event `relevant-done`

## `.forcesRelevance( 'hide' )`

# hides element (no animation, hiding is immediate)
# disables descendent form fields and self (if a form field)
# adds `@hidden` attribute
# adds `aria-hidden`
# fires event `irrelevant-done`

## Events

|| Event name || Fired when || If you cancel it… ||
| `relevant` | an element that is hidden has become relevant and will be shown | the element will remain irrelevant and stay hidden |
| `irrelevant` | an element that is shown has become irrelevant and will be hidden | the element will remain relevant and be visible |
| `relevant-done` | an element became relevant and is now shown | not applicable |
| `irrelevant-done` | an element became irrelevant and has been hidden | not applicable |

You can suppress the `relevant` and `irrelevant` events and cancel them to prevent an elements relevance state from changing.
You will need to cancel the event before it reaches the `document` (this is where the default handlers are bound).

The `relevant-done` and `irrelevant-done` events are fired after animations are complete and are provided as hooks in case you need to redraw the layout.
