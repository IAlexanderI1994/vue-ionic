<template>
	<div class="ion-page">
		<ion-header>
			<ion-toolbar>
				<ion-title> VueIonic</ion-title>
			</ion-toolbar>
		</ion-header>
		<ion-content class="ion-padding">
			<zip-search @get-zip="getZipInfo"/>
			<zip-info :info="info"/>
			<clear-info :info="info" @clear-info="clearInfo"></clear-info>
		</ion-content>

	</div>
</template>

<script>

  import ZipSearch from '../components/ZipSearch'
  import ZipInfo from '../components/ZipInfo'
  import ClearInfo from '../components/ClearInfo'

  export default {
    name: 'home',
    components: {
      ZipSearch,
      ZipInfo,
      ClearInfo
    },
    data () {
      return {
        info: null
      }
    },
    methods: {
      async getZipInfo (zip) {

        const response = await fetch(`http://api.zippopotam.us/RU/${zip}`)
        if (response.status === 404) return this.showAlert()

        this.info = await response.json()

      },
      showAlert () {
        return this.$ionic.alertController
                   .create({
                     header: 'Почтовый индекс не найден',
                     message: 'Пожалуйста, введите корректный почтовый индекс',
                     buttons: ['OK']
                   })
                   .then(a => a.present())
      },
      clearInfo() {
        this.info = null
      }
    }
  }
</script>
