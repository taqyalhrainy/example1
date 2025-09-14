<!DOCTYPE html>
<html lang="en" dir="ltr">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Animal Welfare — Your donation saves lives</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <style>
    :root{
      --brand-primary:#16a34a; /* green-600 */
      --brand-secondary:#2563eb; /* blue-600 */
      --brand-accent:#f59e0b;   /* amber-500 */
    }
    .btn-primary{background:var(--brand-primary);color:#fff}
    .btn-primary:hover{filter:brightness(0.95)}
    .glass{backdrop-filter:blur(10px);background:rgba(255,255,255,.7)}
    .blob{filter:blur(50px);opacity:.5;position:absolute;border-radius:9999px;pointer-events:none;z-index:-1}
    .fade-up{opacity:0;transform:translateY(10px);transition:opacity .6s ease, transform .6s ease}
    .fade-up.in{opacity:1;transform:none}
    .rtl-shadow{box-shadow:0 10px 30px rgba(0,0,0,.08)}
    .menu-link:hover{color:#166534}
    .modal-enter{animation:pop .35s cubic-bezier(.2,.8,.2,1)}
    @keyframes pop{0%{opacity:0;transform:translateY(20px)}100%{opacity:1;transform:none}}
    .preset-btn{transition:background-color .2s,color .2s}
    .preset-btn:hover{background:#f9fafb}
    .preset-btn.selected{background:#16a34a;color:#fff;border-color:#16a34a}
    .preset-btn.selected:hover{background:#15803d;color:#fff}
    /* Mobile usability helpers */
    .long-id{word-break:break-all;overflow-wrap:anywhere}
    .scroll-h{overflow-x:auto;-webkit-overflow-scrolling:touch}
    /* Hide language toggle since site is English-only */
    #langToggle{display:none}
  </style>
</head>
<body class="min-h-screen bg-white text-gray-900">
  <!-- ============== CONFIG ============== -->
  <script>
    const siteConfig = {
      clinicName: "Animal Welfare Clinic",
      tagline: "Your donation today saves a life tomorrow",
      priceLocale: "en-US",
      currency: "USD",
      brand: {
        logo: "https://images.unsplash.com/photo-1561037404-61cd46aa615b?w=256&q=80&auto=format&fit=crop",
        primary: getComputedStyle(document.documentElement).getPropertyValue('--brand-primary').trim(),
        secondary: getComputedStyle(document.documentElement).getPropertyValue('--brand-secondary').trim(),
        accent: getComputedStyle(document.documentElement).getPropertyValue('--brand-accent').trim(),
      },
      contact: {
        phone: "+962795764229",
        email: "takee12345678900@gmail.com",
        address: "Amman, Jordan",
        address_en: "Amman, Jordan",
        instagram: "https://instagram.com/its_taqi2003",
        facebook: "#",
        youtube: "#"
      },
      payments: {
        paypal: "https://paypal.me/Taqihr",
        stripe: "#",
        bankIban: "JO69UBSI1010000010160371415501"
      },
      hero: {
        images:[
          "https://images.unsplash.com/photo-1574158622682-e40e69881006?q=80&w=1600&auto=format&fit=crop",
          "https://images.unsplash.com/photo-1534361960057-19889db9621e?q=80&w=1600&auto=format&fit=crop"
        ]
      },
      tiers:[
        {title:"Emergency Vaccine",amount:5,desc:"Covers a vaccine dose or basic medicine."},
        {title:"Meal & Treatment",amount:15,desc:"Provides a nutritious meal with simple treatment."},
        {title:"Life-saving Surgery",amount:50,desc:"A meaningful share in a life-saving operation."}
      ],
      money(v){try{return new Intl.NumberFormat(this.priceLocale,{style:'currency',currency:this.currency,maximumFractionDigits:0}).format(v)}catch(e){return "$"+v}}
    };
  </script>

  <!-- ============== I18N (English only) ============== -->
  <script>
    const i18n = {
      en: {
        dir: 'ltr', lang: 'en',
        clinicName: 'Animal Welfare Clinic',
        tagline: 'Your donation today saves a life tomorrow',
        menu: ['About','Donate','Contact'],
        heroP: 'Every donation—no matter the size—gives a new chance of life to a cat or dog awaiting treatment and care.',
        ctaDonate: 'Donate Now',
        ctaLearn: 'Learn more',
        features: ['High transparency','Secure payments','Immediate impact'],
        quickTitle: '❤️ Quick Donate',
        quickBtn: 'Pay now',
        quickNote: 'You will be redirected to a secure payment gateway.',
        quickAmountLabel: 'Amount',
        aboutH2: 'Why this site?',
        aboutP: 'Many clinics cover the treatment costs of animals left at their doors. This site makes your support easy and direct via secure gateways and transparent reports.',
        aboutLis: [
          '✔️ Instant forwarding to the clinic’s links (Visa/Stripe/Bank).',
          '✔️ Customizable logo, colors, and content in minutes.',
          '✔️ Arabic support (RTL) and a smooth mobile experience.'
        ],
        donateH2: 'Choose your contribution',
        donateP: 'Flexible donation plans—you can also set a custom amount.',
        customH: 'Enter a custom amount',
        amountLabel: 'Amount',
        customPay: 'Pay now',
        galleryH2: 'Photos from our cases',
        contactH2: 'Contact us',
        contactP: 'We are happy to answer your questions about donations or volunteering.',
        instagram: 'Instagram',
        footerRights: 'All rights reserved',
        footerBadge: '🛡️ Independent donation platform — payment links go directly to the clinic',
        modalTitle: '❤️ Complete Donation',
        modalChoose: 'Choose a method: Visa, transfer via CliQ, or bank transfer (IBAN).',
        modalAgree: 'I agree to the terms and privacy policy.',
        more: 'More',
        payPaypal: 'Pay via Visa ↗',
        payCliq: 'Transfer via CliQ',
        payIban: 'Bank transfer (IBAN)',
        cliqTitle: 'Transfer via CliQ',
        cliqP: 'Open your banking app → CliQ → Send → Enter the following identifier:',
        copy: 'Copy', copied: 'Copied ✔',
        cliqCopyFallback: 'Copy failed. Please copy the identifier manually: TAQY123',
        ibanTitle: 'Bank transfer (IBAN)',
        ibanP: 'Copy the IBAN, then transfer from your banking app:',
        ibanCopyFallback: 'Copy failed. Please copy the IBAN manually.',
        alternative: 'Alternative: Bank transfer to IBAN:',
        tierBtn: 'Donate this amount',
      }
    };
    let currentLang = 'en';
  </script>

  <!-- =================== NAVBAR =================== -->
  <header class="sticky top-0 z-40 border-b glass">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-16 flex items-center justify-between">
      <div class="flex items-center gap-3">
        <img id="logo" class="h-9 w-9 rounded-xl object-cover rtl-shadow" alt="logo">
        <span id="brandName" class="font-extrabold tracking-tight text-lg sm:text-xl">Animal Welfare Clinic</span>
      </div>
      <nav class="hidden md:flex items-center gap-6 text-sm font-medium">
        <a href="#about" class="menu-link transition">About</a>
        <a href="#donate" class="menu-link transition">Donate</a>
        <a href="#contact" class="menu-link transition">Contact</a>
      </nav>
      <div class="flex items-center gap-2">
        <button id="langToggle" class="px-3 py-2 rounded-2xl border text-sm font-semibold">EN</button>
        <button id="donateTop" class="btn-primary px-4 py-2 rounded-2xl rtl-shadow text-sm font-semibold">Donate Now</button>
      </div>
    </div>
  </header>

  <!-- =================== MAIN (Home) =================== -->
  <div id="pageHome">
    <!-- HERO -->
    <section class="relative overflow-hidden">
      <div class="absolute inset-0 -z-10">
        <img id="heroImg" class="w-full h-full object-cover opacity-30" alt="hero" />
        <div class="blob -top-24 -left-24 h-96 w-96 bg-green-300 absolute animate-pulse"></div>
        <div class="blob -bottom-24 -right-24 h-96 w-96 bg-amber-300 absolute animate-[pulse_12s_ease-in-out_infinite]"></div>
      </div>
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-12 sm:py-20">
        <div class="grid lg:grid-cols-2 gap-8 sm:gap-10 items-center">
          <div>
            <h1 id="tagline" class="fade-up text-2xl sm:text-4xl md:text-5xl font-extrabold leading-tight">Your donation today saves a life tomorrow</h1>
            <p class="fade-up mt-3 sm:mt-4 text-base sm:text-lg text-gray-600" id="heroP">Every donation—no matter the size—gives a new chance of life to a cat or dog awaiting treatment and care.</p>
            <div class="fade-up mt-5 sm:mt-6 flex flex-wrap gap-3">
              <button id="donateHero" class="btn-primary px-5 py-3 rounded-2xl text-base font-semibold flex items-center gap-2">
                <span id="donateHeroTxt">Donate Now</span>
                <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7"/></svg>
              </button>
              <a id="learnMoreLink" href="#about" class="inline-flex items-center gap-2 font-semibold hover:opacity-80">Learn more</a>
            </div>
            <div class="fade-up flex items-center gap-4 sm:gap-6 text-sm text-gray-600 pt-5 sm:pt-6" id="featuresRow">
              <div class="flex items-center gap-2">🔒 High transparency</div>
              <div class="flex items-center gap-2">💳 Secure payments</div>
              <div class="flex items-center gap-2">🐾 Immediate impact</div>
            </div>
          </div>
          <div>
            <div class="fade-up max-w-md mx-auto bg-white rounded-2xl border rtl-shadow">
              <div id="quickTitle" class="p-4 border-b font-bold flex items-center gap-2">❤️ Quick Donate</div>
              <div class="p-4 space-y-4">
                <!-- Mobile: 2 columns, from sm: 4 columns -->
                <div class="grid grid-cols-2 sm:grid-cols-4 gap-2" id="presetBtns"></div>
                <div>
                  <label class="text-sm" id="quickAmountLabel">Amount (<span id="currencyQuick"></span>)</label>
                  <input id="quickCustomAmount" inputmode="decimal" type="number" min="1" class="mt-1 w-full rounded-xl border px-3 py-3" />
                </div>
                <button id="donateQuick" class="btn-primary w-full rounded-xl py-3 font-semibold">Pay now</button>
                <p id="quickNote" class="text-xs text-gray-500">You will be redirected to a secure payment gateway.</p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- ABOUT -->
    <section id="about" class="py-12 sm:py-16">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 grid lg:grid-cols-2 gap-8 sm:gap-10 items-center">
        <div class="order-2 lg:order-1">
          <h2 class="fade-up text-2xl sm:text-3xl font-extrabold" id="aboutH2">Why this site?</h2>
          <p class="fade-up text-gray-600 mt-3 sm:mt-4 leading-relaxed" id="aboutP">
            Many clinics cover the treatment costs of animals left at their doors. This site makes your support easy and direct via secure gateways and transparent reports.
          </p>
          <ul class="fade-up mt-5 sm:mt-6 space-y-3 text-gray-700" id="aboutList">
            <li>✔️ Instant forwarding to the clinic’s links (Visa/Stripe/Bank).</li>
            <li>✔️ Customizable logo, colors, and content in minutes.</li>
            <li>✔️ Arabic support (RTL) and a smooth mobile experience.</li>
          </ul>
        </div>
        <div class="order-1 lg:order-2 relative">
          <img id="aboutImg" class="fade-up rounded-2xl rtl-shadow w-full h-auto" alt="about" />
          <div class="blob h-32 w-32 bg-blue-200 absolute -bottom-6 -left-6 animate-pulse"></div>
        </div>
      </div>
    </section>

    <!-- DONATE -->
    <section id="donate" class="py-12 sm:py-16">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="text-center mb-8 sm:mb-10">
          <h2 id="donateH2" class="fade-up text-2xl sm:text-3xl font-extrabold">Choose your contribution</h2>
          <p id="donateP" class="fade-up text-gray-600 mt-2">Flexible donation plans—you can also set a custom amount.</p>
        </div>
        <div id="tiers" class="grid sm:grid-cols-2 md:grid-cols-3 gap-4 sm:gap-6"></div>
        <div class="fade-up mt-6 sm:mt-8 bg-white rounded-2xl border rtl-shadow">
          <div id="customH" class="p-4 border-b font-bold">Enter a custom amount</div>
          <div class="p-4 grid md:grid-cols-1 gap-4">
            <div>
              <label class="text-sm" id="amountLabel">Amount (<span id="currency2"></span>)</label>
              <input id="customAmount" inputmode="decimal" type="number" min="1" class="mt-1 w-full rounded-xl border px-3 py-3" />
            </div>
          </div>
          <div class="p-4 flex flex-wrap gap-2">
            <button id="donateCustom" class="btn-primary rounded-xl px-4 py-3 font-semibold w-full sm:w-auto">Pay now</button>
          </div>
        </div>
      </div>
    </section>

    <!-- GALLERY -->
    <section class="py-12 sm:py-16">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <h2 id="galleryH2" class="fade-up text-2xl sm:text-3xl font-extrabold mb-6 sm:mb-8 text-center">Photos from our cases</h2>
        <div class="grid sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-4">
          <img class="fade-up h-48 w-full object-cover rounded-2xl border" src="https://images.unsplash.com/photo-1517849845537-4d257902454a?q=80&w=1200&auto=format&fit=crop" alt="gallery-1">
          <img class="fade-up h-48 w-full object-cover rounded-2xl border" src="https://images.unsplash.com/photo-1543852786-1cf6624b9987?q=80&w=1200&auto=format&fit=crop" alt="gallery-2">
          <img class="fade-up h-48 w-full object-cover rounded-2xl border" src="https://images.unsplash.com/photo-1561037404-61cd46aa615b?q=80&w=1200&auto=format&fit=crop" alt="gallery-3">
          <img class="fade-up h-48 w-full object-cover rounded-2xl border" src="https://images.unsplash.com/photo-1534361960057-19889db9621e?q=80&w=1200&auto=format&fit=crop" alt="gallery-4">
        </div>
      </div>
    </section>
  </div><!-- /#pageHome -->

  <!-- CONTACT -->
  <section id="contact" class="py-12 sm:py-16 bg-green-50">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <h2 class="fade-up text-2xl sm:text-3xl font-extrabold" id="contactH2">Contact us</h2>
      <p class="fade-up text-gray-600 mt-2" id="contactP">We are happy to answer your questions about donations or volunteering.</p>
      <div class="fade-up mt-5 sm:mt-6 space-y-3 text-gray-700">
        <div>📞 <span id="phone"></span></div>
        <div>✉️ <span id="email"></span></div>
        <div>📍 <span id="address"></span></div>
      </div>
      <div class="fade-up flex gap-3 mt-6">
        <a id="ig" href="#" class="inline-flex items-center gap-2 px-4 py-2 rounded-xl border hover:bg-gray-50">Instagram</a>
      </div>
    </div>
  </section>

  <!-- FOOTER -->
  <footer class="py-10 border-t bg-white">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 flex flex-col md:flex-row items-center justify-between gap-4">
      <div class="flex items-center gap-3">
        <img id="logo2" class="h-8 w-8 rounded-lg object-cover" alt="logo"/>
        <div>
          <div id="brandName2" class="font-bold">Animal Welfare Clinic</div>
          <div class="text-xs text-gray-500">© <span id="year"></span> <span id="footerRights">All rights reserved</span></div>
        </div>
      </div>
      <div id="footerBadge" class="text-sm text-gray-600 flex items-center gap-2 text-center">🛡️ Independent donation platform — payment links go directly to the clinic</div>
    </div>
  </footer>

  <!-- DONATE MODAL -->
  <div id="donateModal" class="hidden fixed inset-0 z-50 bg-black/40 items-center justify-center p-3 sm:p-4">
    <div class="modal-enter w-full max-w-lg rounded-2xl bg-white shadow-2xl overflow-hidden">
      <div class="flex items-center justify-between p-4 border-b">
        <div id="modalTitle" class="font-bold flex items-center gap-2">❤️ Complete Donation</div>
        <button id="closeModal" class="p-1 rounded hover:bg-gray-100">✖️</button>
      </div>
      <div class="p-4 sm:p-5 space-y-4">
        <div class="text-lg sm:text-xl font-extrabold text-green-700" id="modalAmount">0</div>
        <p class="text-gray-600 text-sm sm:text-base" id="modalChooseTxt">Choose a method: Visa, transfer via CliQ, or bank transfer (IBAN).</p>
        <label class="flex items-center gap-2 text-xs sm:text-sm flex-wrap">
          <input type="checkbox" id="agree" checked>
          <span id="agreeTxt">I agree to the terms and privacy policy.</span>
          <a id="termsLink" href="#" class="text-blue-600 underline ms-2">More</a>
        </label>

        <div class="grid grid-cols-1 sm:grid-cols-3 gap-3">
          <a id="payPaypal" target="_blank" class="inline-flex items-center justify-center gap-2 px-4 py-3 rounded-xl border font-semibold hover:bg-gray-50 w-full">Pay via Visa ↗</a>
          <button id="payCliq" class="inline-flex items-center justify-center gap-2 px-4 py-3 rounded-xl border font-semibold hover:bg-gray-50 w-full">Transfer via CliQ</button>
          <button id="payIban" class="inline-flex items-center justify-center gap-2 px-4 py-3 rounded-xl border font-semibold hover:bg-gray-50 w-full">Bank transfer (IBAN)</button>
        </div>

        <!-- CliQ box: wrap + horizontal scroll if needed -->
        <div id="cliqBox" class="hidden rounded-2xl border p-4 bg-green-50">
          <div id="cliqTitle" class="font-bold mb-1">Transfer via CliQ</div>
          <p id="cliqP" class="text-sm text-gray-700">Open your banking app → CliQ → Send → Enter the following identifier:</p>
          <div class="mt-2 flex items-center gap-2">
            <div class="scroll-h max-w-full">
              <code id="cliqId" class="px-3 py-2 rounded-lg bg-white border rtl-shadow font-mono text-sm long-id inline-block">TAQY123</code>
            </div>
            <button id="copyCliq" class="btn-primary rounded-lg px-3 py-2 text-sm">Copy</button>
          </div>
        </div>

        <!-- IBAN box: wrap + horizontal scroll if needed -->
        <div id="ibanBox" class="hidden rounded-2xl border p-4 bg-blue-50">
          <div id="ibanTitle" class="font-bold mb-1">Bank transfer (IBAN)</div>
          <p id="ibanP" class="text-sm text-gray-700">Copy the IBAN, then transfer from your banking app:</p>
          <div class="mt-2 flex items-center gap-2">
            <div class="scroll-h max-w-full">
              <code id="ibanCode" class="px-3 py-2 rounded-lg bg-white border rtl-shadow font-mono text-sm long-id inline-block">JO69UBSI1010000010160371415501</code>
            </div>
            <button id="copyIban" class="btn-primary rounded-lg px-3 py-2 text-sm">Copy</button>
          </div>
        </div>

        <!-- Also wrap IBAN in the alternative line -->
        <div id="altLine" class="text-xs text-gray-500">Alternative: Bank transfer to IBAN:
          <span class="font-mono long-id inline-block max-w-full scroll-h align-middle" id="iban"></span>
        </div>
      </div>
    </div>
  </div>

  <!-- TERMS "PAGE" (English only) -->
  <main id="pageTerms" class="hidden max-w-3xl mx-auto px-4 py-10">
    <a id="backLink" href="./" class="text-blue-600 underline text-sm">Back</a>
    <h1 id="pageTitle" class="text-3xl font-extrabold mt-4 mb-6">Terms & Privacy Policy</h1>
    <section id="terms_en" class="space-y-6" lang="en" dir="ltr">
      <p class="text-gray-700">We value your trust. By using this donation site, you agree to the terms and privacy policy below.</p>
      <h2 class="text-xl font-bold">1) Purpose of the Platform</h2>
      <p class="text-gray-700">This platform provides a simple, secure way to send donations directly to the listed clinic. Payment links lead to external providers (e.g., PayPal or banking gateways).</p>
      <h2 class="text-xl font-bold">2) Payment Methods</h2>
      <ul class="list-disc ps-6 text-gray-700">
        <li>Payments may be processed by trusted third parties (PayPal, CliQ, or bank transfer).</li>
        <li>Fees may be charged by your payment provider or bank.</li>
      </ul>
      <h2 class="text-xl font-bold">3) Transparency & Receipts</h2>
      <ul class="list-disc ps-6 text-gray-700">
        <li>Donations are recorded by the payment provider. Keep the receipt you receive from that provider.</li>
        <li>For questions about allocation or reports, please contact the clinic via the email listed on the main site.</li>
      </ul>
      <h2 class="text-xl font-bold">4) Privacy Policy</h2>
      <ul class="list-disc ps-6 text-gray-700">
        <li>We collect no more personal data than necessary to complete the donation and communicate with you.</li>
        <li>Your card details are processed by the external payment provider and are not stored on this platform.</li>
        <li>We may retain basic contact info (e.g., email) for follow-up in accordance with applicable laws.</li>
      </ul>
      <h2 class="text-xl font-bold">5) Refunds & Cancellations</h2>
      <p class="text-gray-700">Donations are voluntary contributions. Refund requests are assessed case-by-case with the payment provider and in line with local laws.</p>
      <h2 class="text-xl font-bold">6) Disclaimer</h2>
      <p class="text-gray-700">This platform is provided “as is.” We are not responsible for outages or technical issues of payment providers or banks.</p>
      <h2 class="text-xl font-bold">7) Contact</h2>
      <p class="text-gray-700">For any questions, please use the email provided on the “Contact us” section of the main site.</p>
      <p class="text-xs text-gray-500">Last updated: 12 September 2025</p>
    </section>
  </main>

  <!-- =================== SCRIPTS =================== -->
  <script>
    const $ = (sel)=>document.querySelector(sel);
    const $$ = (sel)=>document.querySelectorAll(sel);
    const getT = ()=> i18n[currentLang];

    // basics
    logo.src = siteConfig.brand.logo;
    logo2.src = siteConfig.brand.logo;
    brandName.textContent = siteConfig.clinicName;
    brandName2.textContent = siteConfig.clinicName;
    $('#year').textContent = new Date().getFullYear();

    // hero/about images & tagline
    heroImg.src = siteConfig.hero.images[0];
    aboutImg.src = siteConfig.hero.images[1];
    tagline.textContent = siteConfig.tagline;

    // contacts
    phone.textContent = siteConfig.contact.phone;
    email.textContent = siteConfig.contact.email;
    address.textContent = siteConfig.contact.address_en || siteConfig.contact.address;
    ig.href = siteConfig.contact.instagram;

    // currency labels
    $('#currency2').textContent = siteConfig.currency;

    // presets/amounts
    const presetValues = [5,10,20,50];
    let selectedAmount = 10;
    const money = (v)=> siteConfig.money(v);

    function renderPresetButtons(){
      const c = $('#presetBtns');
      if (!c) return;

      c.innerHTML = presetValues.map(v=>`
        <button data-amt="${v}" class="preset-btn py-3 rounded-xl border text-sm font-semibold">
          ${money(v)}
        </button>`).join('');

      $$('#presetBtns .preset-btn').forEach(btn=>{
        if (Number(btn.dataset.amt) === Number(selectedAmount)){
          btn.classList.add('selected');
        }
        btn.addEventListener('click', ()=>{
          selectedAmount = Number(btn.dataset.amt);
          $$('#presetBtns .preset-btn').forEach(b=>b.classList.remove('selected'));
          btn.classList.add('selected');
          const qi = $('#quickCustomAmount');
          if(qi) qi.value = selectedAmount;
        });
      });

      const cq = $('#currencyQuick'); if (cq) cq.textContent = siteConfig.currency;
    }
    renderPresetButtons();

    // quick custom
    const quickInput = $('#quickCustomAmount');
    if (quickInput){
      quickInput.addEventListener('input', ()=>{
        const v = Number(quickInput.value);
        if (v > 0) selectedAmount = v;
      });
    }

    // tiers renderer
    function renderTiers(mapper=(s)=>s){
      tiers.innerHTML = siteConfig.tiers.map((t)=>`
        <div class="fade-up bg-white rounded-2xl border rtl-shadow flex flex-col">
          <div class="p-4 border-b font-bold flex items-center justify-between">
            <span>${mapper(t.title)}</span><span class="text-amber-500">✦</span>
          </div>
          <div class="p-4">
            <div class="text-3xl sm:text-4xl font-extrabold text-green-700">${money(t.amount)}</div>
            <p class="text-gray-600 mt-2 min-h-[3rem]">${mapper(t.desc)}</p>
          </div>
          <div class="p-4 mt-auto">
            <button data-amt="${t.amount}" class="tierBtn btn-primary w-full rounded-xl py-3 font-semibold">${getT().tierBtn}</button>
          </div>
        </div>`).join('');
      $$('.tierBtn').forEach(b=>b.addEventListener('click',()=>openModal(Number(b.dataset.amt))));
      if (typeof io !== 'undefined' && io) $$('#tiers .fade-up').forEach(el=>io.observe(el));
    }

    // English PayPal NCP base URL
    function payBaseUrl(){
      return "https://www.paypal.com/ncp/payment/YRBDV24CBS3QG";
    }

    // donate modal
    function openModal(amount){
      selectedAmount = amount ?? selectedAmount;
      $('#modalAmount').textContent = money(selectedAmount);

      const baseNcp = payBaseUrl();
      $('#payPaypal').href = `${baseNcp}?amount=${encodeURIComponent(selectedAmount)}&currency_code=${encodeURIComponent(siteConfig.currency)}`;

      const t = getT();
      const termsL = $('#termsLink');
      if (termsL){
        termsL.textContent = t.more;
        termsL.onclick = (e)=>{ e.preventDefault(); goToTerms(currentLang); };
      }

      cliqBox.classList.add('hidden');
      ibanBox.classList.add('hidden');
      $('#iban').textContent = siteConfig.payments.bankIban;

      donateModal.classList.remove('hidden');
      donateModal.classList.add('flex');
    }

    // ensure final link carries the latest amount
    $('#payPaypal').addEventListener('click', ()=>{
      const baseNcp = payBaseUrl();
      const amt = Number(selectedAmount) > 0 ? selectedAmount : 10;
      $('#payPaypal').href = `${baseNcp}?amount=${encodeURIComponent(amt)}&currency_code=${encodeURIComponent(siteConfig.currency)}`;
    });

    function closeModalFn(){
      donateModal.classList.add('hidden');
      donateModal.classList.remove('flex');
    }
    $('#closeModal').addEventListener('click', closeModalFn);
    donateModal.addEventListener('click', (e)=>{ if(e.target===donateModal) closeModalFn(); });

    donateTop.addEventListener('click', ()=>openModal(selectedAmount));
    donateHero.addEventListener('click', ()=>openModal(selectedAmount));
    donateQuick.addEventListener('click', ()=>openModal(selectedAmount));
    donateCustom.addEventListener('click', ()=>openModal(Number(customAmount.value||10)));

    function togglePay(enabled){
      [payPaypal, payCliq, payIban].forEach(a=>{
        a.style.opacity = enabled? '1':'0.5';
        if(!enabled){a.setAttribute('tabindex','-1');a.style.pointerEvents='none'} else {a.removeAttribute('tabindex');a.style.pointerEvents='auto'}
      })
    }
    togglePay(true);
    agree.addEventListener('change', e=> togglePay(e.target.checked));

    copyCliq.addEventListener('click', async ()=>{
      try {
        await navigator.clipboard.writeText($('#cliqId').textContent.trim());
        copyCliq.textContent = getT().copied;
        setTimeout(()=> copyCliq.textContent = getT().copy, 1600);
      } catch(e){
        alert(getT().cliqCopyFallback);
      }
    });
    copyIban.addEventListener('click', async ()=>{
      try {
        await navigator.clipboard.writeText(siteConfig.payments.bankIban);
        copyIban.textContent = getT().copied;
        setTimeout(()=> copyIban.textContent = getT().copy, 1600);
      } catch(e){
        alert(getT().ibanCopyFallback);
      }
    });

    payCliq.addEventListener('click', ()=>{
      const willOpen = cliqBox.classList.contains('hidden');
      ibanBox.classList.add('hidden');
      cliqBox.classList.toggle('hidden', !willOpen ? true : false);
      if(willOpen){ cliqBox.scrollIntoView({behavior:'smooth', block:'nearest'}); }
    });
    payIban.addEventListener('click', ()=>{
      const willOpen = ibanBox.classList.contains('hidden');
      cliqBox.classList.add('hidden');
      $('#ibanCode').textContent = siteConfig.payments.bankIban;
      ibanBox.classList.toggle('hidden', !willOpen ? true : false);
      if(willOpen){ ibanBox.scrollIntoView({behavior:'smooth', block:'nearest'}); }
    });

    const io = new IntersectionObserver((entries)=>{ entries.forEach(en=>{ if(en.isIntersecting) en.target.classList.add('in') }) },{threshold:.15});
    $$('.fade-up').forEach(el=>io.observe(el));

    // setLocale (English only)
    function setLocale(){
      const t = i18n.en; // force English
      currentLang = 'en';

      document.documentElement.dir = t.dir;
      document.documentElement.lang = t.lang;

      // Navbar/Brand
      brandName.textContent = t.clinicName;
      brandName2.textContent = t.clinicName;
      const navLinks = $$('nav a');
      if(navLinks.length>=3){ navLinks[0].textContent = t.menu[0]; navLinks[1].textContent = t.menu[1]; navLinks[2].textContent = t.menu[2]; }

      // Hero
      tagline.textContent = t.tagline;
      $('#heroP').textContent = t.heroP;
      $('#donateTop').textContent = t.ctaDonate;
      $('#donateHeroTxt').textContent = t.ctaDonate;
      $('#learnMoreLink').textContent = t.ctaLearn;

      // Features
      const feats = $('#featuresRow').children;
      if (feats.length>=3){
        feats[0].textContent = '🔒 ' + t.features[0];
        feats[1].textContent = '💳 ' + t.features[1];
        feats[2].textContent = '🐾 ' + t.features[2];
      }

      // About
      $('#aboutH2').textContent = t.aboutH2;
      $('#aboutP').textContent = t.aboutP;
      $('#aboutList').innerHTML = t.aboutLis.map(item=>`<li>${item}</li>`).join('');

      // Donate section headings
      $('#donateH2').textContent = t.donateH2;
      $('#donateP').textContent = t.donateP;

      // Tiers
      const mapTierText = s => s;
      renderTiers(mapTierText);

      // Custom amount block
      $('#customH').textContent = t.customH;
      $('#amountLabel').innerHTML = `${t.amountLabel} (<span id="currency2">${siteConfig.currency}</span>)`;
      $('#donateCustom').textContent = t.customPay;

      // Quick donate box
      $('#quickTitle').textContent = t.quickTitle;
      $('#donateQuick').textContent = t.quickBtn;
      $('#quickNote').textContent = t.quickNote;
      $('#quickAmountLabel').innerHTML = `${t.quickAmountLabel} (<span id="currencyQuick">${siteConfig.currency}</span>)`;
      renderPresetButtons();

      // Contact
      $('#contactH2').textContent = t.contactH2;
      $('#contactP').textContent = t.contactP;
      $('#ig').textContent = t.instagram;
      address.textContent = siteConfig.contact.address_en || siteConfig.contact.address;

      // Footer
      $('#footerRights').textContent = t.footerRights;
      $('#footerBadge').textContent = t.footerBadge;

      // Modal texts
      $('#modalTitle').textContent = t.modalTitle;
      $('#modalChooseTxt').textContent = t.modalChoose;
      $('#agreeTxt').textContent = t.modalAgree;
      $('#payPaypal').textContent = t.payPaypal;
      $('#payCliq').textContent = t.payCliq;
      $('#payIban').textContent = t.payIban;
      $('#cliqTitle').textContent = t.cliqTitle;
      $('#cliqP').textContent = t.cliqP;
      $('#ibanTitle').textContent = t.ibanTitle;
      $('#ibanP').textContent = t.ibanP;
      $('#altLine').innerHTML = `${t.alternative} <span class="font-mono long-id inline-block max-w-full scroll-h align-middle" id="iban">${siteConfig.payments.bankIban}</span>`;

      // If modal is open, refresh amount & Visa link
      if (!donateModal.classList.contains('hidden')) {
        $('#modalAmount').textContent = money(selectedAmount);
        const baseNcp = payBaseUrl();
        $('#payPaypal').href = `${baseNcp}?amount=${encodeURIComponent(selectedAmount)}&currency_code=${encodeURIComponent(siteConfig.currency)}`;
      }

      // Gallery heading
      $('#galleryH2').textContent = t.galleryH2;
    }

    // Router
    function getParams(){
      const p = new URLSearchParams(location.search);
      return { page: (p.get('page')||'').toLowerCase(), lang: 'en' };
    }
    function goToTerms(){
      const url = `${location.pathname}?page=terms&lang=en${location.hash||''}`;
      location.assign(url);
    }
    function goHome(){ location.assign(`${location.pathname}${location.hash||''}`); }

    document.getElementById('backLink').addEventListener('click', (e)=>{ e.preventDefault(); goHome(); });

    function route(){
      const {page} = getParams();
      const home = $('#pageHome');
      const terms = $('#pageTerms');

      if (page === 'terms'){
        closeModalFn();
        home.classList.add('hidden');
        $('#contact').classList.add('hidden');
        $('footer').classList.add('hidden');
        terms.classList.remove('hidden');

        setLocale();
        $('#pageTitle').textContent = 'Terms & Privacy Policy';
        $('#backLink').textContent = 'Back';
        document.title = 'Terms & Privacy — Animal Welfare Clinic';
      } else {
        home.classList.remove('hidden');
        $('#contact').classList.remove('hidden');
        $('footer').classList.remove('hidden');
        terms.classList.add('hidden');
        document.title = 'Animal Welfare — Your donation saves lives';
      }
    }
    window.addEventListener('popstate', route);
    window.addEventListener('DOMContentLoaded', route);

    // INIT
    setLocale();
    const currencyQuickInit = $('#currencyQuick');
    if(currencyQuickInit) currencyQuickInit.textContent = siteConfig.currency;
    (function initRoute(){
      const p=new URLSearchParams(location.search);
      if ((p.get('page')||'').toLowerCase()==='terms'){ route(); }
    })();
  </script>
</body>
</html>

