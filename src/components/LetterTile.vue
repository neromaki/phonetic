<template>
    <div class="grid__cell">
        <div class="phonetic-tile">
          <h3>{{ letter.character }}</h3>
          <h4>{{ letter.phonetic }}</h4>
        </div>
    </div>
</template>

<script type="text/javascript">
export default {
  name: 'LetterTile',
  props: ['letter'],
};
</script>
