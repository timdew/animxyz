---
title: Utilities
id: utilities
quote: With our powers combined...

examples:
  - name: Utilities
    template: |
      <div class="example-wrap">
        <XyzTransition duration="auto" v-xyz="data.utilities" v-on="data.listeners">
          <div class="item-group xyz-none" v-if="data.toggled">
            <div class="square xyz-nested" v-for="index in 3" :key="index"></div>
          </div>
        </XyzTransition>
      </div>
    code:
      - name: HTML
        content: |
          ##html
          <div class="item-group" ${data.utilitiesString && `xyz="${data.utilitiesString}"`}>
            <div class="square ${data.mode}"></div>
            <div class="square ${data.mode}"></div>
            <div class="square ${data.mode}"></div>
          </div>
      - name: Vue
        content: |
          ##vue
          <XyzTransitionGroup class="item-group" ${data.utilitiesString && `xyz="${data.utilitiesString}"`}>
            <div class="square" v-if="${data.toggled}"></div>
            <div class="square" v-if="${data.toggled}"></div>
            <div class="square" v-if="${data.toggled}"></div>
          </XyzTransitionGroup>
      - name: React
        content: |
          ##jsx
          <XyzTransitionGroup className="item-group" ${data.utilitiesString && `xyz="${data.utilitiesString}"`}>
            {${data.toggled} && <div className="square" />}
            {${data.toggled} && <div className="square" />}
            {${data.toggled} && <div className="square" />}
          </XyzTransitionGroup>

modifiers:
  utilities:
    defaults: [fade]
  variables:
    hide: true
  groups:
    - name: Fade
      types: [opacity]
    - name: Translate
      types: [translate]
    - name: Rotate
      types: [rotate]
    - name: Scale
      types: [scale]
    - name: Skew
      types: [skew]
    - name: Perspective
      types: [perspective]
    - name: Origin
      types: [origin]
    - name: Timing
      types: [duration, delay]
    - name: Ease
      types: [ease]
    - name: Stagger
      types: [stagger]
    - name: Iterate
      types: [iterate]
    - name: Direction
      types: [direction]
---

AnimXYZ has the unique ability to mix and match animation utilities, letting you compose an enormous variety of animations without any extra code. For example `xyz="up left small"` will make an element move to and from the upper left while expanding in and contracting out. Spin an element while collapsing it to a sliver, expand an element while it swings in from its corner, the possibilities are endless! Here are just a few of the many combinations you can do:

[😐 fade up](?tab=examples&utilities=fade;up#utilities)  
[🙂 fade flip-up flip-left](?tab=examples&utilities=fade;flip-up;flip-left#utilities)  
[😀 fade down-5 rotate-right-50% stagger](?tab=examples&utilities=fade;down-5;rotate-right-50%;stagger#utilities)  
[😃 fade front-3 flip-down-50% duration-10 stagger-5](?tab=examples&utilities=fade;front-3;flip-down-50%;duration-10;stagger-5#utilities)  
[🤪 fade up-100% flip-down flip-right-50% rotate-left-100% origin-bottom duration-10 stagger](?tab=examples&utilities=fade;up-100%;flip-down;flip-right-50%;rotate-left-100%;origin-bottom;duration-10;stagger#utilities) 

### Direction Variants
Utilities can be applied specifically to one of the animation direction variants **In**, **Out**, and **Appear** by prepending the utility with the variant name. For example if you wanted a longer duration and a different translate direction coming in versus out you could set `xyz="fade up out-down appear-big duration-5 in-duration-10"`. Check out the [active classes](#active-classes) section to learn more about using different utilities when animating in or out.

### Conflicts
Certain utilities won't work with other utilities if they both change the same property. For example `xyz="up down"` will not work because both `up` and `down` change the `--xyz-translate-y` variable. 

### Variables
Every utility sets one or more [AnimXYZ variables](#variables). If you manually set the variable on an element, it will take precedence over the value set by any utilities.

You can combine utilities with variables for more custom animations. For example `xyz="fade tall" style="--xyz-rotate-z: 33deg"` will make an element fade and change height by their default amounts, and rotate in and out by 33 degrees.
