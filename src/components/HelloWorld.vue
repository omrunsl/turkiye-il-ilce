<template>
<div class="container">
  <div class="row">
    <div class="col-md-4 col-md-ofset-2 form-group">
      <label class="my-1 mr-2" for="inlineFormCustomSelectPref">İl</label>
      <select class="custom-select my-1 mr-sm-2 form-control" v-model="selected" @change="getIlce()" id="inlineFormCustomSelectPref">
        <option v-if="selected == 'Seçiniz'">Seçiniz</option>
        <option 
          v-for="item in iller"  
          v-bind:key="item.il"
        >
          {{item.il}}
        </option>
      </select>
    </div>

    <div class="col-md-4  form-group">
      <label class="my-1 mr-2" for="inlineFormCustomSelectPref">İlçe</label>
      <select class="custom-select my-1 mr-sm-2 form-control" id="inlineFormCustomSelectPref">
        <option v-if="selectedIl == false">Seçiniz</option>
        <option
        v-for="ilce in ilceler"
        v-bind:key="ilce"
        >
          {{ilce}}
        </option>
      </select>
    </div>

    <div class="col-md-4  form-group">
      <label class="my-1 mr-2" for="inlineFormCustomSelectPref">Bölge</label>
      <input type="text" class="my-1 mr-sm-2 form-control" v-model="bolge['0']">
    </div>
    
  </div>
</div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data() {
    return {
      selected:'Seçiniz',
      iller:{},
      ilceler:[],
      selectedIl:false,
      bolge:[]
    }
  },
  created() {
    this.getIl()
  },
  methods:{
    getIl() {
      axios.get('json/il-bolge.json')
      .then(res => this.iller = res.data)
    },
    getIlce() {
      this.selectedIl = true
      this.ilceler = []
      this.bolge = []
      axios.get('json/il-ilce.json')
      .then(res => {
        res.data.forEach(i => {
          if(this.selected == i.il){
            this.ilceler.push(i.ilce)
            this.bolge.push(i.bolge)
          }
        })
      })
    }
  }
}
</script>


