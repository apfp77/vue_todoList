<script setup lang="ts">

import { ref, computed } from "vue";

let id = 0;
let messages = ref([
  { id: id++, text: 'test1', done: false},
  { id: id++, text: 'test2', done: false},
  { id: id++, text: 'test3', done: false},
]);

let newText:string = '';
let hide_flag = ref(false);

//생성
const addTodo = () => {
	if (newText)
	{
		messages.value.push({ id: id++, text: newText, done:false });
		newText = '';
		messages.value.forEach((value) => console.log(value));
	}
}

//삭제
const removeTodo = () => {
	messages.value = messages.value.filter((value) => {
		if (value.done === false)
		return value;
	})
}

//숨김
// const hideTodo = () => {
// 	hide_flag.value = !hide_flag.value;
// 	if (hide_flag.value)
// 	{
// 		// let ret = messages.value.filter((value) => {
// 		// if (value.done === false)
// 		// 	return value;
// 		// });
// 		// return ret;
// 		return messages.value.filter((t) => !t.done);
// 	}
// }

const hideTodo = computed(()=>{
	if (hide_flag.value)
	{
		let ret = messages.value.filter((value) => {
		if (value.done === false)
			return value;
		});
		console.log(ret);
		return ret;
	}
	return messages.value
});


</script>


<template>
	<input v-model="newText" placeholder="입력창">
	<button @click="addTodo">생성</button>
	<li v-for="key in hideTodo" v-bind:key="key.id">
		<input v-model="key.done" type="checkbox">
		<span>{{ key.text }}</span>
	</li>
	<button @click="removeTodo">삭제</button>
	<button @click="hide_flag = !hide_flag">{{ hide_flag ? '보이기':'숨김'}}</button>
</template>
