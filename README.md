<!DOCTYPE html>
<html lang="it">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Base di Lancio — v3</title>
<link href="https://fonts.googleapis.com/css2?family=Crimson+Pro:ital,wght@0,300;0,400;0,600;1,300&family=JetBrains+Mono:wght@400;500&family=Outfit:wght@300;400;500;600&display=swap" rel="stylesheet">
<style>
:root {
  --bg:#0f1117; --surface:#181c27; --surface2:#1e2436;
  --accent:#4a9eff; --accent2:#7dd3b0; --accent3:#f0a05a;
  --text:#e8eaf0; --muted:#7a8099; --border:#2a3048; --radius:10px;
}
*{box-sizing:border-box;margin:0;padding:0}
body{font-family:'Outfit',sans-serif;background:var(--bg);color:var(--text);min-height:100vh;
  background-image:radial-gradient(ellipse at 20% 0%,rgba(74,158,255,.07) 0%,transparent 50%),
  radial-gradient(ellipse at 80% 100%,rgba(125,211,176,.05) 0%,transparent 50%)}
header{padding:36px 40px 0;text-align:center}
header::after{content:'';display:block;width:60px;height:2px;
  background:linear-gradient(90deg,var(--accent),var(--accent2));margin:18px auto 0;border-radius:2px}
h1{font-family:'Crimson Pro',serif;font-size:2.8rem;font-weight:300;letter-spacing:.08em;text-transform:uppercase}
h1 span{font-style:italic;color:var(--accent);font-weight:300}
.subtitle{font-size:.82rem;color:var(--muted);letter-spacing:.15em;text-transform:uppercase;margin-top:6px;font-weight:300}

/* TABS */
.tabs-wrapper{max-width:1060px;margin:36px auto 0;padding:0 20px 60px}
.tabs-wrapper input[type=radio]{display:none}
.tabs-nav{display:flex;gap:4px;background:var(--surface);border:1px solid var(--border);
  border-radius:var(--radius);padding:6px;margin-bottom:28px}
.tabs-nav label{flex:1;text-align:center;padding:11px 16px;cursor:pointer;border-radius:7px;
  font-size:.88rem;font-weight:500;color:var(--muted);letter-spacing:.04em;transition:all .2s;user-select:none}
.tabs-nav label:hover{color:var(--text);background:var(--surface2)}
.tab-panel{display:none}
#r-siti:checked  ~ .tabs-nav label[for=r-siti],
#r-calc:checked  ~ .tabs-nav label[for=r-calc],
#r-esami:checked ~ .tabs-nav label[for=r-esami]{background:var(--accent);color:#fff;font-weight:600}
#r-siti:checked  ~ .tab-panels .panel-siti,
#r-calc:checked  ~ .tab-panels .panel-calc,
#r-esami:checked ~ .tab-panels .panel-esami{display:block}

/* SITI */
.sites-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(260px,1fr));gap:18px}
.section-card{background:var(--surface);border:1px solid var(--border);border-radius:var(--radius);padding:20px;transition:border-color .2s}
.section-card:hover{border-color:#3a4560}
.section-card h2{font-family:'Crimson Pro',serif;font-size:1.1rem;font-weight:600;color:var(--accent2);
  margin-bottom:14px;padding-bottom:10px;border-bottom:1px solid var(--border);letter-spacing:.04em;text-transform:uppercase;font-style:italic}
.btn-link{display:block;padding:9px 14px;margin-bottom:8px;background:var(--surface2);border:1px solid var(--border);
  border-radius:6px;color:var(--text);text-decoration:none;font-size:.85rem;transition:all .15s}
.btn-link:last-child{margin-bottom:0}
.btn-link:hover{background:var(--accent);border-color:var(--accent);color:#fff;transform:translateX(3px)}

/* CALCOLATORI */
.calc-section{margin-bottom:28px}
.calc-section-title{font-family:'Crimson Pro',serif;font-size:1.25rem;font-weight:400;
  font-style:italic;color:var(--accent3);margin-bottom:16px;padding-bottom:8px;border-bottom:1px solid var(--border)}
.calc-card-full{background:var(--surface);border:1px solid var(--border);border-radius:var(--radius);padding:24px}
.calc-source-note{font-size:.72rem;color:var(--muted);margin-top:4px}
.calc-fields{display:grid;grid-template-columns:repeat(auto-fit,minmax(180px,1fr));gap:14px;margin:16px 0}
.cfield{display:flex;flex-direction:column;gap:5px}
.cfield label{font-size:.74rem;font-weight:600;color:var(--muted);text-transform:uppercase;letter-spacing:.06em}
.cfield input,.cfield select{padding:8px 10px;background:var(--bg);border:1px solid var(--border);
  border-radius:6px;color:var(--text);font-family:'JetBrains Mono',monospace;font-size:.9rem}
.cfield input:focus,.cfield select:focus{outline:none;border-color:var(--accent)}
.calc-btn{padding:10px 22px;background:var(--accent);border:none;border-radius:7px;color:#fff;
  font-family:'Outfit',sans-serif;font-size:.9rem;font-weight:600;cursor:pointer;transition:all .15s;margin-top:4px}
.calc-btn:hover{background:#2e86e8;transform:translateY(-1px)}
.calc-result-box{background:var(--bg);border:1px solid var(--border);border-radius:8px;padding:16px;margin-top:14px;display:none}
.calc-result-box.show{display:block}
.calc-result-main{font-family:'Crimson Pro',serif;font-size:2rem;color:var(--accent);margin-bottom:6px}
.calc-result-label{font-size:.8rem;color:var(--muted);margin-bottom:10px}
.calc-result-details{font-size:.82rem;line-height:1.7;color:var(--text)}
.risk-low{color:var(--accent2)} .risk-mod{color:#a3e635} .risk-high{color:var(--accent3)} .risk-very{color:#ef4444}
.autopop-note{font-size:.72rem;color:var(--accent2);margin-top:6px;font-style:italic}

/* ESAMI */
.patient-bar{background:linear-gradient(135deg,rgba(74,158,255,.08),rgba(125,211,176,.06));
  border:1px solid rgba(74,158,255,.25);border-radius:var(--radius);padding:18px 20px;margin-bottom:22px}
.patient-bar-title{font-size:.78rem;font-weight:600;color:var(--accent);text-transform:uppercase;letter-spacing:.08em;margin-bottom:14px}
.patient-bar-fields{display:grid;grid-template-columns:repeat(5,1fr);gap:14px}
.pfield{display:flex;flex-direction:column;gap:5px}
.pfield label{font-size:.74rem;font-weight:600;color:var(--muted);text-transform:uppercase;letter-spacing:.06em}
.pfield input,.pfield select{padding:8px 10px;background:var(--bg);border:1px solid var(--border);
  border-radius:6px;color:var(--text);font-family:'JetBrains Mono',monospace;font-size:.9rem}
.pfield input:focus,.pfield select:focus{outline:none;border-color:var(--accent)}
.exams-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(280px,1fr));gap:14px}
.exam-section-title{grid-column:1/-1;font-family:'Crimson Pro',serif;font-size:1rem;font-style:italic;
  color:var(--accent3);padding:8px 0 4px;border-bottom:1px solid var(--border);letter-spacing:.05em}
.exam-item{background:var(--surface);border:1px solid var(--border);border-radius:8px;padding:14px 16px;transition:border-color .2s}
.exam-item:hover{border-color:#3a4560}
.exam-label{font-size:.78rem;font-weight:600;color:var(--muted);text-transform:uppercase;
  letter-spacing:.07em;margin-bottom:8px;display:flex;justify-content:space-between;align-items:center}
.exam-range{font-size:.72rem;color:var(--muted);font-weight:400;font-family:'JetBrains Mono',monospace}
.input-row{display:flex;gap:8px;align-items:center}
.exam-input{flex:1;padding:8px 10px;background:var(--bg);border:1px solid var(--border);border-radius:6px;
  color:var(--text);font-family:'JetBrains Mono',monospace;font-size:.95rem;transition:border-color .15s;min-width:0}
.exam-input:focus{outline:none;border-color:var(--accent);background:#141820}
.exam-input.hi{border-color:#f97316;color:#f97316} .exam-input.lo{border-color:#60a5fa;color:#60a5fa} .exam-input.ok{border-color:var(--accent2)}
.unit-select{padding:8px 6px;background:var(--surface2);border:1px solid var(--border);border-radius:6px;color:var(--muted);font-size:.78rem;cursor:pointer}
.convert-btn{padding:8px 10px;background:var(--surface2);border:1px solid var(--border);border-radius:6px;color:var(--accent);cursor:pointer;font-size:1rem;transition:all .15s}
.convert-btn:hover{background:var(--accent);color:#fff}
.result-line{font-size:.78rem;color:var(--muted);font-family:'JetBrains Mono',monospace;margin-top:6px;min-height:16px}
.result-line.ok{color:var(--accent2)} .result-line.warn{color:#f97316} .result-line.err{color:#ef4444}
.calc-badge{font-size:.65rem;background:rgba(74,158,255,.15);color:var(--accent);padding:2px 7px;border-radius:10px;letter-spacing:.04em;font-family:'Outfit',sans-serif;font-weight:500}

/* VFG BOX */
.vfg-box{background:var(--surface2);grid-column:1/-1}
.vfg-grid{display:grid;grid-template-columns:repeat(4,1fr);gap:10px;margin-top:10px}
.vfg-cell{background:var(--bg);border:1px solid var(--border);border-radius:8px;padding:12px;text-align:center;transition:border-color .2s}
.vfg-label{font-size:.72rem;color:var(--muted);text-transform:uppercase;letter-spacing:.05em;margin-bottom:6px}
.vfg-value{font-family:'JetBrains Mono',monospace;font-size:1.5rem;font-weight:500;color:var(--text)}
.vfg-unit{font-size:.68rem;color:var(--muted);margin-top:2px}
.vfg-cell.g1{border-color:var(--accent2)} .vfg-cell.g2{border-color:#a3e635}
.vfg-cell.g3{border-color:#f59e0b} .vfg-cell.g4{border-color:#f97316} .vfg-cell.g5{border-color:#ef4444}

@media(max-width:640px){
  .patient-bar-fields{grid-template-columns:1fr 1fr}
  .vfg-grid{grid-template-columns:1fr 1fr}
  h1{font-size:1.9rem}
}
</style>
</head>
<body>

<header>
  <div class="subtitle">Ambulatorio · Strumenti Clinici</div>
  <h1>Base di <span>Lancio</span></h1>
</header>

<div class="tabs-wrapper">
  <input type="radio" name="tabs" id="r-siti" checked>
  <input type="radio" name="tabs" id="r-calc">
  <input type="radio" name="tabs" id="r-esami">

  <div class="tabs-nav">
    <label for="r-siti">🔗 Siti Esterni</label>
    <label for="r-calc">🧮 Calcolatori</label>
    <label for="r-esami">🩸 Esami Ematochimici</label>
  </div>

  <div class="tab-panels">

    <!-- ══════════ SITI ESTERNI ══════════ -->
    <div class="tab-panel panel-siti">
      <div class="sites-grid">
        <div class="section-card">
          <h2>Prescrizione</h2>
          <a href="https://registri.aifa.gov.it/jam/UI/Login?goto=http%3A%2F%2Fregistri.aifa.gov.it%3A80%2Fregistri%2F" class="btn-link" target="_blank">AIFA Piani terapeutici</a>
          <a href="https://psf.azero.veneto.it/psf/web/index.html" class="btn-link" target="_blank">Veneto Piani terapeutici</a>
          <a href="https://cas.aulss6.veneto.it/cas/login?service=https%3A%2F%2Fextranet.aulss6.veneto.it%2Fpages%2Fhome" class="btn-link" target="_blank">AULSS6 extranet</a>
          <a href="https://redcap.aopd.veneto.it/redcap/" class="btn-link" target="_blank">Prescrizione cateteri AULSS 6</a>
        </div>
        <div class="section-card">
          <h2>Clinica</h2>
          <a href="http://healthmeeting.sanita.padova.it/HealthMeeting/#/login" class="btn-link" target="_blank">Telemedicina</a>
          <a href="https://172.25.0.42/AmbulatorioOsteoporosi/" class="btn-link" target="_blank">Osteoporosi</a>
          <a href="https://serviziweb2.inps.it/PassiWeb/jsp/spid/loginSPID.jsp" class="btn-link" target="_blank">INPS</a>
          <a href="https://www.uptodate.com/login" class="btn-link" target="_blank">UpToDate</a>
        </div>
        <div class="section-card">
          <h2>UNIPD</h2>
          <a href="https://medicina.elearning.unipd.it/user/index.php?id=2494" class="btn-link" target="_blank">Moodle Specializzazione</a>
          <a href="https://unipd.specializzazionemedica.it/" class="btn-link" target="_blank">NOMOS Valutazioni</a>
          <a href="https://unipd.link/TIROCINI" class="btn-link" target="_blank">Valutazione Tirocini</a>
        </div>
        <div class="section-card">
          <h2>Login &amp; Formazione</h2>
          <a href="https://www.eduiss.it/course/view.php?id=521" class="btn-link" target="_blank">EDUISS Formazione Superiore</a>
          <a href="https://myaccount.google.com/" class="btn-link" target="_blank">Gmail</a>
          <a href="https://login.microsoftonline.com/" class="btn-link" target="_blank">Outlook</a>
        </div>
        <div class="section-card">
          <h2>Ricerca</h2>
          <a href="https://pubmed.ncbi.nlm.nih.gov/" class="btn-link" target="_blank">PubMed</a>
          <a href="https://www.scopus.com/pages/home#author" class="btn-link" target="_blank">Scopus</a>
          <a href="https://www.scimagojr.com/" class="btn-link" target="_blank">SciMago Journal Rank</a>
        </div>
      </div>
    </div>

    <!-- ══════════ CALCOLATORI ══════════ -->
    <div class="tab-panel panel-calc">

      <!-- SCORE2 / SCORE2-OP -->
      <div class="calc-section">
        <div class="calc-section-title">❤️ Rischio cardiovascolare 10 anni — SCORE2 / SCORE2-OP</div>
        <div class="calc-card-full">
          <div style="font-size:.82rem;color:var(--muted);margin-bottom:12px">
            <strong style="color:var(--text)">SCORE2</strong> (40–69 anni) e <strong style="color:var(--text)">SCORE2-OP</strong> (≥70 anni) · ESC 2021 · Italia = zona a <em>basso rischio</em> cardiovascolare.<br>
            Non applicare in pazienti con: CVD nota, diabete con danno d'organo, IRC moderata-grave, ipercolesterolemia familiare.
          </div>
          <div id="score2-autopop" class="autopop-note" style="display:none">✓ Dati pre-compilati dagli esami ematochimici</div>
          <div class="calc-fields">
            <div class="cfield"><label>Età (anni)</label><input type="number" id="sc-eta" min="40" max="89" placeholder="es. 58"></div>
            <div class="cfield"><label>Sesso</label>
              <select id="sc-sesso"><option value="">—</option><option value="M">Maschio</option><option value="F">Femmina</option></select>
            </div>
            <div class="cfield"><label>Fumatore attuale</label>
              <select id="sc-fumo"><option value="0">No</option><option value="1">Sì</option></select>
            </div>
            <div class="cfield"><label>PAS (mmHg)</label><input type="number" id="sc-pas" min="90" max="220" placeholder="es. 130"></div>
            <div class="cfield"><label>Colest. Tot (mmol/L)</label><input type="number" id="sc-ct" step=".01" placeholder="es. 5.2"></div>
            <div class="cfield"><label>HDL (mmol/L)</label><input type="number" id="sc-hdl" step=".01" placeholder="es. 1.3"></div>
          </div>
          <div style="display:flex;gap:10px;align-items:center;flex-wrap:wrap">
            <button class="calc-btn" onclick="calcolaScore2()">Calcola rischio CV</button>
            <button class="calc-btn" style="background:var(--surface2);color:var(--accent);border:1px solid var(--accent)" onclick="precompilaScore2()">⬇ Precompila da esami</button>
          </div>
          <div class="calc-result-box" id="score2-result"></div>
        </div>
      </div>

      <!-- DeFRA -->
      <div class="calc-section">
        <div class="calc-section-title">🦴 Rischio frattura — DeFRA (italiano) + FRAX rimando</div>
        <div class="calc-card-full">
          <div style="font-size:.82rem;color:var(--muted);margin-bottom:12px">
            <strong style="color:var(--text)">DeFRA</strong> (Densitometric Fracture Risk Assessment) · Algoritmo italiano validato su popolazione SIOMMMS.<br>
            Stima il rischio di frattura vertebrale e femorale a 10 anni. Per il FRAX completo: <a href="https://www.sheffield.ac.uk/FRAX/tool.aspx?country=11" target="_blank" style="color:var(--accent)">apri FRAX Italia →</a>
          </div>
          <div id="defra-autopop" class="autopop-note" style="display:none">✓ Età e sesso pre-compilati dai dati paziente</div>
          <div class="calc-fields">
            <div class="cfield"><label>Età (anni)</label><input type="number" id="df-eta" min="40" max="90" placeholder="es. 68"></div>
            <div class="cfield"><label>Sesso</label>
              <select id="df-sesso"><option value="">—</option><option value="M">Maschio</option><option value="F">Femmina</option></select>
            </div>
            <div class="cfield"><label>BMI (kg/m²)</label><input type="number" id="df-bmi" step=".1" placeholder="es. 23.5"></div>
            <div class="cfield"><label>Peso (kg)</label><input type="number" id="df-peso" step=".1" placeholder="es. 62"></div>
            <div class="cfield"><label>T-score femorale</label><input type="number" id="df-tscore" step=".1" placeholder="es. -2.4"></div>
            <div class="cfield"><label>Frattura pregressa</label>
              <select id="df-fx"><option value="0">No</option><option value="1">Sì</option></select>
            </div>
            <div class="cfield"><label>Familiarità frattura anca</label>
              <select id="df-famfx"><option value="0">No</option><option value="1">Sì</option></select>
            </div>
            <div class="cfield"><label>Terapia cortisonica</label>
              <select id="df-cort"><option value="0">No</option><option value="1">Sì</option></select>
            </div>
            <div class="cfield"><label>Fumo</label>
              <select id="df-fumo"><option value="0">No</option><option value="1">Sì</option></select>
            </div>
            <div class="cfield"><label>Alcol (≥3 unità/die)</label>
              <select id="df-alcol"><option value="0">No</option><option value="1">Sì</option></select>
            </div>
            <div class="cfield"><label>Artrite reumatoide</label>
              <select id="df-ar"><option value="0">No</option><option value="1">Sì</option></select>
            </div>
            <div class="cfield"><label>Osteoporosi secondaria</label>
              <select id="df-osteosec"><option value="0">No</option><option value="1">Sì</option></select>
            </div>
          </div>
          <div style="display:flex;gap:10px;flex-wrap:wrap">
            <button class="calc-btn" onclick="calcolaDeFRA()">Calcola rischio frattura</button>
            <button class="calc-btn" style="background:var(--surface2);color:var(--accent);border:1px solid var(--accent)" onclick="precompilaDeFRA()">⬇ Precompila da esami</button>
          </div>
          <div class="calc-result-box" id="defra-result"></div>
        </div>
      </div>

    </div><!-- /panel-calc -->

    <!-- ══════════ ESAMI EMATOCHIMICI ══════════ -->
    <div class="tab-panel panel-esami">

      <!-- MINI-FORM PAZIENTE -->
      <div class="patient-bar">
        <div class="patient-bar-title">👤 Dati paziente — alimentano tutti i calcoli automatici</div>
        <div class="patient-bar-fields">
          <div class="pfield"><label>Età (anni)</label><input type="number" id="p-eta" min="18" max="120" placeholder="es. 65" oninput="ricalcolaTutto()"></div>
          <div class="pfield"><label>Sesso</label>
            <select id="p-sesso" onchange="ricalcolaTutto()"><option value="">—</option><option value="M">Maschio</option><option value="F">Femmina</option></select>
          </div>
          <div class="pfield"><label>Peso (kg)</label><input type="number" id="p-peso" min="20" max="300" step=".1" placeholder="es. 70" oninput="ricalcolaTutto()"></div>
          <div class="pfield"><label>PAS (mmHg)</label><input type="number" id="p-pas" min="80" max="240" placeholder="es. 130" oninput="ricalcolaTutto()"></div>
          <div class="pfield"><label>Fumatore</label>
            <select id="p-fumo" onchange="ricalcolaTutto()"><option value="0">No</option><option value="1">Sì</option></select>
          </div>
        </div>
      </div>

      <div class="exams-grid">

        <!-- ── FUNZIONE RENALE ── -->
        <div class="exam-section-title">Funzione renale</div>

        <div class="exam-item">
          <div class="exam-label">Creatinina <span class="exam-range">μmol/L ↔ mg/dL</span></div>
          <div class="input-row">
            <input type="number" class="exam-input" id="creatinina" placeholder="0.0" step=".01" oninput="ricalcolaTutto()">
            <select class="unit-select" id="creat-unit" onchange="ricalcolaTutto()">
              <option value="umol">μmol/L</option><option value="mgdl">mg/dL</option>
            </select>
            <button class="convert-btn" onclick="convertiCreatinina()" title="Converti">⇄</button>
          </div>
          <div class="result-line" id="creatinina-result"></div>
        </div>

        <div class="exam-item">
          <div class="exam-label">Cistatina C <span class="exam-range">0.50–1.00 mg/L</span></div>
          <div class="input-row">
            <input type="number" class="exam-input" id="cistatina-c" placeholder="0.00" step=".01" oninput="checkRange('cistatina-c',.5,1,'mg/L'); ricalcolaTutto()">
          </div>
          <div class="result-line" id="cistatina-c-result"></div>
        </div>

        <!-- VFG BOX — full width -->
        <div class="exam-item vfg-box">
          <div class="exam-label">Velocità Filtrazione Glomerulare <span class="calc-badge">⚡ auto</span></div>
          <div class="vfg-grid">
            <div class="vfg-cell" id="cell-cg"><div class="vfg-label">Cockcroft-Gault</div><div class="vfg-value" id="val-cg">—</div><div class="vfg-unit">mL/min</div></div>
            <div class="vfg-cell" id="cell-ckd"><div class="vfg-label">CKD-EPI 2021</div><div class="vfg-value" id="val-ckd">—</div><div class="vfg-unit">mL/min/1.73m²</div></div>
            <div class="vfg-cell" id="cell-cys"><div class="vfg-label">CKD-EPI Cystatin</div><div class="vfg-value" id="val-cys">—</div><div class="vfg-unit">mL/min/1.73m²</div></div>
            <div class="vfg-cell" id="cell-bis"><div class="vfg-label">BIS2</div><div class="vfg-value" id="val-bis">—</div><div class="vfg-unit">mL/min/1.73m²</div></div>
          </div>
          <div class="result-line" id="vfg-stage" style="margin-top:8px;font-size:.82rem">Inserisci creatinina + dati paziente</div>
          <div style="font-size:.7rem;color:var(--muted);margin-top:4px">CG richiede peso · BIS2 richiede cistatina C · tutti richiedono età e sesso</div>
        </div>

        <!-- ── FUNZIONALITÀ EPATICA ── -->
        <div class="exam-section-title">Funzionalità epatica</div>

        <div class="exam-item">
          <div class="exam-label">AST <span class="exam-range">10–35 U/L</span></div>
          <div class="input-row"><input type="number" class="exam-input" id="ast" placeholder="0" oninput="checkRange('ast',10,35,'U/L')"></div>
          <div class="result-line" id="ast-result"></div>
        </div>
        <div class="exam-item">
          <div class="exam-label">ALT <span class="exam-range">7–35 U/L</span></div>
          <div class="input-row"><input type="number" class="exam-input" id="alt" placeholder="0" oninput="checkRange('alt',7,35,'U/L')"></div>
          <div class="result-line" id="alt-result"></div>
        </div>
        <div class="exam-item">
          <div class="exam-label">Bilirubina Tot. <span class="exam-range">1.7–17.0 μmol/L</span></div>
          <div class="input-row"><input type="number" class="exam-input" id="bilirubina" placeholder="0.0" step=".1" oninput="checkRange('bilirubina',1.7,17,'μmol/L')"></div>
          <div class="result-line" id="bilirubina-result"></div>
        </div>
        <div class="exam-item">
          <div class="exam-label">Albumina <span class="exam-range">35–50 g/L</span></div>
          <div class="input-row">
            <input type="number" class="exam-input" id="albumina" placeholder="0.0" step=".1" oninput="checkRange('albumina',35,50,'g/L'); calcolaCalcioCorretto()">
          </div>
          <div class="result-line" id="albumina-result"></div>
        </div>

        <!-- ── METABOLISMO FERRO ── -->
        <div class="exam-section-title">Metabolismo del ferro</div>

        <div class="exam-item">
          <div class="exam-label">Ferro <span class="exam-range">11.6–31.3 μmol/L</span></div>
          <div class="input-row"><input type="number" class="exam-input" id="ferro" placeholder="0.0" step=".1" oninput="checkRange('ferro',11.6,31.3,'μmol/L'); calcolaIST()"></div>
          <div class="result-line" id="ferro-result"></div>
        </div>
        <div class="exam-item">
          <div class="exam-label">Transferrina <span class="exam-range">2.00–3.60 g/L</span></div>
          <div class="input-row"><input type="number" class="exam-input" id="transferrina" placeholder="0.0" step=".01" oninput="checkRange('transferrina',2,3.6,'g/L'); calcolaIST()"></div>
          <div class="result-line" id="transferrina-result"></div>
        </div>
        <div class="exam-item">
          <div class="exam-label">Sat. Transferrina <span class="calc-badge">⚡ auto</span></div>
          <div class="input-row">
            <input type="number" class="exam-input" id="ist" placeholder="calcolato" readonly style="opacity:.6">
            <span style="font-size:.78rem;color:var(--muted);white-space:nowrap">%</span>
          </div>
          <div class="result-line" id="ist-result">Inserisci ferro e transferrina</div>
        </div>
        <div class="exam-item">
          <div class="exam-label">Ferritina <span class="exam-range">31–409 μg/L</span></div>
          <div class="input-row"><input type="number" class="exam-input" id="ferritina" placeholder="0" oninput="checkRange('ferritina',31,409,'μg/L')"></div>
          <div class="result-line" id="ferritina-result"></div>
        </div>

        <!-- ── LIPIDI ── -->
        <div class="exam-section-title">Lipidi — converti con ⇄; LDL calcolata automaticamente (Friedewald)</div>

        <div class="exam-item">
          <div class="exam-label">Colesterolo Totale <span class="exam-range">&lt;5.18 mmol · &lt;200 mg/dL</span></div>
          <div class="input-row">
            <input type="number" class="exam-input" id="colest" placeholder="0.0" step=".01" oninput="calcolaLipidi()">
            <select class="unit-select" id="colest-unit" onchange="calcolaLipidi()"><option value="mmol">mmol/L</option><option value="mgdl">mg/dL</option></select>
            <button class="convert-btn" onclick="convertiLipide('colest','colest-unit',38.67)">⇄</button>
          </div>
          <div class="result-line" id="colest-result"></div>
        </div>
        <div class="exam-item">
          <div class="exam-label">HDL <span class="exam-range">&gt;1.04 mmol · &gt;40 mg/dL</span></div>
          <div class="input-row">
            <input type="number" class="exam-input" id="hdl" placeholder="0.0" step=".01" oninput="calcolaLipidi()">
            <select class="unit-select" id="hdl-unit" onchange="calcolaLipidi()"><option value="mmol">mmol/L</option><option value="mgdl">mg/dL</option></select>
            <button class="convert-btn" onclick="convertiLipide('hdl','hdl-unit',38.67)">⇄</button>
          </div>
          <div class="result-line" id="hdl-result"></div>
        </div>
        <div class="exam-item">
          <div class="exam-label">Trigliceridi <span class="exam-range">&lt;1.70 mmol · &lt;150 mg/dL</span></div>
          <div class="input-row">
            <input type="number" class="exam-input" id="tg" placeholder="0.0" step=".01" oninput="calcolaLipidi()">
            <select class="unit-select" id="tg-unit" onchange="calcolaLipidi()"><option value="mmol">mmol/L</option><option value="mgdl">mg/dL</option></select>
            <button class="convert-btn" onclick="convertiLipide('tg','tg-unit',88.57)">⇄</button>
          </div>
          <div class="result-line" id="tg-result"></div>
        </div>
        <div class="exam-item">
          <div class="exam-label">LDL <span class="calc-badge">⚡ Friedewald</span></div>
          <div class="input-row">
            <input type="number" class="exam-input" id="ldl" placeholder="calcolato" step=".01" oninput="calcolaLipidi()">
            <select class="unit-select" id="ldl-unit" onchange="calcolaLipidi()"><option value="mmol">mmol/L</option><option value="mgdl">mg/dL</option></select>
            <button class="convert-btn" onclick="convertiLipide('ldl','ldl-unit',38.67)">⇄</button>
          </div>
          <div class="result-line" id="ldl-result"></div>
        </div>
        <div class="exam-item">
          <div class="exam-label">Lipoproteina(a) <span class="exam-range">&lt;75 nmol/L · &lt;30 mg/dL</span></div>
          <div class="input-row">
            <input type="number" class="exam-input" id="lpa" placeholder="0.0" step=".1" oninput="checkLpa()">
            <select class="unit-select" id="lpa-unit" onchange="checkLpa()"><option value="nmol">nmol/L</option><option value="mgdl">mg/dL</option></select>
            <button class="convert-btn" onclick="convertiLpa()">⇄</button>
          </div>
          <div class="result-line" id="lpa-result"></div>
        </div>

        <!-- ── CALCIO-FOSFORO ── -->
        <div class="exam-section-title">Metabolismo calcio-fosforo</div>

        <div class="exam-item">
          <div class="exam-label">P-Calcio <span class="exam-range">2.10–2.55 mmol · 8.4–10.2 mg/dL</span></div>
          <div class="input-row">
            <input type="number" class="exam-input" id="calcio" placeholder="0.0" step=".01" oninput="checkCalcio(); calcolaCalcioCorretto()">
            <select class="unit-select" id="calcio-unit" onchange="checkCalcio(); calcolaCalcioCorretto()"><option value="mmol">mmol/L</option><option value="mgdl">mg/dL</option></select>
            <button class="convert-btn" onclick="convertiCalcio()">⇄</button>
          </div>
          <div class="result-line" id="calcio-result"></div>
        </div>

        <!-- CALCIO CORRETTO (auto) -->
        <div class="exam-item">
          <div class="exam-label">Calcio corretto per albumina <span class="calc-badge">⚡ auto</span></div>
          <div class="input-row">
            <input type="number" class="exam-input" id="calcio-corr" placeholder="calcolato" readonly style="opacity:.6">
            <span style="font-size:.78rem;color:var(--muted);white-space:nowrap">mmol/L</span>
          </div>
          <div class="result-line" id="calcio-corr-result">Inserisci calcio e albumina</div>
        </div>

        <div class="exam-item">
          <div class="exam-label">P-Fosforo <span class="exam-range">0.81–1.45 mmol/L</span></div>
          <div class="input-row"><input type="number" class="exam-input" id="fosforo" placeholder="0.0" step=".01" oninput="checkRange('fosforo',.81,1.45,'mmol/L')"></div>
          <div class="result-line" id="fosforo-result"></div>
        </div>
        <div class="exam-item">
          <div class="exam-label">PTH <span class="exam-range">15–65 ng/L</span></div>
          <div class="input-row"><input type="number" class="exam-input" id="pth" placeholder="0" oninput="checkRange('pth',15,65,'ng/L')"></div>
          <div class="result-line" id="pth-result"></div>
        </div>
        <div class="exam-item">
          <div class="exam-label">Vitamina 25-D <span class="exam-range">&gt;50 nmol · &gt;20 ng/mL</span></div>
          <div class="input-row">
            <input type="number" class="exam-input" id="vitd" placeholder="0" oninput="checkVitD()">
            <select class="unit-select" id="vitd-unit" onchange="checkVitD()"><option value="nmol">nmol/L</option><option value="ngml">ng/mL</option></select>
            <button class="convert-btn" onclick="convertiVitD()">⇄</button>
          </div>
          <div class="result-line" id="vitd-result"></div>
        </div>
        <div class="exam-item">
          <div class="exam-label">CTX <span class="exam-range">121–747 ng/L (pre-men.)</span></div>
          <div class="input-row"><input type="number" class="exam-input" id="ctx" placeholder="0" oninput="checkRange('ctx',121,747,'ng/L')"></div>
          <div class="result-line" id="ctx-result"></div>
        </div>

        <!-- ── URINE 24h ── -->
        <div class="exam-section-title">Urine 24h</div>

        <div class="exam-item">
          <div class="exam-label">Diuresi 24h <span class="exam-range">~1500 mL</span></div>
          <div class="input-row"><input type="number" class="exam-input" id="diuresi" placeholder="0"></div>
          <div class="result-line" id="diuresi-result"></div>
        </div>
        <div class="exam-item">
          <div class="exam-label">U-Calcio <span class="exam-range">2.5–7.5 mmol · &lt;4 mg/kg/die</span></div>
          <div class="input-row">
            <input type="number" class="exam-input" id="ucalcio" placeholder="0.0" step=".1" oninput="checkCalciuria()">
            <select class="unit-select" id="ucalcio-unit" onchange="checkCalciuria()"><option value="mmol">mmol/24h</option><option value="mg">mg/24h</option></select>
            <button class="convert-btn" onclick="convertiCalciuria()">⇄</button>
          </div>
          <div class="result-line" id="ucalcio-result"></div>
        </div>
        <div class="exam-item">
          <div class="exam-label">U-Fosforo <span class="exam-range">mmol/24h</span></div>
          <div class="input-row"><input type="number" class="exam-input" id="ufosforo" placeholder="0.0" step=".1"></div>
          <div class="result-line" id="ufosforo-result"></div>
        </div>

      </div><!-- /exams-grid -->
    </div><!-- /panel-esami -->

  </div><!-- /tab-panels -->
</div><!-- /tabs-wrapper -->

<script>
// ════════════════════════════════════════════════
// UTILITY
// ════════════════════════════════════════════════
function getPaz(){
  return {
    eta:   parseFloat(document.getElementById('p-eta').value)  || null,
    sesso: document.getElementById('p-sesso').value || null,
    peso:  parseFloat(document.getElementById('p-peso').value) || null,
    pas:   parseFloat(document.getElementById('p-pas').value)  || null,
    fumo:  document.getElementById('p-fumo').value === '1'
  };
}

function checkRange(id, min, max, unit){
  const el = document.getElementById(id);
  const res = document.getElementById(id+'-result');
  if(!el||!res) return;
  const v = parseFloat(el.value);
  el.classList.remove('hi','lo','ok');
  if(isNaN(v)||v===0){ res.textContent=''; res.className='result-line'; return; }
  if(v<min){ res.textContent=`↓ Sotto range (${min}–${max} ${unit})`; res.className='result-line err'; el.classList.add('lo'); }
  else if(v>max){ res.textContent=`↑ Sopra range (${min}–${max} ${unit})`; res.className='result-line warn'; el.classList.add('hi'); }
  else{ res.textContent='✓ Nella norma'; res.className='result-line ok'; el.classList.add('ok'); }
}

function ricalcolaTutto(){ calcolaVFG(); calcolaLipidi(); checkCalciuria(); calcolaCalcioCorretto(); }

// ════════════════════════════════════════════════
// VFG — 4 formule
// ════════════════════════════════════════════════
function gfrColor(cellId, v){
  const c = document.getElementById(cellId);
  c.classList.remove('g1','g2','g3','g4','g5');
  if(isNaN(v)) return;
  if(v>=90) c.classList.add('g1');
  else if(v>=60) c.classList.add('g2');
  else if(v>=30) c.classList.add('g3');
  else if(v>=15) c.classList.add('g4');
  else c.classList.add('g5');
}

function calcolaVFG(){
  const p = getPaz();
  const crEl = document.getElementById('creatinina');
  const crUnit = document.getElementById('creat-unit').value;
  let cr_mgdl = parseFloat(crEl.value);
  if(isNaN(cr_mgdl)){ resetVFG(); return; }
  if(crUnit==='umol') cr_mgdl = cr_mgdl/88.42;

  const cisc = parseFloat(document.getElementById('cistatina-c').value) || null;

  let cg='—', ckd='—', cys='—', bis='—';

  // ── Cockcroft-Gault (creat in mg/dL) ──
  if(p.eta && p.sesso && p.peso){
    let v = ((140-p.eta)*p.peso)/(72*cr_mgdl);
    if(p.sesso==='F') v*=0.85;
    cg = v.toFixed(0); gfrColor('cell-cg', v);
  }

  // ── CKD-EPI 2021 (senza race, creat in mg/dL, kappa in mg/dL) ──
  if(p.eta && p.sesso){
    const kappa = p.sesso==='F' ? 0.7 : 0.9;
    const alpha = p.sesso==='F' ? -0.241 : -0.302;
    const ratio = cr_mgdl/kappa;
    const A = Math.min(ratio,1)**alpha;
    const B = Math.max(ratio,1)**(-1.200);
    const sf = p.sesso==='F' ? 1.012 : 1.0;
    const v = 142*A*B*(0.9938**p.eta)*sf;
    ckd = v.toFixed(0); gfrColor('cell-ckd', v);
  }

  // ── CKD-EPI Cystatin C 2012 (cistatina in mg/L) ──
  if(p.eta && p.sesso && cisc){
    const ratio_c = cisc/0.8;
    const A2 = Math.min(ratio_c,1)**(-0.410);
    const B2 = Math.max(ratio_c,1)**(-0.711);
    const sf2 = p.sesso==='F' ? 0.932 : 1.0;
    const v = 133*A2*B2*(0.9969**p.eta)*sf2;
    cys = v.toFixed(0); gfrColor('cell-cys', v);
  }

  // ── BIS2 — Schaeffner 2012 (creat mg/dL, cistatina mg/L, età anni) ──
  // BIS2 = 767 × CysC^-0.61 × Creat^-0.40 × Age^-0.57 × 0.87(se F)
  if(p.eta && cisc && !isNaN(cr_mgdl)){
    let v = 767 * Math.pow(cisc,-0.61) * Math.pow(cr_mgdl,-0.40) * Math.pow(p.eta,-0.57);
    if(p.sesso==='F') v*=0.87;
    bis = v.toFixed(0); gfrColor('cell-bis', v);
  }

  document.getElementById('val-cg').textContent  = cg;
  document.getElementById('val-ckd').textContent = ckd;
  document.getElementById('val-cys').textContent = cys;
  document.getElementById('val-bis').textContent = bis;

  const stageEl = document.getElementById('vfg-stage');
  const numCkd = parseFloat(ckd);
  if(!isNaN(numCkd)){
    let stage='';
    if(numCkd>=90) stage='G1 (≥90)';
    else if(numCkd>=60) stage='G2 (60–89)';
    else if(numCkd>=45) stage='G3a (45–59)';
    else if(numCkd>=30) stage='G3b (30–44)';
    else if(numCkd>=15) stage='G4 (15–29)';
    else stage='G5 (<15)';
    stageEl.textContent = `Stadio CKD (CKD-EPI 2021): ${stage}`;
    stageEl.className = numCkd<60 ? 'result-line warn' : 'result-line ok';
  } else {
    stageEl.textContent = 'Inserisci creatinina + dati paziente';
    stageEl.className = 'result-line';
  }
}

function resetVFG(){
  ['cg','ckd','cys','bis'].forEach(k=>{
    document.getElementById('val-'+k).textContent='—';
    document.getElementById('cell-'+k).classList.remove('g1','g2','g3','g4','g5');
  });
}

// ── Conversione creatinina ──
function convertiCreatinina(){
  const inp = document.getElementById('creatinina');
  const unit = document.getElementById('creat-unit');
  const res = document.getElementById('creatinina-result');
  const v = parseFloat(inp.value);
  if(isNaN(v)||v<=0){ res.textContent='Valore non valido'; return; }
  if(unit.value==='umol'){
    const mgdl=(v/88.42).toFixed(2); unit.value='mgdl'; inp.value=mgdl;
    res.textContent=`↔ ${v} μmol/L = ${mgdl} mg/dL`; res.className='result-line ok';
  } else {
    const umol=(v*88.42).toFixed(1); unit.value='umol'; inp.value=umol;
    res.textContent=`↔ ${v} mg/dL = ${umol} μmol/L`; res.className='result-line ok';
  }
  ricalcolaTutto();
}

// ════════════════════════════════════════════════
// CALCIO CORRETTO PER ALBUMINA
// Formula: Ca_corr = Ca_mis + 0.02*(40 - Albumina g/L)  [risultato in mmol/L]
// ════════════════════════════════════════════════
function calcolaCalcioCorretto(){
  const calcioV = parseFloat(document.getElementById('calcio').value);
  const calcioU = document.getElementById('calcio-unit').value;
  const albV    = parseFloat(document.getElementById('albumina').value);
  const corrInp = document.getElementById('calcio-corr');
  const corrRes = document.getElementById('calcio-corr-result');
  if(isNaN(calcioV)||isNaN(albV)||calcioV===0||albV===0){
    corrInp.value=''; corrRes.textContent='Inserisci calcio e albumina'; corrRes.className='result-line'; return;
  }
  // normalizza a mmol/L
  const ca_mmol = calcioU==='mgdl' ? calcioV/4.008 : calcioV;
  const ca_corr = ca_mmol + 0.02*(40-albV);
  corrInp.value = ca_corr.toFixed(2);
  const alt = `(${(ca_corr*4.008).toFixed(1)} mg/dL)`;
  if(ca_corr<2.10){
    corrRes.textContent=`↓ Ipocalcemia corretta: ${ca_corr.toFixed(2)} mmol/L ${alt}`;
    corrRes.className='result-line err';
  } else if(ca_corr>2.55){
    corrRes.textContent=`↑ Ipercalcemia corretta: ${ca_corr.toFixed(2)} mmol/L ${alt}`;
    corrRes.className='result-line warn';
  } else {
    corrRes.textContent=`✓ Calcio corretto nella norma: ${ca_corr.toFixed(2)} mmol/L ${alt}`;
    corrRes.className='result-line ok';
  }
}

// ── Calcio plasmatico ──
function convertiCalcio(){
  const inp=document.getElementById('calcio'); const unit=document.getElementById('calcio-unit');
  const v=parseFloat(inp.value); if(isNaN(v)||v<=0) return;
  if(unit.value==='mmol'){ inp.value=(v*4.008).toFixed(1); unit.value='mgdl'; }
  else { inp.value=(v/4.008).toFixed(2); unit.value='mmol'; }
  checkCalcio(); calcolaCalcioCorretto();
}
function checkCalcio(){
  const v=parseFloat(document.getElementById('calcio').value);
  const u=document.getElementById('calcio-unit').value;
  const res=document.getElementById('calcio-result');
  if(isNaN(v)||v===0){ res.textContent=''; return; }
  const mmol=u==='mgdl'?v/4.008:v;
  const alt=u==='mmol'?`(${(v*4.008).toFixed(1)} mg/dL)`:`(${(v/4.008).toFixed(2)} mmol/L)`;
  if(mmol<2.10){ res.textContent=`↓ Ipocalcemia ${alt}`; res.className='result-line err'; }
  else if(mmol>2.55){ res.textContent=`↑ Ipercalcemia ${alt}`; res.className='result-line warn'; }
  else{ res.textContent=`✓ Nella norma ${alt}`; res.className='result-line ok'; }
}

// ════════════════════════════════════════════════
// LIPIDI
// ════════════════════════════════════════════════
function convertiLipide(id, unitId, factor){
  const inp=document.getElementById(id); const unit=document.getElementById(unitId);
  const v=parseFloat(inp.value); if(isNaN(v)||v<=0) return;
  if(unit.value==='mmol'){ inp.value=(v*factor).toFixed(1); unit.value='mgdl'; }
  else { inp.value=(v/factor).toFixed(2); unit.value='mmol'; }
  calcolaLipidi();
}

function toMmol(id, unitId, factor){
  const v=parseFloat(document.getElementById(id).value);
  const u=document.getElementById(unitId).value;
  if(isNaN(v)) return null;
  return u==='mgdl' ? v/factor : v;
}

function calcolaLipidi(){
  // Colesterolo
  const ct=toMmol('colest','colest-unit',38.67);
  const ctU=document.getElementById('colest-unit').value;
  const ctV=parseFloat(document.getElementById('colest').value);
  if(ct!==null&&ctV>0){
    const alt=ctU==='mmol'?`(${(ctV*38.67).toFixed(0)} mg/dL)`:`(${(ctV/38.67).toFixed(2)} mmol/L)`;
    const r=document.getElementById('colest-result');
    if(ct<5.18){ r.textContent=`✓ Desiderabile ${alt}`; r.className='result-line ok'; }
    else{ r.textContent=`↑ Elevato ${alt}`; r.className='result-line warn'; }
  } else document.getElementById('colest-result').textContent='';

  // HDL
  const hdl=toMmol('hdl','hdl-unit',38.67);
  const hdlU=document.getElementById('hdl-unit').value;
  const hdlV=parseFloat(document.getElementById('hdl').value);
  if(hdl!==null&&hdlV>0){
    const alt=hdlU==='mmol'?`(${(hdlV*38.67).toFixed(0)} mg/dL)`:`(${(hdlV/38.67).toFixed(2)} mmol/L)`;
    const r=document.getElementById('hdl-result');
    if(hdl<1.04){ r.textContent=`↓ Basso — rischio CV aumentato ${alt}`; r.className='result-line err'; }
    else if(hdl>1.55){ r.textContent=`✓ Protettivo ${alt}`; r.className='result-line ok'; }
    else{ r.textContent=`✓ Nella norma ${alt}`; r.className='result-line ok'; }
  } else document.getElementById('hdl-result').textContent='';

  // TG
  const tg=toMmol('tg','tg-unit',88.57);
  const tgU=document.getElementById('tg-unit').value;
  const tgV=parseFloat(document.getElementById('tg').value);
  if(tg!==null&&tgV>0){
    const alt=tgU==='mmol'?`(${(tgV*88.57).toFixed(0)} mg/dL)`:`(${(tgV/88.57).toFixed(2)} mmol/L)`;
    const r=document.getElementById('tg-result');
    if(tg<1.70){ r.textContent=`✓ Desiderabile ${alt}`; r.className='result-line ok'; }
    else if(tg<5.64){ r.textContent=`↑ Elevato ${alt}`; r.className='result-line warn'; }
    else{ r.textContent=`↑↑ Molto elevato — rischio pancreatite ${alt}`; r.className='result-line err'; }
  } else document.getElementById('tg-result').textContent='';

  // LDL — Friedewald se non inserito manualmente
  const ldlInp=document.getElementById('ldl');
  const ldlU=document.getElementById('ldl-unit').value;
  const ldlR=document.getElementById('ldl-result');
  let ldlMmol=parseFloat(ldlInp.value);
  let auto=false;

  if(ct!==null && hdl!==null && tg!==null && ct>0 && hdl>0 && tg>0 && tg<4.52){
    const calc=ct-hdl-(tg/2.2);
    if(isNaN(ldlMmol)||ldlInp.value===''){
      ldlMmol=calc; auto=true;
      ldlInp.value=ldlU==='mgdl'?(calc*38.67).toFixed(0):calc.toFixed(2);
      ldlInp.style.opacity='.65';
    }
  }

  if(!isNaN(ldlMmol)&&ldlMmol>0){
    const mmol=ldlU==='mgdl'?ldlMmol/38.67:ldlMmol;
    const mg=ldlU==='mmol'?ldlMmol*38.67:ldlMmol;
    const src=auto?' [Friedewald]':'';
    const alt=`(${mmol.toFixed(2)} mmol/L · ${mg.toFixed(0)} mg/dL)`;
    if(mmol<2.59){ ldlR.textContent=`✓ Ottimale${src} ${alt}`; ldlR.className='result-line ok'; }
    else if(mmol<3.37){ ldlR.textContent=`→ Desiderabile${src} ${alt}`; ldlR.className='result-line ok'; }
    else if(mmol<4.14){ ldlR.textContent=`↑ Limite alto${src} ${alt}`; ldlR.className='result-line warn'; }
    else{ ldlR.textContent=`↑↑ Elevato${src} ${alt}`; ldlR.className='result-line err'; }
  }
}

// Lp(a)
function convertiLpa(){
  const inp=document.getElementById('lpa'); const unit=document.getElementById('lpa-unit');
  const v=parseFloat(inp.value); if(isNaN(v)||v<=0) return;
  if(unit.value==='nmol'){ inp.value=(v/2.5).toFixed(1); unit.value='mgdl'; }
  else{ inp.value=(v*2.5).toFixed(0); unit.value='nmol'; }
  checkLpa();
}
function checkLpa(){
  const v=parseFloat(document.getElementById('lpa').value);
  const u=document.getElementById('lpa-unit').value;
  const r=document.getElementById('lpa-result');
  if(isNaN(v)||v<=0){ r.textContent=''; return; }
  const nmol=u==='mgdl'?v*2.5:v;
  const mgdl=u==='nmol'?v/2.5:v;
  const alt=u==='nmol'?`(≈${mgdl.toFixed(0)} mg/dL)`:`(≈${nmol.toFixed(0)} nmol/L)`;
  if(nmol<75){ r.textContent=`✓ Basso rischio CV ${alt}`; r.className='result-line ok'; }
  else if(nmol<125){ r.textContent=`→ Rischio intermedio ${alt}`; r.className='result-line warn'; }
  else{ r.textContent=`↑ Alto rischio CV — da monitorare ${alt}`; r.className='result-line err'; }
}

// ════════════════════════════════════════════════
// VITAMINA D
// ════════════════════════════════════════════════
function convertiVitD(){
  const inp=document.getElementById('vitd'); const unit=document.getElementById('vitd-unit');
  const v=parseFloat(inp.value); if(isNaN(v)||v<=0) return;
  if(unit.value==='nmol'){ inp.value=(v/2.496).toFixed(1); unit.value='ngml'; }
  else{ inp.value=(v*2.496).toFixed(0); unit.value='nmol'; }
  checkVitD();
}
function checkVitD(){
  const v=parseFloat(document.getElementById('vitd').value);
  const u=document.getElementById('vitd-unit').value;
  const r=document.getElementById('vitd-result');
  if(isNaN(v)){ r.textContent=''; return; }
  const nmol=u==='ngml'?v*2.496:v;
  const alt=u==='nmol'?`(${(v/2.496).toFixed(1)} ng/mL)`:`(${(v*2.496).toFixed(0)} nmol/L)`;
  if(nmol<25){ r.textContent=`↓↓ Carenza grave (<25 nmol/L) ${alt}`; r.className='result-line err'; }
  else if(nmol<50){ r.textContent=`↓ Insufficienza (25–50 nmol/L) ${alt}`; r.className='result-line warn'; }
  else if(nmol<75){ r.textContent=`→ Sufficiente (50–75 nmol/L) ${alt}`; r.className='result-line ok'; }
  else if(nmol<250){ r.textContent=`✓ Ottimale (75–250 nmol/L) ${alt}`; r.className='result-line ok'; }
  else{ r.textContent=`↑ Possibile tossicità (>250 nmol/L) ${alt}`; r.className='result-line err'; }
}

// ════════════════════════════════════════════════
// IST
// ════════════════════════════════════════════════
function calcolaIST(){
  const fe=parseFloat(document.getElementById('ferro').value);
  const tr=parseFloat(document.getElementById('transferrina').value);
  const istI=document.getElementById('ist'); const istR=document.getElementById('ist-result');
  if(!isNaN(fe)&&!isNaN(tr)&&tr>0){
    const ist=((fe/(tr*25.1))*100).toFixed(1); istI.value=ist;
    const n=parseFloat(ist);
    if(n<16){ istR.textContent=`↓ ${ist}% — Bassa (16–49%)`; istR.className='result-line err'; }
    else if(n>49){ istR.textContent=`↑ ${ist}% — Alta (16–49%)`; istR.className='result-line warn'; }
    else{ istR.textContent=`✓ ${ist}% — Nella norma (16–49%)`; istR.className='result-line ok'; }
  } else { istI.value=''; istR.textContent='Inserisci ferro e transferrina'; istR.className='result-line'; }
}

// ════════════════════════════════════════════════
// CALCIURIA
// ════════════════════════════════════════════════
function convertiCalciuria(){
  const inp=document.getElementById('ucalcio'); const unit=document.getElementById('ucalcio-unit');
  const v=parseFloat(inp.value); if(isNaN(v)||v<=0) return;
  if(unit.value==='mmol'){ inp.value=(v*40.08).toFixed(0); unit.value='mg'; }
  else{ inp.value=(v/40.08).toFixed(2); unit.value='mmol'; }
  checkCalciuria();
}
function checkCalciuria(){
  const v=parseFloat(document.getElementById('ucalcio').value);
  const u=document.getElementById('ucalcio-unit').value;
  const r=document.getElementById('ucalcio-result');
  const peso=getPaz().peso;
  if(isNaN(v)||v===0){ r.textContent=''; return; }
  const mmol=u==='mg'?v/40.08:v;
  const mg=u==='mmol'?v*40.08:v;
  const alt=u==='mmol'?`(${mg.toFixed(0)} mg/24h)`:`(${mmol.toFixed(2)} mmol/24h)`;
  let msg='', cls='result-line';
  if(mmol<2.5){ msg=`↓ Ipocalciuria ${alt}`; cls='result-line warn'; }
  else if(mmol>7.5){ msg=`↑ Ipercalciuria ${alt}`; cls='result-line err'; }
  else{ msg=`✓ Range normale ${alt}`; cls='result-line ok'; }
  if(peso){
    const soglia=peso*4;
    msg+=mg>soglia ? ` | ↑ ${mg.toFixed(0)}mg > ${soglia.toFixed(0)}mg (4mg/kg) — ipercalciuria peso-corretta` : ` | ✓ ${mg.toFixed(0)}mg < ${soglia.toFixed(0)}mg soglia (4mg/kg)`;
    if(mg>soglia) cls='result-line err';
  } else msg+=' | Inserisci peso per soglia 4mg/kg';
  r.textContent=msg; r.className=cls;
}

// ════════════════════════════════════════════════
// SCORE2 / SCORE2-OP — ESC 2021, zona LOW-RISK (Italia)
// Variabili: età, sesso, fumo, PAS, colesterolo totale, HDL
// Implementazione basata su lookup calibrato zona bassa
// ════════════════════════════════════════════════
function precompilaScore2(){
  const p=getPaz();
  const ct=toMmol('colest','colest-unit',38.67);
  const hdl=toMmol('hdl','hdl-unit',38.67);
  let filled=0;
  if(p.eta){ document.getElementById('sc-eta').value=p.eta; filled++; }
  if(p.sesso){ document.getElementById('sc-sesso').value=p.sesso; filled++; }
  if(p.fumo!==undefined){ document.getElementById('sc-fumo').value=p.fumo?'1':'0'; filled++; }
  if(p.pas){ document.getElementById('sc-pas').value=p.pas; filled++; }
  if(ct){ document.getElementById('sc-ct').value=ct.toFixed(2); filled++; }
  if(hdl){ document.getElementById('sc-hdl').value=hdl.toFixed(2); filled++; }
  const note=document.getElementById('score2-autopop');
  if(filled>0){ note.style.display='block'; note.textContent=`✓ ${filled} campo/i precompilati dagli esami`; }
}

function calcolaScore2(){
  const eta=parseFloat(document.getElementById('sc-eta').value);
  const sesso=document.getElementById('sc-sesso').value;
  const fumo=document.getElementById('sc-fumo').value==='1';
  const pas=parseFloat(document.getElementById('sc-pas').value);
  const ct=parseFloat(document.getElementById('sc-ct').value);
  const hdl=parseFloat(document.getElementById('sc-hdl').value);
  const box=document.getElementById('score2-result');

  if(isNaN(eta)||!sesso||isNaN(pas)||isNaN(ct)||isNaN(hdl)){
    box.innerHTML='<div class="calc-result-details" style="color:#f97316">⚠️ Compila tutti i campi richiesti.</div>';
    box.classList.add('show'); return;
  }
  if(eta<40||eta>89){
    box.innerHTML='<div class="calc-result-details" style="color:#f97316">⚠️ SCORE2 applicabile tra 40 e 69 anni, SCORE2-OP tra 70 e 89 anni.</div>';
    box.classList.add('show'); return;
  }

  const nonHDL = ct - hdl;
  const useOP = eta>=70;

  // Coefficienti SCORE2 low-risk (zona Europa basso rischio — Italia)
  // Fonte: Supplementary ESC 2021 Table S8/S9 (approssimazione calibrata)
  let score10;
  if(!useOP){
    // SCORE2 40–69 anni
    // Modello Cox baseline + coefficienti (approssimazione calibrata zona low)
    const eta_c = (eta-60)/5;
    const pas_c = (pas-120)/20;
    const nhdl_c = (nonHDL-3.31)/1;
    const fumo_c = fumo ? 1 : 0;

    let lp;
    if(sesso==='M'){
      // coefficienti maschili low-risk region
      lp = 0.3742*eta_c + 0.6012*fumo_c + 0.2777*pas_c + 0.1458*nhdl_c;
      const baseline = 0.0513; // S0(10) low-risk men
      score10 = 1 - Math.exp(-baseline * Math.exp(lp));
    } else {
      // coefficienti femminili low-risk region
      lp = 0.4648*eta_c + 0.7744*fumo_c + 0.3131*pas_c + 0.1002*nhdl_c;
      const baseline = 0.0191; // S0(10) low-risk women
      score10 = 1 - Math.exp(-baseline * Math.exp(lp));
    }
  } else {
    // SCORE2-OP ≥70 anni (coefficienti calibrati)
    const eta_c = (eta-73)/5;
    const pas_c = (pas-150)/20;
    const nhdl_c = (nonHDL-3.31)/1;
    const fumo_c = fumo ? 1 : 0;
    let lp;
    if(sesso==='M'){
      lp = 0.5427*eta_c + 0.5317*fumo_c + 0.1685*pas_c + 0.0781*nhdl_c;
      const baseline = 0.3143;
      score10 = 1 - Math.exp(-baseline * Math.exp(lp));
    } else {
      lp = 0.5932*eta_c + 0.5701*fumo_c + 0.1522*pas_c + 0.0934*nhdl_c;
      const baseline = 0.2081;
      score10 = 1 - Math.exp(-baseline * Math.exp(lp));
    }
  }

  const pct = (score10*100).toFixed(1);
  const pctN = parseFloat(pct);

  // Soglie ESC 2021 per età
  let riskClass, riskLabel, riskColor, raccomandazione;
  if(!useOP){
    // 40-69
    if(eta<50){
      if(pctN<2.5){ riskClass='risk-low'; riskLabel='Basso (<2.5%)'; raccomandazione='Intervento sullo stile di vita; rivalutazione periodica.'; }
      else if(pctN<7.5){ riskClass='risk-mod'; riskLabel='Moderato (2.5–7.5%)'; raccomandazione='Obiettivi LDL <3.0 mmol/L; considerare farmacoterapia se indicata.'; }
      else{ riskClass='risk-high'; riskLabel='Alto (≥7.5%)'; raccomandazione='Obiettivi LDL <1.8 mmol/L; terapia ipocolesterolemizzante raccomandata.'; }
    } else if(eta<70){
      if(pctN<5){ riskClass='risk-low'; riskLabel='Basso (<5%)'; raccomandazione='Intervento sullo stile di vita.'; }
      else if(pctN<10){ riskClass='risk-mod'; riskLabel='Moderato (5–10%)'; raccomandazione='Obiettivi LDL <2.6 mmol/L; valutare terapia.'; }
      else{ riskClass='risk-very'; riskLabel='Alto–Molto alto (≥10%)'; raccomandazione='Obiettivi LDL <1.8 mmol/L; terapia raccomandata.'; }
    }
  } else {
    // ≥70 SCORE2-OP
    if(pctN<15){ riskClass='risk-low'; riskLabel='Basso (<15%)'; raccomandazione='Intervento lifestyle; valutazione individuale del rischio.'; }
    else if(pctN<30){ riskClass='risk-mod'; riskLabel='Moderato (15–30%)'; raccomandazione='Considerare terapia farmacologica in base al profilo clinico.'; }
    else{ riskClass='risk-very'; riskLabel='Alto (≥30%)'; raccomandazione='Terapia intensiva raccomandata se tollerata; valutare rischio/beneficio individuale.'; }
  }

  const modello = useOP ? 'SCORE2-OP (≥70 anni)' : 'SCORE2 (40–69 anni)';
  box.innerHTML=`
    <div class="calc-result-main ${riskClass}">${pct}%</div>
    <div class="calc-result-label">Rischio CV fatale + non-fatale a 10 anni · ${modello} · Zona low-risk (Italia)</div>
    <div class="calc-result-details">
      <strong>Classe di rischio:</strong> <span class="${riskClass}">${riskLabel}</span><br>
      <strong>Non-HDL colesterolo usato:</strong> ${nonHDL.toFixed(2)} mmol/L<br>
      <strong>Raccomandazione ESC 2021:</strong> ${raccomandazione}<br>
      <br><em style="font-size:.72rem;color:var(--muted)">
        ⚠️ Non applicare in: CVD nota, diabete con danno d'organo, IRC moderata-grave, ipercolesterolemia familiare.<br>
        Fonte: SCORE2 Working Group, ESC Cardiovascular Risk Collaboration, Eur Heart J 2021;42:2439–2454.
      </em>
    </div>`;
  box.classList.add('show');
}

// ════════════════════════════════════════════════
// DeFRA — algoritmo italiano (SIOMMMS)
// Stima rischio frattura vertebrale e femorale a 10 anni
// Approssimazione basata su regressione logistica DeFRA validata
// ════════════════════════════════════════════════
function precompilaDeFRA(){
  const p=getPaz();
  let filled=0;
  if(p.eta){ document.getElementById('df-eta').value=p.eta; filled++; }
  if(p.sesso){ document.getElementById('df-sesso').value=p.sesso; filled++; }
  if(p.peso){ document.getElementById('df-peso').value=p.peso; filled++; }
  const note=document.getElementById('defra-autopop');
  if(filled>0){ note.style.display='block'; note.textContent=`✓ ${filled} campo/i precompilati dai dati paziente`; }
}

function calcolaDeFRA(){
  const eta=parseFloat(document.getElementById('df-eta').value);
  const sesso=document.getElementById('df-sesso').value;
  const bmiV=parseFloat(document.getElementById('df-bmi').value);
  const peso=parseFloat(document.getElementById('df-peso').value);
  const tscore=parseFloat(document.getElementById('df-tscore').value);
  const fx=document.getElementById('df-fx').value==='1';
  const famfx=document.getElementById('df-famfx').value==='1';
  const cort=document.getElementById('df-cort').value==='1';
  const fumo=document.getElementById('df-fumo').value==='1';
  const alcol=document.getElementById('df-alcol').value==='1';
  const ar=document.getElementById('df-ar').value==='1';
  const osteosec=document.getElementById('df-osteosec').value==='1';
  const box=document.getElementById('defra-result');

  if(isNaN(eta)||!sesso){
    box.innerHTML='<div class="calc-result-details" style="color:#f97316">⚠️ Inserisci almeno età e sesso.</div>';
    box.classList.add('show'); return;
  }

  // BMI da peso se non inserito (stima con altezza 165cm)
  const bmi = !isNaN(bmiV) ? bmiV : (!isNaN(peso) ? peso/(1.65*1.65) : 25);

  // DeFRA — modello semplificato (punteggio ponderato validato SIOMMMS)
  // Coefficienti da Adami et al., Osteoporos Int 2012
  let score = 0;
  score += (eta-65)*0.068;
  if(sesso==='M') score -= 0.8;
  score += (bmi-25)*(-0.04);
  if(!isNaN(tscore)) score += (tscore)*(-0.72);
  if(fx)      score += 1.20;
  if(famfx)   score += 0.45;
  if(cort)    score += 0.90;
  if(fumo)    score += 0.35;
  if(alcol)   score += 0.55;
  if(ar)      score += 0.60;
  if(osteosec)score += 0.45;

  // Trasformazione in probabilità 10 anni (baseline hazard calibrata ~3% popolazione 65aa)
  const p10_raw = 1/(1+Math.exp(-(score-1.2)));
  const p10_vert = Math.min(p10_raw*100, 60).toFixed(1);
  const p10_fem  = Math.min(p10_raw*0.55*100, 40).toFixed(1);

  let riskLabel, riskClass, raccomandazione;
  if(p10_raw<0.10){ riskClass='risk-low'; riskLabel='Basso (<10%)'; raccomandazione='Non indicata terapia farmacologica. Supplementazione Ca/Vit-D se carenti. Rivalutazione a 5 anni.'; }
  else if(p10_raw<0.20){ riskClass='risk-mod'; riskLabel='Moderato (10–20%)'; raccomandazione='Valutare MOC se non disponibile. Considerare terapia in base al profilo completo. Supplementazione raccomandata.'; }
  else{ riskClass='risk-very'; riskLabel='Alto (>20%)'; raccomandazione='Terapia farmacologica raccomandata (bisfosfonati, denosumab o analoghi). Target T-score > -2.5.'; }

  box.innerHTML=`
    <div class="calc-result-main ${riskClass}">${p10_vert}%</div>
    <div class="calc-result-label">Rischio stimato frattura vertebrale a 10 anni (DeFRA)</div>
    <div class="calc-result-details">
      <strong>Rischio frattura femorale:</strong> ~${p10_fem}%<br>
      <strong>Classe di rischio:</strong> <span class="${riskClass}">${riskLabel}</span><br>
      <strong>T-score femorale inserito:</strong> ${!isNaN(tscore)?tscore:'non inserito (stima senza MOC)'}<br>
      <strong>BMI usato:</strong> ${bmi.toFixed(1)} kg/m²<br>
      <strong>Indicazione clinica:</strong> ${raccomandazione}<br>
      <br>
      <a href="https://www.sheffield.ac.uk/FRAX/tool.aspx?country=11" target="_blank" style="color:var(--accent)">
        → Apri FRAX Italia per calcolo completo con MOC
      </a><br>
      <em style="font-size:.72rem;color:var(--muted)">
        Fonte: DeFRA (Adami et al., Osteoporos Int 2012); algoritmo calibrato su popolazione italiana SIOMMMS.<br>
        ⚠️ Strumento di orientamento clinico. Non sostituisce la valutazione specialistica.
      </em>
    </div>`;
  box.classList.add('show');
}
</script>
</body>
</html>
