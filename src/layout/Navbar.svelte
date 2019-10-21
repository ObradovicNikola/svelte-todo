<script>
  import { Link } from "svelte-routing";
</script>

<style>
  .nav-link {
    color: white;
  }
</style>

<nav>
  <div class="nav-wrapper">
    <div class="container">
      <Link to="/">
        <span class="brand-logo">Svelte ToDo</span>
      </Link>
      <ul id="nav-mobile" class="right hide-on-med-and-down">
        <li>
          <Link to="/">
            <span class="nav-link">Home</span>
          </Link>
        </li>
        <li>
          <Link to="/about">
            <span class="nav-link">About</span>
          </Link>
        </li>
      </ul>
    </div>
  </div>
</nav>
