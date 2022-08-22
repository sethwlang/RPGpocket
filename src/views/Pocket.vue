<template>
  <main>
    <label for="pocket-type">Choose a Pocket</label>
    <select name="pocket-type" @change="getGeneralStore($event)">
        <option value="0" >Select Pocket</option>
        <option value="wwn" >Worlds With Out Number</option>
        <option value="dnd" >Dungeons and Dragons</option>
        <option value="deadlands" >Deadlands</option>
    </select>
    <div class="store"></div>
    <div class="pocket"></div>
  </main>
</template>
<script>
export default {
  data() {
    return {
      storeInventory:0,
    }
  },
  mounted() {
    
  },
  methods:{
        getGeneralStore(event){
            console.log(event.target.value);
            if(event.target.value){
            fetch('./test/'+event.target.value+'.json')
                .then((response) => response.json())
                .then((json) => this.storeInventory = json);
            }
        }

  },
}
</script>
