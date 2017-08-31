<template>
    <section class="phonetic-input">
            <p>for when you can't remember <span class="phonetic-input--wrap"><span>{{ phonemeOne.phonetic }}</span> from <span>{{ phonemeTwo.phonetic }}</span></span></p>
            <label id="phonetic-input--label" for="phonetic-input">Type in what you're trying to say</label>
            <input type="text" id="phonetic-input" class="phonetic-input" v-model="input" ref="phoneticInput" @keyup="updateOutput()" placeholder="Type in what you're trying to say" aria-labelledby="phonetic-input--label" autofocus>
    </section>
</template>

<script type="text/javascript">
import PhoneticAlphabet from '@/alphabet.json';

const random = require('lodash/random');
const includes = require('lodash/includes');

export default {
  name: 'Input',
  data() {
    return {
      input: '',
      phonemeOne: '',
      phonemeTwo: '',
      phonemeOneList: [],
      phonemeTwoList: [],
    };
  },
  mounted() {
    this.$root.$emit('phoneticUpdate', this.input);
    this.initPhonemeLists();
    this.updatePhonetics();

    setInterval(() => {
      this.updatePhonemeLists();
      this.updatePhonetics();
    }, 2000);

    this.$refs.phoneticInput.focus();
  },
  methods: {
    updateOutput() {
      this.$root.$emit('phoneticUpdate', this.input);
    },
    addPhonemeToLists() {
      let phonemeOne = this.getRandomPhoneme();
      if (this.phonemeOneList.length > 0) {
        while (includes(this.phonemeOneList, phonemeOne)) {
          phonemeOne = this.getRandomPhoneme();
        }
      }
      this.phonemeOneList.push(phonemeOne);

      let phonemeTwo = this.getRandomPhoneme();
      while (phonemeOne === phonemeTwo) {
        phonemeTwo = this.getRandomPhoneme();
      }
      if (this.phonemeTwoList.length > 0) {
        while (includes(this.phonemeTwoList, phonemeTwo)) {
          phonemeTwo = this.getRandomPhoneme();
        }
      }
      this.phonemeTwoList.push(phonemeTwo);
    },
    initPhonemeLists() {
      let x = 0;
      for (x = 0; x < 3; x++) {
        this.addPhonemeToLists();
      }
    },
    updatePhonemeLists() {
    //
    //   function animate() {
    //     phonemeListOneElement.top
    //   }

    //   const animateList = new Promise((resolve, reject) => {
    //     setInterval(animate, 10);
    //   });
    //   this.addPhonemeToLists();
    //   this.phonemeOneList.shift();
    //   this.phonemeTwoList.shift();
    },
    updatePhonetics() {
      this.phonemeOne = PhoneticAlphabet[random(0, 24)];
      this.phonemeTwo = PhoneticAlphabet[random(0, 24)];
      while (this.phonemeOne === this.phonemeTwo) {
        this.phonemeTwo = PhoneticAlphabet[random(0, 24)];
      }
    },
    getRandomPhoneme() {
      return PhoneticAlphabet[random(0, 24)];
    },
  },
};
</script>
