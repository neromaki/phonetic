<template>
      <main id="app">
        <div class="phonetic-io">
            <phonetic-input></phonetic-input>
            <phonetic-output></phonetic-output>
        </div>
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

<style type="text/css">
    @import '../node_modules/normalize.css/normalize.css';
</style>

<style lang="scss">
@import '../node_modules/avalanche-css/avalanche.min.css';
@import 'assets/scss/app.scss';
</style>
