# Contact Form Setup Options

## Option 1: EmailJS (Recommended - Free & Easy)

### Steps:
1. Go to https://www.emailjs.com/
2. Create a free account
3. Add an email service (Gmail, Outlook, etc.)
4. Create an email template
5. Get your Service ID, Template ID, and Public Key
6. Update your JavaScript code

### Code to add to script.js:
```javascript
// Replace the current contact form handler with this:
const contactForm = document.getElementById('contact-form');
if (contactForm) {
    contactForm.addEventListener('submit', function(e) {
        e.preventDefault();
        
        // Get form data
        const formData = new FormData(this);
        const templateParams = {
            from_name: formData.get('name'),
            from_email: formData.get('email'),
            subject: formData.get('subject'),
            message: formData.get('message')
        };
        
        // Send email using EmailJS
        emailjs.send('YOUR_SERVICE_ID', 'YOUR_TEMPLATE_ID', templateParams, 'YOUR_PUBLIC_KEY')
            .then(function(response) {
                showNotification('Message sent successfully! I\'ll get back to you soon.', 'success');
                contactForm.reset();
            }, function(error) {
                showNotification('Failed to send message. Please try again.', 'error');
                console.error('EmailJS error:', error);
            });
    });
}
```

### Add to HTML head section:
```html
<script src="https://cdn.jsdelivr.net/npm/@emailjs/browser@3/dist/email.min.js"></script>
<script>
    emailjs.init('YOUR_PUBLIC_KEY');
</script>
```

## Option 2: Formspree (Simple Alternative)

### Steps:
1. Go to https://formspree.io/
2. Create account and get form endpoint
3. Update your form action

### Update your form in index.html:
```html
<form id="contact-form" action="https://formspree.io/f/YOUR_FORM_ID" method="POST">
    <input type="hidden" name="_subject" value="New Portfolio Contact">
    <input type="hidden" name="_next" value="thank-you.html">
    <!-- rest of your form fields stay the same -->
</form>
```

## Option 3: Netlify Forms (If hosting on Netlify)

### Add to your form:
```html
<form id="contact-form" name="contact" method="POST" data-netlify="true">
    <input type="hidden" name="form-name" value="contact">
    <!-- rest of your form fields -->
</form>
```

## Option 4: Simple Mailto Link

### Replace form with email link:
```html
<a href="mailto:your-email@example.com?subject=Portfolio Contact&body=Hi Sneha," class="btn btn-primary">
    Send Email
</a>
```

## Option 5: Backend Server (Advanced)

Create a backend API using:
- Node.js + Express
- PHP
- Python + Flask/Django
- Any other backend technology