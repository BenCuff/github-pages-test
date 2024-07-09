---
title: "Test page"
layout: guidance-page
---

[https://www.w3.org/WAI/tutorials/carousels/animations/](https://www.w3.org/WAI/tutorials/carousels/animations/)


## Carousel

<div role="region" aria-roledescription="carousel" aria-label="Tips & Techniques">
  <div role="group" aria-label="Slide controls">
    <button aria-label="Stop auto-rotation">
      <!-- SVG icon -->
    </button>
    <button aria-disabled="true">
      <span class="hide-element">Show slide 1 of 3: Hiding Accessibly</span>
      <!-- SVG icon -->
    </button>
    <button aria-disabled="false">
      <span class="hide-element">Show slide 2 von 3: Accessible Contrasts</span>
      <!-- SVG icon -->
    </button>
    <button aria-disabled="false">
      <span class="hide-element">Show slide 3 von 3: Semantics, WAI-ARIA and Assistive Technologies</span>
      <!-- SVG icon -->
    </button>
    <button aria-label="Previous slide">
      <!-- SVG icon -->
    </button>
    <button aria-label="Next slide">
      <!-- SVG icon -->
    </button>
  </div>
  <div role="group" aria-roledescription="Slide" aria-labelledby="carousel-item-1__heading" id="carousel-item-1">
    <h2 id="carousel-item-1__heading">Hiding accessibly</h2>
    <!-- Further slide contents -->
  </div>
  <div hidden role="group" aria-roledescription="Slide" aria-labelledby="carousel-item-2__heading" id="carousel-item-2">
    <h2 id="carousel-item-2__heading">Accessible Contrasts</h2>
    <!-- Further slide contents -->
  </div>
  <div hidden role="group" aria-roledescription="Slide" aria-labelledby="carousel-item-3__heading" id="carousel-item-3">
    <h2 id="carousel-item-3__heading">Semantics, WAI-ARIA and Assistive Technologies</h2>
    <!-- Further slide contents -->
  </div>
</div>
</script>