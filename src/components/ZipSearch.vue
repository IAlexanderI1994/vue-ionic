<template>
	<ion-grid>
		<form @submit.prevent="onSubmit">
			<ion-col>
				<ion-item>
					<ion-label>Zipcode</ion-label>
					<ion-input
							:value="zip"
							@input="zip = $event.target.value"
							placeholder="Введите почтовый индекс"
							name="zip"/>
				</ion-item>
			</ion-col>
			<ion-col>
				<ion-button type="submit" color="primary" expand="block"> Найти</ion-button>
			</ion-col>
		</form>
	</ion-grid>
</template>

<script>
  /* eslint-disable */
  export default {
    name: 'ZipSearch',
    data () {
      return {
        zip: ''
      }
    },
    methods: {
      onSubmit () {
        // валидируем
        const isCodeValid = /^\d{6}$/.test(this.zip)
        // если зипкод некорректный, выводим сообщение
        if (!isCodeValid) return this.showAlert()

        this.$emit('get-zip', this.zip)
        this.zip = ''

      },
      showAlert () {
        return this.$ionic.alertController
                   .create({
                     header: 'Введите почтовый индекс',
                     message: 'Пожалуйста, введите корректный почтовый индекс',
                     buttons: ['OK']
                   })
                   .then(a => a.present())
      }
    }
  }
</script>
