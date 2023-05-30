<template>
  <ul>
    <li>
      <learning-resource v-for="res in storedResources" :key="res.id">
      </learning-resource>
    </li>
  </ul>
</template>

<script>
import LearningResource from './components/learning-resources/LearningResource.vue';
export default {
  components: {
    LearningResource,
  },
  data() {
    return {
      storedResources: [
        {
          id: 'official-guide',
          title: 'official-guide',
          description: 'The official documentation to Vue JS',
          link: 'https://vuejs.org',
        },
        {
          id: 'google',
          title: 'Google',
          description: 'Learn to google...',
          link: 'https://vuejs.org',
        },
      ],
    };
  },
};
</script>
