<script setup>
import { onMounted } from "vue";
import { RouterLink, RouterView, useRoute, useRouter } from "vue-router";
import { library } from "@fortawesome/fontawesome-svg-core";
import { faFan } from "@fortawesome/free-solid-svg-icons";
import { useApplicationStore } from "./stores/application";

library.add(faFan);

const applicationStore = useApplicationStore();
const router = useRouter();

onMounted(() => {
  applicationStore.getIsSoftAPMode().then(() => {
    if (applicationStore.isSoftAPMode) {
      router.push("/wifimanager");
    }
  });
});
</script>

<template>
  <nav class="navbar navbar-expand-lg bg-light">
    <div class="container-fluid">
      <span class="navbar-brand mb-0 h1">Cabinet Fan Control
        <font-awesome-icon icon="fa-solid fa-fan" spin />
      </span>
      <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent"
        aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav me-auto mb-2 mb-lg-0">
          <li class="nav-item" v-if="!applicationStore.isSoftAPMode">
            <RouterLink class="nav-link" aria-current="page" to="/">Home</RouterLink>
          </li>
          <li class="nav-item">
            <RouterLink class="nav-link" aria-current="page" to="/wifimanager">WiFi Manager</RouterLink>
          </li>
        </ul>
      </div>
    </div>
  </nav>
  <RouterView />
</template>

<style scoped lang="scss">

</style>
