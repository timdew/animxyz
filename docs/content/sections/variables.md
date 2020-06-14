---
title: Variables

examples:
  - name: variables
    title: Variables
    template: |
      <xyz-transition-group tag="div" class="square-group" xyz="fade" v-on="data.listeners">
        <div class="square" v-for="index in 3" v-show="data.toggled" :key="index"></div>
      </xyz-transition-group>
    code:
      - language: html
        content: |
          <div class="square-group" xyz="fade">
            <div class="square ${data.mode}"></div>
            <div class="square ${data.mode}"></div>
            <div class="square ${data.mode}"></div>
          </div>

modifiers:
  utilities:
    hide: true
  groups:
    - name: fade
      title: Fade
      types: [fade]
    - name: translate
      title: Translate
      types: [translate]
    - name: rotate
      title: Rotate
      types: [rotate]
    - name: scale
      title: Scale
      types: [scale]
    - name: origin
      title: Origin
      types: [origin]
    - name: timing
      title: Timing
      types: [duration, delay, stagger]
    - name: ease
      title: Ease
      types: [ease]
---

This is the variables section