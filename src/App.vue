<template>
  <div class="container">
    <div class="card">
      <h1>Vue Composition Api</h1>
      <hr>
      <small>data, methods, computed, watch </small>
      <p>Название: <strong>{{ name }}</strong></p>
      <p>Версия: <strong>{{ version }} ({{doubleVersion}})</strong></p>

      <div class="form-control">
        <input type="text" ref="textInput">
        <input type="text" v-model="firstName">
      </div>

      <button class="btn" @click="change">Изменить</button>
    </div>
  </div>
</template>

<script>
import {
  ref,
  reactive,
  toRefs,
  isRef,
  isReactive,
  computed,
  watch} from 'vue'

export default {
  setup() {
    // ключевое слово this тут не доступно! на момент вызова метода оно еще не равняется инстенсу компонента

    const name = ref('VueJs')
    const version = ref(3)
    const textInput = ref(null)
    const firstName = ref('имя')

    const framework = reactive ({  // reactive - только для объектов!
      name: 'VueJS',
      version: 3
    })

    const doubleVersion = computed(() => {
      return version.value * 2
    })

    watch([doubleVersion, name, firstName], (newValues, oldValues) => {
      console.log('new version', newValues[0])
      console.log('old version', oldValues[0])
      console.log('new name', newValues[1])
      console.log('old name', oldValues[1])
      console.log('new firstName', newValues[2])
      console.log('old firstName', oldValues[2])

    })

    // watch(doubleVersion, (newValue, oldValue) => {
    //   console.log('new', newValue)
    //   console.log('old', oldValue)
    // })

    function changeInfo() {
      name.value = 'Vue JS!'
      version.value = 42
      console.log(textInput.value) // сам инпут
      console.log(textInput.value.value) // значение инпута
    }

    return {
      // ...toRefs(framework),
      name: name,
      version: version,
      change: changeInfo,
      doubleVersion,
      textInput,
      firstName
    }
  }
  // data() {
  //   return {
  //     name: 'VueJS',
  //     version: 3
  //   }
  // },
  // methods: {
  //   changeInfo() {
  //     this.name = 'Vue JS!'
  //     this.version = 4
  //   }
  // }
}
</script>
