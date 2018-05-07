<template>
  <main>
    <section class="list basic" ref="list" :class="['list','basic',opened ? 'opened': '']">
      <row center>
        <column medium="two-third">
          <ul class="list__list" v-if="list.length > 0">
            <li  class="list__item" v-for="(item, index) in list.items" :key="item.id">
              {{item.text}}
              <span v-on:click="list.splice(index, 1)" class="list__remove"><span></span></span>
            </li>
          </ul>
        </column>
      </row>
    </section>
    <section class="add">
      <row center>
        <column medium="two-third">
          <form>
            
            <input type="text" ref="list_item" @keyup.enter.native="addItem()"
  @focus="opened = true"
  @blur="opened = false" />
            <button @click.prevent="addItem()">Add</button>
          </form>
          <div class="error" ref="error" v-if="error">
            {{error}}
          </div>
        </column>
      </row>
    </section>
    <section class="disclaimer basic bg-black">
      <row center>
        <column medium="two-third">
          <p>
            Disclaimer: This is <strong>not</strong> safe en completely public, sharing private information is on your own risk.
          </p>
        </column>
      </row>
    </section>
  </main>
</template>

<script>
export default {
  data() {
    return {
      opened: false,
      list: {
        title: "My list",
        items: []
      },
      error: ""
    };
  },
  methods: {
    randomId() {
      let value = Math.round(Math.random() * Date.now());
      return value;
    },
    addItem() {
      let _this = this;
      let value = _this.$refs.list_item.value;
      if (!value.length) {
        _this.showError(1);
      } else {
        let newItem = { id: _this.randomId(), text: value };
        _this.list.items.push(newItem);
        _this.$refs.list_item.value = "";
        _this.$refs.list.scrollTop = _this.$refs.list.scrollHeight + 100;
        _this.$refs.list_item.focus();
      }
    },
    showError(errorID) {
      let _this = this;
      let errorMessage = "";
      switch (errorID) {
        case 1:
          errorMessage = "Your input is empty, please fill in a message.";
          break;
        case 2:
          errorMessage = "";
          break;
        default:
          cerrorMessage = "";
      }
      _this.error = errorMessage;
      setTimeout(function() {
        _this.$refs.error.classList.add("hide");
        setTimeout(function() {
          _this.$refs.error.classList.remove("hide");
          setTimeout(function() {
            _this.error = "";
          }, 0);
        }, 500);
      }, 1000);
    }
  }
};
</script>


<style lang="scss">
$default-color-set: "vibrant";
@import "~svd-style/ext";

.add {
  padding: 30px;
  background-color: color(Dark);
  @media #{$small-only} {
    height: 110px;
  }
}
.list {
  max-height: calc(100vh - 110px - 80px);
  overflow: auto;
  @media #{$small-only} {
    height: calc(100vh - 110px - 80px);
  }
  &__list {
  }
  &__item {
    padding: 1rem;
    position: relative;
    border: 1px solid color(Blue, 0.5);
    animation: popIn 0.5s forwards;
    & + .list__item {
      margin-top: 1rem;
    }
  }
  &__remove {
    position: absolute;
    top: 50%;
    right: 1.5rem;
    transform: translate(50%, -50%);
    border: 1px solid red;
    width: 1.5rem;
    height: 1.5rem;
    span {
      color: color(Red);
      font-size: 1rem;
      text-align: center;
      line-height: 1.5rem;
      content: "\2326";
    }
  }
}
@keyframes popIn {
  0% {
    transform: scale(1.5);
    background-color: color(Blue);
    opacity: 0;
  }
  50% {
    transform: scale(1);
    background-color: color(Blue, 0.5);
    opacity: 1;
  }
  100% {
    transform: scale(1);
    background-color: color(White);
    opacity: 1;
  }
}

.error {
  background-color: color(Red, 0.2);
  border: 1px solid color(Red, 0.5);
  padding: 1em;
  border-radius: 3px;
  font-size: 12px;
  display: inline-block;
  opacity: 1;
  transition: opacity 0.1s;
  position: absolute;
  color: white;
  &.hide {
    opacity: 0;
  }
}
</style>
