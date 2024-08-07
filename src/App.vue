<template>
  <nav class="navbar navbar-expand-lg bg-body-tertiary">
    <div class="container-fluid">
      <router-link class="navbar-brand" :to="{name: 'Home'}">ssonggary</router-link>
      <ul class="navbar-nav mr-auto">
        <li class="nav-item">
          <router-link class="nav-link active" aria-current="page" :to="{name: 'Todos'}">Todos</router-link>
        </li>
      </ul>
    </div>
  </nav>
  <div class="container">
    <router-view/>
  </div>
  <Transition name="slide-fade">
    <Toast
      :message="toastMessage"
      :type="toastAlertType"
    />
  </Transition>
</template>

<script>
  import Toast from '@/components/Toast.vue';
  import { useToast } from '@/composables/toast';

  export default {
    components: {
      Toast,
    },
    setup() {
      const {
        showToast,
        toastMessage,
        toastAlertType,
        triggerToast,
      } = useToast();

      return {
        showToast,
        toastMessage,
        toastAlertType,
        triggerToast,
      }
    }
  }
</script>

<style scoped>
  .slide-fade-enter-active {
    transition: all 0.3s ease-out;
  }

  .slide-fade-leave-active {
    transition: all 0.8s cubic-bezier(1, 0.5, 0.8, 1);
  }

  .slide-fade-enter-from,
  .slide-fade-leave-to {
    transform: translateY(-20px);
    opacity: 0;
  }
</style>