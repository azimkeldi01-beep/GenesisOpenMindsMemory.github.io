
<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Genesis — Open Minds Memory</title>
<script src="https://cdn.jsdelivr.net/npm/@supabase/supabase-js@2"></script>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&display=swap" rel="stylesheet">

<style>
:root {
  --primary:#4263eb;
  --primary-dark:#304fc5;
  --lime:#c8f169;
  --bg:#f5f7fb;
  --surface:#fff;
  --text:#182238;
  --muted:#8490a5;
  --border:#e8edf4;
  --radius:18px;
  --shadow:0 8px 30px rgba(35,55,90,.06);
}
*{box-sizing:border-box}
body{
  margin:0;background:var(--bg);color:var(--text);
  font-family:Inter,Arial,sans-serif;
  min-height:100vh;
}
button,input,textarea,select{font:inherit}
button{cursor:pointer}
button:disabled{opacity:.5;cursor:not-allowed}
.hidden{display:none!important}
.container{width:min(1180px,calc(100% - 40px));margin:auto}
header{
  background:rgba(255,255,255,.9);border-bottom:1px solid var(--border);
  position:sticky;top:0;z-index:10;backdrop-filter:blur(14px);
}
.nav{
  min-height:76px;display:flex;align-items:center;
  justify-content:space-between;gap:15px;
}
.brand{display:flex;align-items:center;gap:11px;font-weight:800;font-size:19px}
.brand-icon{
  width:39px;height:39px;border-radius:13px;background:var(--primary);
  color:white;display:grid;place-items:center;font-size:21px;
}
.brand small{display:block;color:var(--muted);font-size:9px;letter-spacing:2px;margin-top:3px}
.nav-right{display:flex;align-items:center;gap:12px}
.user-email{font-size:12px;color:var(--muted);max-width:180px;overflow:hidden;text-overflow:ellipsis}
main{padding:38px 0 70px}
.hero{
  background:linear-gradient(120deg,#3456d9,#5477f4);
  color:white;border-radius:25px;padding:38px 42px;
  position:relative;overflow:hidden;margin-bottom:30px;
}
.hero:after{
  content:"✦";position:absolute;right:8%;top:-60px;
  font-size:240px;color:rgba(255,255,255,.08);
}
.eyebrow{font-size:10px;letter-spacing:2px;font-weight:800;opacity:.75}
.hero h1{font-size:clamp(28px,4vw,43px);margin:15px 0 10px;max-width:650px}
.hero p{color:#e2e9ff;line-height:1.7;max-width:550px;font-size:14px}
.hero-tag{
  display:inline-block;background:var(--lime);color:#26351b;
  padding:9px 13px;border-radius:9px;font-size:11px;font-weight:800;margin-top:8px;
}
.section{margin-top:34px}
.section-head{display:flex;align-items:end;justify-content:space-between;gap:15px;margin-bottom:18px}
.section-head h2{font-size:23px;margin:8px 0 5px}
.section-head p{color:var(--muted);font-size:12px;margin:0;line-height:1.6}
.card{
  background:var(--surface);border:1px solid var(--border);
  border-radius:var(--radius);padding:23px;box-shadow:var(--shadow);
}
.layout{display:grid;grid-template-columns:minmax(0,1.1fr) minmax(280px,.9fr);gap:22px}
label{display:block;font-size:12px;font-weight:700;margin:17px 0 8px}
input,textarea,select{
  width:100%;border:1px solid var(--border);border-radius:11px;
  padding:13px 14px;background:#fbfcfe;color:var(--text);outline:none;
  transition:.2s;
}
input:focus,textarea:focus,select:focus{border-color:var(--primary);box-shadow:0 0 0 3px #4263eb15}
textarea{resize:vertical;min-height:100px}
input[type=file]{padding:10px}
.btn{
  border:0;border-radius:11px;padding:12px 17px;
  font-size:12px;font-weight:700;transition:.2s;
}
.btn:hover{transform:translateY(-1px)}
.primary{background:var(--primary);color:white}
.primary:hover{background:var(--primary-dark)}
.secondary{background:#edf1ff;color:var(--primary)}
.danger{background:#fff0f0;color:#d84c4c}
.ghost{background:#f2f4f8;color:#536078}
.full{width:100%;margin-top:17px}
.actions{display:flex;gap:9px;flex-wrap:wrap;margin-top:18px}
.colors{display:flex;gap:10px;flex-wrap:wrap}
.color{
  width:29px;height:29px;border-radius:50%;border:3px solid white;
  outline:1px solid var(--border);cursor:pointer;
}
.color.active{outline:2px solid var(--primary)}
.mood-row{display:flex;gap:9px;flex-wrap:wrap}
.mood{
  border:1px solid var(--border);background:white;border-radius:10px;
  padding:9px 12px;font-size:17px;
}
.mood.active{background:#edf1ff;border-color:var(--primary)}
.grid{
  display:grid;grid-template-columns:repeat(3,minmax(0,1fr));gap:16px;
}
.memory-card{
  border:1px solid var(--border);border-radius:17px;background:white;
  padding:19px;cursor:pointer;transition:.2s;min-width:0;
}
.memory-card:hover{transform:translateY(-3px);box-shadow:var(--shadow);border-color:#c9d4ff}
.memory-top{display:flex;justify-content:space-between;align-items:center;gap:10px}
.memory-dot{width:11px;height:11px;border-radius:50%;flex-shrink:0}
.memory-card h3{font-size:16px;margin:16px 0 8px;overflow-wrap:anywhere}
.memory-card p{font-size:12px;color:var(--muted);line-height:1.6;margin:0;overflow-wrap:anywhere}
.memory-date{font-size:10px;color:var(--muted);margin-top:16px}
.pill{
  display:inline-block;padding:5px 8px;border-radius:6px;
  background:#edf1ff;color:var(--primary);font-size:9px;font-weight:800;
}
.empty{
  grid-column:1/-1;text-align:center;color:var(--muted);
  padding:35px 15px;font-size:13px;border:1px dashed #d8deea;border-radius:15px;
}
.share-panel{margin-top:25px;padding-top:20px;border-top:1px solid var(--border)}
.share-list{display:grid;gap:9px;margin-top:12px}
.share-item{
  display:flex;align-items:center;justify-content:space-between;gap:10px;
  padding:10px;background:#f5f7f8;border-radius:9px;font-size:11px;
  overflow-wrap:anywhere;
}
.file-list{display:grid;gap:8px;margin-top:12px}
.file-item{font-size:11px;padding:10px;background:#f5f7fa;border-radius:9px;overflow-wrap:anywhere}
.file-item a{color:var(--primary);text-decoration:none}
.shared-label{
  display:inline-block;margin-top:7px;padding:4px 8px;
  background:#e9eef2;color:var(--primary);border-radius:5px;
  font-size:10px;font-weight:700;
}
footer{border-top:1px solid var(--border);padding:25px 0;color:var(--muted);font-size:11px;text-align:center}
.modal{
  position:fixed;inset:0;background:#111827a8;z-index:30;
  display:flex;align-items:center;justify-content:center;padding:18px;
}
.modal-box{
  background:white;width:min(650px,100%);max-height:90vh;overflow:auto;
  border-radius:20px;padding:25px;
}
.modal-head{display:flex;justify-content:space-between;gap:12px;align-items:center}
.modal-head h2{font-size:21px;margin:0}
.media-grid{display:grid;grid-template-columns:repeat(2,minmax(0,1fr));gap:10px;margin-top:18px}
.media-grid img,.media-grid video{
  width:100%;max-height:260px;object-fit:contain;background:#f2f4f8;border-radius:12px;
}
.notice{font-size:12px;color:var(--muted);line-height:1.6;margin-top:10px}
.auth-wrap{min-height:100vh;display:grid;place-items:center;padding:20px}
.auth-card{width:min(420px,100%);background:white;border:1px solid var(--border);border-radius:23px;padding:30px;box-shadow:var(--shadow)}
.auth-card h1{font-size:25px;margin:20px 0 8px}
.auth-card p{color:var(--muted);font-size:12px;line-height:1.7}
.auth-switch{text-align:center;font-size:12px;margin-top:20px;color:var(--muted)}
.auth-switch a{color:var(--primary);font-weight:700;cursor:pointer}
.status{font-size:12px;line-height:1.5;margin-top:12px;color:var(--primary);min-height:18px}
@media(max-width:850px){
  .layout{grid-template-columns:1fr}
  .grid{grid-template-columns:repeat(2,minmax(0,1fr))}
}
@media(max-width:560px){
  .container{width:calc(100% - 24px)}
  main{padding:20px 0 45px}
  .nav{min-height:65px}
  .brand{font-size:15px}
  .brand-icon{width:34px;height:34px}
  .user-email{display:none}
  .hero{padding:27px 22px;border-radius:19px}
  .hero h1{font-size:29px}
  .hero p{font-size:12px}
  .section-head h2{font-size:20px}
  .card{padding:17px}
  .grid{grid-template-columns:1fr}
  .section-head{align-items:start;flex-direction:column}
  .actions .btn{flex:1}
  .media-grid{grid-template-columns:1fr}
  .modal-box{padding:19px}
}
</style>
</head>

<body>

<!-- AUTH -->
<div id="authScreen" class="auth-wrap">
  <div class="auth-card">
    <div class="brand">
      <div class="brand-icon">✦</div>
      <div>GENESIS<small>OPEN MINDS MEMORY</small></div>
    </div>
    <h1 id="authTitle">Добро пожаловать</h1>
    <p id="authDescription">Сохраняйте важные моменты своей жизни в одном месте.</p>
    <form id="authForm">
      <label>Электронная почта</label>
      <input id="authEmail" type="email" placeholder="name@example.com" required>
      <label>Пароль</label>
      <input id="authPassword" type="password" placeholder="Минимум 6 символов" minlength="6" required>
      <button id="authButton" class="btn primary full" type="submit">Войти</button>
    </form>
    <div id="authStatus" class="status"></div>
    <div class="auth-switch">
      <span id="switchText">Нет аккаунта?</span>
      <a id="switchAuth">Зарегистрироваться</a>
    </div>
  </div>
</div>

<!-- APPLICATION -->
<div id="appScreen" class="hidden">
<header>
  <div class="container nav">
    <div class="brand">
      <div class="brand-icon">✦</div>
      <div>GENESIS<small>OPEN MINDS MEMORY</small></div>
    </div>
    <div class="nav-right">
      <span id="userEmail" class="user-email"></span>
      <button class="btn ghost" id="logoutButton">Выйти</button>
    </div>
  </div>
</header>

<main class="container">
  <section class="hero">
    <div class="eyebrow">YOUR PERSONAL MEMORY SPACE</div>
    <h1>Каждый момент<br>заслуживает памяти.</h1>
    <p>Создавайте собственную коллекцию воспоминаний, сохраняйте фотографии и делитесь важными моментами с близкими.</p>
    <span class="hero-tag">✦ YOUR STORY. YOUR SPACE.</span>
  </section>

  <section class="layout">
    <div class="card">
      <div class="eyebrow" style="color:var(--primary)">01 / MEMORY EDITOR</div>
      <h2 style="font-size:21px;margin:9px 0">Создать воспоминание</h2>
      <p class="notice">Заполните информацию о моменте, который хотите сохранить.</p>

      <form id="memoryForm">
        <label>Название</label>
        <input id="memoryName" maxlength="100" placeholder="Например, летний вечер..." required>

        <label>Описание</label>
        <textarea id="memoryDescription" maxlength="5000" placeholder="Что произошло? Почему это важно?"></textarea>

        <label>Настроение</label>
        <div class="mood-row" id="moodRow">
          <button type="button" class="mood active" data-mood="😊">😊</button>
          <button type="button" class="mood" data-mood="❤️">❤️</button>
          <button type="button" class="mood" data-mood="🥹">🥹</button>
          <button type="button" class="mood" data-mood="✨">✨</button>
          <button type="button" class="mood" data-mood="🌧️">🌧️</button>
          <button type="button" class="mood" data-mood="🎉">🎉</button>
        </div>

        <label>Цвет карточки</label>
        <div class="colors" id="colors">
          <button type="button" class="color active" data-color="#4263eb" style="background:#4263eb"></button>
          <button type="button" class="color" data-color="#e879a9" style="background:#e879a9"></button>
          <button type="button" class="color" data-color="#e6a23c" style="background:#e6a23c"></button>
          <button type="button" class="color" data-color="#42a98b" style="background:#42a98b"></button>
          <button type="button" class="color" data-color="#9b79dc" style="background:#9b79dc"></button>
          <button type="button" class="color" data-color="#344054" style="background:#344054"></button>
        </div>

        <label>Музыка или ссылка (необязательно)</label>
        <input id="songUrl" type="url" placeholder="https://...">
        <input id="songInfo" placeholder="Название песни или исполнителя">

        <label>Фотографии и видео</label>
        <input id="memoryFiles" type="file" multiple accept="image/*,video/*">
        <div id="selectedFiles" class="notice">Файлы пока не выбраны.</div>
        <div id="existingFiles" class="file-list"></div>

        <div class="actions">
          <button type="submit" class="btn primary" id="saveButton">Сохранить воспоминание</button>
          <button type="button" class="btn ghost" id="newButton">Новое</button>
          <button type="button" class="btn danger" id="deleteButton" disabled>Удалить</button>
        </div>
      </form>

      <div id="memoryStatus" class="status"></div>

      <div class="share-panel" id="sharePanel">
        <h3 style="font-size:15px">Совместный доступ</h3>
        <p class="notice">Поделитесь воспоминанием с зарегистрированным пользователем. Он сможет просматривать его, но не редактировать.</p>
        <label for="shareEmail">Электронная почта получателя</label>
        <input id="shareEmail" type="email" placeholder="friend@example.com">
        <button class="btn secondary full" type="button" id="shareButton">Поделиться воспоминанием</button>
        <div id="shareList" class="share-list"></div>
        <div id="shareStatus" class="status"></div>
      </div>
    </div>

    <div class="card">
      <div class="eyebrow" style="color:var(--primary)">02 / YOUR COLLECTION</div>
      <h2 style="font-size:21px;margin:9px 0">Мои воспоминания</h2>
      <p class="notice">Все моменты, которые вы сохранили.</p>
      <div id="myMemoryGrid" class="grid" style="grid-template-columns:1fr;margin-top:18px">
        <div class="empty">Загрузка...</div>
      </div>
    </div>
  </section>

  <section class="section">
    <div class="section-head">
      <div>
        <div class="eyebrow" style="color:var(--primary)">03 / SHARED MEMORIES</div>
        <h2>Со мной поделились</h2>
        <p>Воспоминания, которыми поделились другие пользователи.</p>
      </div>
    </div>
    <div id="sharedArchiveGrid" class="grid">
      <div class="empty">Загрузка...</div>
    </div>
  </section>
</main>

<footer>GENESIS OPEN MINDS MEMORY · YOUR STORY MATTERS</footer>
</div>

<!-- VIEW MODAL -->
<div id="viewModal" class="modal hidden">
  <div class="modal-box">
    <div class="modal-head">
      <h2 id="viewTitle"></h2>
      <button class="btn ghost" id="closeModal">Закрыть ✕</button>
    </div>
    <div id="viewMeta" class="notice"></div>
    <p id="viewDescription" style="font-size:14px;line-height:1.8;white-space:pre-wrap"></p>
    <div id="viewSong"></div>
    <div id="viewFiles" class="media-grid"></div>
    <p id="viewSharedNote" class="notice"></p>
  </div>
</div>

<script>
const SUPABASE_URL = "https://ydrzlazhucdlvvyjisnm.supabase.co";
const SUPABASE_KEY = "sb_publishable_l_aik6ePDy4GFPZRwBH1ZQ_9oSb_Dji";
const supabaseClient = window.supabase.createClient(SUPABASE_URL, SUPABASE_KEY);

const $ = selector => document.querySelector(selector);

let currentUser = null;
let folders = [];
let sharedMemories = [];
let myShares = [];
let currentId = null;
let currentFiles = [];
let selectedColor = "#4263eb";
let selectedMood = "😊";
let authMode = "login";

const BUCKET = "memory-files";

function escapeHTML(value="") {
  return String(value).replace(/[&<>"']/g, char => ({
    "&":"&amp;","<":"&lt;",">":"&gt;",'"':"&quot;","'":"&#039;"
  })[char]);
}

function status(element,message,isError=false) {
  element.textContent = message;
  element.style.color = isError ? "#d84c4c" : "#4263eb";
}

function setAuthMode(mode) {
  authMode = mode;
  const register = mode === "register";
  $("#authTitle").textContent = register ? "Создать аккаунт" : "Добро пожаловать";
  $("#authDescription").textContent = register
    ? "Зарегистрируйтесь, чтобы начать сохранять свои воспоминания."
    : "Сохраняйте важные моменты своей жизни в одном месте.";
  $("#authButton").textContent = register ? "Зарегистрироваться" : "Войти";
  $("#switchText").textContent = register ? "Уже есть аккаунт?" : "Нет аккаунта?";
  $("#switchAuth").textContent = register ? "Войти" : "Зарегистрироваться";
  $("#authStatus").textContent = "";
}

$("#switchAuth").addEventListener("click", () => {
  setAuthMode(authMode === "login" ? "register" : "login");
});

$("#authForm").addEventListener("submit", async event => {
  event.preventDefault();
  const email = $("#authEmail").value.trim();
  const password = $("#authPassword").value;
  const button = $("#authButton");
  button.disabled = true;
  status($("#authStatus"),"Подождите...");

  try {
    let result;
    if (authMode === "register") {
      result = await supabaseClient.auth.signUp({email,password});
    } else {
      result = await supabaseClient.auth.signInWithPassword({email,password});
    }
    if (result.error) throw result.error;

    if (authMode === "register" && !result.data.session) {
      status($("#authStatus"),"Аккаунт создан! Проверьте почту и подтвердите регистрацию.");
    } else {
      status($("#authStatus"),"Успешно!");
    }
  } catch(error) {
    status($("#authStatus"),error.message || "Ошибка авторизации",true);
  } finally {
    button.disabled = false;
  }
});

function showApp(user) {
  currentUser = user;
  $("#authScreen").classList.add("hidden");
  $("#appScreen").classList.remove("hidden");
  $("#userEmail").textContent = user.email || "";
  loadMemories();
}

function showAuth() {
  currentUser = null;
  folders = [];
  sharedMemories = [];
  myShares = [];
  currentId = null;
  currentFiles = [];
  $("#appScreen").classList.add("hidden");
  $("#authScreen").classList.remove("hidden");
  resetForm();
}

$("#logoutButton").addEventListener("click", async () => {
  const {error} = await supabaseClient.auth.signOut();
  if (error) alert(error.message);
});

supabaseClient.auth.onAuthStateChange((event,session) => {
  if (session?.user) {
    showApp(session.user);
  } else {
    showAuth();
  }
});

async function loadMemories() {
  if (!currentUser) return;

  status($("#memoryStatus"),"Загружаем воспоминания...");

  const {data,error} = await supabaseClient
    .from("memories")
    .select("*")
    .order("created_at",{ascending:false});

  if (error) {
    status($("#memoryStatus"),error.message,true);
    return;
  }

  const allVisible = data || [];
  folders = allVisible.filter(memory => memory.user_id === currentUser.id);

  const {data:receivedShares,error:receivedError} = await supabaseClient
    .from("memory_shares")
    .select("memory_id,owner_id,created_at")
    .eq("shared_with",currentUser.id);

  if (receivedError) {
    status($("#memoryStatus"),receivedError.message,true);
    return;
  }

  const sharedIds = (receivedShares || []).map(item => item.memory_id);
  if (sharedIds.length) {
    const {data:sharedData,error:sharedError} = await supabaseClient
      .from("memories")
      .select("*")
      .in("id",sharedIds);

    if (sharedError) {
      status($("#memoryStatus"),sharedError.message,true);
      return;
    }
    sharedMemories = (sharedData || []).map(memory => ({...memory,isShared:true}));
  } else {
    sharedMemories = [];
  }

  renderFolders();
  renderSharedArchive();

  if (currentId) {
    const selected = folders.find(item => item.id === currentId);
    if (selected) openFolder(selected.id);
    else resetForm();
  }
  status($("#memoryStatus"),"Воспоминания загружены.");
}

function renderFolders() {
  const grid = $("#myMemoryGrid");
  if (!folders.length) {
    grid.innerHTML = '<div class="empty">Пока нет воспоминаний. Создайте первое!</div>';
    return;
  }

  grid.innerHTML = folders.map(memory => `
    <article class="memory-card" data-memory="${escapeHTML(memory.id)}">
      <div class="memory-top">
        <span class="memory-dot" style="background:${escapeHTML(memory.color || "#4263eb")}"></span>
        <span class="pill">${escapeHTML(memory.mood || "✦")}</span>
      </div>
      <h3>${escapeHTML(memory.name)}</h3>
      <p>${escapeHTML((memory.description || "Без описания").slice(0,110))}</p>
      <div class="memory-date">${new Date(memory.created_at).toLocaleDateString("ru-RU")}</div>
    </article>
  `).join("");
}

function renderSharedArchive() {
  const grid = $("#sharedArchiveGrid");
  if (!sharedMemories.length) {
    grid.innerHTML = '<div class="empty">Пока с вами никто не поделился воспоминаниями.</div>';
    return;
  }

  grid.innerHTML = sharedMemories.map(memory => `
    <article class="memory-card" data-shared-memory="${escapeHTML(memory.id)}">
      <div class="memory-top">
        <span class="memory-dot" style="background:${escapeHTML(memory.color || "#4263eb")}"></span>
        <span class="pill">Доступно вам</span>
      </div>
      <h3>${escapeHTML(memory.name)}</h3>
      <p>${escapeHTML((memory.description || "Без описания").slice(0,110))}</p>
      <div class="memory-date">${new Date(memory.created_at).toLocaleDateString("ru-RU")}</div>
      <span class="shared-label">Только просмотр</span>
    </article>
  `).join("");
}

$("#myMemoryGrid").addEventListener("click",event => {
  const card = event.target.closest("[data-memory]");
  if (card) openFolder(card.dataset.memory);
});

$("#sharedArchiveGrid").addEventListener("click",event => {
  const card = event.target.closest("[data-shared-memory]");
  if (!card) return;
  const memory = sharedMemories.find(item => item.id === card.dataset.sharedMemory);
  if (memory) showMemory(memory);
});

function openFolder(id) {
  const memory = folders.find(item => item.id === id);
  if (!memory) return;

  currentId = id;
  currentFiles = Array.isArray(memory.files) ? memory.files : [];
  $("#memoryName").value = memory.name || "";
  $("#memoryDescription").value = memory.description || "";
  $("#songUrl").value = memory.song_url || "";
  $("#songInfo").value = memory.song_info || "";
  selectedColor = memory.color || "#4263eb";
  selectedMood = memory.mood || "😊";

  updateColorSelection();
  updateMoodSelection();
  renderExistingFiles();
  $("#deleteButton").disabled = false;
  $("#saveButton").textContent = "Сохранить изменения";
  $("#shareEmail").value = "";
  $("#shareStatus").textContent = "";
  loadMyShares();
  window.scrollTo({top:0,behavior:"smooth"});
}

function resetForm() {
  currentId = null;
  currentFiles = [];
  $("#memoryForm").reset();
  $("#selectedFiles").textContent = "Файлы пока не выбраны.";
  $("#existingFiles").innerHTML = "";
  $("#deleteButton").disabled = true;
  $("#saveButton").textContent = "Сохранить воспоминание";
  selectedColor = "#4263eb";
  selectedMood = "😊";
  updateColorSelection();
  updateMoodSelection();
  $("#shareList").innerHTML = "";
  $("#shareStatus").textContent = "";
}

$("#newButton").addEventListener("click",resetForm);

$("#colors").addEventListener("click",event => {
  const button = event.target.closest("[data-color]");
  if (!button) return;
  selectedColor = button.dataset.color;
  updateColorSelection();
});

function updateColorSelection() {
  document.querySelectorAll(".color").forEach(button => {
    button.classList.toggle("active",button.dataset.color === selectedColor);
  });
}

$("#moodRow").addEventListener("click",event => {
  const button = event.target.closest("[data-mood]");
  if (!button) return;
  selectedMood = button.dataset.mood;
  updateMoodSelection();
});

function updateMoodSelection() {
  document.querySelectorAll(".mood").forEach(button => {
    button.classList.toggle("active",button.dataset.mood === selectedMood);
  });
}

$("#memoryFiles").addEventListener("change",() => {
  const files = [...$("#memoryFiles").files];
  $("#selectedFiles").textContent = files.length
    ? "Выбрано файлов: " + files.length
    : "Файлы пока не выбраны.";
});

function renderExistingFiles() {
  $("#existingFiles").innerHTML = currentFiles.map((file,index) => `
    <div class="file-item">
      ${escapeHTML(file.name || "Файл")}
      <button type="button" class="btn danger" style="padding:5px 8px;float:right"
        data-remove-file="${index}">Удалить</button>
    </div>
  `).join("");
}

$("#existingFiles").addEventListener("click",event => {
  const button = event.target.closest("[data-remove-file]");
  if (!button) return;
  currentFiles.splice(Number(button.dataset.removeFile),1);
  renderExistingFiles();
});

async function uploadFiles(files,memoryId) {
  const uploaded = [];

  for (const file of files) {
    const safeName = file.name.replace(/[^a-zA-Z0-9._-]/g,"_");
    const path = `${currentUser.id}/${memoryId}/${crypto.randomUUID()}-${safeName}`;

    const {error} = await supabaseClient.storage
      .from(BUCKET)
      .upload(path,file,{upsert:false,contentType:file.type});

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

$("#memoryForm").addEventListener("submit",async event => {
  event.preventDefault();
  if (!currentUser) return;

  const button = $("#saveButton");
  button.disabled = true;
  status($("#memoryStatus"),"Сохраняем...");

  let uploadedPaths = [];
  let createdId = currentId;

  try {
    const payload = {
      user_id:currentUser.id,
      name:$("#memoryName").value.trim(),
      description:$("#memoryDescription").value.trim(),
      color:selectedColor,
      mood:selectedMood,
      song_url:$("#songUrl").value.trim(),
      song_info:$("#songInfo").value.trim(),
      files:currentFiles
    };

    if (!payload.name) throw new Error("Введите название воспоминания.");

    if (currentId) {
      const {error} = await supabaseClient.from("memories")
        .update(payload)
        .eq("id",currentId)
        .eq("user_id",currentUser.id);
      if (error) throw error;
    } else {
      const {data,error} = await supabaseClient.from("memories")
        .insert(payload)
        .select()
        .single();
      if (error) throw error;
      createdId = data.id;
    }

    const newFiles = [...$("#memoryFiles").files];
    if (newFiles.length) {
      const uploaded = await uploadFiles(newFiles,createdId);
      uploadedPaths = uploaded.map(file => file.path);

      const updatedFiles = [...currentFiles,...uploaded];
      const {error} = await supabaseClient.from("memories")
        .update({files:updatedFiles})
        .eq("id",createdId)
        .eq("user_id",currentUser.id);

      if (error) {
        await supabaseClient.storage.from(BUCKET).remove(uploadedPaths);
        throw error;
      }
      currentFiles = updatedFiles;
    }

    currentId = createdId;
    $("#memoryFiles").value = "";
    $("#selectedFiles").textContent = "Файлы загружены.";
    await loadMemories();
    openFolder(createdId);
    status($("#memoryStatus"),"Воспоминание успешно сохранено!");
  } catch(error) {
    status($("#memoryStatus"),error.message || "Не удалось сохранить воспоминание.",true);
  } finally {
    button.disabled = false;
  }
});

$("#deleteButton").addEventListener("click",async () => {
  if (!currentId || !confirm("Удалить это воспоминание?")) return;

  status($("#memoryStatus"),"Удаляем...");
  $("#deleteButton").disabled = true;

  try {
    const memory = folders.find(item => item.id === currentId);
    const paths = (memory?.files || []).map(file => file.path).filter(Boolean);

    const {error} = await supabaseClient.from("memories")
      .delete()
      .eq("id",currentId)
      .eq("user_id",currentUser.id);

    if (error) throw error;

    if (paths.length) {
      await supabaseClient.storage.from(BUCKET).remove(paths);
    }

    resetForm();
    await loadMemories();
    status($("#memoryStatus"),"Воспоминание удалено.");
  } catch(error) {
    status($("#memoryStatus"),error.message,true);
    $("#deleteButton").disabled = false;
  }
});

async function getFileUrl(path) {
  const {data,error} = await supabaseClient.storage
    .from(BUCKET)
    .createSignedUrl(path,3600);

  if (error) throw error;
  return data.signedUrl;
}

async function showMemory(memory) {
  $("#viewTitle").textContent = memory.name || "Воспоминание";
  $("#viewMeta").textContent =
    `${memory.mood || ""} · ${new Date(memory.created_at).toLocaleDateString("ru-RU")}`;
  $("#viewDescription").textContent = memory.description || "";
  $("#viewSong").innerHTML = memory.song_url
    ? `<p class="notice">🎵 ${escapeHTML(memory.song_info || "Музыка")} · <a href="${escapeHTML(memory.song_url)}" target="_blank" rel="noopener">Открыть ссылку</a></p>`
    : "";

  $("#viewFiles").innerHTML = "";
  $("#viewSharedNote").textContent = memory.isShared
    ? "Это воспоминание доступно только для просмотра."
    : "";

  $("#viewModal").classList.remove("hidden");

  for (const file of (memory.files || [])) {
    if (!file.path) continue;

    try {
      const url = await getFileUrl(file.path);
      const element = document.createElement(
        file.type?.startsWith("video/") ? "video" : "img"
      );
      element.src = url;
      if (element.tagName === "VIDEO") {
        element.controls = true;
        element.playsInline = true;
      } else {
        element.alt = file.name || "Фото воспоминания";
      }
      $("#viewFiles").appendChild(element);
    } catch(error) {
      const message = document.createElement("p");
      message.className = "notice";
      message.textContent = "Не удалось открыть файл: " + (file.name || "");
      $("#viewFiles").appendChild(message);
    }
  }
}

$("#closeModal").addEventListener("click",() => {
  $("#viewModal").classList.add("hidden");
});

$("#viewModal").addEventListener("click",event => {
  if (event.target.id === "viewModal") {
    $("#viewModal").classList.add("hidden");
  }
});

async function shareCurrentMemory() {
  if (!currentId) {
    status($("#shareStatus"),"Сначала сохраните воспоминание.",true);
    return;
  }

  const email = $("#shareEmail").value.trim().toLowerCase();
  if (!email) {
    status($("#shareStatus"),"Введите электронную почту.",true);
    return;
  }

  const button = $("#shareButton");
  button.disabled = true;
  status($("#shareStatus"),"Отправляем приглашение...");

  try {
    const {error} = await supabaseClient.rpc("share_memory_with_email",{
      p_memory_id:currentId,
      p_email:email
    });

    if (error) throw error;

    $("#shareEmail").value = "";
    status($("#shareStatus"),"Доступ успешно предоставлен!");
    await loadMyShares();
  } catch(error) {
    status($("#shareStatus"),error.message || "Не удалось поделиться воспоминанием.",true);
  } finally {
    button.disabled = false;
  }
}

$("#shareButton").addEventListener("click",shareCurrentMemory);

async function loadMyShares() {
  if (!currentId) return;

  const {data,error} = await supabaseClient
    .from("memory_shares")
    .select("id,shared_email,shared_with,created_at")
    .eq("memory_id",currentId)
    .eq("owner_id",currentUser.id);

  if (error) {
    status($("#shareStatus"),error.message,true);
    return;
  }

  myShares = data || [];
  renderMyShares();
}

function renderMyShares() {
  $("#shareList").innerHTML = myShares.length
    ? myShares.map(share => `
      <div class="share-item">
        <span>${escapeHTML(share.shared_email || share.shared_with)}</span>
        <button class="btn danger" style="padding:7px 9px"
          data-revoke="${escapeHTML(share.id)}">Отозвать</button>
      </div>
    `).join("")
    : '<p class="notice">Пока никто не имеет доступа.</p>';
}

$("#shareList").addEventListener("click",async event => {
  const button = event.target.closest("[data-revoke]");
  if (!button) return;

  if (!confirm("Отозвать доступ у этого пользователя?")) return;

  button.disabled = true;

  try {
    const {error} = await supabaseClient.rpc("revoke_memory_share",{
      p_share_id:button.dataset.revoke
    });
    if (error) throw error;

    status($("#shareStatus"),"Доступ отозван.");
    await loadMyShares();
  } catch(error) {
    status($("#shareStatus"),error.message,true);
    button.disabled = false;
  }
});

// Initial session check
(async () => {
  const {data,error} = await supabaseClient.auth.getSession();
  if (error) {
    status($("#authStatus"),error.message,true);
    return;
  }
  if (data.session?.user) {
    showApp(data.session.user);
  } else {
    showAuth();
  }
})();
</script>
</body>
</html>
