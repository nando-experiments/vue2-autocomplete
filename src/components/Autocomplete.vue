<template>
  <div class="autocomplete__group" v-bind:class="{'open':openSuggestion}">
    <input class="form-control input-lg" type="text" placeholder="Type a keyword of a city" :value="value" @input="updateValue($event.target.value)" @keydown.enter="enter" @keydown.down="down" @keydown.up="up">
    <ul class="autocomplete__dropdown dropdown-menu">
      <li v-for="(suggestion, index) in matches" class="autocomplete__dropdown-item" v-bind:class="{'active': isActive(index)}" @click="suggestionClick(index)" v-bind:key="index">
        <a href="#"><strong>{{ suggestion.city }}</strong> - <small>{{ suggestion.state }}</small></a>
      </li>
    </ul>
  </div>
</template>

<style scoped>
.autocomplete__group {
  position: relative;
}
.autocomplete__dropdown {
  border-radius: 0;
  padding: 0;
  width: 100%;
}
.autocomplete__dropdown-item a {
  padding: 15px;
}
</style>

<script>
  export default {
    data () {
      return {
        open: false,
        current: 0
      }
    },
    props: {
      value: {
        type: String,
        required: true
      },
      suggestions: {
        type: Array,
        required: true
      }
    },
    computed: {
      matches () {
        return this.suggestions.filter(obj => obj.city.indexOf(this.value) >= 0)
      },
      openSuggestion () {
        return this.selection !== '' &&
              this.matches.length !== 0 &&
              this.open === true
      }
    },
    methods: {
      // Triggered the input event to cascade the updates to
      // parent component
      updateValue (value) {
        if (this.open === false) {
          this.open = true
          this.current = 0
        }
        this.$emit('input', value)
      },

      // When enter key pressed on the input
      enter () {
        this.$emit('input', this.matches[this.current].city)
        this.open = false
      },

      // When up arrow pressed while suggestions are open
      up () {
        if (this.current > 0) {
          this.current--
        }
      },

      // When down arrow pressed while suggestions are open
      down () {
        if (this.current < this.matches.length - 1) {
          this.current++
        }
      },

      // For highlighting element
      isActive (index) {
        return index === this.current
      },

      // When one of the suggestion is clicked
      suggestionClick (index) {
        this.$emit('input', this.matches[index].city)
        this.open = false
      }
    }
  }
</script>
