<template>
    <section class="phonetic-input">
            <p>for when you can't remember <span class="phonetic-input--wrap"><span>{{ phoneticOne.phonetic }}</span> from <span>{{ phoneticTwo.phonetic }}</span></span></p>
            <label id="phonetic-input--label" for="phonetic-input">Type in what you're trying to say</label>
            <input type="text" id="phonetic-input" class="phonetic-input" v-model="input" @keyup="updateOutput()" placeholder="Type in what you're trying to say" aria-labelledby="phonetic-input--label" autofocus>
    </section>
</template>

<script type="text/javascript">
import PhoneticAlphabet from '@/alphabet.json';

export default {
  name: 'Input',
  data() {
    return {
      input: '',
      phoneticOne: '',
      phoneticTwo: '',
    };
  },
  mounted() {
    this.$root.$emit('phoneticUpdate', this.input);
    this.updatePhonetics();

    setInterval(() => {
      this.updatePhonetics();
    }, 2000);

    window.onload = (() => {
      document.getElementById('phonetic-input').focus();
    });
  },
  methods: {
    updateOutput() {
      this.$root.$emit('phoneticUpdate', this.input);
    },
    updatePhonetics() {
      this.phoneticOne = PhoneticAlphabet[_.random(0, 24)];
      this.phoneticTwo = PhoneticAlphabet[_.random(0, 24)];
    },
  },
};
</script>
