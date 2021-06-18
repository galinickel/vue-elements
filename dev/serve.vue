<script>
import Vue from 'vue';
// Uncomment import and local "components" registration if library is not registered globally.
import { Button,Input,Loader,Form } from '@/entry.esm';

export default Vue.extend({
  name: 'ServeDev',
  components: {
    Button,Input,Loader,Form ,
  }
});
</script>

<template>
  <div id="app">
    <Button text="gali"/>
    <Input/>
    <Loader/>
    <Form/>
  </div>
</template>
