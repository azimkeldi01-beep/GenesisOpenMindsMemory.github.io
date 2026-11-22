<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Genesis — Open Minds Memory</title>
<script src="https://cdn.jsdelivr.net/npm/@supabase/supabase-js@2/dist/umd/supabase.js"></script>
<style>
:root{
  --bg:#f3f8ff;
  --panel:#ffffff;
  --panel2:#eaf3ff;
  --blue:#3478f6;
  --blue-dark:#245ac4;
  --lime:#c8f169;
  --lime-dark:#a8d94b;
  --text:#17243a;
  --muted:#687991;
  --border:#dce8f7;
  --shadow:0 12px 34px rgba(45,91,150,.09);
}
*{box-sizing:border-box}
html{scroll-behavior:smooth}
body{margin:0;background:linear-gradient(135deg,#f5f9ff 0%,#edf6ff 55%,#f7fbea 100%);color:var(--text);font-family:Inter,Arial,sans-serif;min-height:100vh}
button,input,textarea{font:inherit}
button{border:0;border-radius:14px;padding:12px 18px;background:var(--blue);color:#fff;cursor:pointer;font-weight:650;box-shadow:0 5px 14px rgba(52,120,246,.15);transition:transform .18s,filter .18s,box-shadow .18s}
button:hover{filter:brightness(1.04);transform:translateY(-1px);box-shadow:0 8px 18px rgba(52,120,246,.2)}
button:active{transform:translateY(0)}
button.secondary{background:#edf4ff;color:#315b9d;border:1px solid #d8e6fa;box-shadow:none}
button.gold{background:var(--lime);color:#26351a;box-shadow:0 5px 14px rgba(168,217,75,.2)}
input,textarea{width:100%;padding:13px 15px;margin:7px 0 14px;background:#fbfdff;color:var(--text);border:1px solid var(--border);border-radius:14px;outline:none;transition:border-color .2s,box-shadow .2s}
input:focus,textarea:focus{border-color:var(--blue);box-shadow:0 0 0 4px rgba(52,120,246,.1)}
textarea{min-height:110px;resize:vertical}
label{font-size:13px;color:var(--muted);font-weight:650}
.hidden{display:none!important}
#authScreen{min-height:100vh;display:grid;place-items:center;padding:24px;background:radial-gradient(circle at 15% 10%,#dceaff 0,transparent 36%),radial-gradient(circle at 90% 90%,#e7f8c9 0,transparent 34%)}
.auth-card{width:min(440px,100%);padding:34px;background:rgba(255,255,255,.94);border:1px solid var(--border);border-radius:26px;box-shadow:0 24px 75px rgba(45,91,150,.14)}
.logo{font-size:34px;font-weight:850;color:var(--blue);letter-spacing:3px}
.subtitle{color:var(--muted);margin:8px 0 25px;line-height:1.55}
#app{min-height:100vh}
header{display:flex;align-items:center;justify-content:space-between;gap:20px;padding:17px clamp(20px,5vw,76px);border-bottom:1px solid var(--border);background:rgba(255,255,255,.88);backdrop-filter:blur(14px);position:sticky;top:0;z-index:5}
header .logo{font-size:23px}
.layout{display:flex;width:min(1600px,100%);min-height:calc(100vh - 70px);margin:0 auto}
aside{width:255px;flex:0 0 255px;padding:28px 18px;border-right:1px solid var(--border);background:rgba(255,255,255,.48)}
.nav-btn{width:100%;text-align:left;margin:5px 0;background:transparent;color:#63748d;box-shadow:none;border-radius:14px;padding:13px 15px}
.nav-btn.active,.nav-btn:hover{background:#eaf2ff;color:var(--blue-dark);box-shadow:none;transform:none}
main{flex:1;padding:clamp(28px,4vw,58px);min-width:0;max-width:1320px;margin:0 auto}
h1{font-size:clamp(27px,3vw,36px);letter-spacing:-.7px;margin:0 0 9px}
h2{font-size:21px;margin:0 0 18px}
.muted{color:var(--muted);line-height:1.65}
.section{display:none}.section.active{display:block;animation:fadeIn .25s ease}
@keyframes fadeIn{from{opacity:0;transform:translateY(5px)}to{opacity:1;transform:translateY(0)}}
.panel{background:var(--panel);border:1px solid var(--border);border-radius:22px;padding:clamp(18px,2.5vw,28px);margin:22px 0;box-shadow:var(--shadow)}
.grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(min(100%,260px),1fr));gap:18px;margin-top:22px}
.card{background:var(--panel);border:1px solid var(--border);border-radius:21px;padding:22px;min-width:0;box-shadow:var(--shadow);transition:transform .2s,box-shadow .2s}
.card:hover{transform:translateY(-3px);box-shadow:0 16px 38px rgba(45,91,150,.13)}
.card h3{margin:0 0 10px;overflow-wrap:anywhere;font-size:18px}
.card p{color:var(--muted);white-space:pre-wrap;overflow-wrap:anywhere;line-height:1.6}
.row{display:flex;gap:12px;flex-wrap:wrap;align-items:center}.row>*{flex:1;min-width:0}
.small{font-size:12px;color:var(--muted)}
.actions{display:flex;gap:9px;flex-wrap:wrap;margin-top:15px}.actions button{font-size:13px;padding:10px 14px}
.file-row{padding:14px 16px;background:#f4f8ff;border:1px solid #e3edfa;border-radius:15px;margin:9px 0;display:flex;justify-content:space-between;gap:12px;align-items:center;overflow-wrap:anywhere}
#message{position:fixed;bottom:22px;right:22px;z-index:20;background:var(--lime);color:#26351a;padding:14px 20px;border-radius:15px;display:none;max-width:min(440px,90%);box-shadow:var(--shadow);font-weight:650}
.empty{padding:34px 20px;text-align:center;color:var(--muted);background:rgba(255,255,255,.65);border:1px dashed #cbdcf0;border-radius:18px}
hr{border:0;border-top:1px solid var(--border);margin:20px 0}
@media(min-width:1500px){main{padding:58px 68px}.grid{grid-template-columns:repeat(3,minmax(0,1fr))}}
@media(max-width:900px){aside{width:220px;flex-basis:220px}main{padding:28px}}
@media(max-width:700px){header{padding:13px 15px;gap:10px}header .logo{font-size:19px}.layout{display:block}aside{width:100%;min-height:0;display:flex;gap:5px;overflow-x:auto;padding:9px 12px;border-right:0;border-bottom:1px solid var(--border)}.nav-btn{width:auto;flex:0 0 auto;white-space:nowrap;padding:11px 13px;margin:0}main{padding:20px 15px}.panel{padding:17px}.grid{grid-template-columns:1fr}.auth-card{padding:25px;border-radius:22px}header .row{gap:7px}#userEmail{max-width:120px;overflow:hidden;text-overflow:ellipsis}}
</style>
</head>
<body>

<div id="authScreen">
  <div class="auth-card">
    <div class="logo">GENESIS ✨</div>
    <div class="subtitle">Open Minds Memory — твоя история начинается здесь</div>
    <div id="loginForm">
      <h2>👋 Добро пожаловать</h2>
      <label>Email</label>
      <input id="loginEmail" type="email" placeholder="your@email.com">
      <label>Пароль</label>
      <input id="loginPassword" type="password" placeholder="Пароль">
      <button style="width:100%" onclick="login()">🔐 Войти</button>
      <p class="small">Нет аккаунта? <a href="#" onclick="toggleAuth(true)" style="color:var(--blue)">Зарегистрироваться</a></p>
    </div>
    <div id="registerForm" class="hidden">
      <h2>🌱 Создать аккаунт</h2>
      <label>Email</label>
      <input id="registerEmail" type="email" placeholder="your@email.com">
      <label>Пароль</label>
      <input id="registerPassword" type="password" placeholder="Минимум 6 символов">
      <button style="width:100%" onclick="register()">✨ Зарегистрироваться</button>
      <p class="small">Уже есть аккаунт? <a href="#" onclick="toggleAuth(false)" style="color:var(--blue)">Войти</a></p>
    </div>
  </div>
</div>

<div id="app" class="hidden">
  <header>
    <div class="logo">GENESIS ✨</div>
    <div class="row" style="flex:0;align-items:center">
      <span id="userEmail" class="small"></span>
      <button class="secondary" onclick="logout()">🚪 Выйти</button>
    </div>
  </header>

  <div class="layout">
    <aside>
      <button class="nav-btn active" data-section="home">🏠 Главная</button>
      <button class="nav-btn" data-section="memories">📸 Мои воспоминания</button>
      <button class="nav-btn" data-section="shared">💌 Со мной поделились</button>
      <button class="nav-btn" data-section="folders">📁 Общие папки</button>
    </aside>

    <main>
      <section id="home" class="section active">
        <h1>✨ Твоя история.</h1>
        <p class="muted">Место, где моменты становятся воспоминаниями.</p>
        <div class="grid">
          <div class="card">
            <h3>📚 Личный архив</h3>
            <p>Сохраняй важные моменты своей жизни.</p>
            <button onclick="navigate('memories')">📖 Открыть архив</button>
          </div>
          <div class="card">
            <h3>💝 Общие воспоминания</h3>
            <p>Смотри моменты, которыми поделились с тобой.</p>
            <button onclick="navigate('shared')">💌 Открыть</button>
          </div>
          <div class="card">
            <h3>🗂️ Общие папки</h3>
            <p>Работай над папками вместе с другими людьми.</p>
            <button onclick="navigate('folders')">📂 Открыть</button>
          </div>
        </div>
      </section>

      <section id="memories" class="section">
        <h1>📸 Мои воспоминания</h1>
        <p class="muted">Сохраняй то, что хочется помнить.</p>
        <div class="panel">
          <h2>📝 Новое воспоминание</h2>
          <label>🏷️ Название</label>
          <input id="memoryName" placeholder="Например, незабываемый день">
          <label>✍️ Описание</label>
          <textarea id="memoryDescription" placeholder="Расскажи, что произошло..."></textarea>
          <div class="row">
            <div><label>😊 Настроение</label><input id="memoryMood" placeholder="Радость, спокойствие..."></div>
            <div><label>🌤️ Погода</label><input id="memoryWeather" placeholder="Солнечно, дождь..."></div>
          </div>
          <label>🎵 Ссылка на песню (необязательно)</label>
          <input id="memorySong" placeholder="https://...">
          <label>🖼️ Файлы и фотографии</label>
          <input id="memoryFiles" type="file" multiple>
          <button class="gold" onclick="createMemory()">💾 Сохранить воспоминание</button>
        </div>
        <div id="myMemories" class="grid"></div>
      </section>

      <section id="shared" class="section">
        <h1>💌 Со мной поделились</h1>
        <p class="muted">Воспоминания, доступ к которым тебе предоставили.</p>
        <div id="receivedMemories" class="grid"></div>
      </section>

      <section id="folders" class="section">
        <h1>📁 Общие папки</h1>
        <p class="muted">Совместное пространство для идей, заметок и файлов.</p>
        <div class="panel">
          <h2>🗂️ Создать общую папку</h2>
          <input id="newFolderName" placeholder="Название папки">
          <button class="gold" onclick="createFolder()">➕ Создать</button>
        </div>
        <div id="folderList" class="grid"></div>
        <div id="folderWorkspace" class="panel hidden">
          <div class="row">
            <h2 id="currentFolderTitle"></h2>
            <button class="secondary" onclick="closeFolder()">↩️ Назад</button>
          </div>
          <div class="row">
            <button onclick="createSharedItem('folder')">📁 Папка</button>
            <button onclick="createSharedItem('note')">📝 Заметка</button>
            <button onclick="document.getElementById('sharedUpload').click()">📎 Файл</button>
            <input id="sharedUpload" type="file" class="hidden" onchange="uploadSharedFile(this.files[0])">
          </div>
          <div class="actions">
            <button class="secondary" onclick="makeInvite()">🔗 Создать ссылку-приглашение</button>
            <button class="secondary" onclick="showMembers()">👥 Участники</button>
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

async function createMemory() {
  const name = document.getElementById("memoryName").value.trim();
  if (!name) return toast("Введи название воспоминания");
  const filesInput = document.getElementById("memoryFiles");
  const uploaded = [];
  for (const file of filesInput.files) {
    const path = currentUser.id + "/" + crypto.randomUUID() + "_" + file.name;
    const {error} = await db.storage.from("memory-files").upload(path,file);
    if (error) return toast("Ошибка загрузки файла: " + error.message);
    uploaded.push({name:file.name,path,mime_type:file.type});
  }
  const record = {
    user_id:currentUser.id,
    name,
    description:document.getElementById("memoryDescription").value,
    mood:document.getElementById("memoryMood").value,
    weather:document.getElementById("memoryWeather").value,
    song_url:document.getElementById("memorySong").value,
    files:uploaded
  };
  const {error} = await db.from("memories").insert(record);
  if (error) return toast(error.message);
  ["memoryName","memoryDescription","memoryMood","memoryWeather","memorySong"].forEach(id =>
    document.getElementById(id).value = ""
  );
  filesInput.value = "";
  toast("Воспоминание сохранено!");
  loadMemories();
}
async function loadMemories() {
  if (!currentUser) return;
  const {data,error} = await db.from("memories").select("*").order("created_at",{ascending:false});
  if (error) return toast(error.message);
  allMemories = data || [];
  renderMemories(allMemories.filter(m => m.user_id === currentUser.id),"myMemories",true);
}
async function loadReceivedMemories() {
  if (!currentUser) return;
  const {data,error} = await db.from("memories").select("*").neq("user_id",currentUser.id).order("created_at",{ascending:false});
  if (error) return toast(error.message);
  renderMemories(data || [],"receivedMemories",false);
}
function renderMemories(items,target,owned) {
  const el = document.getElementById(target);
  if (!items.length) {
    el.innerHTML = '<div class="empty">Пока здесь ничего нет.</div>';
    return;
  }
  el.innerHTML = items.map(m => `
    <div class="card">
      <h3>✨ ${escapeHTML(m.name)}</h3>
      <p>${escapeHTML(m.description)}</p>
      <div class="small">😊 ${escapeHTML(m.mood || "")} ${m.weather ? " · 🌤️ " + escapeHTML(m.weather) : ""}</div>
      <div class="small">📅 ${m.created_at ? new Date(m.created_at).toLocaleDateString() : ""}</div>
      ${m.song_url ? `<p><a href="${escapeHTML(m.song_url)}" target="_blank" rel="noopener" style="color:var(--blue)">🎵 Открыть песню</a></p>` : ""}
      <div class="actions">
        <button class="secondary" onclick="showMemoryFiles('${m.id}')">📎 Файлы</button>
        ${owned ? `<button onclick="shareMemory('${m.id}')">💌 Поделиться</button>
        <button class="secondary" onclick="deleteMemory('${m.id}')">🗑️ Удалить</button>` : ""}
      </div>
      <div id="memoryFiles-${m.id}"></div>
    </div>
  `).join("");
}
async function showMemoryFiles(id) {
  const memory = allMemories.find(m => m.id === id);
  const box = document.getElementById("memoryFiles-" + id);
  if (!memory || !box) return;
  const files = Array.isArray(memory.files) ? memory.files : [];
  if (!files.length) {box.innerHTML = '<p class="small">📭 Файлов нет.</p>';return;}
  let html = "";
  for (const file of files) {
    const {data,error} = await db.storage.from("memory-files").createSignedUrl(file.path,3600);
    html += error
      ? `<p class="small">${escapeHTML(file.name)} — ${escapeHTML(error.message)}</p>`
      : `<div class="file-row"><span>📎 ${escapeHTML(file.name)}</span><a style="color:var(--blue)" target="_blank" rel="noopener" href="${escapeHTML(data.signedUrl)}">Открыть ↗</a></div>`;
  }
  box.innerHTML = html;
}
async function deleteMemory(id) {
  if (!confirm("Удалить это воспоминание?")) return;
  const memory = allMemories.find(m => m.id === id);
  const paths = (Array.isArray(memory?.files) ? memory.files : []).map(f => f.path);
  if (paths.length) {
    const {error:storageError} = await db.storage.from("memory-files").remove(paths);
    if (storageError) return toast(storageError.message);
  }
  const {error} = await db.from("memories").delete().eq("id",id);
  if (error) return toast(error.message);
  toast("🗑️ Воспоминание удалено");
  loadMemories();
}
async function shareMemory(id) {
  const email = prompt("Email пользователя, с которым поделиться:");
  if (!email) return;
  const {error} = await db.rpc("share_memory_with_email",{
    p_memory_id:id,
    p_email:email.trim()
  });
  if (error) return toast(error.message);
  toast("💌 Доступ предоставлен!");
}

// Общие папки
async function createFolder() {
  const name = document.getElementById("newFolderName").value.trim();
  if (!name) return toast("Введи название папки");
  const {error} = await db.rpc("create_shared_folder",{p_name:name});
  if (error) return toast(error.message);
  document.getElementById("newFolderName").value = "";
  toast("📁 Общая папка создана");
  loadFolders();
}
async function loadFolders() {
  if (!currentUser) return;
  const {data,error} = await db.from("shared_folders").select("*").order("created_at",{ascending:false});
  if (error) return toast(error.message);
  const el = document.getElementById("folderList");
  if (!data?.length) {
    el.innerHTML = '<div class="empty">📭 Общих папок пока нет.</div>';
    return;
  }
  el.innerHTML = data.map(f => `
    <div class="card">
      <h3>📁 ${escapeHTML(f.name)}</h3>
      <p class="small">👥 Общее пространство</p>
      <button onclick="openFolder('${f.id}','${escapeHTML(f.name)}')">📂 Открыть</button>
    </div>
  `).join("");
}
async function openFolder(id,name) {
  currentFolder = id;
  currentParent = null;
  folderStack = [];
  document.getElementById("folderWorkspace").classList.remove("hidden");
  document.getElementById("currentFolderTitle").textContent = "📁 " + name;
  await loadSharedItems();
  document.getElementById("folderWorkspace").scrollIntoView({behavior:"smooth"});
}
function closeFolder() {
  currentFolder = null;
  document.getElementById("folderWorkspace").classList.add("hidden");
}
async function loadSharedItems() {
  if (!currentFolder) return;
  const {data,error} = await db.from("shared_folder_items")
    .select("*").eq("folder_id",currentFolder)
    .order("created_at",{ascending:true});
  if (error) return toast(error.message);
  const items = (data || []).filter(x => (x.parent_id || null) === currentParent);
  document.getElementById("folderBreadcrumb").textContent =
    "📁 Папка" + (folderStack.length ? " / " + folderStack.map(x => x.name).join(" / ") : "");
  const el = document.getElementById("sharedItems");
  if (!items.length) {
    el.innerHTML = '<div class="empty">📭 Здесь пока пусто. Создай папку, заметку или добавь файл.</div>';
    return;
  }
  el.innerHTML = items.map(item => `
    <div class="file-row">
      <span>${item.item_type === "folder" ? "📁" : item.item_type === "note" ? "📝" : "📎"}
      ${escapeHTML(item.name)}</span>
      <div class="actions">
        ${item.item_type === "folder" ? `<button onclick="enterFolder('${item.id}','${escapeHTML(item.name)}')">📂 Открыть</button>` : ""}
        ${item.item_type === "note" ? `<button class="secondary" onclick="readNote('${item.id}')">📖 Читать</button>` : ""}
        ${item.item_type === "file" ? `<button class="secondary" onclick="openSharedFile('${item.id}')">📂 Открыть</button>` : ""}
        <button class="secondary" onclick="deleteSharedItem('${item.id}','${item.item_type}')">🗑️ Удалить</button>
      </div>
    </div>
  `).join("");
}
function enterFolder(id,name) {
  folderStack.push({id:currentParent,name});
  currentParent = id;
  loadSharedItems();
}
async function createSharedItem(type) {
  const name = prompt(type === "folder" ? "Название папки:" : "Название заметки:");
  if (!name) return;
  let content = null;
  if (type === "note") {
    content = prompt("Текст заметки:") || "";
  }
  const {error} = await db.from("shared_folder_items").insert({
    folder_id:currentFolder,
    parent_id:currentParent,
    item_type:type,
    name,
    content,
    created_by:currentUser.id
  });
  if (error) return toast(error.message);
  toast("✅ Добавлено");
  loadSharedItems();
}
async function readNote(id) {
  const {data,error} = await db.from("shared_folder_items").select("name,content").eq("id",id).single();
  if (error) return toast(error.message);
  alert("📝 " + data.name + "\n\n" + (data.content || ""));
}
async function uploadSharedFile(file) {
  if (!file || !currentFolder) return;
  const path = currentFolder + "/" + crypto.randomUUID() + "_" + file.name;
  const {error:uploadError} = await db.storage.from("shared-folder-files").upload(path,file);
  if (uploadError) return toast(uploadError.message);
  const {error} = await db.from("shared_folder_items").insert({
    folder_id:currentFolder,
    parent_id:currentParent,
    item_type:"file",
    name:file.name,
    storage_path:path,
    mime_type:file.type,
    size_bytes:file.size,
    created_by:currentUser.id
  });
  if (error) {
    await db.storage.from("shared-folder-files").remove([path]);
    return toast(error.message);
  }
  document.getElementById("sharedUpload").value = "";
  toast("📎 Файл загружен");
  loadSharedItems();
}
async function openSharedFile(id) {
  const {data,error} = await db.from("shared_folder_items").select("*").eq("id",id).single();
  if (error) return toast(error.message);
  const result = await db.storage.from("shared-folder-files").createSignedUrl(data.storage_path,3600);
  if (result.error) return toast(result.error.message);
  window.open(result.data.signedUrl,"_blank","noopener");
}
async function deleteSharedItem(id,type) {
  const item = (await db.from("shared_folder_items")
    .select("*").eq("id",id).single()).data;

  if (!item || !confirm(`Удалить «${item.name}»?`)) return;

  const {data:allItems,error:loadError} = await db.from("shared_folder_items")
    .select("id,parent_id,item_type,storage_path")
    .eq("folder_id",currentFolder);

  if (loadError) return toast(loadError.message);

  const idsToDelete = new Set([id]);

  if (type === "folder") {
    let changed = true;
    while (changed) {
      changed = false;
      for (const child of (allItems || [])) {
        if (child.parent_id && idsToDelete.has(child.parent_id) && !idsToDelete.has(child.id)) {
          idsToDelete.add(child.id);
          changed = true;
        }
      }
    }
  }

  const descendants = (allItems || []).filter(entry => idsToDelete.has(entry.id));
  const paths = descendants.map(entry => entry.storage_path).filter(Boolean);

  if (paths.length) {
    const {error:storageError} = await db.storage
      .from("shared-folder-files")
      .remove(paths);
    if (storageError) return toast(storageError.message);
  }

  const {error} = await db.from("shared_folder_items")
    .delete()
    .in("id",Array.from(idsToDelete));

  if (error) return toast(error.message);

  toast("🗑️ Материал удалён");
  await loadSharedItems();
}
async function makeInvite() {
  const {data,error} = await db.rpc("create_shared_folder_invite",{
    p_folder_id:currentFolder
  });
  if (error) return toast(error.message);
  const link = location.origin + location.pathname + "?invite=" + encodeURIComponent(data);
  try {
    await navigator.clipboard.writeText(link);
    toast("🔗 Ссылка-приглашение скопирована! Она действует 7 дней.");
  } catch {
    prompt("Скопируй ссылку-приглашение:",link);
  }
}
async function acceptInviteFromUrl() {
  const params = new URLSearchParams(location.search);
  const token = params.get("invite");
  if (!token || !currentUser) return;
  const {error} = await db.rpc("accept_shared_folder_invite",{p_token:token});
  if (error) toast("Не удалось принять приглашение: " + error.message);
  else toast("🎉 Ты присоединился к общей папке!");
  history.replaceState({},document.title,location.pathname);
  loadFolders();
}
async function showMembers() {
  const {data,error} = await db.from("shared_folder_members")
    .select("user_id,role,joined_at").eq("folder_id",currentFolder);
  if (error) return toast(error.message);
  document.getElementById("folderMembers").innerHTML =
    "<hr><b>👥 Участники:</b><br>" + (data || []).map(m =>
      `<p>${escapeHTML(m.role)} · ${escapeHTML(m.user_id)}</p>`
    ).join("");
}
</script>
</body>
</html>
