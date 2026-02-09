<script setup>
const skillCategories = [
  {
    name: 'Frontend',
    skills: ['Vue.js', 'React', 'TypeScript', 'Tailwind CSS', 'GSAP']
  },
  {
    name: 'Backend',
    skills: ['Node.js', 'Express', 'Python', 'PostgreSQL', 'Redis']
  },
  {
    name: 'Tools & DevOps',
    skills: ['Git', 'Docker', 'AWS', 'Vite', 'Figma']
  }
]
</script>

<template>
  <section id="skills" class="section">
    <div class="section-header">
      <h2 class="section-title">Technical <span class="gradient-text">Skills</span></h2>
      <p class="section-subtitle">The tools and technologies I use to bring ideas to life.</p>
    </div>

    <div class="skills-grid">
      <div v-for="category in skillCategories" :key="category.name" class="glass skill-category">
        <h3 class="category-name">{{ category.name }}</h3>
        <div class="skills-list">
          <div v-for="skill in category.skills" :key="skill" class="skill-item">
            <div class="skill-dot"></div>
            <span>{{ skill }}</span>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.section-header {
  margin-bottom: 3rem;
}

.section-title {
  font-size: 2.5rem;
  margin-bottom: 1rem;
}

.section-subtitle {
  color: var(--text-secondary);
}

.skills-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 2rem;
}

.skill-category {
  padding: 2rem;
  transition: var(--transition-smooth);
}

.skill-category:hover {
  border-color: var(--accent-color);
  transform: scale(1.02);
}

.category-name {
  font-size: 1.5rem;
  margin-bottom: 1.5rem;
  color: var(--text-primary);
}

.skills-list {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.skill-item {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  color: var(--text-secondary);
}

.skill-dot {
  width: 8px;
  height: 8px;
  background: var(--accent-gradient);
  border-radius: 50%;
}

.skill-item span {
  font-weight: 500;
}
</style>
