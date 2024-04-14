<template>
	<div class="chat__bottom">
		<input
			type="text"
			placeholder="Написать сообщение..."
			v-model="msgController"
		/>
		<button v-show="msgController.length" @click="sendMsg">
			<img src="@/assets/images/Message.svg" alt="" />
		</button>
		<button v-show="!msgController.length" @click="window = true">
			<img src="@/assets/images/Camera.svg" alt="" />
		</button>
		<div class="window" v-if="window" @click="window = false">
			<div class="window__body" @click.stop>
				<h3>Отправить картинку</h3>
				<label for="">
					<span>URL</span>
					<input type="text" placeholder="URL" v-model="msgController" />
				</label>
				<label for="">
					<span>Комментарий</span>
					<input
						type="text"
						placeholder="Комментарий"
						
					/>
				</label>
				<div class="window__body-btns">
					<button class="window__body-btn back" @click="window = false">
						Отмена
					</button>
					<button class="window__body-btn send" @click="addMsg">Отправить</button>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
export default {
	data() {
		return {
			msgController: '',
			
			window: false,
		}
	},
	props: ['sender'],

	methods: {
		sendMsg() {
			const hour = new Date().getHours()
			const min = new Date().getMinutes()
			const time = `${hour < 10 ? '0' + hour : hour}:${
				min < 10 ? '0' + min : min
			} `
			if (this.msgController.length) {
				const message = {
					body: this.msgController.trim(),
					sendId: this.sender,
					time: time,
				}
				if (this.msgController.trim() != '') {
					this.$emit('msg', message)
					this.msgController = ''
				}
			}
		},
		addMsg() {
			if (this.msgController ) {
				const msg = {
					msg: this.msgController,
					body: this.msgController,
					date: new Date().toLocaleDateString()
				}
				
				this.$emit('addMsg',msg)
			}
		},
		sendImg () {
			this.$emit('')
		}
		
	},
}
</script>

<style>
.window__body-btns {
	display: flex;
	justify-content: end;
	margin-top: 20px;
}
.window__body-btn {
	font-size: 14px;
	font-weight: 500;
	line-height: 20px;
	letter-spacing: 0.1px;
	text-transform: uppercase;
}
.back {
	color: rgb(207, 27, 27);
}
.send {
	color: rgb(103, 80, 164);
}
.window__body {
	width: 100%;
	max-width: 312px;
	padding: 24px;
	border-radius: 24px;
	background: #fff;
}
.window__body label {
	display: flex;
	flex-direction: column;
	border-radius: 4px 4px 0px 0px;
	background: rgb(226, 237, 255);
	margin-top: 16px;
	padding: 16px;
	border-bottom: 1px solid #323232;
}
.window__body input {
	background: transparent;
	padding: 0 !important;
}
.window__body label span {
	color: rgb(0, 0, 0);
	font-size: 12px;
	font-weight: 400;
	line-height: 16px;
}
.window {
	width: 100%;
	height: 100vh;
	background: rgb(0, 0, 0, 0.35);
	position: fixed;
	top: 0;
	left: 0;
	display: flex;
	justify-items: center;
	align-items: center;
}
.chat__bottom {
	display: flex;
	align-items: center;
	background: #323232;
	width: 100%;
	border-radius: 0 0 10px;
}
.chat__bottom input {
	color: #fff;
	width: 100%;
	font-size: 14px;
	resize: none;
	background: transparent;
	padding: 20px;
	color: rgb(73, 69, 79);
	font-size: 16px;
	font-weight: 400;
	line-height: 24px;
}
.chat__bottom input::placeholder {
	color: #fff;
}
.chat__bottom button {
	background: transparent;
	outline: none;
	border: none;
	padding: 0 20px;
	transition: 5s;
}
.chat__bottom button:active {
	transform: scale(0.95);
}
</style>
