<template>
  <div class="card">
    <div class="cards">
      <div class="card-header">Добавить опрос</div>
      <div class="card-type-one" v-for="(card,index) in cards" v-bind:key="card.id" :style="card.back_color">
        <div class="card-one">
          <div :style="card.text_color">Условие {{index+1}}</div>
          <div>
            <select class="input_question" v-model="card.selected" @change="getValue(card.id,card.selected)">
              <option v-for="option in options" v-bind:key="option.id" :value="option.id">
                {{ option.name }}
              </option>
            </select>
          </div>
        </div>
        <div v-show="card.selected==1" class="card-two" v-for="(item,index) in card.range" v-bind:key="item.id">
          <div style="font-size:15px;">Диапазон {{index+1}}</div>
          <div style="margin-left:195px;">
            от <input class="input_question" v-model="item.range_start" style="width:70px;max-height:32px;" /> &nbsp;&nbsp; 
            до <input class="input_question" v-model="item.range_end" style="width:70px;max-height:32px;" />
          </div>
        </div>
        <div v-show="card.selected==2" class="card-two" v-for="(item,index) in card.range" v-bind:key="item.id">
          <div style="font-size:15px;">Тип {{index+1}}</div>
          <div style="margin-left:235px;">
            <select class="input_question" v-model="item.value" style="width:300px;">
              <option v-for="option in types" v-bind:key="option.id" :value="option.id">
                {{ option.name }}
              </option>
            </select>
          </div>
        </div>
        <div v-show="card.selected==3" class="card-two" v-for="(item,index) in card.range" v-bind:key="item.id">
          <div style="font-size:15px;">Статус {{index+1}}</div>
          <div style="margin-left:213px;">
            <select class="input_question" v-model="item.value" style="width:300px;">
              <option v-for="option in states" v-bind:key="option.id" :value="option.id">
                {{ option.name }}
              </option>
            </select>
          </div>
        </div>
        <div style="margin-left:310px;padding-bottom:30px;padding-top:15px;" v-show="card.selected==1">
          <div style="display:flex;align-items:center;">
            <button class="btn success" @click="addItem(card.id)">Добавить диапазон</button>
            <button class="btn danger" style="margin-left:135px;" @click="deleteItem(card.id)">Удалить условие</button>
          </div>
        </div>
        <div style="margin-left:310px;padding-bottom:30px;padding-top:15px;" v-show="card.selected==2">
          <div style="display:flex;align-items:center;">
            <button class="btn success" @click="addItem(card.id)">Добавить тип</button>
            <button class="btn danger" style="margin-left:180px;" @click="deleteItem(card.id)">Удалить условие</button>
          </div>
        </div>
        <div style="margin-left:310px;padding-bottom:30px;padding-top:15px;" v-show="card.selected==3">
          <div style="display:flex;align-items:center;">
            <button class="btn success" @click="addItem(card.id)">Добавить статус</button>
            <button class="btn danger" style="margin-left:160px;" @click="deleteItem(card.id)">Удалить условие</button>
          </div>
        </div>
      </div>
      <div style="text-align:center;color:#28AF44;padding:40px 30px;">
        <div class="footer" @click="addCard()">
          <div></div>
          <div>Нажмите, чтобы добавить новое условие выборки.</div>
          <div>Все условия связываются между собой логическим "И".</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'FormTest',
  data () {
    return {
      cards:[
        {id:1,text_color:'color:#A37200;',back_color:'background-color:#FFFCF5;',range:[{id:1,range_start:2,range_end:5}],selected:1},
        {id:2,text_color:'color:#2B50AA;',back_color:'background-color:#F8FAFF;',range:[{id:1,value:1}],selected:2},
        {id:3,text_color:'color:#6DA622;',back_color:'background-color:#FAFFF8;',range:[{id:1,value:1}],selected:3}
      ],
      options:[
        {id:1,name:"Возраст респондента"},
        {id:2,name:"Тип карты лояльности"},
        {id:3,name:"Статус карты лояльности"}
      ],
      types:[
        {id:1,name:"Gold"}
      ],
      states:[
        {id:1,name:"Активна"}
      ]
    }
  },
  methods: {
    getValue(card_id,option_selected) {
      if(option_selected==1) {
        this.cards.filter((k)=>k.id==card_id)[0].text_color='color:#A37200';
        this.cards.filter((k)=>k.id==card_id)[0].back_color='background-color:#FFFCF5;';
        this.cards.filter((k)=>k.id==card_id)[0].range=[{id:this.uuidv4()}];
      }else if(option_selected==2) {
        this.cards.filter((k)=>k.id==card_id)[0].text_color='color:#2B50AA';
        this.cards.filter((k)=>k.id==card_id)[0].back_color='background-color:#F8FAFF;';
        this.cards.filter((k)=>k.id==card_id)[0].range=[{id:this.uuidv4()}];
      }else {
        this.cards.filter((k)=>k.id==card_id)[0].text_color='color:#6DA622';
        this.cards.filter((k)=>k.id==card_id)[0].back_color='background-color:#FAFFF8;';
        this.cards.filter((k)=>k.id==card_id)[0].range=[{id:this.uuidv4()}];
      }
    },
    uuidv4() {
      return 'xxxxxxxx-xxxx-4xxx-yxxx-xxxxxxxxxxxx'.replace(/[xy]/g, function(c) {
        var r = Math.random() * 16 | 0, v = c == 'x' ? r : (r & 0x3 | 0x8);
        return v.toString(16);
      });
    },
    addCard() {
      this.cards.push({id:this.uuidv4(),text_color:'color:black;',back_color:'background-color:#fff;',range:[{id:this.uuidv4()}]})
    },
    deleteItem(id) {
      this.cards=this.cards.filter((k)=>k.id!==id)
    },
    addItem(card_id) {
      this.cards.filter((k)=>k.id===card_id)[0].range.push({id:this.uuidv4()})
      console.log(this.cards)
    }
  }
}
</script>

<style scoped>
  .card {
    display: flex;
    justify-content: center;
    margin-top: 30px;
  }
  .cards {
    width: 800px;
    height: auto;
    background-color: #fff;
    box-shadow: rgba(149, 157, 165, 0.2) 0px 8px 24px;
  }
  .card-header {
    color:#AEAEAE;
    text-align:left;
    padding:15px 40px;
    text-shadow: 0px 0px 1px #AEAEAE;
  }
  .card-one {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    align-items: center;
    padding:15px 40px;
    color:black;
  }
  .card-two {
    display:flex;
    align-items: center;
    padding:15px 40px;
    color:black;
  }
  .input_question {
    font-size: 14px;
    line-height: 28px;
    padding: 8px 2px 8px 5px;
    width: 450px;
    cursor: pointer;
    border: unset;
    border-radius: 4px;
    outline-color: rgb(84 105 212 / 0.5);
    background-color: rgb(255, 255, 255);
    box-shadow: rgba(0, 0, 0, 0) 0px 0px 0px 0px, 
                rgba(0, 0, 0, 0) 0px 0px 0px 0px, 
                rgba(0, 0, 0, 0) 0px 0px 0px 0px, 
                rgba(60, 66, 87, 0.16) 0px 0px 0px 1px, 
                rgba(0, 0, 0, 0) 0px 0px 0px 0px, 
                rgba(0, 0, 0, 0) 0px 0px 0px 0px, 
                rgba(0, 0, 0, 0) 0px 0px 0px 0px;
  }
  .btn {
    border: 1px solid #81A500;
    border: none;
    background-color: white;
    color: #81A500;
    padding: 10px 14px;
    font-size: 15px;
    border-radius:4px;
    box-shadow: 0 0 3px;
    cursor: pointer;
  }
  .success {
    border-color: #81A500;
    color: #81A500;
  }

  .success:hover {
    background-color: #81A500;
    color: white;
    transition:.2s linear;
  }
  .danger {
    border-color: #f44336;
    color: red
  }

  .danger:hover {
    background: #f44336;
    color: white;
    transition:.2s linear;
  }
  .footer {
    border:0.5px solid #E5ECF0;
    padding:30px 20px;
    border-radius:4px;
    cursor: pointer;
  }
  .footer:hover {
    color:#fff;
    background-color: #28AF44;
    transition: .2s linear;
  }
</style>
