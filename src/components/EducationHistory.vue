<script setup>
import { onMounted } from "vue";
import gsap from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";
import { GraduationCap, School, Code } from "lucide-vue-next";

gsap.registerPlugin(ScrollTrigger);

const education = [
  {
    title: "Korea Software HRD Center",
    period: "January 2025 - December 2025",
    description: "Intensive Full Stack Development & Cybersecurity Training",
    details: [
      "Basic Course: Comprehensive training in Web Development (HTML5, CSS3, JavaScript, Vue.js) and Backend systems (SpringBoot, PostgreSQL).",
      "Advanced Course: Specialized in Cybersecurity foundations, including Network Security, Web Vulnerability Scanning (Black box/White box), and secure coding practices.",
      "Successfully completed real-world team projects like Zentrio (Project Management) and PentraBox (Security Scanner).",
    ],
    icon: Code,
    color: "#a855f7",
  },
  {
    title: "University (In Progress)",
    period: "2023 - Present",
    description: "Bachelor of Computer Science",
    details: [
      "Currently focusing on core Computer Science principles: Algorithms, Data Structures, and Software Engineering.",
      "Developing projects using C# and exploring mobile development with Flutter.",
      "Maintaining a strong academic record while actively participating in tech workshops and university clubs.",
    ],
    icon: GraduationCap,
    color: "#6366f1",
  },
  {
    title: "High School",
    period: "2020 - 2022",
    description: "General Education Diploma",
    details: [
      "Graduated from Hunsen Chamkar Leu High School with a focus on Mathematics and English.",
      "Participated in various extracurricular activities and developed early interests in technology.",
    ],
    icon: School,
    color: "#3b82f6",
  },
];

onMounted(() => {
  const items = document.querySelectorAll(".timeline-item");

  items.forEach((item, index) => {
    gsap.from(item, {
      scrollTrigger: {
        trigger: item,
        start: "top 85%",
        toggleActions: "play none none none",
      },
      x: index % 2 === 0 ? -50 : 50,
      opacity: 0,
      duration: 1,
      ease: "power3.out",
    });
  });

  gsap.from(".timeline-line", {
    scrollTrigger: {
      trigger: ".timeline-container",
      start: "top 80%",
      end: "bottom 20%",
      scrub: 1,
    },
    scaleY: 0,
    transformOrigin: "top",
  });
});
</script>

<template>
  <section id="history" class="section">
    <div class="section-header">
      <h2 class="section-title">
        My <span class="gradient-text">Education</span>
      </h2>
      <p class="section-subtitle">
        A journey of continuous learning and growth.
      </p>
    </div>

    <div class="timeline-container">
      <div class="timeline-line"></div>

      <div
        v-for="(item, index) in education"
        :key="index"
        class="timeline-item"
        :class="{ reverse: index % 2 !== 0 }"
      >
        <div class="timeline-dot-wrapper">
          <div class="timeline-dot" :style="{ backgroundColor: item.color }">
            <component :is="item.icon" :size="18" color="white" />
          </div>
        </div>

        <div class="timeline-card-wrapper">
          <div class="glass timeline-card">
            <div class="card-header">
              <span class="period">{{ item.period }}</span>
              <h3 class="milestone-title">{{ item.title }}</h3>
            </div>
            <p class="milestone-desc">{{ item.description }}</p>
            <ul class="milestone-details">
              <li v-for="(detail, i) in item.details" :key="i">{{ detail }}</li>
            </ul>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.timeline-container {
  position: relative;
  max-width: 1000px;
  margin: 4rem auto 0;
  padding: 2rem 0;
}

.timeline-line {
  position: absolute;
  left: 50%;
  top: 0;
  bottom: 0;
  width: 2px;
  background: var(--accent-gradient);
  transform: translateX(-50%);
  opacity: 0.3;
}

.timeline-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 4rem;
  width: 100%;
}

.timeline-item.reverse {
  flex-direction: row-reverse;
}

.timeline-card-wrapper {
  width: 45%;
}

.timeline-dot-wrapper {
  width: 10%;
  display: flex;
  justify-content: center;
  position: relative;
  z-index: 10;
}

.timeline-dot {
  width: 42px;
  height: 42px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  background: var(--accent-color);
  box-shadow: 0 0 20px rgba(99, 102, 241, 0.4);
  border: 4px solid var(--bg-color);
}

.timeline-card {
  padding: 2rem;
  transition: var(--transition-smooth);
  cursor: default;
}

.timeline-card:hover {
  transform: translateY(-5px);
  border-color: var(--accent-color);
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
}

.card-header {
  margin-bottom: 1rem;
}

.period {
  font-size: 0.85rem;
  font-weight: 600;
  color: var(--accent-color);
  text-transform: uppercase;
  letter-spacing: 0.05em;
}

.milestone-title {
  font-size: 1.5rem;
  margin-top: 0.25rem;
}

.milestone-desc {
  color: var(--text-primary);
  font-weight: 500;
  margin-bottom: 1rem;
}

.milestone-details {
  padding-left: 1.25rem;
  color: var(--text-secondary);
  font-size: 0.95rem;
}

.milestone-details li {
  margin-bottom: 0.5rem;
  list-style-type: circle;
}

@media (max-width: 768px) {
  .timeline-line {
    left: 30px;
  }

  .timeline-item,
  .timeline-item.reverse {
    flex-direction: row;
    justify-content: flex-start;
    padding-left: 60px;
  }

  .timeline-card-wrapper {
    width: 100%;
  }

  .timeline-dot-wrapper {
    position: absolute;
    left: 8px;
    width: auto;
  }

  .timeline-dot {
    width: 36px;
    height: 36px;
  }
}
</style>
