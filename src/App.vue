<template>
  <div id="app" class="min-h-screen bg-grey-darker p-8">
    <div class="max-w-sm mx-auto card mt-8">
      <label class="form-label mb-2">Tags</label>
      <inline-tag-input v-model="tags"/>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import InlineTagInput from '@/components/InlineTagInput.vue';

@Component({
  name: "App",
  components: {
    InlineTagInput
  }
})
export default class App extends Vue {
  tags = ["first", "second", "third"];
}
</script>

<style src="@/assets/css/app.css"></style>
