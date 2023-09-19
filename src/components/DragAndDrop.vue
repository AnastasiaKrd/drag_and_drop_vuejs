<template> 
  <h1>{{ msg }}</h1>  
  <div class="wrapper">
    <DropZone list="To do"/>
    <DropZone list="Done"/>  
  </div>  
</template>

<script>

import DropZone from './DropZone.vue'

export default {
  components: {
    DropZone
  },

  props: {
    msg: {
      type: String,
      default: '',
      required: true
    },
  },  
  setup() {
    
    return {
      
    }
    
  },

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
h1 {
  margin: 40px 0 0;
}

.wrapper {
  display: flex;
  column-gap: 10%;
}

.wrapper .wrapper-column {
  width: 50%;
  padding: 5%;
}

</style>
