<template> 
    <div class="wrapper-column">
        <h3 class="divider gradient">{{ list }}</h3>
        <div
          class="drop-zone"
          @drop="drop($event, list)"
          @dragenter.prevent
          @dragover.prevent
        >
          <div
            :class="list==='Done' ? 'drag-el deleted' : 'drag-el'"
            v-for="item in getList(list)"
            :key="item.id"
            draggable="true"
            @dragstart="drag($event, item)"   
            >
            {{ item.title }}
          </div>    
        </div>
    </div>
  </template>
  
  <script>
  
  import { ref } from '@vue/runtime-core'
  import data from '@/assets/data.json'
  

  export default {
    components: {
    },
    props: {
        list: {
        type: String,
        default: '',
        required: true
      },
    },  
    setup() {
      const items= ref(data)
      const getList = (list) => {
        return items.value.filter((item) => item.list === list)
      }
      
      const drag = (event, item) => {
        event.dataTransfer.dropEffect = 'move'
        event.dataTransfer.effectAllowed = 'move'
        event.dataTransfer.setData('itemID', item.id)
      }
      const drop = (event, list) => {
        const itemID = event.dataTransfer.getData('itemID')
        const item = items.value.find((item) => item.id == itemID)
        item.list = list
      }
  
      return {
        getList,
        drag,
        drop
      }
      
    },
  
  }
  </script>
  
  <!-- Add "scoped" attribute to limit CSS to this component only -->
  <style scoped lang="scss">
  
  h3 {
    font-weight: bold;
  }

  .divider {
    display: flex;

    &:before,
    &:after {
      content: "";
      flex: 1;
    }
  }

  .gradient {
    align-items: stretch;
    margin: 1em 0;
    height: 2em;
    line-height: 2em;
    color: white;
    background: #42b883;
    
    &:before {
      background: linear-gradient(to right, white, #42b883);
    }
    
    &:after {
      background: linear-gradient(to left, white, #42b883);
    }
  }

  .drop-zone {
    background-color: #35495e;
    margin: 20px auto;
    padding: 20px;
    min-height: 10px;
  }
  .drop-zone .drag-el {
    background-color: #f0f8ff;
    color: #35495e;
    margin-bottom: 10px;
    padding: 5px;
  }
  .drop-zone .deleted {
    text-decoration: line-through;
  }
  </style>
  