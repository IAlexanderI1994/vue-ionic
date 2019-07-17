<template>
	<ion-button
			color="light"
			expand="block"
			v-if="info"
			@click="$emit('clear-info')"
	> Очистить
	</ion-button>
</template>

<script>
  export default {
    name: 'ClearInfo',
    props: ['info']
  }
</script>

<style scoped>

</style>