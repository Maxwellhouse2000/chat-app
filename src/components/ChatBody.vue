<template>
  <div class="chat__body">
    <div class="list">
      <div class="chat__body-item" v-for="(msg, idx) in msgs" :key="idx">
        <div
          class="chat__body-item-content"
          :class="{
            send: msg.sendId == sender,
            get: msg.sendId != sender,
          }"
        >
          <span>{{ msg.time }}</span>
          <div>
            <p @click="openModalToDelete(idx)">{{ msg.body }}</p> <!-- При клике на сообщение вызывается метод openModalToDelete, который эмитит два события в родительский компонент: -->
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      msgIndexToDelete: null,
    }
  },
  props: ['msgs', 'sender'],
  methods: {
    openModalToDelete(index) {
      this.msgIndexToDelete = index;
      this.$emit('openModal', true);
    },
    closeModal() {
      this.$emit('closeModal', false);
    },
    deleteMsg() {
      this.$emit('deleteMsg', this.msgIndexToDelete);
      this.msgIndexToDelete = null;
    },
		openModalToDelete(index) {
  this.$emit('openModal', true); /* открывает модальное окно. */
  this.$emit('msgIndexToDelete', index); /*передает индекс сообщения, которое нужно удалить. */
},

  },
}
</script>



<style>
.chat__body {
	height: 80%;
	overflow-y: auto;
	overflow-x: hidden;
}
.chat__body-item {
	display: flex;
	flex-direction: column;
	gap: 10px;
	padding: 10px 5px;
}
.chat__body-item-content {
	display: flex;
	align-items: center;
	padding: 0 5px;
	gap: 5px;
}
.chat__body-item-content p {
	color: rgb(0, 0, 0);
	font-size: 16px;
	font-weight: 400;
	line-height: 19px;
	width: 100%;
	max-width: 300px;
	word-wrap: break-word;
	word-break: break-word;
}

.chat__body-item-content.send {
	justify-content: end;
}
.chat__body-item-content.send div {
	border-radius: 15px 15px 0px 15px;
	background: rgb(208, 220, 255);
}
.chat__body-item-content.get {
	justify-content: start;
	flex-direction: row-reverse;
}
.chat__body-item-content.get div {
	border-radius: 15px 15px 0 15px;
	background: rgb(196, 191, 255);
	padding: 5px 10px;
}
</style>
