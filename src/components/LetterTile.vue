<template>
    <div class="column is-mobile is-3-mobile is-2-tablet is-1-desktop">
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
