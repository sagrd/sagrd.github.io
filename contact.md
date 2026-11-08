---
layout: page
title: Get in touch
---

<div class="container">
  <div class="column">
    <ul>
      <li>Want to say hello or got a problem that I can help you with? Please use the form alongside. Alternatively, you can reach out to me at <a href="javascript:location='mailto:\u0068\u0069\u0065\u0073\u0061\u0067\u0061\u0072\u0040\u0067\u006d\u0061\u0069\u006c\u002e\u0063\u006f\u006d';void 0"><script type="text/javascript">document.write('\u0068\u0069\u0065\u0073\u0061\u0067\u0061\u0072\u0040\u0067\u006d\u0061\u0069\u006c\u002e\u0063\u006f\u006d')</script></a></li>
      <li>I am also on <a href="https://www.linkedin.com/in/sagrdl/">linkedin</a> and <a href="https://github.com/sagrd">github</a></li>
    </ul>
  </div>
  <div class="column">
    <form id="contact-form" action="https://api.web3forms.com/submit" method="POST">
      <input type="hidden" name="access_key" value="80cf630d-71b0-49ba-b8bc-f316231cbaa5">
      <input type="checkbox" name="botcheck" style="display: none;">
      <input type="text" name="name" placeholder="Name" required>
      <input type="email" name="email" placeholder="Email" required>
      <textarea name="message" placeholder="Message" rows="5" required></textarea>
      <button type="submit" id="submit-btn">Submit Form</button>
      <div id="form-result" class="form-result" style="display: none;"></div>
    </form>
  </div>
</div>

<script>
  const form = document.getElementById('contact-form');
  const result = document.getElementById('form-result');
  const submitBtn = document.getElementById('submit-btn');

  if (form) {
    form.addEventListener('submit', function(e) {
      e.preventDefault();
      submitBtn.disabled = true;
      submitBtn.innerText = 'Sending...';
      result.style.display = 'none';
      result.className = 'form-result';

      const formData = new FormData(form);
      const object = Object.fromEntries(formData);
      const json = JSON.stringify(object);

      fetch('https://api.web3forms.com/submit', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
          'Accept': 'application/json'
        },
        body: json
      })
      .then(async (response) => {
        const data = await response.json();
        if (response.status === 200) {
          result.innerText = 'Thank you! Your message has been sent successfully.';
          result.className = 'form-result success';
          result.style.display = 'block';
          form.reset();
        } else {
          result.innerText = data.message || 'Something went wrong. Please try again.';
          result.className = 'form-result error';
          result.style.display = 'block';
        }
      })
      .catch((error) => {
        result.innerText = 'Something went wrong. Please try again or reach out via email.';
        result.className = 'form-result error';
        result.style.display = 'block';
      })
      .finally(() => {
        submitBtn.disabled = false;
        submitBtn.innerText = 'Submit Form';
      });
    });
  }
</script>


