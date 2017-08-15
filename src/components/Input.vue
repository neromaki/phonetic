<template>
    <section class="phonetic-input">
        <div class="container is-fluid">
            <input type="text" class="phonetic-input" v-model="input" @keyup="updateOutput()" />
        </div>
    </section>
</template>

<script type="text/javascript">
export default {
  name: 'Input',
  data() {
    return {
      input: '',
    };
  },
  methods: {
    updateOutput() {
      this.$root.$emit('phoneticUpdate', this.input);
    },
  },
};
</script>
