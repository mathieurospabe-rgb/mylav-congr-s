<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0">
<title>MYLAV · Contacts Congrès</title>
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;600;700;800&family=DM+Sans:wght@300;400;500&display=swap" rel="stylesheet">
<style>
  :root {
    --navy: #1a2744;
    --navy-2: #253460;
    --gold: #C8973A;
    --gold-l: #e8b55a;
    --bg: #0f1829;
    --bg-2: #162035;
    --surface: #1e2d4a;
    --surface-2: #243558;
    --border: rgba(255,255,255,0.08);
    --border-gold: rgba(200,151,58,0.3);
    --text: #e8edf5;
    --text-mid: #8a9bc0;
    --text-dim: #4a5a7a;
    --success: #2ecc8a;
    --error: #e05c5c;
    --radius: 14px;
  }

  * { margin:0; padding:0; box-sizing:border-box; -webkit-tap-highlight-color:transparent; }

  body {
    font-family: 'DM Sans', sans-serif;
    background: var(--bg);
    color: var(--text);
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  body::before {
    content:'';
    position:fixed;
    inset:0;
    background:
      radial-gradient(ellipse 80% 40% at 50% 0%, rgba(200,151,58,0.07) 0%, transparent 60%),
      radial-gradient(ellipse 60% 60% at 90% 100%, rgba(26,39,68,0.5) 0%, transparent 70%);
    pointer-events:none;
    z-index:0;
  }

  .app {
    width:100%;
    max-width:480px;
    padding:0 16px 60px;
    position:relative;
    z-index:1;
  }

  /* HEADER */
  .header {
    display:flex;
    align-items:center;
    justify-content:space-between;
    padding:20px 0 28px;
  }

  .logo {
    display:flex;
    align-items:center;
    gap:8px;
  }

  .logo-mark {
    width:32px; height:32px;
    border-radius:8px;
    background:linear-gradient(135deg, var(--navy-2), var(--gold));
    display:flex;
    align-items:center;
    justify-content:center;
    font-family:'Syne', sans-serif;
    font-weight:800;
    font-size:13px;
    color:#fff;
    letter-spacing:0.5px;
  }

  .logo-name {
    font-family:'Syne', sans-serif;
    font-weight:700;
    font-size:16px;
    color:var(--text);
    letter-spacing:2px;
  }

  .header-tag {
    font-size:11px;
    font-weight:500;
    color:var(--gold);
    background:rgba(200,151,58,0.1);
    border:1px solid var(--border-gold);
    padding:4px 10px;
    border-radius:100px;
    letter-spacing:0.5px;
  }

  /* CONGRES SELECTOR */
  .congres-bar {
    background:var(--surface);
    border:1px solid var(--border);
    border-radius:var(--radius);
    padding:12px 16px;
    display:flex;
    align-items:center;
    gap:10px;
    margin-bottom:20px;
    cursor:pointer;
    transition:border-color 0.2s;
  }

  .congres-bar:focus-within { border-color:var(--gold); }

  .congres-icon { font-size:18px; }

  .congres-info { flex:1; }

  .congres-label {
    font-size:10px;
    font-weight:500;
    text-transform:uppercase;
    letter-spacing:1px;
    color:var(--text-mid);
    margin-bottom:2px;
  }

  .congres-input {
    background:transparent;
    border:none;
    outline:none;
    font-family:'DM Sans', sans-serif;
    font-size:14px;
    font-weight:500;
    color:var(--text);
    width:100%;
  }

  .congres-input::placeholder { color:var(--text-dim); }

  /* MODE TABS */
  .mode-tabs {
    display:grid;
    grid-template-columns:1fr 1fr;
    gap:8px;
    margin-bottom:20px;
  }

  .mode-tab {
    background:var(--surface);
    border:1.5px solid var(--border);
    border-radius:var(--radius);
    padding:14px 12px;
    cursor:pointer;
    transition:all 0.2s;
    text-align:center;
  }

  .mode-tab.active {
    border-color:var(--gold);
    background:rgba(200,151,58,0.08);
  }

  .mode-tab-icon { font-size:22px; margin-bottom:6px; }

  .mode-tab-label {
    font-size:12px;
    font-weight:600;
    color:var(--text);
    font-family:'Syne', sans-serif;
    margin-bottom:2px;
  }

  .mode-tab-sub {
    font-size:11px;
    color:var(--text-mid);
  }

  /* PANELS */
  .panel { display:none; }
  .panel.active { display:block; animation:fadeUp 0.3s ease both; }

  /* PHOTO UPLOAD */
  .upload-zone {
    border:2px dashed var(--border);
    border-radius:var(--radius);
    padding:32px 20px;
    text-align:center;
    cursor:pointer;
    transition:all 0.2s;
    position:relative;
    overflow:hidden;
    margin-bottom:16px;
  }

  .upload-zone:hover, .upload-zone.drag { border-color:var(--gold); background:rgba(200,151,58,0.04); }

  .upload-zone input {
    position:absolute;
    inset:0;
    opacity:0;
    cursor:pointer;
    width:100%;
    height:100%;
  }

  .upload-icon { font-size:36px; margin-bottom:10px; }
  .upload-title { font-family:'Syne', sans-serif; font-size:15px; font-weight:600; color:var(--text); margin-bottom:4px; }
  .upload-sub { font-size:12px; color:var(--text-mid); }

  #preview-img {
    width:100%;
    border-radius:10px;
    margin-bottom:12px;
    display:none;
    max-height:200px;
    object-fit:cover;
  }

  /* MANUAL MODE */
  .manual-row {
    display:grid;
    grid-template-columns:1fr 1fr;
    gap:10px;
    margin-bottom:10px;
  }

  /* FORM FIELDS */
  .field {
    margin-bottom:10px;
  }

  .field-label {
    font-size:11px;
    font-weight:500;
    text-transform:uppercase;
    letter-spacing:1px;
    color:var(--text-mid);
    margin-bottom:6px;
    display:flex;
    align-items:center;
    gap:6px;
  }

  .field-label .auto-tag {
    font-size:9px;
    background:rgba(200,151,58,0.15);
    color:var(--gold);
    padding:2px 6px;
    border-radius:4px;
    letter-spacing:0.5px;
    font-weight:600;
  }

  .field input, .field select {
    width:100%;
    background:var(--surface);
    border:1.5px solid var(--border);
    border-radius:10px;
    padding:12px 14px;
    font-family:'DM Sans', sans-serif;
    font-size:14px;
    color:var(--text);
    outline:none;
    transition:border-color 0.2s;
    appearance:none;
  }

  .field input:focus, .field select:focus { border-color:var(--gold); }
  .field input::placeholder { color:var(--text-dim); }

  .field input.auto-filled {
    border-color:rgba(46,204,138,0.3);
    background:rgba(46,204,138,0.04);
  }

  /* RESULTS SECTION */
  .results-section {
    background:var(--surface);
    border:1px solid var(--border);
    border-radius:var(--radius);
    padding:16px;
    margin-bottom:16px;
    display:none;
  }

  .results-section.show { display:block; animation:fadeUp 0.3s ease both; }

  .results-header {
    display:flex;
    align-items:center;
    gap:8px;
    margin-bottom:14px;
  }

  .results-header-icon { font-size:16px; }

  .results-header-text {
    font-family:'Syne', sans-serif;
    font-size:13px;
    font-weight:600;
    color:var(--text);
  }

  .results-header-sub { font-size:11px; color:var(--text-mid); margin-top:1px; }

  /* STATUS BAR */
  .status-bar {
    background:var(--surface);
    border:1px solid var(--border);
    border-radius:10px;
    padding:12px 14px;
    display:flex;
    align-items:center;
    gap:10px;
    margin-bottom:16px;
    display:none;
  }

  .status-bar.show { display:flex; animation:fadeUp 0.2s ease both; }

  .status-spinner {
    width:18px; height:18px;
    border:2px solid var(--border);
    border-top-color:var(--gold);
    border-radius:50%;
    animation:spin 0.8s linear infinite;
    flex-shrink:0;
  }

  .status-text { font-size:13px; color:var(--text-mid); }

  /* STATUT SELECT */
  .statut-grid {
    display:grid;
    grid-template-columns:1fr 1fr;
    gap:8px;
    margin-bottom:16px;
  }

  .statut-btn {
    background:var(--surface);
    border:1.5px solid var(--border);
    border-radius:10px;
    padding:10px 8px;
    cursor:pointer;
    text-align:center;
    transition:all 0.15s;
    font-family:'DM Sans', sans-serif;
    font-size:12px;
    font-weight:500;
    color:var(--text-mid);
  }

  .statut-btn.selected {
    border-color:var(--gold);
    background:rgba(200,151,58,0.1);
    color:var(--gold);
  }

  .statut-btn-icon { font-size:16px; display:block; margin-bottom:4px; }

  /* NOTES */
  .field textarea {
    width:100%;
    background:var(--surface);
    border:1.5px solid var(--border);
    border-radius:10px;
    padding:12px 14px;
    font-family:'DM Sans', sans-serif;
    font-size:14px;
    color:var(--text);
    outline:none;
    resize:none;
    min-height:80px;
    transition:border-color 0.2s;
  }

  .field textarea:focus { border-color:var(--gold); }
  .field textarea::placeholder { color:var(--text-dim); }

  /* BTN */
  .btn-submit {
    width:100%;
    padding:16px;
    background:linear-gradient(135deg, var(--gold), var(--gold-l));
    border:none;
    border-radius:var(--radius);
    font-family:'Syne', sans-serif;
    font-size:15px;
    font-weight:700;
    color:#fff;
    cursor:pointer;
    transition:all 0.2s;
    letter-spacing:0.5px;
    display:flex;
    align-items:center;
    justify-content:center;
    gap:8px;
    margin-bottom:12px;
  }

  .btn-submit:hover { transform:translateY(-1px); box-shadow:0 8px 24px rgba(200,151,58,0.25); }
  .btn-submit:disabled { opacity:0.4; cursor:default; transform:none; }

  .btn-search {
    width:100%;
    padding:13px;
    background:var(--surface-2);
    border:1.5px solid var(--border-gold);
    border-radius:var(--radius);
    font-family:'Syne', sans-serif;
    font-size:13px;
    font-weight:600;
    color:var(--gold);
    cursor:pointer;
    transition:all 0.2s;
    display:flex;
    align-items:center;
    justify-content:center;
    gap:8px;
    margin-bottom:16px;
  }

  .btn-search:hover { background:rgba(200,151,58,0.1); }
  .btn-search:disabled { opacity:0.4; cursor:default; }

  /* SUCCESS */
  .success-toast {
    position:fixed;
    bottom:24px;
    left:50%;
    transform:translateX(-50%) translateY(80px);
    background:var(--success);
    color:#fff;
    padding:12px 24px;
    border-radius:100px;
    font-size:14px;
    font-weight:600;
    font-family:'Syne', sans-serif;
    transition:transform 0.3s cubic-bezier(0.34,1.56,0.64,1);
    z-index:100;
    white-space:nowrap;
  }

  .success-toast.show { transform:translateX(-50%) translateY(0); }

  /* CONFIG MODAL */
  .config-btn {
    background:var(--surface);
    border:1px solid var(--border);
    border-radius:8px;
    padding:6px 10px;
    font-size:12px;
    color:var(--text-mid);
    cursor:pointer;
    font-family:'DM Sans', sans-serif;
    transition:all 0.2s;
  }

  .config-btn:hover { border-color:var(--gold); color:var(--gold); }

  .modal-overlay {
    position:fixed;
    inset:0;
    background:rgba(0,0,0,0.6);
    z-index:50;
    display:none;
    align-items:flex-end;
    justify-content:center;
    padding:16px;
  }

  .modal-overlay.show { display:flex; }

  .modal {
    background:var(--bg-2);
    border:1px solid var(--border);
    border-radius:20px 20px 16px 16px;
    padding:24px;
    width:100%;
    max-width:480px;
    animation:slideUp 0.3s ease both;
  }

  .modal-title {
    font-family:'Syne', sans-serif;
    font-size:16px;
    font-weight:700;
    color:var(--text);
    margin-bottom:4px;
  }

  .modal-sub { font-size:13px; color:var(--text-mid); margin-bottom:20px; }

  .modal-close {
    float:right;
    background:none;
    border:none;
    color:var(--text-mid);
    font-size:20px;
    cursor:pointer;
    margin-top:-4px;
  }

  /* SEPARATOR */
  .sep {
    height:1px;
    background:var(--border);
    margin:16px 0;
  }

  .section-title {
    font-family:'Syne', sans-serif;
    font-size:12px;
    font-weight:600;
    color:var(--text-mid);
    text-transform:uppercase;
    letter-spacing:1px;
    margin-bottom:12px;
  }

  /* ANIMATIONS */
  @keyframes fadeUp {
    from { opacity:0; transform:translateY(12px); }
    to { opacity:1; transform:translateY(0); }
  }

  @keyframes spin { to { transform:rotate(360deg); } }

  @keyframes slideUp {
    from { opacity:0; transform:translateY(20px); }
    to { opacity:1; transform:translateY(0); }
  }

  /* COUNTER */
  .counter-bar {
    display:flex;
    align-items:center;
    justify-content:space-between;
    background:var(--surface);
    border:1px solid var(--border);
    border-radius:10px;
    padding:10px 14px;
    margin-bottom:20px;
    font-size:13px;
  }

  .counter-num {
    font-family:'Syne', sans-serif;
    font-size:20px;
    font-weight:700;
    color:var(--gold);
  }

  .counter-label { color:var(--text-mid); font-size:12px; }
</style>
</head>
<body>
<div class="app">

  <!-- HEADER -->
  <div class="header">
    <div class="logo">
      <div class="logo-mark">ML</div>
      <div class="logo-name">MYLAV</div>
    </div>
    <div style="display:flex;gap:8px;align-items:center;">
      <div class="header-tag">Congrès</div>
      <button class="config-btn" onclick="openConfig()">⚙ Config</button>
    </div>
  </div>

  <!-- CONGRES NAME -->
  <div class="congres-bar">
    <div class="congres-icon">📍</div>
    <div class="congres-info">
      <div class="congres-label">Congrès actuel</div>
      <input class="congres-input" id="congres-name" type="text" placeholder="Ex : GEO 2026 – Le Pouliguen" />
    </div>
  </div>

  <!-- COUNTER -->
  <div class="counter-bar">
    <div>
      <div class="counter-label">Contacts enregistrés aujourd'hui</div>
    </div>
    <div class="counter-num" id="counter">0</div>
  </div>

  <!-- MODE TABS -->
  <div class="mode-tabs">
    <div class="mode-tab active" id="tab-scan" onclick="switchMode('scan')">
      <div class="mode-tab-icon">📷</div>
      <div class="mode-tab-label">Scanner badge</div>
      <div class="mode-tab-sub">Photo → extraction auto</div>
    </div>
    <div class="mode-tab" id="tab-manual" onclick="switchMode('manual')">
      <div class="mode-tab-icon">✏️</div>
      <div class="mode-tab-label">Saisie manuelle</div>
      <div class="mode-tab-sub">Nom → recherche auto</div>
    </div>
  </div>

  <!-- SCAN PANEL -->
  <div class="panel active" id="panel-scan">
    <div class="upload-zone" id="upload-zone">
      <input type="file" id="badge-input" accept="image/*" capture="environment" onchange="handleImage(event)" />
      <div class="upload-icon">🪪</div>
      <div class="upload-title">Photographier le badge</div>
      <div class="upload-sub">Appuyez pour ouvrir l'appareil photo</div>
    </div>
    <img id="preview-img" alt="Badge" />
    <button class="btn-search" id="btn-extract" onclick="extractFromBadge()" disabled>
      <span>🔍</span> Extraire les informations du badge
    </button>
  </div>

  <!-- MANUAL PANEL -->
  <div class="panel" id="panel-manual">
    <div class="manual-row">
      <div class="field">
        <div class="field-label">Prénom</div>
        <input type="text" id="manual-prenom" placeholder="Marie" />
      </div>
      <div class="field">
        <div class="field-label">Nom</div>
        <input type="text" id="manual-nom" placeholder="Dupont" />
      </div>
    </div>
    <button class="btn-search" id="btn-search-manual" onclick="searchFromName()">
      <span>🔍</span> Rechercher la clinique automatiquement
    </button>
  </div>

  <!-- STATUS -->
  <div class="status-bar" id="status-bar">
    <div class="status-spinner"></div>
    <div class="status-text" id="status-text">Analyse en cours…</div>
  </div>

  <!-- RESULTS / FORM -->
  <div class="results-section" id="results-section">
    <div class="results-header">
      <div class="results-header-icon">✦</div>
      <div>
        <div class="results-header-text">Fiche contact</div>
        <div class="results-header-sub">Vérifiez et complétez si besoin</div>
      </div>
    </div>

    <div class="manual-row">
      <div class="field">
        <div class="field-label">Prénom</div>
        <input type="text" id="f-prenom" placeholder="Marie" />
      </div>
      <div class="field">
        <div class="field-label">Nom</div>
        <input type="text" id="f-nom" placeholder="Dupont" />
      </div>
    </div>

    <div class="field">
      <div class="field-label">Clinique <span class="auto-tag">AUTO</span></div>
      <input type="text" id="f-clinique" placeholder="Clinique Vétérinaire…" />
    </div>

    <div class="manual-row">
      <div class="field">
        <div class="field-label">Ville <span class="auto-tag">AUTO</span></div>
        <input type="text" id="f-ville" placeholder="Paris" />
      </div>
      <div class="field">
        <div class="field-label">Téléphone <span class="auto-tag">AUTO</span></div>
        <input type="tel" id="f-tel" placeholder="01 23 45 67 89" />
      </div>
    </div>

    <div class="field">
      <div class="field-label">Email professionnel</div>
      <input type="email" id="f-email" placeholder="marie.dupont@clinique.fr" />
    </div>

    <div class="sep"></div>

    <div class="section-title">Statut</div>
    <div class="statut-grid">
      <button class="statut-btn" onclick="selectStatut(this, 'Client MYLAV')">
        <span class="statut-btn-icon">✅</span>Déjà client
      </button>
      <button class="statut-btn" onclick="selectStatut(this, 'Prospect chaud')">
        <span class="statut-btn-icon">🔥</span>Prospect chaud
      </button>
      <button class="statut-btn" onclick="selectStatut(this, 'Prospect froid')">
        <span class="statut-btn-icon">❄️</span>Prospect froid
      </button>
      <button class="statut-btn" onclick="selectStatut(this, 'À recontacter')">
        <span class="statut-btn-icon">📞</span>À recontacter
      </button>
    </div>

    <div class="field">
      <div class="field-label">Note du commercial</div>
      <textarea id="f-note" placeholder="Contexte, intérêt exprimé, suite à donner…"></textarea>
    </div>

    <button class="btn-submit" id="btn-submit" onclick="submitToNotion()">
      <span>💾</span> Enregistrer dans Notion
    </button>
  </div>

</div>

<!-- CONFIG MODAL -->
<div class="modal-overlay" id="modal-overlay" onclick="closeConfigOutside(event)">
  <div class="modal">
    <button class="modal-close" onclick="closeConfig()">×</button>
    <div class="modal-title">Configuration</div>
    <div class="modal-sub">Renseignez vos clés API une seule fois</div>

    <div class="field">
      <div class="field-label">Clé API Anthropic</div>
      <input type="password" id="cfg-anthropic" placeholder="sk-ant-…" />
    </div>

    <div class="field">
      <div class="field-label">Token d'intégration Notion</div>
      <input type="password" id="cfg-notion-token" placeholder="secret_…" />
    </div>

    <div class="field">
      <div class="field-label">ID base Notion "Contacts Congrès"</div>
      <input type="text" id="cfg-notion-db" placeholder="xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx" />
    </div>

    <div class="field">
      <div class="field-label">Commercial (prénom)</div>
      <input type="text" id="cfg-commercial" placeholder="Ex : Quentin" />
    </div>

    <button class="btn-submit" onclick="saveConfig()" style="margin-top:8px;">
      <span>✓</span> Sauvegarder
    </button>
  </div>
</div>

<!-- TOAST -->
<div class="success-toast" id="toast">✓ Contact enregistré dans Notion</div>

<script>
// ─── CONFIG ───
function loadConfig() {
  return {
    anthropicKey: localStorage.getItem('ml_anthropic') || '',
    notionToken: localStorage.getItem('ml_notion_token') || '',
    notionDb: localStorage.getItem('ml_notion_db') || '',
    commercial: localStorage.getItem('ml_commercial') || ''
  };
}

function saveConfig() {
  localStorage.setItem('ml_anthropic', document.getElementById('cfg-anthropic').value.trim());
  localStorage.setItem('ml_notion_token', document.getElementById('cfg-notion-token').value.trim());
  localStorage.setItem('ml_notion_db', document.getElementById('cfg-notion-db').value.trim());
  localStorage.setItem('ml_commercial', document.getElementById('cfg-commercial').value.trim());
  closeConfig();
  showToast('✓ Configuration sauvegardée');
}

function openConfig() {
  const cfg = loadConfig();
  document.getElementById('cfg-anthropic').value = cfg.anthropicKey;
  document.getElementById('cfg-notion-token').value = cfg.notionToken;
  document.getElementById('cfg-notion-db').value = cfg.notionDb;
  document.getElementById('cfg-commercial').value = cfg.commercial;
  document.getElementById('modal-overlay').classList.add('show');
}

function closeConfig() { document.getElementById('modal-overlay').classList.remove('show'); }
function closeConfigOutside(e) { if (e.target === document.getElementById('modal-overlay')) closeConfig(); }

// ─── COUNTER ───
let sessionCount = parseInt(sessionStorage.getItem('ml_count') || '0');
function updateCounter() {
  sessionStorage.setItem('ml_count', sessionCount);
  document.getElementById('counter').textContent = sessionCount;
}
updateCounter();

// ─── MODE SWITCH ───
function switchMode(mode) {
  document.getElementById('tab-scan').classList.toggle('active', mode === 'scan');
  document.getElementById('tab-manual').classList.toggle('active', mode === 'manual');
  document.getElementById('panel-scan').classList.toggle('active', mode === 'scan');
  document.getElementById('panel-manual').classList.toggle('active', mode === 'manual');
  hideResults();
}

// ─── IMAGE HANDLING ───
let currentImageBase64 = null;

function handleImage(e) {
  const file = e.target.files[0];
  if (!file) return;
  const reader = new FileReader();
  reader.onload = ev => {
    currentImageBase64 = ev.target.result.split(',')[1];
    const img = document.getElementById('preview-img');
    img.src = ev.target.result;
    img.style.display = 'block';
    document.getElementById('btn-extract').disabled = false;
  };
  reader.readAsDataURL(file);
}

// ─── EXTRACT FROM BADGE (OCR via Claude) ───
async function extractFromBadge() {
  const cfg = loadConfig();
  if (!cfg.anthropicKey) { alert('Configurez votre clé API Anthropic d\'abord (⚙ Config)'); return; }
  if (!currentImageBase64) return;

  showStatus('Lecture du badge en cours…');

  try {
    const response = await fetch('https://api.anthropic.com/v1/messages', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json', 'x-api-key': cfg.anthropicKey, 'anthropic-version': '2023-06-01' },
      body: JSON.stringify({
        model: 'claude-sonnet-4-20250514',
        max_tokens: 300,
        messages: [{
          role: 'user',
          content: [
            { type: 'image', source: { type: 'base64', media_type: 'image/jpeg', data: currentImageBase64 } },
            { type: 'text', text: `C'est un badge de congrès vétérinaire. Extrais uniquement : prénom, nom, clinique/établissement, ville. Réponds UNIQUEMENT en JSON strict sans markdown : {"prenom":"","nom":"","clinique":"","ville":""}. Si une info est absente, laisse la valeur vide.` }
          ]
        }]
      })
    });

    const data = await response.json();
    const text = data.content?.[0]?.text || '{}';
    const clean = text.replace(/```json|```/g, '').trim();
    const parsed = JSON.parse(clean);

    document.getElementById('f-prenom').value = parsed.prenom || '';
    document.getElementById('f-nom').value = parsed.nom || '';
    document.getElementById('f-clinique').value = parsed.clinique || '';
    document.getElementById('f-ville').value = parsed.ville || '';

    hideStatus();

    // Si nom extrait, lancer la recherche complémentaire
    if (parsed.prenom || parsed.nom) {
      await enrichContact(parsed.prenom, parsed.nom, parsed.clinique, parsed.ville);
    } else {
      showResults();
    }

  } catch(err) {
    hideStatus();
    showResults();
    console.error(err);
  }
}

// ─── SEARCH FROM NAME ───
async function searchFromName() {
  const prenom = document.getElementById('manual-prenom').value.trim();
  const nom = document.getElementById('manual-nom').value.trim();
  if (!prenom && !nom) { alert('Saisissez au moins un nom ou prénom.'); return; }

  document.getElementById('f-prenom').value = prenom;
  document.getElementById('f-nom').value = nom;
  document.getElementById('f-clinique').value = '';
  document.getElementById('f-ville').value = '';
  document.getElementById('f-tel').value = '';

  await enrichContact(prenom, nom, '', '');
}

// ─── ENRICH CONTACT (Claude web search) ───
async function enrichContact(prenom, nom, cliniqueConnue, villeConnue) {
  const cfg = loadConfig();
  if (!cfg.anthropicKey) { showResults(); return; }

  showStatus('Recherche de la clinique en cours…');

  const nomComplet = `${prenom} ${nom}`.trim();
  const contexteClinique = cliniqueConnue ? `, clinique : ${cliniqueConnue}` : '';
  const contexteVille = villeConnue ? `, ville : ${villeConnue}` : '';

  try {
    const response = await fetch('https://api.anthropic.com/v1/messages', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json', 'x-api-key': cfg.anthropicKey, 'anthropic-version': '2023-06-01' },
      body: JSON.stringify({
        model: 'claude-sonnet-4-20250514',
        max_tokens: 400,
        tools: [{ type: 'web_search_20250305', name: 'web_search' }],
        messages: [{
          role: 'user',
          content: `Tu es un assistant de recherche. Trouve les informations professionnelles du vétérinaire suivant en France : ${nomComplet}${contexteClinique}${contexteVille}. Recherche sa clinique vétérinaire, sa ville d'exercice et le téléphone de la clinique. Réponds UNIQUEMENT avec ce JSON strict sans markdown ni explication : {"clinique":"","ville":"","telephone":""}. Si une information est introuvable, laisse la valeur vide. Ne devine pas.`
        }]
      })
    });

    const data = await response.json();
    // Chercher le dernier bloc texte (après tool use)
    let text = '';
    for (const block of (data.content || [])) {
      if (block.type === 'text') text = block.text;
    }
    const clean = text.replace(/```json|```/g, '').trim();

    try {
      const parsed = JSON.parse(clean);
      if (parsed.clinique && !document.getElementById('f-clinique').value) {
        document.getElementById('f-clinique').value = parsed.clinique;
        document.getElementById('f-clinique').classList.add('auto-filled');
      }
      if (parsed.ville && !document.getElementById('f-ville').value) {
        document.getElementById('f-ville').value = parsed.ville;
        document.getElementById('f-ville').classList.add('auto-filled');
      }
      if (parsed.telephone) {
        document.getElementById('f-tel').value = parsed.telephone;
        document.getElementById('f-tel').classList.add('auto-filled');
      }
    } catch(e) {}

  } catch(err) {
    console.error('Enrichissement échoué:', err);
  }

  hideStatus();
  showResults();
}

// ─── STATUT ───
let selectedStatut = '';

function selectStatut(btn, value) {
  document.querySelectorAll('.statut-btn').forEach(b => b.classList.remove('selected'));
  btn.classList.add('selected');
  selectedStatut = value;
}

// ─── SUBMIT TO NOTION ───
async function submitToNotion() {
  const cfg = loadConfig();
  if (!cfg.notionToken || !cfg.notionDb) {
    alert('Configurez le token Notion et l\'ID de la base dans ⚙ Config');
    return;
  }

  const prenom = document.getElementById('f-prenom').value.trim();
  const nom = document.getElementById('f-nom').value.trim();
  if (!prenom && !nom) { alert('Renseignez au moins le nom du vétérinaire.'); return; }

  const btn = document.getElementById('btn-submit');
  btn.disabled = true;
  btn.innerHTML = '<span>⏳</span> Enregistrement…';

  const congres = document.getElementById('congres-name').value.trim() || 'Congrès non précisé';
  const today = new Date().toISOString().split('T')[0];

  const payload = {
    parent: { database_id: cfg.notionDb.replace(/-/g, '') },
    properties: {
      "Nom": { title: [{ text: { content: `${prenom} ${nom}`.trim() } }] },
      "Prénom": { rich_text: [{ text: { content: prenom } }] },
      "Nom de famille": { rich_text: [{ text: { content: nom } }] },
      "Clinique": { rich_text: [{ text: { content: document.getElementById('f-clinique').value.trim() } }] },
      "Ville": { rich_text: [{ text: { content: document.getElementById('f-ville').value.trim() } }] },
      "Téléphone": { phone_number: document.getElementById('f-tel').value.trim() || null },
      "Email": { email: document.getElementById('f-email').value.trim() || null },
      "Statut": { select: selectedStatut ? { name: selectedStatut } : null },
      "Congrès": { rich_text: [{ text: { content: congres } }] },
      "Date de contact": { date: { start: today } },
      "Commercial": { rich_text: [{ text: { content: cfg.commercial } }] },
      "Notes": { rich_text: [{ text: { content: document.getElementById('f-note').value.trim() } }] }
    }
  };

  // Nettoyer les nulls
  for (const key in payload.properties) {
    const v = payload.properties[key];
    if (v.phone_number === null) delete payload.properties[key];
    if (v.email === null) delete payload.properties[key];
    if (v.select?.name === null) delete payload.properties[key];
  }

  try {
    const res = await fetch('https://api.anthropic.com/v1/messages', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json', 'x-api-key': cfg.anthropicKey, 'anthropic-version': '2023-06-01' },
      body: JSON.stringify({
        model: 'claude-sonnet-4-20250514',
        max_tokens: 200,
        mcp_servers: [{ type: 'url', url: 'https://mcp.notion.com/mcp', name: 'notion', authorization_token: cfg.notionToken }],
        messages: [{
          role: 'user',
          content: `Crée une nouvelle page dans la base Notion avec l'ID "${cfg.notionDb}" avec ces propriétés : ${JSON.stringify({
            nom: `${prenom} ${nom}`.trim(),
            prenom, nom,
            clinique: document.getElementById('f-clinique').value.trim(),
            ville: document.getElementById('f-ville').value.trim(),
            telephone: document.getElementById('f-tel').value.trim(),
            email: document.getElementById('f-email').value.trim(),
            statut: selectedStatut,
            congres,
            date: today,
            commercial: cfg.commercial,
            notes: document.getElementById('f-note').value.trim()
          })}. Réponds uniquement "OK" si réussi.`
        }]
      })
    });

    sessionCount++;
    updateCounter();
    showToast(`✓ ${prenom} ${nom} enregistré(e) dans Notion`);
    resetForm();

  } catch(err) {
    alert('Erreur lors de l\'envoi vers Notion. Vérifiez la configuration.');
    console.error(err);
  }

  btn.disabled = false;
  btn.innerHTML = '<span>💾</span> Enregistrer dans Notion';
}

// ─── HELPERS ───
function showStatus(msg) {
  document.getElementById('status-text').textContent = msg;
  document.getElementById('status-bar').classList.add('show');
}

function hideStatus() {
  document.getElementById('status-bar').classList.remove('show');
}

function showResults() {
  document.getElementById('results-section').classList.add('show');
}

function hideResults() {
  document.getElementById('results-section').classList.remove('show');
}

function showToast(msg) {
  const t = document.getElementById('toast');
  t.textContent = msg;
  t.classList.add('show');
  setTimeout(() => t.classList.remove('show'), 3000);
}

function resetForm() {
  ['f-prenom','f-nom','f-clinique','f-ville','f-tel','f-email','f-note'].forEach(id => {
    const el = document.getElementById(id);
    el.value = '';
    el.classList.remove('auto-filled');
  });
  document.querySelectorAll('.statut-btn').forEach(b => b.classList.remove('selected'));
  selectedStatut = '';
  document.getElementById('preview-img').style.display = 'none';
  document.getElementById('btn-extract').disabled = true;
  currentImageBase64 = null;
  document.getElementById('badge-input').value = '';
  document.getElementById('manual-prenom').value = '';
  document.getElementById('manual-nom').value = '';
  hideResults();
}
</script>
</body>
</html>
