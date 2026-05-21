---
layout: page
title: About Me
icon: fas fa-info-circle
order: 1
---

<div class="about-header">
  <h2 class="cyber-title">System.init("Omar El Bouhsaini")</h2>
  <p class="cyber-subtitle">Future Cybersecurity Engineer | Digital Developer</p>
</div>

<div class="cv-section" style="margin-top: 40px;">
  <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 15px;">
    <h3 style="font-family: 'JetBrains Mono', monospace;">> Terminal.access("Resume_v2026.pdf")</h3>
    <a href="/assets/img/CV_Omar_EL_BOUHSAINI_Cybersecurity_frnc.pdf" target="_blank" class="cyber-btn-small">
      <i class="fas fa-external-link-alt"></i> Full Screen
    </a>
  </div>
  
  <div class="pdf-wrapper">
    <iframe src="/assets/img/CV_Omar_EL_BOUHSAINI_Cybersecurity_frnc.pdf" class="pdf-embed"></iframe>
  </div>
</div>

I am a **4th-year Engineering Student** at **ENSA Fez**, specializing in **Digital Development and Cybersecurity**. My work focuses on the intersection of secure software architecture and offensive security methodologies.

Driven by a "Security-by-Design" mindset, I develop scalable applications while actively exploring threat hunting, penetration testing, and AI-driven anomaly detection.

---

## Technical Arsenal

<div class="skills-grid">
  <div class="skill-category">
    <div class="category-header">
      <i class="fas fa-user-secret"></i>
      <h3>Offensive Security</h3>
    </div>
    <div class="skill-list">
      <div class="skill-item"><span>OWASP Top 10</span></div>
      <div class="skill-item"><span>Network Pentesting (Nmap, Wireshark)</span></div>
      <div class="skill-item"><span>Exploitation Frameworks (Metasploit)</span></div>
      <div class="skill-item"><span>Vulnerability Assessment (Burp Suite)</span></div>
    </div>
  </div>

  <div class="skill-category">
    <div class="category-header">
      <i class="fas fa-code"></i>
      <h3>Secure Development</h3>
    </div>
    <div class="skill-list">
      <div class="skill-item"><span>Python (Security Automation)</span></div>
      <div class="skill-item"><span>PHP 8.3 (Secure MVC)</span></div>
      <div class="skill-item"><span>C / C++ & Java</span></div>
      <div class="skill-item"><span>Secure API Design</span></div>
    </div>
  </div>

  <div class="skill-category">
    <div class="category-header">
      <i class="fas fa-microchip"></i>
      <h3>Infrastructure & AI</h3>
    </div>
    <div class="skill-list">
      <div class="skill-item"><span>Network Protocols (TCP/IP, BGP)</span></div>
      <div class="skill-item"><span>Machine Learning for Security</span></div>
      <div class="skill-item"><span>Database Security (MySQL, Oracle)</span></div>
      <div class="skill-item"><span>Linux System Administration</span></div>
    </div>
  </div>
</div>

<style>
  /* --- Styles Globales --- */
  .cyber-title { font-family: 'JetBrains Mono', monospace; color: #ff3333; font-weight: 800; margin-bottom: 5px; }
  .cyber-subtitle { font-size: 1.1rem; color: #888; margin-bottom: 20px; font-family: monospace; }

  /* --- Styles PDF Viewer --- */
  .pdf-wrapper {
    width: 100%; height: 600px; background: #1e1e1e;
    border: 2px solid #ff3333; border-radius: 8px;
    overflow: hidden; box-shadow: 0 0 20px rgba(255, 51, 51, 0.2);
  }
  .pdf-embed { width: 100%; height: 100%; border: none; }
  .cyber-btn-small {
    font-family: 'JetBrains Mono', monospace; font-size: 0.8rem;
    color: #ff3333; border: 1px solid #ff3333; padding: 5px 10px;
    border-radius: 4px; text-decoration: none; transition: 0.3s;
  }
  .cyber-btn-small:hover { background: #ff3333; color: white; }

  /* --- Skills Grid --- */
  .skills-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 20px; margin-top: 20px; }
  .skill-category { background: rgba(136, 136, 136, 0.05); border: 1px solid rgba(136, 136, 136, 0.2); border-radius: 12px; padding: 20px; transition: all 0.3s ease; }
  .skill-category:hover { border-color: #ff3333; box-shadow: 0 5px 15px rgba(255, 51, 51, 0.1); transform: translateY(-5px); }
  .category-header { display: flex; align-items: center; gap: 12px; margin-bottom: 20px; border-bottom: 1px solid rgba(255, 51, 51, 0.3); padding-bottom: 10px; }
  .category-header i { color: #ff3333; font-size: 1.4rem; }
  .skill-item { background: rgba(136, 136, 136, 0.05); border: 1px solid rgba(136, 136, 136, 0.1); padding: 8px 12px; border-radius: 6px; font-family: monospace; font-size: 0.9rem; margin-bottom: 8px; transition: all 0.2s ease; }
  .skill-item:hover { background: rgba(255, 51, 51, 0.05); border-color: rgba(255, 51, 51, 0.4); padding-left: 18px; }
  
  @media (max-width: 768px) { .pdf-wrapper { height: 400px; } }
  html[data-mode="dark"] .skill-category { background: #1e1e1e; }
</style>