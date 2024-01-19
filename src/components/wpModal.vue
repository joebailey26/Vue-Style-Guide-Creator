<template>
  <div class="modal">
    <h2>
      Yarn
    </h2>
    <pre>{{ wp.terminal }}</pre>
    <h2>
      CSS
    </h2>
    <pre>{{ wp.css }}</pre>
    <h2>header.php</h2>
    <pre>{{ wp.php }}</pre>
  </div>
</template>

<script>
export default {
  props: {
    wp: {
      type: Object,
      required: true
    }
  }
}
</script>
