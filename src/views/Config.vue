<template>
  <div class="container">
    <div class="row">
      <h5>Названия колонок</h5>
    </div>
    <div class="row">
      <div class="col s6">
        <p>Тип билета</p>
      </div>
      <div class="col s6">
        <input type="text" name="pe_ticket_type_column" id="pe_ticket_type_column" class="input-field">
      </div>
    </div>
    <div class="row">
      <div class="col s6">
        <p>Цена</p>
      </div>
      <div class="col s6">
        <input type="text" name="pe_price_column" id="pe_price_column" class="input-field">
      </div>
    </div>
    <div class="row">
      <div class="col s6">
        <p>Количество билетов</p>
      </div>
      <div class="col s6">
        <input type="text" name="pe_quantity_column" id="pe_quantity_column" class="input-field">
      </div>
    </div>
     <div class="row">
      <div class="col s6">
        <p>Дата</p>
      </div>
      <div class="col s6">
        <input type="text" name="pe_date_column" id="pe_date_column" class="input-field">
      </div>
    </div>
    <div class="row">
      <h5>Настройки модели</h5>
    </div>
    <div class="row">
      <div class="col s6">
        <p>Целевой год</p>
      </div>
      <div class="col s6">
        <input type="text" name="pe_target_year" id="pe_target_year" class="input-field">
      </div>
    </div>
    <div class="row">
      <div class="col s6">
        <p>Высокий сезон</p>
      </div>
      <div class="col s6">
        <input type="text" name="pe_season_high" id="pe_season_high" class="input-field">
      </div>
    </div>
    <div class="row">
      <div class="col s6">
        <p>Средний сезон</p>
      </div>
      <div class="col s6">
        <input type="text" name="pe_season_weak" id="pe_season_weak" class="input-field">
      </div>
    </div>
    <div class="row">
      <div class="col s6">
        <p>Количество бинов</p>
      </div>
      <div class="col s6">
        <input type="text" name="pe_bins" id="pe_bins" class="input-field">
      </div>
    </div>
    <button @click="updateValues()" class="btn right">Обновить настройки</button>
  </div>
</template>

<script>
export default {
  mounted: function () {
    // get all config
    fetch('/api/price-elasticity/config', {
      method: 'GET'
    }).then(response => {
      return response.json()
    }).then(response => {
      try {
        var d = response.message
        var inputs = document.querySelectorAll('input')
        for (var el in inputs) {
          inputs[el].value = d[inputs[el].id]
        }
      } catch (error) {
        console.log(`Problem with element ${el}`)
      }
    })
  },
  methods: {
    updateValues () {
      var inputs = document.querySelectorAll('input')
      console.log(inputs)
      var data = {}
      for (var el in inputs) {
        data[inputs[el].id] = inputs[el].value
      }
      fetch('/api/price-elasticity/config', {
        method: 'POST',
        mode: 'no-cors', // no-cors, *cors, same-origin
        cache: 'no-cache', // *default, no-cache, reload, force-cache, only-if-cached
        credentials: 'same-origin', // include, *same-origin, omit
        headers: {
          'Content-Type': 'application/json'
          // 'Content-Type': 'application/x-www-form-urlencoded',
        },
        redirect: 'follow', // manual, *follow, error
        referrerPolicy: 'no-referrer',
        body: JSON.stringify(data)
      }).then(response => {
        console.log('Done!')
      })
    }
  }
}
</script>

<style>

</style>
