<template>
    <section class="phonetic-input">
            <p>for when you can't remember <span class="phonetic-input--wrap"><span>{{ phonemeOne.phonetic }}</span> from <span>{{ phonemeTwo.phonetic }}</span></span></p>
            <label id="phonetic-input--label" for="phonetic-input">Type in what you're trying to say</label>
            <input type="text" id="phonetic-input" class="phonetic-input" v-model="input" ref="phoneticInput" @keyup="updateOutput()" placeholder="Type in what you're trying to say" aria-labelledby="phonetic-input--label" autofocus>
    </section>
</template>

<script type="text/javascript">
import PhoneticAlphabet from '@/alphabet.json';

export default {
  name: 'Input',
  data() {
    return {
      input: '',
      phonemeOne: '',
      phonemeTwo: '',
    };
  },
  mounted() {
    this.$root.$emit('phoneticUpdate', this.input);
    this.updatePhonetics();

    setInterval(() => {
      this.updatePhonetics();
    }, 2000);

    this.$refs.phoneticInput.focus();
  },
  methods: {
    updateOutput() {
      this.$root.$emit('phoneticUpdate', this.input);
    },
    updatePhonetics() {
      this.phonemeOne = PhoneticAlphabet[_.random(0, 24)];
      this.phonemeTwo = PhoneticAlphabet[_.random(0, 24)];
      while (this.phonemeOne === this.phonemeTwo) {
        this.phonemeTwo = PhoneticAlphabet[_.random(0, 24)];
      }
    },
  },
};
</script>
