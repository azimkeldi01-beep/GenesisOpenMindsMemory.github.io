
<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>ArtTech Genesis</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&display=swap" rel="stylesheet">
<script src="https://cdn.jsdelivr.net/npm/@supabase/supabase-js@2"></script>
<style>
:root {
  --bg:#f3f5f7;
  --surface:#fff;
  --surface2:#e9eef2;
  --primary:#29465f;
  --primary2:#426d8e;
  --text:#192b3b;
  --muted:#73808d;
  --border:#dce3e9;
  --radius:12px;
}
*{box-sizing:border-box}
html{scroll-behavior:smooth}
body{margin:0;background:var(--bg);color:var(--text);font-family:Inter,Arial,sans-serif;line-height:1.6}
button,input,textarea,select{font:inherit}
button{cursor:pointer}
a{text-decoration:none;color:inherit}
[hidden]{display:none!important}
.topbar{height:76px;background:#ffffffed;border-bottom:1px solid var(--border);display:flex;align-items:center;padding:0 6%;gap:35px;position:sticky;top:0;z-index:10}
.logo{font-size:21px;font-weight:800;letter-spacing:-1px}
.logo span{color:var(--primary2)}
nav{display:flex;gap:28px}
nav a{font-size:13px;color:var(--muted);font-weight:600}
nav a:hover{color:var(--primary)}
#userBox{margin-left:auto;font-size:13px;display:flex;align-items:center;gap:12px}
.btn{border:1px solid var(--border);background:#fff;color:var(--text);padding:11px 19px;border-radius:8px;font-size:13px;font-weight:600;transition:.2s}
.btn:hover{background:var(--surface2)}
.btn.primary{background:var(--primary);color:#fff;border-color:var(--primary)}
.btn.primary:hover{background:var(--primary2)}
.btn.danger{color:#a34c4c}
.btn.small{padding:8px 13px;font-size:12px}
.btn.full{width:100%;margin-top:14px}
section{padding:90px 6%}
.container{max-width:1200px;margin:auto}
.hero{background:#e8edf1;min-height:620px;display:flex;align-items:center}
.hero-inner{max-width:1200px;margin:auto;width:100%;display:grid;grid-template-columns:1.1fr .9fr;gap:65px;align-items:center}
.eyebrow{font-size:11px;letter-spacing:3px;text-transform:uppercase;color:var(--primary2);font-weight:700}
h1,h2,h3,h4,p{margin-top:0}
h1{font-size:clamp(42px,7vw,82px);line-height:1.02;letter-spacing:-5px;margin:22px 0}
h1 span{color:var(--primary2)}
.hero-description{max-width:550px;color:#596a79;font-size:16px;line-height:1.9}
.hero-buttons{display:flex;gap:12px;margin-top:30px;flex-wrap:wrap}
.hero-visual{display:grid;grid-template-columns:1fr 1fr;gap:15px;transform:rotate(-2deg)}
.visual-card{height:210px;border-radius:8px;box-shadow:0 15px 35px #263d5020}
.visual-card:nth-child(1){background:linear-gradient(145deg,#526e7e,#a7b9c3)}
.visual-card:nth-child(2){background:linear-gradient(145deg,#263a4c,#718798);margin-top:35px}
.visual-card:nth-child(3){background:linear-gradient(145deg,#8c9ba4,#d4d9db);margin-top:-25px}
.visual-card:nth-child(4){background:linear-gradient(145deg,#526778,#c1cbd0)}
.visual-caption{background:#fff;padding:15px;border-radius:7px;font-size:12px;font-weight:600;grid-column:1/3}
.section-heading{margin-bottom:38px}
.section-heading h2{font-size:clamp(32px,4vw,48px);letter-spacing:-2px;margin-bottom:8px}
.section-heading p{color:var(--muted);font-size:14px}
.studio{background:var(--bg)}
.studio-grid{display:grid;grid-template-columns:310px 1fr;gap:24px;align-items:start}
.card{background:var(--surface);border:1px solid var(--border);border-radius:var(--radius);padding:25px;box-shadow:0 5px 20px #1c344308}
.card h3{font-size:19px;letter-spacing:-.5px;margin-bottom:17px}
label{display:block;font-size:12px;font-weight:600;margin:15px 0 7px}
input,textarea,select{width:100%;padding:12px 13px;border:1px solid var(--border);border-radius:7px;background:#fff;color:var(--text);font-size:13px;outline:none}
input:focus,textarea:focus,select:focus{border-color:var(--primary2);box-shadow:0 0 0 3px #426d8e18}
textarea{resize:vertical}
.palette{display:flex;gap:10px;flex-wrap:wrap;margin:13px 0}
.color{width:29px;height:29px;border-radius:50%;border:3px solid white;outline:1px solid var(--border)}
.color.active{outline:2px solid var(--primary)}
.folder-list{display:grid;grid-template-columns:1fr 1fr;gap:10px;margin-top:16px}
.folder-item{border:1px solid var(--border);border-radius:8px;padding:13px 9px;background:#fff;text-align:center;cursor:pointer;transition:.2s}
.folder-item:hover,.folder-item.active{border-color:var(--primary2);background:#edf2f6}
.folder-icon{height:35px;width:48px;margin:0 auto 8px;border-radius:5px 5px 7px 7px;position:relative;background:var(--folder-color,#29465f)}
.folder-icon:before{content:"";position:absolute;top:-5px;left:0;width:20px;height:8px;border-radius:4px 4px 0 0;background:inherit}
.folder-item strong{display:block;font-size:11px;overflow-wrap:anywhere}
.folder-item small{font-size:10px;color:var(--muted)}
.empty{text-align:center;padding:75px 15px;color:var(--muted)}
.empty-icon{font-size:42px;color:#9aaab7;margin-bottom:12px}
.workspace-head{display:flex;align-items:center;gap:15px;border-bottom:1px solid var(--border);padding-bottom:18px;margin-bottom:20px}
.workspace-head h3{margin:0}
.workspace-head p{margin:3px 0 0;font-size:12px;color:var(--muted)}
.drop{border:1px dashed #9eafbd;border-radius:9px;background:#f7f9fa;text-align:center;padding:28px;margin-top:18px;color:var(--muted);font-size:13px}
.drop.drag{background:#e7eef3;border-color:var(--primary)}
.drop input{display:none}
.file-list{display:flex;gap:10px;flex-wrap:wrap;margin-top:15px}
.file-item{width:90px;height:90px;border-radius:7px;position:relative;overflow:hidden;background:#e8edf1}
.file-item img,.file-item video{width:100%;height:100%;object-fit:cover}
.file-item .remove{position:absolute;top:4px;right:4px;background:#fff;border:0;border-radius:50%;width:22px;height:22px}
.file-audio{height:100%;display:flex;align-items:center;justify-content:center;font-size:12px}
.row{display:grid;grid-template-columns:1fr 1fr;gap:15px}
.actions{display:flex;justify-content:flex-end;gap:10px;margin-top:22px;flex-wrap:wrap}
.archive{background:#e8edf1}
.archive-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(235px,1fr));gap:18px}
.day-card{background:#fff;border:1px solid var(--border);border-radius:10px;overflow:hidden;cursor:pointer;transition:.2s}
.day-card:hover{transform:translateY(-4px);box-shadow:0 12px 25px #20384b16}
.day-cover{height:155px;background:#526d82;display:flex;align-items:center;justify-content:center;color:white;font-size:38px;background-size:cover;background-position:center}
.day-info{padding:17px}
.day-info h3{font-size:17px;margin:0 0 5px}
.day-info p{font-size:11px;color:var(--muted);margin:0}
.day-preview{font-size:12px;margin-top:10px;color:#536474}
footer{padding:28px 6%;text-align:center;background:#fff;color:var(--muted);font-size:11px;border-top:1px solid var(--border)}
.modal{position:fixed;inset:0;background:#102234a8;z-index:20;display:none;align-items:center;justify-content:center;padding:20px}
.modal.open{display:flex}
.modal-box{background:white;border-radius:12px;width:100%;max-width:440px;padding:30px;max-height:90vh;overflow:auto;position:relative}
.modal-box.wide{max-width:900px;padding:0}
.close{position:absolute;right:15px;top:12px;border:0;background:#edf1f4;border-radius:6px;width:32px;height:32px;font-size:20px;z-index:2}
.modal-box h2{font-size:26px;letter-spacing:-1px}
.tabs{display:flex;gap:5px;background:#edf1f4;padding:4px;border-radius:7px;margin:20px 0}
.tabs button{flex:1;border:0;background:transparent;padding:9px;border-radius:5px;font-size:12px;font-weight:600}
.tabs button.active{background:#fff;color:var(--primary)}
.memory-layout{display:grid;grid-template-columns:1.1fr .9fr;min-height:480px}
.memory-photo{background:#344f64;min-height:350px;display:flex;align-items:center;justify-content:center;color:white;background-size:cover;background-position:center}
.memory-content{padding:30px;background:#f5f7f8}
.memory-content h2{font-size:30px}
.memory-content p{font-size:13px;white-space:pre-wrap}
.memory-meta{color:var(--muted);font-size:11px;margin-bottom:20px}
.memory-files{display:flex;gap:10px;flex-wrap:wrap;margin-top:15px}
.memory-files img,.memory-files video{max-width:100%;max-height:180px;border-radius:8px}
.toast{position:fixed;bottom:25px;left:50%;transform:translate(-50%,20px);background:#192f41;color:white;padding:12px 20px;border-radius:7px;font-size:12px;opacity:0;transition:.2s;z-index:40;pointer-events:none}
.toast.show{opacity:1;transform:translate(-50%,0)}
@media(max-width:800px){
 .hero-inner{grid-template-columns:1fr;gap:35px}
 .hero{padding-top:65px;padding-bottom:65px}
 .hero-visual{max-width:500px}
 .studio-grid{grid-template-columns:1fr}
 .topbar{padding:0 18px}
 nav{gap:12px}
 section{padding:65px 5%}
}
@media(max-width:520px){
 .topbar{height:65px;gap:12px}
 .logo{font-size:17px}
 nav{display:none}
 h1{letter-spacing:-3px}
 .row{grid-template-columns:1fr;gap:0}
 .memory-layout{grid-template-columns:1fr}
 .memory-photo{min-height:240px}
 .modal-box{padding:23px}
 .folder-list{grid-template-columns:repeat(2,1fr)}
 .hero-visual .visual-card{height:145px}
}
</style>
</head>
<body>

<header class="topbar">
 <a href="#home" class="logo">ArtTech <span>Genesis</span></a>
 <nav>
  <a href="#studio">Рабочее пространство</a>
  <a href="#archive">Дневник</a>
 </nav>
 <div id="userBox"><button class="btn small" onclick="openAuth()">Войти</button></div>
</header>

<section class="hero" id="home">
 <div class="hero-inner">
  <div>
   <div class="eyebrow">GENESIS OPEN MINDS · DIGITAL DIARY</div>
   <h1>ArtTech<br><span>Genesis.</span></h1>
   <p class="hero-description">Личное цифровое пространство для сохранения воспоминаний. Текст, фотографии и музыка объединяются в единую историю, отражающую настроение и атмосферу каждого дня.</p>
   <div class="hero-buttons">
    <button class="btn primary" onclick="goToStudio()">Создать воспоминание</button>
    <button class="btn" onclick="openAuth()">Войти в аккаунт</button>
   </div>
  </div>
  <div class="hero-visual">
   <div class="visual-card"></div>
   <div class="visual-card"></div>
   <div class="visual-card"></div>
   <div class="visual-card"></div>
   <div class="visual-caption">Каждый день — отдельная история. Каждая история — часть вашей жизни.</div>
  </div>
 </div>
</section>

<section class="studio" id="studio">
 <div class="container">
  <div class="section-heading">
   <div class="eyebrow">01 / WORKSPACE</div>
   <h2>Рабочее пространство</h2>
   <p>Создавайте папки, добавляйте материалы и сохраняйте свои воспоминания.</p>
  </div>
  <div class="studio-grid">
   <div class="card">
    <h3>Создать папку</h3>
    <form id="folderForm">
     <label for="folderName">Название папки</label>
     <input id="folderName" maxlength="60" placeholder="Например, Незабываемый день" required>
     <label>Цвет папки</label>
     <div class="palette" id="palette"></div>
     <button class="btn primary full" type="submit">Создать папку</button>
    </form>
    <h3 style="margin-top:30px">Мои папки</h3>
    <div class="folder-list" id="folderList"></div>
   </div>

   <div class="card" id="workspace">
    <div class="empty" id="empty">
     <div class="empty-icon">▤</div>
     <h3>Рабочее пространство пусто</h3>
     <p>Создайте папку, чтобы начать работу с воспоминаниями.</p>
    </div>
    <div id="editor" hidden>
     <div class="workspace-head">
      <div class="folder-icon" id="editorIcon"></div>
      <div><h3 id="editorTitle"></h3><p id="editorDate"></p></div>
     </div>
     <label for="dayText">Описание дня</label>
     <textarea id="dayText" rows="6" placeholder="Опишите события, эмоции, места и людей, которые сделали этот день особенным..."></textarea>
     <div class="drop" id="drop">
      <p><strong>Добавить фотографии, видео или музыку</strong></p>
      <p>Перетащите файлы сюда или выберите их на устройстве.</p>
      <button class="btn small" type="button" id="chooseFiles">Выбрать файлы</button>
      <input type="file" id="fileInput" accept="image/*,video/*,audio/*" multiple>
     </div>
     <div class="file-list" id="fileList"></div>
     <div class="row">
      <div><label for="songUrl">Ссылка на песню</label><input id="songUrl" type="url" placeholder="Ссылка на музыку"></div>
      <div><label for="songInfo">Исполнитель и название</label><input id="songInfo" placeholder="Название композиции"></div>
     </div>
     <div class="row">
      <div><label for="mood">Настроение дня</label>
       <select id="mood"><option value="">Не выбрано</option><option>Спокойствие</option><option>Радость</option><option>Ностальгия</option><option>Вдохновение</option><option>Грусть</option><option>Приключение</option></select>
      </div>
      <div><label for="weather">Атмосфера</label>
       <select id="weather"><option value="">Не выбрано</option><option>Солнечно</option><option>Облачно</option><option>Дождливо</option><option>Снежно</option><option>Вечер</option><option>Ночь</option></select>
      </div>
     </div>
     <div class="actions">
      <button class="btn danger" type="button" onclick="deleteCurrent()">Удалить папку</button>
      <button class="btn primary" type="button" id="saveButton" onclick="saveCurrent()">Сохранить воспоминание</button>
     </div>
    </div>
   </div>
  </div>
 </div>
</section>

<section class="archive" id="archive">
 <div class="container">
  <div class="section-heading">
   <div class="eyebrow">02 / PERSONAL ARCHIVE</div>
   <h2>Мой дневник</h2>
   <p>Все сохранённые воспоминания собраны в одном месте.</p>
  </div>
  <div class="archive-grid" id="archiveGrid">
   <p class="empty">Войдите в аккаунт, чтобы увидеть свои воспоминания.</p>
  </div>
 </div>
</section>

<footer>ArtTech Genesis · Personal Digital Diary</footer>

<div class="modal" id="authModal">
 <div class="modal-box">
  <button class="close" onclick="closeModal('authModal')">×</button>
  <div class="eyebrow">PERSONAL ACCOUNT</div>
  <h2 id="authTitle">Вход в аккаунт</h2>
  <div class="tabs">
   <button id="loginTab" class="active" onclick="switchAuth('login')">Вход</button>
   <button id="registerTab" onclick="switchAuth('register')">Регистрация</button>
  </div>
  <form id="authForm">
   <label for="authName" id="nameLabel" hidden>Имя пользователя</label>
   <input id="authName" placeholder="Ваше имя" hidden>
   <label for="authEmail">Электронная почта</label>
   <input id="authEmail" type="email" placeholder="name@example.com" required>
   <label for="authPassword">Пароль</label>
   <input id="authPassword" type="password" minlength="6" placeholder="Минимум 6 символов" required>
   <button class="btn primary full" type="submit" id="authSubmit">Войти</button>
  </form>
  <p id="authMessage" style="font-size:12px;color:var(--muted);margin-top:14px"></p>
 </div>
</div>

<div class="modal" id="memoryModal">
 <div class="modal-box wide">
  <button class="close" onclick="closeModal('memoryModal')">×</button>
  <div class="memory-layout">
   <div class="memory-photo" id="memoryPhoto">ARTTECH GENESIS</div>
   <div class="memory-content">
    <div class="eyebrow">PERSONAL MEMORY</div>
    <h2 id="memoryTitle"></h2>
    <div class="memory-meta" id="memoryDate"></div>
    <p id="memoryText"></p>
    <p id="memoryMood"></p>
    <p id="memorySong"></p>
    <div class="memory-files" id="memoryFiles"></div>
   </div>
  </div>
 </div>
</div>

<div class="toast" id="toast"></div>

<script>
const SUPABASE_URL = "https://ydrzlazhucdlvvyjisnm.supabase.co";
const SUPABASE_KEY = "sb_publishable_l_aik6ePDy4GFPZRwBH1ZQ_9oSb_Dji";
const supabaseClient = window.supabase.createClient(SUPABASE_URL, SUPABASE_KEY);

const $ = selector => document.querySelector(selector);
const colors = ["#29465f","#426d8e","#647b8b","#52645b","#766b61","#6c6d80","#384d58","#8a765f"];

let selectedColor = colors[0];
let currentUser = null;
let folders = [];
let currentId = null;
let currentFiles = [];
let authMode = "login";

function toast(message) {
 const element = $("#toast");
 element.textContent = message;
 element.classList.add("show");
 setTimeout(() => element.classList.remove("show"), 2500);
}

function escapeHTML(value) {
 return String(value || "").replace(/[&<>"']/g, char => ({
  "&":"&amp;","<":"&lt;",">":"&gt;",'"':"&quot;","'":"&#39;"
 }[char]));
}

function formatDate(date) {
 return new Date(date).toLocaleDateString("ru-RU", {
  day:"numeric",month:"long",year:"numeric"
 });
}

function initPalette() {
 $("#palette").innerHTML = colors.map((color,index) =>
  `<button type="button" class="color ${index===0?"active":""}" style="background:${color}" data-color="${color}" aria-label="Цвет ${index+1}"></button>`
 ).join("");
}

$("#palette").addEventListener("click", event => {
 const button = event.target.closest("[data-color]");
 if (!button) return;
 selectedColor = button.dataset.color;
 document.querySelectorAll(".color").forEach(item =>
  item.classList.toggle("active", item === button)
 );
});

function goToStudio() {
 if (!currentUser) {
  openAuth();
  return;
 }
 $("#studio").scrollIntoView({behavior:"smooth"});
}

async function loadMemories() {
 if (!currentUser) return;
 const {data,error} = await supabaseClient
  .from("memories")
  .select("*")
  .order("created_at",{ascending:false});

 if (error) {
  toast("Не удалось загрузить воспоминания");
  console.error(error);
  return;
 }

 folders = data || [];
 renderFolders();
 renderArchive();
 if (currentId) {
  const selected = folders.find(item => item.id === currentId);
  if (selected) openFolder(selected.id);
  else openFolder(null);
 }
}

function renderFolders() {
 $("#folderList").innerHTML = folders.length
  ? folders.map(folder => `
   <div class="folder-item ${folder.id===currentId?"active":""}" data-id="${folder.id}">
    <div class="folder-icon" style="--folder-color:${escapeHTML(folder.color)}"></div>
    <strong>${escapeHTML(folder.name)}</strong>
    <small>${formatDate(folder.created_at)}</small>
   </div>
  `).join("")
  : '<p style="font-size:12px;color:var(--muted)">Папок пока нет.</p>';
}

async function getFileUrl(path) {
 const {data,error} = await supabaseClient.storage
  .from("memory-files")
  .createSignedUrl(path,3600);

 if (error) {
  console.error(error);
  return "";
 }
 return data.signedUrl;
}

async function renderArchive() {
 const saved = folders;
 if (!currentUser) {
  $("#archiveGrid").innerHTML = '<p class="empty">Войдите в аккаунт, чтобы увидеть свои воспоминания.</p>';
  return;
 }

 if (!saved.length) {
  $("#archiveGrid").innerHTML = '<p class="empty">Пока здесь нет сохранённых воспоминаний.</p>';
  return;
 }

 const cards = await Promise.all(saved.map(async folder => {
  const photo = (folder.files || []).find(file => file.type?.startsWith("image/"));
  const imageUrl = photo ? await getFileUrl(photo.path) : "";
  return `
   <article class="day-card" data-memory="${folder.id}">
    <div class="day-cover" style="${imageUrl ? `background-image:url('${imageUrl}')` : `background-color:${escapeHTML(folder.color)}`}">${imageUrl ? "" : "▤"}</div>
    <div class="day-info">
     <h3>${escapeHTML(folder.name)}</h3>
     <p>${formatDate(folder.created_at)}</p>
     <div class="day-preview">${escapeHTML((folder.description || "Воспоминание").slice(0,100))}</div>
    </div>
   </article>
  `;
 }));
 $("#archiveGrid").innerHTML = cards.join("");
}

async function openFolder(id) {
 currentId = id;
 const folder = folders.find(item => item.id === id);
 $("#empty").hidden = !!folder;
 $("#editor").hidden = !folder;

 if (!folder) {
  currentFiles = [];
  renderFolders();
  return;
 }

 $("#editorTitle").textContent = folder.name;
 $("#editorDate").textContent = formatDate(folder.created_at);
 $("#editorIcon").style.setProperty("--folder-color",folder.color);
 $("#dayText").value = folder.description || "";
 $("#songUrl").value = folder.song_url || "";
 $("#songInfo").value = folder.song_info || "";
 $("#mood").value = folder.mood || "";
 $("#weather").value = folder.weather || "";

 currentFiles = await Promise.all((folder.files || []).map(async file => ({
  ...file,
  url: await getFileUrl(file.path)
 })));

 renderFiles();
 renderFolders();
}

function renderFiles() {
 $("#fileList").innerHTML = currentFiles.map((file,index) => {
  let content = "";
  if (file.type.startsWith("image/")) {
   content = `<img src="${file.url || file.preview}" alt="">`;
  } else if (file.type.startsWith("video/")) {
   content = `<video src="${file.url || file.preview}"></video>`;
  } else {
   content = '<div class="file-audio">♫ AUDIO</div>';
  }

  return `<div class="file-item">${content}<button class="remove" data-remove="${index}" type="button">×</button></div>`;
 }).join("");
}

$("#folderList").addEventListener("click",event => {
 const item = event.target.closest("[data-id]");
 if (item) openFolder(item.dataset.id);
});

$("#folderForm").addEventListener("submit",async event => {
 event.preventDefault();
 if (!currentUser) {
  openAuth();
  return;
 }

 const name = $("#folderName").value.trim();
 if (!name) return;

 const {data,error} = await supabaseClient
  .from("memories")
  .insert({
   user_id:currentUser.id,
   name,
   color:selectedColor
  })
  .select()
  .single();

 if (error) {
  toast("Не удалось создать папку");
  console.error(error);
  return;
 }

 folders.unshift(data);
 $("#folderName").value = "";
 openFolder(data.id);
 renderArchive();
 toast("Папка создана");
});

$("#chooseFiles").onclick = () => $("#fileInput").click();
$("#fileInput").addEventListener("change",event => addFiles(event.target.files));

async function addFiles(files) {
 for (const file of files) {
  if (file.size > 25 * 1024 * 1024) {
   toast("Файл больше 25 МБ");
   continue;
  }

  currentFiles.push({
   name:file.name,
   type:file.type || "application/octet-stream",
   file,
   preview:URL.createObjectURL(file),
   pending:true
  });
 }

 renderFiles();
 $("#fileInput").value = "";
}

$("#fileList").addEventListener("click",async event => {
 const button = event.target.closest("[data-remove]");
 if (!button) return;

 const index = Number(button.dataset.remove);
 const file = currentFiles[index];

 if (file.path) {
  const {error} = await supabaseClient.storage
   .from("memory-files")
   .remove([file.path]);

  if (error) {
   toast("Не удалось удалить файл");
   console.error(error);
   return;
  }
 }

 if (file.preview) URL.revokeObjectURL(file.preview);
 currentFiles.splice(index,1);
 renderFiles();
});

const drop = $("#drop");
drop.addEventListener("dragover",event => {
 event.preventDefault();
 drop.classList.add("drag");
});
drop.addEventListener("dragleave",() => drop.classList.remove("drag"));
drop.addEventListener("drop",event => {
 event.preventDefault();
 drop.classList.remove("drag");
 addFiles(event.dataTransfer.files);
});

async function saveCurrent() {
 const folder = folders.find(item => item.id === currentId);
 if (!folder) return;

 const saveButton = $("#saveButton");
 saveButton.disabled = true;
 saveButton.textContent = "Сохранение...";

 try {
  const filesToSave = [];

  for (const item of currentFiles) {
   if (item.pending && item.file) {
    const safeName = item.file.name.replace(/[^a-zA-Z0-9._-]/g,"_");
    const path = `${currentUser.id}/${folder.id}/${crypto.randomUUID()}-${safeName}`;

    const {error:uploadError} = await supabaseClient.storage
     .from("memory-files")
     .upload(path,item.file,{upsert:false});

    if (uploadError) throw uploadError;

    filesToSave.push({
     name:item.name,
     type:item.type,
     path
    });
   } else if (item.path) {
    filesToSave.push({
     name:item.name,
     type:item.type,
     path:item.path
    });
   }
  }

  const updates = {
   description:$("#dayText").value,
   song_url:$("#songUrl").value,
   song_info:$("#songInfo").value,
   mood:$("#mood").value,
   weather:$("#weather").value,
   files:filesToSave
  };

  const {error} = await supabaseClient
   .from("memories")
   .update(updates)
   .eq("id",folder.id);

  if (error) throw error;

  Object.assign(folder,updates);
  currentFiles = await Promise.all(filesToSave.map(async file => ({
   ...file,
   url:await getFileUrl(file.path)
  })));

  renderFiles();
  renderFolders();
  renderArchive();
  toast("Воспоминание сохранено");
 } catch(error) {
  console.error(error);
  toast("Ошибка сохранения. Проверьте подключение.");
 } finally {
  saveButton.disabled = false;
  saveButton.textContent = "Сохранить воспоминание";
 }
}

async function deleteCurrent() {
 if (!currentId || !confirm("Удалить эту папку и её содержимое?")) return;

 const folder = folders.find(item => item.id === currentId);
 if (folder?.files?.length) {
  const paths = folder.files.map(file => file.path);
  const {error:storageError} = await supabaseClient.storage
   .from("memory-files")
   .remove(paths);

  if (storageError) {
   toast("Не удалось удалить файлы");
   console.error(storageError);
   return;
  }
 }

 const {error} = await supabaseClient
  .from("memories")
  .delete()
  .eq("id",currentId);

 if (error) {
  toast("Не удалось удалить папку");
  console.error(error);
  return;
 }

 folders = folders.filter(item => item.id !== currentId);
 currentId = null;
 openFolder(null);
 renderFolders();
 renderArchive();
 toast("Папка удалена");
}

$("#archiveGrid").addEventListener("click",async event => {
 const card = event.target.closest("[data-memory]");
 if (!card) return;

 const folder = folders.find(item => item.id === card.dataset.memory);
 if (!folder) return;

 $("#memoryTitle").textContent = folder.name;
 $("#memoryDate").textContent = formatDate(folder.created_at);
 $("#memoryText").textContent = folder.description || "Описание отсутствует.";
 $("#memoryMood").textContent = folder.mood ? "Настроение: " + folder.mood : "";
 $("#memorySong").textContent = folder.song_info ? "Музыка: " + folder.song_info : "";

 const photo = (folder.files || []).find(file => file.type.startsWith("image/"));
 const photoUrl = photo ? await getFileUrl(photo.path) : "";
 $("#memoryPhoto").style.backgroundImage = photoUrl ? `url("${photoUrl}")` : "";
 $("#memoryPhoto").textContent = photoUrl ? "" : "ARTTECH GENESIS";

 const media = await Promise.all((folder.files || []).map(async file => {
  const url = await getFileUrl(file.path);
  if (file.type.startsWith("image/")) return `<img src="${url}" alt="">`;
  if (file.type.startsWith("video/")) return `<video src="${url}" controls></video>`;
  if (file.type.startsWith("audio/")) return `<audio src="${url}" controls></audio>`;
  return "";
 }));

 const song = folder.song_url
  ? `<a href="${escapeHTML(folder.song_url)}" target="_blank" rel="noopener" class="btn small">Открыть музыку</a>`
  : "";

 $("#memoryFiles").innerHTML = media.join("") + song;
 $("#memoryModal").classList.add("open");
});

function openAuth() {
 switchAuth("login");
 $("#authModal").classList.add("open");
}

function closeModal(id) {
 $("#"+id).classList.remove("open");
}

function switchAuth(mode) {
 authMode = mode;
 $("#loginTab").classList.toggle("active",mode==="login");
 $("#registerTab").classList.toggle("active",mode==="register");
 $("#authTitle").textContent = mode==="login" ? "Вход в аккаунт" : "Создание аккаунта";
 $("#nameLabel").hidden = mode!=="register";
 $("#authName").hidden = mode!=="register";
 $("#authName").required = mode==="register";
 $("#authSubmit").textContent = mode==="login" ? "Войти" : "Зарегистрироваться";
 $("#authMessage").textContent = "";
}

$("#authForm").addEventListener("submit",async event => {
 event.preventDefault();

 const email = $("#authEmail").value.trim().toLowerCase();
 const password = $("#authPassword").value;
 const message = $("#authMessage");
 const submit = $("#authSubmit");

 submit.disabled = true;
 submit.textContent = "Подождите...";

 try {
  if (authMode === "register") {
   const name = $("#authName").value.trim();
   if (!name) throw new Error("Введите имя");

   const {data,error} = await supabaseClient.auth.signUp({
    email,
    password,
    options:{data:{name}}
   });

   if (error) throw error;

   if (!data.session) {
    message.textContent = "Аккаунт создан. Проверьте почту и подтвердите регистрацию.";
    return;
   }
  } else {
   const {error} = await supabaseClient.auth.signInWithPassword({
    email,
    password
   });
   if (error) throw error;
  }

  closeModal("authModal");
  toast("Вы вошли в аккаунт");
 } catch(error) {
  message.textContent = error.message || "Произошла ошибка";
 } finally {
  submit.disabled = false;
  submit.textContent = authMode==="login" ? "Войти" : "Зарегистрироваться";
 }
});

async function logout() {
 await supabaseClient.auth.signOut();
 currentUser = null;
 folders = [];
 currentId = null;
 currentFiles = [];
 updateUser();
 renderFolders();
 renderArchive();
 openFolder(null);
 toast("Вы вышли из аккаунта");
}

function updateUser() {
 $("#userBox").innerHTML = currentUser
  ? `<span style="font-weight:600">${escapeHTML(currentUser.user_metadata?.name || currentUser.email)}</span><button class="btn small" onclick="logout()">Выйти</button>`
  : '<button class="btn small" onclick="openAuth()">Войти</button>';
}

supabaseClient.auth.onAuthStateChange(async (event,session) => {
 currentUser = session?.user || null;
 updateUser();

 if (currentUser) {
  await loadMemories();
 } else {
  folders = [];
  currentId = null;
  renderFolders();
  renderArchive();
  openFolder(null);
 }
});

document.querySelectorAll(".modal").forEach(modal => {
 modal.addEventListener("click",event => {
  if (event.target === modal) modal.classList.remove("open");
 });
});

async function startApp() {
 initPalette();
 const {data,error} = await supabaseClient.auth.getSession();

 if (error) {
  console.error(error);
  toast("Не удалось проверить аккаунт");
 }

 currentUser = data?.session?.user || null;
 updateUser();

 if (currentUser) await loadMemories();
 else {
  renderFolders();
  renderArchive();
 }
}

startApp();
</script>
</body>
</html>
