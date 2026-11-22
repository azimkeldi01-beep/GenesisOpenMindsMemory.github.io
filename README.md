<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Genesis — Open Minds Memory</title>
<style>
:root {
  --bg: #080707;
  --surface: #151010;
  --surface2: #201313;
  --primary: #a51e28;
  --primary-light: #d33b45;
  --gold: #c5a36a;
  --text: #f5eeee;
  --muted: #a99a9a;
  --border: rgba(255,255,255,.12);
  --radius: 20px;
}
* { box-sizing: border-box; }
html { scroll-behavior: smooth; }
body {
  margin: 0;
  background: var(--bg);
  color: var(--text);
  font-family: Inter, Arial, sans-serif;
  overflow-x: hidden;
}
body::before {
  content: "";
  position: fixed;
  inset: 0;
  z-index: -1;
  pointer-events: none;
  background:
    radial-gradient(ellipse at 10% 0%, rgba(133,13,23,.3), transparent 45%),
    radial-gradient(ellipse at 95% 80%, rgba(95,13,18,.2), transparent 40%);
}
button, input, textarea, select { font: inherit; }
button { cursor: pointer; }
.hidden { display: none !important; }
a { color: inherit; }
.topline {
  height: 5px;
  background: linear-gradient(90deg,#5e090e,#b92a35,#21080a);
}
.auth-screen {
  min-height: 100vh;
  display: grid;
  place-items: center;
  padding: 24px;
}
.auth-card {
  width: min(440px,100%);
  background: rgba(20,12,12,.9);
  border: 1px solid var(--border);
  border-radius: 25px;
  padding: 36px;
  box-shadow: 0 25px 90px rgba(0,0,0,.5);
  backdrop-filter: blur(18px);
}
.brand {
  font-family: Georgia,serif;
  letter-spacing: .17em;
  font-size: 30px;
  font-weight: 400;
}
.brand span { color: var(--primary-light); }
.eyebrow {
  font-size: 10px;
  letter-spacing: .2em;
  color: var(--gold);
  text-transform: uppercase;
}
.auth-card h1 {
  font-size: 29px;
  font-weight: 500;
  margin: 32px 0 8px;
}
.auth-card p,.notice {
  color: var(--muted);
  line-height: 1.6;
  font-size: 13px;
}
label {
  display: block;
  color: #d5c4c4;
  font-size: 12px;
  margin: 17px 0 8px;
}
input,textarea,select {
  width: 100%;
  padding: 13px 14px;
  color: var(--text);
  background: #100c0c;
  border: 1px solid var(--border);
  border-radius: 11px;
  outline: none;
}
input:focus,textarea:focus,select:focus {
  border-color: var(--primary-light);
  box-shadow: 0 0 0 3px rgba(180,35,45,.12);
}
textarea { resize: vertical; min-height: 100px; }
input::placeholder,textarea::placeholder { color: #766969; }
.btn {
  border: 1px solid var(--border);
  border-radius: 12px;
  padding: 12px 17px;
  color: var(--text);
  background: #211515;
  transition: .2s;
}
.btn:hover { transform: translateY(-2px); border-color: #a54a50; }
.btn.primary {
  background: linear-gradient(120deg,#8b101b,#bd2934);
  border-color: #b63b44;
}
.btn.secondary { background: #241515; }
.btn.ghost { background: transparent; }
.btn.full { width: 100%; margin-top: 18px; }
.auth-switch {
  color: var(--gold);
  background: none;
  border: 0;
  padding: 0;
}
.status { font-size: 12px; margin-top: 10px; color: var(--gold); }
.app-screen { min-height: 100vh; }
.nav {
  max-width: 1320px;
  padding: 20px 5%;
  margin: auto;
  display: flex;
  justify-content: space-between;
  align-items: center;
  border-bottom: 1px solid var(--border);
}
.nav-right { display: flex; align-items: center; gap: 14px; }
.user-email { color: var(--muted); font-size: 12px; }
.hero {
  max-width: 1320px;
  margin: 35px auto 65px;
  padding: 65px 5%;
  min-height: 430px;
  position: relative;
  overflow: hidden;
  display: flex;
  align-items: center;
  background:
    linear-gradient(90deg,rgba(0,0,0,.96),rgba(0,0,0,.65),rgba(0,0,0,.12)),
    radial-gradient(circle at 80% 40%,#642026,#160b0b 55%);
  border: 1px solid var(--border);
  border-radius: 4px;
}
.hero::after {
  content: "GENESIS";
  position: absolute;
  right: -15px;
  bottom: -55px;
  font-family: Georgia,serif;
  font-size: clamp(80px,17vw,220px);
  letter-spacing: .06em;
  color: rgba(255,255,255,.035);
  white-space: nowrap;
  pointer-events: none;
}
.hero-content { position: relative; z-index: 1; max-width: 620px; }
.hero h1 {
  font-family: Georgia,serif;
  font-size: clamp(46px,8vw,92px);
  line-height: .98;
  font-weight: 400;
  letter-spacing: -.04em;
  margin: 20px 0;
}
.hero h1 em { color: #d5a4a0; font-weight: 400; }
.hero p { color: #c3b4b4; line-height: 1.8; max-width: 460px; }
.hero-line {
  height: 1px;
  width: 100px;
  background: var(--gold);
  margin: 25px 0;
}
.main-content { max-width: 1320px; margin: auto; padding: 0 5% 80px; }
.section { margin: 70px 0; }
.section-head { margin-bottom: 25px; }
.section-head h2 {
  font-family: Georgia,serif;
  font-weight: 400;
  font-size: clamp(28px,4vw,43px);
  margin: 9px 0;
}
.section-head p { color: var(--muted); font-size: 13px; }
.layout-two {
  display: grid;
  grid-template-columns: minmax(0,1.05fr) minmax(0,.95fr);
  gap: 22px;
}
.card {
  background: linear-gradient(145deg,rgba(34,19,19,.95),rgba(15,12,12,.95));
  border: 1px solid var(--border);
  border-radius: var(--radius);
  padding: 25px;
  box-shadow: 0 15px 45px rgba(0,0,0,.18);
}
.card h2,.card h3 { font-weight: 500; }
.card h3 { font-size: 17px; }
.form-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 0 14px;
}
.form-grid .wide { grid-column: 1/-1; }
.color-row,.mood-row { display: flex; gap: 10px; flex-wrap: wrap; margin-top: 10px; }
.color-dot {
  width: 27px; height: 27px; border-radius: 50%;
  border: 2px solid rgba(255,255,255,.25);
  cursor: pointer;
}
.color-dot.selected { outline: 2px solid white; outline-offset: 3px; }
.mood-button {
  border: 1px solid var(--border);
  background: #120d0d;
  border-radius: 10px;
  padding: 8px 10px;
  font-size: 19px;
}
.mood-button.selected { border-color: var(--gold); background: #382020; }
.share-panel {
  border-top: 1px solid var(--border);
  margin-top: 22px;
  padding-top: 20px;
}
.stats { display: flex; gap: 12px; margin: 22px 0; }
.stat {
  flex: 1;
  background: rgba(145,28,38,.13);
  border: 1px solid rgba(175,60,70,.16);
  border-radius: 13px;
  padding: 16px;
}
.stat strong { display: block; font-size: 28px; color: #e5b5a9; }
.stat span { color: var(--muted); font-size: 10px; letter-spacing: .1em; }
.grid {
  display: grid;
  grid-template-columns: repeat(3,minmax(0,1fr));
  gap: 17px;
}
.memory-card {
  background: #151010;
  border: 1px solid var(--border);
  border-radius: 17px;
  overflow: hidden;
  transition: .25s;
}
.memory-card:hover { transform: translateY(-4px); border-color: #91414a; }
.memory-cover {
  min-height: 125px;
  padding: 20px;
  display: flex;
  align-items: end;
  background: linear-gradient(140deg,var(--cover,#7c1822),#130b0b);
}
.memory-cover h3 { font-family: Georgia,serif; font-size: 24px; margin: 0; }
.memory-info { padding: 17px; }
.memory-info p { color: var(--muted); font-size: 12px; line-height: 1.6; }
.memory-meta { font-size: 10px; color: var(--gold); margin: 10px 0; }
.memory-actions { display: flex; gap: 8px; flex-wrap: wrap; }
.memory-actions .btn { padding: 8px 10px; font-size: 11px; }
.empty {
  border: 1px dashed var(--border);
  border-radius: 16px;
  padding: 35px;
  text-align: center;
  color: var(--muted);
  grid-column: 1/-1;
}
.shared-folder-layout {
  display: grid;
  grid-template-columns: minmax(260px,.75fr) minmax(0,1.5fr);
  gap: 20px;
}
.shared-folder-list { display: grid; gap: 9px; margin-top: 15px; }
.shared-folder-entry {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 10px;
  padding: 12px;
  background: #110c0c;
  border: 1px solid var(--border);
  border-radius: 11px;
  cursor: pointer;
}
.shared-folder-entry.active { border-color: var(--primary-light); background: #2b1114; }
.shared-folder-entry strong { font-size: 12px; }
.shared-folder-entry small { display: block; color: var(--muted); font-size: 10px; margin-top: 4px; }
.shared-workspace { min-height: 400px; }
.shared-members {
  color: var(--muted);
  font-size: 11px;
  margin: 15px 0;
  padding: 12px;
  background: #100b0b;
  border-radius: 10px;
}
.shared-invite { display: flex; gap: 8px; margin-top: 10px; }
.shared-invite input { min-width: 0; }
.shared-breadcrumb {
  color: var(--gold);
  font-size: 12px;
  margin: 22px 0 12px;
}
.shared-toolbar { display: flex; gap: 8px; flex-wrap: wrap; }
.shared-toolbar .btn { font-size: 11px; padding: 9px 12px; }
.shared-items {
  display: grid;
  grid-template-columns: repeat(2,minmax(0,1fr));
  gap: 10px;
  margin-top: 18px;
}
.shared-item {
  border: 1px solid var(--border);
  background: #100c0c;
  border-radius: 13px;
  padding: 15px;
  min-width: 0;
}
.shared-item strong { display: block; overflow-wrap: anywhere; font-size: 13px; }
.shared-item small { color: var(--muted); font-size: 10px; }
.shared-item p { color: #c5b7b7; font-size: 12px; line-height: 1.6; overflow-wrap: anywhere; }
.shared-item-actions { display: flex; gap: 6px; flex-wrap: wrap; margin-top: 12px; }
.shared-item-actions .btn { font-size: 10px; padding: 7px 9px; }
.modal {
  position: fixed; inset: 0; z-index: 10;
  background: rgba(0,0,0,.8);
  display: grid; place-items: center;
  padding: 20px;
}
.modal-box {
  width: min(650px,100%);
  max-height: 85vh;
  overflow: auto;
  background: #171010;
  border: 1px solid var(--border);
  border-radius: 18px;
  padding: 24px;
}
.modal-head { display: flex; justify-content: space-between; align-items: center; gap: 15px; }
.modal-head h2 { font-family: Georgia,serif; font-weight: 400; }
footer {
  text-align: center;
  border-top: 1px solid var(--border);
  padding: 28px 15px;
  color: #786b6b;
  font-size: 10px;
  letter-spacing: .16em;
}
@media(max-width:850px) {
  .layout-two,.shared-folder-layout { grid-template-columns: 1fr; }
  .grid { grid-template-columns: repeat(2,minmax(0,1fr)); }
}
@media(max-width:560px) {
  .nav { padding: 16px 5%; }
  .brand { font-size: 23px; }
  .user-email { display: none; }
  .hero { margin: 15px 4% 40px; padding: 40px 7%; min-height: 360px; }
  .main-content { padding: 0 4% 50px; }
  .section { margin: 48px 0; }
  .card { padding: 18px; }
  .grid { grid-template-columns: 1fr; }
  .form-grid { grid-template-columns: 1fr; }
  .form-grid .wide { grid-column: auto; }
  .shared-items { grid-template-columns: 1fr; }
  .stats { gap: 8px; }
  .stat { padding: 12px; }
  .shared-invite { flex-direction: column; }
}
</style>
</head>
<body>
<div class="topline"></div>

<section class="auth-screen" id="authScreen">
  <div class="auth-card">
    <div class="brand">GENESIS<span>.</span></div>
    <div class="eyebrow" style="margin-top:12px">OPEN MINDS MEMORY</div>
    <h1 id="authTitle">Добро пожаловать</h1>
    <p id="authDescription">Сохраняйте важные моменты своей жизни в одном месте.</p>
    <form id="authForm">
      <label>Электронная почта</label>
      <input id="authEmail" type="email" required placeholder="you@example.com">
      <label>Пароль</label>
      <input id="authPassword" type="password" required minlength="6" placeholder="Минимум 6 символов">
      <button class="btn primary full" id="authButton" type="submit">Войти</button>
      <div id="authStatus" class="status"></div>
    </form>
    <p style="margin-top:22px">
      <span id="switchText">Нет аккаунта?</span>
      <button class="auth-switch" id="switchAuth" type="button">Зарегистрироваться</button>
    </p>
  </div>
</section>

<div class="app-screen hidden" id="appScreen">
  <nav class="nav">
    <div class="brand">GENESIS<span>.</span></div>
    <div class="nav-right">
      <span class="user-email" id="userEmail"></span>
      <button class="btn ghost" id="logoutButton">Выйти</button>
    </div>
  </nav>

  <header class="hero">
    <div class="hero-content">
      <div class="eyebrow">YOUR STORY · YOUR SPACE</div>
      <h1>Keep your<br><em>moments.</em></h1>
      <div class="hero-line"></div>
      <p>Каждое мгновение заслуживает того, чтобы остаться с вами. Создавайте свою историю, сохраняйте воспоминания и делитесь ими с близкими.</p>
      <a href="#createMemory" class="btn primary" style="display:inline-block;text-decoration:none;margin-top:12px">Создать воспоминание ↗</a>
    </div>
  </header>

  <main class="main-content">
    <section class="section layout-two" id="createMemory">
      <div class="card">
        <div class="eyebrow">01 / NEW MEMORY</div>
        <h2 style="font-family:Georgia,serif;font-size:30px;font-weight:400;margin:12px 0">Запечатлеть момент</h2>
        <p class="notice">Добавьте детали, чтобы сохранить воспоминание таким, каким вы его помните.</p>
        <form id="memoryForm">
          <label>Название воспоминания</label>
          <input id="memoryName" required maxlength="100" placeholder="Например, незабываемый вечер">
          <label>Описание</label>
          <textarea id="memoryDescription" placeholder="Расскажите свою историю..."></textarea>
          <div class="form-grid">
            <div>
              <label>Песня / ссылка</label>
              <input id="songUrl" placeholder="https://...">
            </div>
            <div>
              <label>Название песни</label>
              <input id="songInfo" placeholder="Название — исполнитель">
            </div>
            <div>
              <label>Погода</label>
              <input id="weather" placeholder="Солнечно ☀️">
            </div>
            <div>
              <label>Настроение</label>
              <div class="mood-row">
                <button type="button" class="mood-button selected" data-mood="😊">😊</button>
                <button type="button" class="mood-button" data-mood="❤️">❤️</button>
                <button type="button" class="mood-button" data-mood="🥹">🥹</button>
                <button type="button" class="mood-button" data-mood="🌙">🌙</button>
                <button type="button" class="mood-button" data-mood="✨">✨</button>
              </div>
            </div>
          </div>
          <label>Цвет карточки</label>
          <div class="color-row">
            <button type="button" class="color-dot selected" data-color="#8b1824" style="background:#8b1824"></button>
            <button type="button" class="color-dot" data-color="#76502e" style="background:#76502e"></button>
            <button type="button" class="color-dot" data-color="#354c55" style="background:#354c55"></button>
            <button type="button" class="color-dot" data-color="#594267" style="background:#594267"></button>
            <button type="button" class="color-dot" data-color="#4b5a3c" style="background:#4b5a3c"></button>
          </div>
          <label>Фотографии и файлы</label>
          <input id="memoryFiles" type="file" multiple>
          <button class="btn primary full" type="submit">Сохранить воспоминание</button>
          <div id="memoryStatus" class="status"></div>
        </form>
      </div>

      <div class="card">
        <div class="eyebrow">02 / YOUR COLLECTION</div>
        <h2 style="font-family:Georgia,serif;font-size:30px;font-weight:400;margin:12px 0">Ваше пространство</h2>
        <p class="notice">Личный архив моментов, которые хочется сохранить.</p>
        <div class="stats">
          <div class="stat"><strong id="memoryCount">0</strong><span>ВОСПОМИНАНИЙ</span></div>
          <div class="stat"><strong id="sharedCount">0</strong><span>ДОСТУПОВ</span></div>
        </div>
        <div class="share-panel">
          <h3>Поделиться воспоминанием</h3>
          <p class="notice">Введите почту зарегистрированного пользователя Genesis.</p>
          <label>Электронная почта получателя</label>
          <input id="shareEmail" type="email" placeholder="friend@example.com">
          <button class="btn secondary full" id="shareButton" type="button">Поделиться</button>
          <div id="shareStatus" class="status"></div>
        </div>
      </div>
    </section>

    <section class="section">
      <div class="section-head">
        <div class="eyebrow">03 / PRIVATE ARCHIVE</div>
        <h2>Мои воспоминания</h2>
        <p>Все моменты, которые вы сохранили.</p>
      </div>
      <div id="memoryGrid" class="grid"><div class="empty">Загрузка воспоминаний...</div></div>
    </section>

    <section class="section">
      <div class="section-head">
        <div class="eyebrow">04 / SHARED WITH ME</div>
        <h2>Со мной поделились</h2>
        <p>Воспоминания, которыми поделились другие пользователи.</p>
      </div>
      <div id="receivedGrid" class="grid"><div class="empty">Загрузка...</div></div>
    </section>

    <section class="section" id="sharedFoldersSection">
      <div class="section-head">
        <div class="eyebrow">05 / COLLABORATION SPACE</div>
        <h2>Общие папки</h2>
        <p>Создавайте общие пространства, приглашайте участников и собирайте материалы вместе.</p>
      </div>
      <div class="shared-folder-layout">
        <div class="card">
          <h3>Создать папку</h3>
          <label>Название общей папки</label>
          <input id="newSharedFolderName" maxlength="80" placeholder="Например, Наш проект">
          <button class="btn primary full" id="createSharedFolderButton" type="button">Создать общую папку</button>
          <div id="sharedFolderCreateStatus" class="status"></div>

          <div class="share-panel">
            <h3>Войти по приглашению</h3>
            <p class="notice">Вставьте ссылку или код приглашения, который вам отправили.</p>
            <input id="sharedInviteInput" placeholder="Ссылка или код приглашения">
            <button class="btn secondary full" id="joinSharedFolderButton" type="button">Присоединиться</button>
            <div id="sharedInviteStatus" class="status"></div>
          </div>

          <div class="share-panel">
            <h3>Мои общие папки</h3>
            <div id="sharedFolderList" class="shared-folder-list"><div class="empty">Загрузка папок...</div></div>
          </div>
        </div>

        <div class="card shared-workspace">
          <div class="eyebrow">SHARED WORKSPACE</div>
          <h3 id="activeSharedFolderTitle" style="font-family:Georgia,serif;font-size:25px;font-weight:400">Выберите общую папку</h3>
          <p id="activeSharedFolderDescription" class="notice">Откройте папку слева или создайте новую. Участники смогут совместно добавлять материалы.</p>
          <div id="sharedFolderWorkspace" class="hidden">
            <div class="shared-members" id="sharedFolderMembers"></div>
            <div id="sharedFolderInviteArea" class="hidden">
              <button class="btn secondary" id="createSharedInviteButton" type="button">Создать ссылку-приглашение</button>
              <div id="sharedFolderInviteStatus" class="status"></div>
              <div class="shared-invite hidden" id="sharedInviteLinkArea">
                <input id="sharedInviteLink" readonly>
                <button class="btn ghost" id="copySharedInviteButton" type="button">Копировать</button>
              </div>
            </div>
            <div class="shared-breadcrumb" id="sharedFolderBreadcrumb"></div>
            <div class="shared-toolbar">
              <button class="btn secondary" id="sharedBackButton" type="button">← Назад</button>
              <button class="btn primary" id="newSharedSubfolderButton" type="button">＋ Папка</button>
              <button class="btn secondary" id="newSharedNoteButton" type="button">＋ Заметка</button>
              <button class="btn secondary" id="uploadSharedFilesButton" type="button">＋ Файлы</button>
              <input id="sharedFilesInput" type="file" multiple class="hidden">
            </div>
            <div id="sharedFolderStatus" class="status"></div>
            <div id="sharedFolderItems" class="shared-items"></div>
          </div>
        </div>
      </div>
    </section>
  </main>
  <footer>GENESIS — OPEN MINDS MEMORY · YOUR STORY. YOUR SPACE.</footer>
</div>

<div id="memoryModal" class="modal hidden">
  <div class="modal-box">
    <div class="modal-head">
      <h2 id="modalTitle">Воспоминание</h2>
      <button class="btn ghost" id="closeModalButton">Закрыть</button>
    </div>
    <div id="modalBody"></div>
  </div>
</div>

<script>
const SUPABASE_URL = "https://ydrzlazhucdlvvyjisnm.supabase.co";
const SUPABASE_ANON_KEY = "sb_publishable_l_aik6ePDy4GFPZRwBH1ZQ_9oSb_Dji";

const supabase = window.supabase.createClient(SUPABASE_URL, SUPABASE_ANON_KEY);

let currentUser = null;
let isSignUp = false;
let selectedColor = "#8b1824";
let selectedMood = "😊";
let myMemories = [];
let receivedMemories = [];
let sharedFolders = [];
let sharedFolderMembers = [];
let sharedFolderItems = [];
let activeSharedFolder = null;
let sharedFolderPath = [];

const $ = (id) => document.getElementById(id);

function escapeHTML(value) {
  return String(value ?? "").replace(/[&<>"']/g, char => ({
    "&":"&amp;","<":"&lt;",">":"&gt;",'"':"&quot;","'":"&#39;"
  }[char]));
}

function status(id, message, isError = false) {
  const element = $(id);
  if (!element) return;
  element.textContent = message;
  element.style.color = isError ? "#e46b72" : "var(--gold)";
}

function formatDate(value) {
  return new Date(value).toLocaleString("ru-RU", {
    day:"numeric",month:"long",year:"numeric",
    hour:"2-digit",minute:"2-digit"
  });
}

function safeFileName(name) {
  return String(name || "file").replace(/[^\wа-яА-ЯёЁ.-]+/g, "_").slice(0,100);
}

// AUTHENTICATION
$("switchAuth").addEventListener("click", () => {
  isSignUp = !isSignUp;
  $("authTitle").textContent = isSignUp ? "Создать аккаунт" : "Добро пожаловать";
  $("authDescription").textContent = isSignUp
    ? "Зарегистрируйтесь, чтобы начать сохранять воспоминания."
    : "Сохраняйте важные моменты своей жизни в одном месте.";
  $("authButton").textContent = isSignUp ? "Зарегистрироваться" : "Войти";
  $("switchText").textContent = isSignUp ? "Уже есть аккаунт?" : "Нет аккаунта?";
  $("switchAuth").textContent = isSignUp ? "Войти" : "Зарегистрироваться";
});

$("authForm").addEventListener("submit", async (event) => {
  event.preventDefault();
  const email = $("authEmail").value.trim();
  const password = $("authPassword").value;
  status("authStatus", "Пожалуйста, подождите...");

  const result = isSignUp
    ? await supabase.auth.signUp({ email, password })
    : await supabase.auth.signInWithPassword({ email, password });

  if (result.error) {
    status("authStatus", result.error.message, true);
    return;
  }
  if (isSignUp && !result.data.session) {
    status("authStatus", "Аккаунт создан. Проверьте почту и подтвердите регистрацию.");
    return;
  }
  status("authStatus", "Успешно!");
});

$("logoutButton").addEventListener("click", async () => {
  await supabase.auth.signOut();
});

async function showApp(user) {
  currentUser = user;
  $("authScreen").classList.add("hidden");
  $("appScreen").classList.remove("hidden");
  $("userEmail").textContent = user.email || "";
  await loadMemories();
  await loadReceivedMemories();
  await loadSharedFolders();
  await handlePendingSharedInvite();
}

async function showAuth() {
  currentUser = null;
  activeSharedFolder = null;
  sharedFolderPath = [];
  $("appScreen").classList.add("hidden");
  $("authScreen").classList.remove("hidden");
}

supabase.auth.onAuthStateChange((event, session) => {
  if (session?.user) showApp(session.user);
  else showAuth();
});

// COLORS AND MOODS
document.querySelectorAll(".color-dot").forEach(button => {
  button.addEventListener("click", () => {
    document.querySelectorAll(".color-dot").forEach(item => item.classList.remove("selected"));
    button.classList.add("selected");
    selectedColor = button.dataset.color;
  });
});
document.querySelectorAll(".mood-button").forEach(button => {
  button.addEventListener("click", () => {
    document.querySelectorAll(".mood-button").forEach(item => item.classList.remove("selected"));
    button.classList.add("selected");
    selectedMood = button.dataset.mood;
  });
});

// STORAGE HELPERS
async function uploadMemoryFiles(files, memoryId) {
  const uploaded = [];
  for (const file of files) {
    const path = `${currentUser.id}/${memoryId}/${crypto.randomUUID()}-${safeFileName(file.name)}`;
    const { error } = await supabase.storage.from("memory-files").upload(path, file);
    if (error) throw error;
    uploaded.push({
      name:file.name,
      path,
      type:file.type,
      size:file.size
    });
  }
  return uploaded;
}

async function getMemoryFileUrl(path) {
  const { data, error } = await supabase.storage.from("memory-files").createSignedUrl(path, 3600);
  if (error) throw error;
  return data.signedUrl;
}

// CREATE MEMORY
$("memoryForm").addEventListener("submit", async (event) => {
  event.preventDefault();
  if (!currentUser) return;
  status("memoryStatus", "Сохраняем воспоминание...");
  const memoryId = crypto.randomUUID();
  const files = Array.from($("memoryFiles").files || []);
  let uploadedFiles = [];

  try {
    if (files.length) uploadedFiles = await uploadMemoryFiles(files, memoryId);
    const memory = {
      id:memoryId,
      user_id:currentUser.id,
      name:$("memoryName").value.trim(),
      color:selectedColor,
      description:$("memoryDescription").value.trim(),
      song_url:$("songUrl").value.trim(),
      song_info:$("songInfo").value.trim(),
      mood:selectedMood,
      weather:$("weather").value.trim(),
      files:uploadedFiles
    };
    const { error } = await supabase.from("memories").insert(memory);
    if (error) throw error;
    $("memoryForm").reset();
    selectedMood = "😊";
    selectedColor = "#8b1824";
    document.querySelectorAll(".mood-button").forEach((item,i) => item.classList.toggle("selected",i===0));
    document.querySelectorAll(".color-dot").forEach((item,i) => item.classList.toggle("selected",i===0));
    status("memoryStatus", "Воспоминание сохранено!");
    await loadMemories();
  } catch (error) {
    status("memoryStatus", error.message || "Не удалось сохранить файл.", true);
  }
});

// LOAD PERSONAL MEMORIES
async function loadMemories() {
  if (!currentUser) return;
  const { data, error } = await supabase
    .from("memories")
    .select("*")
    .eq("user_id",currentUser.id)
    .order("created_at",{ascending:false});

  if (error) {
    $("memoryGrid").innerHTML = `<div class="empty">Ошибка загрузки: ${escapeHTML(error.message)}</div>`;
    return;
  }
  myMemories = data || [];
  $("memoryCount").textContent = myMemories.length;
  $("memoryGrid").innerHTML = myMemories.length
    ? myMemories.map(memory => memoryCard(memory,false)).join("")
    : `<div class="empty">Пока нет воспоминаний. Сохраните свой первый момент.</div>`;
}

function memoryCard(memory, isReceived) {
  const color = escapeHTML(memory.color || "#8b1824");
  return `
    <article class="memory-card">
      <div class="memory-cover" style="--cover:${color}">
        <h3>${escapeHTML(memory.name)}</h3>
      </div>
      <div class="memory-info">
        <div class="memory-meta">${escapeHTML(memory.mood || "")} · ${escapeHTML(memory.weather || "")}</div>
        <p>${escapeHTML((memory.description || "").slice(0,150))}${(memory.description || "").length>150?"…":""}</p>
        ${memory.song_info ? `<p>♫ ${escapeHTML(memory.song_info)}</p>` : ""}
        <div class="memory-meta">${formatDate(memory.created_at)}</div>
        <div class="memory-actions">
          <button class="btn secondary" onclick="openMemory('${memory.id}',${isReceived})">Открыть</button>
          ${!isReceived ? `<button class="btn ghost" onclick="deleteMemory('${memory.id}')">Удалить</button>` : ""}
        </div>
      </div>
    </article>`;
}

async function loadReceivedMemories() {
  if (!currentUser) return;
  const { data:shares, error } = await supabase
    .from("memory_shares")
    .select("memory_id")
    .eq("shared_with",currentUser.id);

  if (error) {
    $("receivedGrid").innerHTML = `<div class="empty">Не удалось загрузить: ${escapeHTML(error.message)}</div>`;
    return;
  }
  const ids = (shares || []).map(item => item.memory_id);
  $("sharedCount").textContent = ids.length;
  if (!ids.length) {
    receivedMemories = [];
    $("receivedGrid").innerHTML = `<div class="empty">Пока никто не поделился с вами воспоминаниями.</div>`;
    return;
  }
  const { data, error:memoryError } = await supabase
    .from("memories").select("*").in("id",ids).order("created_at",{ascending:false});
  if (memoryError) {
    $("receivedGrid").innerHTML = `<div class="empty">Ошибка: ${escapeHTML(memoryError.message)}</div>`;
    return;
  }
  receivedMemories = data || [];
  $("receivedGrid").innerHTML = receivedMemories.length
    ? receivedMemories.map(memory => memoryCard(memory,true)).join("")
    : `<div class="empty">Нет доступных воспоминаний.</div>`;
}

// OPEN MEMORY
async function openMemory(id,isReceived=false) {
  const memory = [...myMemories,...receivedMemories].find(item => item.id===id);
  if (!memory) return;
  $("modalTitle").textContent = memory.name;
  let filesHTML = "";
  for (const file of memory.files || []) {
    try {
      const url = await getMemoryFileUrl(file.path);
      filesHTML += `<p><a href="${url}" target="_blank" rel="noopener">${escapeHTML(file.name)}</a></p>`;
    } catch {}
  }
  $("modalBody").innerHTML = `
    <div class="memory-meta">${escapeHTML(memory.mood || "")} · ${escapeHTML(memory.weather || "")}</div>
    <p style="line-height:1.8;white-space:pre-wrap">${escapeHTML(memory.description || "Без описания")}</p>
    ${memory.song_info ? `<p>♫ ${escapeHTML(memory.song_info)}</p>` : ""}
    ${memory.song_url ? `<p><a href="${escapeHTML(memory.song_url)}" target="_blank" rel="noopener">Открыть песню ↗</a></p>` : ""}
    <div>${filesHTML}</div>
    <p class="memory-meta">${formatDate(memory.created_at)}</p>`;
  $("memoryModal").classList.remove("hidden");
}

$("closeModalButton").addEventListener("click", () => $("memoryModal").classList.add("hidden"));
$("memoryModal").addEventListener("click", event => {
  if (event.target.id==="memoryModal") $("memoryModal").classList.add("hidden");
});

async function deleteMemory(id) {
  if (!confirm("Удалить это воспоминание?")) return;
  const memory = myMemories.find(item => item.id===id);
  if (memory?.files?.length) {
    await supabase.storage.from("memory-files").remove(memory.files.map(file=>file.path));
  }
  const { error } = await supabase.from("memories").delete().eq("id",id).eq("user_id",currentUser.id);
  if (error) alert(error.message);
  else await loadMemories();
}

// SHARE PERSONAL MEMORY
$("shareButton").addEventListener("click", async () => {
  const email = $("shareEmail").value.trim();
  if (!email) return status("shareStatus","Введите электронную почту.",true);
  const memoryName = prompt("Введите название воспоминания, которым хотите поделиться:");
  if (!memoryName) return;
  const memory = myMemories.find(item => item.name.toLowerCase()===memoryName.trim().toLowerCase());
  if (!memory) return status("shareStatus","Воспоминание с таким названием не найдено.",true);
  status("shareStatus","Отправляем доступ...");
  const { error } = await supabase.rpc("share_memory_with_email",{
    p_memory_id:memory.id,
    p_email:email
  });
  if (error) status("shareStatus",error.message,true);
  else {
    status("shareStatus","Доступ предоставлен!");
    $("shareEmail").value="";
    await loadReceivedMemories();
  }
});

// SHARED FOLDERS
async function loadSharedFolders() {
  if (!currentUser) return;
  const { data, error } = await supabase
    .from("shared_folders")
    .select("*")
    .order("created_at",{ascending:false});
  if (error) {
    $("sharedFolderList").innerHTML = `<div class="empty">Ошибка: ${escapeHTML(error.message)}</div>`;
    return;
  }
  sharedFolders = data || [];
  renderSharedFolderList();
}

function renderSharedFolderList() {
  $("sharedFolderList").innerHTML = sharedFolders.length
    ? sharedFolders.map(folder => `
      <div class="shared-folder-entry ${activeSharedFolder?.id===folder.id?"active":""}" onclick="openSharedFolder('${folder.id}')">
        <div><strong>▣ ${escapeHTML(folder.name)}</strong><small>${folder.owner_id===currentUser.id?"Ваша папка":"Общая папка"}</small></div>
        <span>↗</span>
      </div>`).join("")
    : `<div class="empty">У вас пока нет общих папок.</div>`;
}

$("createSharedFolderButton").addEventListener("click",async () => {
  const name = $("newSharedFolderName").value.trim();
  if (!name) return status("sharedFolderCreateStatus","Введите название папки.",true);
  status("sharedFolderCreateStatus","Создаём папку...");
  const { data,error } = await supabase.rpc("create_shared_folder",{p_name:name});
  if (error) return status("sharedFolderCreateStatus",error.message,true);
  $("newSharedFolderName").value="";
  status("sharedFolderCreateStatus","Папка создана!");
  await loadSharedFolders();
  const folderId = typeof data==="string" ? data : data?.id;
  if (folderId) await openSharedFolder(folderId);
});

function extractInviteToken(value) {
  const input = value.trim();
  try {
    const url = new URL(input);
    return url.searchParams.get("invite") || input;
  } catch {
    return input;
  }
}

async function joinSharedFolder(token) {
  const { error } = await supabase.rpc("accept_shared_folder_invite",{p_token:token});
  if (error) throw error;
  await loadSharedFolders();
  status("sharedInviteStatus","Вы присоединились к общей папке!");
  $("sharedInviteInput").value="";
}

$("joinSharedFolderButton").addEventListener("click",async () => {
  const token = extractInviteToken($("sharedInviteInput").value);
  if (!token) return status("sharedInviteStatus","Вставьте ссылку или код приглашения.",true);
  status("sharedInviteStatus","Проверяем приглашение...");
  try { await joinSharedFolder(token); }
  catch(error) { status("sharedInviteStatus",error.message,true); }
});

async function handlePendingSharedInvite() {
  const params = new URLSearchParams(location.search);
  const token = params.get("invite");
  if (!token || !currentUser) return;
  try {
    await joinSharedFolder(token);
    params.delete("invite");
    const newUrl = location.pathname + (params.toString() ? "?"+params.toString() : "");
    history.replaceState({}, "", newUrl);
  } catch(error) {
    status("sharedInviteStatus",error.message,true);
  }
}

async function openSharedFolder(folderId) {
  const folder = sharedFolders.find(item=>item.id===folderId);
  if (!folder) return;
  activeSharedFolder = folder;
  sharedFolderPath = [];
  $("activeSharedFolderTitle").textContent = folder.name;
  $("activeSharedFolderDescription").textContent = "Общее пространство участников.";
  $("sharedFolderWorkspace").classList.remove("hidden");
  $("sharedFolderInviteArea").classList.toggle("hidden",folder.owner_id!==currentUser.id);
  $("sharedInviteLinkArea").classList.add("hidden");
  renderSharedFolderList();
  await loadSharedFolderMembers();
  await loadSharedFolderItems();
}

async function loadSharedFolderMembers() {
  if (!activeSharedFolder) return;
  const { data,error } = await supabase
    .from("shared_folder_members")
    .select("*")
    .eq("folder_id",activeSharedFolder.id);
  if (error) {
    $("sharedFolderMembers").textContent = "Не удалось загрузить участников: "+error.message;
    return;
  }
  sharedFolderMembers = data || [];
  $("sharedFolderMembers").textContent =
    `Участников: ${sharedFolderMembers.length}/4 · ` +
    sharedFolderMembers.map(member => `${member.role==="owner"?"Владелец":"Участник"} (${member.user_id.slice(0,8)}…)`).join(" · ");
}

async function createSharedInvite() {
  if (!activeSharedFolder) return;
  status("sharedFolderInviteStatus","Создаём ссылку...");
  const { data,error } = await supabase.rpc("create_shared_folder_invite",{
    p_folder_id:activeSharedFolder.id
  });
  if (error) return status("sharedFolderInviteStatus",error.message,true);
  const token = typeof data==="string" ? data : data?.token;
  if (!token) return status("sharedFolderInviteStatus","Сервер не вернул код приглашения.",true);
  const link = `${location.origin}${location.pathname}?invite=${encodeURIComponent(token)}`;
  $("sharedInviteLink").value=link;
  $("sharedInviteLinkArea").classList.remove("hidden");
  status("sharedFolderInviteStatus","Ссылка готова. Она действует 7 дней.");
}

$("createSharedInviteButton").addEventListener("click",createSharedInvite);
$("copySharedInviteButton").addEventListener("click",async () => {
  try {
    await navigator.clipboard.writeText($("sharedInviteLink").value);
    status("sharedFolderInviteStatus","Ссылка скопирована!");
  } catch {
    $("sharedInviteLink").select();
    document.execCommand("copy");
    status("sharedFolderInviteStatus","Ссылка скопирована!");
  }
});

async function loadSharedFolderItems() {
  if (!activeSharedFolder) return;
  const { data,error } = await supabase
    .from("shared_folder_items")
    .select("*")
    .eq("folder_id",activeSharedFolder.id)
    .order("created_at",{ascending:true});
  if (error) {
    status("sharedFolderStatus",error.message,true);
    return;
  }
  sharedFolderItems = data || [];
  renderSharedFolderItems();
}

function currentSharedParent() {
  return sharedFolderPath.length ? sharedFolderPath[sharedFolderPath.length-1].id : null;
}

function renderSharedFolderItems() {
  const parent = currentSharedParent();
  const items = sharedFolderItems.filter(item=>item.parent_id===parent);
  const pathNames = [activeSharedFolder.name,...sharedFolderPath.map(item=>item.name)];
  $("sharedFolderBreadcrumb").textContent = pathNames.join(" / ");
  $("sharedBackButton").disabled = sharedFolderPath.length===0;
  $("sharedBackButton").style.opacity = sharedFolderPath.length===0 ? ".4" : "1";

  $("sharedFolderItems").innerHTML = items.length ? items.map(item => {
    const icon = item.item_type==="folder" ? "▣" : item.item_type==="note" ? "✎" : "↗";
    return `
      <div class="shared-item">
        <strong>${icon} ${escapeHTML(item.name)}</strong>
        <small>${item.item_type==="folder"?"Папка":item.item_type==="note"?"Заметка":"Файл"} · ${formatDate(item.created_at)}</small>
        ${item.item_type==="note" ? `<p>${escapeHTML(item.content || "")}</p>` : ""}
        <div class="shared-item-actions">
          ${item.item_type==="folder" ? `<button class="btn secondary" onclick="enterSharedSubfolder('${item.id}')">Открыть</button>` : ""}
          ${item.item_type==="file" ? `<button class="btn secondary" onclick="openSharedFile('${item.id}')">Открыть файл</button>` : ""}
          ${item.item_type==="note" ? `<button class="btn secondary" onclick="editSharedNote('${item.id}')">Изменить</button>` : ""}
          <button class="btn ghost" onclick="deleteSharedItem('${item.id}')">Удалить</button>
        </div>
      </div>`;
  }).join("") : `<div class="empty">В этой папке пока ничего нет.</div>`;
}

function enterSharedSubfolder(id) {
  const folder = sharedFolderItems.find(item=>item.id===id && item.item_type==="folder");
  if (!folder) return;
  sharedFolderPath.push(folder);
  renderSharedFolderItems();
}

$("sharedBackButton").addEventListener("click",() => {
  if (sharedFolderPath.length) {
    sharedFolderPath.pop();
    renderSharedFolderItems();
  }
});

$("newSharedSubfolderButton").addEventListener("click",async () => {
  const name = prompt("Название новой папки:");
  if (!name?.trim()) return;
  const { error } = await supabase.from("shared_folder_items").insert({
    folder_id:activeSharedFolder.id,
    parent_id:currentSharedParent(),
    item_type:"folder",
    name:name.trim(),
    created_by:currentUser.id
  });
  if (error) status("sharedFolderStatus",error.message,true);
  else {
    status("sharedFolderStatus","Папка создана!");
    await loadSharedFolderItems();
  }
});

$("newSharedNoteButton").addEventListener("click",async () => {
  const name = prompt("Название заметки:");
  if (!name?.trim()) return;
  const content = prompt("Текст заметки:") || "";
  const { error } = await supabase.from("shared_folder_items").insert({
    folder_id:activeSharedFolder.id,
    parent_id:currentSharedParent(),
    item_type:"note",
    name:name.trim(),
    content,
    created_by:currentUser.id
  });
  if (error) status("sharedFolderStatus",error.message,true);
  else {
    status("sharedFolderStatus","Заметка добавлена!");
    await loadSharedFolderItems();
  }
});

async function editSharedNote(id) {
  const item = sharedFolderItems.find(entry=>entry.id===id);
  if (!item) return;
  const content = prompt("Изменить текст заметки:",item.content || "");
  if (content===null) return;
  const { error } = await supabase.from("shared_folder_items")
    .update({content,updated_at:new Date().toISOString()})
    .eq("id",id);
  if (error) status("sharedFolderStatus",error.message,true);
  else await loadSharedFolderItems();
}

$("uploadSharedFilesButton").addEventListener("click",()=>$("sharedFilesInput").click());

$("sharedFilesInput").addEventListener("change",async event => {
  const files = Array.from(event.target.files || []);
  if (!files.length || !activeSharedFolder) return;
  status("sharedFolderStatus","Загружаем файлы...");
  for (const file of files) {
    const itemId = crypto.randomUUID();
    const path = `${activeSharedFolder.id}/${itemId}/${crypto.randomUUID()}-${safeFileName(file.name)}`;
    const { error:uploadError } = await supabase.storage
      .from("shared-folder-files").upload(path,file);
    if (uploadError) {
      status("sharedFolderStatus",uploadError.message,true);
      continue;
    }
    const { error:insertError } = await supabase.from("shared_folder_items").insert({
      id:itemId,
      folder_id:activeSharedFolder.id,
      parent_id:currentSharedParent(),
      item_type:"file",
      name:file.name,
      storage_path:path,
      mime_type:file.type,
      size_bytes:file.size,
      created_by:currentUser.id
    });
    if (insertError) {
      await supabase.storage.from("shared-folder-files").remove([path]);
      status("sharedFolderStatus",insertError.message,true);
    }
  }
  event.target.value="";
  await loadSharedFolderItems();
  status("sharedFolderStatus","Загрузка завершена.");
});

async function openSharedFile(id) {
  const item = sharedFolderItems.find(entry=>entry.id===id);
  if (!item?.storage_path) return;
  const { data,error } = await supabase.storage
    .from("shared-folder-files").createSignedUrl(item.storage_path,3600);
  if (error) return status("sharedFolderStatus",error.message,true);
  window.open(data.signedUrl,"_blank","noopener");
}

async function deleteSharedItem(id) {
  const item = sharedFolderItems.find(entry=>entry.id===id);
  if (!item || !confirm(`Удалить «${item.name}»?`)) return;
  const idsToDelete = new Set([id]);
  if (item.item_type==="folder") {
    let changed = true;
    while (changed) {
      changed = false;
      for (const child of sharedFolderItems) {
        if (child.parent_id && idsToDelete.has(child.parent_id) && !idsToDelete.has(child.id)) {
          idsToDelete.add(child.id);
          changed = true;
        }
      }
    }
  }
  const descendants = sharedFolderItems.filter(entry=>idsToDelete.has(entry.id));
  const paths = descendants.map(entry=>entry.storage_path).filter(Boolean);
  if (paths.length) {
    const { error:storageError } = await supabase.storage.from("shared-folder-files").remove(paths);
    if (storageError) return status("sharedFolderStatus",storageError.message,true);
  }
  const { error } = await supabase.from("shared_folder_items").delete().eq("id",id);
  if (error) status("sharedFolderStatus",error.message,true);
  else {
    status("sharedFolderStatus","Материал удалён.");
    await loadSharedFolderItems();
  }
}

// INITIAL SESSION CHECK
(async () => {
  const { data } = await supabase.auth.getSession();
  if (data.session?.user) await showApp(data.session.user);
  else await showAuth();
})();
</script>
</body>
</html>
