---
title: Iterate
id: iterate
quote: Two hops this time!

examples:
  - name: Iterate
    template: |
      <div class="example-wrap">
        <XyzTransition xyz="duration-20 ease-in-out-back flip-up-100%" v-xyz="data.utilities" :style="data.variables" v-on="data.listeners">
          <div class="square" v-if="data.toggled"></div>
        </XyzTransition>
      </div>
    code:
      - name: HTML
        content: |
          ##html
          <div class="square ${data.mode}" xyz="duration-20 ease-in-out-back flip-up-100%${data.utilitiesString && ' ' + data.utilitiesString}"></div>

          ${data.variablesString && `
          <style>
            .square { ${data.variablesString} }
          </style>
          `}
      - name: Vue
        content: |
          ##vue
          <XyzTransition xyz="duration-20 ease-in-out-back flip-up-100%${data.utilitiesString && ' ' + data.utilitiesString}">
            <div class="square" v-if="${data.toggled}"></div>
          </XyzTransition>

          ${data.variablesString && `
          ##html
          <style>
            .square { ${data.variablesString} }
          </style>
          `}
      - name: React
        content: |
          ##jsx
          <XyzTransition xyz="duration-20 ease-in-out-back flip-up-100%${data.utilitiesString && ' ' + data.utilitiesString}">
            {${data.toggled} && <div className="square" />}
          </XyzTransition>

          ${data.variablesString && `
          ##html
          <style>
            .square { ${data.variablesString} }
          </style>
          `}

modifiers:
  utilities:
    defaults: [iterate-infinite]
  variables: true
  groups:
    - name: Iterate
      types: [iterate]

---

The iterate utilities and variables set the [animation-iteration-count](https://developer.mozilla.org/en-US/docs/Web/CSS/animation-iteration-count) of an animation. This allows you to have the animation repeat a set number of times or indefinitely.

---
## Variables

<div class="variables-table table-wrap shadow-scroll">
  <table class="shadow-scroll-content">
    <thead>
      <tr>
        <th></th>
        <th>Overall</th>
        <th>In</th>
        <th>Out</th>
        <th>Appear</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <th scope="row">Iterate</th>
        <td>--xyz-iterate</td>
        <td>--xyz-in-iterate</td>
        <td>--xyz-out-iterate</td>
        <td>--xyz-appear-iterate</td>
      </tr>
    </tbody>
  </table>
</div>

See the [variables](#variables) section to learn more.

---
## Defaults

<div class="variables-table table-wrap shadow-scroll">
  <table class="shadow-scroll-content">
    <thead>
      <tr>
        <th></th>
        <th>Variable</th>
        <th>Value</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <th scope="row">Iterate</th>
        <td>--xyz-iterate-default</td>
        <td>1</td>
      </tr>
    </tbody>
  </table>
</div>

See the [defaults](#defaults) section to learn more.
