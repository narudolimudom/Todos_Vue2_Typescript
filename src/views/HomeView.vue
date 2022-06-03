<template>
<div>
  <h1>{{mydata}}</h1>
</div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';

export default class App extends Vue{

  mydata : string = 'hello';
}

</script>
