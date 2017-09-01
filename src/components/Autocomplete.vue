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
/**
 * Component is described here.
 *
 * @example ./extra.examples.md
 */
export default {
  name: 'Autocomplete',
  data () {
    return {
      /**
      * The color for the button.
      */
      open: false,
      /**
      * The color for the button.
      */
      current: 0
    }
  },
  props: {
    /**
     * Gets called when the user clicks on the button
     *
     * @param {SyntheticEvent} event The react `SyntheticEvent`
     * @param {Number} num Numbers of examples
     */
    value: {
      type: String,
      required: true
    },
    /**
     * Gets called when the user clicks on the button
     *
     * @param {SyntheticEvent} event The react `SyntheticEvent`
     * @param {Number} num Numbers of examples
     */
    suggestions: {
      type: Array,
      required: true
    }
  },
  computed: {
    /**
     * Gets called when the user clicks on the button
     *
     * @param {SyntheticEvent} event The react `SyntheticEvent`
     * @param {Number} num Numbers of examples
     */
    matches () {
      return this.suggestions.filter(obj => obj.city.indexOf(this.value) >= 0)
    },
    /**
     * Gets called when the user clicks on the button
     *
     * @param {SyntheticEvent} event The react `SyntheticEvent`
     * @param {Number} num Numbers of examples
     */
    openSuggestion () {
      return this.selection !== '' &&
            this.matches.length !== 0 &&
            this.open === true
    }
  },
  methods: {
    /**
     * Gets called when the user clicks on the button
     *
     * @param {SyntheticEvent} event The react `SyntheticEvent`
     * @param {Number} num Numbers of examples
     */
    updateValue (value) {
      if (this.open === false) {
        this.open = true
        this.current = 0
      }
      this.$emit('input', value)
    },
    /**
     * Gets called when the user clicks on the button
     *
     * @param {SyntheticEvent} event The react `SyntheticEvent`
     * @param {Number} num Numbers of examples
     */
    enter () {
      this.$emit('input', this.matches[this.current].city)
      this.open = false
    },
    /**
     * Gets called when the user clicks on the button
     *
     * @param {SyntheticEvent} event The react `SyntheticEvent`
     * @param {Number} num Numbers of examples
     */
    up () {
      if (this.current > 0) {
        this.current--
      }
    },
    /**
     * Gets called when the user clicks on the button
     *
     * @param {SyntheticEvent} event The react `SyntheticEvent`
     * @param {Number} num Numbers of examples
     */
    down () {
      if (this.current < this.matches.length - 1) {
        this.current++
      }
    },
    /**
     * Gets called when the user clicks on the button
     *
     * @param {SyntheticEvent} event The react `SyntheticEvent`
     * @param {Number} num Numbers of examples
     */
    isActive (index) {
      return index === this.current
    },
    /**
     * Gets called when the user clicks on the button
     *
     * @param {SyntheticEvent} event The react `SyntheticEvent`
     * @param {Number} num Numbers of examples
     */
    suggestionClick (index) {
      this.$emit('input', this.matches[index].city)
      this.open = false
    }
  }
}
</script>
