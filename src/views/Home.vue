<template>
	<div class="ion-page">
		<ion-header>
			<ion-toolbar>
				<ion-title> VueIonic</ion-title>
			</ion-toolbar>
		</ion-header>
		<ion-content class="ion-padding">
			<zip-search @get-zip="getZipInfo"/>
		</ion-content>

	</div>
</template>

<script>

  import ZipSearch from '../components/ZipSearch'

  export default {
    name: 'home',
    components: {
      ZipSearch
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
      }
    }
  }
</script>
