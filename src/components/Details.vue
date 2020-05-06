<template>
    <div>
        {{details}}
    </div>
</template>

<script>

import {EventBus} from '../main';
export default {
    data(){
        return{
            details: [],
        }
    },
    mounted() {
      EventBus.$on('details-movie', data =>{
          this.details = data
      });
  }   
}
</script>

<style lang="scss">

</style>