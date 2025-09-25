<!DOCTYPE html>
<html lang="it">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Il mio Cruscotto</title>
    <style>
        body {
            /* Sfondo sfumato scuro, dal nero al grigio scuro */
            background: linear-gradient(to right, #000000, #2c3e50);
            color: #ecf0f1; /* Colore del testo bianco/grigio chiaro */
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 20px;
            height: 100vh;
            display: flex;
            flex-direction: column;
            justify-content: flex-start; /* Allinea il contenuto in alto */
            align-items: center;
            text-align: center;
        }

        h1 {
            font-size: 3em;
            text-shadow: 2px 2px 4px #000000; /* Ombra per rendere il titolo più leggibile */
            margin-bottom: 40px;
        }
        
        /* Stili per le schede */
        .tabs {
            max-width: 900px;
            width: 100%;
            margin: 0 auto;
            background-color: rgba(0, 0, 0, 0.4);
            border-radius: 10px;
            padding: 20px;
        }

        .tabs input[type="radio"] {
            display: none;
        }

        .tabs-list {
            display: flex;
            justify-content: center;
            border-bottom: 2px solid #555;
            margin-bottom: 20px;
        }

        .tabs-list label {
            padding: 10px 20px;
            cursor: pointer;
            transition: background-color 0.3s ease;
            font-weight: bold;
            border-radius: 5px 5px 0 0;
            user-select: none;
        }

        .tabs-list label:hover {
            background-color: #555;
        }
        
        .tab-content {
            display: none;
            padding: 20px 0;
        }

        /* Mostra il contenuto della scheda selezionata */
        #tab1:checked ~ .tab-content.calcolatori,
        #tab2:checked ~ .tab-content.esami,
        #tab3:checked ~ .tab-content.siti {
            display: block;
        }

        /* Stile per la scheda selezionata */
        #tab1:checked ~ .tabs-list label[for="tab1"],
        #tab2:checked ~ .tabs-list label[for="tab2"],
        #tab3:checked ~ .tabs-list label[for="tab3"] {
            background-color: #2c3e50;
        }
        
        /* Stili per i riquadri e i pulsanti all'interno della scheda */
        .sites-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
            padding-top: 20px;
        }

        .section-container {
            background-color: rgba(44, 62, 80, 0.6);
            border: 1px solid #34495e;
            border-radius: 8px;
            padding: 15px;
            text-align: center;
        }

        .section-container h2 {
            font-size: 1.5em;
            margin-top: 0;
            border-bottom: 2px solid #3498db;
            padding-bottom: 10px;
            margin-bottom: 15px;
        }

        .button-list {
            display: flex;
            flex-direction: column;
            gap: 10px;
        }

        .button-link {
            display: block;
            background-color: #3498db;
            color: white;
            padding: 12px;
            text-decoration: none;
            border-radius: 5px;
            font-weight: bold;
            transition: background-color 0.3s ease;
        }

        .button-link:hover {
            background-color: #2980b9;
        }

        /* Stili aggiuntivi per i campi di input degli esami */
        .exams-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 15px;
            text-align: left;
            padding: 0 20px;
        }
        .exam-item {
            display: flex;
            flex-direction: column;
            gap: 5px;
        }
        .exam-item label {
            font-weight: bold;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        .exam-item input[type="text"] {
            width: 100%;
            padding: 8px;
            border: none;
            border-radius: 4px;
            background-color: #34495e;
            color: #ecf0f1;
            box-sizing: border-box;
            font-size: 1em;
        }
        .exam-item .range {
            font-size: 0.8em;
            color: #bdc3c7;
            margin-top: 5px;
        }

    </style>
</head>
<body>

    <h1>Base di lancio</h1>

    <div class="tabs">
        <input type="radio" name="tabs" id="tab1" checked>
        <input type="radio" name="tabs" id="tab2">
        <input type="radio" name="tabs" id="tab3">

        <div class="tabs-list">
            <label for="tab3">Siti Esterni</label>
            <label for="tab1">Calcolatori</label>
            <label for="tab2">Esami Ematochimici</label>
        </div>
        <div class="tab-content siti">
            <div class="sites-grid">
                <div class="section-container">
                    <h2>Prescrizione</h2>
                    <div class="button-list">
                        <a href="https://registri.aifa.gov.it/jam/UI/Login?goto=http%3A%2F%2Fregistri.aifa.gov.it%3A80%2Fregistri%2F" class="button-link">AIFA Piani terapeutici</a>
                        <a href="https://psf.azero.veneto.it/psf/web/index.html" class="button-link">Veneto Piani terapeutici</a>
                        <a href="https://cas.aulss6.veneto.it/cas/login?service=https%3A%2F%2Fextranet.aulss6.veneto.it%2Fpages%2Fhome" class="button-link">AULSS6 extranet</a>
                        <a href="https://redcap.aopd.veneto.it/redcap/" class="button-link">Prescrizione cateteri AULSS 6</a>
                    </div>
                </div>

                <div class="section-container">
                    <h2>Clinica</h2>
                    <div class="button-list">
                        <a href="http://healthmeeting.sanita.padova.it/HealthMeeting/#/login" class="button-link">Telemedicina</a>
                        <a href="https://172.25.0.42/AmbulatorioOsteoporosi/" class="button-link">Osteoporosi</a>
                        <a href="https://serviziweb2.inps.it/PassiWeb/jsp/spid/loginSPID.jsp?uri=https%3a%2f%2fservizi2.inps.it%2fservizi%2fareariservata&S=S" class="button-link">INPS</a>
                        <a href="https://www.uptodate.com/login" class="button-link">UPTODATE</a>
						<a href="https://medicinali.aifa.gov.it/it/#/it/" class="button-link">Schede tecniche farmaci</a>
                    </div>
                </div>

                <div class="section-container">
                    <h2>UNIPD</h2>
                    <div class="button-list">
                        <a href="https://medicina.elearning.unipd.it/user/index.php?id=2494" class="button-link">MOODLE scuola di specializzazione</a>
                        <a href="https://unipd.specializzazionemedica.it/" class="button-link">NOMOS valutazioni specializzandi</a>
                        <a href="https://unipd.link/TIROCINI" class="button-link">Valutazione tirocini studenti</a>
                    </div>
                </div>

                <div class="section-container">
                    <h2>Login</h2>
                    <div class="button-list">
                        <a href="https://www.eduiss.it/course/view.php?id=521" class="button-link">EDUISS FORMAZIONE SUPERIORE</a>
                        <a href="https://myaccount.google.com/" class="button-link">Gmail</a>
                        <a href="https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=9199bf20-a13f-4107-85dc-02114787ef48&scope=https%3A%2F%2Foutlook.office.com%2F.default%20openid%20profile%20offline_access&redirect_uri=https%3A%2F%2Foutlook.live.com%2Fmail%2F&clien" class="button-link">Outlook</a>
                    </div>
                </div>
                <div class="section-container">
                    <h2>Ricerca</h2>
                    <div class="button-list">
                        <a href="https://pubmed.ncbi.nlm.nih.gov/" class="button-link">PUBMED</a>
                        <a href="https://www.scopus.com/pages/home#author" class="button-link">SCOPUS</a>
                        <a href="https://www.scimagojr.com/" class="button-link">Statistiche riviste</a>
                    </div>
                </div>

            </div>
        </div>

        <div class="tab-content calcolatori">
            <p>Contenuto della scheda Calcolatori.</p>
        </div>

        <div class="tab-content esami">
            <p>Contenuto della scheda Esami Ematochimici.</p>
            <div class="exams-grid">
                <div class="exam-item">
  		   <label for="creatinina">Creatinina</label>
  		   <div style="display: flex; gap: 5px; align-items: center;">
    		   <input type="text" id="creatinina" name="creatinina">
    		   <select id="unit">
      		   <option value="μmol">μmol/L</option>
      		   <option value="mgdl">mg/dL</option>
    		   </select>
    		   <button type="button" onclick="converti()">↔</button>
  		</div>
  		   <p id="risultato" style="font-size:0.9em; color:#bdc3c7; 		   margin-top:5px;"></p>
		</div>

                <div class="exam-item">
                    <label for="ast">AST (U/L)</label>
                    <input type="text" id="ast">
                    <span class="range">Range: 10 - 35</span>
                </div>
                <div class="exam-item">
                    <label for="alt">ALT (U/L)</label>
                    <input type="text" id="alt">
                    <span class="range">Range: 7 - 35</span>
                </div>
                <div class="exam-item">
                    <label for="bilirubina">Bilirubina Totale (umol/L)</label>
                    <input type="text" id="bilirubina">
                    <span class="range">Range: 1,7 - 17,0</span>
                </div>
                <div class="exam-item">
                    <label for="ferro">Ferro (umol/L)</label>
                    <input type="text" id="ferro">
                    <span class="range">Range: 11,6 - 31,3</span>
                </div>
                <div class="exam-item">
                    <label for="transferrina">Transferrina (g/L)</label>
                    <input type="text" id="transferrina">
                    <span class="range">Range: 2,00 - 3,60</span>
                </div>
                <div class="exam-item">
                    <label for="saturazione-transferrina">Saturazione Transferrina (%)</label>
                    <input type="text" id="saturazione-transferrina">
                    <span class="range">Range: 16,00 - 49,00</span>
                </div>
                <div class="exam-item">
                    <label for="ferritina">Ferritina (ug/L)</label>
                    <input type="text" id="ferritina">
                    <span class="range">Range: 31 - 409</span>
                </div>
                <div class="exam-item">
                    <label for="colesterolo-totale">Colesterolo Totale (mmol/L)</label>
                    <input type="text" id="colesterolo-totale">
                    <span class="range">Desiderabile: &lt; 5,18</span>
                </div>
                <div class="exam-item">
                    <label for="hdl">HDL (mmol/L)</label>
                    <input type="text" id="hdl">
                    <span class="range">Desiderabile: > 1,04</span>
                </div>
                <div class="exam-item">
                    <label for="ldl">LDL (mmol/L)</label>
                    <input type="text" id="ldl">
                    <span class="range"></span>
                </div>
                <div class="exam-item">
                    <label for="trigliceridi">Trigliceridi (mmol/L)</label>
                    <input type="text" id="trigliceridi">
                    <span class="range">Desiderabile: < 1,70</span>
                </div>
                <div class="exam-item">
                    <label for="p-calcio">P-Calcio (mmol/L)</label>
                    <input type="text" id="p-calcio">
                    <span class="range">Range: 2,10 - 2,55</span>
                </div>
                <div class="exam-item">
                    <label for="p-fosforo">P-Fosforo (mmol/L)</label>
                    <input type="text" id="p-fosforo">
                    <span class="range"></span>
                </div>
                <div class="exam-item">
                    <label for="diuresi-24h">Diuresi 24h (mL)</label>
                    <input type="text" id="diuresi-24h">
                    <span class="range">Range: ~1500</span>
                </div>
                <div class="exam-item">
                    <label for="u-calcio">U-Calcio (mmol/24h)</label>
                    <input type="text" id="u-calcio">
                    <span class="range">Range: 2,50 - 7,50</span>
                </div>
                <div class="exam-item">
                    <label for="u-fosforo">U-Fosforo (mmol/24h)</label>
                    <input type="text" id="u-fosforo">
                    <span class="range"></span>
                </div>
                <div class="exam-item">
                    <label for="pth">PTH (ng/L)</label>
                    <input type="text" id="pth">
                    <span class="range"></span>
                </div>
                <div class="exam-item">
                    <label for="ctx">CTX (ng/L)</label>
                    <input type="text" id="ctx">
                    <span class="range">Pre-menopausa: 121 - 747</span>
                </div>
                <div class="exam-item">
                    <label for="vitamina-d">Vitamina 25-D (nmol/L)</label>
                    <input type="text" id="vitamina-d">
                    <span class="range">Soglia: > 50</span>
                </div>
            </div>
        </div>        
    </div>

</body>

<script>
function converti() {
  let valore = parseFloat(document.getElementById("creatinina").value);
  let unita = document.getElementById("unit").value;
  let risultato, nuovaUnita;
  
  if (isNaN(valore)) {
    document.getElementById("risultato").innerText = "Inserisci un valore valido.";
    return;
  }
  
  if (unita === "μmol") {
    risultato = (valore / 88.4).toFixed(2);
    nuovaUnita = "mg/dL";
  } else {
    risultato = (valore * 88.4).toFixed(2);
    nuovaUnita = "μmol/L";
  }
  
  document.getElementById("risultato").innerText =
    "Valore convertito: " + risultato + " " + nuovaUnita;
}
</script>

</html>
