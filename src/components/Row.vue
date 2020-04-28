<template>
	<tr>
		<td>{{row.name}}</td>
		<td>{{row.phone}}</td>
		<td>{{row.activity}}</td>
		<td>{{row.city}}</td>
	</tr>
</template>

<script>
	export default {
		name: "Row",
		props: ["row"],
	}
	
</script>

<style scoped>

</style>