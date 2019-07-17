<template>
	<ion-card v-if="info">
		<ion-card-header>
			<ion-card-title><strong> Почтовый индекс: </strong>{{ info['post code']}}</ion-card-title>
		</ion-card-header>
		<ion-card-content>
			<ion-list>
				<ion-item>
					<ion-label>
						<strong> Город: </strong>
						{{ info['places'][0]['state']}}
					</ion-label>
				</ion-item>
				<ion-item>
					<ion-label>
						<strong> Широта: </strong>
						{{ info['places'][0]['latitude']}}
					</ion-label>
				</ion-item>
				<ion-item>
					<ion-label>
						<strong> Долгота: </strong>
						{{ info['places'][0]['longitude']}}
					</ion-label>
				</ion-item>
			</ion-list>
		</ion-card-content>
	</ion-card>
</template>

<script>
  export default {
    name: 'ZipInfo',
    props: ['info']
  }
</script>

<style scoped>

</style>