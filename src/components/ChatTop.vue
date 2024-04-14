<template>
	<div class="chat__top">
		<img :src="images[img]" alt="" />
		<div class="chat__top-info">
			<h2>{{ name }}</h2>
			<span>Онлайн</span>
		</div>
	</div>
</template>

<script>
export default {
	data() {
		return {
			images: {
				alex: require('@/assets/images/Aleksandr.png'),
				jenya: require('@/assets/images/Evgeniy.png'),
				
			},
		}
	},
	props: ['img', 'name'],
}
</script>

<style>
.chat__top {
	padding: 30px 20px;
	border-radius: 10px 10px 0 0;
	background: rgb(50, 50, 50);
	display: flex;
	align-items: center;
	gap: 10px;
}
.chat__top-info {
	display: flex;
	gap: 2px;
	flex-direction: column;
}

.chat__top h2 {
	color: rgb(255, 255, 255);
	font-size: 18px;
	font-weight: 500;
	line-height: 14px;
}
.chat__top span {
	color: rgb(255, 255, 255);
	font-size: 14px;
	font-weight: 300;
	line-height: 18px;
}
</style>
