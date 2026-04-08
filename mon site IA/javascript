let demoOrders = [];
let demoOrderId = 0;

const demoData = [
  { name: 'M. Dupont', dishes: 'Burger + Frites' },
  { name: 'Mme Martin', dishes: 'Pizza Margherita' },
  { name: 'Jean Petit', dishes: 'Steak + Salade' },
  { name: 'Sophie Laurent', dishes: 'Poulet rôti + légumes' },
  { name: 'M. Bernard', dishes: 'Pâtes Carbonara' }
];

window.addDemoOrder = function() {
  const randomData = demoData[Math.floor(Math.random() * demoData.length)];
  const order = {
    id: demoOrderId++,
    name: randomData.name,
    dishes: randomData.dishes,
    status: 'new',
    time: Math.floor(Math.random() * 25) + 5
  };
  demoOrders.push(order);
  if (demoOrders.length > 6) demoOrders.shift();
  renderDemoOrders();
};

window.updateDemoOrder = function() {
  if (demoOrders.length === 0) return;
  const randomIdx = Math.floor(Math.random() * demoOrders.length);
  const statuses = ['new', 'prep', 'ready'];
  const currentIdx = statuses.indexOf(demoOrders[randomIdx].status);
  if (currentIdx < statuses.length - 1) {
    demoOrders[randomIdx].status = statuses[currentIdx + 1];
  } else {
    demoOrders.splice(randomIdx, 1);
  }
  renderDemoOrders();
};

window.clearDemoOrders = function() {
  demoOrders = [];
  demoOrderId = 0;
  renderDemoOrders();
};

function renderDemoOrders() {
  const container = document.getElementById('demo-orders');
  if (!container) return;

  if (demoOrders.length === 0) {
    container.innerHTML = '<div class="demo-empty"><p>Aucune commande pour le moment</p><p style="font-size: 12px; color: #9ab89a; margin-top: 10px;">Cliquez sur "Ajouter une commande" pour commencer</p></div>';
  } else {
    container.innerHTML = demoOrders.map(order => {
      const statusMap = {
        'new': { badge: 'NOUVELLE', class: 'new' },
        'prep': { badge: 'EN PREP', class: 'prep' },
        'ready': { badge: 'PRÊTE', class: 'ready' }
      };
      const status = statusMap[order.status];
      const initials = order.name.split(' ').map(n => n[0]).join('').toUpperCase();
      return `<div class="demo-card ${order.status === 'ready' ? 'ready' : ''}"><div class="demo-card-header"><div class="demo-avatar">${initials}</div><div class="demo-name">${order.name}</div></div><div class="demo-content">${order.dishes}</div><div style="display: flex; justify-content: space-between; align-items: center;"><span class="demo-badge ${status.class}">${status.badge}</span><span style="font-size: 11px; color: #9ab89a;">~${order.time}min</span></div></div>`;
    }).join('');
  }
  
  const total = demoOrders.length;
  const ready = demoOrders.filter(o => o.status === 'ready').length;
  const countEl = document.getElementById('demo-count');
  const readyEl = document.getElementById('demo-ready');
  if (countEl) countEl.textContent = total - ready;
  if (readyEl) readyEl.textContent = ready;
}

window.scrollToSection = function(id) {
  const element = document.getElementById(id);
  if (element) element.scrollIntoView({ behavior: 'smooth' });
};

window.handleCTA = function() {
  const modal = document.getElementById('navigationModal');
  if (modal) modal.classList.add('active');
};

window.closeNavigationModal = function() {
  const modal = document.getElementById('navigationModal');
  if (modal) modal.classList.remove('active');
};

window.goToSection = function(id) {
  window.closeNavigationModal();
  window.scrollToSection(id);
};

document.addEventListener('DOMContentLoaded', function() {
  const hamburger = document.getElementById('hamburger');
  const navMenu = document.getElementById('navMenu');
  if (hamburger && navMenu) {
    hamburger.addEventListener('click', function() {
      navMenu.style.display = navMenu.style.display === 'flex' ? 'none' : 'flex';
    });
  }

  document.querySelectorAll('.nav-link').forEach(link => {
    link.addEventListener('click', function() {
      if (navMenu) navMenu.style.display = 'none';
    });
  });

  const modal = document.getElementById('navigationModal');
  if (modal) {
    modal.addEventListener('click', function(e) {
      if (e.target === modal) modal.classList.remove('active');
    });
  }

  document.querySelectorAll('a[href^="#"]').forEach(anchor => {
    anchor.addEventListener('click', function(e) {
      const href = this.getAttribute('href');
      if (href && href !== '#') {
        e.preventDefault();
        const target = document.querySelector(href);
        if (target) {
          target.scrollIntoView({ behavior: 'smooth' });
          if (navMenu) navMenu.style.display = 'none';
        }
      }
    });
  });

  setTimeout(() => {
    window.addDemoOrder();
    setTimeout(() => {
      window.addDemoOrder();
      setTimeout(() => {
        window.addDemoOrder();
      }, 500);
    }, 500);
  }, 300);

  const observerOptions = { threshold: 0.1, rootMargin: '0px 0px -100px 0px' };
  const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        entry.target.style.opacity = '1';
        entry.target.style.transform = 'translateY(0)';
      }
    });
  }, observerOptions);

  document.querySelectorAll('.problem-card, .feature-card, .tech-card, .advantage-item').forEach(card => {
    card.style.opacity = '0';
    card.style.transform = 'translateY(20px)';
    card.style.transition = 'opacity 0.5s ease, transform 0.5s ease';
    observer.observe(card);
  });
});

const style = document.createElement('style');
style.textContent = `@keyframes fadeInUp { from { opacity: 0; transform: translateY(30px); } to { opacity: 1; transform: translateY(0); } } @keyframes slideInRight { from { opacity: 0; transform: translateX(30px); } to { opacity: 1; transform: translateX(0); } } .hero-content { animation: fadeInUp 0.6s ease-out; } .hero-image { animation: slideInRight 0.8s ease-out 0.2s both; }`;
document.head.appendChild(style);
document.querySelectorAll('.faq-question').forEach(question => {
  question.addEventListener('click', function() {
    const faqItem = this.closest('.faq-item');
    const isActive = faqItem.classList.contains('active');
    
    document.querySelectorAll('.faq-item').forEach(item => item.classList.remove('active'));
    
    if (!isActive) {
      faqItem.classList.add('active');
    }
  });
});