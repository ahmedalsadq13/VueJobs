<script setup>

import { RouterLink } from 'vue-router';

</script>

<template>
    
    <!-- Go Back -->
    <section>
      <div class="container mr-auto py-6 px-6 w-fit">
        <RouterLink
          to="/jobs"
          class="text-green-500 hover:text-green-600 flex items-center py-3 px-5"
        >
          <i class="pi pi-arrow-circle-left mr-2"></i> Back to Job Listings
        </RouterLink>
      </div>
    </section>

</template>