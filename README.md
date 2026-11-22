<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Genesis — Open Minds Memory</title>
<script src="https://cdn.jsdelivr.net/npm/@supabase/supabase-js@2/dist/umd/supabase.js"></script>
<style>
:root {
  --bg:#100d10;
  --panel:#1b151a;
  --panel2:#241b22;
  --red:#762b42;
  --gold:#d5ad69;
  --text:#f4eae8;
  --muted:#a99ba0;
  --border:#3b2932;
}
*{box-sizing:border-box}
body{
  margin:0;background:var(--bg);color:var(--text);
  font-family:Arial,sans-serif;min-height:100vh;
}
button,input,textarea{font:inherit}
button{
  border:0;border-radius:10px;padding:12px 17px;
  background:var(--red);color:white;cursor:pointer;
  transition:.2s;
}
button:hover{filter:brightness(1.2)}
button.secondary{background:var(--panel2);border:1px solid var(--border)}
button.gold{background:var(--gold);color:#21170e}
input,textarea{
  width:100%;padding:13px;margin:7px 0 14px;
  background:#120f12;color:var(--text);
  border:1px solid var(--border);border-radius:10px;
  outline:none;
}
input:focus,textarea:focus{border-color:var(--gold)}
textarea{min-height:100px;resize:vertical}
label{font-size:13px;color:var(--muted)}
.hidden{display:none!important}
#authScreen{
  min-height:100vh;display:grid;place-items:center;padding:20px;
  background:radial-gradient(circle at top,#38202c 0%,var(--bg) 55%);
}
.auth-card{
  width:min(430px,100%);padding:30px;
  background:var(--panel);border:1px solid var(--border);
  border-radius:20px;box-shadow:0 20px 70px #0008;
}
.logo{font-size:34px;font-weight:bold;color:var(--gold);letter-spacing:3px}
.subtitle{color:var(--muted);margin:8px 0 25px}
#app{min-height:100vh}
header{
  display:flex;align-items:center;justify-content:space-between;
  padding:18px 5%;border-bottom:1px solid var(--border);
  background:#151015;position:sticky;top:0;z-index:5;
}
header .logo{font-size:23px}
.layout{display:flex;max-width:1450px;margin:auto}
aside{
  width:230px;padding:25px 15px;border-right:1px solid var(--border);
  min-height:calc(100vh - 65px);
}
.nav-btn{
  width:100%;text-align:left;margin:5px 0;
  background:transparent;color:var(--muted);
}
.nav-btn.active,.nav-btn:hover{background:var(--panel2);color:var(--gold)}
main{flex:1;padding:30px;min-width:0}
h1{font-size:28px;margin:0 0 8px}
h2{font-size:20px;margin:0 0 18px}
.muted{color:var(--muted)}
.section{display:none}
.section.active{display:block}
.panel{
  background:var(--panel);border:1px solid var(--border);
  border-radius:16px;padding:22px;margin:18px 0;
}
.grid{
  display:grid;grid-template-columns:repeat(auto-fill,minmax(230px,1fr));
  gap:15px;margin-top:20px;
}
.card{
  background:var(--panel);border:1px solid var(--border);
  border-radius:15px;padding:18px;min-width:0;
}
.card h3{margin:0 0 9px;overflow-wrap:anywhere}
.card p{color:var(--muted);white-space:pre-wrap;overflow-wrap:anywhere}
.row{display:flex;gap:10px;flex-wrap:wrap;align-items:center}
.row>*{flex:1}
.small{font-size:12px;color:var(--muted)}
.actions{display:flex;gap:8px;flex-wrap:wrap;margin-top:14px}
.actions button{font-size:13px;padding:9px 12px}
.file-row{
  padding:12px;background:var(--panel2);border-radius:10px;
  margin:8px 0;display:flex;justify-content:space-between;
  gap:10px;align-items:center;overflow-wrap:anywhere;
}
#message{
  position:fixed;bottom:20px;right:20px;z-index:20;
  background:var(--gold);color:#21170e;padding:14px 20px;
  border-radius:12px;display:none;max-width:90%;
}
.empty{padding:30px;text-align:center;color:var(--muted)}
hr{border:0;border-top:1px solid var(--border);margin:20px 0}
@media(max-width:700px){
  header{padding:14px}
  .layout{display:block}
  aside{
    width:100%;min-height:0;display:flex;overflow-x:auto;
    padding:8px;border-right:0;border-bottom:1px solid var(--border);
  }
  .nav-btn{width:auto;white-space:nowrap;padding:10px}
  main{padding:18px}
  .panel{padding:16px}
  header .logo{font-size:19px}
}
</style>
</head>
<body>

<div id="authScreen">
  <div class="auth-card">
    <div class="logo">GENESIS</div>
    <div class="subtitle">Open Minds Memory — твоя история начинается здесь</div>
    <div id="loginForm">
      <h2>Добро пожаловать</h2>
      <label>Email</label>
      <input id="loginEmail" type="email" placeholder="your@email.com">
      <label>Пароль</label>
      <input id="loginPassword" type="password" placeholder="Пароль">
      <button style="width:100%" onclick="login()">Войти</button>
      <p class="small">Нет аккаунта? <a href="#" onclick="toggleAuth(true)" style="color:var(--gold)">Зарегистрироваться</a></p>
    </div>
    <div id="registerForm" class="hidden">
      <h2>Создать аккаунт</h2>
      <label>Email</label>
      <input id="registerEmail" type="email" placeholder="your@email.com">
      <label>Пароль</label>
      <input id="registerPassword" type="password" placeholder="Минимум 6 символов">
      <button style="width:100%" onclick="register()">Зарегистрироваться</button>
      <p class="small">Уже есть аккаунт? <a href="#" onclick="toggleAuth(false)" style="color:var(--gold)">Войти</a></p>
    </div>
  </div>
</div>

<div id="app" class="hidden">
  <header>
    <div class="logo">GENESIS</div>
    <div class="row" style="flex:0;align-items:center">
      <span id="userEmail" class="small"></span>
      <button class="secondary" onclick="logout()">Выйти</button>
    </div>
  </header>

  <div class="layout">
    <aside>
      <button class="nav-btn active" data-section="home">⌂ Главная</button>
      <button class="nav-btn" data-section="memories">✦ Мои воспоминания</button>
      <button class="nav-btn" data-section="shared">♡ Со мной поделились</button>
      <button class="nav-btn" data-section="folders">▣ Общие папки</button>
    </aside>

    <main>
      <section id="home" class="section active">
        <h1>Твоя история.</h1>
        <p class="muted">Место, где моменты становятся воспоминаниями.</p>
        <div class="grid">
          <div class="card">
            <h3>✦ Личный архив</h3>
            <p>Сохраняй важные моменты своей жизни.</p>
            <button onclick="navigate('memories')">Открыть архив</button>
          </div>
          <div class="card">
            <h3>♡ Общие воспоминания</h3>
            <p>Смотри моменты, которыми поделились с тобой.</p>
            <button onclick="navigate('shared')">Открыть</button>
          </div>
          <div class="card">
            <h3>▣ Общие папки</h3>
            <p>Работай над папками вместе с другими людьми.</p>
            <button onclick="navigate('folders')">Открыть</button>
          </div>
        </div>
      </section>

      <section id="memories" class="section">
        <h1>Мои воспоминания</h1>
        <p class="muted">Сохраняй то, что хочется помнить.</p>
        <div class="panel">
          <h2>＋ Новое воспоминание</h2>
          <label>Название</label>
          <input id="memoryName" placeholder="Например, незабываемый день">
          <label>Описание</label>
          <textarea id="memoryDescription" placeholder="Расскажи, что произошло..."></textarea>
          <div class="row">
            <div><label>Настроение</label><input id="memoryMood" placeholder="Радость, спокойствие..."></div>
            <div><label>Погода</label><input id="memoryWeather" placeholder="Солнечно, дождь..."></div>
          </div>
          <label>Ссылка на песню (необязательно)</label>
          <input id="memorySong" placeholder="https://...">
          <label>Файлы и фотографии</label>
          <input id="memoryFiles" type="file" multiple>
          <button class="gold" onclick="createMemory()">Сохранить воспоминание</button>
        </div>
        <div id="myMemories" class="grid"></div>
      </section>

      <section id="shared" class="section">
        <h1>Со мной поделились</h1>
        <p class="muted">Воспоминания, доступ к которым тебе предоставили.</p>
        <div id="receivedMemories" class="grid"></div>
      </section>

      <section id="folders" class="section">
        <h1>Общие папки</h1>
        <p class="muted">Совместное пространство для идей, заметок и файлов.</p>
        <div class="panel">
          <h2>＋ Создать общую папку</h2>
          <input id="newFolderName" placeholder="Название папки">
          <button class="gold" onclick="createFolder()">Создать</button>
        </div>
        <div id="folderList" class="grid"></div>
        <div id="folderWorkspace" class="panel hidden">
          <div class="row">
            <h2 id="currentFolderTitle"></h2>
            <button class="secondary" onclick="closeFolder()">Назад</button>
          </div>
          <div class="row">
            <button onclick="createSharedItem('folder')">＋ Папка</button>
            <button onclick="createSharedItem('note')">＋ Заметка</button>
            <button onclick="document.getElementById('sharedUpload').click()">＋ Файл</button>
            <input id="sharedUpload" type="file" class="hidden" onchange="uploadSharedFile(this.files[0])">
          </div>
          <div class="actions">
            <button class="secondary" onclick="makeInvite()">Создать ссылку-приглашение</button>
            <button class="secondary" onclick="showMembers()">Участники</button>
          </div>
          <div id="folderBreadcrumb" class="small" style="margin:15px 0"></div>
          <div id="sharedItems"></div>
          <div id="folderMembers" class="small"></div>
        </div>
      </section>
    </main>
  </div>
</div>

<div id="message"></div>

<script>
const SUPABASE_URL = "https://ydrzlazhucdlvvyjisnm.supabase.co";
const SUPABASE_ANON_KEY = "sb_publishable_l_aik6ePDy4GFPZRwBH1ZQ_9oSb_Dji";
const db = window.supabase.createClient(SUPABASE_URL, SUPABASE_ANON_KEY);

let currentUser = null;
let currentFolder = null;
let currentParent = null;
let folderStack = [];
let allMemories = [];

function toast(text) {
  const el = document.getElementById("message");
  el.textContent = text;
  el.style.display = "block";
  setTimeout(() => el.style.display = "none", 3500);
}
function escapeHTML(value) {
  return String(value ?? "").replace(/[&<>"']/g, c => ({
    "&":"&amp;","<":"&lt;",">":"&gt;",'"':"&quot;","'":"&#39;"
  }[c]));
}
function toggleAuth(registerMode) {
  document.getElementById("loginForm").classList.toggle("hidden", registerMode);
  document.getElementById("registerForm").classList.toggle("hidden", !registerMode);
}
function navigate(section) {
  document.querySelectorAll(".section").forEach(x => x.classList.remove("active"));
  document.getElementById(section).classList.add("active");
  document.querySelectorAll(".nav-btn").forEach(x =>
    x.classList.toggle("active", x.dataset.section === section)
  );
  if (section === "memories") loadMemories();
  if (section === "shared") loadReceivedMemories();
  if (section === "folders") loadFolders();
}
document.querySelectorAll(".nav-btn").forEach(btn =>
  btn.addEventListener("click", () => navigate(btn.dataset.section))
);

async function login() {
  const email = document.getElementById("loginEmail").value.trim();
  const password = document.getElementById("loginPassword").value;
  if (!email || !password) return toast("Заполни email и пароль");
  const {error} = await db.auth.signInWithPassword({email,password});
  if (error) toast(error.message);
}
async function register() {
  const email = document.getElementById("registerEmail").value.trim();
  const password = document.getElementById("registerPassword").value;
  if (!email || password.length < 6) return toast("Проверь email и пароль (минимум 6 символов)");
  const {data,error} = await db.auth.signUp({email,password});
  if (error) return toast(error.message);
  if (!data.session) toast("Проверь почту и подтверди регистрацию.");
  else toast("Аккаунт создан!");
}
async function logout() {
  const {error} = await db.auth.signOut();
  if (error) toast(error.message);
}
function showApp(user) {
  currentUser = user;
  document.getElementById("authScreen").classList.add("hidden");
  document.getElementById("app").classList.remove("hidden");
  document.getElementById("userEmail").textContent = user.email || "";
  loadMemories();
  loadFolders();
  acceptInviteFromUrl();
}
function showAuth() {
  currentUser = null;
  document.getElementById("app").classList.add("hidden");
  document.getElementById("authScreen").classList.remove("hidden");
}
db.auth.onAuthStateChange((event,session) => {
  if (session?.user) showApp(session.user);
  else showAuth();
});
