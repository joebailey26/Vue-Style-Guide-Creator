<template>
  <div class="modal">
    <h2>
      Yarn
    </h2>
    <pre>{{ nuxt.terminal }}</pre>
    <h2>
      CSS
    </h2>
    <pre>{{ nuxt.css }}</pre>
    <h2>nuxt.config.js</h2>
    <pre>{{ nuxt.js }}</pre>
  </div>
</template>

<script>
export default {
  props: {
    nuxt: {
      type: Object,
      required: true
    }
  }
}
</script>
