<template>
    <section class="phnetic-alphabet">
        <div class="container is-fluid">
            <h2>Alphabet</h2>
            <div class="columns is-multiline">
                <letter-tile v-for="letter in alphabet" v-if="letter.type === 'letter'" :key="alphabet.character" :letter="letter"></letter-tile>
            </div>
        </div>
    </section>
</template>


<script type="text/javascript">
import PhoneticAlphabet from '@/alphabet.json';
import LetterTile from '@/components/LetterTile';

export default {
  name: 'alphabet',
  components: { LetterTile },
  data() {
    return {
      alphabet: PhoneticAlphabet,
    };
  },
};
</script>
