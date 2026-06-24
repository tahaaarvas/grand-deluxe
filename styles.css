// Slider + reveal + mobile nav + SSS accordion + lightbox + WhatsApp helper

document.addEventListener('DOMContentLoaded', () => {
  // Footer year
  const yearEl = document.getElementById('year');
  if (yearEl) yearEl.textContent = new Date().getFullYear();

  // -------------------- Overlay fade out --------------------
  function triggerOverlayFade() {
    const overlay = document.querySelector('.page-overlay');
    if (!overlay) return;
    overlay.classList.add('fade-out');
    const onAnim = () => {
      overlay.remove();
      overlay.removeEventListener('animationend', onAnim);
    };
    overlay.addEventListener('animationend', onAnim);
    setTimeout(() => {
      if (document.body.contains(overlay)) overlay.remove();
    }, 1500);
  }
  window.addEventListener('load', triggerOverlayFade);
  setTimeout(triggerOverlayFade, 900);

  // -------------------- WhatsApp links (placeholders) --------------------
  const phoneDisplayEl = document.querySelector('[data-whatsapp-display]');
  const waTextEl = document.querySelector('[data-whatsapp-cta]');
  const waAnchor = document.querySelector('[data-whatsapp-link]');
  const phones = ['905336617010', '905052245390'];
  const placeholderPrimaryNumber = phones[0];
  const placeholderSecondaryNumber = phones[1];

  // WhatsApp CTA'lar: data-whatsapp-cta (primary) / data-whatsapp-cta-2 (secondary)
  const waCtaPrimary = document.querySelector('[data-whatsapp-cta]');
  const waCtaSecondary = document.querySelector('[data-whatsapp-cta-2]');

  const waDefaultMessage = encodeURIComponent('Merhaba Grand Deluxe! Tarih ve paket bilgisi almak istiyorum.');



  const buildWhatsappUrl = (phoneNumber, message) => {
    return `https://wa.me/${phoneNumber}?text=${message}`;
  };

  if (waAnchor) {
    waAnchor.href = buildWhatsappUrl(placeholderPrimaryNumber, waDefaultMessage);

    waAnchor.target = '_blank';
    waAnchor.rel = 'noopener noreferrer';
  }
  if (waTextEl) {
    waTextEl.href = buildWhatsappUrl(placeholderPrimaryNumber, waDefaultMessage);

    waTextEl.target = '_blank';
    waTextEl.rel = 'noopener noreferrer';
  }

  // CTA'ları tek mesajla güncelle (primary + secondary)
  if (waCtaPrimary) {
    waCtaPrimary.href = buildWhatsappUrl(placeholderPrimaryNumber, waDefaultMessage);
    waCtaPrimary.target = '_blank';
    waCtaPrimary.rel = 'noopener noreferrer';
  }
  if (waCtaSecondary) {
    waCtaSecondary.href = buildWhatsappUrl(placeholderSecondaryNumber, waDefaultMessage);
    waCtaSecondary.target = '_blank';
    waCtaSecondary.rel = 'noopener noreferrer';
  }


  // Make contact chips focusable even if href was '#'
  if (phoneDisplayEl) {
    phoneDisplayEl.addEventListener('click', (e) => {
      // Do nothing; real link is in WhatsApp chip
      e.preventDefault();
    });
  }

  // -------------------- Mobile nav --------------------
  const navToggle = document.querySelector('.nav-toggle');
  const nav = document.querySelector('.nav ul');
  if (navToggle && nav) {
    navToggle.addEventListener('click', () => {
      const isOpen = nav.classList.toggle('open');
      navToggle.setAttribute('aria-expanded', String(isOpen));
    });

    // Close menu on link click
    nav.querySelectorAll('a').forEach(a => {
      a.addEventListener('click', () => {
        nav.classList.remove('open');
        navToggle.setAttribute('aria-expanded', 'false');
      });
    });
  }

  // -------------------- Slider --------------------
  const slidesWrap = document.querySelector('.slides');
  const slides = document.querySelectorAll('.slide');
  const prev = document.querySelector('.prev');
  const next = document.querySelector('.next');
  const indicators = document.querySelector('.indicators');
  const sliderEl = document.querySelector('.slider');

  let index = 0;
  let timer = null;

  if (slidesWrap && slides.length > 0 && indicators) {
    // build indicators
    slides.forEach((s, i) => {
      const btn = document.createElement('button');
      btn.type = 'button';
      btn.setAttribute('aria-label', `slayt ${i + 1}`);
      btn.addEventListener('click', () => goTo(i));
      if (i === 0) btn.classList.add('active');
      indicators.appendChild(btn);
    });

    update();
    resetTimer();

    function update() {
      slidesWrap.style.transform = `translateX(${-index * 100}%)`;
      indicators.querySelectorAll('button').forEach((b, i) => b.classList.toggle('active', i === index));

      slides.forEach((s, i) => {
        const content = s.querySelector('.slide-content');
        if (!content) return;
        if (i === index) {
          setTimeout(() => content.classList.add('active'), 80);
        } else {
          content.classList.remove('active');
        }
      });
    }

    function goTo(i) {
      index = (i + slides.length) % slides.length;
      update();
      resetTimer();
    }

    function nextSlide() {
      goTo(index + 1);
    }

    function prevSlide() {
      goTo(index - 1);
    }

    if (next) next.addEventListener('click', nextSlide);
    if (prev) prev.addEventListener('click', prevSlide);

    function resetTimer() {
      clearInterval(timer);
      timer = setInterval(nextSlide, 5200);
    }

    if (sliderEl) {
      sliderEl.addEventListener('mouseenter', () => clearInterval(timer));
      sliderEl.addEventListener('mouseleave', () => resetTimer());
    }

    // touch swipe
    let startX = 0;
    let deltaX = 0;
    slidesWrap.addEventListener('touchstart', (e) => {
      startX = e.touches[0].clientX;
      clearInterval(timer);
    }, { passive: true });
    slidesWrap.addEventListener('touchmove', (e) => {
      deltaX = e.touches[0].clientX - startX;
    }, { passive: true });
    slidesWrap.addEventListener('touchend', () => {
      if (Math.abs(deltaX) > 50) {
        if (deltaX < 0) nextSlide(); else prevSlide();
      }
      deltaX = 0;
      resetTimer();
    });
  }

  // -------------------- Reveal on scroll --------------------
  const revealEls = Array.from(document.querySelectorAll('.reveal'));
  const io = new IntersectionObserver((entries) => {
    entries.forEach(e => {
      if (e.isIntersecting) {
        e.target.classList.add('in-view');
        io.unobserve(e.target);
      }
    });
  }, { threshold: 0.12 });

  revealEls.forEach((el, i) => {
    el.style.transitionDelay = `${i * 70}ms`;
    io.observe(el);
  });

  // -------------------- Accordion (SSS) --------------------
  const accordion = document.getElementById('accordion');
  if (accordion) {
    accordion.querySelectorAll('.acc-btn').forEach(btn => {
      btn.addEventListener('click', () => {
        const item = btn.closest('.acc-item');
        const expanded = btn.getAttribute('aria-expanded') === 'true';

        // close others
        accordion.querySelectorAll('.acc-btn').forEach(other => {
          if (other === btn) return;
          other.setAttribute('aria-expanded', 'false');
          const otherPanel = other.closest('.acc-item')?.querySelector('.acc-panel');
          if (otherPanel) otherPanel.style.maxHeight = '0px';
          const otherIcon = other.querySelector('.acc-icon');
          if (otherIcon) otherIcon.textContent = '+';
        });

        // toggle this
        btn.setAttribute('aria-expanded', String(!expanded));
        const panel = item.querySelector('.acc-panel');
        const icon = btn.querySelector('.acc-icon');
        if (panel) {
          if (expanded) {
            panel.style.maxHeight = '0px';
            if (icon) icon.textContent = '+';
          } else {
            panel.style.maxHeight = panel.scrollHeight + 'px';
            if (icon) icon.textContent = '–';
          }
        }
      });
    });

    // initialize open ones
    accordion.querySelectorAll('.acc-item').forEach(item => {
      const btn = item.querySelector('.acc-btn');
      const expanded = btn?.getAttribute('aria-expanded') === 'true';
      const panel = item.querySelector('.acc-panel');
      if (expanded && panel) {
        panel.style.maxHeight = panel.scrollHeight + 'px';
        const icon = btn.querySelector('.acc-icon');
        if (icon) icon.textContent = '–';
      } else if (panel) {
        panel.style.maxHeight = '0px';
      }
    });
  }

  // -------------------- Lightbox --------------------
  const lightbox = document.querySelector('.lightbox');
  const lightboxImg = document.querySelector('.lightbox-img');
  const lightboxClose = document.querySelector('.lightbox-close');
  const galleryGrid = document.getElementById('galleryGrid');

  function openLightbox(src) {
    if (!lightbox || !lightboxImg) return;
    lightboxImg.src = src;
    lightbox.classList.add('open');
    lightbox.setAttribute('aria-hidden', 'false');
    document.body.style.overflow = 'hidden';
    lightboxClose?.focus();
  }

  function closeLightbox() {
    if (!lightbox) return;
    lightbox.classList.remove('open');
    lightbox.setAttribute('aria-hidden', 'true');
    document.body.style.overflow = '';
  }

  if (galleryGrid) {
    galleryGrid.querySelectorAll('.grid-item').forEach(btn => {
      btn.addEventListener('click', (e) => {
        // Link olsa bile lightbox aç
        e.preventDefault();
        const src = btn.getAttribute('data-full') || btn.getAttribute('href');
        if (src) openLightbox(src);
      });
    });
  }

  if (lightboxClose) lightboxClose.addEventListener('click', closeLightbox);
  if (lightbox) {
    lightbox.addEventListener('click', (e) => {
      if (e.target === lightbox) closeLightbox();
    });
    document.addEventListener('keydown', (e) => {
      if (e.key === 'Escape') closeLightbox();
    });
  }

  // -------------------- Form submit demo + optional WhatsApp --------------------
  const form = document.querySelector('.contact-form');
  if (form) {
    form.addEventListener('submit', (e) => {
      e.preventDefault();

      const fd = new FormData(form);
      const isim = fd.get('isim') || '';
      const email = fd.get('email') || '';
      const telefon = fd.get('telefon') || '';
      const tarih = fd.get('tarih') || '';
      const mesaj = fd.get('mesaj') || '';

      // Demo: WhatsApp'a yönlendirme
      const message = encodeURIComponent(
        `Merhaba Grand Deluxe!\n\nİsim: ${isim}\nEmail: ${email}\nTelefon: ${telefon}\nTarih: ${tarih}\n\nMesaj: ${mesaj}`
      );
      const url = `https://wa.me/${placeholderPrimaryNumber}?text=${message}`;


      alert('Demo: Form alındı. WhatsApp’tan mesaj taslağı açılacak.');
      window.open(url, '_blank', 'noopener,noreferrer');
    });
  }
});

