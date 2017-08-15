<template>
    <section class="phonetic-output">
        <div class="container is-fluid">
            <h2>Output</h2>
            <span v-for="character in output">{{ character.phonetic }}</span>
        </div>
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
