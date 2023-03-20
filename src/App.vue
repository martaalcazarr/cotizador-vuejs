<script setup>
  import {ref, computed} from 'vue'
  import Header from './components/Header.vue'
  import Button from './components/Button.vue'

  const cantidad = ref(2500000)
  const meses = ref(6)
  const MIN = 0
  const MAX = 5000000
  const STEP = 100000
 
const formatearDinero = computed(() => {
  const formatter = new Intl.NumberFormat('en-US', {
    style: 'currency',
    currency: 'CLP'
  })
  return formatter.format(cantidad.value)
})

const handleChangeDecremento = () => {
  const valor = cantidad.value - STEP
  if(valor < MIN){
    alert('Cantidad no válida')
    return
  }
  cantidad.value = valor
}

const handleChangeIncremento = () =>{
  const valor = cantidad.value + STEP
  if(valor > MAX){
    alert('Cantidad no válida')
    return
  }
  cantidad.value = valor
}


  
</script>

<template>
  <div class="my-20 max-w-lg mx-auto bg-white shadow p-10">
    <Header />
    <div class="flex justify-between mt-10">
      <Button
        :operador="'-'"
        @fn="handleChangeDecremento"
      />
      <Button
      :operador="'+'"
      @fn="handleChangeIncremento"
      />

    </div>
    <div class="my-5">
      <input 
        type="range"
        class="w-full bg-gray-200 accent-lime-500 hover:accent-lime-600"
        :min="MIN"
        :max="MAX"
        :step="STEP"
        v-model.number="cantidad"
        
        />
        <p class="text-center my-10 text-5xl font-extrabold text-teal-600">{{ formatearDinero }}</p>
        <h2 class="text-2xl font-extrabold text-gray-500 text-center">
          Elige un <span class="text-teal-600">
            plazo
          </span>
          a pagar
        </h2>
        <select
          class="w-full p-2 mt-5 bg-white border border-gray-300 rounded-lg text-center text-xl font-bold text-gray-500"
          value="meses"
          >
          <option value="6">6 Meses</option>
          <option value="12">12 Meses</option>
          <option value="24">24 Meses</option>
        </select>
    </div>
  </div>
 
</template>


