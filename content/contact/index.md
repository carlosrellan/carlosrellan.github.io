---
title: Contact
summary: Contact form
hide_date: true
reading_time: false
share: false
---

Please use this form for academic enquiries. For course-related questions and office hours (*tutorías*), see my <a href="https://www.ugr.es/personal/carlos-cristian-rodriguez-rellan" target="_blank" rel="noopener">staff page at the University of Granada</a>.

<style>
  .cform { max-width: 40rem; margin-top: 1.5rem; }
  .cform label { display: block; font-weight: 600; margin: 1rem 0 0.35rem; }
  .cform input[type="text"], .cform input[type="email"], .cform textarea {
    width: 100%; box-sizing: border-box; border: 1px solid rgba(128,128,128,0.5); border-radius: 0.375rem;
    padding: 0.55rem 0.75rem; background: transparent; color: inherit; font: inherit;
  }
  .cform textarea { min-height: 10rem; resize: vertical; }
  .cform .cform__consent { display: flex; gap: 0.6rem; align-items: flex-start; font-weight: 400; }
  .cform .cform__consent input { margin-top: 0.35rem; }
  .cform button {
    margin-top: 1.25rem; border: 1px solid currentColor; border-radius: 0.375rem; padding: 0.55rem 1.4rem;
    background: transparent; color: inherit; font: inherit; font-weight: 600; cursor: pointer;
  }
  .cform button[disabled] { opacity: 0.5; cursor: wait; }
  .cform input:focus-visible, .cform textarea:focus-visible, .cform button:focus-visible { outline: 2px solid currentColor; outline-offset: 2px; }
  .cform__hp { position: absolute !important; left: -10000px !important; width: 1px; height: 1px; overflow: hidden; }
  .cform__status { margin-top: 1rem; font-weight: 600; }
  .cform__privacy { font-size: 0.85em; opacity: 0.85; margin-top: 2rem; }
</style>
<form id="contact-form" class="cform" action="https://formspree.io/f/maenvzjy" method="POST" accept-charset="UTF-8">
  <input type="hidden" name="_subject" value="New message from carlosrellan.github.io">
  <label for="cf-name">Name</label>
  <input id="cf-name" type="text" name="name" autocomplete="name" required maxlength="120">
  <label for="cf-email">Email</label>
  <input id="cf-email" type="email" name="email" autocomplete="email" required maxlength="200">
  <label for="cf-subject">Subject</label>
  <input id="cf-subject" type="text" name="subject" required maxlength="200">
  <label for="cf-message">Message</label>
  <textarea id="cf-message" name="message" required minlength="10" maxlength="5000"></textarea>
  <div class="cform__hp" aria-hidden="true">
    <label for="cf-gotcha">Leave this field empty</label>
    <input id="cf-gotcha" type="text" name="_gotcha" tabindex="-1" autocomplete="off">
  </div>
  <label class="cform__consent" for="cf-consent">
    <input id="cf-consent" type="checkbox" name="consent" value="yes" required>
    <span>I have read the privacy notice below and consent to the processing of my data in order to receive a reply.</span>
  </label>
  <button type="submit">Send message</button>
  <p id="cf-status" class="cform__status" role="status" aria-live="polite"></p>
</form>
<div class="cform__privacy">
  <p><strong>Privacy notice.</strong> Controller: Carlos Rodríguez Rellán. Purpose: to reply to your enquiry; the data you provide (name, email address, subject and message) will not be used for any other purpose or shared with third parties beyond the service provider mentioned below. Legal basis: your consent (Art. 6(1)(a) GDPR), which you may withdraw at any time. Processor: the form is handled by Formspree (<a href="https://formspree.io" target="_blank" rel="noopener">formspree.io</a>), which hosts data on Amazon Web Services servers in the United States under Standard Contractual Clauses and keeps submissions in its archive for up to 30 days. Your message is kept in my mailbox only for as long as necessary to deal with your enquiry. You may exercise your rights of access, rectification, erasure, restriction, portability and objection by writing to me, and you may lodge a complaint with the Spanish Data Protection Agency (<a href="https://www.aepd.es" target="_blank" rel="noopener">AEPD</a>).</p>
</div>
<script>
(function () {
  var form = document.getElementById('contact-form');
  if (!form || !window.fetch) return;
  var status = document.getElementById('cf-status');
  var button = form.querySelector('button[type="submit"]');
  var loadedAt = Date.now();
  form.addEventListener('submit', function (ev) {
    ev.preventDefault();
    if (form.elements['_gotcha'].value !== '') return;
    if (Date.now() - loadedAt < 3000) {
      status.textContent = 'Please take a moment to review your message and try again.';
      return;
    }
    button.disabled = true;
    status.textContent = 'Sending…';
    fetch(form.action, { method: 'POST', body: new FormData(form), headers: { 'Accept': 'application/json' } })
      .then(function (r) {
        if (r.ok) {
          form.reset();
          status.textContent = 'Thank you. Your message has been sent.';
        } else {
          status.textContent = 'Sorry, the message could not be sent. Please try again later.';
        }
      })
      .catch(function () {
        status.textContent = 'Sorry, the message could not be sent. Please check your connection and try again.';
      })
      .then(function () { button.disabled = false; });
  });
})();
</script>
