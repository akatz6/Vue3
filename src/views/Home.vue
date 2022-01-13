<template>
  <div class="home">{{ name }}</div>
</template>

<script lang="ts">
import { ref, computed, watch, defineComponent, toRefs } from 'vue';
import HelloWorld from '@/components/HelloWorld.vue'; // @ is an alias to /src
import { useStore } from 'vuex';

export default defineComponent({
  name: 'Home',
  components: {
    // HelloWorld,
  },
  setup(props: any, context: any) {
    const store = useStore();
    store.dispatch('user/setName', 'Aaron');
    const name = computed(() => store.getters['user/getName']);
    const activeSearchTerm = ref('');
    const enteredSearchTerm = ref('');
    watch(enteredSearchTerm, function (newValue) {
      setTimeout(() => {
        if (newValue === enteredSearchTerm.value) {
          activeSearchTerm.value = newValue;
        }
      }, 300);
    });
    console.log(name.value);
    store.dispatch('user/setName', 'Betty');
    console.log(name.value);
    return {
      name,
    };
  },
});
</script>
