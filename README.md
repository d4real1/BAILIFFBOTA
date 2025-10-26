# BAILIFFBOTA
Law on removal of goods 
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>AI Lawyer – Police & Bailiff Powers | Free Instant Advice</title>
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <meta name="description" content="Know your rights when police or bailiffs come to collect goods or enforce a warrant. 100 % free, anonymous, UK-law accurate.">
  <meta name="keywords" content="bailiff rights, police warrant, goods collection, UK enforcement law, AI legal advice">
  <link rel="canonical" href="https://yourdomain.co.uk/">
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600&display=swap" rel="stylesheet">
  <link rel="preload" href="globals.css" as="style" onload="this.rel='stylesheet'">
  <noscript><link rel="stylesheet" href="globals.css"></noscript>
</head>
<body>
  <header>
    <h1>AI Lawyer – Police & Bailiff Powers</h1>
    <p>Instant, anonymous advice on warrants, goods collection, and your rights. 100 % free.</p>
    <a class="btn" href="#guild">Start the Guild</a>
  </header>

  <section id="guild" class="guild">
    <h2>Beginner Guild – 8 Steps to Protect Yourself</h2>
    <ol>
      <li><strong>Who’s knocking?</strong> Bailiffs must show ID and the Notice of Enforcement; police must state the power used (PACE s 24).</li>
      <li><strong>Notice check.</strong> A valid notice needs 7 clear items (TCEA 2007 Sch 12, Reg 8) including debt amount and compliance date.</li>
      <li><strong>Fee cap.</strong> £75 compliance, £235 enforcement, £110 sale. No VAT on top (HMRC scale).</li>
      <li><strong>Exempt goods.</strong> Cooker, fridge, kids’ items, tools of trade up to £1 350 (Reg 4).</li>
      <li><strong>Vulnerability.</strong> Tell them if you’re disabled, elderly, mentally unwell—they must pause (Reg 13).</li>
      <li><strong>Police powers.</strong> Entry without warrant for indictable offence only; must caution and use necessity test (PACE ss 28, 117).</li>
      <li><strong>Warrant check.</strong> Must be court-sealed, dated, signed—photograph it and ask for a copy (CPR Pt 83).</li>
      <li><strong>Complaint.</strong> Use the template the bot generates; send to Local Government Ombudsman or court within 12 weeks.</li>
    </ol>
  </section>

  <section>
    <h2>Chat Now – No Sign-Up</h2>
    <p>Click the blue bubble. Ask anything: “bailiff at my door”, “check warrant”, “exempt goods list”.</p>
  </section>

  <footer>
    <p>Legal review dated <time>2025-06-25</time>. Disclaimer: general information only; not regulated legal advice.</p>
    <p><a href="/accessibility">Accessibility Statement</a> | <a href="/privacy">Privacy</a></p>
  </footer>

  <!-- Chat Widget -->
  <div id="chatWidget" aria-label="Open chat" role="button" tabindex="0">💬</div>
  <div id="chatWindow">
    <div id="chatHeader">
      <span>AI Lawyer</span>
      <button id="closeBtn" aria-label="Close chat"><span aria-hidden="true">×</span></button>
    </div>
    <div id="chatLog" aria-live="polite"></div>
    <input id="chatInput" type="text" placeholder="Ask a question…" aria-label="Type your question">
  </div>

  <script src="app.js" defer></script>
</body>
</html>
:root{--blue:#1d4ed8;--grey:#f3f4f6;--dark:#111827}
*{box-sizing:border-box;margin:0;padding:0;font-family:Inter,system-ui,sans-serif}
body{background:var(--grey);color:var(--dark);line-height:1.55}
header{background:var(--blue);color:#fff;padding:2rem 1rem;text-align:center}
header h1{font-size:2rem;margin-bottom:.5rem}
.btn{display:inline-block;margin-top:1rem;padding:.75rem 1.25rem;background:#fff;color:var(--blue);border-radius:4px;font-weight:600;text-decoration:none}
.btn:hover{opacity:.9}
section{padding:2rem 1rem;max-width:800px;margin:auto}
.guild ol{margin-left:1.25rem}
.guild li{margin:.5rem 0}
#chatWidget{position:fixed;bottom:20px;right:20px;width:60px;height:60px;background:var(--blue);border-radius:50%;display:flex;align-items:center;justify-content:center;color:#fff;font-size:24px;cursor:pointer;box-shadow:0 4px 12px rgba(0,0,0,.25)}
#chatWindow{display:none;position:fixed;bottom:90px;right:20px;width:340px;height:460px;background:#fff;border-radius:8px;box-shadow:0 6px 20px rgba(0,0,0,.2);flex-direction:column}
#chatHeader{background:var(--blue);color:#fff;padding:.5rem;border-radius:8px 8px 0 0;display:flex;justify-content:space-between;align-items:center}
#chatInput{border:none;border-top:1px solid #ddd;padding:.5rem;font-size:.9rem;width:100%}
.sr-only{position:absolute;width:1px;height:1px;padding:0;margin:-1px;overflow:hidden;clip:rect(0,0,0,0);white-space:nowrap;border:0}
@media (prefers-reduced-motion: reduce){*{transition:none!important}}
// ---- Chat Widget ----
const widget = document.getElementById('chatWidget');
const win    = document.getElementById('chatWindow');
const log    = document.getElementById('chatLog');
const input  = document.getElementById('chatInput');
const close  = document.getElementById('closeBtn');

function toggle(open){
  win.style.display = open ? 'flex' : 'none';
  if(open) input.focus();
}
widget.addEventListener('click', () => toggle(true));
widget.addEventListener('keydown', (e) => {if (e.key === 'Enter') toggle(true);});
close.addEventListener('click',  () => toggle(false));

input.addEventListener('keydown', async (e) => {
  if (e.key !== 'Enter') return;
  const q = input.value.trim();
  if (!q) return;
  appendLog('user', q);
  input.value = '';
  try {
    const res = await fetch('/api/chat', {
      method : 'POST',
      headers: {'Content-Type':'application/json'},
      body   : JSON.stringify({message: q})
    });
    const data = await res.json();
    appendLog('bot', data.reply || 'Sorry, please try again.');
  } catch (err) {
    appendLog('bot', 'Network error – please refresh.');
  }
});

function appendLog(sender, txt){
  const p = document.createElement('p');
  p.innerHTML = `<strong>${sender}:</strong> ${txt}`;
  log.appendChild(p);
  log.scrollTop = log.scrollHeight;
}{
  "headers": [
    {
      "source": "/(.*)",
      "headers": [
        { "key": "Content-Security-Policy", "value": "default-src 'self'; script-src 'self' 'unsafe-inline'; style-src 'self' 'unsafe-inline' https://fonts.googleapis.com; font-src https://fonts.gstatic.com; img-src 'self' data:; connect-src 'self' https://www.google-analytics.com https://your-rasa.com; frame-ancestors 'none';" },
        { "key": "X-Content-Type-Options", "value": "nosniff" },
        { "key": "Referrer-Policy", "value": "strict-origin-when-cross-origin" }
      ]
    }
  ]
}
