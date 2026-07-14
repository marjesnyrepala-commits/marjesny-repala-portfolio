[index.html](https://github.com/user-attachments/files/30019855/index.html)
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Marjesny Repala — Operations Console</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@500;600;700&family=IBM+Plex+Mono:wght@400;500;600&family=IBM+Plex+Sans:wght@400;500;600&display=swap" rel="stylesheet">
<style>
  :root{
    --bg:#1B2027;
    --panel:#242B33;
    --panel-alt:#2A323B;
    --line:#3A424C;
    --ink:#E8E6DF;
    --muted:#8B93A0;
    --teal:#4FBDBA;
    --amber:#E0A458;
    --red:#D9695F;
  }
  *{margin:0;padding:0;box-sizing:border-box;}
  html{scroll-behavior:smooth;}
  @media (prefers-reduced-motion: reduce){
    html{scroll-behavior:auto;}
    *{animation-duration:0.001ms !important; animation-iteration-count:1 !important; transition-duration:0.001ms !important;}
  }
  body{
    background:var(--bg);
    color:var(--ink);
    font-family:'IBM Plex Sans',sans-serif;
    background-image:
      linear-gradient(var(--line) 1px, transparent 1px),
      linear-gradient(90deg, var(--line) 1px, transparent 1px);
    background-size:64px 64px;
    background-position:center top;
    background-attachment:fixed;
    background-color:var(--bg);
  }
  body::before{
    content:"";
    position:fixed;inset:0;
    background:radial-gradient(ellipse at top, rgba(27,32,39,0) 0%, var(--bg) 78%);
    pointer-events:none;
    z-index:0;
  }
  a{color:inherit;}
  .mono{font-family:'IBM Plex Mono',monospace;}
  .display{font-family:'Space Grotesk',sans-serif;}

  :focus-visible{outline:2px solid var(--teal); outline-offset:3px;}

  .wrap{max-width:1040px;margin:0 auto;padding:0 24px;position:relative;z-index:1;}

  /* ---------------- TOP STATUS BAR ---------------- */
  .statusbar{
    border-bottom:1px solid var(--line);
    background:rgba(36,43,51,0.7);
    backdrop-filter:blur(6px);
    position:sticky;top:0;z-index:10;
  }
  .statusbar-inner{
    max-width:1040px;margin:0 auto;padding:10px 24px;
    display:flex;justify-content:space-between;align-items:center;
    flex-wrap:wrap;gap:8px 20px;
    font-family:'IBM Plex Mono',monospace;
    font-size:11.5px;color:var(--muted);
  }
  .dot{
    display:inline-block;width:7px;height:7px;border-radius:50%;
    background:var(--teal);margin-right:6px;
    box-shadow:0 0 0 0 rgba(79,189,186,0.6);
    animation:pulse 2.4s infinite;
  }
  @keyframes pulse{
    0%{box-shadow:0 0 0 0 rgba(79,189,186,0.55);}
    70%{box-shadow:0 0 0 7px rgba(79,189,186,0);}
    100%{box-shadow:0 0 0 0 rgba(79,189,186,0);}
  }
  .clocks{display:flex;gap:18px;flex-wrap:wrap;}
  .clocks span b{color:var(--ink);font-weight:500;}

  /* ---------------- HERO ---------------- */
  .hero{padding:64px 0 40px;}
  .eyebrow{
    font-family:'IBM Plex Mono',monospace;
    font-size:11.5px;letter-spacing:0.14em;text-transform:uppercase;
    color:var(--teal);margin-bottom:16px;
  }
  .hero h1{
    font-family:'Space Grotesk',sans-serif;
    font-weight:700;
    font-size:clamp(38px,6vw,64px);
    line-height:1.05;
    letter-spacing:-0.01em;
  }
  .hero .subtitle{
    margin-top:14px;
    font-size:16px;color:var(--muted);
    max-width:52ch;line-height:1.6;
  }
  .hero-meta{
    display:flex;gap:28px;flex-wrap:wrap;margin-top:32px;
  }
  .meta-stat{
    font-family:'IBM Plex Mono',monospace;
  }
  .meta-stat .num{
    font-size:26px;color:var(--amber);font-weight:600;display:block;
  }
  .meta-stat .label{
    font-size:10.5px;color:var(--muted);text-transform:uppercase;letter-spacing:0.1em;
  }
  .contact-row{
    margin-top:32px;
    display:flex;gap:18px;flex-wrap:wrap;
    font-family:'IBM Plex Mono',monospace;font-size:13px;
  }
  .contact-row a{
    color:var(--ink);text-decoration:none;
    border-bottom:1px solid var(--line);
    padding-bottom:2px;
    transition:border-color 0.15s ease, color 0.15s ease;
  }
  .contact-row a:hover{color:var(--teal);border-color:var(--teal);}

  /* ---------------- SECTION FRAME ---------------- */
  .section{padding:52px 0;border-top:1px solid var(--line);}
  .section-head{
    display:flex;align-items:center;gap:12px;margin-bottom:28px;
  }
  .section-head .tag{
    font-family:'IBM Plex Mono',monospace;
    font-size:10.5px;color:var(--bg);
    background:var(--teal);
    padding:3px 8px;border-radius:2px;
    letter-spacing:0.06em;font-weight:600;
  }
  .section-head h2{
    font-family:'Space Grotesk',sans-serif;
    font-size:22px;font-weight:600;
  }

  /* ---------------- MODULES (skills) ---------------- */
  .modules{
    display:grid;grid-template-columns:repeat(3,1fr);gap:14px;
  }
  @media (max-width:760px){.modules{grid-template-columns:1fr;}}
  .module{
    background:var(--panel);
    border:1px solid var(--line);
    border-radius:6px;
    padding:18px 18px 16px;
  }
  .module-head{
    display:flex;justify-content:space-between;align-items:center;
    margin-bottom:12px;
  }
  .module-head b{font-family:'Space Grotesk',sans-serif;font-size:14.5px;font-weight:600;}
  .status-pill{
    font-family:'IBM Plex Mono',monospace;font-size:9.5px;
    color:var(--teal);
    display:flex;align-items:center;gap:5px;
    text-transform:uppercase;letter-spacing:0.06em;
  }
  .status-pill .dot{margin-right:0;}
  .module ul{list-style:none;}
  .module li{
    font-size:13px;color:var(--muted);
    padding:5px 0;
    border-top:1px dashed var(--line);
  }
  .module li:first-child{border-top:none;}

  /* ---------------- TICKET LOG (experience) ---------------- */
  .ticket-log{border:1px solid var(--line);border-radius:6px;overflow:hidden;}
  .ticket{
    padding:22px 22px;
    border-bottom:1px solid var(--line);
    background:var(--panel);
  }
  .ticket:nth-child(even){background:var(--panel-alt);}
  .ticket:last-child{border-bottom:none;}
  .ticket-top{
    display:flex;justify-content:space-between;align-items:center;flex-wrap:wrap;gap:8px;
    margin-bottom:10px;
  }
  .ticket-id{
    font-family:'IBM Plex Mono',monospace;font-size:11.5px;color:var(--amber);
  }
  .ticket-status{
    font-family:'IBM Plex Mono',monospace;font-size:10.5px;
    text-transform:uppercase;letter-spacing:0.06em;
    padding:2px 9px;border-radius:20px;
    border:1px solid var(--teal);color:var(--teal);
  }
  .ticket-status.active{border-color:var(--amber);color:var(--amber);}
  .ticket h3{
    font-family:'Space Grotesk',sans-serif;font-size:18px;font-weight:600;margin-bottom:2px;
  }
  .ticket .org{
    font-size:13.5px;color:var(--muted);margin-bottom:12px;
  }
  .ticket .dates{
    font-family:'IBM Plex Mono',monospace;font-size:11.5px;color:var(--muted);
  }
  .ticket ul{margin-top:12px;padding-left:18px;}
  .ticket li{font-size:13.5px;color:var(--muted);line-height:1.6;margin-bottom:6px;}
  .ticket li::marker{color:var(--teal);}

  /* ---------------- INCIDENT REPORTS (case studies) ---------------- */
  .incidents{display:grid;grid-template-columns:1fr 1fr;gap:16px;}
  @media (max-width:760px){.incidents{grid-template-columns:1fr;}}
  .incident{
    background:var(--panel);border:1px solid var(--line);border-radius:6px;
    padding:22px;
  }
  .incident-head{
    display:flex;justify-content:space-between;align-items:flex-start;gap:10px;
    margin-bottom:14px;
  }
  .sev{
    font-family:'IBM Plex Mono',monospace;font-size:10px;
    text-transform:uppercase;letter-spacing:0.06em;
    padding:2px 8px;border-radius:3px;white-space:nowrap;
    background:rgba(224,164,88,0.15);color:var(--amber);
    border:1px solid var(--amber);
  }
  .incident h3{font-family:'Space Grotesk',sans-serif;font-size:16.5px;font-weight:600;line-height:1.3;}
  .field{margin-bottom:12px;}
  .field b{
    display:block;font-family:'IBM Plex Mono',monospace;font-size:10px;
    text-transform:uppercase;letter-spacing:0.08em;color:var(--teal);margin-bottom:4px;
  }
  .field p{font-size:13.5px;color:var(--muted);line-height:1.55;}

  /* ---------------- CERTIFICATIONS ---------------- */
  .certs{display:grid;grid-template-columns:1fr 1fr;gap:14px;}
  @media (max-width:640px){.certs{grid-template-columns:1fr;}}
  .cert{
    background:var(--panel);border:1px solid var(--line);border-radius:6px;
    padding:18px 20px;
    display:flex;justify-content:space-between;align-items:center;gap:12px;
  }
  .cert div b{display:block;font-size:14.5px;margin-bottom:4px;font-weight:600;}
  .cert div span{font-size:12.5px;color:var(--muted);}
  .cert-check{
    flex:0 0 auto;width:26px;height:26px;border-radius:50%;
    border:1.5px solid var(--teal);color:var(--teal);
    display:flex;align-items:center;justify-content:center;font-size:13px;
  }

  /* ---------------- FOOTER / TERMINAL ---------------- */
  footer{padding:52px 0 64px;border-top:1px solid var(--line);}
  .terminal{
    background:var(--panel);border:1px solid var(--line);border-radius:6px;
    padding:22px 24px;font-family:'IBM Plex Mono',monospace;font-size:13.5px;
    color:var(--muted);max-width:560px;
  }
  .terminal .line{margin-bottom:8px;}
  .terminal .prompt{color:var(--teal);}
  .terminal a{color:var(--amber);text-decoration:none;border-bottom:1px dotted var(--amber);}
  .terminal a:hover{color:var(--ink);}
  .cursor{
    display:inline-block;width:8px;height:14px;background:var(--teal);
    vertical-align:middle;margin-left:4px;
    animation:blink 1s steps(1) infinite;
  }
  @keyframes blink{50%{opacity:0;}}
</style>
</head>
<body>

  <div class="statusbar">
    <div class="statusbar-inner">
      <span><span class="dot"></span>SYSTEM STATUS: <b style="color:var(--ink)">ALL OPERATIONAL</b></span>
      <div class="clocks">
        <span id="clock-ph">MANILA <b>--:--</b></span>
        <span id="clock-de">BERLIN <b>--:--</b></span>
        <span id="clock-us">SAN FRANCISCO <b>--:--</b></span>
      </div>
    </div>
  </div>

  <div class="wrap">

    <section class="hero">
      <div class="eyebrow">// Operations Console — Marjesny Repala</div>
      <h1 class="display">Global Operations &amp;<br>E-Commerce Specialist</h1>
      <p class="subtitle">Keeping international fulfillment, support queues, and cross-border logistics running on schedule — across time zones, tools, and teams.</p>

      <div class="hero-meta">
        <div class="meta-stat"><span class="num">9+</span><span class="label">Years in ops</span></div>
        <div class="meta-stat"><span class="num">3</span><span class="label">Global orgs</span></div>
        <div class="meta-stat"><span class="num">0</span><span class="label">Open incidents</span></div>
      </div>

      <div class="contact-row">
        <a href="mailto:marjesny.repala@gmail.com">marjesny.repala@gmail.com</a>
        <a href="tel:+639458531039">+63 945 853 1039</a>
        <a href="https://linkedin.com/in/marjesny" target="_blank" rel="noopener">linkedin.com/in/marjesny</a>
        <span style="color:var(--muted)">📍 Antipolo City, PH</span>
      </div>
    </section>

    <section class="section" id="modules">
      <div class="section-head">
        <span class="tag">MODULES</span>
        <h2 class="display">System Capabilities</h2>
      </div>
      <div class="modules">
        <div class="module">
          <div class="module-head"><b>Operations &amp; E-Commerce</b><span class="status-pill"><span class="dot"></span>Online</span></div>
          <ul>
            <li>Shopify Administration</li>
            <li>Order &amp; Inventory Management</li>
            <li>Logistics &amp; Warehouse Coordination</li>
            <li>Returns &amp; Warranty Processing</li>
          </ul>
        </div>
        <div class="module">
          <div class="module-head"><b>Customer Experience</b><span class="status-pill"><span class="dot"></span>Online</span></div>
          <ul>
            <li>Global Support Operations</li>
            <li>SLA &amp; Quality Management</li>
            <li>Complex Escalations</li>
            <li>SOP &amp; Documentation Creation</li>
          </ul>
        </div>
        <div class="module">
          <div class="module-head"><b>Tools &amp; Platforms</b><span class="status-pill"><span class="dot"></span>Online</span></div>
          <ul>
            <li>Shopify · Gorgias · CRM Systems</li>
            <li>Asana · Slack</li>
            <li>Google Workspace</li>
            <li>Microsoft Excel</li>
          </ul>
        </div>
      </div>
    </section>

    <section class="section" id="experience">
      <div class="section-head">
        <span class="tag">LOG</span>
        <h2 class="display">Ticket History — Experience</h2>
      </div>
      <div class="ticket-log">
        <div class="ticket">
          <div class="ticket-top">
            <span class="ticket-id">#TCK-2023-GLOBALOPS</span>
            <span class="ticket-status active">In progress</span>
          </div>
          <h3 class="display">Global Operations Specialist</h3>
          <div class="org">Toddlekind GmbH · Remote</div>
          <div class="dates">2023 — PRESENT</div>
          <ul>
            <li>Lead international operational workflows, ensuring seamless front-to-back e-commerce fulfillment.</li>
            <li>Coordinate directly with logistics hubs and warehouses to proactively resolve inventory discrepancies and shipping delays.</li>
            <li>Author and continuously update internal SOPs to build repeatable, efficient business processes.</li>
          </ul>
        </div>
        <div class="ticket">
          <div class="ticket-top">
            <span class="ticket-id">#TCK-2016-UBERSUPPORT</span>
            <span class="ticket-status">Resolved</span>
          </div>
          <h3 class="display">Email Support Representative</h3>
          <div class="org">Uber Technologies</div>
          <div class="dates">2016 — 2023</div>
          <ul>
            <li>Managed and resolved high-volume international rider and driver inquiries via email and CRM systems.</li>
            <li>Investigated financial disputes, account safety issues, and policy violations with precise attention to detail.</li>
          </ul>
        </div>
        <div class="ticket">
          <div class="ticket-top">
            <span class="ticket-id">#TCK-2015-SMARTCARE</span>
            <span class="ticket-status">Resolved</span>
          </div>
          <h3 class="display">Customer Service Representative</h3>
          <div class="org">Smart Communications</div>
          <div class="dates">2015 — 2016</div>
          <ul>
            <li>Handled account modifications, technical support, and billing inquiries in a fast-paced telecom contact center.</li>
          </ul>
        </div>
      </div>
    </section>

    <section class="section" id="incidents">
      <div class="section-head">
        <span class="tag">REPORTS</span>
        <h2 class="display">Incident Reports — Case Studies</h2>
      </div>
      <div class="incidents">
        <div class="incident">
          <div class="incident-head">
            <h3 class="display">Global E-Commerce Operations &amp; Logistics Optimization</h3>
            <span class="sev">Priority: High</span>
          </div>
          <div class="field"><b>Detected</b><p>Fragmented international order fulfillment, inventory discrepancies, and cross-border shipping escalations across multiple markets.</p></div>
          <div class="field"><b>Resolution</b><p>Synchronized workflows between Shopify, logistics partners, and international warehouses; maintained central SOPs for order processing, returns, and warranty claims; used Gorgias to speed up ticket response and cross-team communication.</p></div>
          <div class="field"><b>Outcome</b><p>Mitigated complex operational bottlenecks, improved cross-functional response efficiency, and sustained high customer satisfaction globally.</p></div>
        </div>
        <div class="incident">
          <div class="incident-head">
            <h3 class="display">International Scale Support &amp; High-Volume Ticket Management</h3>
            <span class="sev">Priority: High</span>
          </div>
          <div class="field"><b>Detected</b><p>High-stakes global disputes over payments, accounts, and policies under strict, aggressive productivity and quality metrics.</p></div>
          <div class="field"><b>Resolution</b><p>Ran deep-dive investigations into user, trip, and payment disputes using advanced internal CRM tools; collaborated with technical teams on system-wide bugs affecting users globally.</p></div>
          <div class="field"><b>Outcome</b><p>Consistently exceeded strict quality assurance targets while maintaining data integrity and meticulous documentation.</p></div>
        </div>
      </div>
    </section>

    <section class="section" id="certs">
      <div class="section-head">
        <span class="tag">CERTS</span>
        <h2 class="display">Education &amp; Certifications</h2>
      </div>
      <div class="certs">
        <div class="cert">
          <div><b>B.Tech, Electronics &amp; Communications Engineering Technology</b><span>Technological University of the Philippines</span></div>
          <div class="cert-check">✓</div>
        </div>
        <div class="cert">
          <div><b>Basic Agent (Shopify)</b><span>Gorgias Academy</span></div>
          <div class="cert-check">✓</div>
        </div>
      </div>
    </section>

  </div>

  <footer>
    <div class="wrap" style="padding:0;">
      <div class="terminal">
        <div class="line"><span class="prompt">$</span> contact --initiate</div>
        <div class="line">Reaching out regarding a role or project?</div>
        <div class="line">Send details to <a href="mailto:marjesny.repala@gmail.com">marjesny.repala@gmail.com</a><span class="cursor"></span></div>
      </div>
    </div>
  </footer>

  <script>
    function fmt(tz){
      try{
        return new Intl.DateTimeFormat('en-US',{hour:'2-digit',minute:'2-digit',hour12:false,timeZone:tz}).format(new Date());
      }catch(e){ return '--:--'; }
    }
    function tick(){
      var ph = document.getElementById('clock-ph');
      var de = document.getElementById('clock-de');
      var us = document.getElementById('clock-us');
      if(ph) ph.innerHTML = 'MANILA <b>' + fmt('Asia/Manila') + '</b>';
      if(de) de.innerHTML = 'BERLIN <b>' + fmt('Europe/Berlin') + '</b>';
      if(us) us.innerHTML = 'SAN FRANCISCO <b>' + fmt('America/Los_Angeles') + '</b>';
    }
    tick();
    setInterval(tick, 30000);
  </script>

</body>
</html>
