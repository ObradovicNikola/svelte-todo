<script>
  import { createEventDispatcher } from "svelte";
  import shortid from "shortid";

  export let editingTodo;

  const dispatch = createEventDispatcher();

  $: title = editingTodo.title;
  function onSubmit(event) {
    event.preventDefault();

    if (title.trim() === "") {
      alert("error");
      return;
    } else {
      let todos = JSON.parse(window.localStorage.getItem("todos"));
      if (editingTodo.id !== null) {
        const newTodo = {
          title,
          timestamp: new Date(),
          id: editingTodo.id
        };
        const index = todos.findIndex(todo => todo.id === newTodo.id);
        todos[index] = newTodo;
      } else {
        const newTodo = {
          title,
          timestamp: new Date(),
          id: shortid.generate()
        };
        todos = [newTodo, ...todos];
      }
      window.localStorage.setItem("todos", JSON.stringify(todos));
      dispatch("todoCreated");
      editingTodo = {
        title: "",
        id: null
      };
    }
  }
</script>

<style>
  form {
    padding: 20px;
  }
</style>

<form on:submit={onSubmit} action="">
  <div class="input-field">
    <label for="title">Title</label>
    <input id="input-title" type="text" bind:value={editingTodo.title} />
  </div>
  <button type="submit" class="waves-effect waves-light btn">
    {editingTodo.id ? 'Update' : 'Add'}
  </button>
</form>
