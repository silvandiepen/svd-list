<template>
  <row center>
    <column medium="two-third">
      <section class="list basic">
        <ul class="list__list" v-if="list.length > 0">
          <li  class="list__item" v-for="item in list" :key="item.id">
            {{item.text}}
          </li>
        </ul>

      </section>
      <section class="add basic">
        <form>

          <input type="text" ref="list_item" @keyup.enter.native="addItem()" />
          <button @click.prevent="addItem()">Add</button>
        </form>
        <div class="error" ref="error" v-if="error">
          {{error}}
        </div>

      </section>
      <section class="settings basic">
      </section>
        <section class="disclaimer basic">
        <p>
          Disclaimer: This is <strong>not</strong> safe en completely public, sharing private information is on your own risk.
        </p>
      </section>
    </column>
  </row>
</template>

<script>
  export default{
    data(){
      return{
        list: [],
        error: ''
      }
    },
    methods: {
      randomId() {
        let value = Math.round(Math.random() * Date.now());
        return value;
      },
      addItem () {
        let _this = this;
        let value = _this.$refs.list_item.value;
        if(!value.length){
          _this.showError(1);
        } else {
          let newItem = { id: _this.randomId(), text: value }
          _this.list.push(newItem);
          _this.$refs.list_item.value = '';
        }
      },
      showError(errorID){
        let _this = this;
        let errorMessage = '';
        switch(errorID) {
            case 1:
                errorMessage = 'Your input is empty, please fill in a message.';
                break;
            case 2:
                errorMessage = '';
                break;
            default:
                cerrorMessage = '';
        }
        _this.error = errorMessage;
        setTimeout(function(){
          _this.$refs.error.classList.add('hide');
          setTimeout(function(){
            _this.$refs.error.classList.remove('hide');
            setTimeout(function(){
              _this.error = '';
            },0);
          },500);
        },1000);
      }
    }
  }
</script>


<style lang="scss">
@import '~svd-style/ext';

.list{
  &__list{
  }
  &__item{ padding: 1rem;
    border: 1px solid color(Offwhite);
    animation: popIn 1s forwards;
    & + .list__item{
      margin-top: 1rem;
    }
  }
}
@keyframes popIn{
  0%{ transform: scale(1.5); background-color: color(Blue); opacity: 0; }
  50%{ transform: scale(1); background-color: color(Blue,.5); opacity: 1;  }
  100%{ transform: scale(1); background-color: color(White); opacity: 1;  }
}

.error{
  background-color: color(Red,.2);
  border: 1px solid color(Red,.5);
  padding: 1em; border-radius: 3px;
  font-size: 12px;
  display: inline-block;
  opacity: 1;
  transition: opacity .1s;
  position: absolute;
  &.hide{
    opacity: 0;
  }
}


</style>
