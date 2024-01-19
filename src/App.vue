<style>
* {
  box-sizing: border-box
}
body {
  display: grid;
  min-height: 100vh;
  margin: 0;
  background: white;
  place-content: center;
  place-items: center
}
#app {
  max-width: 1200px;
  margin: 40px auto 60px;
  padding: 0 2rem;
  color: var(--secondaryColor);
  font-size: var(--fontSize);
  font-family: var(--secondaryFont);
  text-align: left
}
h1, h2, h3, h4, h5, h6 {
  color: var(--primaryColor);
  font-family: var(--primaryFont)
}
.container {
  display: grid;
  gap: 2rem;
  width: 100%;
  place-content: start;
  place-items: start
}
h1, h2 {
  width: 100%;
  margin-bottom: 0
}
.container.column {
  grid-auto-columns: max-content;
  grid-auto-flow: column
}
label {
  width: min-content
}
input {
  padding: 6px;
  font-size: 1.2rem;
  border: 1px solid var(--primaryColor);
  border-radius: var(--borderRadius)
}
.btn {
  min-width: 26ch;
  padding: 1rem;
  border-radius: var(--borderRadius);
  cursor: pointer;
  transition: .5s
}
.primary-btn {
  color: var(--tertiaryColor);
  background-color: var(--primaryColor);
  border: 1px solid var(--secondaryColor)
}
.primary-btn:hover {
  background-color: var(--secondaryColor)
}
.secondary-btn {
  color: var(--primaryColor);
  background-color: var(--tertiaryColor);
  border: 1px solid var(--primaryColor)
}
.secondary-btn:hover {
  color: var(--tertiaryColor);
  background-color: var(--primaryColor)
}
.fonts {
  align-items: start
}
.modal-container {
  background-color: rgba(0,0,0,0.5)
}
.modal-item {
  width: 80%;
  margin-left: auto;
  margin-right: auto;
  background-color: white;
  padding: 1rem 1.5rem;
  max-height: 80%;
  overflow: auto;
}
pre {
  display: block;
  width: 100%;
  padding: 1rem;
  white-space: pre-wrap;
  word-wrap: break-word;
  background-color: #EFEFEF;
  border-radius: 8px;
  user-select: all
}
div[id^='font-picker'], .vc-chrome {
  border: 1px solid #AFAFAF;
  /* stylelint-disable-next-line declaration-no-important */
  box-shadow: none!important
}
</style>

<template>
  <div id="app" class="container" :style="variables">
    <div>
      <h1>
        Style Guide Creator
      </h1>
      <h2>Colors</h2>
    </div>
    <div class="colors container column">
      <Color :primary="true" color="#1a237e" />
      <Color :secondary="true" color="#212121" />
      <Color :tertiary="true" color="#ffffff" />
    </div>
    <h2>Typography</h2>
    <div class="fonts">
      <div class="container column">
        <label>
          Heading Font
          <!-- <FontPicker :api-key="apiKey" :options="options1" :active-font="fontHeading.family" @change="headingFont" /> -->
        </label>
        <label>
          Body Font
          <!-- <FontPicker :api-key="apiKey" :options="options2" :active-font="fontBody.family" @change="bodyFont" /> -->
        </label>
        <label>
          Font Size
          <input v-model.number="fontSize" type="number">
        </label>
      </div>
      <h1>Heading 1</h1>
      <h2>Heading 2</h2>
      <h3>Heading 3</h3>
      <h4>Heading 4</h4>
      <h5>Heading 5</h5>
      <h6>Heading 6</h6>
      <p>I show my fluffy belly but it's a trap! if you pet it i will tear up your hand. Check cat door for ambush 10 times before coming in cat fur is the new black and i hate cucumber pls dont throw it at me jump on counter removed by human jump on counter again removed by human meow before jumping on counter this time to let the human know am coming back.</p>
    </div>
    <h2>Variables</h2>
    <div class="inputs container column">
      <label>
        Border Radius
        <input v-model.number="borderRadius" type="number">
      </label>
    </div>
    <h2>Download / Buttons</h2>
    <div class="btns container column">
      <button class="btn primary-btn" @click="openModal(NuxtModal, { nuxt })">
        Get code for Vue/Nuxt
      </button>
      <button class="btn secondary-btn" @click="openModal(WpModal, { wp })">
        Get code for WordPress
      </button>
    </div>
    <ModalContainer />
  </div>
</template>

<script>
// import FontPicker from 'font-picker-vue'
import { container, openModal } from 'jenesius-vue-modal'
import Color from './components/color'
import NuxtModal from './components/nuxtModal'
import WpModal from './components/wpModal'

export default {
  components: {
    Color,
    // FontPicker,
    ModalContainer: container
  },
  setup () {
    return { openModal, NuxtModal, WpModal }
  },
  data () {
    return {
      apiKey: 'AIzaSyCYTib-0NYDlyJQbJACMdIGoP2qgw3zXNc',
      borderRadius: 0,
      primaryColor: '#1a237e',
      secondaryColor: '#212121',
      tertiaryColor: '#ffffff',
      fontHeading: {
        family: 'Open Sans',
        category: 'sans-serif'
      },
      fontBody: {
        family: 'Open Sans',
        category: 'sans-serif'
      },
      fontSize: 16,
      options1: {
        name: 'headings'
      },
      options2: {
        name: 'body'
      }
    }
  },
  computed: {
    variables () {
      return `--primaryColor: ${this.primaryColor};
  --secondaryColor: ${this.secondaryColor};
  --tertiaryColor: ${this.tertiaryColor};
  --primaryFont: ${this.fontHeading.family}, ${this.fontHeading.family} fallback, ${this.fontHeading.category};
  --secondaryFont: ${this.fontBody.family}, ${this.fontBody.family} fallback, ${this.fontBody.category};
  --borderRadius: ${this.borderRadius}px;
  --fontSize: ${this.fontSize}px`
    },
    nuxt () {
      return {
        css: `@font-face {
  font-family: ${this.fontHeading.family} fallback;
  size-adjust: 100%; // Adjust as needed
  src: local('Arial') // Change as needed
}
@font-face {
  font-family: ${this.fontBody.family} fallback;
  size-adjust: 100%; // Adjust as needed
  src: local('Arial') // Change as needed
}
:root {
  ${this.variables}
}
h1, h2, h3, h4, h5, h6 {
  font-family: var(--primaryFont);
  color: var(--primaryColor)
}
body {
  font-family: var(--secondaryFont);
  color: var(--secondaryColor)
}`,
        terminal: `yarn add @fontsource/${this.fontHeading.family.toLowerCase().replaceAll(' ', '-')} ${this.fontBody.family !== this.fontHeading.family ? `@fontsource/${this.fontBody.family.toLowerCase().replaceAll(' ', '-')}` : ''}`,
        js: `css: [
  '@fontsource/${this.fontHeading.family.toLowerCase().replaceAll(' ', '-')}/400.css',
  '@fontsource/${this.fontHeading.family.toLowerCase().replaceAll(' ', '-')}/700.css',
  ${this.fontBody.family !== this.fontHeading.family
  ? `'@fontsource/${this.fontBody.family.toLowerCase().replaceAll(' ', '-')}/400.css',
  '@fontsource/${this.fontBody.family.toLowerCase().replaceAll(' ', '-')}/700.css'`
: ''}
]`
      }
    },
    wp () {
      return {
        css: `@font-face {
  font-family: ${this.fontHeading.family} fallback;
  size-adjust: 100%; // Adjust as needed
  src: local('Arial') // Change as needed
}
@font-face {
  font-family: ${this.fontBody.family} fallback;
  size-adjust: 100%; // Adjust as needed
  src: local('Arial') // Change as needed
}
:root {
  ${this.variables}
}
h1, h2, h3, h4, h5, h6 {
  font-family: var(--primaryFont);
  color: var(--primaryColor)
}
body {
  font-family: var(--secondaryFont);
  color: var(--secondaryColor)
}`,
        terminal: `yarn add @fontsource/${this.fontHeading.family.toLowerCase().replaceAll(' ', '-')} ${this.fontBody.family !== this.fontHeading.family ? `@fontsource/${this.fontBody.family.toLowerCase().replaceAll(' ', '-')}` : ''}`,
        php: `function galexia_enqueue_fonts() {
  wp_enqueue_style( '${this.fontHeading.family.toLowerCase().replaceAll(' ', '-')}-regular', get_template_directory_uri() . '/node_modules/@fontsource/${this.fontHeading.family.toLowerCase().replaceAll(' ', '-')}/400.css' );
  wp_enqueue_style( '${this.fontHeading.family.toLowerCase().replaceAll(' ', '-')}-bold', get_template_directory_uri() . '/node_modules/@fontsource/${this.fontHeading.family.toLowerCase().replaceAll(' ', '-')}/700.css' );
  ${this.fontBody.family !== this.fontHeading.family
  ? `wp_enqueue_style( '${this.fontBody.family.toLowerCase().replaceAll(' ', '-')}-regular', get_template_directory_uri() . '/node_modules/@fontsource/${this.fontBody.family.toLowerCase().replaceAll(' ', '-')}/400.css' );
  wp_enqueue_style( '${this.fontBody.family.toLowerCase().replaceAll(' ', '-')}-bold', get_template_directory_uri() . '/node_modules/@fontsource/${this.fontBody.family.toLowerCase().replaceAll(' ', '-')}/700.css' );`
: ''}
}
add_action( 'wp_enqueue_scripts', 'galexia_enqueue_fonts' );`
      }
    }
  },
  methods: {
    headingFont (font) {
      this.fontHeading = font
    },
    bodyFont (font) {
      this.fontBody = font
    }
  }
}
</script>
