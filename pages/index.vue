<template>
<div class="main-container">
  <header>Title</header>
  <div class="prefecture">
    <div class="prefecture__title">
      都道府県
    </div>
    <div class="prefecture__body">
      <div class='prefecture__element' v-for="p in prefectures">
        <label :for=p.prefCode>
          <input type="checkbox" :id=p.prefCode :name=p.prefCode :value=p.prefCode />{{ p.prefName }}
        </label>
      </div>
    </div>
  </div>
  <div class="chart">
    <highcharts class="hc" :options="chartOptions" ref="chart"></highcharts>
  </div>
</div>
</template>
<style lang="sass">
header
  background-color: #ddd
  font-size: 20px
  line-hight: 30px
  padding: 10px

.main-container
  width: 540px
  margin: auto

.prefecture
  &__title
    margin-top: 20px
    padding-left: 10px
    font-size: 10px

  &__element
    display: inline-block

header
  text-align: center


</style>
<script>
export default {
  data() {
    return {
      prefectures: [],
      chartOptions: {
        series: [
          {
            data: [1, 2, 3]
          }
        ]
      }
    }
  },
  mounted() {
    this.$axios.get('https://opendata.resas-portal.go.jp/api/v1/prefectures', {
      headers: {
        'X-API-KEY': '9hJ9SReXpMJvEYdyNC2WyK6jfHRwvYaURpl2LoPy',
      }
    }).then(response => {
      this.prefectures = response.data.result
    }
    )
  },
}
</script>
