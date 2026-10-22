<script setup>
import { ref, reactive, onMounted, onUnmounted } from 'vue'
import './index.css'

const menuOpen = ref(false)
const imageError = ref(false)

const navItems = [
  { id: 'home', label: 'Home' },
  { id: 'about', label: 'About' },
  { id: 'skills', label: 'Skills' },
  { id: 'projects', label: 'Projects' },
  { id: 'education', label: 'Education' },
  { id: 'certifications', label: 'Certifications' },
  { id: 'contact', label: 'Contact' }
]

const skills = [
  { name: 'Communication Skills', icon: '𓇵', level: 90, label: 'Comfortable',
    description: 'Active listening and articulate expression that foster collaboration, and strengthen stakeholder relationships.' },

  { name: 'Resolve Hardware Issues', icon: '𓇲', level: 84, label: 'Developing',
    description: 'Diagnosing, troubleshooting, and repairing computer components and peripheral devices.' },

  { name: 'Designing and Implementing circuits', icon: '𓆰', level: 88, label: 'Developing',
    description: 'Creating efficient circuit designs, and validating performance against rigorous technical specifications.' },

  { name: 'Testing and Debugging', icon: '𓍝', level: 79, label: 'Learning',
    description: 'Identifying, diagnosing, and resolving bugs and system vulnerabilities to ensure seamless, error-free execution.' },

  { name: 'Problem Solving', icon: '𓌩', level: 85, label: 'Developing',
    description: 'Deconstructing complex obstacles and applying analytical thinking to deliver optimal, innovative solutions under pressure.' },

  { name: 'Teamwork', icon: '𓎬', level: 89, label: 'Developing',
    description: 'Communicating, collaborating, and sharing ideas openly to strengthen team dynamics and deliver high-quality outcomes.' }
]

const projects = [
  {
    title: 'Custom Regulated Power Supply',
    symbol: '⚡',
    tags: ['Hardware', 'Circuit Design'],
    description: 'An electronics project focused on regulated power supply design and providing a controlled DC output.',
    category: 'ELECTRONICS'
  },
  {
    title: 'Custom PIC Development Board',
    symbol: '🛠️',
    tags: ['PIC', 'Hardware'],
    description: 'A specialized hardware platform designed to simplify the prototyping, testing, and debugging of projects using Microchip PIC microcontrollers.',
    category: 'ELECTRONICS'
  },
  {
    title: 'Illegal Parking Detector',
    symbol: '🚗',
    tags: ['Detection System', 'Engineering'],
    description: 'An automated, smart surveillance system designed to monitor restricted zones and identify vehicle parking violations in real time.',
    category: 'EMBEDDED SYSTEMS',
  },
  {
    title: 'Computer Engineering Alumni Job Portal', 
    symbol: '💻',
    tags: ['UI/UX Design', 'Database'],
    description: 'A specialized web application engineered to bridge the gap between graduating students, seasoned alumni, and tech industry employers.',
    category: 'WEB DEVELOPMENT',
    
  },
  {
    title: 'Arduino-Based Automated Ventilation System', 
    symbol: '🌡️',
    tags: ['Arduino', 'Sensors', 'SMS'],
    description: 'An intelligent climate control system designed to automatically regulate indoor air quality, temperature, and airflow.',
    category: 'AUTOMATION'
  }
]

const certifications = [
  {
    title: 'Regional ITE Summit 2026',
    theme: 'Theme: Building Smarter Futures through Technology and Engineering',
    year: '[2026]'
  },
  {
    title: 'International Conference on Engineering the Intelligent Future',
    theme: 'Theme: ENVISION, CONSTRUCT, EMPOWER',
    year: '[2026]',
  },
  {
    title: 'Frontiers of Computer Engineering: 2025 International Conference on New and Emerging Technologies',
    theme: 'Theme: Collaborative Innovation: Shaping the Future of Technology through Academic-Industry Partnership',
    year: '[2025]',
  }
]

const email = 'cristylsacatani6@gmail.com'
const location = 'Tuguegarao City, Cagayan, Philippines'

const socials = [
  { name: 'GitHub', url: 'https://github.com/cristylsacatani-cell' },
  { name: 'Facebook', url: 'https://www.facebook.com/share/1EkYFKhuSo/' }
]

const form = reactive({
  name: '',
  email: '',
  subject: '',
  message: ''
})

function sendMessage() {
  const body = [
    `Name: ${form.name}`,
    `Email: ${form.email}`,
    '',
    form.message
  ].join('\n')

  const mailto = `mailto:${email}?subject=${encodeURIComponent(form.subject)}&body=${encodeURIComponent(body)}`
  window.location.href = mailto
}

let observer

onMounted(() => {
  observer = new IntersectionObserver((entries) => {
    entries.forEach((entry) => {
      if (entry.isIntersecting) {
        entry.target.classList.add('visible')
        observer.unobserve(entry.target)
      }
    })
  }, { threshold: 0.12 })

  document.querySelectorAll('.reveal').forEach((element) => {
    observer.observe(element)
  })
})

onUnmounted(() => {
  observer?.disconnect()
})
</script>


<template>
  <div class="portfolio">
    <!-- Navigation -->
    <header class="navbar">
      <a href="#home" class="logo">C<span>S</span></a>

      <button class="menu-toggle" @click="menuOpen = !menuOpen"
        aria-label="Toggle navigation">
        {{ menuOpen ? '✕' : '☰' }}
      </button>

      <nav :class="{ 'nav-open': menuOpen }">
        <a v-for="item in navItems" :key="item.id"
          :href="'#' + item.id" @click="menuOpen = false">
          {{ item.label }}
        </a>
        <a href="#contact" class="nav-cta" @click="menuOpen = false">
          Let's Talk ↗
        </a>
      </nav>
    </header>

    <main>
      <!-- HOME -->
      <section id="home" class="hero section">
        <div class="hero-content reveal">
          <p class="eyebrow">
            <span class="status-dot"></span>
            Aspiring Developer & Creative Thinker
          </p>

          <h1>
            Hi, I'm<br />
            <span class="gradient-text">Cristyl Joy</span><br />
            E. Sacatani<span class="accent"></span>
          </h1>

          <p class="hero-description">
            I'm passionate about technology, creative problem-solving,
            and building digital experiences that turn ideas into reality.
            Welcome to my personal portfolio.
          </p>

          <div class="hero-actions">
            <div class="cv-dropdown-container">
  <!-- Hidden checkbox that stores the toggled state -->
  <input type="checkbox" id="cv-dropdown-toggle" class="dropdown-checkbox" />

  <!-- The main button styled as a label connected to the checkbox -->
  <label for="cv-dropdown-toggle" class="btn btn-primary cv-btn">
    <span>Curriculum Vitae</span>
    <span class="chevron">▾</span>
  </label>

  <!-- Dropdown Menu Options -->
  <div class="cv-dropdown-menu">
    <a 
      href="/Sacatani_cv.pdf" 
      target="_blank" 
      rel="noopener noreferrer" 
      class="cv-dropdown-item"
    >
      <span class="icon">👁️</span>
      <div class="item-text">
        <strong>View CV</strong>
        <small>Open PDF in browser</small>
      </div>
    </a>

    <a 
      href="/Sacatani_cv.pdf" 
      download="Sacatani_cv.pdf" 
      class="cv-dropdown-item"
    >
      <span class="icon">📥</span>
      <div class="item-text">
        <strong>Download CV</strong>
        <small>Save PDF file</small>
      </div>
    </a>
  </div>
</div>
            <a href="#projects" class="btn btn-outline">
              Explore My Work <span>↗</span>
            </a>
          </div>

          <div class="hero-socials">
            <span>LET'S CONNECT</span>
            <a href="#contact" aria-label="Contact me">✉</a>
            <a href="#projects" aria-label="View projects">⌘</a>
          </div>
        </div>

        <div class="hero-visual reveal">
          <div class="orbit orbit-one"></div>
          <div class="orbit orbit-two"></div>
          <div class="photo-frame">
            <img
              src="/home_pic.jpg"
              alt="Cristyl Sacatani profile"
              class="profile-image"
              @error="imageError = true"
              v-if="!imageError"
            />
            <div class="photo-placeholder" v-else>
              <span>CS.</span>
              <p>ADD YOUR PROFILE PHOTO</p>
              <small>Save your image as public/profile.jpg</small>
            </div>
          </div>
          <div class="floating-tag tag-top">♠ CREATIVE</div>
          <div class="floating-tag tag-bottom">CODE. CREATE. INSPIRE.</div>
          <div class="hero-number">01 <span>/ 07</span></div>
        </div>

        <a href="#about" class="scroll-indicator">
          <span></span> SCROLL TO DISCOVER
        </a>
      </section>

<!-- ABOUT -->
      <section id="about" class="section about-section">
        <div class="section-heading reveal">
          <p class="eyebrow">02 / GET TO KNOW ME</p>
          <h2>More Than Just <span class="gradient-text">A Name.</span></h2>
        </div>

        <div class="about-grid">
          <div class="about-visual reveal">
            <div class="orbit orbit-one"></div>
            <div class="orbit orbit-two"></div>
            <div class="photo-frame">
              <img
                src="/about_pic.jpg"
                alt="Cristyl Sacatani profile"
                class="profile-image"
                @error="imageError = true"
                v-if="!imageError"
              />
              <div class="photo-placeholder" v-else>
                <span>CS.</span>
                <p>ADD YOUR ABOUT PHOTO</p>
                <small>Save your image as public/about_pic.jpg</small>
              </div>
            </div>
          </div>

          <div class="about-content reveal">
            <p>
              I am an aspiring developer driven by
              a passion for technology, software engineering, and digital 
              innovation. I thrive on tackling complex technical challenges 
              and translating abstract concepts into functional, real-world 
              applications through hands-on development.
            </p>
            <p>
              My goal is to continue growing as a developer, create
              meaningful digital solutions, and turn every learning
              experience into an opportunity to improve.
            </p>

            <div class="about-stats">
              <div><strong>01</strong><span>CURIOSITY</span></div>
              <div><strong>02</strong><span>ADOPTABILITY</span></div>
              <div><strong>03</strong><span>EXECUTION</span></div>
            </div>
            <a href="#contact" class="text-link">Let's work together ↗</a>
          </div>
        </div>
      </section>


      <!-- SKILLS -->
      <section id="skills" class="section dark-section">
        <div class="section-heading reveal">
          <p class="eyebrow">03 / WHAT I BRING</p>
          <h2>My <span class="gradient-text">Skills</span></h2>
          <p class="section-description">
            A practical breakdown of the skills I use to turn ideas into tangible projects
          </p>
        </div>

        <div class="skills-grid">
          <article class="skill-card reveal"
            v-for="(skill, index) in skills" :key="skill.name">
            <div class="skill-card-top">
              <span class="skill-index">0{{ index + 1 }}</span>
              <span class="skill-icon">{{ skill.icon }}</span>
            </div>
            <h3>{{ skill.name }}</h3>
            <p>{{ skill.description }}</p>
            <div class="skill-track">
              <span :style="{ width: skill.level + '%' }"></span>
            </div>
            <div class="skill-meta">
              <span>{{ skill.level }}%</span>
              <span>{{ skill.label }}</span>
            </div>
          </article>
        </div>
      </section>

      <!-- PROJECTS -->
      <section id="projects" class="section">
        <div class="section-heading reveal">
          <p class="eyebrow">04 / WHAT I'VE BUILT</p>
          <h2>Featured <span class="gradient-text">Projects</span></h2>
          <p class="section-description">
            Projects and ideas
          </p>
        </div>

        <div class="projects-grid">
          <article class="project-card reveal"
            v-for="(project, index) in projects" :key="project.title">
            <div class="project-art" :class="'art-' + (index + 1)">
              <span class="project-art-number">0{{ index + 1 }}</span>
              <span class="project-art-symbol">{{ project.symbol }}</span>
              <span class="project-art-caption">{{ project.category }}</span>
            </div>
            <div class="project-info">
              <div class="project-tags">
                <span v-for="tag in project.tags" :key="tag">{{ tag }}</span>
              </div>
              <h3>{{ project.title }}</h3>
              <p>{{ project.description }}</p>
            </div>
          </article>
        </div>
      </section>

      <!-- EDUCATION -->
      <section id="education" class="section dark-section">
        <div class="section-heading reveal">
          <p class="eyebrow">05 / MY ACADEMIC JOURNEY</p>
          <h2>My <span class="gradient-text">Education</span></h2>
        </div>

        <div class="timeline">
          <article class="timeline-item reveal">
            <div class="timeline-dot"></div>
            <div class="timeline-date">PRESENT</div>
            <div class="timeline-card">
              <span class="timeline-type">CURRENT EDUCATION</span>
              <h3>Bachelor of Science in Computer Engineering</h3>
              <h4>Cagayan State University - Carig Campus</h4>
              <p>
                Developing my knowledge, technical skills, and practical
                experience through academic learning and projects.
              </p>
              <span class="timeline-period">[2023 – Present]</span>
            </div>
          </article>

          <article class="timeline-item reveal">
            <div class="timeline-dot"></div>
            <div class="timeline-date">PREVIOUS</div>
            <div class="timeline-card">
              <span class="timeline-type">PREVIOUS EDUCATION</span>
              <h3>Science, Technology, Engineering and Mathematics</h3>
              <h4>Pamplona National School of Fisheries</h4>
              <p>
                Built a foundation in learning, communication,
                collaboration, and problem-solving.
              </p>
              <span class="timeline-period">[2021 – 2023]</span>
            </div>
          </article>
        </div>
      </section>

      <!-- CERTIFICATIONS -->
      <section id="certifications" class="section">
        <div class="section-heading reveal">
          <p class="eyebrow">06 / LEARNING NEVER STOPS</p>
          <h2>Certifications<span class="gr
            adient-text"></span></h2>
          <p class="section-description">
            Courses, training, and achievements that support my growth
          </p>
        </div>

        <div class="cert-grid">
          <article class="cert-card reveal"
            v-for="(cert, index) in certifications" :key="cert.title">
            <div class="cert-icon">⁂</div>
            <div class="cert-number">CERTIFICATE / 0{{ index + 1 }}</div>
            <h3>{{ cert.title }}</h3>
            <p>{{ cert.theme }}</p>
            <span class="cert-year">{{ cert.year }}</span>
            <a v-if="cert.link" :href="cert.link"
              target="_blank" rel="noopener noreferrer" class="text-link">
              View Credential ↗
            </a>
          </article>
        </div>
      </section>

      <!-- CONTACT -->
      <section id="contact" class="section contact-section dark-section">
        <div class="contact-grid">
          <div class="contact-content reveal">
            <p class="eyebrow">07 / LET'S CONNECT</p>
            <h2>Have an Idea?<br /><span class="gradient-text">Let's Talk.</span></h2>
            <p>
              Have a question, collaboration idea, or opportunity?
              I'd love to hear from you. Send me a message.
            </p>

            <div class="contact-detail">
              <span class="contact-icon">✉</span>
              <div>
                <small>EMAIL ME</small>
                <a :href="'mailto:' + email">{{ email }}</a>
              </div>
            </div>

            <div class="contact-detail">
              <span class="contact-icon">⌖</span>
              <div>
                <small>LOCATION</small>
                <span>{{ location }}</span>
              </div>
            </div>

            <div class="social-links">
              <a v-for="social in socials" :key="social.name"
                :href="social.url" target="_blank"
                rel="noopener noreferrer">{{ social.name }} ↗</a>
            </div>
          </div>

          <form class="contact-form reveal" @submit.prevent="sendMessage">
            <h3>Send a Message<span class="accent">.</span></h3>

            <label for="name">YOUR NAME</label>
            <input id="name" v-model.trim="form.name"
              type="text" placeholder="Enter your name" required />

            <label for="sender-email">YOUR EMAIL</label>
            <input id="sender-email" v-model.trim="form.email"
              type="email" placeholder="you@example.com" required />

            <label for="message">MESSAGE</label>
            <textarea id="message" v-model.trim="form.message"
              rows="5" placeholder="Write your message..." required></textarea>

            <button class="btn btn-primary submit-btn" type="submit">
              Send message<span>➢</span>
            </button>
          </form>
        </div>
      </section>
    </main>

    <!-- FOOTER -->
    <footer class="footer">
      <a href="#home" class="logo">C<span>S</span></a>
      <p>Designed & built by <strong>Cristyl Joy E. Sacatani</strong></p>
      <a href="#home" class="back-top">BACK TO TOP ↑</a>
      <p class="copyright">© {{ new Date().getFullYear() }} All rights reserved.</p>
    </footer>
  </div>
</template>
