<template>
    <section class="phonetic-output">
        <div class="output">
            <span v-for="character in output" v-bind:class="[character.active ? 'active' : '', character.type]">{{ character.phonetic }}</span>
        </div>

        <div v-if="output.length > 0" class="output-controls">
            <button type="button" class="previous" data-action="previous" @click="phoneticMovePrevious">
                <svg viewBox="0 0 582 998" aria-labelledby="assi-awesome-angle-left-title" id="si-awesome-angle-left" width="100%" height="100%"><title id="assi-awesome-angle-left-title">icon angle-left</title><path d="M582 83q0 13-10 23L179 499l393 393q10 10 10 23t-10 23l-50 50q-10 10-23 10t-23-10L10 522Q0 512 0 499t10-23L476 10q10-10 23-10t23 10l50 50q10 10 10 23z"></path></svg>
            </button>
            <button type="button" class="next" data-action="next" @click="phoneticMoveNext">
                <svg viewBox="0 0 582 998" aria-labelledby="atsi-awesome-angle-right-title" id="si-awesome-angle-right" width="100%" height="100%"><title id="atsi-awesome-angle-right-title">icon angle-right</title><path d="M582 499q0 13-10 23L106 988q-10 10-23 10t-23-10l-50-50Q0 928 0 915t10-23l393-393L10 106Q0 96 0 83t10-23l50-50Q70 0 83 0t23 10l466 466q10 10 10 23z"></path></svg>
            </button>
        </div>
    </section>
</template>

<script type="text/javascript">
import PhoneticAlphabet from '@/alphabet.json';

const find = require('lodash/find');
const each = require('lodash/each');
const findIndex = require('lodash/findIndex');

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

      each(input, (char) => {
        const character = find(PhoneticAlphabet, { character: char.toUpperCase() });
        if (character) {
          character.active = false;
          // Pushing the actual object from the json creates a reference to it instead of a copy,
          // which makes the whole 'move the active phonetic' a bit weird
          phoneticOutput.push(
            {
              active: false,
              character: character.character,
              phonetic: character.phonetic,
              type: character.type,
            },
          );
        }
      });
      that.output = phoneticOutput;
      if (that.output.length > 0) {
        that.output[0].active = true;
      }
    });
  },
  methods: {
    phoneticMoveNext() {
      const charIndex = findIndex(this.output, { active: true });

      if (charIndex >= 0 && (charIndex + 1) <= (this.output.length - 1)) {
        this.output[charIndex].active = false;
        this.output[charIndex + 1].active = true;
      }
    },

    phoneticMovePrevious() {
      const charIndex = findIndex(this.output, { active: true });

      if ((charIndex - 1) >= 0 && charIndex <= (this.output.length - 1)) {
        this.output[charIndex].active = false;
        this.output[charIndex - 1].active = true;
      }
    },
  },
};
</script>
