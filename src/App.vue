<template>
      <main id="app">
        <phonetic-input></phonetic-input>
        <phonetic-output></phonetic-output>
        <phonetic-alphabet></phonetic-alphabet>
    </main>
</template>

<script>
import PhoneticInput from './components/Input';
import PhoneticOutput from './components/Output';
import PhoneticAlphabet from './components/Alphabet';

export default {
  name: 'app',
  components: {
    PhoneticInput,
    PhoneticOutput,
    PhoneticAlphabet,
  },
};
</script>

<style lang="scss">
@import '../node_modules/bulma/css/bulma.css';
@import 'assets/scss/app.scss';
</style>
