<template>
    <section class="phonetic-output">
        <span v-for="character in output" v-bind:class="character.type">{{ character.phonetic }}</span>
    </section>
</template>

<script type="text/javascript">
import PhoneticAlphabet from '@/alphabet.json';

export default {
  name: 'Output',
  data() {
    return {
      output: '',
    };
  },
  mounted() {
    const that = this;
    this.$root.$on('phoneticUpdate', (input) => {
      const phoneticOutput = [];
      _.each(input, (char) => {
        const character = _.find(PhoneticAlphabet, { character: char.toUpperCase() });
        if (character) {
          phoneticOutput.push(character);
        }
      });
      that.output = phoneticOutput;
    });
  },
};
</script>
