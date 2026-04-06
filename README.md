<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>DESPS · Parc Informatique</title>
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;600;700;800&family=IBM+Plex+Mono:wght@400;500&family=Outfit:wght@300;400;500;600&display=swap" rel="stylesheet">
<style>
  :root {
    --navy: #0a1628;
    --blue-dark: #0d2144;
    --blue-mid: #1a4080;
    --blue: #1e5cb3;
    --blue-light: #3b82d4;
    --accent: #00c9a7;
    --accent2: #f59e0b;
    --accent3: #ef4444;
    --white: #f8fafc;
    --gray1: #e2e8f0;
    --gray2: #94a3b8;
    --gray3: #475569;
    --surface: #0f1f3d;
    --surface2: #132540;
    --card: #162a4a;
    --border: rgba(59,130,212,0.2);
  }
  * { margin:0; padding:0; box-sizing:border-box; }
  body {
    font-family: 'Outfit', sans-serif;
    background: var(--navy);
    color: var(--white);
    min-height: 100vh;
    overflow-x: hidden;
  }

  /* SIDEBAR */
  .sidebar {
    position: fixed; left:0; top:0; bottom:0; width:240px;
    background: var(--blue-dark);
    border-right: 1px solid var(--border);
    display: flex; flex-direction: column;
    z-index: 100;
    transition: transform 0.3s ease;
  }
  .sidebar-logo {
    padding: 24px 20px 16px;
    border-bottom: 1px solid var(--border);
  }
  .sidebar-logo .org { font-family:'Syne',sans-serif; font-weight:800; font-size:13px; color:var(--accent); letter-spacing:2px; text-transform:uppercase; }
  .sidebar-logo .title { font-family:'Syne',sans-serif; font-weight:700; font-size:18px; color:var(--white); line-height:1.2; margin-top:2px; }
  .sidebar-logo .subtitle { font-size:11px; color:var(--gray2); margin-top:4px; }
  .nav-section { padding:12px 12px 4px; font-size:10px; color:var(--gray2); letter-spacing:2px; text-transform:uppercase; font-family:'IBM Plex Mono',monospace; }
  .nav-item {
    display:flex; align-items:center; gap:10px;
    padding:10px 16px; margin:2px 8px; border-radius:8px;
    cursor:pointer; font-size:14px; font-weight:500; color:var(--gray2);
    transition:all 0.2s;
  }
  .nav-item:hover { background:rgba(59,130,212,0.12); color:var(--white); }
  .nav-item.active { background:linear-gradient(135deg,rgba(30,92,179,0.4),rgba(0,201,167,0.15)); color:var(--white); border-left:3px solid var(--accent); margin-left:5px; }
  .nav-item .nav-icon { font-size:18px; width:22px; text-align:center; }
  .nav-badge { margin-left:auto; background:var(--blue); color:var(--white); font-size:10px; padding:2px 7px; border-radius:20px; font-family:'IBM Plex Mono',monospace; }
  .sidebar-bottom { margin-top:auto; padding:16px; border-top:1px solid var(--border); }
  .sidebar-user { font-size:12px; color:var(--gray2); }
  .sidebar-user strong { color:var(--white); display:block; font-size:13px; }

  /* MAIN CONTENT */
  .main { margin-left:240px; min-height:100vh; display:flex; flex-direction:column; }
  .topbar {
    height:60px; background:var(--surface); border-bottom:1px solid var(--border);
    display:flex; align-items:center; padding:0 24px; gap:16px; position:sticky; top:0; z-index:50;
  }
  .topbar-title { font-family:'Syne',sans-serif; font-weight:700; font-size:16px; flex:1; }
  .search-bar {
    display:flex; align-items:center; gap:8px;
    background:var(--card); border:1px solid var(--border); border-radius:8px;
    padding:8px 14px; min-width:300px;
  }
  .search-bar input {
    background:none; border:none; outline:none; color:var(--white); font-size:14px; flex:1;
    font-family:'Outfit',sans-serif;
  }
  .search-bar input::placeholder { color:var(--gray2); }
  .btn {
    padding:8px 16px; border-radius:8px; border:none; cursor:pointer;
    font-family:'Outfit',sans-serif; font-size:13px; font-weight:600;
    display:flex; align-items:center; gap:6px; transition:all 0.2s;
  }
  .btn-primary { background:var(--accent); color:var(--navy); }
  .btn-primary:hover { background:#00b896; transform:translateY(-1px); }
  .btn-secondary { background:var(--card); color:var(--white); border:1px solid var(--border); }
  .btn-secondary:hover { background:var(--blue-mid); border-color:var(--blue-light); }
  .btn-danger { background:rgba(239,68,68,0.2); color:#ef4444; border:1px solid rgba(239,68,68,0.3); }
  .btn-danger:hover { background:rgba(239,68,68,0.35); }
  .btn-sm { padding:5px 11px; font-size:12px; }
  .btn-icon { padding:7px 10px; font-size:16px; }

  /* CONTENT */
  .content { flex:1; padding:24px; }

  /* STAT CARDS */
  .stats-grid { display:grid; grid-template-columns:repeat(4,1fr); gap:16px; margin-bottom:24px; }
  .stat-card {
    background:var(--card); border:1px solid var(--border); border-radius:12px;
    padding:20px; position:relative; overflow:hidden;
    transition:transform 0.2s, box-shadow 0.2s;
  }
  .stat-card:hover { transform:translateY(-2px); box-shadow:0 8px 24px rgba(0,0,0,0.3); }
  .stat-card::before { content:''; position:absolute; top:0; right:0; width:60px; height:60px; border-radius:0 12px 0 60px; }
  .stat-card.blue::before { background:rgba(30,92,179,0.3); }
  .stat-card.green::before { background:rgba(0,201,167,0.3); }
  .stat-card.orange::before { background:rgba(245,158,11,0.3); }
  .stat-card.red::before { background:rgba(239,68,68,0.3); }
  .stat-label { font-size:11px; color:var(--gray2); text-transform:uppercase; letter-spacing:1px; margin-bottom:8px; }
  .stat-value { font-family:'Syne',sans-serif; font-size:32px; font-weight:800; }
  .stat-card.blue .stat-value { color:var(--blue-light); }
  .stat-card.green .stat-value { color:var(--accent); }
  .stat-card.orange .stat-value { color:var(--accent2); }
  .stat-card.red .stat-value { color:var(--accent3); }
  .stat-sub { font-size:12px; color:var(--gray2); margin-top:4px; }

  /* TABLE */
  .table-wrapper {
    background:var(--card); border:1px solid var(--border); border-radius:12px; overflow:hidden;
  }
  .table-header {
    display:flex; align-items:center; justify-content:space-between;
    padding:16px 20px; border-bottom:1px solid var(--border);
    background:rgba(0,0,0,0.2);
  }
  .table-header h3 { font-family:'Syne',sans-serif; font-weight:700; font-size:15px; }
  .table-actions { display:flex; gap:8px; align-items:center; }
  .filter-row { padding:12px 20px; border-bottom:1px solid var(--border); display:flex; gap:10px; flex-wrap:wrap; }
  select.filter-select {
    background:var(--surface); border:1px solid var(--border); color:var(--white);
    padding:6px 10px; border-radius:6px; font-size:12px; font-family:'Outfit',sans-serif;
    cursor:pointer; outline:none;
  }
  .table-scroll { overflow-x:auto; }
  table { width:100%; border-collapse:collapse; }
  thead { background:rgba(0,0,0,0.3); }
  th { padding:10px 14px; text-align:left; font-size:11px; font-weight:600; color:var(--gray2); text-transform:uppercase; letter-spacing:1px; white-space:nowrap; }
  td { padding:10px 14px; font-size:13px; border-bottom:1px solid rgba(59,130,212,0.08); vertical-align:middle; }
  tr:last-child td { border-bottom:none; }
  tr:hover td { background:rgba(30,92,179,0.08); }
  .badge {
    display:inline-block; padding:3px 9px; border-radius:20px; font-size:11px; font-weight:600;
    font-family:'IBM Plex Mono',monospace;
  }
  .badge-green { background:rgba(0,201,167,0.15); color:var(--accent); border:1px solid rgba(0,201,167,0.3); }
  .badge-orange { background:rgba(245,158,11,0.15); color:var(--accent2); border:1px solid rgba(245,158,11,0.3); }
  .badge-red { background:rgba(239,68,68,0.15); color:#ef4444; border:1px solid rgba(239,68,68,0.3); }
  .badge-blue { background:rgba(59,130,212,0.15); color:var(--blue-light); border:1px solid rgba(59,130,212,0.3); }
  .badge-gray { background:rgba(148,163,184,0.15); color:var(--gray2); border:1px solid rgba(148,163,184,0.3); }
  .actions-cell { display:flex; gap:6px; }
  .icon-btn { background:none; border:none; cursor:pointer; padding:5px; border-radius:6px; font-size:15px; transition:background 0.15s; }
  .icon-btn:hover { background:rgba(255,255,255,0.1); }
  .pagination { display:flex; align-items:center; justify-content:space-between; padding:12px 20px; border-top:1px solid var(--border); }
  .pagination-info { font-size:13px; color:var(--gray2); }
  .pagination-btns { display:flex; gap:4px; }
  .pag-btn { padding:5px 10px; border-radius:6px; background:var(--surface); border:1px solid var(--border); color:var(--white); cursor:pointer; font-size:12px; transition:all 0.15s; }
  .pag-btn:hover { background:var(--blue-mid); }
  .pag-btn.active { background:var(--blue); border-color:var(--blue-light); }
  .pag-btn:disabled { opacity:0.4; cursor:default; }

  /* MODAL */
  .modal-overlay {
    display:none; position:fixed; inset:0; background:rgba(0,0,0,0.7); z-index:200;
    align-items:center; justify-content:center; backdrop-filter:blur(4px);
  }
  .modal-overlay.active { display:flex; }
  .modal {
    background:var(--blue-dark); border:1px solid var(--border); border-radius:16px;
    width:660px; max-width:95vw; max-height:90vh; overflow-y:auto;
    animation: slideUp 0.3s ease;
  }
  @keyframes slideUp { from { transform:translateY(30px); opacity:0; } to { transform:translateY(0); opacity:1; } }
  .modal-header {
    padding:20px 24px; border-bottom:1px solid var(--border); display:flex; align-items:center; justify-content:space-between;
    position:sticky; top:0; background:var(--blue-dark); z-index:1;
  }
  .modal-header h3 { font-family:'Syne',sans-serif; font-size:16px; font-weight:700; }
  .modal-close { background:none; border:none; color:var(--gray2); font-size:22px; cursor:pointer; padding:4px; line-height:1; }
  .modal-close:hover { color:var(--white); }
  .modal-body { padding:24px; }
  .form-grid { display:grid; grid-template-columns:1fr 1fr; gap:16px; }
  .form-group { display:flex; flex-direction:column; gap:6px; }
  .form-group.full { grid-column:1/-1; }
  .form-group label { font-size:12px; color:var(--gray2); font-weight:500; text-transform:uppercase; letter-spacing:0.5px; }
  .form-group input, .form-group select, .form-group textarea {
    background:var(--surface); border:1px solid var(--border); color:var(--white);
    padding:9px 12px; border-radius:8px; font-size:13px; font-family:'Outfit',sans-serif;
    outline:none; transition:border-color 0.2s;
  }
  .form-group input:focus, .form-group select:focus, .form-group textarea:focus { border-color:var(--blue-light); }
  .form-group textarea { resize:vertical; min-height:70px; }
  .modal-footer { padding:16px 24px; border-top:1px solid var(--border); display:flex; justify-content:flex-end; gap:10px; }

  /* TABS */
  .tabs { display:flex; gap:4px; padding:0 20px; border-bottom:1px solid var(--border); background:rgba(0,0,0,0.2); }
  .tab { padding:12px 16px; font-size:13px; cursor:pointer; color:var(--gray2); border-bottom:2px solid transparent; margin-bottom:-1px; transition:all 0.2s; }
  .tab:hover { color:var(--white); }
  .tab.active { color:var(--accent); border-bottom-color:var(--accent); font-weight:600; }

  /* IMPORT/EXPORT */
  .upload-zone {
    border:2px dashed var(--border); border-radius:12px; padding:32px;
    text-align:center; cursor:pointer; transition:all 0.2s;
    background:rgba(30,92,179,0.05);
  }
  .upload-zone:hover { border-color:var(--blue-light); background:rgba(30,92,179,0.1); }
  .upload-zone .icon { font-size:40px; margin-bottom:12px; }
  .upload-zone h4 { font-size:15px; font-weight:600; margin-bottom:6px; }
  .upload-zone p { font-size:13px; color:var(--gray2); }
  .page { display:none; }
  .page.active { display:block; }

  /* DETAIL VIEW */
  .detail-grid { display:grid; grid-template-columns:1fr 1fr; gap:16px; }
  .detail-item { background:var(--surface); border:1px solid var(--border); border-radius:8px; padding:12px; }
  .detail-label { font-size:11px; color:var(--gray2); text-transform:uppercase; letter-spacing:1px; margin-bottom:4px; }
  .detail-value { font-size:14px; font-weight:500; }

  /* SCROLLBAR */
  ::-webkit-scrollbar { width:6px; height:6px; }
  ::-webkit-scrollbar-track { background:var(--navy); }
  ::-webkit-scrollbar-thumb { background:var(--blue-mid); border-radius:3px; }
  ::-webkit-scrollbar-thumb:hover { background:var(--blue); }

  /* NOTIFICATION */
  .notif { position:fixed; top:20px; right:20px; z-index:999; padding:12px 18px; border-radius:10px; font-size:14px; font-weight:500; display:flex; align-items:center; gap:8px; animation:slideIn 0.3s ease; box-shadow:0 4px 20px rgba(0,0,0,0.4); }
  @keyframes slideIn { from { transform:translateX(100px); opacity:0; } }
  .notif-success { background:#0d3d2e; border:1px solid var(--accent); color:var(--accent); }
  .notif-error { background:#3d0d0d; border:1px solid #ef4444; color:#ef4444; }
  .notif-info { background:#0d2144; border:1px solid var(--blue-light); color:var(--blue-light); }

  /* RESPONSIVE HIDE */
  .hide-sm { display:table-cell; }
  @media(max-width:900px) { .hide-sm { display:none!important; } }

  /* EMPTY STATE */
  .empty-state { text-align:center; padding:60px 20px; color:var(--gray2); }
  .empty-state .icon { font-size:48px; margin-bottom:12px; }

  /* KOBO CARD */
  .kobo-grid { display:grid; grid-template-columns:repeat(auto-fill,minmax(280px,1fr)); gap:16px; }
  .kobo-card { background:var(--card); border:1px solid var(--border); border-radius:12px; overflow:hidden; transition:transform 0.2s; }
  .kobo-card:hover { transform:translateY(-3px); box-shadow:0 12px 32px rgba(0,0,0,0.4); }
  .kobo-card-img { height:120px; background:var(--surface2); display:flex; align-items:center; justify-content:center; font-size:40px; }
  .kobo-card-body { padding:14px; }
  .kobo-card-body h4 { font-size:14px; font-weight:600; margin-bottom:6px; }
  .kobo-card-meta { font-size:12px; color:var(--gray2); display:flex; flex-direction:column; gap:3px; }

  /* HEADER GRADIENT LINE */
  .gradient-line { height:3px; background:linear-gradient(90deg,var(--blue),var(--accent),var(--blue-light)); }
</style>
</head>
<body>

<aside class="sidebar">
  <div class="sidebar-logo">
    <div class="org">MENAET · DESPS</div>
    <div class="title">Parc Informatique</div>
    <div class="subtitle">Base de données matériels</div>
  </div>
  <div class="gradient-line"></div>
  
  <div class="nav-section">Navigation</div>
  <div class="nav-item active" onclick="showPage('dashboard')">
    <span class="nav-icon">📊</span> Tableau de bord
  </div>
  <div class="nav-item" onclick="showPage('ordinateurs')">
    <span class="nav-icon">💻</span> Ordinateurs
    <span class="nav-badge" id="badge-ordi">—</span>
  </div>
  <div class="nav-item" onclick="showPage('portables')">
    <span class="nav-icon">🖥️</span> PC Portable
    <span class="nav-badge" id="badge-port">—</span>
  </div>
  <div class="nav-item" onclick="showPage('imprimantes')">
    <span class="nav-icon">🖨️</span> Imprimantes
    <span class="nav-badge" id="badge-impr">—</span>
  </div>
  <div class="nav-item" onclick="showPage('tablettes')">
    <span class="nav-icon">📱</span> Tablettes &amp; Autres
    <span class="nav-badge" id="badge-tab">—</span>
  </div>
  <div class="nav-item" onclick="showPage('kobo')">
    <span class="nav-icon">🔗</span> Base KoboToolbox
    <span class="nav-badge" id="badge-kobo">—</span>
  </div>

  <div class="nav-section">Outils</div>
  <div class="nav-item" onclick="showPage('import')">
    <span class="nav-icon">📥</span> Import / Export
  </div>

  <div class="sidebar-bottom">
    <div class="sidebar-user">
      <strong>DIOMANDE YAYA</strong>
      Chargé d'Étude<br>
      <span style="font-size:11px;line-height:1.4;display:block;margin-top:2px;">SERVICE DIGITALISATION, EXPLOITATION DES PLATEFORMES ET MAINTENANCE INFORMATIQUE</span>
    </div>
  </div>
</aside>

<main class="main">
  <div class="topbar">
    <div class="topbar-title" id="topbar-title">Tableau de bord</div>
    <div class="search-bar">
      <span>🔍</span>
      <input type="text" id="global-search" placeholder="Rechercher N° série, nom, projet..." oninput="onGlobalSearch(this.value)">
    </div>
    <button class="btn btn-primary" onclick="openAddModal()">＋ Ajouter</button>
  </div>

  <div class="content">

    <div id="page-dashboard" class="page active">
      <div class="stats-grid">
        <div class="stat-card blue">
          <div class="stat-label">Ordinateurs de bureau</div>
          <div class="stat-value" id="stat-ordi">—</div>
          <div class="stat-sub">Enregistrés dans la base</div>
        </div>
        <div class="stat-card green">
          <div class="stat-label">PC Portable</div>
          <div class="stat-value" id="stat-port">—</div>
          <div class="stat-sub">Distribués aux agents</div>
        </div>
        <div class="stat-card orange">
          <div class="stat-label">Imprimantes</div>
          <div class="stat-value" id="stat-impr">—</div>
          <div class="stat-sub">Parc imprimantes</div>
        </div>
        <div class="stat-card red">
          <div class="stat-label">Tablettes &amp; Autres</div>
          <div class="stat-value" id="stat-tab">—</div>
          <div class="stat-sub">Tablettes enregistrées</div>
        </div>
      </div>
      ```

Les modifications ont été appliquées aux lignes suivantes :
1.  **Ligne 178** : Le nom du menu latéral est passé de "PC Portables CLEF" à "**PC Portable**".
2.  **Ligne 215** : Le libellé de la carte statistique sur le tableau de bord est passé de "PC Portables CLEF" à "**PC Portable**".
