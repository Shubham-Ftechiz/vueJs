<script setup>
import { ref, onMounted, computed, watch } from 'vue'
// ref - way to use or handle state
// onMounted - when we first render the page
// computed - computed the order we created
// watch - watch any changes in the reference

const todos = ref([])
const name = ref('')

const input_content = ref('')
const input_contegory = ref(null)

const todos_asc = computed(()=> todos.value.sort((a,b)=>{
  return b.createdAt - a.createdAt
}))

watch(name,(newVal)=>{
  localStorage.setItem("name", newVal)
})

onMounted(()=>{
  name.value = localStorage.getItem("name") || ''
})

const addTodo = () => {
}

</script>
<template>
  <main class="app">
    <section class="greeting">
      <h2 class="title">
        What's up, <input type="text" placeholder="Name here" 
        v-model="name" />
      </h2>
    </section>

    <section class="create-todo">
      <h3>CREATE A TODO</h3>

      <form @submit.prevent="addTodo">
        <h4>What's on your todo list?</h4>
        <input type="text" placeholder="e.g make a video" v-model="input_content"/>

        <h4>Pick a category</h4>
        <div class="options">

            <label>
              <input 
              type="radio" name="category" 
              value="business"
              v-model="input_contegory"/>
              <span class="bubble business"></span>
              <div>Business</div>
            </label>

            <label>
              <input 
              type="radio" name="category" 
              value="personal"
              v-model="input_contegory"/>
              <span class="bubble personal"></span>
              <div>Personal</div>
            </label>

            <!-- {{ input_contegory }} -->
        </div>
          <input type="submit" value="Add todo">
      </form>
    </section>
  </main>
</template>
