<template>
  <component :is="wrapper" :class="['input', { 'input-expand': width === 'expand' }]">
    <label :for="id" v-if="label">{{ label }}</label>
    <input
      :id="id"
      :disabled="disabled"
      :type="type"
      :value="value"
      :class="state"
      :placeholder="placeholder"
      @input="onInput($event.target.value)"
      @focus="onFocus($event.target.value)"
    />
  </component>
</template>

<script>
/**
 * Form Inputs are used to allow users to provide text input when the expected
 * input is short. Form Input has a range of options and supports several text
 * formats including numbers. For longer input, use the form `Textarea` element.
 */
export default {
  name: "Input",
  status: "ready",
  release: "1.0.0",
  props: {
    /**
     * The type of the form input field.
     * `text, number, email`
     */
    type: {
      type: String,
      default: "text",
      validator: value => {
        return value.match(/(text|number|email)/)
      },
    },
    /**
     * Text value of the form input field.
     */
    value: {
      type: String,
      default: null,
    },
    /**
     * The placeholder value for the form input field.
     */
    placeholder: {
      type: String,
      default: null,
    },
    /**
     * The label of the form input field.
     */
    label: {
      type: String,
      default: null,
    },
    /**
     * The html element name used for the wrapper.
     * `div, section`
     */
    wrapper: {
      type: String,
      default: "div",
      validator: value => {
        return value.match(/(div|section)/)
      },
    },
    /**
     * Unique identifier of the form input field.
     */
    id: {
      type: String,
      default: null,
    },
    /**
     * The width of the form input field.
     * `auto, expand`
     */
    width: {
      type: String,
      default: "expand",
      validator: value => {
        return value.match(/(auto|expand)/)
      },
    },
    /**
     * Whether the form input field is disabled or not.
     * `true, false`
     */
    disabled: {
      type: Boolean,
      default: false,
    },
    /**
     * Manually trigger various states of the input.
     * `hover, active, focus`
     */
    state: {
      type: String,
      default: null,
      validator: value => {
        return value.match(/(hover|active|focus)/)
      },
    },
  },
  methods: {
    onInput(value) {
      this.$emit("change", value)
    },
    onFocus(value) {
      this.$emit("focus", value)
    },
  },
}
</script>

<style lang="scss" scoped>
// Design Tokens with local scope
$color-placeholder: $color-grey-dark;

.input {
  @include stack-space($space-s);
  font-weight: $weight-normal;
  font-family: $font-text;
  font-size: $size-s;
  line-height: $line-height-xs;
  width: auto;
  &-expand {
    width: 100%;
  }
  label {
    cursor: pointer;
    display: block;
    font-size: $size-xs;
    color: $color-asphalt;
    @include stack-space($space-xxs);
  }
  input {
    @include reset;
    @include inset-squish-space($space-s);
    box-sizing: border-box;
    transition: all 0.2s ease;
    -webkit-appearance: none;
    appearance: none;
    font-size: $size-s;
    font-family: $font-text;
    background: $color-white;
    border-radius: $radius-default;
    color: $color-asphalt;
    width: 100%;
    margin: 0;
    border: 1px solid $color-asphalt;
    box-shadow: 0 0 0 0;
    padding: $space-xs $space-s;
    &::-webkit-input-placeholder {
      -webkit-font-smoothing: antialiased;
      color: $color-placeholder;
    }
    &:-ms-input-placeholder {
      color: $color-placeholder;
    }
    &::-moz-placeholder {
      color: $color-placeholder;
      -moz-osx-font-smoothing: grayscale;
      opacity: 1;
    }
    &:hover,
    &.hover {
      box-shadow: $shadow-s;
    }
    &:focus,
    &.focus {
      transition: box-shadow 0.2s ease;
      box-shadow: $shadow-focus;
      outline: 0;
    }
    &[disabled] {
      -webkit-font-smoothing: antialiased;
      -moz-osx-font-smoothing: grayscale;
      box-shadow: 0 0 0 1px tint($color-grey-darker, 80%);
      background: lighten($color-placeholder, 42%);
      color: $color-asphalt;
      cursor: not-allowed;
      opacity: 0.7;
      background: $color-grey;
      border: 1px solid $color-grey;
    }
  }
}
</style>

<docs>
  ```jsx
  <div>
    <Input label="Default input" placeholder="Write your text" id="input-1" />
    <Input label=":hover" state="hover" placeholder="Write your text" id="input-2" />
    <Input label=":focus" state="focus" placeholder="Write your text" id="input-3" />
    <Input label="[disabled]" disabled id="input-4" />
    <Input label="[disabled]" value="Disabled text" disabled id="input-4" />

    <div style="display:flex;">
      <Button>Subscribe</Button>
      <Input placeholder="Write your text" id="input-1"/>
    </div>
  </div>
  ```
</docs>
