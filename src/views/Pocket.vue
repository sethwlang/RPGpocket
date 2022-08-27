<template>
  <main>
    <label for="pocket-type">Choose a Pocket</label>
    <select name="pocket-type" @change="getGeneralStore($event)">
        <option value="0" >Select Pocket</option>
        <option value="wwn" >Worlds With Out Number</option>
        <option value="dnd" >Dungeons and Dragons</option>
        <option value="deadlands" >Deadlands</option>
    </select>
    <div class="store" v-show="storeInventory" style="width:40%">
      <h3>Store</h3>
      <div>Search: <input/></div>
      <table style="border: solid">
        <th>Name</th>
        <th>Description</th>
        <th>Price</th>
        <th>Weight</th>
        <th>Type</th>
        <th>Add</th>
        <tr v-for="item in storeInventory" :key="item.id">
          <td>{{item.name}}</td>
          <td>{{item.description}}</td>
          <td>{{item.price}}</td>
          <td>{{item.weight}}</td>
          <td>{{item.type}}</td>
          <td><button @click.prevent="addToInventory(item)">Add</button></td>
        </tr>
      </table>
    </div>
    <div class="pocket" v-show="myInventory.length >0" style="width:40%">
      <h3>Pocket</h3><span>Total Weight:<span>{{totalWeight}}</span></span>
      <table style="border: solid">
        <th>Name</th>
        <th>Description</th>
        <th>Price</th>
        <th>Weight</th>
        <th>QTY</th>
        <tr v-for="item in myInventory" :key="item.id">
          <td>{{item.name}}</td>
          <td>{{item.description}}</td>
          <td>{{item.price}}</td>
          <td>{{item.weight}}</td>
          <td>{{item.qty}}</td>
        </tr>
      </table>
    </div>
  </main>
</template>
<script>

export default {
  name:"RPGpocket",
  data() {
    return {
      storeInventory:0,
      myInventory:[],
      totalWeight:0,
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
        },
        addToInventory(item){
          item.qty = 1;
          //for lopp to check if item has already been added or not.
            this.myInventory.push(item);
            this.totalWeight += item.weight;

        },
        search(searchValue){

            

        },
    

  },
}
</script>
