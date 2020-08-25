<template>
  <div class="dropdown">
    <input
      type="text"
      class="dropdown__input"
      placeholder="Search"
      ref="dropdowninput"
      v-model.trim="inputValue"
      v-if="Object.keys(selectedItem).length === 0"
      v-bind:class="{ active: inputValue !== '' && itemList.length !== 0}"
    >
    <div
      v-else
      @click="resetItem"
      class="dropdown__selected"
    >
      {{ selectedItem.name }}
    </div>

    <div
      v-show="inputValue && apiLoaded"
      class="dropdown__list"
    >
      <div
        v-for="item in itemList"
        v-show="findItem(item)"
        @click="selectItem(item)"
        :key="item.name"
        class="dropdown__item"
      >
        {{ item.name }}
      </div>
    </div>
  </div>
</template>


<script>
import axios from 'axios';

export default {
  name: 'Dropdown',
  data() {
    return {
      itemList: [],
      apiLoaded: false,
      apiError: false,
      apiUrl: 'https://restcountries.eu/rest/v2/all?fields=name;flag',
      inputValue: '',
      selectedItem: {},
    }
  },
  mounted() {
    this.getData()
  },
  methods: {
    getData() {
      axios.get(this.apiUrl)
        .then(response => {
          this.itemList = response.data;
          this.apiLoaded = true;
        })
        .catch(error => {
          this.apiError = true;
          console.error(error.message);
        })
    },
    findItem(item) {
      let name = item.name.toLowerCase();
      let input = this.inputValue.toLowerCase();
      return name.includes(input);
    },
    selectItem(item) {
      this.selectedItem = item;
      this.inputValue = '';
      this.$emit('on-item-selected', item);
    },
    resetItem () {
      this.selectedItem = {}
      this.$nextTick( () => this.$refs.dropdowninput.focus() )
      this.$emit('on-item-reset')
    },
  }
}
</script>

<style scoped lang="scss">
  .dropdown {
    margin: 20px auto 0;
    width: 30%;

    &__input,
    &__selected {
      width: 100%;
      padding: 15px;

      font-size: 20px;

      border: 1px solid rgb(225, 231, 237);
      border-radius: 30px;
    }

    &__input {
      box-shadow: 0 1px 8px rgba(61, 78, 97, 0.1);

      &:hover {
        box-shadow: 0 3px 8px rgba(61, 78, 97, 0.2);
      }

      &:focus {
        background: linear-gradient(180deg, #fff 0%, #f6f6f7 100%);
        outline: none;
      }
    }

    &__selected {
      font-weight: bold;
      cursor: pointer;
    }

    &__list {
      width: 100%;
      border: 1px solid rgb(225, 231, 237);
      border-radius: 0 0 30px 30px;
      border-top: none;
    }

    &__item {
      padding: 15px;
      font-size: 20px;
      cursor: pointer;
    }
  }

  .active {
    border-radius: 30px 30px 0 0;
  }

  @media screen and (max-width: 1200px) {
    .dropdown {
      width: 45%;
    }
  }

  @media screen and (max-width: 750px) {
    .dropdown {
      width: 60%;
    }
  }
</style>
