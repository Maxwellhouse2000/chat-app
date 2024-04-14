<template>
	<div class="wrapper">
		<div class="chat__user">
			<ChatTop name="Александр" img="alex" />
			<ChatBody
			sender="1"
			:msgs="msgs"
			@openModal="openModal"
			@closeModal="closeModal"
			@deleteMsg="deleteMsg"
			@msgIndexToDelete="msgIndexToDelete = $event"
/>

			<ChatBottom sender="1" @msg="sendMsg" @addMsg="addMsg" />
			<Modal
				:showModal="showModal"
				@closeModal="closeModal"
				:deleteMsg="deleteMsg"
			/>
		</div>
		<div class="chat__user">
			<ChatTop name="Евгений" img="jenya" />
			<ChatBody
			sender="2"
			:msgs="msgs"
			@openModal="openModal"
			@closeModal="closeModal"
			@deleteMsg="deleteMsg"
			@msgIndexToDelete="msgIndexToDelete = $event"
/>
			<ChatBottom sender="2" @msg="sendMsg" @addMsg="addMsg" />
			<Modal
			:showModal="showModal"
			@closeModal="closeModal"
			@deleteMsg="deleteMsg"
			:msgIndex="msgIndexToDelete"
/>
		</div>
	</div>
</template>

<script>
import ChatTop from './components/ChatTop.vue'
import ChatBody from './components/ChatBody.vue'
import ChatBottom from './components/ChatBottom.vue'
import Modal from '@/components/Modal.vue'
export default {
	data() {
  return {
    msgs: [],
    window: false,
    showModal: false,
    msgIndexToDelete: null, /* Изначальное значенние перменной null, но когда приходит index сообщения которое нужно удалить, этой переменной присваевается значения того сообщения которое нужно удалить */
  }
},
	methods: {
		sendMsg(msg) {
			this.msgs.push(msg)
		},
		addMsg(msg) {
			this.msgs.push(msg)
			this.window = false
		},
		getMsg() {
			let localData = localStorage.msgs
			if (localData) {
				this.msgs = JSON.parse(localData)
			}
		},
		openModal(status) {
			this.showModal = status
		},
		closeModal(status) {
			this.showModal = status
		},
deleteMsg() {
  if (this.msgIndexToDelete !== null) {
    this.msgs.splice(this.msgIndexToDelete, 1);  /* Просиходит удаление, по тому индексу который присваевается переменной */
    this.showModal = false;
    this.msgIndexToDelete = null;
  }
}

	},
	created() {
		this.getMsg()
	},
	watch: {
		msgs: {
			handler() {
				localStorage.msgs = JSON.stringify(this.msgs)
			},
			deep: true,
		},
	},
	components: {
		ChatTop,
		ChatBody,
		ChatBottom,
		Modal,
	},
}
</script>

<style>
* {
	padding: 0;
	margin: 0;
	box-sizing: border-box;
	font-family: 'Roboto';
}
li {
	list-style: none;
}
a {
	text-decoration: none;
}
input {
	outline: none;
	border: none;
}
body {
	height: 120vh;
	display: flex;
	align-items: center;
	justify-content: center;
	background: rgb(152, 192, 255);
}
.wrapper {
	display: flex;
	gap: 20px;
}
.chat__user {
	display: flex;
	flex-direction: column;
	height: 800px;
	width: 400px;
	background-image: url('@/assets/images/bg.png');
}
</style>
