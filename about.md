---
layout: page
title: Contact
---
<style>
  .contact-section {
    width: 100%;
    max-width: 20rem;
    margin-left: auto;
    margin-right: auto;
    padding-left: 2rem;
  }

  .contact-intro > * + * {
  }

  .contact-title {
    font-size: 1.875rem;
    line-height: 2.25rem;
    font-weight: 700;
  }

  .contact-description {
    color: rgb(107 114 128);
  }

  .form-group-container {
    display: grid;
    gap: 1rem;
    margin-top: 2rem;
  }

  .form-group {
    display: flex;
    flex-direction: column;
  }

  .form-label {
    margin-bottom: 0.5rem;
  }

  .form-input,
  .form-textarea {
    padding: 0.5rem;
    border: 1px solid #e5e7eb;
    display: flex;
    height: 2.5rem;
    width: 100%;
    border-radius: 0.375rem;
    font-size: 0.875rem;
    line-height: 1.25rem;
    background-color: #F5EFE0;
  }

  .form-input::placeholder,
  .form-textarea:focus-visible {
    color: #6b7280;
  }

  .form-input:focus-visible,
  .form-textarea:focus-visible {
    outline: 2px solid #2563eb;
    outline-offset: 2px;
  }

  .form-textarea {
    min-height: 120px;
  }

  .form-submit {
    width: 100%;
    margin-top: 1.2rem;
    background-color: #F5EFE0;
    color: #000;
    padding: 13px 5px;
    border-radius: 0.375rem;
  }
</style>




<div class="container">  
  <div class="column"> 
    <br/>
    <p>Want to say hello or got a problem that I can help you with? Please use the attached form. I am also on <a href='https://www.linkedin.com/in/sagrdl/' target='_blank'>linkedin</a> and <a href='https://github.com/sagrd' target='_blank'>github</a></p>
    <p>Alternatively, you can reach out to me at hiesagar {at} gmail {dot} com </p>
  </div> 

  <div class="column">
    <section class="contact-section">
    <form class="contact-form" action="https://api.web3forms.com/submit" method="POST">
      <input type="hidden" name="access_key" value="80cf630d-71b0-49ba-b8bc-f316231cbaa5" />
      <input type="hidden" name="subject" value="New Contact Form Submission from Web3Forms" />
      <input type="hidden" name="from_name" value="My Website" />
      <div class="form-group-container">
        <div class="form-group">
          <label for="name" class="form-label">Name</label>
          <input id="name" name="name" class="form-input" placeholder="Your name" type="text" />
        </div>
        <div class="form-group">
          <label for="email" class="form-label">Email</label>
          <input id="email" name="email" class="form-input" placeholder="Your email" type="email" />
        </div>
        <div class="form-group">
          <label for="message" class="form-label">Message</label>
          <textarea class="form-textarea" id="message" name="message" placeholder="Your message"></textarea>
        </div>
      </div>
      <button class="form-submit" type="submit">Send Message</button>
    </form>
  </section>
  </div> 
</div>
