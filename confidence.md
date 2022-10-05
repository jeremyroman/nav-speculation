# Modelling confidence

When a user agent is presented with potentially many links to preload, it's useful to have a conceptual model for how "confidence" (roughly, precision and recall) work, even if the goal is not to confine the user agent's exact approach.

This can be thought of in a few aspects:

* __prior confidence__ that a user will navigate to a link
* __computed confidence__ given the prior confidence and signals such as user interaction and charateristics of the link
* __target confidence__ which indicates what the computed confidence should be before prefetching is attempted (an adjusted level may be used for simply doing DNS prefetch or preconnect, if applicable); this reflects the "cost" to the user, author or service provider

Browsers take action when computed confidence exceeds target confidence.

These are expressly not probabilities, precision/recall targets, etc., though they're intended to explain the behavior that results in those.

## Prior confidence

By default, the prior confidence mode is "`auto`". In that case, it is computed by some simple rules which are included in the specification, such as:

* if the candidate was found in a list rule, then the prior confidence is _(some constant TBD)_
* if the candidate was found in a document rule, then the prior confidence is _(some constant TBD)_

If this proves not suitable for all cases, this can be fully replaced by an author-specified value in the rule or, possibly, as a content attribute on the individual links (in the case of document rules).

## Computed confidence

Browsers can adjust these in implementation-, platform-, device- and user-specific ways. For example, the following seem likely to be desirable:
* if a link is not in the viewport, adjust its confidence downward
* if a link is hovered (where the pointer supports hover) or focused, or is so for some amount of time, adjust its confidence upward
* if a pointer is currently down on a link, adjust its confidence upward

## Target confidence

By default, the target confidence mode is "`auto`". In that case, it is computed by some simple rules which are included in the specification, such as:

* if the candidate URL is same-origin, then the target confidence is _(some constant TBD)_
* if the candidate URL is cross-origin, then the target confidence is _(some constant TBD)_

If this proves not suitable for all cases, this can be fully replaced by an author-specified value in the rule or, possibly, as a content attribute on the individual links (in the case of document rules).