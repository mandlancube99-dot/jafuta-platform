[index.html](https://github.com/user-attachments/files/33495354/index.html)
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0">
<title>Jafuta Foundation Platform</title>
<style>
  :root {
    --primary: #1a6b3c;
    --primary-light: #27a85f;
    --primary-dark: #114a2a;
    --accent: #f0a500;
    --accent-light: #ffd166;
    --danger: #e63946;
    --bg: #f5f7f5;
    --card: #ffffff;
    --text: #1a1a1a;
    --muted: #6b7280;
    --border: #d1d5db;
    --shadow: 0 2px 8px rgba(0,0,0,0.10);
    --radius: 12px;
  }
  * { box-sizing: border-box; margin: 0; padding: 0; }
  body { font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif; background: var(--bg); color: var(--text); min-height: 100vh; }

  /* AUTH SCREENS */
  #auth-screen { display: flex; align-items: center; justify-content: center; min-height: 100vh; background: linear-gradient(135deg, var(--primary-dark) 0%, var(--primary) 60%, var(--primary-light) 100%); padding: 20px; }
  .auth-card { background: white; border-radius: 20px; padding: 36px 28px; width: 100%; max-width: 380px; box-shadow: 0 8px 32px rgba(0,0,0,0.18); }
  .auth-logo { text-align: center; margin-bottom: 24px; }
  .auth-logo .logo-circle { width: 72px; height: 72px; background: var(--primary); border-radius: 50%; display: inline-flex; align-items: center; justify-content: center; font-size: 32px; margin-bottom: 10px; }
  .auth-logo h1 { font-size: 20px; font-weight: 700; color: var(--primary); }
  .auth-logo p { font-size: 13px; color: var(--muted); margin-top: 2px; }
  .auth-tabs { display: flex; background: var(--bg); border-radius: 8px; padding: 3px; margin-bottom: 20px; }
  .auth-tab { flex: 1; text-align: center; padding: 8px; border-radius: 6px; font-size: 14px; font-weight: 500; cursor: pointer; transition: all 0.2s; color: var(--muted); }
  .auth-tab.active { background: white; color: var(--primary); box-shadow: var(--shadow); }
  .form-group { margin-bottom: 14px; }
  .form-group label { display: block; font-size: 13px; font-weight: 500; margin-bottom: 5px; color: var(--text); }
  .form-group input, .form-group select, .form-group textarea { width: 100%; padding: 10px 12px; border: 1.5px solid var(--border); border-radius: 8px; font-size: 14px; outline: none; transition: border 0.2s; }
  .form-group input:focus, .form-group select:focus, .form-group textarea:focus { border-color: var(--primary); }
  .btn { display: inline-flex; align-items: center; justify-content: center; gap: 6px; padding: 10px 18px; border: none; border-radius: 8px; font-size: 14px; font-weight: 600; cursor: pointer; transition: all 0.2s; text-decoration: none; }
  .btn-primary { background: var(--primary); color: white; }
  .btn-primary:hover { background: var(--primary-dark); }
  .btn-accent { background: var(--accent); color: white; }
  .btn-danger { background: var(--danger); color: white; }
  .btn-outline { background: transparent; border: 1.5px solid var(--border); color: var(--text); }
  .btn-sm { padding: 6px 12px; font-size: 12px; }
  .btn-full { width: 100%; }
  .auth-error { background: #fee2e2; color: #991b1b; padding: 10px 12px; border-radius: 8px; font-size: 13px; margin-bottom: 12px; }
  .auth-success { background: #d1fae5; color: #065f46; padding: 10px 12px; border-radius: 8px; font-size: 13px; margin-bottom: 12px; }

  /* MAIN APP */
  #app { display: none; }
  #loading-screen { display: flex; align-items: center; justify-content: center; min-height: 100vh; background: var(--primary); color: white; flex-direction: column; gap: 16px; }
  .spinner { width: 40px; height: 40px; border: 4px solid rgba(255,255,255,0.3); border-top-color: white; border-radius: 50%; animation: spin 0.8s linear infinite; }
  @keyframes spin { to { transform: rotate(360deg); } }

  /* TOP BAR */
  .topbar { background: var(--primary); color: white; display: flex; align-items: center; justify-content: space-between; padding: 12px 16px; position: sticky; top: 0; z-index: 100; }
  .topbar-left { display: flex; align-items: center; gap: 10px; }
  .topbar-logo { font-size: 18px; font-weight: 700; }
  .topbar-sub { font-size: 12px; opacity: 0.8; }
  .topbar-right { display: flex; align-items: center; gap: 8px; }
  .role-badge { background: rgba(255,255,255,0.2); padding: 3px 8px; border-radius: 20px; font-size: 11px; font-weight: 600; }
  .logout-btn { background: transparent; border: 1px solid rgba(255,255,255,0.4); color: white; padding: 4px 10px; border-radius: 6px; font-size: 12px; cursor: pointer; }

  /* HOME SCREEN */
  #home-screen { padding: 24px 16px; }
  .home-greeting { margin-bottom: 24px; }
  .home-greeting h2 { font-size: 22px; font-weight: 700; }
  .home-greeting p { color: var(--muted); font-size: 14px; margin-top: 4px; }
  .home-cards { display: grid; grid-template-columns: 1fr 1fr; gap: 16px; }
  .home-card { background: var(--card); border-radius: var(--radius); padding: 24px 16px; text-align: center; cursor: pointer; box-shadow: var(--shadow); border: 2px solid transparent; transition: all 0.2s; }
  .home-card:hover { border-color: var(--primary); transform: translateY(-2px); }
  .home-card .icon { font-size: 40px; margin-bottom: 10px; }
  .home-card h3 { font-size: 15px; font-weight: 700; color: var(--primary); }
  .home-card p { font-size: 12px; color: var(--muted); margin-top: 4px; }
  .home-stats { margin-top: 24px; background: var(--card); border-radius: var(--radius); padding: 16px; box-shadow: var(--shadow); }
  .home-stats h3 { font-size: 14px; font-weight: 600; margin-bottom: 12px; color: var(--muted); text-transform: uppercase; letter-spacing: 0.05em; }
  .stats-row { display: grid; grid-template-columns: repeat(3, 1fr); gap: 12px; }
  .stat-box { text-align: center; }
  .stat-box .num { font-size: 24px; font-weight: 700; color: var(--primary); }
  .stat-box .lbl { font-size: 11px; color: var(--muted); }

  /* SECTION LAYOUT */
  .section-header { background: var(--primary); color: white; padding: 12px 16px; display: flex; align-items: center; gap: 10px; }
  .section-header .back-btn { background: rgba(255,255,255,0.2); border: none; color: white; width: 32px; height: 32px; border-radius: 8px; cursor: pointer; font-size: 18px; display: flex; align-items: center; justify-content: center; }
  .section-header h2 { font-size: 17px; font-weight: 700; }
  .tab-nav { display: flex; overflow-x: auto; background: white; border-bottom: 1px solid var(--border); padding: 0 4px; gap: 0; scrollbar-width: none; }
  .tab-nav::-webkit-scrollbar { display: none; }
  .tab-btn { white-space: nowrap; padding: 12px 14px; border: none; background: transparent; cursor: pointer; font-size: 13px; font-weight: 500; color: var(--muted); border-bottom: 2px solid transparent; margin-bottom: -1px; }
  .tab-btn.active { color: var(--primary); border-bottom-color: var(--primary); }
  .tab-content { display: none; padding: 16px; }
  .tab-content.active { display: block; }

  /* CARDS, FORMS */
  .card { background: var(--card); border-radius: var(--radius); padding: 16px; box-shadow: var(--shadow); margin-bottom: 12px; }
  .card-title { font-size: 15px; font-weight: 600; margin-bottom: 12px; display: flex; align-items: center; justify-content: space-between; }
  .badge { display: inline-block; padding: 2px 8px; border-radius: 20px; font-size: 11px; font-weight: 600; }
  .badge-green { background: #d1fae5; color: #065f46; }
  .badge-blue { background: #dbeafe; color: #1e40af; }
  .badge-yellow { background: #fef3c7; color: #92400e; }
  .badge-red { background: #fee2e2; color: #991b1b; }
  table { width: 100%; border-collapse: collapse; font-size: 13px; }
  th { background: var(--bg); padding: 8px 10px; text-align: left; font-weight: 600; color: var(--muted); font-size: 12px; }
  td { padding: 8px 10px; border-bottom: 1px solid var(--border); }
  tr:last-child td { border-bottom: none; }
  .empty-state { text-align: center; padding: 40px 20px; color: var(--muted); }
  .empty-state .icon { font-size: 40px; margin-bottom: 8px; }
  .checkbox-group { display: grid; grid-template-columns: 1fr 1fr; gap: 6px; }
  .checkbox-item { display: flex; align-items: center; gap: 6px; font-size: 13px; cursor: pointer; }
  .checkbox-item input { width: 16px; height: 16px; accent-color: var(--primary); }
  .app-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 6px; }
  .app-item { display: flex; flex-direction: column; align-items: center; padding: 8px 4px; border: 1.5px solid var(--border); border-radius: 8px; cursor: pointer; font-size: 11px; text-align: center; transition: all 0.15s; }
  .app-item.selected { border-color: var(--primary); background: #f0fdf4; color: var(--primary); }
  .app-item input { display: none; }
  .photo-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 8px; }
  .photo-thumb { aspect-ratio: 1; object-fit: cover; border-radius: 8px; width: 100%; background: var(--bg); }
  .reminder-item { display: flex; align-items: flex-start; gap: 10px; padding: 10px 0; border-bottom: 1px solid var(--border); }
  .reminder-item:last-child { border-bottom: none; }
  .reminder-dot { width: 10px; height: 10px; border-radius: 50%; background: var(--accent); margin-top: 4px; flex-shrink: 0; }
  .zoom-chip { background: #EEF2FF; color: #4338ca; padding: 2px 8px; border-radius: 4px; font-size: 11px; font-weight: 600; }
  .section-divider { border: none; border-top: 1px solid var(--border); margin: 16px 0; }
  .reading-bar { height: 6px; border-radius: 3px; background: var(--border); overflow: hidden; margin-top: 4px; }
  .reading-fill { height: 100%; border-radius: 3px; background: var(--primary-light); }
  .viewer-notice { background: #fef3c7; border: 1px solid #fbbf24; padding: 10px 14px; border-radius: 8px; font-size: 13px; margin-bottom: 12px; color: #92400e; }

  /* MONTHLY REPORT */
  .report-section { background: var(--card); border-radius: var(--radius); padding: 16px; margin-bottom: 12px; box-shadow: var(--shadow); }
  .report-section h3 { font-size: 14px; font-weight: 700; color: var(--primary); margin-bottom: 12px; padding-bottom: 8px; border-bottom: 1px solid var(--border); display: flex; align-items: center; gap: 6px; }
  .report-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; }
  .report-field { }
  .report-field label { font-size: 12px; font-weight: 500; color: var(--muted); display: block; margin-bottom: 3px; }
  .report-field input, .report-field select, .report-field textarea { width: 100%; padding: 8px 10px; border: 1px solid var(--border); border-radius: 6px; font-size: 13px; }
  .report-field textarea { resize: vertical; min-height: 70px; }
  .report-field.full { grid-column: 1 / -1; }
  .health-table td input, .health-table td select { width: 100%; border: none; background: transparent; font-size: 12px; }
  .status-checks { display: flex; gap: 12px; flex-wrap: wrap; }
  .status-check { display: flex; align-items: center; gap: 5px; font-size: 13px; }

  /* TOAST */
  #toast { position: fixed; bottom: 24px; left: 50%; transform: translateX(-50%); background: #1a1a1a; color: white; padding: 10px 20px; border-radius: 8px; font-size: 14px; z-index: 9999; display: none; box-shadow: 0 4px 12px rgba(0,0,0,0.3); }

  /* COMMENT PANEL (viewer) */
  .comment-box { background: #f0fdf4; border: 1px solid #86efac; border-radius: 8px; padding: 12px; margin-top: 12px; }
  .comment-box h4 { font-size: 13px; font-weight: 600; margin-bottom: 8px; color: var(--primary); }
  .comment-item { font-size: 13px; padding: 6px 0; border-bottom: 1px solid #d1fae5; }
  .comment-item:last-child { border-bottom: none; }
  .comment-meta { font-size: 11px; color: var(--muted); margin-bottom: 2px; }

  @media (min-width: 600px) {
    .home-cards { grid-template-columns: repeat(2, 1fr); }
    .report-grid { grid-template-columns: repeat(3, 1fr); }
    .app-grid { grid-template-columns: repeat(5, 1fr); }
  }
  @media (max-width: 400px) {
    .home-cards { grid-template-columns: 1fr; }
    .checkbox-group { grid-template-columns: 1fr; }
  }
</style>
</head>
<body>

<!-- LOADING -->
<div id="loading-screen">
  <div class="spinner"></div>
  <p style="font-size:15px;opacity:0.8">Loading Jafuta Platform…</p>
</div>

<!-- AUTH -->
<div id="auth-screen" style="display:none">
  <div class="auth-card">
    <div class="auth-logo">
      <div class="logo-circle">🌿</div>
      <h1>Jafuta Foundation</h1>
      <p>Innovation & Literacy Platform</p>
    </div>
    <div class="auth-tabs">
      <div class="auth-tab active" onclick="switchAuthTab('login')">Sign In</div>
      <div class="auth-tab" onclick="switchAuthTab('register')">Register</div>
    </div>
    <div id="auth-error" class="auth-error" style="display:none"></div>
    <div id="auth-success" class="auth-success" style="display:none"></div>

    <!-- LOGIN -->
    <div id="login-form">
      <div class="form-group">
        <label>Email</label>
        <input type="email" id="login-email" placeholder="your@email.com" autocomplete="email">
      </div>
      <div class="form-group">
        <label>Password</label>
        <input type="password" id="login-pass" placeholder="Password" autocomplete="current-password">
      </div>
      <button class="btn btn-primary btn-full" onclick="doLogin()">Sign In</button>
    </div>

    <!-- REGISTER -->
    <div id="register-form" style="display:none">
      <div class="form-group">
        <label>Full Name</label>
        <input type="text" id="reg-name" placeholder="Mandla Ncube">
      </div>
      <div class="form-group">
        <label>Email</label>
        <input type="email" id="reg-email" placeholder="your@email.com" autocomplete="email">
      </div>
      <div class="form-group">
        <label>Password</label>
        <input type="password" id="reg-pass" placeholder="Min 6 characters">
      </div>
      <div class="form-group">
        <label>Role</label>
        <select id="reg-role">
          <option value="viewer">Viewer (read-only)</option>
          <option value="admin">Admin (full access)</option>
        </select>
      </div>
      <button class="btn btn-primary btn-full" onclick="doRegister()">Create Account</button>
    </div>
  </div>
</div>

<!-- MAIN APP -->
<div id="app">
  <!-- TOPBAR -->
  <div class="topbar">
    <div class="topbar-left">
      <span style="font-size:22px">🌿</span>
      <div>
        <div class="topbar-logo">Jafuta Foundation</div>
        <div class="topbar-sub" id="topbar-sub">Innovation Platform</div>
      </div>
    </div>
    <div class="topbar-right">
      <span class="role-badge" id="role-badge">admin</span>
      <button class="logout-btn" onclick="doLogout()">Logout</button>
    </div>
  </div>

  <!-- HOME -->
  <div id="home-screen">
    <div style="padding:16px">
      <div class="home-greeting">
        <h2 id="home-greeting-text">Good morning 👋</h2>
        <p id="home-date-text"></p>
      </div>
      <div class="home-cards">
        <div class="home-card" onclick="openModule('hub')">
          <div class="icon">🏢</div>
          <h3>Innovation Hub</h3>
          <p>Check-ins, lesson plans &amp; dashboard</p>
        </div>
        <div class="home-card" onclick="openModule('lit')">
          <div class="icon">📚</div>
          <h3>English Literacy</h3>
          <p>Students, sessions &amp; reports</p>
        </div>
      </div>
      <div class="home-stats" id="home-stats">
        <h3>Today at a Glance</h3>
        <div class="stats-row">
          <div class="stat-box"><div class="num" id="stat-checkins">—</div><div class="lbl">Check-ins today</div></div>
          <div class="stat-box"><div class="num" id="stat-students">—</div><div class="lbl">Lit. students</div></div>
          <div class="stat-box"><div class="num" id="stat-sessions">—</div><div class="lbl">Sessions this month</div></div>
        </div>
      </div>
    </div>
  </div>

  <!-- HUB MODULE -->
  <div id="hub-module" style="display:none">
    <div class="section-header">
      <button class="back-btn" onclick="goHome()">←</button>
      <h2>🏢 Innovation Hub</h2>
    </div>
    <div class="tab-nav" id="hub-tabs"></div>
    <div id="hub-tab-contents"></div>
  </div>

  <!-- LIT MODULE -->
  <div id="lit-module" style="display:none">
    <div class="section-header">
      <button class="back-btn" onclick="goHome()">←</button>
      <h2>📚 English Literacy</h2>
    </div>
    <div class="tab-nav" id="lit-tabs"></div>
    <div id="lit-tab-contents"></div>
  </div>
</div>

<div id="toast"></div>

<script type="module">
// ══════════════════════════════════════════════
//  FIREBASE SETUP
// ══════════════════════════════════════════════
import { initializeApp } from "https://www.gstatic.com/firebasejs/10.12.0/firebase-app.js";
import { getAuth, createUserWithEmailAndPassword, signInWithEmailAndPassword, signOut, onAuthStateChanged } from "https://www.gstatic.com/firebasejs/10.12.0/firebase-auth.js";
import { getFirestore, collection, doc, setDoc, getDoc, getDocs, addDoc, query, where, orderBy, onSnapshot, serverTimestamp, deleteDoc, updateDoc } from "https://www.gstatic.com/firebasejs/10.12.0/firebase-firestore.js";

const firebaseConfig = {
  apiKey: "AIzaSyCht9ZYR53YUrvKmYj_j8QriXwQiUU0OVI",
  authDomain: "jafuta-foundation.firebaseapp.com",
  projectId: "jafuta-foundation",
  storageBucket: "jafuta-foundation.firebasestorage.app",
  messagingSenderId: "437029431715",
  appId: "1:437029431715:web:17ecfdf619328466b25216"
};

const firebaseApp = initializeApp(firebaseConfig);
const auth = getAuth(firebaseApp);
const db = getFirestore(firebaseApp);

// ══════════════════════════════════════════════
//  STATE
// ══════════════════════════════════════════════
let currentUser = null;
let currentRole = 'viewer';
let currentModule = null;
let currentTab = {};

// ══════════════════════════════════════════════
//  UTILITIES
// ══════════════════════════════════════════════
window.toast = function(msg, dur=2500) {
  const t = document.getElementById('toast');
  t.textContent = msg;
  t.style.display = 'block';
  setTimeout(() => t.style.display = 'none', dur);
};

function show(id) { document.getElementById(id).style.display = 'block'; }
function hide(id) { document.getElementById(id).style.display = 'none'; }
function el(id) { return document.getElementById(id); }

function todayStr() {
  return new Date().toISOString().split('T')[0];
}
function monthStr() {
  const d = new Date();
  return `${d.getFullYear()}-${String(d.getMonth()+1).padStart(2,'0')}`;
}
function fmtDate(ts) {
  if (!ts) return '';
  const d = ts.toDate ? ts.toDate() : new Date(ts);
  return d.toLocaleDateString('en-ZW', { day:'2-digit', month:'short', year:'numeric' });
}
function fmtTime(ts) {
  if (!ts) return '';
  const d = ts.toDate ? ts.toDate() : new Date(ts);
  return d.toLocaleTimeString('en-ZW', { hour:'2-digit', minute:'2-digit' });
}

function exportCSV(headers, rows, filename) {
  const csvContent = [headers, ...rows].map(r => r.map(c => `"${(c||'').toString().replace(/"/g,'""')}"`).join(',')).join('\n');
  const blob = new Blob([csvContent], { type: 'text/csv' });
  const url = URL.createObjectURL(blob);
  const a = document.createElement('a'); a.href = url; a.download = filename; a.click();
  URL.revokeObjectURL(url);
}

// ══════════════════════════════════════════════
//  AUTH
// ══════════════════════════════════════════════
window.switchAuthTab = function(tab) {
  document.querySelectorAll('.auth-tab').forEach((t,i) => t.classList.toggle('active', (i===0&&tab==='login')||(i===1&&tab==='register')));
  el('login-form').style.display = tab==='login' ? 'block' : 'none';
  el('register-form').style.display = tab==='register' ? 'block' : 'none';
  el('auth-error').style.display='none'; el('auth-success').style.display='none';
};

window.doLogin = async function() {
  const email = el('login-email').value.trim();
  const pass = el('login-pass').value;
  el('auth-error').style.display='none';
  try {
    await signInWithEmailAndPassword(auth, email, pass);
  } catch(e) {
    el('auth-error').textContent = e.message;
    el('auth-error').style.display='block';
  }
};

window.doRegister = async function() {
  const name = el('reg-name').value.trim();
  const email = el('reg-email').value.trim();
  const pass = el('reg-pass').value;
  const role = el('reg-role').value;
  el('auth-error').style.display='none';
  if (!name) { el('auth-error').textContent='Please enter your name'; el('auth-error').style.display='block'; return; }
  try {
    const cred = await createUserWithEmailAndPassword(auth, email, pass);
    await setDoc(doc(db, 'users', cred.user.uid), { name, email, role, createdAt: serverTimestamp() });
    el('auth-success').textContent = 'Account created! Signing you in…';
    el('auth-success').style.display = 'block';
  } catch(e) {
    el('auth-error').textContent = e.message;
    el('auth-error').style.display='block';
  }
};

window.doLogout = async function() {
  await signOut(auth);
};

// ══════════════════════════════════════════════
//  AUTH STATE OBSERVER
// ══════════════════════════════════════════════
onAuthStateChanged(auth, async (user) => {
  hide('loading-screen');
  if (user) {
    currentUser = user;
    // load role from Firestore
    const snap = await getDoc(doc(db, 'users', user.uid));
    currentRole = snap.exists() ? (snap.data().role || 'viewer') : 'viewer';
    const name = snap.exists() ? snap.data().name : user.email;
    el('role-badge').textContent = currentRole;
    // greeting
    const hr = new Date().getHours();
    const greet = hr < 12 ? 'Good morning' : hr < 17 ? 'Good afternoon' : 'Good evening';
    el('home-greeting-text').textContent = `${greet}, ${name.split(' ')[0]} 👋`;
    el('home-date-text').textContent = new Date().toLocaleDateString('en-ZW', { weekday:'long', day:'numeric', month:'long', year:'numeric' });
    el('topbar-sub').textContent = `Logged in as ${name}`;
    hide('auth-screen');
    show('app');
    loadHomeStats();
    buildHubModule();
    buildLitModule();
  } else {
    currentUser = null;
    hide('app');
    show('auth-screen');
    hide('loading-screen');
  }
});

// ══════════════════════════════════════════════
//  HOME STATS
// ══════════════════════════════════════════════
async function loadHomeStats() {
  // check-ins today
  const today = todayStr();
  const ciSnap = await getDocs(query(collection(db,'checkins'), where('date','==',today)));
  el('stat-checkins').textContent = ciSnap.size;
  // lit students
  const stSnap = await getDocs(collection(db,'students'));
  el('stat-students').textContent = stSnap.size;
  // sessions this month
  const mo = monthStr();
  const seSnap = await getDocs(query(collection(db,'sessions'), where('month','==',mo)));
  el('stat-sessions').textContent = seSnap.size;
}

// ══════════════════════════════════════════════
//  NAVIGATION
// ══════════════════════════════════════════════
window.openModule = function(mod) {
  hide('home-screen');
  if (mod==='hub') { show('hub-module'); currentModule='hub'; }
  else { show('lit-module'); currentModule='lit'; }
};

window.goHome = function() {
  hide('hub-module'); hide('lit-module');
  show('home-screen');
  currentModule=null;
  loadHomeStats();
};

function activateTab(mod, tabId) {
  currentTab[mod] = tabId;
  document.querySelectorAll(`#${mod}-tabs .tab-btn`).forEach(b => b.classList.toggle('active', b.dataset.tab===tabId));
  document.querySelectorAll(`#${mod}-tab-contents .tab-content`).forEach(c => c.classList.toggle('active', c.id===tabId));
}

// ══════════════════════════════════════════════
//  HUB MODULE
// ══════════════════════════════════════════════
const HUB_TABS = [
  {id:'hub-checkin',    label:'✅ Check-In'},
  {id:'hub-lessonplan', label:'📋 Lesson Plan'},
  {id:'hub-reminders',  label:'🔔 Reminders'},
  {id:'hub-dashboard',  label:'📊 Dashboard'},
];
const IPAD_APPS = ['GarageBand','iMovie','Keynote','Duolingo','Docs','Books','Freeform','ABCya! Games','BoldVoice','ClassDojo','Clips','Code Teens','Codie Blocks','Coding Awbie','Coding Safari','CrossRoad','Detective','DinoCoding','Doceri','Khan Academy','Khan Kids','Kids A-Z','LittleLit','Matchimals','Math Champ','Monster','Newton','Numbers','Numbers Classic','Pages','Pizza Co','Playground','Swift Playgrounds','Puppet Edu','SAM Root','Science Zone','ScratchJr','Sheets','ShowMe','SisandaApp','Sketchbook','SketchesSchool','Slides','Sphero Edu','Stage','Tangram Classic','Tynker','Tynker Jr','Words Classic','World Geography'];

function buildHubModule() {
  // tabs
  const tabNav = el('hub-tabs');
  tabNav.innerHTML = HUB_TABS.map(t=>`<button class="tab-btn" data-tab="${t.id}" onclick="activateTabGlobal('hub','${t.id}')">${t.label}</button>`).join('');
  // contents
  const tabContents = el('hub-tab-contents');
  tabContents.innerHTML = `
    ${hubCheckinHTML()}
    ${hubLessonPlanHTML()}
    ${hubRemindersHTML()}
    ${hubDashboardHTML()}
  `;
  activateTab('hub','hub-checkin');
  loadCheckinList();
  loadReminders();
  loadHubDashboard();
}
window.activateTabGlobal = function(mod, tabId) { activateTab(mod, tabId); };

function hubCheckinHTML() {
  const isAdmin = currentRole==='admin';
  return `<div class="tab-content" id="hub-checkin">
    ${!isAdmin ? '<div class="viewer-notice">👁 Viewer mode — you can view check-ins but cannot add or delete.</div>' : ''}
    ${isAdmin ? `<div class="card">
      <div class="card-title">New Check-In</div>
      <div class="form-group"><label>Full Name *</label><input type="text" id="ci-name" placeholder="Visitor name"></div>
      <div class="form-group"><label>Age Group</label>
        <select id="ci-age">
          <option>Under 12</option><option>12–17</option><option>18–25</option><option>26–35</option><option>36–50</option><option>50+</option>
        </select>
      </div>
      <div class="form-group"><label>Phone Number</label><input type="tel" id="ci-phone" placeholder="07X XXX XXXX"></div>
      <div class="form-group"><label>Service Used</label>
        <select id="ci-service">
          <option>iPad Learning</option><option>Computer Access</option><option>Coding Session</option><option>Robotics</option><option>Career Guidance</option><option>AI Workshop</option><option>Literacy Class</option><option>Community Meeting</option><option>Other</option>
        </select>
      </div>
      <div class="form-group"><label>Grade / Class</label>
        <select id="ci-grade">
          <option>Primary</option><option>Secondary</option><option>MCRI Potential Candidates</option><option>Community Member</option><option>Teacher</option>
        </select>
      </div>
      <button class="btn btn-primary btn-full" onclick="saveCheckin()">✅ Check In</button>
    </div>` : ''}
    <div class="card">
      <div class="card-title">Today's Check-Ins <span id="ci-count-badge" class="badge badge-green">0</span></div>
      <div id="ci-list"><div class="empty-state"><div class="icon">📋</div><p>No check-ins today</p></div></div>
      ${isAdmin ? `<button class="btn btn-outline btn-sm" style="margin-top:8px" onclick="exportCheckins()">⬇ Export CSV</button>` : ''}
    </div>
  </div>`;
}

window.saveCheckin = async function() {
  const name = el('ci-name').value.trim();
  if (!name) { toast('Please enter a name'); return; }
  await addDoc(collection(db,'checkins'), {
    name, age: el('ci-age').value, phone: el('ci-phone').value,
    service: el('ci-service').value, grade: el('ci-grade').value,
    date: todayStr(), month: monthStr(), createdAt: serverTimestamp(), createdBy: currentUser.uid
  });
  el('ci-name').value=''; el('ci-phone').value='';
  toast('✅ Checked in!');
  loadCheckinList();
};

async function loadCheckinList() {
  const snap = await getDocs(query(collection(db,'checkins'), where('date','==',todayStr())));
  const list = el('ci-list');
  if (!list) return;
  el('ci-count-badge').textContent = snap.size;
  if (snap.empty) { list.innerHTML='<div class="empty-state"><div class="icon">📋</div><p>No check-ins today</p></div>'; return; }
  const rows = [];
  snap.forEach(d => rows.push({id:d.id, ...d.data()}));
  rows.sort((a,b) => (a.createdAt?.seconds||0) - (b.createdAt?.seconds||0));
  list.innerHTML = `<table><thead><tr><th>#</th><th>Name</th><th>Grade</th><th>Service</th>${currentRole==='admin'?'<th></th>':''}</tr></thead><tbody>
    ${rows.map((r,i)=>`<tr><td>${i+1}</td><td><b>${r.name}</b><br><span style="font-size:11px;color:var(--muted)">${r.age||''} · ${r.phone||''}</span></td><td>${r.grade||''}</td><td>${r.service||''}</td>${currentRole==='admin'?`<td><button class="btn btn-danger btn-sm" onclick="deleteDoc_('checkins','${r.id}',loadCheckinList)">🗑</button></td>`:''}</tr>`).join('')}
  </tbody></table>`;
}

window.exportCheckins = async function() {
  const snap = await getDocs(query(collection(db,'checkins'), orderBy('createdAt','desc')));
  const rows = []; snap.forEach(d => rows.push(d.data()));
  exportCSV(['Date','Name','Age','Phone','Service','Grade'], rows.map(r=>[r.date,r.name,r.age,r.phone,r.service,r.grade]), `checkins-${todayStr()}.csv`);
};

function hubLessonPlanHTML() {
  const isAdmin = currentRole==='admin';
  const appCheckboxes = IPAD_APPS.map(a=>`<label class="app-item" onclick="toggleApp(this,'${a.replace(/'/g,"\\'")}')"><input type="checkbox" value="${a}">📱<span>${a}</span></label>`).join('');
  return `<div class="tab-content" id="hub-lessonplan">
    ${!isAdmin ? '<div class="viewer-notice">👁 Viewer mode.</div>' : ''}
    ${isAdmin ? `<div class="card">
      <div class="card-title">New Lesson Plan</div>
      <div class="form-group"><label>Date</label><input type="date" id="lp-date" value="${todayStr()}"></div>
      <div class="form-group"><label>Class</label>
        <select id="lp-class"><option>Primary</option><option>Secondary</option><option>MCRI Potential Candidates</option><option>Community</option></select>
      </div>
      <div class="form-group"><label>Topic</label><input type="text" id="lp-topic" placeholder="e.g. Introduction to Coding"></div>
      <div class="form-group"><label>Activities</label><textarea id="lp-activities" placeholder="Describe session activities…" rows="2"></textarea></div>
      <div class="form-group"><label>Essential Questions</label><textarea id="lp-eq" placeholder="What questions will guide the session?" rows="2"></textarea></div>
      <div class="form-group"><label>Resources / iPad Apps Used</label>
        <div class="app-grid" id="app-select-grid">${appCheckboxes}</div>
      </div>
      <div class="form-group"><label>Notes</label><textarea id="lp-notes" placeholder="Additional notes…" rows="2"></textarea></div>
      <button class="btn btn-primary btn-full" onclick="saveLessonPlan()">💾 Save Lesson Plan</button>
    </div>` : ''}
    <div class="card">
      <div class="card-title">Recent Lesson Plans</div>
      <div id="lp-list"><div class="empty-state"><div class="icon">📋</div><p>No lesson plans yet</p></div></div>
      ${isAdmin ? `<button class="btn btn-outline btn-sm" style="margin-top:8px" onclick="exportLessonPlans()">⬇ Export CSV</button>` : ''}
    </div>
  </div>`;
}

window.toggleApp = function(el, appName) {
  el.classList.toggle('selected');
};

window.saveLessonPlan = async function() {
  const topic = el('lp-topic').value.trim();
  if (!topic) { toast('Please enter a topic'); return; }
  const selectedApps = Array.from(document.querySelectorAll('#app-select-grid .app-item.selected')).map(a=>a.querySelector('span').textContent);
  await addDoc(collection(db,'lessonplans'), {
    date: el('lp-date').value, class: el('lp-class').value, topic,
    activities: el('lp-activities').value, essentialQuestions: el('lp-eq').value,
    apps: selectedApps, notes: el('lp-notes').value,
    month: monthStr(), createdAt: serverTimestamp(), createdBy: currentUser.uid
  });
  // reset
  el('lp-topic').value=''; el('lp-activities').value=''; el('lp-eq').value=''; el('lp-notes').value='';
  document.querySelectorAll('#app-select-grid .app-item.selected').forEach(a=>a.classList.remove('selected'));
  toast('✅ Lesson plan saved!');
  loadLessonPlans();
};

async function loadLessonPlans() {
  const snap = await getDocs(query(collection(db,'lessonplans'), orderBy('createdAt','desc')));
  const list = el('lp-list');
  if (!list) return;
  if (snap.empty) { list.innerHTML='<div class="empty-state"><div class="icon">📋</div><p>No lesson plans yet</p></div>'; return; }
  const rows=[];
  snap.forEach(d=>rows.push({id:d.id,...d.data()}));
  list.innerHTML = rows.slice(0,20).map(r=>`<div class="card" style="margin-bottom:8px;padding:12px">
    <div style="display:flex;justify-content:space-between;align-items:flex-start">
      <div><b>${r.topic}</b><br><span style="font-size:12px;color:var(--muted)">${r.date} · ${r.class}</span></div>
      ${currentRole==='admin'?`<button class="btn btn-danger btn-sm" onclick="deleteDoc_('lessonplans','${r.id}',loadLessonPlans)">🗑</button>`:''}
    </div>
    ${r.activities?`<p style="font-size:12px;margin-top:6px;color:var(--muted)">${r.activities}</p>`:''}
    ${r.apps&&r.apps.length?`<p style="font-size:11px;margin-top:4px;color:var(--primary)">Apps: ${r.apps.join(', ')}</p>`:''}
  </div>`).join('');
}

window.exportLessonPlans = async function() {
  const snap = await getDocs(query(collection(db,'lessonplans'), orderBy('createdAt','desc')));
  const rows=[]; snap.forEach(d=>rows.push(d.data()));
  exportCSV(['Date','Class','Topic','Activities','Essential Questions','Apps','Notes'], rows.map(r=>[r.date,r.class,r.topic,r.activities,r.essentialQuestions,(r.apps||[]).join('; '),r.notes]), `lesson-plans-${monthStr()}.csv`);
};

function hubRemindersHTML() {
  const isAdmin = currentRole==='admin';
  return `<div class="tab-content" id="hub-reminders">
    ${isAdmin ? `<div class="card">
      <div class="card-title">Add Reminder / Zoom</div>
      <div class="form-group"><label>Title *</label><input type="text" id="rem-title" placeholder="e.g. Staff meeting, Parent visit"></div>
      <div class="form-group"><label>Date & Time</label><input type="datetime-local" id="rem-dt"></div>
      <div class="form-group"><label>Description</label><textarea id="rem-desc" rows="2" placeholder="Details…"></textarea></div>
      <div class="form-group"><label>Zoom Link (optional)</label><input type="url" id="rem-zoom" placeholder="https://zoom.us/j/…"></div>
      <button class="btn btn-primary btn-full" onclick="saveReminder()">🔔 Add Reminder</button>
    </div>` : ''}
    <div class="card">
      <div class="card-title">Upcoming Reminders</div>
      <div id="rem-list"><div class="empty-state"><div class="icon">🔔</div><p>No reminders yet</p></div></div>
    </div>
  </div>`;
}

window.saveReminder = async function() {
  const title = el('rem-title').value.trim();
  if (!title) { toast('Please enter a title'); return; }
  await addDoc(collection(db,'reminders'), {
    title, datetime: el('rem-dt').value, description: el('rem-desc').value,
    zoom: el('rem-zoom').value, createdAt: serverTimestamp(), createdBy: currentUser.uid
  });
  el('rem-title').value=''; el('rem-dt').value=''; el('rem-desc').value=''; el('rem-zoom').value='';
  toast('🔔 Reminder added!');
  loadReminders();
};

async function loadReminders() {
  const snap = await getDocs(query(collection(db,'reminders'), orderBy('createdAt','desc')));
  const list = el('rem-list');
  if (!list) return;
  if (snap.empty) { list.innerHTML='<div class="empty-state"><div class="icon">🔔</div><p>No reminders yet</p></div>'; return; }
  const rows=[]; snap.forEach(d=>rows.push({id:d.id,...d.data()}));
  list.innerHTML = rows.slice(0,20).map(r=>`<div class="reminder-item">
    <div class="reminder-dot"></div>
    <div style="flex:1">
      <div style="font-weight:600;font-size:14px">${r.title}</div>
      ${r.datetime?`<div style="font-size:12px;color:var(--muted)">${new Date(r.datetime).toLocaleString('en-ZW',{weekday:'short',day:'2-digit',month:'short',hour:'2-digit',minute:'2-digit'})}</div>`:''}
      ${r.description?`<div style="font-size:12px;margin-top:2px">${r.description}</div>`:''}
      ${r.zoom?`<a href="${r.zoom}" target="_blank" class="zoom-chip" style="margin-top:4px;display:inline-block;text-decoration:none">🎥 Join Zoom</a>`:''}
    </div>
    ${currentRole==='admin'?`<button class="btn btn-danger btn-sm" onclick="deleteDoc_('reminders','${r.id}',loadReminders)">🗑</button>`:''}
  </div>`).join('');
}

function hubDashboardHTML() {
  return `<div class="tab-content" id="hub-dashboard">
    <div class="card">
      <div class="card-title">Hub Statistics</div>
      <div id="hub-dash-content"><div class="empty-state"><div class="icon">📊</div><p>Loading…</p></div></div>
      <button class="btn btn-outline btn-sm" style="margin-top:8px" onclick="loadHubDashboard()">🔄 Refresh</button>
    </div>
    <div class="card">
      <div class="card-title">Check-Ins This Month</div>
      <div id="hub-month-checkins"></div>
      ${currentRole==='admin'?`<button class="btn btn-outline btn-sm" style="margin-top:8px" onclick="exportCheckins()">⬇ Export All Check-ins CSV</button>`:''}
    </div>
  </div>`;
}

async function loadHubDashboard() {
  const dashEl = el('hub-dash-content');
  if (!dashEl) return;
  const mo = monthStr();
  const ciSnap = await getDocs(query(collection(db,'checkins'), where('month','==',mo)));
  const lpSnap = await getDocs(query(collection(db,'lessonplans'), where('month','==',mo)));
  const gradeCounts = {};
  const serviceCounts = {};
  ciSnap.forEach(d=>{
    const data=d.data();
    gradeCounts[data.grade]=(gradeCounts[data.grade]||0)+1;
    serviceCounts[data.service]=(serviceCounts[data.service]||0)+1;
  });
  dashEl.innerHTML = `
    <div class="stats-row" style="margin-bottom:16px">
      <div class="stat-box"><div class="num">${ciSnap.size}</div><div class="lbl">Check-ins this month</div></div>
      <div class="stat-box"><div class="num">${lpSnap.size}</div><div class="lbl">Lesson plans</div></div>
      <div class="stat-box"><div class="num">${[...new Set([...ciSnap.docs.map(d=>d.data().date)])].length}</div><div class="lbl">Active days</div></div>
    </div>
    <div style="margin-bottom:12px"><b style="font-size:13px">By Grade</b>${Object.entries(gradeCounts).map(([k,v])=>`<div style="display:flex;justify-content:space-between;font-size:13px;padding:3px 0"><span>${k}</span><b>${v}</b></div>`).join('') || '<p style="font-size:12px;color:var(--muted)">No data</p>'}</div>
    <div><b style="font-size:13px">By Service</b>${Object.entries(serviceCounts).map(([k,v])=>`<div style="display:flex;justify-content:space-between;font-size:13px;padding:3px 0"><span>${k}</span><b>${v}</b></div>`).join('') || '<p style="font-size:12px;color:var(--muted)">No data</p>'}</div>
  `;
  // month check-ins list
  const monthListEl = el('hub-month-checkins');
  if (!monthListEl) return;
  if (ciSnap.empty) { monthListEl.innerHTML='<div class="empty-state"><div class="icon">📋</div><p>No check-ins this month</p></div>'; return; }
  const rows=[]; ciSnap.forEach(d=>rows.push(d.data()));
  rows.sort((a,b)=>b.date.localeCompare(a.date));
  monthListEl.innerHTML=`<table><thead><tr><th>Date</th><th>Name</th><th>Grade</th><th>Service</th></tr></thead><tbody>${rows.slice(0,30).map(r=>`<tr><td>${r.date}</td><td>${r.name}</td><td>${r.grade||''}</td><td>${r.service||''}</td></tr>`).join('')}</tbody></table>`;
}

// ══════════════════════════════════════════════
//  LIT MODULE
// ══════════════════════════════════════════════
const LIT_TABS = [
  {id:'lit-register', label:'📋 Register'},
  {id:'lit-students', label:'👧 Students'},
  {id:'lit-enrol',    label:'➕ Enrol'},
  {id:'lit-photos',   label:'📸 Photos'},
  {id:'lit-reports',  label:'📊 Reports'},
  {id:'lit-monthly',  label:'📄 Monthly Report'},
];

function buildLitModule() {
  const tabNav = el('lit-tabs');
  tabNav.innerHTML = LIT_TABS.map(t=>`<button class="tab-btn" data-tab="${t.id}" onclick="activateTabGlobal('lit','${t.id}');loadLitTab('${t.id}')">${t.label}</button>`).join('');
  const tabContents = el('lit-tab-contents');
  tabContents.innerHTML = `
    ${litRegisterHTML()}
    ${litStudentsHTML()}
    ${litEnrolHTML()}
    ${litPhotosHTML()}
    ${litReportsHTML()}
    ${litMonthlyHTML()}
  `;
  activateTab('lit','lit-register');
  loadLitTab('lit-register');
}

window.loadLitTab = function(tabId) {
  if (tabId==='lit-register') loadSessions();
  else if (tabId==='lit-students') loadStudents();
  else if (tabId==='lit-photos') loadPhotos();
  else if (tabId==='lit-reports') loadLitReports();
};

function litRegisterHTML() {
  const isAdmin = currentRole==='admin';
  return `<div class="tab-content" id="lit-register">
    ${!isAdmin ? '<div class="viewer-notice">👁 Viewer mode.</div>' : ''}
    ${isAdmin ? `<div class="card">
      <div class="card-title">Log Session</div>
      <div class="form-group"><label>Date</label><input type="date" id="sess-date" value="${todayStr()}"></div>
      <div class="form-group"><label>Class</label>
        <select id="sess-class"><option>Primary</option><option>Secondary</option><option>MCRI Potential Candidates</option></select>
      </div>
      <div class="form-group"><label>Topic / Activity</label><input type="text" id="sess-topic" placeholder="e.g. Phonics, Reading comprehension"></div>
      <div class="form-group"><label>Number of Learners</label><input type="number" id="sess-learners" min="0" placeholder="0"></div>
      <div class="form-group"><label>Duration (minutes)</label><input type="number" id="sess-duration" min="0" placeholder="60"></div>
      <div class="form-group"><label>Notes</label><textarea id="sess-notes" rows="2" placeholder="Session notes…"></textarea></div>
      <button class="btn btn-primary btn-full" onclick="saveSession()">📋 Log Session</button>
    </div>` : ''}
    <div class="card">
      <div class="card-title">Recent Sessions</div>
      <div id="sess-list"><div class="empty-state"><div class="icon">📋</div><p>No sessions logged</p></div></div>
      ${isAdmin?`<button class="btn btn-outline btn-sm" style="margin-top:8px" onclick="exportSessions()">⬇ Export CSV</button>`:''}
    </div>
  </div>`;
}

window.saveSession = async function() {
  const topic = el('sess-topic').value.trim();
  if (!topic) { toast('Please enter a topic'); return; }
  await addDoc(collection(db,'sessions'), {
    date: el('sess-date').value, class: el('sess-class').value, topic,
    learners: parseInt(el('sess-learners').value)||0, duration: parseInt(el('sess-duration').value)||0,
    notes: el('sess-notes').value, month: monthStr(), createdAt: serverTimestamp(), createdBy: currentUser.uid
  });
  el('sess-topic').value=''; el('sess-learners').value=''; el('sess-duration').value=''; el('sess-notes').value='';
  toast('✅ Session logged!');
  loadSessions();
};

async function loadSessions() {
  const snap = await getDocs(query(collection(db,'sessions'), orderBy('createdAt','desc')));
  const list = el('sess-list');
  if (!list) return;
  if (snap.empty) { list.innerHTML='<div class="empty-state"><div class="icon">📋</div><p>No sessions logged</p></div>'; return; }
  const rows=[]; snap.forEach(d=>rows.push({id:d.id,...d.data()}));
  list.innerHTML=`<table><thead><tr><th>Date</th><th>Class</th><th>Topic</th><th>Learners</th>${currentRole==='admin'?'<th></th>':''}</tr></thead><tbody>${rows.slice(0,30).map(r=>`<tr><td>${r.date}</td><td>${r.class}</td><td>${r.topic}</td><td>${r.learners||0}</td>${currentRole==='admin'?`<td><button class="btn btn-danger btn-sm" onclick="deleteDoc_('sessions','${r.id}',loadSessions)">🗑</button></td>`:''}</tr>`).join('')}</tbody></table>`;
}

window.exportSessions = async function() {
  const snap = await getDocs(query(collection(db,'sessions'), orderBy('createdAt','desc')));
  const rows=[]; snap.forEach(d=>rows.push(d.data()));
  exportCSV(['Date','Class','Topic','Learners','Duration (min)','Notes'], rows.map(r=>[r.date,r.class,r.topic,r.learners,r.duration,r.notes]), `sessions-${monthStr()}.csv`);
};

function litStudentsHTML() {
  return `<div class="tab-content" id="lit-students">
    <div class="card">
      <div class="card-title">Student Progress</div>
      <div id="student-list"><div class="empty-state"><div class="icon">👧</div><p>No students enrolled</p></div></div>
      ${currentRole==='admin'?`<button class="btn btn-outline btn-sm" style="margin-top:8px" onclick="exportStudents()">⬇ Export CSV</button>`:''}
    </div>
  </div>`;
}

async function loadStudents() {
  const snap = await getDocs(query(collection(db,'students'), orderBy('name')));
  const list = el('student-list');
  if (!list) return;
  if (snap.empty) { list.innerHTML='<div class="empty-state"><div class="icon">👧</div><p>No students enrolled yet. Use the Enrol tab to add students.</p></div>'; return; }
  const rows=[]; snap.forEach(d=>rows.push({id:d.id,...d.data()}));
  const readingColors = {'Pre-Reader':'badge-red','Early Reader':'badge-yellow','Fluent':'badge-green'};
  list.innerHTML=rows.map(r=>`<div class="card" style="margin-bottom:8px;padding:12px">
    <div style="display:flex;justify-content:space-between;align-items:center">
      <div>
        <b style="font-size:14px">${r.name}</b>
        <div style="font-size:12px;color:var(--muted)">${r.class||''} · Enrolled ${r.enrollDate||''}</div>
      </div>
      <span class="badge ${readingColors[r.readingLevel]||'badge-blue'}">${r.readingLevel||'Unknown'}</span>
    </div>
    ${currentRole==='admin'?`<div style="display:flex;gap:6px;margin-top:8px">
      <select onchange="updateReadingLevel('${r.id}',this.value)" style="font-size:12px;padding:4px 6px;border:1px solid var(--border);border-radius:6px">
        <option value="">Update level…</option>
        <option value="Pre-Reader">Pre-Reader</option>
        <option value="Early Reader">Early Reader</option>
        <option value="Fluent">Fluent</option>
      </select>
      <button class="btn btn-danger btn-sm" onclick="deleteDoc_('students','${r.id}',loadStudents)">🗑</button>
    </div>`:''}
  </div>`).join('');
}

window.updateReadingLevel = async function(id, level) {
  if (!level) return;
  await updateDoc(doc(db,'students',id), { readingLevel: level });
  toast(`Reading level updated to ${level}`);
  loadStudents();
};

window.exportStudents = async function() {
  const snap = await getDocs(query(collection(db,'students'), orderBy('name')));
  const rows=[]; snap.forEach(d=>rows.push(d.data()));
  exportCSV(['Name','Class','Age','Enrol Date','Reading Level','Notes'], rows.map(r=>[r.name,r.class,r.age,r.enrollDate,r.readingLevel,r.notes]), `students-${monthStr()}.csv`);
};

function litEnrolHTML() {
  const isAdmin = currentRole==='admin';
  return `<div class="tab-content" id="lit-enrol">
    ${!isAdmin ? '<div class="viewer-notice">👁 Viewer mode.</div>' : ''}
    ${isAdmin ? `<div class="card">
      <div class="card-title">Enrol New Student</div>
      <div class="form-group"><label>Full Name *</label><input type="text" id="enrol-name" placeholder="Student full name"></div>
      <div class="form-group"><label>Age</label><input type="number" id="enrol-age" placeholder="Age"></div>
      <div class="form-group"><label>Class</label>
        <select id="enrol-class"><option>Primary</option><option>Secondary</option><option>MCRI Potential Candidates</option><option>Community</option></select>
      </div>
      <div class="form-group"><label>Reading Level</label>
        <select id="enrol-level"><option>Pre-Reader</option><option>Early Reader</option><option>Fluent</option></select>
      </div>
      <div class="form-group"><label>Notes</label><textarea id="enrol-notes" rows="2" placeholder="Any notes about this student…"></textarea></div>
      <button class="btn btn-primary btn-full" onclick="enrolStudent()">➕ Enrol Student</button>
    </div>` : '<div class="card"><div class="empty-state"><div class="icon">➕</div><p>Admin access required to enrol students.</p></div></div>'}
  </div>`;
}

window.enrolStudent = async function() {
  const name = el('enrol-name').value.trim();
  if (!name) { toast('Please enter a name'); return; }
  await addDoc(collection(db,'students'), {
    name, age: el('enrol-age').value, class: el('enrol-class').value,
    readingLevel: el('enrol-level').value, notes: el('enrol-notes').value,
    enrollDate: todayStr(), createdAt: serverTimestamp(), createdBy: currentUser.uid
  });
  el('enrol-name').value=''; el('enrol-age').value=''; el('enrol-notes').value='';
  toast('✅ Student enrolled!');
};

function litPhotosHTML() {
  const isAdmin = currentRole==='admin';
  return `<div class="tab-content" id="lit-photos">
    ${!isAdmin ? '<div class="viewer-notice">👁 Viewer mode — photos are visible.</div>' : ''}
    ${isAdmin ? `<div class="card">
      <div class="card-title">Upload Session Photo</div>
      <div class="form-group"><label>Caption</label><input type="text" id="photo-caption" placeholder="e.g. Reading group session 12 Oct"></div>
      <div class="form-group"><label>Photo</label><input type="file" id="photo-file" accept="image/*"></div>
      <button class="btn btn-primary btn-full" onclick="uploadPhoto()">📸 Upload Photo</button>
    </div>` : ''}
    <div class="card">
      <div class="card-title">Session Photos</div>
      <div id="photo-grid" class="photo-grid"></div>
      <div id="photo-empty" class="empty-state" style="display:none"><div class="icon">📸</div><p>No photos yet</p></div>
    </div>
  </div>`;
}

window.uploadPhoto = async function() {
  const file = el('photo-file').files[0];
  const caption = el('photo-caption').value.trim();
  if (!file) { toast('Please select a photo'); return; }
  if (file.size > 500000) { toast('Photo too large (max 500KB). Please resize first.'); return; }
  const reader = new FileReader();
  reader.onload = async (e) => {
    await addDoc(collection(db,'photos'), {
      caption, dataUrl: e.target.result, date: todayStr(), month: monthStr(),
      createdAt: serverTimestamp(), createdBy: currentUser.uid
    });
    el('photo-caption').value=''; el('photo-file').value='';
    toast('📸 Photo uploaded!');
    loadPhotos();
  };
  reader.readAsDataURL(file);
};

async function loadPhotos() {
  const snap = await getDocs(query(collection(db,'photos'), orderBy('createdAt','desc')));
  const grid = el('photo-grid');
  const emptyEl = el('photo-empty');
  if (!grid) return;
  if (snap.empty) { grid.innerHTML=''; if(emptyEl){emptyEl.style.display='block';} return; }
  if(emptyEl){emptyEl.style.display='none';}
  const rows=[]; snap.forEach(d=>rows.push({id:d.id,...d.data()}));
  grid.innerHTML=rows.slice(0,18).map(r=>`<div style="position:relative">
    <img src="${r.dataUrl}" class="photo-thumb" alt="${r.caption||''}">
    <div style="font-size:10px;text-align:center;color:var(--muted);margin-top:2px">${r.caption||r.date||''}</div>
    ${currentRole==='admin'?`<button class="btn btn-danger btn-sm" style="position:absolute;top:4px;right:4px;padding:2px 6px" onclick="deleteDoc_('photos','${r.id}',loadPhotos)">✕</button>`:''}
  </div>`).join('');
}

function litReportsHTML() {
  return `<div class="tab-content" id="lit-reports">
    <div class="card">
      <div class="card-title">Literacy Statistics</div>
      <div id="lit-stats-content"><div class="empty-state"><div class="icon">📊</div><p>Loading…</p></div></div>
    </div>
    <div class="card">
      <div class="card-title">Reading Level Distribution</div>
      <div id="lit-reading-dist"></div>
    </div>
    <div class="card">
      ${currentRole==='admin'?`<div style="display:flex;gap:8px;flex-wrap:wrap">
        <button class="btn btn-outline btn-sm" onclick="exportSessions()">⬇ Sessions CSV</button>
        <button class="btn btn-outline btn-sm" onclick="exportStudents()">⬇ Students CSV</button>
      </div>`:''}
    </div>
  </div>`;
}

async function loadLitReports() {
  const mo = monthStr();
  const sessSnap = await getDocs(query(collection(db,'sessions'), where('month','==',mo)));
  const studSnap = await getDocs(collection(db,'students'));
  let totalLearners=0, totalHours=0;
  const classCounts = {};
  sessSnap.forEach(d=>{
    const data=d.data();
    totalLearners += data.learners||0;
    totalHours += (data.duration||0)/60;
    classCounts[data.class]=(classCounts[data.class]||0)+1;
  });
  const statsEl = el('lit-stats-content');
  if (statsEl) statsEl.innerHTML=`
    <div class="stats-row">
      <div class="stat-box"><div class="num">${sessSnap.size}</div><div class="lbl">Sessions this month</div></div>
      <div class="stat-box"><div class="num">${studSnap.size}</div><div class="lbl">Enrolled students</div></div>
      <div class="stat-box"><div class="num">${totalHours.toFixed(1)}</div><div class="lbl">Total hours</div></div>
    </div>
    <hr class="section-divider">
    <div style="font-size:13px;font-weight:600;margin-bottom:8px">Sessions by Class</div>
    ${Object.entries(classCounts).map(([k,v])=>`<div style="display:flex;justify-content:space-between;font-size:13px;padding:3px 0"><span>${k}</span><b>${v}</b></div>`).join('') || '<p style="font-size:12px;color:var(--muted)">No data</p>'}
  `;
  // reading dist
  const readingCounts = {'Pre-Reader':0,'Early Reader':0,'Fluent':0};
  studSnap.forEach(d=>{ const l=d.data().readingLevel; if(readingCounts[l]!==undefined) readingCounts[l]++; });
  const total = studSnap.size || 1;
  const distEl = el('lit-reading-dist');
  if (distEl) distEl.innerHTML = Object.entries(readingCounts).map(([k,v])=>`
    <div style="margin-bottom:10px">
      <div style="display:flex;justify-content:space-between;font-size:13px;margin-bottom:3px"><span>${k}</span><b>${v} (${Math.round(v/total*100)}%)</b></div>
      <div class="reading-bar"><div class="reading-fill" style="width:${v/total*100}%"></div></div>
    </div>`).join('');
}

// ══════════════════════════════════════════════
//  MONTHLY REPORT (13 SECTIONS)
// ══════════════════════════════════════════════
function litMonthlyHTML() {
  return `<div class="tab-content" id="lit-monthly">
    ${currentRole!=='admin' ? '<div class="viewer-notice">👁 Viewer mode — you can view and add comments.</div>' : ''}
    <div style="display:flex;gap:8px;flex-wrap:wrap;margin-bottom:12px">
      ${currentRole==='admin'?`<button class="btn btn-primary" onclick="saveMonthlyReport()">💾 Save Report</button>`:''}
      ${currentRole==='admin'?`<button class="btn btn-accent" onclick="autoFillReport()">✨ Auto-fill from Data</button>`:''}
      <button class="btn btn-outline" onclick="printReport()">🖨 Print</button>
    </div>

    <!-- S1: System Info -->
    <div class="report-section">
      <h3>📋 S1: System Information</h3>
      <div class="report-grid">
        <div class="report-field"><label>Month / Year</label><input type="text" id="r-month" placeholder="e.g. October 2026"></div>
        <div class="report-field"><label>Completed By</label><input type="text" id="r-completedby" placeholder="Mandla Ncube"></div>
        <div class="report-field"><label>Location</label><input type="text" id="r-location" placeholder="Jafuta Foundation Innovation Hub"></div>
        <div class="report-field"><label>Period</label><input type="text" id="r-period" placeholder="01 – 31 October 2026"></div>
        <div class="report-field"><label>Date Submitted</label><input type="date" id="r-submitted"></div>
        <div class="report-field"><label>System Downtime (hours)</label><input type="number" id="r-downtime" min="0" placeholder="0"></div>
        <div class="report-field full"><label>Status</label>
          <div class="status-checks">
            <label class="status-check"><input type="checkbox" id="r-status-op"> Operational</label>
            <label class="status-check"><input type="checkbox" id="r-status-partial"> Partial</label>
            <label class="status-check"><input type="checkbox" id="r-status-down"> Down</label>
            <label class="status-check"><input type="checkbox" id="r-status-maint"> Under Maintenance</label>
          </div>
        </div>
      </div>
    </div>

    <!-- S2: Device Accountability -->
    <div class="report-section">
      <h3>📱 S2: Device Accountability</h3>
      <div class="report-grid">
        <div class="report-field"><label>Responsible Person</label><input type="text" id="r-responsible" placeholder="Mandla Ncube"></div>
        <div class="report-field"><label>Device in Possession</label><select id="r-possession"><option>Yes</option><option>No</option></select></div>
        <div class="report-field full"><label>Device Left Jafuta?</label><select id="r-leftjafuta"><option>No</option><option>Yes</option></select></div>
        <div class="report-field full" id="r-leftjafuta-details-row"><label>If Yes — details</label><textarea id="r-leftdetails" rows="2" placeholder="Reason, destination, date returned…"></textarea></div>
      </div>
    </div>

    <!-- S3: Monthly Health Check -->
    <div class="report-section">
      <h3>🔧 S3: Monthly Health Check</h3>
      <table class="health-table">
        <thead><tr><th>Item</th><th>Status</th><th>Notes</th></tr></thead>
        <tbody id="health-check-body"></tbody>
      </table>
    </div>

    <!-- S4: Utilisation Dashboard -->
    <div class="report-section">
      <h3>📊 S4: Utilisation Dashboard</h3>
      <div style="font-weight:600;font-size:13px;margin-bottom:8px">Learners by Type</div>
      <div class="report-grid">
        <div class="report-field"><label>Primary</label><input type="number" id="r-u-primary" min="0" value="0"></div>
        <div class="report-field"><label>Secondary</label><input type="number" id="r-u-secondary" min="0" value="0"></div>
        <div class="report-field"><label>School Leavers</label><input type="number" id="r-u-leavers" min="0" value="0"></div>
        <div class="report-field"><label>Vocational</label><input type="number" id="r-u-vocational" min="0" value="0"></div>
        <div class="report-field"><label>Community</label><input type="number" id="r-u-community" min="0" value="0"></div>
        <div class="report-field"><label>Teachers</label><input type="number" id="r-u-teachers" min="0" value="0"></div>
      </div>
      <hr class="section-divider">
      <div style="font-weight:600;font-size:13px;margin-bottom:8px">Sessions by Subject</div>
      <div class="report-grid">
        <div class="report-field"><label>English Literacy</label><input type="number" id="r-s-literacy" min="0" value="0"></div>
        <div class="report-field"><label>ICT</label><input type="number" id="r-s-ict" min="0" value="0"></div>
        <div class="report-field"><label>Coding</label><input type="number" id="r-s-coding" min="0" value="0"></div>
        <div class="report-field"><label>Robotics</label><input type="number" id="r-s-robotics" min="0" value="0"></div>
        <div class="report-field"><label>AI</label><input type="number" id="r-s-ai" min="0" value="0"></div>
        <div class="report-field"><label>Career Guidance</label><input type="number" id="r-s-career" min="0" value="0"></div>
        <div class="report-field"><label>Teacher Development</label><input type="number" id="r-s-teachdev" min="0" value="0"></div>
        <div class="report-field"><label>Community Learning</label><input type="number" id="r-s-commlearn" min="0" value="0"></div>
        <div class="report-field"><label>Research</label><input type="number" id="r-s-research" min="0" value="0"></div>
        <div class="report-field"><label>Other</label><input type="number" id="r-s-other" min="0" value="0"></div>
      </div>
      <hr class="section-divider">
      <div class="report-grid">
        <div class="report-field"><label>Total Hours</label><input type="number" id="r-u-hours" min="0" step="0.5" value="0"></div>
        <div class="report-field"><label>Avg. Daily Users</label><input type="number" id="r-u-avgdaily" min="0" value="0"></div>
        <div class="report-field"><label>Most Used Resource</label><input type="text" id="r-u-mostused" placeholder="e.g. Khan Academy"></div>
        <div class="report-field"><label>Least Used Resource</label><input type="text" id="r-u-leastused" placeholder="e.g. GarageBand"></div>
      </div>
    </div>

    <!-- S5: Programme Impact -->
    <div class="report-section">
      <h3>🎯 S5: Programme Impact</h3>
      ${['English Literacy','ICT','Career Guidance','Teacher Development','Community Learning'].map(prog=>`
      <div style="margin-bottom:14px">
        <div style="font-weight:600;font-size:13px;margin-bottom:6px">${prog}</div>
        <div class="report-grid">
          <div class="report-field"><label>Learners Reached</label><input type="number" id="r-imp-${prog.replace(/\s+/g,'-').toLowerCase()}-learners" min="0" value="0"></div>
          <div class="report-field"><label>Sessions Held</label><input type="number" id="r-imp-${prog.replace(/\s+/g,'-').toLowerCase()}-sessions" min="0" value="0"></div>
          <div class="report-field full"><label>Key Outcome</label><textarea id="r-imp-${prog.replace(/\s+/g,'-').toLowerCase()}-outcome" rows="2" placeholder="Describe the main outcome…"></textarea></div>
        </div>
      </div>`).join('')}
    </div>

    <!-- S6: Equipment Register -->
    <div class="report-section">
      <h3>🖥 S6: Equipment Register</h3>
      <table>
        <thead><tr><th>Item</th><th>Qty</th><th>Working</th><th>Faulty</th></tr></thead>
        <tbody id="equipment-body"></tbody>
      </table>
    </div>

    <!-- S7: Incident Log -->
    <div class="report-section">
      <h3>⚠️ S7: Incident Log</h3>
      <div id="incident-list"></div>
      ${currentRole==='admin'?`<button class="btn btn-outline btn-sm" onclick="addIncidentRow()">+ Add Incident</button>`:''}
    </div>

    <!-- S8: Communication Log -->
    <div class="report-section">
      <h3>💬 S8: Communication Log</h3>
      <div id="comms-list"></div>
      ${currentRole==='admin'?`<button class="btn btn-outline btn-sm" onclick="addCommsRow()">+ Add Entry</button>`:''}
    </div>

    <!-- S9: Maintenance Log -->
    <div class="report-section">
      <h3>🔨 S9: Maintenance Log</h3>
      <table>
        <thead><tr><th>Task</th><th>Performed By</th><th>Date</th></tr></thead>
        <tbody id="maintenance-body"></tbody>
      </table>
    </div>

    <!-- S10: Risks -->
    <div class="report-section">
      <h3>⚡ S10: Risk Register</h3>
      <div id="risks-list"></div>
      ${currentRole==='admin'?`<button class="btn btn-outline btn-sm" onclick="addRiskRow()">+ Add Risk</button>`:''}
    </div>

    <!-- S11: Support Required -->
    <div class="report-section">
      <h3>🆘 S11: Support Required</h3>
      <div id="support-list"></div>
      ${currentRole==='admin'?`<button class="btn btn-outline btn-sm" onclick="addSupportRow()">+ Add Item</button>`:''}
    </div>

    <!-- S12: Evidence -->
    <div class="report-section">
      <h3>📎 S12: Evidence Checklist</h3>
      <div class="checkbox-group" id="evidence-checks">
        ${['Photos attached','Usage statistics included','Attendance registers attached','Training registers attached','Maintenance records attached','Backup confirmation included','Incident reports attached','Teacher feedback collected','Student feedback collected'].map(item=>`<label class="checkbox-item"><input type="checkbox" id="ev-${item.replace(/\s+/g,'-').toLowerCase()}"> ${item}</label>`).join('')}
      </div>
    </div>

    <!-- S13: Monthly Summary -->
    <div class="report-section">
      <h3>📝 S13: Monthly Summary</h3>
      <div class="report-field" style="margin-bottom:10px"><label>What Worked Well</label><textarea id="r-worked-well" rows="3" placeholder="Describe successes this month…"></textarea></div>
      <div class="report-field" style="margin-bottom:10px"><label>Challenges</label><textarea id="r-challenges" rows="3" placeholder="Describe challenges faced…"></textarea></div>
      <div class="report-field" style="margin-bottom:10px"><label>Key Achievements</label><textarea id="r-achievements" rows="3" placeholder="List key achievements…"></textarea></div>
      <div class="report-field" style="margin-bottom:10px"><label>Lessons Learned</label><textarea id="r-lessons" rows="3" placeholder="What was learned this month?"></textarea></div>
      <div class="report-field"><label>Top Priorities for Next Month</label><textarea id="r-priorities" rows="3" placeholder="List top priorities…"></textarea></div>
    </div>

    <!-- Viewer comments -->
    <div class="comment-box">
      <h4>💬 Comments</h4>
      <div id="report-comments-list"><p style="font-size:13px;color:var(--muted)">No comments yet.</p></div>
      <div class="form-group" style="margin-top:8px">
        <textarea id="new-comment" rows="2" placeholder="Add a comment…" style="width:100%;padding:8px;border:1px solid var(--border);border-radius:6px;font-size:13px"></textarea>
        <button class="btn btn-primary btn-sm" style="margin-top:6px" onclick="addReportComment()">Post Comment</button>
      </div>
    </div>

    <div style="height:40px"></div>
  </div>`;
}

// Health check items
const HEALTH_ITEMS = ['Device powers on','Device boots correctly','Storage adequate','Wireless connectivity','AI platform functioning','Educational library accessible','Whiteboard connected','External monitor working','Power supply inspected','Ports inspected','Shutdown correctly'];
// Equipment items
const EQUIPMENT_ITEMS = ['Beelink Mini PC','Screen/Monitor','Power Supply','UPS','Router/WiFi','Interactive Whiteboard','Chromebooks','iPads','MacBooks'];
// Maintenance tasks
const MAINTENANCE_TASKS = ['General cleaning','Software updates','Data backups','System testing','Hardware inspection','Network testing','Cooling/ventilation inspection'];

function buildReportTables() {
  // Health check
  const hb = el('health-check-body');
  if (hb && !hb.hasChildNodes()) {
    hb.innerHTML = HEALTH_ITEMS.map(item=>`<tr>
      <td>${item}</td>
      <td><select style="font-size:12px;padding:3px;border:1px solid var(--border);border-radius:4px" id="hc-${item.replace(/\s+/g,'-').toLowerCase()}"><option>✅ OK</option><option>⚠️ Issue</option><option>❌ Fail</option><option>N/A</option></select></td>
      <td><input type="text" placeholder="Notes" style="font-size:12px;padding:3px;border:1px solid var(--border);border-radius:4px;width:100%" id="hcn-${item.replace(/\s+/g,'-').toLowerCase()}"></td>
    </tr>`).join('');
  }
  // Equipment
  const eb = el('equipment-body');
  if (eb && !eb.hasChildNodes()) {
    eb.innerHTML = EQUIPMENT_ITEMS.map(item=>`<tr>
      <td>${item}</td>
      <td><input type="number" min="0" value="1" style="width:50px;font-size:12px;padding:3px;border:1px solid var(--border);border-radius:4px" id="eq-qty-${item.replace(/\s+/g,'-').toLowerCase()}"></td>
      <td><input type="number" min="0" value="1" style="width:50px;font-size:12px;padding:3px;border:1px solid var(--border);border-radius:4px" id="eq-ok-${item.replace(/\s+/g,'-').toLowerCase()}"></td>
      <td><input type="number" min="0" value="0" style="width:50px;font-size:12px;padding:3px;border:1px solid var(--border);border-radius:4px" id="eq-fault-${item.replace(/\s+/g,'-').toLowerCase()}"></td>
    </tr>`).join('');
  }
  // Maintenance
  const mb = el('maintenance-body');
  if (mb && !mb.hasChildNodes()) {
    mb.innerHTML = MAINTENANCE_TASKS.map(task=>`<tr>
      <td>${task}</td>
      <td><input type="text" placeholder="Name" style="font-size:12px;padding:3px;border:1px solid var(--border);border-radius:4px;width:100%" id="mt-by-${task.replace(/\s+/g,'-').toLowerCase()}"></td>
      <td><input type="date" style="font-size:12px;padding:3px;border:1px solid var(--border);border-radius:4px" id="mt-date-${task.replace(/\s+/g,'-').toLowerCase()}"></td>
    </tr>`).join('');
  }
  // Incident
  const il = el('incident-list');
  if (il && !il.hasChildNodes()) addIncidentRow();
  // Comms
  const cl = el('comms-list');
  if (cl && !cl.hasChildNodes()) addCommsRow();
  // Risks
  const rl = el('risks-list');
  if (rl && !rl.hasChildNodes()) addRiskRow();
  // Support
  const sl = el('support-list');
  if (sl && !sl.hasChildNodes()) addSupportRow();
}

let incidentCount=0, commsCount=0, riskCount=0, supportCount=0;

window.addIncidentRow = function() {
  const i = incidentCount++;
  el('incident-list').insertAdjacentHTML('beforeend',`<div class="card" style="margin-bottom:8px;padding:10px" id="incident-${i}">
    <div style="display:flex;justify-content:space-between;margin-bottom:6px"><b style="font-size:13px">Incident ${i+1}</b><button class="btn btn-danger btn-sm" onclick="el('incident-${i}').remove()">✕</button></div>
    <div class="report-grid">
      <div class="report-field"><label>Date</label><input type="date" id="inc-date-${i}"></div>
      <div class="report-field"><label>Who Informed</label><input type="text" id="inc-who-${i}" placeholder="Name/Role"></div>
      <div class="report-field full"><label>Description</label><textarea id="inc-desc-${i}" rows="2" placeholder="Describe the incident…"></textarea></div>
      <div class="report-field full"><label>Impact</label><textarea id="inc-impact-${i}" rows="2" placeholder="What was the impact?"></textarea></div>
      <div class="report-field full"><label>Action Taken</label><textarea id="inc-action-${i}" rows="2" placeholder="What was done?"></textarea></div>
      <div class="report-field"><label>Date Resolved</label><input type="date" id="inc-resolved-${i}"></div>
      <div class="report-field"><label>Outstanding?</label><select id="inc-outstanding-${i}"><option>No</option><option>Yes</option></select></div>
    </div>
  </div>`);
};

window.addCommsRow = function() {
  const i = commsCount++;
  el('comms-list').insertAdjacentHTML('beforeend',`<div class="card" style="margin-bottom:8px;padding:10px" id="comms-${i}">
    <div style="display:flex;justify-content:space-between;margin-bottom:6px"><b style="font-size:13px">Entry ${i+1}</b><button class="btn btn-danger btn-sm" onclick="el('comms-${i}').remove()">✕</button></div>
    <div class="report-grid">
      <div class="report-field"><label>Date</label><input type="date" id="comm-date-${i}"></div>
      <div class="report-field"><label>Person</label><input type="text" id="comm-person-${i}" placeholder="Name"></div>
      <div class="report-field full"><label>Issue / Topic</label><textarea id="comm-issue-${i}" rows="2" placeholder="What was discussed?"></textarea></div>
      <div class="report-field full"><label>Outcome</label><textarea id="comm-outcome-${i}" rows="2" placeholder="What was the outcome?"></textarea></div>
    </div>
  </div>`);
};

window.addRiskRow = function() {
  const i = riskCount++;
  el('risks-list').insertAdjacentHTML('beforeend',`<div class="card" style="margin-bottom:8px;padding:10px" id="risk-${i}">
    <div style="display:flex;justify-content:space-between;margin-bottom:6px"><b style="font-size:13px">Risk ${i+1}</b><button class="btn btn-danger btn-sm" onclick="el('risk-${i}').remove()">✕</button></div>
    <div class="report-grid">
      <div class="report-field full"><label>Risk</label><input type="text" id="risk-desc-${i}" placeholder="Describe the risk…"></div>
      <div class="report-field"><label>Likelihood</label><select id="risk-like-${i}"><option>Low</option><option>Medium</option><option>High</option></select></div>
      <div class="report-field"><label>Impact</label><select id="risk-impact-${i}"><option>Low</option><option>Medium</option><option>High</option></select></div>
      <div class="report-field full"><label>Mitigation</label><textarea id="risk-mit-${i}" rows="2" placeholder="How is this being managed?"></textarea></div>
      <div class="report-field"><label>Responsible</label><input type="text" id="risk-resp-${i}" placeholder="Name/Role"></div>
    </div>
  </div>`);
};

window.addSupportRow = function() {
  const i = supportCount++;
  el('support-list').insertAdjacentHTML('beforeend',`<div class="card" style="margin-bottom:8px;padding:10px" id="support-${i}">
    <div style="display:flex;justify-content:space-between;margin-bottom:6px"><b style="font-size:13px">Item ${i+1}</b><button class="btn btn-danger btn-sm" onclick="el('support-${i}').remove()">✕</button></div>
    <div class="report-grid">
      <div class="report-field full"><label>Resource / Support Needed</label><input type="text" id="sup-res-${i}" placeholder="Describe what is needed…"></div>
      <div class="report-field full"><label>Reason</label><textarea id="sup-reason-${i}" rows="2" placeholder="Why is this needed?"></textarea></div>
      <div class="report-field full"><label>Impact if Not Provided</label><textarea id="sup-impact-${i}" rows="2" placeholder="What happens without it?"></textarea></div>
      <div class="report-field"><label>Priority</label><select id="sup-priority-${i}"><option>High</option><option>Medium</option><option>Low</option></select></div>
    </div>
  </div>`);
};

// Auto-fill from live Firestore data
window.autoFillReport = async function() {
  const mo = monthStr();
  const d = new Date();
  const monthName = d.toLocaleDateString('en-ZW',{month:'long',year:'numeric'});
  el('r-month').value = monthName;
  el('r-completedby').value = 'Mandla Ncube';
  el('r-location').value = 'Jafuta Foundation Innovation Hub, Bulawayo';
  el('r-submitted').value = todayStr();
  el('r-responsible').value = 'Mandla Ncube';

  // sessions data
  const sessSnap = await getDocs(query(collection(db,'sessions'), where('month','==',mo)));
  let litSessions=0, totalLearners=0, totalHours=0, primaryCount=0, secondaryCount=0, mcriCount=0;
  sessSnap.forEach(d=>{
    const data=d.data();
    litSessions++;
    totalLearners += data.learners||0;
    totalHours += (data.duration||0)/60;
    if (data.class==='Primary') primaryCount += data.learners||0;
    else if (data.class==='Secondary') secondaryCount += data.learners||0;
    else if (data.class==='MCRI Potential Candidates') mcriCount += data.learners||0;
  });
  el('r-s-literacy').value = litSessions;
  el('r-u-primary').value = primaryCount;
  el('r-u-secondary').value = secondaryCount;
  el('r-u-hours').value = totalHours.toFixed(1);
  // impact
  const impLit = el('r-imp-english-literacy-learners');
  const impSess = el('r-imp-english-literacy-sessions');
  if (impLit) impLit.value = totalLearners;
  if (impSess) impSess.value = litSessions;

  // check-ins for hub
  const ciSnap = await getDocs(query(collection(db,'checkins'), where('month','==',mo)));
  const activeDays = new Set(ciSnap.docs.map(d=>d.data().date)).size;
  el('r-u-avgdaily').value = activeDays > 0 ? Math.round(ciSnap.size/activeDays) : 0;

  toast('✨ Report auto-filled from live data!');
};

window.saveMonthlyReport = async function() {
  const month = el('r-month').value;
  if (!month) { toast('Please enter the month'); return; }
  await addDoc(collection(db,'monthlyreports'), {
    month, completedBy: el('r-completedby').value,
    location: el('r-location').value, period: el('r-period').value,
    submittedDate: el('r-submitted').value, downtime: el('r-downtime').value,
    workedWell: el('r-worked-well').value, challenges: el('r-challenges').value,
    achievements: el('r-achievements').value, lessons: el('r-lessons').value,
    priorities: el('r-priorities').value,
    savedAt: serverTimestamp(), createdBy: currentUser.uid
  });
  toast('✅ Monthly report saved!');
};

window.addReportComment = async function() {
  const text = el('new-comment').value.trim();
  if (!text) return;
  const snap = await getDoc(doc(db,'users',currentUser.uid));
  const name = snap.exists() ? snap.data().name : currentUser.email;
  await addDoc(collection(db,'reportcomments'), {
    text, authorName: name, authorRole: currentRole,
    date: todayStr(), createdAt: serverTimestamp()
  });
  el('new-comment').value = '';
  toast('💬 Comment added!');
  loadReportComments();
};

async function loadReportComments() {
  const snap = await getDocs(query(collection(db,'reportcomments'), orderBy('createdAt','desc')));
  const list = el('report-comments-list');
  if (!list) return;
  if (snap.empty) { list.innerHTML='<p style="font-size:13px;color:var(--muted)">No comments yet.</p>'; return; }
  const rows=[]; snap.forEach(d=>rows.push({id:d.id,...d.data()}));
  list.innerHTML=rows.map(r=>`<div class="comment-item">
    <div class="comment-meta">${r.authorName||'User'} (${r.authorRole||''}) · ${r.date||''}</div>
    <div>${r.text}</div>
  </div>`).join('');
}

window.printReport = function() { window.print(); };

// Build tables when monthly tab is activated
const origActivateTabGlobal = window.activateTabGlobal;
window.activateTabGlobal = function(mod, tabId) {
  origActivateTabGlobal(mod, tabId);
  if (tabId === 'lit-monthly') {
    buildReportTables();
    loadReportComments();
  }
  if (tabId === 'lit-reports') loadLitReports();
  if (tabId === 'hub-lessonplan') loadLessonPlans();
};

// Load lesson plans on tab build
setTimeout(loadLessonPlans, 500);

// ══════════════════════════════════════════════
//  SHARED UTIL: deleteDoc
// ══════════════════════════════════════════════
window.deleteDoc_ = async function(collName, docId, refreshFn) {
  if (!confirm('Delete this record?')) return;
  await deleteDoc(doc(db, collName, docId));
  toast('🗑 Deleted');
  if (typeof refreshFn === 'function') refreshFn();
};

window.el = el;
</script>
</body>
</html>
