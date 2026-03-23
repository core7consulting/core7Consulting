# GitHub Copilot Context for Core7 Consulting

## 1. Project Overview

- Static marketing website for Core7 Consulting.
- French-language IT consulting and digital transformation services showcase.
- Target users: potential clients and partners seeking IT transformation, DevOps, security, Big Data, and strategy support.
- Core purpose: brand positioning, service presentation, and contact capture (email/WhatsApp link).

## 2. Tech Stack

- Languages:
  - HTML
  - CSS (embedded in `<style>` inside the HTML)
- Frameworks:
  - None (pure static front-end)
- Libraries:
  - Google Fonts (Inter, Montserrat)
  - No JavaScript libraries (no JS present)

## 3. Architecture

- This is a monolithic static website (single page application-like structure, not SPA with routing).
- Folder structure:
  - `webSite.html` (single entry point)
  - `images/` (static assets for icons/logo)
- Key modules (sections in the page):
  - Header/navigation
  - Hero section
  - Strategy (mission/vision/values)
  - Services domain grid
  - Expertises tech tag area
  - Contact section with email & WhatsApp CTAs
  - Footer
- Data flow: simple static content delivery; user interaction is navigation to anchors and external contact links.

## 4. Key Features

- Sticky header with internal anchor links.
- Responsive layout for mobile (`@media max-width: 768px`, hides nav, condenses layout).
- Service presentation cards.
- Expertise tag cloud.
- Contact buttons for email and WhatsApp.
- Visual identity with consistent CSS variable-driven theme.

## 5. Important Files

- Entry point: `webSite.html`
- Config files: none
- Core logic: only inline CSS and markup in `webSite.html`

## 6. Coding Conventions

- Naming patterns:
  - BEM-like CSS class names (e.g., `.service-card`, `.contact-section`, `.hero`).
  - French text content in markup with semantic structure.
- Code style:
  - Embedded CSS in head with custom properties (CSS variables).
  - Section-based styles with consistent indentation.
  - Use of modern CSS features: grid, flexbox, variables.
- Patterns:
  - Single-page anchors for navigation.
  - Reuse of component classes for layout blocks.

## 7. Improvement Suggestions

- Performance:
  - Extract CSS to an external file for better caching and maintainability.
  - Add responsive image formats and lazy-loading for `images/` assets.
- Structure:
  - Split into `index.html` with dedicated CSS/JS directories for more scalable dev structure.
  - Add a `README.md` to document how to deploy.
- Security:
  - Add `rel="noopener noreferrer"` to external WhatsApp link when using `target="_blank"`.
  - Ensure no personal contact details are hardcoded in source for public repo (use environment or obfuscation if required).
- Scalability:
  - Add a small JS component for form-based lead capture (instead of direct mailto) to support analytics or CRM integration.
  - Consider integrating with a CMS or static site generator if content updates become frequent.

> Assumption: The repository contains only the static website files visible (`webSite.html`, `images/`) and no backend code. If additional sources exist outside this folder, they were not present in the inspection boundary.

## Contact System

- Formulaire de contact entièrement localisé en français dans `webSite.html`.
- Champs utilisateur en français : Prénom, Nom, Email, Numéro de téléphone, Type de demande, Objet, Message.
- Validation côté client en français : champ obligatoire, format email, messages d'erreur inline.
- Intégration EmailJS via CDN dans JavaScript vanilla.
- Variables envoyées dans EmailJS : first_name, last_name, email, phone, request_type, subject, message.
- Flux de données : formulaire -> validation JS -> emailjs.send() -> EmailJS envoie l'email ciblé.
- UI de statut : état de chargement, message de succès, message d'erreur, réinitialisation du formulaire après succès.

### EmailJS template (texte en français)

- Nom complet: {{first_name}} {{last_name}}
- Email: {{email}}
- Téléphone: {{phone}}

- Type de demande: {{request_type}}
- Objet: {{subject}}

- Message:
  {{message}}

### EmailJS configuration instructions

- Provide `EMAILJS_PUBLIC_KEY` in JS constant `EMAILJS_PUBLIC_KEY` (needs from EmailJS user dashboard).
- Provide `EMAILJS_SERVICE_ID` and `EMAILJS_TEMPLATE_ID` in JS constants `EMAILJS_SERVICE_ID` and `EMAILJS_TEMPLATE_ID`.
- Replace placeholder values with real IDs or use environment injection techniques at build/time (for GitHub pages static site, keep public key only and assume other keys are non-secret).

### Future improvements

- Persist leads in database using serverless function / API endpoint.
- Connect form to CRM (HubSpot, Salesforce, Pipedrive).
- Add spam protection (reCAPTCHA, honeypot field, rate limiting) and advanced validation.
