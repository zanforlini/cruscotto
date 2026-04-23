<!DOCTYPE html>
<html lang="it">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Base di Lancio</title>
<link href="https://fonts.googleapis.com/css2?family=Crimson+Pro:ital,wght@0,300;0,400;0,600;1,300&family=JetBrains+Mono:wght@400;500&family=Outfit:wght@300;400;500;600&display=swap" rel="stylesheet">
<style>
  :root {
    --bg: #0f1117;
    --surface: #181c27;
    --surface2: #1e2436;
    --accent: #4a9eff;
    --accent2: #7dd3b0;
    --accent3: #f0a05a;
    --text: #e8eaf0;
    --text-muted: #7a8099;
    --border: #2a3048;
    --tab-active: #4a9eff;
    --radius: 10px;
  }

  * { box-sizing: border-box; margin: 0; padding: 0; }

  body {
    font-family: 'Outfit', sans-serif;
    background: var(--bg);
    color: var(--text);
    min-height: 100vh;
    background-image: 
      radial-gradient(ellipse at 20% 0%, rgba(74,158,255,0.07) 0%, transparent 50%),
      radial-gradient(ellipse at 80% 100%, rgba(125,211,176,0.05) 0%, transparent 50%);
  }

  /* ── HEADER ── */
  header {
    padding: 36px 40px 0;
    text-align: center;
    position: relative;
  }
  header::after {
    content: '';
    display: block;
    width: 60px;
    height: 2px;
    background: linear-gradient(90deg, var(--accent), var(--accent2));
    margin: 18px auto 0;
    border-radius: 2px;
  }
  h1 {
    font-family: 'Crimson Pro', serif;
    font-size: 2.8rem;
    font-weight: 300;
    letter-spacing: 0.08em;
    color: var(--text);
    text-transform: uppercase;
  }
  h1 span {
    font-style: italic;
    color: var(--accent);
    font-weight: 300;
  }
  .subtitle {
    font-size: 0.82rem;
    color: var(--text-muted);
    letter-spacing: 0.15em;
    text-transform: uppercase;
    margin-top: 6px;
    font-weight: 300;
  }

  /* ── TABS SYSTEM (CSS-only, fixed mapping) ── */
  .tabs-wrapper {
    max-width: 1000px;
    margin: 36px auto 0;
    padding: 0 20px 60px;
  }

  /* hidden radios */
  .tabs-wrapper input[type="radio"] { display: none; }

  /* tab bar */
  .tabs-nav {
    display: flex;
    gap: 4px;
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: var(--radius);
    padding: 6px;
    margin-bottom: 28px;
  }
  .tabs-nav label {
    flex: 1;
    text-align: center;
    padding: 11px 16px;
    cursor: pointer;
    border-radius: 7px;
    font-size: 0.88rem;
    font-weight: 500;
    color: var(--text-muted);
    letter-spacing: 0.04em;
    transition: all 0.2s;
    user-select: none;
  }
  .tabs-nav label:hover { color: var(--text); background: var(--surface2); }

  /* content panels */
  .tab-panel { display: none; }

  /* ── CORRECT MAPPING ──
     tab-siti   → radio #r-siti   → panel .panel-siti
     tab-calc   → radio #r-calc   → panel .panel-calc
     tab-esami  → radio #r-esami  → panel .panel-esami
  */
  #r-siti:checked  ~ .tabs-nav label[for="r-siti"],
  #r-calc:checked  ~ .tabs-nav label[for="r-calc"],
  #r-esami:checked ~ .tabs-nav label[for="r-esami"] {
    background: var(--accent);
    color: #fff;
    font-weight: 600;
  }
  #r-siti:checked  ~ .tab-panels .panel-siti,
  #r-calc:checked  ~ .tab-panels .panel-calc,
  #r-esami:checked ~ .tab-panels .panel-esami {
    display: block;
  }

  /* ── SITI ESTERNI ── */
  .sites-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
    gap: 18px;
  }
  .section-card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: var(--radius);
    padding: 20px;
    transition: border-color 0.2s;
  }
  .section-card:hover { border-color: #3a4560; }
  .section-card h2 {
    font-family: 'Crimson Pro', serif;
    font-size: 1.1rem;
    font-weight: 600;
    color: var(--accent2);
    margin-bottom: 14px;
    padding-bottom: 10px;
    border-bottom: 1px solid var(--border);
    letter-spacing: 0.04em;
    text-transform: uppercase;
    font-style: italic;
  }
  .btn-link {
    display: block;
    padding: 9px 14px;
    margin-bottom: 8px;
    background: var(--surface2);
    border: 1px solid var(--border);
    border-radius: 6px;
    color: var(--text);
    text-decoration: none;
    font-size: 0.85rem;
    font-weight: 400;
    transition: all 0.15s;
  }
  .btn-link:last-child { margin-bottom: 0; }
  .btn-link:hover {
    background: var(--accent);
    border-color: var(--accent);
    color: white;
    transform: translateX(3px);
  }

  /* ── CALCOLATORI (placeholder) ── */
  .placeholder-box {
    background: var(--surface);
    border: 1px dashed var(--border);
    border-radius: var(--radius);
    padding: 60px 40px;
    text-align: center;
    color: var(--text-muted);
  }
  .placeholder-box .icon { font-size: 2.5rem; margin-bottom: 14px; }
  .placeholder-box h3 { font-family: 'Crimson Pro', serif; font-size: 1.4rem; font-weight: 300; margin-bottom: 8px; color: var(--text); }
  .placeholder-box p { font-size: 0.88rem; line-height: 1.6; }
  .calc-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
    gap: 16px;
    margin-top: 24px;
  }
  .calc-card {
    background: var(--surface2);
    border: 1px solid var(--border);
    border-radius: var(--radius);
    padding: 20px;
    text-align: center;
    cursor: pointer;
    transition: all 0.2s;
    opacity: 0.5;
  }
  .calc-card .calc-icon { font-size: 1.8rem; margin-bottom: 8px; }
  .calc-card h4 { font-size: 0.9rem; font-weight: 600; margin-bottom: 4px; }
  .calc-card p { font-size: 0.76rem; color: var(--text-muted); }
  .calc-card.coming { border-style: dashed; }
  .coming-label {
    display: inline-block;
    font-size: 0.68rem;
    background: var(--surface);
    border: 1px solid var(--border);
    color: var(--text-muted);
    padding: 2px 8px;
    border-radius: 20px;
    margin-top: 6px;
    letter-spacing: 0.05em;
    text-transform: uppercase;
  }

  /* ── ESAMI EMATOCHIMICI ── */
  .exams-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    gap: 14px;
  }
  .exam-item {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 8px;
    padding: 14px 16px;
    transition: border-color 0.2s;
  }
  .exam-item:hover { border-color: #3a4560; }
  .exam-label {
    font-size: 0.78rem;
    font-weight: 600;
    color: var(--text-muted);
    text-transform: uppercase;
    letter-spacing: 0.07em;
    margin-bottom: 8px;
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  .exam-range {
    font-size: 0.72rem;
    color: var(--text-muted);
    font-weight: 400;
    font-family: 'JetBrains Mono', monospace;
  }
  .input-row {
    display: flex;
    gap: 8px;
    align-items: center;
  }
  .exam-input {
    flex: 1;
    padding: 8px 10px;
    background: var(--bg);
    border: 1px solid var(--border);
    border-radius: 6px;
    color: var(--text);
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.95rem;
    transition: border-color 0.15s;
    min-width: 0;
  }
  .exam-input:focus {
    outline: none;
    border-color: var(--accent);
    background: #141820;
  }
  .exam-input.out-of-range { border-color: #e74c3c; color: #e74c3c; }
  .exam-input.in-range { border-color: var(--accent2); }

  .unit-select {
    padding: 8px 6px;
    background: var(--surface2);
    border: 1px solid var(--border);
    border-radius: 6px;
    color: var(--text-muted);
    font-size: 0.78rem;
    cursor: pointer;
  }
  .convert-btn {
    padding: 8px 10px;
    background: var(--surface2);
    border: 1px solid var(--border);
    border-radius: 6px;
    color: var(--accent);
    cursor: pointer;
    font-size: 1rem;
    transition: all 0.15s;
  }
  .convert-btn:hover { background: var(--accent); color: white; }

  .result-line {
    font-size: 0.78rem;
    color: var(--text-muted);
    font-family: 'JetBrains Mono', monospace;
    margin-top: 6px;
    min-height: 16px;
  }
  .result-line.ok { color: var(--accent2); }
  .result-line.warn { color: #e67e22; }
  .result-line.err { color: #e74c3c; }

  /* section dividers within exams */
  .exam-section-title {
    grid-column: 1 / -1;
    font-family: 'Crimson Pro', serif;
    font-size: 1rem;
    font-style: italic;
    color: var(--accent3);
    padding: 8px 0 4px;
    border-bottom: 1px solid var(--border);
    letter-spacing: 0.05em;
  }

  /* calculated badge */
  .calc-badge {
    font-size: 0.65rem;
    background: rgba(74,158,255,0.15);
    color: var(--accent);
    padding: 2px 7px;
    border-radius: 10px;
    letter-spacing: 0.04em;
    font-family: 'Outfit', sans-serif;
    font-weight: 500;
  }

  @media (max-width: 600px) {
    h1 { font-size: 1.9rem; }
    .tabs-nav { flex-direction: column; }
    .exams-grid { grid-template-columns: 1fr; }
  }
</style>
</head>
<body>

<header>
  <div class="subtitle">Ambulatorio · Strumenti Clinici</div>
  <h1>Base di <span>Lancio</span></h1>
</header>

<div class="tabs-wrapper">

  <!-- RADIO CONTROLS — corrected mapping -->
  <input type="radio" name="tabs" id="r-siti" checked>
  <input type="radio" name="tabs" id="r-calc">
  <input type="radio" name="tabs" id="r-esami">

  <!-- NAV -->
  <div class="tabs-nav">
    <label for="r-siti">🔗 Siti Esterni</label>
    <label for="r-calc">🧮 Calcolatori</label>
    <label for="r-esami">🩸 Esami Ematochimici</label>
  </div>

  <!-- PANELS -->
  <div class="tab-panels">

    <!-- ══ SITI ESTERNI ══ -->
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
          <a href="https://unipd.specializzazionemedica.it/" class="btn-link" target="_blank">NOMOS Valutazioni Specializzandi</a>
          <a href="https://unipd.link/TIROCINI" class="btn-link" target="_blank">Valutazione Tirocini Studenti</a>
        </div>

        <div class="section-card">
          <h2>Login & Formazione</h2>
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

    <!-- ══ CALCOLATORI ══ -->
    <div class="tab-panel panel-calc">
      <div class="placeholder-box">
        <div class="icon">🧮</div>
        <h3>Calcolatori Clinici</h3>
        <p>Sezione in costruzione. Indica quali calcolatori inserire come priorità<br>e li implementiamo nella prossima sessione.</p>
      </div>
      <div class="calc-grid" style="margin-top:20px">
        <div class="calc-card coming">
          <div class="calc-icon">🫀</div>
          <h4>eGFR / CKD-EPI</h4>
          <p>Filtrato glomerulare stimato</p>
          <div class="coming-label">prossimo</div>
        </div>
        <div class="calc-card coming">
          <div class="calc-icon">🦴</div>
          <h4>FRAX</h4>
          <p>Rischio frattura osteoporotica</p>
          <div class="coming-label">prossimo</div>
        </div>
        <div class="calc-card coming">
          <div class="calc-icon">❤️</div>
          <h4>Score cardiovascolare</h4>
          <p>SCORE2 / Framingham</p>
          <div class="coming-label">da definire</div>
        </div>
        <div class="calc-card coming">
          <div class="calc-icon">💊</div>
          <h4>Altro</h4>
          <p>Aggiungi su richiesta</p>
          <div class="coming-label">da definire</div>
        </div>
      </div>
    </div>

    <!-- ══ ESAMI EMATOCHIMICI ══ -->
    <div class="tab-panel panel-esami">

      <!-- ── MINI-FORM PAZIENTE ── -->
      <div class="patient-bar">
        <div class="patient-bar-title">👤 Dati paziente — usati per tutti i calcoli</div>
        <div class="patient-bar-fields">
          <div class="pfield">
            <label>Età (anni)</label>
            <input type="number" id="p-eta" min="18" max="120" placeholder="es. 65" oninput="ricalcolaTutto()">
          </div>
          <div class="pfield">
            <label>Sesso</label>
            <select id="p-sesso" onchange="ricalcolaTutto()">
              <option value="">—</option>
              <option value="M">Maschio</option>
              <option value="F">Femmina</option>
            </select>
          </div>
          <div class="pfield">
            <label>Peso (kg)</label>
            <input type="number" id="p-peso" min="20" max="300" step="0.1" placeholder="es. 70" oninput="ricalcolaTutto()">
          </div>
          <div class="pfield">
            <label>Cistatina C (mg/L)</label>
            <input type="number" id="p-cisc" min="0" max="10" step="0.01" placeholder="es. 0.90" oninput="ricalcolaTutto()">
          </div>
        </div>
      </div>

      <div class="exams-grid">

        <!-- ════ FUNZIONE RENALE ════ -->
        <div class="exam-section-title">Funzione renale</div>

        <!-- CREATININA -->
        <div class="exam-item">
          <div class="exam-label">Creatinina <span class="exam-range">μmol/L ↔ mg/dL</span></div>
          <div class="input-row">
            <input type="number" class="exam-input" id="creatinina" placeholder="0.0" step="0.01" oninput="ricalcolaTutto()">
            <select class="unit-select" id="creat-unit" onchange="ricalcolaTutto()">
              <option value="umol">μmol/L</option>
              <option value="mgdl">mg/dL</option>
            </select>
            <button class="convert-btn" onclick="convertiCreatinina()" title="Converti unità">⇄</button>
          </div>
          <div class="result-line" id="creatinina-result"></div>
        </div>

        <!-- BOX VFG — occupa tutta la larghezza -->
        <div class="exam-item vfg-box full-width">
          <div class="exam-label">Velocità Filtrazione Glomerulare <span class="calc-badge">⚡ auto</span></div>
          <div class="vfg-grid" id="vfg-grid">
            <div class="vfg-cell" id="vfg-cg">
              <div class="vfg-label">Cockcroft-Gault</div>
              <div class="vfg-value" id="vfg-cg-val">—</div>
              <div class="vfg-unit">mL/min</div>
            </div>
            <div class="vfg-cell" id="vfg-ckd">
              <div class="vfg-label">CKD-EPI 2021</div>
              <div class="vfg-value" id="vfg-ckd-val">—</div>
              <div class="vfg-unit">mL/min/1.73m²</div>
            </div>
            <div class="vfg-cell" id="vfg-cys">
              <div class="vfg-label">CKD-EPI Cystatin</div>
              <div class="vfg-value" id="vfg-cys-val">—</div>
              <div class="vfg-unit">mL/min/1.73m²</div>
            </div>
            <div class="vfg-cell" id="vfg-bis">
              <div class="vfg-label">BIS2</div>
              <div class="vfg-value" id="vfg-bis-val">—</div>
              <div class="vfg-unit">mL/min/1.73m²</div>
            </div>
          </div>
          <div class="result-line" id="vfg-stage" style="margin-top:8px;font-size:0.82rem"></div>
          <div style="font-size:0.72rem;color:var(--text-muted);margin-top:4px">Richiede: età, sesso, peso (CG), creatinina. BIS2 richiede anche cistatina C.</div>
        </div>

        <!-- ════ FUNZIONALITÀ EPATICA ════ -->
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
          <div class="input-row"><input type="number" class="exam-input" id="bilirubina" placeholder="0.0" step="0.1" oninput="checkRange('bilirubina',1.7,17,'μmol/L')"></div>
          <div class="result-line" id="bilirubina-result"></div>
        </div>

        <!-- ════ METABOLISMO FERRO ════ -->
        <div class="exam-section-title">Metabolismo del ferro</div>

        <div class="exam-item">
          <div class="exam-label">Ferro <span class="exam-range">11.6–31.3 μmol/L</span></div>
          <div class="input-row"><input type="number" class="exam-input" id="ferro" placeholder="0.0" step="0.1" oninput="checkRange('ferro',11.6,31.3,'μmol/L'); calcolaIST()"></div>
          <div class="result-line" id="ferro-result"></div>
        </div>
        <div class="exam-item">
          <div class="exam-label">Transferrina <span class="exam-range">2.00–3.60 g/L</span></div>
          <div class="input-row"><input type="number" class="exam-input" id="transferrina" placeholder="0.0" step="0.01" oninput="checkRange('transferrina',2,3.6,'g/L'); calcolaIST()"></div>
          <div class="result-line" id="transferrina-result"></div>
        </div>
        <div class="exam-item">
          <div class="exam-label">Sat. Transferrina <span class="calc-badge">⚡ auto</span></div>
          <div class="input-row">
            <input type="number" class="exam-input" id="ist" placeholder="calcolato" readonly style="opacity:0.6">
            <span style="font-size:0.78rem;color:var(--text-muted);white-space:nowrap">%</span>
          </div>
          <div class="result-line" id="ist-result">Inserisci ferro e transferrina</div>
        </div>
        <div class="exam-item">
          <div class="exam-label">Ferritina <span class="exam-range">31–409 μg/L</span></div>
          <div class="input-row"><input type="number" class="exam-input" id="ferritina" placeholder="0" oninput="checkRange('ferritina',31,409,'μg/L')"></div>
          <div class="result-line" id="ferritina-result"></div>
        </div>

        <!-- ════ LIPIDI ════ -->
        <div class="exam-section-title">Lipidi — <span style="font-size:0.85em;font-style:italic;color:var(--text-muted)">seleziona unità; converti con ⇄</span></div>

        <!-- Colesterolo totale -->
        <div class="exam-item">
          <div class="exam-label">Colesterolo Totale <span class="exam-range">&lt;5.18 mmol/L · &lt;200 mg/dL</span></div>
          <div class="input-row">
            <input type="number" class="exam-input" id="colest" placeholder="0.0" step="0.01" oninput="calcolaLipidi()">
            <select class="unit-select" id="colest-unit" onchange="calcolaLipidi()">
              <option value="mmol">mmol/L</option>
              <option value="mgdl">mg/dL</option>
            </select>
            <button class="convert-btn" onclick="convertiLipide('colest','colest-unit',0.02586)" title="Converti">⇄</button>
          </div>
          <div class="result-line" id="colest-result"></div>
        </div>

        <!-- HDL -->
        <div class="exam-item">
          <div class="exam-label">HDL <span class="exam-range">&gt;1.04 mmol/L · &gt;40 mg/dL</span></div>
          <div class="input-row">
            <input type="number" class="exam-input" id="hdl" placeholder="0.0" step="0.01" oninput="calcolaLipidi()">
            <select class="unit-select" id="hdl-unit" onchange="calcolaLipidi()">
              <option value="mmol">mmol/L</option>
              <option value="mgdl">mg/dL</option>
            </select>
            <button class="convert-btn" onclick="convertiLipide('hdl','hdl-unit',0.02586)" title="Converti">⇄</button>
          </div>
          <div class="result-line" id="hdl-result"></div>
        </div>

        <!-- Trigliceridi -->
        <div class="exam-item">
          <div class="exam-label">Trigliceridi <span class="exam-range">&lt;1.70 mmol/L · &lt;150 mg/dL</span></div>
          <div class="input-row">
            <input type="number" class="exam-input" id="tg" placeholder="0.0" step="0.01" oninput="calcolaLipidi()">
            <select class="unit-select" id="tg-unit" onchange="calcolaLipidi()">
              <option value="mmol">mmol/L</option>
              <option value="mgdl">mg/dL</option>
            </select>
            <button class="convert-btn" onclick="convertiLipide('tg','tg-unit',0.01129)" title="Converti">⇄</button>
          </div>
          <div class="result-line" id="tg-result"></div>
        </div>

        <!-- LDL inserito o calcolato -->
        <div class="exam-item">
          <div class="exam-label">LDL <span class="calc-badge">⚡ Friedewald auto</span></div>
          <div class="input-row">
            <input type="number" class="exam-input" id="ldl" placeholder="calcolato" step="0.01" oninput="calcolaLipidi()">
            <select class="unit-select" id="ldl-unit" onchange="calcolaLipidi()">
              <option value="mmol">mmol/L</option>
              <option value="mgdl">mg/dL</option>
            </select>
            <button class="convert-btn" onclick="convertiLipide('ldl','ldl-unit',0.02586)" title="Converti">⇄</button>
          </div>
          <div class="result-line" id="ldl-result"></div>
        </div>

        <!-- Lipoproteina(a) -->
        <div class="exam-item">
          <div class="exam-label">Lipoproteina(a) <span class="exam-range">&lt;75 nmol/L · &lt;30 mg/dL</span></div>
          <div class="input-row">
            <input type="number" class="exam-input" id="lpa" placeholder="0.0" step="0.1" oninput="checkLpa()">
            <select class="unit-select" id="lpa-unit" onchange="checkLpa()">
              <option value="nmol">nmol/L</option>
              <option value="mgdl">mg/dL</option>
            </select>
            <button class="convert-btn" onclick="convertiLpa()" title="Converti">⇄</button>
          </div>
          <div class="result-line" id="lpa-result"></div>
        </div>

        <!-- ════ CALCIO-FOSFORO ════ -->
        <div class="exam-section-title">Metabolismo calcio-fosforo</div>

        <!-- Calcio plasmatico con conversione -->
        <div class="exam-item">
          <div class="exam-label">P-Calcio <span class="exam-range">2.10–2.55 mmol/L · 8.4–10.2 mg/dL</span></div>
          <div class="input-row">
            <input type="number" class="exam-input" id="calcio" placeholder="0.0" step="0.01" oninput="checkCalcio()">
            <select class="unit-select" id="calcio-unit" onchange="checkCalcio()">
              <option value="mmol">mmol/L</option>
              <option value="mgdl">mg/dL</option>
            </select>
            <button class="convert-btn" onclick="convertiCalcio()" title="Converti">⇄</button>
          </div>
          <div class="result-line" id="calcio-result"></div>
        </div>

        <div class="exam-item">
          <div class="exam-label">P-Fosforo <span class="exam-range">0.81–1.45 mmol/L</span></div>
          <div class="input-row"><input type="number" class="exam-input" id="fosforo" placeholder="0.0" step="0.01" oninput="checkRange('fosforo',0.81,1.45,'mmol/L')"></div>
          <div class="result-line" id="fosforo-result"></div>
        </div>

        <div class="exam-item">
          <div class="exam-label">PTH <span class="exam-range">15–65 ng/L</span></div>
          <div class="input-row"><input type="number" class="exam-input" id="pth" placeholder="0" oninput="checkRange('pth',15,65,'ng/L')"></div>
          <div class="result-line" id="pth-result"></div>
        </div>

        <!-- Vitamina D con conversione -->
        <div class="exam-item">
          <div class="exam-label">Vitamina 25-D <span class="exam-range">&gt;50 nmol/L · &gt;20 ng/mL</span></div>
          <div class="input-row">
            <input type="number" class="exam-input" id="vitd" placeholder="0" oninput="checkVitD()">
            <select class="unit-select" id="vitd-unit" onchange="checkVitD()">
              <option value="nmol">nmol/L</option>
              <option value="ngml">ng/mL</option>
            </select>
            <button class="convert-btn" onclick="convertiVitD()" title="Converti">⇄</button>
          </div>
          <div class="result-line" id="vitd-result"></div>
        </div>

        <div class="exam-item">
          <div class="exam-label">CTX <span class="exam-range">121–747 ng/L (pre-men.)</span></div>
          <div class="input-row"><input type="number" class="exam-input" id="ctx" placeholder="0" oninput="checkRange('ctx',121,747,'ng/L')"></div>
          <div class="result-line" id="ctx-result"></div>
        </div>

        <!-- ════ URINE 24h ════ -->
        <div class="exam-section-title">Urine 24h</div>

        <div class="exam-item">
          <div class="exam-label">Diuresi 24h <span class="exam-range">~1500 mL</span></div>
          <div class="input-row"><input type="number" class="exam-input" id="diuresi" placeholder="0"></div>
          <div class="result-line" id="diuresi-result"></div>
        </div>

        <!-- Calciuria con soglia 4mg/kg -->
        <div class="exam-item">
          <div class="exam-label">U-Calcio <span class="exam-range">2.50–7.50 mmol/24h · &lt;4 mg/kg/die</span></div>
          <div class="input-row">
            <input type="number" class="exam-input" id="ucalcio" placeholder="0.0" step="0.1" oninput="checkCalciuria()">
            <select class="unit-select" id="ucalcio-unit" onchange="checkCalciuria()">
              <option value="mmol">mmol/24h</option>
              <option value="mg">mg/24h</option>
            </select>
            <button class="convert-btn" onclick="convertiCalciuria()" title="Converti">⇄</button>
          </div>
          <div class="result-line" id="ucalcio-result"></div>
        </div>

        <div class="exam-item">
          <div class="exam-label">U-Fosforo <span class="exam-range">mmol/24h</span></div>
          <div class="input-row"><input type="number" class="exam-input" id="ufosforo" placeholder="0.0" step="0.1"></div>
          <div class="result-line" id="ufosforo-result"></div>
        </div>

      </div><!-- /exams-grid -->
    </div><!-- /panel-esami -->

  </div><!-- /tab-panels -->
</div><!-- /tabs-wrapper -->

<style>
/* ── PATIENT BAR ── */
.patient-bar {
  background: linear-gradient(135deg, rgba(74,158,255,0.08), rgba(125,211,176,0.06));
  border: 1px solid rgba(74,158,255,0.25);
  border-radius: var(--radius);
  padding: 18px 20px;
  margin-bottom: 22px;
}
.patient-bar-title {
  font-size: 0.78rem;
  font-weight: 600;
  color: var(--accent);
  text-transform: uppercase;
  letter-spacing: 0.08em;
  margin-bottom: 14px;
}
.patient-bar-fields {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 14px;
}
.pfield { display: flex; flex-direction: column; gap: 5px; }
.pfield label {
  font-size: 0.74rem;
  font-weight: 600;
  color: var(--text-muted);
  text-transform: uppercase;
  letter-spacing: 0.06em;
}
.pfield input, .pfield select {
  padding: 8px 10px;
  background: var(--bg);
  border: 1px solid var(--border);
  border-radius: 6px;
  color: var(--text);
  font-family: 'JetBrains Mono', monospace;
  font-size: 0.9rem;
}
.pfield input:focus, .pfield select:focus { outline: none; border-color: var(--accent); }

/* ── VFG BOX ── */
.vfg-box { background: var(--surface2); }
.full-width { grid-column: 1 / -1; }
.vfg-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 10px;
  margin-top: 10px;
}
.vfg-cell {
  background: var(--bg);
  border: 1px solid var(--border);
  border-radius: 8px;
  padding: 12px;
  text-align: center;
  transition: border-color 0.2s;
}
.vfg-label { font-size: 0.72rem; color: var(--text-muted); text-transform: uppercase; letter-spacing: 0.05em; margin-bottom: 6px; }
.vfg-value { font-family: 'JetBrains Mono', monospace; font-size: 1.5rem; font-weight: 500; color: var(--text); }
.vfg-unit  { font-size: 0.68rem; color: var(--text-muted); margin-top: 2px; }
.vfg-cell.stage-1 { border-color: var(--accent2); }
.vfg-cell.stage-2 { border-color: #a3e635; }
.vfg-cell.stage-3 { border-color: #f59e0b; }
.vfg-cell.stage-4 { border-color: #f97316; }
.vfg-cell.stage-5 { border-color: #ef4444; }

@media (max-width: 640px) {
  .patient-bar-fields { grid-template-columns: 1fr 1fr; }
  .vfg-grid { grid-template-columns: 1fr 1fr; }
}
</style>

<script>
// ══════════════════════════════════════════
// UTILITY
// ══════════════════════════════════════════
function getPaziente() {
  return {
    eta:  parseFloat(document.getElementById('p-eta').value)  || null,
    sesso: document.getElementById('p-sesso').value || null,
    peso: parseFloat(document.getElementById('p-peso').value) || null,
    cisc: parseFloat(document.getElementById('p-cisc').value) || null,
  };
}

function checkRange(id, min, max, unit) {
  const val = parseFloat(document.getElementById(id).value);
  const res = document.getElementById(id + '-result');
  const inp = document.getElementById(id);
  if (!res) return;
  if (isNaN(val) || val === 0) {
    res.textContent = ''; res.className = 'result-line';
    inp.classList.remove('out-of-range','in-range'); return;
  }
  if (val < min) {
    res.textContent = `↓ Sotto range (${min}–${max} ${unit})`;
    res.className = 'result-line err';
    inp.classList.add('out-of-range'); inp.classList.remove('in-range');
  } else if (val > max) {
    res.textContent = `↑ Sopra range (${min}–${max} ${unit})`;
    res.className = 'result-line warn';
    inp.classList.add('out-of-range'); inp.classList.remove('in-range');
  } else {
    res.textContent = `✓ Nella norma`;
    res.className = 'result-line ok';
    inp.classList.add('in-range'); inp.classList.remove('out-of-range');
  }
}

function setVfgColor(cellId, gfr) {
  const cell = document.getElementById(cellId);
  cell.classList.remove('stage-1','stage-2','stage-3','stage-4','stage-5');
  if (isNaN(gfr)) return;
  if (gfr >= 90)       cell.classList.add('stage-1');
  else if (gfr >= 60)  cell.classList.add('stage-2');
  else if (gfr >= 30)  cell.classList.add('stage-3');
  else if (gfr >= 15)  cell.classList.add('stage-4');
  else                 cell.classList.add('stage-5');
}

function ckdStage(gfr) {
  if (isNaN(gfr)) return '';
  if (gfr >= 90) return 'G1 (≥90)';
  if (gfr >= 60) return 'G2 (60–89)';
  if (gfr >= 45) return 'G3a (45–59)';
  if (gfr >= 30) return 'G3b (30–44)';
  if (gfr >= 15) return 'G4 (15–29)';
  return 'G5 (<15)';
}

// ══════════════════════════════════════════
// VFG — quattro formule
// ══════════════════════════════════════════
function calcolaVFG() {
  const p = getPaziente();
  const creatEl  = document.getElementById('creatinina');
  const creatUnit = document.getElementById('creat-unit').value;
  let creat_mgdl = parseFloat(creatEl.value);
  if (isNaN(creat_mgdl)) { resetVFG(); return; }
  // normalizza a mg/dL
  if (creatUnit === 'umol') creat_mgdl = creat_mgdl / 88.42;

  let cgVal='—', ckdVal='—', cysVal='—', bisVal='—';

  // ── Cockcroft-Gault ──
  if (p.eta && p.sesso && p.peso) {
    let cg = ((140 - p.eta) * p.peso) / (72 * creat_mgdl);
    if (p.sesso === 'F') cg *= 0.85;
    cgVal = cg.toFixed(0);
    setVfgColor('vfg-cg', cg);
  }

  // ── CKD-EPI 2021 (senza race) — usa mg/dL con kappa in mg/dL ──
  if (p.eta && p.sesso) {
    // kappa in mg/dL: F=0.7, M=0.9
    const kappa = p.sesso === 'F' ? 0.7 : 0.9;
    const alpha = p.sesso === 'F' ? -0.241 : -0.302;
    const ratio = creat_mgdl / kappa;
    const A = Math.min(ratio, 1) ** alpha;
    const B = Math.max(ratio, 1) ** (-1.200);
    const sex_f = p.sesso === 'F' ? 1.012 : 1.0;
    const ckd = 142 * A * B * (0.9938 ** p.eta) * sex_f;
    ckdVal = ckd.toFixed(0);
    setVfgColor('vfg-ckd', ckd);
  }

  // ── CKD-EPI Cystatin C 2012 — cistatina da campo esami ──
  const ciscVal = parseFloat(document.getElementById('cistatina-c')?.value) || p.cisc;
  if (p.eta && p.sesso && ciscVal) {
    const ratio_c = ciscVal / 0.8;
    const A2 = Math.min(ratio_c, 1) ** (-0.410);
    const B2 = Math.max(ratio_c, 1) ** (-0.711);
    const sex_f2 = p.sesso === 'F' ? 0.932 : 1.0;
    const cys = 133 * A2 * B2 * (0.9969 ** p.eta) * sex_f2;
    cysVal = cys.toFixed(0);
    setVfgColor('vfg-cys', cys);
  }

  // ── BIS2 — formula corretta Schaeffner 2012 (creat in mg/dL, cistatina in mg/L) ──
  // BIS2 = 767 × CysC^-0.61 × Creat^-0.40 × Age^-0.57 × 0.87(se F)
  if (p.eta && ciscVal) {
    let bis2 = 767 * Math.pow(ciscVal, -0.61) * Math.pow(creat_mgdl, -0.40) * Math.pow(p.eta, -0.57);
    if (p.sesso === 'F') bis2 *= 0.87;
    bisVal = bis2.toFixed(0);
    setVfgColor('vfg-bis', bis2);
  }

  document.getElementById('vfg-cg-val').textContent  = cgVal;
  document.getElementById('vfg-ckd-val').textContent = ckdVal;
  document.getElementById('vfg-cys-val').textContent = cysVal;
  document.getElementById('vfg-bis-val').textContent = bisVal;

  // CKD stage dal CKD-EPI
  const numCkd = parseFloat(ckdVal);
  const stageEl = document.getElementById('vfg-stage');
  if (!isNaN(numCkd)) {
    const stage = ckdStage(numCkd);
    stageEl.textContent = `Stadio CKD (CKD-EPI): ${stage}`;
    stageEl.className = numCkd < 60 ? 'result-line warn' : 'result-line ok';
  } else {
    stageEl.textContent = 'Inserisci creatinina + dati paziente per calcolare VFG';
    stageEl.className = 'result-line';
  }
}

function resetVFG() {
  ['vfg-cg-val','vfg-ckd-val','vfg-cys-val','vfg-bis-val'].forEach(id => {
    document.getElementById(id).textContent = '—';
    ['stage-1','stage-2','stage-3','stage-4','stage-5'].forEach(c =>
      document.getElementById(id.replace('-val','')).classList.remove(c));
  });
  document.getElementById('vfg-stage').textContent = 'Inserisci creatinina + dati paziente';
  document.getElementById('vfg-stage').className = 'result-line';
}

// ══════════════════════════════════════════
// CREATININA — conversione
// ══════════════════════════════════════════
function convertiCreatinina() {
  const input = document.getElementById('creatinina');
  const unit  = document.getElementById('creat-unit');
  const res   = document.getElementById('creatinina-result');
  const val   = parseFloat(input.value);
  if (isNaN(val) || val <= 0) { res.textContent='Valore non valido'; return; }
  if (unit.value === 'umol') {
    const mgdl = (val / 88.42).toFixed(2);
    unit.value = 'mgdl'; input.value = mgdl;
    res.textContent = `↔ ${val} μmol/L = ${mgdl} mg/dL`;
    res.className = 'result-line ok';
  } else {
    const umol = (val * 88.42).toFixed(1);
    unit.value = 'umol'; input.value = umol;
    res.textContent = `↔ ${val} mg/dL = ${umol} μmol/L`;
    res.className = 'result-line ok';
  }
  ricalcolaTutto();
}

// ══════════════════════════════════════════
// LIPIDI
// ══════════════════════════════════════════
// factor = mmol→mgdl: colest/HDL/LDL = 38.67, TG = 88.57
// direction: se unità è mmol, il valore è in mmol → converti a mg/dL = val/factor_mmol_per_mgdl
// Semplificato: convertiLipide gestisce il toggle e usa i fattori corretti per ciascun analita

function convertiLipide(inputId, unitId, factorMmolToMgdl) {
  // factorMmolToMgdl non usato qui direttamente — usiamo fattori fissi per precisione
  const factors = { colest: 38.67, hdl: 38.67, ldl: 38.67, tg: 88.57, lpa: null };
  const f = factors[inputId] || 38.67;
  const input = document.getElementById(inputId);
  const unit  = document.getElementById(unitId);
  const val   = parseFloat(input.value);
  if (isNaN(val) || val <= 0) return;
  if (unit.value === 'mmol') {
    input.value = (val * f).toFixed(1);
    unit.value = 'mgdl';
  } else {
    input.value = (val / f).toFixed(2);
    unit.value = 'mmol';
  }
  calcolaLipidi();
}

function toMmol(val, unitId) {
  const factors = { colest: 38.67, hdl: 38.67, ldl: 38.67, tg: 88.57 };
  const id = unitId.replace('-unit','');
  const f = factors[id] || 38.67;
  return document.getElementById(unitId).value === 'mgdl' ? val / f : val;
}

function calcolaLipidi() {
  // Colesterolo totale
  const colestV = parseFloat(document.getElementById('colest').value);
  const colestU = document.getElementById('colest-unit').value;
  if (!isNaN(colestV) && colestV > 0) {
    const mmol = colestU === 'mgdl' ? colestV/38.67 : colestV;
    const res = document.getElementById('colest-result');
    const alt = colestU === 'mmol' ? `(${(colestV*38.67).toFixed(0)} mg/dL)` : `(${(colestV/38.67).toFixed(2)} mmol/L)`;
    if (mmol < 5.18) { res.textContent=`✓ Desiderabile ${alt}`; res.className='result-line ok'; }
    else { res.textContent=`↑ Elevato ${alt}`; res.className='result-line warn'; }
  } else { document.getElementById('colest-result').textContent=''; }

  // HDL
  const hdlV = parseFloat(document.getElementById('hdl').value);
  const hdlU = document.getElementById('hdl-unit').value;
  if (!isNaN(hdlV) && hdlV > 0) {
    const mmol = hdlU === 'mgdl' ? hdlV/38.67 : hdlV;
    const res = document.getElementById('hdl-result');
    const alt = hdlU === 'mmol' ? `(${(hdlV*38.67).toFixed(0)} mg/dL)` : `(${(hdlV/38.67).toFixed(2)} mmol/L)`;
    if (mmol < 1.04) { res.textContent=`↓ Basso — rischio CV ${alt}`; res.className='result-line err'; }
    else if (mmol > 1.55) { res.textContent=`✓ Elevato — protettivo ${alt}`; res.className='result-line ok'; }
    else { res.textContent=`✓ Nella norma ${alt}`; res.className='result-line ok'; }
  } else { document.getElementById('hdl-result').textContent=''; }

  // Trigliceridi
  const tgV = parseFloat(document.getElementById('tg').value);
  const tgU = document.getElementById('tg-unit').value;
  if (!isNaN(tgV) && tgV > 0) {
    const mmol = tgU === 'mgdl' ? tgV/88.57 : tgV;
    const res = document.getElementById('tg-result');
    const alt = tgU === 'mmol' ? `(${(tgV*88.57).toFixed(0)} mg/dL)` : `(${(tgV/88.57).toFixed(2)} mmol/L)`;
    if (mmol < 1.70)       { res.textContent=`✓ Desiderabile ${alt}`; res.className='result-line ok'; }
    else if (mmol < 5.64)  { res.textContent=`↑ Elevato ${alt}`; res.className='result-line warn'; }
    else                   { res.textContent=`↑↑ Molto elevato — rischio pancreatite ${alt}`; res.className='result-line err'; }
  } else { document.getElementById('tg-result').textContent=''; }

  // LDL — Friedewald se non inserito manualmente
  const ldlInput = document.getElementById('ldl');
  const ldlRes = document.getElementById('ldl-result');
  let ldlMmol = parseFloat(ldlInput.value);
  let ldlAuto = false;

  if (!isNaN(colestV) && !isNaN(hdlV) && !isNaN(tgV) && colestV > 0 && hdlV > 0 && tgV > 0) {
    const cMmol = toMmol(colestV,'colest-unit');
    const hMmol = toMmol(hdlV,'hdl-unit');
    const tMmol = toMmol(tgV,'tg-unit');
    if (tMmol < 4.52) { // Friedewald valido solo per TG < 4.52 mmol/L (400 mg/dL)
      const calcLdl = cMmol - hMmol - (tMmol / 2.2);
      if (isNaN(ldlMmol) || ldlInput.value === '') {
        ldlMmol = calcLdl;
        ldlAuto = true;
        const ldlU = document.getElementById('ldl-unit').value;
        ldlInput.value = ldlU === 'mgdl' ? (calcLdl * 38.67).toFixed(0) : calcLdl.toFixed(2);
        ldlInput.style.opacity = '0.7';
      }
    }
  }

  if (!isNaN(ldlMmol) && ldlMmol > 0) {
    const ldlU = document.getElementById('ldl-unit').value;
    const mmol = ldlU === 'mgdl' ? ldlMmol/38.67 : ldlMmol;
    const alt = ldlU === 'mmol' ? `(${(ldlMmol*38.67).toFixed(0)} mg/dL)` : `(${(ldlMmol/38.67).toFixed(2)} mmol/L)`;
    const src = ldlAuto ? ' [Friedewald]' : '';
    if (mmol < 2.59)       { ldlRes.textContent=`✓ Ottimale${src} ${alt}`; ldlRes.className='result-line ok'; }
    else if (mmol < 3.37)  { ldlRes.textContent=`→ Desiderabile${src} ${alt}`; ldlRes.className='result-line ok'; }
    else if (mmol < 4.14)  { ldlRes.textContent=`↑ Limite alto${src} ${alt}`; ldlRes.className='result-line warn'; }
    else                   { ldlRes.textContent=`↑↑ Elevato${src} ${alt}`; ldlRes.className='result-line err'; }
  }
}

function convertiLpa() {
  const input = document.getElementById('lpa');
  const unit  = document.getElementById('lpa-unit');
  const val   = parseFloat(input.value);
  if (isNaN(val) || val <= 0) return;
  // fattore approssimativo: 1 mg/dL ≈ 2.5 nmol/L
  if (unit.value === 'nmol') {
    input.value = (val / 2.5).toFixed(1);
    unit.value = 'mgdl';
  } else {
    input.value = (val * 2.5).toFixed(0);
    unit.value = 'nmol';
  }
  checkLpa();
}

function checkLpa() {
  const val = parseFloat(document.getElementById('lpa').value);
  const unit = document.getElementById('lpa-unit').value;
  const res  = document.getElementById('lpa-result');
  if (isNaN(val) || val <= 0) { res.textContent=''; return; }
  const nmol = unit === 'mgdl' ? val * 2.5 : val;
  const mgdl = unit === 'nmol' ? val / 2.5 : val;
  const alt = unit === 'nmol' ? `(≈${mgdl.toFixed(0)} mg/dL)` : `(≈${nmol.toFixed(0)} nmol/L)`;
  if (nmol < 75)       { res.textContent=`✓ Basso rischio cardiovascolare ${alt}`; res.className='result-line ok'; }
  else if (nmol < 125) { res.textContent=`→ Rischio intermedio ${alt}`; res.className='result-line warn'; }
  else                 { res.textContent=`↑ Alto rischio CV — monitorare ${alt}`; res.className='result-line err'; }
}

// ══════════════════════════════════════════
// CALCIO
// ══════════════════════════════════════════
function convertiCalcio() {
  const input = document.getElementById('calcio');
  const unit  = document.getElementById('calcio-unit');
  const val   = parseFloat(input.value);
  if (isNaN(val) || val <= 0) return;
  if (unit.value === 'mmol') {
    input.value = (val * 4.008).toFixed(1);
    unit.value = 'mgdl';
  } else {
    input.value = (val / 4.008).toFixed(2);
    unit.value = 'mmol';
  }
  checkCalcio();
}

function checkCalcio() {
  const val  = parseFloat(document.getElementById('calcio').value);
  const unit = document.getElementById('calcio-unit').value;
  const res  = document.getElementById('calcio-result');
  if (isNaN(val) || val === 0) { res.textContent=''; return; }
  const mmol = unit === 'mgdl' ? val / 4.008 : val;
  const alt  = unit === 'mmol' ? `(${(val*4.008).toFixed(1)} mg/dL)` : `(${(val/4.008).toFixed(2)} mmol/L)`;
  if (mmol < 2.10)      { res.textContent=`↓ Ipocalcemia ${alt}`; res.className='result-line err'; }
  else if (mmol > 2.55) { res.textContent=`↑ Ipercalcemia ${alt}`; res.className='result-line warn'; }
  else                  { res.textContent=`✓ Nella norma ${alt}`; res.className='result-line ok'; }
}

// ══════════════════════════════════════════
// VITAMINA D
// ══════════════════════════════════════════
function convertiVitD() {
  const input = document.getElementById('vitd');
  const unit  = document.getElementById('vitd-unit');
  const val   = parseFloat(input.value);
  if (isNaN(val) || val <= 0) return;
  if (unit.value === 'nmol') {
    input.value = (val / 2.496).toFixed(1);
    unit.value = 'ngml';
  } else {
    input.value = (val * 2.496).toFixed(0);
    unit.value = 'nmol';
  }
  checkVitD();
}

function checkVitD() {
  const val  = parseFloat(document.getElementById('vitd').value);
  const unit = document.getElementById('vitd-unit').value;
  const res  = document.getElementById('vitd-result');
  const inp  = document.getElementById('vitd');
  if (isNaN(val)) { res.textContent=''; return; }
  const nmol = unit === 'ngml' ? val * 2.496 : val;
  const alt  = unit === 'nmol' ? `(${(val/2.496).toFixed(1)} ng/mL)` : `(${(val*2.496).toFixed(0)} nmol/L)`;
  if (nmol < 25)       { res.textContent=`↓↓ Carenza grave (<25 nmol/L) ${alt}`; res.className='result-line err'; inp.classList.add('out-of-range'); }
  else if (nmol < 50)  { res.textContent=`↓ Insufficienza (25–50 nmol/L) ${alt}`; res.className='result-line warn'; inp.classList.add('out-of-range'); }
  else if (nmol < 75)  { res.textContent=`→ Sufficiente (50–75 nmol/L) ${alt}`; res.className='result-line ok'; inp.classList.remove('out-of-range'); }
  else if (nmol < 250) { res.textContent=`✓ Ottimale (75–250 nmol/L) ${alt}`; res.className='result-line ok'; inp.classList.remove('out-of-range'); }
  else                 { res.textContent=`↑ Possibile tossicità (>250 nmol/L) ${alt}`; res.className='result-line err'; inp.classList.add('out-of-range'); }
}

// ══════════════════════════════════════════
// CALCIURIA — range + soglia 4 mg/kg
// ══════════════════════════════════════════
function convertiCalciuria() {
  const input = document.getElementById('ucalcio');
  const unit  = document.getElementById('ucalcio-unit');
  const val   = parseFloat(input.value);
  if (isNaN(val) || val <= 0) return;
  if (unit.value === 'mmol') {
    input.value = (val * 40.08).toFixed(0);
    unit.value = 'mg';
  } else {
    input.value = (val / 40.08).toFixed(2);
    unit.value = 'mmol';
  }
  checkCalciuria();
}

function checkCalciuria() {
  const val  = parseFloat(document.getElementById('ucalcio').value);
  const unit = document.getElementById('ucalcio-unit').value;
  const res  = document.getElementById('ucalcio-result');
  const peso = getPaziente().peso;
  if (isNaN(val) || val === 0) { res.textContent=''; return; }

  const mmol = unit === 'mg' ? val / 40.08 : val;
  const mg   = unit === 'mmol' ? val * 40.08 : val;
  const alt  = unit === 'mmol' ? `(${mg.toFixed(0)} mg/24h)` : `(${mmol.toFixed(2)} mmol/24h)`;

  let rangeMsg = '';
  let cls = 'result-line';
  if (mmol < 2.50)      { rangeMsg = `↓ Ipocalciuria ${alt}`; cls='result-line warn'; }
  else if (mmol > 7.50) { rangeMsg = `↑ Ipercalciuria ${alt}`; cls='result-line err'; }
  else                  { rangeMsg = `✓ Range normale ${alt}`; cls='result-line ok'; }

  // soglia 4 mg/kg/die
  let pesoMsg = '';
  if (peso) {
    const soglia = peso * 4;
    if (mg > soglia) {
      pesoMsg = ` | ↑ ${mg.toFixed(0)} mg > ${soglia.toFixed(0)} mg (4mg/kg) — ipercalciuria peso-corretta`;
      cls = 'result-line err';
    } else {
      pesoMsg = ` | ✓ ${mg.toFixed(0)} mg < ${soglia.toFixed(0)} mg (4mg/kg)`;
    }
  } else {
    pesoMsg = ' | Inserisci peso per soglia 4mg/kg';
  }

  res.textContent = rangeMsg + pesoMsg;
  res.className = cls;
}

// ══════════════════════════════════════════
// IST AUTO
// ══════════════════════════════════════════
function calcolaIST() {
  const ferro  = parseFloat(document.getElementById('ferro').value);
  const transf = parseFloat(document.getElementById('transferrina').value);
  const istInput  = document.getElementById('ist');
  const istResult = document.getElementById('ist-result');
  if (!isNaN(ferro) && !isNaN(transf) && transf > 0) {
    const ist = ((ferro / (transf * 25.1)) * 100).toFixed(1);
    istInput.value = ist;
    const n = parseFloat(ist);
    if (n < 16)      { istResult.textContent=`↓ ${ist}% — Bassa (16–49%)`; istResult.className='result-line err'; }
    else if (n > 49) { istResult.textContent=`↑ ${ist}% — Alta (16–49%)`; istResult.className='result-line warn'; }
    else             { istResult.textContent=`✓ ${ist}% — Nella norma (16–49%)`; istResult.className='result-line ok'; }
  } else {
    istInput.value='';
    istResult.textContent='Inserisci ferro e transferrina';
    istResult.className='result-line';
  }
}

// ══════════════════════════════════════════
// RICALCOLA TUTTO (chiamato dai campi paziente)
// ══════════════════════════════════════════
function ricalcolaTutto() {
  calcolaVFG();
  calcolaLipidi();
  checkCalciuria();
}
</script>
</body>
</html>
