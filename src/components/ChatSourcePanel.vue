<template>
  <div class="source-panel">
    <h3>Sources for {{ chat?.name }}</h3>

    <div
      v-for="(sources, category) in chat?.sources || {}"
      :key="category"
      class="category-section"
    >
      <button class="category-toggle" @click="toggleSection(category)">
        {{ formatCategoryName(category) }}
        <span>{{ isOpen(category) ? '▲' : '▼' }}</span>
      </button>

      <ul v-show="isOpen(category)">
        <li v-for="source in sources" :key="source.url" class="source-item">
          <div class="source-wrapper">
            <div class="thumbnail" v-if="source.article_image_url">
              <img :src="source.article_image_url" alt="Source Image" />
            </div>

            <div class="content">
              <a :href="source.url" target="_blank" rel="noopener noreferrer">
                {{ source.title }}
              </a>
              <p class="summary">{{ source.placeholder_summary }}</p>
              <p class="meta">
                <strong>{{ source.entity_name }}</strong>
              </p>
            </div>
          </div>
        </li>

        <li v-if="sources.length === 0" class="empty">No sources available for this category.</li>
      </ul>
    </div>
  </div>
</template>

<script setup>
  import { defineProps, reactive } from 'vue';

  const props = defineProps({
    chat: Object,
    isExpanded: Boolean
  });

  const openSections = reactive({});

  const toggleSection = (section) => {
    openSections[section] = !openSections[section];
  };

  const isOpen = (section) => openSections[section];

  const formatCategoryName = (key) =>
    key.charAt(0).toUpperCase() + key.slice(1);
</script>

<style scoped>
.source-panel {
  width: 100%;
  padding: 15px;
  background: #ffffff;
  overflow-y: auto;
  font-family: sans-serif;
}

h3 {
  font-size: 1.25rem;
  margin-bottom: 15px;
  color: #1d352d;
}

.category-section {
  margin-bottom: 20px;
}

.category-toggle {
  background: #c0d6df;
  border: none;
  padding: 10px 12px;
  font-weight: 600;
  width: 100%;
  text-align: left;
  font-size: 1rem;
  cursor: pointer;
  display: flex;
  justify-content: space-between;
  border-radius: 6px;
  transition: background 0.2s ease;
}

.category-toggle:hover {
  background: #a9d6e5;
}

ul {
  list-style: none;
  padding: 0;
  margin-top: 12px;
}

.source-item {
  padding: 12px;
  margin-bottom: 10px;
  background: white;
  border-radius: 8px;
  border: 2px solid #0e6ba8;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.03);
}

.source-wrapper {
  display: flex;
  align-items: center;
  gap: 15px;
}

.thumbnail {
  width: 80px;
  height: 80px;
  flex-shrink: 0;
  display: flex;
  align-items: center;
  justify-content: center;
}

.thumbnail img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  border-radius: 6px;
  border: none;
}

.content {
  flex: 1;
  text-align: left;
}

.content a {
  font-weight: bold;
  color: #0077cc;
  text-decoration: none;
  font-size: 1rem;
}

.content a:hover {
  text-decoration: underline;
}

.summary {
  font-size: 0.9rem;
  color: #081c15;
  margin: 5px 0;
}

.meta {
  font-size: 0.8rem;
  color: #081c15;
}

.empty {
  font-style: italic;
  color: #59a5d8;
  padding-left: 10px;
}
</style>
