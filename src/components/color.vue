<template>
  <ChromePicker v-model="actual" @input="updateColor" />
</template>

<script>
import { Chrome } from '@ckpack/vue-color'

export default {
  name: 'Color',
  components: {
    ChromePicker: Chrome
  },
  props: {
    primary: Boolean,
    secondary: Boolean,
    tertiary: Boolean,
    color: {
      type: String,
      default: '#000000'
    }
  },
  data () {
    return {
      actual: null
    }
  },
  beforeMount () {
    this.actual = this.color
  },
  methods: {
    updateColor () {
      if (this.primary) {
        this.$parent.primaryColor = this.actual.hex
      } else if (this.secondary) {
        this.$parent.secondaryColor = this.actual.hex
      } else if (this.tertiary) {
        this.$parent.tertiaryColor = this.actual.hex
      }
    }
  }
}
</script>
