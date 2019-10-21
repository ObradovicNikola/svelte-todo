<script>
  import { setContext, getContext } from "svelte";
  import shortid from "shortid";
  import PostForm from "../components/PostForm.svelte";
  let todos = [];
  todos = JSON.parse(window.localStorage.getItem("todos"));
  let editingTodo = {
    title: "",
    id: null
  };
  function editTodo(todo) {
    editingTodo = todo;
    document.getElementById("input-title").focus();
  }

  function deleteTodo(todo) {
    todos = todos.filter(item => item.id !== todo.id);
    window.localStorage.setItem("todos", JSON.stringify(todos));
  }

  function addTodo() {
    todos = JSON.parse(window.localStorage.getItem("todos"));
  }
</script>

<style>
  .delete-btn {
    color: red !important;
  }

  .card .card-content .card-title {
    margin-bottom: 0;
  }
  .card .card-content p.timestamp {
    color: grey;
    margin-bottom: 10px;
  }
</style>

<div class="row">
  <div class="col s6">
    <PostForm on:todoCreated={addTodo} {editingTodo} />
  </div>
</div>
<div class="row">
  {#if todos.length > 0}
    {#each todos as todo}
      <div class="col s6">
        <div class="card">
          <div class="card-content">
            <p class="card-title">{todo.title}</p>
            <p class="timestamp">{todo.timestamp}</p>
          </div>
          <div class="card-action">
            <a href="#" on:click={() => editTodo(todo)}>Edit</a>
            <a href="#" class="delete-btn" on:click={() => deleteTodo(todo)}>
              Delete
            </a>
          </div>
        </div>
      </div>
    {/each}
  {:else}
    <div>Nothing to do for you.</div>
  {/if}
</div>
