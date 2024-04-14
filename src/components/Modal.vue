<template>
  <div class="modal" v-if="showModal" @click="closeModal">
    <div class="modal__body" @click.stop>
      <h2 class="modal__body-title">Удалить сообщение</h2>

      <div class="modal__body-btns">
        <button class="modal__body-btn back" @click="closeModal">Отмена</button>
        <button class="modal__body-btn add" @click="deleteMsg()">Удалить</button> <!-- вызывается метод deleteMsg, который эмитит событие deleteMsg с переданным ранее индексом сообщения для удаления.  -->
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    showModal: Boolean,
    edit: Boolean,
    msgIndex: Number
  },
  methods: {
    closeModal() {
      this.$emit('closeModal', false)
    },
    deleteMsg() { 
      this.$emit('deleteMsg', this.msgIndex);
    },
  },
}
</script>


<style>
.modal {
	position: fixed;
	width: 100%;
	height: 100vh;
	background: rgba(0, 0, 0, 0.35);
	top: 0;
	left: 0;
	display: flex;
	justify-content: center;
	align-items: center;
}
.modal__body {
	padding: 24px;
	background: rgb(243, 237, 247);
	width: 100%;
	max-width: 312px;
	border-radius: 24px;
}
.modal__body-title {
	color: rgb(28, 27, 31);
	font-size: 24px;
	font-weight: 400;
	line-height: 32px;
}

.modal__body-btns {
	display: flex;
	justify-content: center;
	margin-top: 14px;
	gap: 5px;
}
.modal__body-btn {
	padding: 10px 12px;
	cursor: pointer;
}
.delete {
	color: rgb(207, 27, 27);
	font-size: 14px;
	font-weight: 500;
	line-height: 20px;
	text-transform: uppercase;
}
.edit {
	color: rgb(103, 80, 164);
	font-size: 14px;
	font-weight: 500;
	line-height: 20px;
	text-transform: uppercase;
}
</style>
