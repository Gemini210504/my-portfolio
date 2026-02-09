<script setup>
import { Mail, MessageSquare, Send, Loader2 } from 'lucide-vue-next'
import { ref } from 'vue'
import emailjs from '@emailjs/browser'
import { toast } from 'vue-sonner'

const name = ref('')
const email = ref('')
const message = ref('')
const isSending = ref(false)

const handleSubmit = async () => {
  if (isSending.value) return
  
  isSending.value = true
  
  const templateParams = {
    from_name: name.value,
    from_email: email.value,
    message: message.value,
    to_name: 'Leang Chhengleap'
  }

  try {
    // NOTE: You need to replace these with your actual EmailJS IDs
    // Service ID, Template ID, and Public Key from your EmailJS dashboard
    await emailjs.send(
      'YOUR_SERVICE_ID', 
      'YOUR_TEMPLATE_ID', 
      templateParams,
      'YOUR_PUBLIC_KEY'
    )

    toast.success('Message sent successfully! I will get back to you soon.')
    
    // Reset form
    name.value = ''
    email.value = ''
    message.value = ''
  } catch (error) {
    console.error('EmailJS Error:', error)
    toast.error('Failed to send message. Please try again or email me directly.')
  } finally {
    isSending.value = false
  }
}
</script>

<template>
  <section id="contact" class="section">
    <div class="glass contact-container">
      <div class="contact-info">
        <h2 class="section-title">Let's <span class="gradient-text">Connect</span></h2>
        <p class="contact-desc">
          I'm currently looking for new opportunities. Whether you have a question 
          or just want to say hi, I'll try my best to get back to you!
        </p>
        
        <div class="contact-methods">
          <div class="method-item">
            <Mail :size="20" class="method-icon" />
            <div>
              <h4>Email</h4>
              <p>chhing020518@gmail.com</p>
            </div>
          </div>
          <div class="method-item">
            <MessageSquare :size="20" class="method-icon" />
            <div>
              <h4>Discord</h4>
              <p>leap#1234</p>
            </div>
          </div>
        </div>
      </div>

      <form class="contact-form" @submit.prevent="handleSubmit">
        <div class="form-group">
          <label for="name">Name</label>
          <input type="text" id="name" v-model="name" placeholder="Your Name" required />
        </div>
        <div class="form-group">
          <label for="email">Email</label>
          <input type="email" id="email" v-model="email" placeholder="your@email.com" required />
        </div>
        <div class="form-group">
          <label for="message">Message</label>
          <textarea id="message" v-model="message" rows="5" placeholder="Your Message" required></textarea>
        </div>
        <button type="submit" class="btn btn-primary submit-btn" :disabled="isSending">
          <template v-if="!isSending">
            Send Message <Send :size="18" />
          </template>
          <template v-else>
            Sending... <Loader2 :size="18" class="spin" />
          </template>
        </button>
      </form>
    </div>
  </section>
</template>

<style scoped>
.contact-container {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 4rem;
  padding: 4rem;
  border-radius: var(--border-radius);
}

.section-title {
  font-size: 2.5rem;
  margin-bottom: 1.5rem;
}

.contact-desc {
  color: var(--text-secondary);
  margin-bottom: 3rem;
  font-size: 1.1rem;
}

.contact-methods {
  display: flex;
  flex-direction: column;
  gap: 2rem;
}

.method-item {
  display: flex;
  gap: 1.5rem;
}

.method-icon {
  color: var(--accent-color);
  margin-top: 4px;
}

.method-item h4 {
  margin-bottom: 0.25rem;
}

.method-item p {
  color: var(--text-secondary);
}

.contact-form {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
}

.form-group {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

.form-group label {
  font-weight: 500;
  font-size: 0.9rem;
  color: var(--text-secondary);
}

.form-group input, 
.form-group textarea {
  background: rgba(255, 255, 255, 0.05);
  border: 1px solid var(--glass-border);
  padding: 1rem;
  border-radius: 8px;
  color: var(--text-primary);
  font-family: inherit;
  transition: var(--transition-smooth);
}

.form-group input:focus, 
.form-group textarea:focus {
  outline: none;
  border-color: var(--accent-color);
  background: rgba(255, 255, 255, 0.08);
}

.submit-btn {
  width: 100%;
  justify-content: center;
  margin-top: 1rem;
}

.submit-btn:disabled {
  opacity: 0.7;
  cursor: not-allowed;
}

.spin {
  animation: spin 1s linear infinite;
}

@keyframes spin {
  from { transform: rotate(0deg); }
  to { transform: rotate(360deg); }
}

.btn {
  padding: 0.8rem 2rem;
  border-radius: 50px;
  font-weight: 600;
  display: flex;
  align-items: center;
  gap: 0.75rem;
  transition: var(--transition-smooth);
  cursor: pointer;
}

.btn-primary {
  background: var(--accent-gradient);
  color: white;
  border: none;
}

.btn-primary:hover:not(:disabled) {
  transform: translateY(-2px);
  box-shadow: 0 10px 20px rgba(99, 102, 241, 0.3);
}

@media (max-width: 968px) {
  .contact-container {
    grid-template-columns: 1fr;
    padding: 2.5rem;
    gap: 3rem;
  }
}
</style>
