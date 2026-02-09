<script setup>
import { ExternalLink, Github } from "lucide-vue-next";
import PentraBox from "@/assets/images/teamPentrabox.jpg";
import Zentrio from "@/assets/images/teamZentrio.jpg";
import SmartQuiz from "@/assets/images/SmartQuiz.jpg";
const projects = [
  {
    id: 1,
    title: "PentraBox",
    description:
      "It is a project that do in Advance Course. This project have two feature are Black box and White box. For Black box is use for scan website find vulnerability. For White box is use for scan code find vulnerability.",
    tags: ["Next.js", "FastAPI", "PostgreSQL"],
    github: "#",
    demo: "#",
    image: PentraBox,
  },
  {
    id: 2,
    title: "Zentrio",
    description:
      "It is a project that do in Basic Course. This project for help people to manage their task and schedule. We have gantt chart, calendar, and task management features. That make them easy to manage their work.",
    tags: ["Next.js", "SpringBoot", "PostgreSQL"],
    github: "#",
    demo: "#",
    image: Zentrio,
  },
  {
    id: 3,
    title: "SmartQuiz",
    description:
      "It is a small project that do in university. This project we practice on flutter and this app for use for assign quiz and student can join quiz. ( This is just small , no have real api just static with mock api)",
    tags: ["Flutter", "Mock API"],
    github: "https://github.com/Gemini210504",
    demo: "#",
    image: SmartQuiz,
  },
  {
    id: 4,
    title: "Attendance System",
    description:
      "It is a project that do in university. We create this project for inspire by school attendance system. ( This is just small , no have real api just static with mock api)",
    tags: ["C#", "PostgreSQL"],
    github: "https://github.com/Gemini210504/AttendanceSystem.git",
    demo: "#",
    image:
      "https://images.unsplash.com/photo-1472851294608-062f824d29cc?auto=format&fit=crop&q=80&w=2670",
  },
];
</script>

<template>
  <section id="projects" class="section">
    <div class="section-header">
      <h2 class="section-title">
        Selected <span class="gradient-text">Projects</span>
      </h2>
      <p class="section-subtitle">
        A collection of things I've built with passion and precision.
      </p>
    </div>

    <div class="projects-grid">
      <div
        v-for="project in projects"
        :key="project.id"
        class="glass project-card"
      >
        <div class="project-image-wrapper">
          <img
            :src="project.image"
            :alt="project.title"
            class="project-image"
          />
          <div class="project-overlay">
            <div class="overlay-links">
              <a
                :href="project.github"
                target="_blank"
                rel="noopener noreferrer"
                class="overlay-btn icon-btn"
                aria-label="GitHub"
              >
                <Github :size="20" />
              </a>
              <a
                :href="project.demo"
                target="_blank"
                rel="noopener noreferrer"
                class="overlay-btn icon-btn"
                aria-label="Live Demo"
              >
                <ExternalLink :size="20" />
              </a>
            </div>
          </div>
        </div>

        <div class="project-info">
          <div class="project-tags">
            <span v-for="tag in project.tags" :key="tag" class="tag">{{
              tag
            }}</span>
          </div>
          <h3 class="project-title">{{ project.title }}</h3>
          <p class="project-description">{{ project.description }}</p>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.section-header {
  margin-bottom: 3rem;
  text-align: center;
}

.section-title {
  font-size: 2.5rem;
  margin-bottom: 1rem;
}

.section-subtitle {
  color: var(--text-secondary);
}

.projects-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(350px, 1fr));
  gap: 2rem;
}

.project-card {
  overflow: hidden;
  display: flex;
  flex-direction: column;
  transition: var(--transition-smooth);
}

.project-card:hover {
  transform: translateY(-10px);
  border-color: var(--accent-color);
}

.project-image-wrapper {
  position: relative;
  aspect-ratio: 16 / 9;
  overflow: hidden;
}

.project-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.6s cubic-bezier(0.4, 0, 0.2, 1);
}

.project-card:hover .project-image {
  transform: scale(1.1);
}

.project-overlay {
  position: absolute;
  inset: 0;
  background: rgba(0, 0, 0, 0.6);
  display: flex;
  align-items: center;
  justify-content: center;
  opacity: 0;
  transition: var(--transition-smooth);
}

.project-card:hover .project-overlay {
  opacity: 1;
}

.overlay-links {
  display: flex;
  gap: 1.5rem;
}

.overlay-btn {
  background: white;
  color: black;
  width: 45px;
  height: 45px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: var(--transition-smooth);
}

.overlay-btn:hover {
  transform: scale(1.1);
  background: var(--accent-color);
  color: white;
}

.project-info {
  padding: 1.5rem;
  flex: 1;
}

.project-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
  margin-bottom: 1rem;
}

.tag {
  font-size: 0.75rem;
  font-weight: 600;
  padding: 0.2rem 0.6rem;
  background: var(--glass-bg);
  border: 1px solid var(--glass-border);
  border-radius: 4px;
  color: var(--text-secondary);
}

.project-title {
  font-size: 1.25rem;
  margin-bottom: 0.75rem;
}

.project-description {
  color: var(--text-secondary);
  font-size: 0.95rem;
  display: -webkit-box;
  -webkit-line-clamp: 3;
  -webkit-box-orient: vertical;
  overflow: hidden;
}

@media (max-width: 480px) {
  .projects-grid {
    grid-template-columns: 1fr;
  }
}
</style>
