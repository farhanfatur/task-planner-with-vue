<template>
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
      <div class="container-fluid">
        <a class="navbar-brand" href="#">Task Planner</a>
        <div class="collapse navbar-collapse" id="navbarText">
          <ul class="navbar-nav me-auto mb-2 mb-lg-0">
            <li class="nav-item">
              <b-link class="nav-link" href="#" @click="$emit('modalCard')" v-b-modal.modal-card>+ Add</b-link>
            </li>
          </ul>
        </div>
      </div>
    </nav>
</template>
<script>
export default {
    name: "Header",
    props: {

    }
}
</script>