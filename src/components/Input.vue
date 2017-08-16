<template>
    <section class="phonetic-input">
            <p>for when you can't remember <span>{{ phoneticOne.phonetic }}</span> from <span>{{ phoneticTwo.phonetic }}</span></p>
            <input type="text" class="phonetic-input" v-model="input" @keyup="updateOutput()" placeholder="Type in what you're trying to say" />
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
