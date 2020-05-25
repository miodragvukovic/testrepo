<template>
    <header>
      <div class="container">
        <div class="flex flex-end">
          <select @change="onChange($event)" name="select" id="main-select">
            <option v-for="(each, index) in listData.contract_length_options" :key="`list-item-${index}`"
            :value="each"
            :selected="each == listData.preselected_contract_length"
            >{{each}}</option>
          </select>
        </div>
      </div>
    </header>
</template>

<script>
import EventBus from '@/EventBus';

export default {
  name: 'Dropdown',
  props: ['listData'],
  data() {
    return {
    }
  },
  methods: {
    onChange(event) {
      EventBus.$emit('selected', event.target.value);
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
