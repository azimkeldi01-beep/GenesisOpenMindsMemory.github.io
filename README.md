
<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<meta name="theme-color" content="#4263eb">
<title>Genesis — Open Minds Memory</title>
<script src="https://cdn.jsdelivr.net/npm/@supabase/supabase-js@2"></script>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&display=swap" rel="stylesheet">

<style>
:root{
 --primary:#4263eb;
 --primary-dark:#304fc5;
 --lime:#c8f169;
 --bg:#f5f7fb;
 --surface:#fff;
 --text:#182238;
 --muted:#8490a5;
 --border:#e8edf4;
 --shadow:0 8px 30px rgba(35,55,90,.06);
}
*{box-sizing:border-box}
body{margin:0;background:var(--bg);color:var(--text);font-family:Inter,Arial,sans-serif}
button,input,textarea,select{font:inherit}
button{cursor:pointer}
button:disabled{opacity:.55;cursor:not-allowed}
.hidden,[hidden]{display:none!important}
.container{width:min(1180px,calc(100% - 36px));margin:auto}

header{
 background:#ffffffed;
 border-bottom:1px solid var(--border);
 position:sticky;
 top:0;
 z-index:10;
 backdrop-filter:blur(12px)
}
.nav{
 min-height:72px;
 display:flex;
 align-items:center;
 justify-content:space-between;
 gap:15px
}
.brand{
 font-weight:800;
 font-size:21px;
 letter-spacing:-1px;
 text-decoration:none;
 color:var(--text)
}
.brand span{color:var(--primary)}
.nav-right{display:flex;align-items:center;gap:12px}
.user-email{
 font-size:12px;
 color:var(--muted);
 max-width:180px;
 overflow:hidden;
 text-overflow:ellipsis
}

.btn{
 border:1px solid var(--border);
 background:#fff;
 color:var(--text);
 padding:11px 17px;
 border-radius:10px;
 font-size:13px;
 font-weight:650;
 transition:.2s
}
.btn:hover{transform:translateY(-1px);background:#f0f3f8}
.btn.primary{background:var(--primary);border-color:var(--primary);color:#fff}
.btn.primary:hover{background:var(--primary-dark)}
.btn.lime{background:var(--lime);border-color:var(--lime);color:#26351a}
.btn.danger{color:#bd4a4a}
.btn.small{padding:8px 12px;font-size:12px}
.btn.full{width:100%;margin-top:12px}

.hero{
 padding:75px 0;
 background:linear-gradient(120deg,#3456d9,#5477f4);
 color:#fff;
 overflow:hidden
}
.hero-inner{
 display:grid;
 grid-template-columns:1.2fr .8fr;
 align-items:center;
 gap:40px
}
.eyebrow{font-size:10px;letter-spacing:2px;font-weight:800;opacity:.75}
.hero h1{
 font-size:clamp(36px,6vw,65px);
 line-height:1.05;
 margin:18px 0;
 letter-spacing:-3px
}
.hero p{max-width:570px;color:#e4eaff;line-height:1.8;font-size:14px}
.hero-buttons{display:flex;gap:10px;flex-wrap:wrap;margin-top:25px}
.hero-art{
 display:grid;
 grid-template-columns:1fr 1fr;
 gap:12px;
 transform:rotate(-3deg)
}
.art-card{
 height:150px;
 border-radius:18px;
 background:linear-gradient(140deg,#d8e4ff,#9cb4ff);
 box-shadow:0 15px 35px #172e7c30
}
.art-card:nth-child(2){background:linear-gradient(140deg,#c8f169,#91b947);margin-top:25px}
.art-card:nth-child(3){background:linear-gradient(140deg,#b9caff,#738ee8);margin-top:-15px}
.art-card:nth-child(4){background:linear-gradient(140deg,#f0f3ff,#b9c8f6)}

section{padding:55px 0}
.section-title{margin-bottom:25px}
.section-title h2{
 font-size:clamp(27px,4vw,38px);
 letter-spacing:-1.5px;
 margin:8px 0
}
.section-title p{font-size:13px;color:var(--muted)}
.eyebrow.blue{color:var(--primary);opacity:1}

.card{
 background:var(--surface);
 border:1px solid var(--border);
 border-radius:18px;
 padding:22px;
 box-shadow:var(--shadow);
 min-width:0
}
.card h3{font-size:17px;margin:0 0 15px}

label{display:block;font-size:12px;font-weight:650;margin:14px 0 7px}
input,textarea,select{
 width:100%;
 padding:12px;
 border:1px solid var(--border);
 border-radius:10px;
 background:#fff;
 color:var(--text);
 font-size:13px;
 outline:none
}
input:focus,textarea:focus,select:focus{
 border-color:var(--primary);
 box-shadow:0 0 0 3px #4263eb18
}
textarea{min-height:120px;resize:vertical}

.palette{display:flex;gap:10px;flex-wrap:wrap;margin:12px 0}
.color{
 width:28px;
 height:28px;
 border-radius:50%;
 border:2px solid white;
 outline:1px solid var(--border);
 padding:0
}
.color.active{outline:2px solid var(--primary)}

.folder-list{
 display:grid;
 grid-template-columns:repeat(2,minmax(0,1fr));
 gap:10px;
 margin-top:15px
}
.folder-item{
 border:1px solid var(--border);
 border-radius:12px;
 padding:15px 8px;
 text-align:center;
 cursor:pointer;
 min-width:0;
 background:#fff;
 transition:.2s
}
.folder-item:hover{
 border-color:var(--primary);
 background:#f1f4ff;
 transform:translateY(-2px)
}
.folder-icon{
 width:42px;
 height:30px;
 border-radius:5px;
 background:var(--folder-color);
 margin:0 auto 9px;
 position:relative
}
.folder-icon:before{
 content:"";
 position:absolute;
 top:-5px;
 left:0;
 width:18px;
 height:8px;
 background:inherit;
 border-radius:4px 4px 0 0
}
.folder-item strong{
 font-size:11px;
 display:block;
 overflow-wrap:anywhere
}
.folder-item small{font-size:10px;color:var(--muted)}

.notice{
 padding:18px;
 background:#f2f5fc;
 border:1px solid var(--border);
 border-radius:12px;
 color:var(--muted);
 font-size:13px;
 text-align:center
}
.empty{text-align:center;padding:35px 15px;color:var(--muted)}
.empty-icon{font-size:38px;margin-bottom:10px}

.archive{background:#edf1f8}
.archive-grid{
 display:grid;
 grid-template-columns:repeat(auto-fill,minmax(220px,1fr));
 gap:16px
}
.day-card{
 background:#fff;
 border:1px solid var(--border);
 border-radius:14px;
 overflow:hidden;
 cursor:pointer;
 transition:.2s
}
.day-card:hover{transform:translateY(-3px);box-shadow:var(--shadow)}
.day-cover{
 height:135px;
 background:var(--cover-color,#4263eb);
 display:grid;
 place-items:center;
 color:#fff;
 font-size:35px;
 background-size:cover;
 background-position:center
}
.day-info{padding:15px}
.day-info h3{
 font-size:15px;
 margin:0 0 5px;
 overflow-wrap:anywhere
}
.day-info small{font-size:10px;color:var(--muted)}
.day-info p{
 font-size:12px;
 color:#65718a;
 margin:9px 0 0;
 overflow-wrap:anywhere
}

footer{text-align:center;padding:25px;color:var(--muted);font-size:11px;background:#fff}

/* ОКНО ПАПКИ */
.modal{
 position:fixed;
 inset:0;
 background:#101b35b8;
 z-index:30;
 display:none;
 align-items:center;
 justify-content:center;
 padding:18px;
 backdrop-filter:blur(5px)
}
.modal.open{display:flex}
.modal-box{
 width:min(440px,100%);
 max-height:92vh;
 overflow:auto;
 background:#fff;
 border-radius:18px;
 padding:25px;
 position:relative
}
.modal-box.wide{
 width:min(850px,100%);
 padding:0
}
.close{
 position:absolute;
 right:14px;
 top:14px;
 border:0;
 background:#edf1f8;
 border-radius:9px;
 width:36px;
 height:36px;
 font-size:23px;
 z-index:5;
 color:var(--text)
}
.close:hover{background:#e1e7f2}
.folder-modal-header{
 padding:25px 65px 20px 25px;
 border-bottom:1px solid var(--border);
 display:flex;
 align-items:center;
 gap:15px
}
.folder-modal-header .folder-icon{flex-shrink:0;margin:0}
.folder-modal-header h2{font-size:21px;margin:0;overflow-wrap:anywhere}
.folder-modal-header p{font-size:11px;color:var(--muted);margin:5px 0 0}
.folder-modal-body{padding:25px}
.drop{
 border:1px dashed #aab6ca;
 border-radius:12px;
 padding:22px;
 text-align:center;
 background:#f8f9fc;
 margin-top:15px;
 color:var(--muted);
 font-size:12px
}
.drop input{display:none}
.file-list{display:flex;gap:9px;flex-wrap:wrap;margin-top:12px}
.file-item{
 background:#edf1fa;
 border-radius:9px;
 padding:9px 10px;
 font-size:11px;
 max-width:100%;
 overflow-wrap:anywhere
}
.file-item button{
 border:0;
 background:none;
 color:#c44;
 margin-left:7px;
 font-size:15px
}
.row{display:grid;grid-template-columns:1fr 1fr;gap:12px}
.actions{
 display:flex;
 justify-content:space-between;
 gap:10px;
 flex-wrap:wrap;
 margin-top:20px
}
.status{font-size:12px;color:var(--muted);min-height:18px;margin:12px 0}
.status.error{color:#bd4a4a}
.status.success{color:#39815e}

.tabs{display:flex;background:#edf1f8;border-radius:10px;padding:4px;margin:17px 0}
.tabs button{
 flex:1;
 border:0;
 background:none;
 padding:9px;
 border-radius:8px;
 font-size:12px
}
.tabs button.active{background:#fff;color:var(--primary);font-weight:700}

.toast{
 position:fixed;
 bottom:20px;
 left:50%;
 transform:translate(-50%,20px);
 background:#182238;
 color:#fff;
 padding:12px 18px;
 border-radius:10px;
 font-size:12px;
 opacity:0;
 transition:.2s;
 z-index:50;
 pointer-events:none;
 max-width:90%;
 text-align:center
}
.toast.show{opacity:1;transform:translate(-50%,0)}

@media(max-width:800px){
 .hero-inner{grid-template-columns:1fr}
 .hero-art{max-width:420px}
}
@media(max-width:550px){
 .nav{min-height:65px}
 .brand{font-size:17px}
 .user-email{max-width:100px}
 .hero{padding:50px 0}
 .hero h1{letter-spacing:-2px}
 .art-card{height:110px}
 .row{grid-template-columns:1fr;gap:0}
 .folder-modal-body{padding:17px}
 .folder-modal-header{padding:20px 60px 17px 17px}
 .modal{padding:8px}
 .modal-box.wide{max-height:96vh}
 .card{padding:16px}
 .actions .btn{flex:1}
 .archive-grid{grid-template-columns:1fr 1fr}
 .day-cover{height:105px}
 .day-info{padding:11px}
}
@media(max-width:350px){
 .archive-grid{grid-template-columns:1fr}
}
</style>
</head>

<body>

<header>
 <div class="container nav">
  <a class="brand" href="#home">GENESIS<span>✦</span></a>
  <div class="nav-right" id="userBox">
   <button class="btn small" onclick="openAuth('login')">Войти</button>
  </div>
 </div>
</header>

<section class="hero" id="home">
 <div class="container hero-inner">
  <div>
   <div class="eyebrow">GENESIS OPEN MINDS · DIGITAL MEMORY</div>
   <h1>Твои моменты.<br>Твоя история.</h1>
   <p>Личное облачное пространство для воспоминаний. Сохраняй фотографии, тексты, музыку и важные моменты своей жизни в одном месте.</p>
   <div class="hero-buttons">
    <button class="btn lime" onclick="goToWorkspace()">Создать воспоминание</button>
    <button class="btn" onclick="openAuth('register')">Создать аккаунт</button>
   </div>
  </div>
  <div class="hero-art">
   <div class="art-card"></div>
   <div class="art-card"></div>
   <div class="art-card"></div>
   <div class="art-card"></div>
  </div>
 </div>
</section>

<!-- СОЗДАНИЕ ПАПОК -->
<section id="studio">
 <div class="container">

  <div id="signedOutNotice" class="notice">
   Чтобы пользоваться пространством, войди или зарегистрируйся.
   <button class="btn primary small" onclick="openAuth('login')">Войти</button>
  </div>

  <div id="privateStudio" hidden>
   <div class="card" style="max-width:850px;margin:auto">
    <h3>＋ Создать новую папку</h3>

    <form id="folderForm">
     <label for="folderName">Название папки</label>
     <input id="folderName" maxlength="60" placeholder="Например, Лето 2026" required>

     <label>Цвет папки</label>
     <div class="palette" id="palette"></div>

     <button class="btn primary" id="createFolderBtn" type="submit">＋ Создать папку</button>
    </form>

    <div style="display:flex;align-items:center;justify-content:space-between;gap:10px;margin-top:30px">
     <h3 style="margin:0">Мои папки</h3>
     <span id="folderCount" style="font-size:11px;color:var(--muted)">0 папок</span>
    </div>

    <div class="folder-list" id="folderList"></div>
   </div>
  </div>

 </div>
</section>

<!-- ДНЕВНИК -->
<section class="archive" id="archive">
 <div class="container">
  <div class="section-title">
   <div class="eyebrow blue">PERSONAL ARCHIVE</div>
   <h2>Мой дневник</h2>
   <p>Все твои папки и сохранённые воспоминания в одном месте.</p>
  </div>

  <div id="archiveSignedOut" class="notice">
   Дневник доступен после входа в аккаунт.
   <button class="btn primary small" onclick="openAuth('login')">Войти</button>
  </div>

  <div class="archive-grid" id="archiveGrid" hidden></div>
 </div>
</section>

<footer>GENESIS · OPEN MINDS MEMORY</footer>

<!-- ОКНО РЕДАКТИРОВАНИЯ ПАПКИ -->
<div class="modal" id="folderModal">
 <div class="modal-box wide">

  <button class="close" type="button" onclick="closeFolder()">×</button>

  <div class="folder-modal-header">
   <div class="folder-icon" id="editorIcon"></div>
   <div>
    <h2 id="editorTitle">Название папки</h2>
    <p id="editorDate"></p>
   </div>
  </div>

  <div class="folder-modal-body">

   <label for="dayText">Описание воспоминания</label>
   <textarea id="dayText" maxlength="10000" placeholder="Расскажи, что произошло..."></textarea>

   <div class="drop" id="drop">
    <p><b>Добавить фотографии, видео или аудио</b></p>
    <p>Выбери файлы со своего устройства. Максимальный размер — 25 МБ на файл.</p>
    <button class="btn small" type="button" id="chooseFiles">Выбрать файлы</button>
    <input type="file" id="fileInput" accept="image/*,video/*,audio/*" multiple>
   </div>

   <div class="file-list" id="fileList"></div>

   <div class="row">
    <div>
     <label for="songUrl">Ссылка на музыку</label>
     <input id="songUrl" type="url" placeholder="https://...">
    </div>
    <div>
     <label for="songInfo">Название и исполнитель</label>
     <input id="songInfo" maxlength="180" placeholder="Название песни">
    </div>
   </div>

   <div class="row">
    <div>
     <label for="mood">Настроение</label>
     <select id="mood">
      <option value="">Не выбрано</option>
      <option>Радость</option>
      <option>Спокойствие</option>
      <option>Ностальгия</option>
      <option>Вдохновение</option>
      <option>Грусть</option>
      <option>Приключение</option>
     </select>
    </div>

    <div>
     <label for="weather">Атмосфера</label>
     <select id="weather">
      <option value="">Не выбрано</option>
      <option>Солнечно</option>
      <option>Облачно</option>
      <option>Дождливо</option>
      <option>Снежно</option>
      <option>Вечер</option>
      <option>Ночь</option>
     </select>
    </div>
   </div>

   <p class="status" id="saveStatus" aria-live="polite"></p>

   <div class="actions">
    <button class="btn danger" type="button" onclick="deleteCurrent()">Удалить папку</button>
    <button class="btn primary" type="button" id="saveBtn" onclick="saveCurrent()">Сохранить воспоминание</button>
   </div>

  </div>
 </div>
</div>

<!-- АВТОРИЗАЦИЯ -->
<div class="modal" id="authModal">
 <div class="modal-box">
  <button class="close" onclick="closeModal('authModal')">×</button>

  <div class="eyebrow blue">PERSONAL ACCOUNT</div>
  <h2 id="authTitle">Вход в аккаунт</h2>

  <div class="tabs">
   <button id="loginTab" class="active" type="button" onclick="switchAuth('login')">Вход</button>
   <button id="registerTab" type="button" onclick="switchAuth('register')">Регистрация</button>
  </div>

  <form id="authForm">
   <div id="nameField" hidden>
    <label for="authName">Имя</label>
    <input id="authName" maxlength="60" placeholder="Твоё имя">
   </div>

   <label for="authEmail">Электронная почта</label>
   <input id="authEmail" type="email" required placeholder="name@example.com">

   <label for="authPassword">Пароль</label>
   <input id="authPassword" type="password" minlength="8" required placeholder="Не менее 8 символов">

   <button class="btn primary full" id="authSubmit" type="submit">Войти</button>
  </form>

  <p class="status" id="authMessage"></p>
  <p style="font-size:11px;color:var(--muted)">При регистрации может потребоваться подтверждение электронной почты.</p>
 </div>
</div>

<div class="toast" id="toast"></div>

<script>
/* SUPABASE */
const SUPABASE_URL = "https://ydrzlazhucdlvvyjisnm.supabase.co";
const SUPABASE_KEY = "sb_publishable_l_aik6ePDy4GFPZRwBH1ZQ_9oSb_Dji";
const BUCKET = "memory-files";
const MAX_FILE_SIZE = 25 * 1024 * 1024;

const $ = s => document.querySelector(s);

const colors = [
 "#4263eb","#8c70d6","#55a58a","#e2a44b",
 "#df758b","#607d9e","#87954c","#526078"
];

let db = null;
let currentUser = null;
let folders = [];
let currentId = null;
let currentFiles = [];
let selectedColor = colors[0];
let authMode = "login";
let busy = false;
let toastTimer = null;

function toast(message){
 const el=$("#toast");
 el.textContent=message;
 el.classList.add("show");
 clearTimeout(toastTimer);
 toastTimer=setTimeout(()=>el.classList.remove("show"),3200);
}

function status(el,message,type=""){
 el.textContent=message;
 el.className="status"+(type?" "+type:"");
}

function escapeHTML(value){
 return String(value??"").replace(/[&<>"']/g,c=>({
  "&":"&amp;",
  "<":"&lt;",
  ">":"&gt;",
  '"':"&quot;",
  "'":"&#39;"
 }[c]));
}

function formatDate(value){
 const d=new Date(value);
 if(Number.isNaN(d.getTime()))return "";
 return d.toLocaleDateString("ru-RU",{
  day:"numeric",
  month:"long",
  year:"numeric"
 });
}

function setBusy(value){
 busy=value;
 ["#authSubmit","#createFolderBtn","#saveBtn"].forEach(s=>{
  const el=$(s);
  if(el)el.disabled=value;
 });
}

function requireAuth(){
 if(!currentUser){
  toast("Сначала войди в аккаунт.");
  openAuth("login");
  return false;
 }
 return true;
}

/* ЦВЕТА ПАПОК */
function initPalette(){
 $("#palette").innerHTML=colors.map((c,i)=>`
  <button type="button"
   class="color ${i===0?"active":""}"
   style="background:${c}"
   data-color="${c}"
   aria-label="Цвет ${i+1}">
  </button>
 `).join("");
}

$("#palette").addEventListener("click",e=>{
 const b=e.target.closest("[data-color]");
 if(!b)return;

 selectedColor=b.dataset.color;

 document.querySelectorAll(".color").forEach(x=>{
  x.classList.toggle("active",x===b);
 });
});

/* ИНТЕРФЕЙС */
function updateInterface(){
 const signedIn=!!currentUser;

 $("#signedOutNotice").hidden=signedIn;
 $("#privateStudio").hidden=!signedIn;
 $("#archiveSignedOut").hidden=signedIn;
 $("#archiveGrid").hidden=!signedIn;

 if(signedIn){
  $("#userBox").innerHTML=`
   <span class="user-email">${escapeHTML(currentUser.email)}</span>
   <button class="btn small" onclick="logout()">Выйти</button>
  `;
 }else{
  $("#userBox").innerHTML=`
   <button class="btn small" onclick="openAuth('login')">Войти</button>
  `;

  folders=[];
  currentId=null;
  currentFiles=[];

  closeFolder();
  renderFolders();
  renderArchive();
 }
}

function goToWorkspace(){
 $("#studio").scrollIntoView({behavior:"smooth"});
 if(!currentUser)openAuth("login");
}

/* ОТОБРАЖЕНИЕ ПАПОК */
function renderFolders(){
 const target=$("#folderList");

 $("#folderCount").textContent=
  folders.length+" "+(folders.length===1?"папка":"папок");

 if(!folders.length){
  target.innerHTML=`
   <p style="font-size:12px;color:var(--muted)">
    Папок пока нет. Создай свою первую папку!
   </p>
  `;
  return;
 }

 target.innerHTML=folders.map(f=>`
  <div class="folder-item"
   data-id="${escapeHTML(f.id)}"
   tabindex="0"
   role="button">

   <div class="folder-icon"
    style="--folder-color:${escapeHTML(f.color||colors[0])}">
   </div>

   <strong>${escapeHTML(f.name)}</strong>
   <small>${formatDate(f.created_at)}</small>
  </div>
 `).join("");
}

/* ДНЕВНИК */
function renderArchive(){
 const target=$("#archiveGrid");

 if(!folders.length){
  target.innerHTML=`
   <p class="empty">
    Твой дневник пока пуст. Создай первую папку!
   </p>
  `;
  return;
 }

 target.innerHTML=folders.map(f=>{
  const files=Array.isArray(f.files)?f.files:[];
  const photo=files.find(x=>(x.type||"").startsWith("image/"));

  return `
   <article class="day-card"
    data-memory="${escapeHTML(f.id)}"
    tabindex="0"
    role="button">

    <div class="day-cover"
     data-cover="${escapeHTML(f.id)}"
     style="--cover-color:${escapeHTML(f.color||colors[0])}">
     ${photo?"":"✦"}
    </div>

    <div class="day-info">
     <h3>${escapeHTML(f.name)}</h3>
     <small>${formatDate(f.created_at)}</small>
     <p>${escapeHTML((f.description||"Пока нет описания.").slice(0,110))}</p>
    </div>
   </article>
  `;
 }).join("");

 loadArchiveCovers();
}

async function getFileUrl(path){
 const {data,error}=await db.storage
  .from(BUCKET)
  .createSignedUrl(path,3600);

 if(error){
  console.error(error);
  return "";
 }

 return data?.signedUrl||"";
}

async function loadArchiveCovers(){
 for(const f of folders){
  const photo=(Array.isArray(f.files)?f.files:[])
   .find(x=>(x.type||"").startsWith("image/"));

  if(!photo)continue;

  const url=await getFileUrl(photo.path);

  const cover=document.querySelector(
   `[data-cover="${CSS.escape(f.id)}"]`
  );

  if(cover&&url){
   cover.style.backgroundImage=`url("${url}")`;
   cover.textContent="";
  }
 }
}

/* ЗАГРУЗКА ПАПОК ИЗ БАЗЫ */
async function refreshFolders(){
 if(!currentUser)return;

 const {data,error}=await db.from("memories")
  .select("*")
  .eq("user_id",currentUser.id)
  .order("created_at",{ascending:false});

 if(error){
  console.error(error);
  toast("Ошибка загрузки папок: "+error.message);
  return;
 }

 folders=data||[];

 renderFolders();
 renderArchive();

 if(currentId&&!folders.some(f=>f.id===currentId)){
  closeFolder();
 }
}

/* ОТКРЫТИЕ ПАПКИ В ОКНЕ */
function openFolder(id){
 if(!currentUser)return;

 const f=folders.find(x=>x.id===id);
 if(!f)return;

 currentId=id;

 $("#editorTitle").textContent=f.name;
 $("#editorDate").textContent=formatDate(f.created_at);

 $("#editorIcon").style.setProperty(
  "--folder-color",
  f.color||colors[0]
 );

 $("#dayText").value=f.description||"";
 $("#songUrl").value=f.song_url||"";
 $("#songInfo").value=f.song_info||"";
 $("#mood").value=f.mood||"";
 $("#weather").value=f.weather||"";

 currentFiles=(Array.isArray(f.files)?f.files:[])
  .map(x=>({...x,existing:true}));

 renderFiles();
 status($("#saveStatus"),"");

 $("#folderModal").classList.add("open");
 document.body.style.overflow="hidden";
}

function closeFolder(){
 $("#folderModal").classList.remove("open");
 document.body.style.overflow="";
}

/* СОЗДАНИЕ ПАПКИ */
async function createFolder(event){
 event.preventDefault();

 if(!requireAuth()||busy)return;

 const name=$("#folderName").value.trim();

 if(!name){
  toast("Введи название папки.");
  return;
 }

 setBusy(true);
 $("#createFolderBtn").textContent="Создание…";

 const {data,error}=await db.from("memories")
  .insert({
   user_id:currentUser.id,
   name,
   color:selectedColor,
   description:"",
   files:[]
  })
  .select()
  .single();

 setBusy(false);
 $("#createFolderBtn").textContent="＋ Создать папку";

 if(error){
  console.error(error);
  toast("Не удалось создать папку: "+error.message);
  return;
 }

 folders.unshift(data);

 $("#folderName").value="";
 selectedColor=colors[0];

 document.querySelectorAll(".color").forEach((el,i)=>{
  el.classList.toggle("active",i===0);
 });

 renderFolders();
 renderArchive();

 openFolder(data.id);

 toast("Папка успешно создана!");
}

$("#folderForm").addEventListener("submit",createFolder);

/* КЛИК ПО ПАПКЕ */
$("#folderList").addEventListener("click",e=>{
 const item=e.target.closest("[data-id]");
 if(item)openFolder(item.dataset.id);
});

$("#folderList").addEventListener("keydown",e=>{
 if((e.key==="Enter"||e.key===" ")&&e.target.matches("[data-id]")){
  e.preventDefault();
  openFolder(e.target.dataset.id);
 }
});

/* КЛИК ПО КАРТОЧКЕ ДНЕВНИКА */
$("#archiveGrid").addEventListener("click",e=>{
 const card=e.target.closest("[data-memory]");
 if(card)openFolder(card.dataset.memory);
});

$("#archiveGrid").addEventListener("keydown",e=>{
 if((e.key==="Enter"||e.key===" ")&&e.target.matches("[data-memory]")){
  e.preventDefault();
  openFolder(e.target.dataset.memory);
 }
});

/* ФАЙЛЫ */
$("#chooseFiles").addEventListener("click",()=>{
 if(requireAuth())$("#fileInput").click();
});

$("#fileInput").addEventListener("change",e=>{
 addFiles(e.target.files);
});

function addFiles(fileList){
 if(!requireAuth())return;

 for(const file of Array.from(fileList||[])){
  if(file.size>MAX_FILE_SIZE){
   toast(file.name+": файл больше 25 МБ.");
   continue;
  }

  if(!/^(image|video|audio)\//.test(file.type)){
   toast(file.name+": неподдерживаемый формат.");
   continue;
  }

  currentFiles.push({
   name:file.name,
   type:file.type,
   file,
   existing:false
  });
 }

 renderFiles();
 $("#fileInput").value="";
}

function renderFiles(){
 $("#fileList").innerHTML=currentFiles.map((f,i)=>`
  <div class="file-item">
   ${escapeHTML(f.name)}
   <button type="button"
    data-remove="${i}"
    aria-label="Удалить файл">×</button>
  </div>
 `).join("");
}

$("#fileList").addEventListener("click",e=>{
 const b=e.target.closest("[data-remove]");
 if(!b)return;

 currentFiles.splice(Number(b.dataset.remove),1);
 renderFiles();
});

/* ПЕРЕТАСКИВАНИЕ ФАЙЛОВ */
const drop=$("#drop");

drop.addEventListener("dragover",e=>{
 e.preventDefault();
 drop.style.background="#edf1ff";
});

drop.addEventListener("dragleave",()=>{
 drop.style.background="";
});

drop.addEventListener("drop",e=>{
 e.preventDefault();
 drop.style.background="";
 addFiles(e.dataTransfer.files);
});

function safeFileName(name){
 return String(name).normalize("NFKD")
  .replace(/[^a-zA-Z0-9._-]/g,"_")
  .slice(-90)||"file";
}

/* ЗАГРУЗКА НОВЫХ ФАЙЛОВ В SUPABASE */
async function uploadNewFiles(){
 const uploaded=[];
 const newlyUploadedPaths=[];

 try{
  for(const item of currentFiles){
   if(item.existing){
    uploaded.push({
     name:item.name,
     type:item.type,
     path:item.path
    });
    continue;
   }

   const path=
    `${currentUser.id}/${currentId}/${crypto.randomUUID()}-${safeFileName(item.name)}`;

   const {error}=await db.storage.from(BUCKET).upload(
    path,
    item.file,
    {
     contentType:item.type,
     upsert:false
    }
   );

   if(error)throw error;

   newlyUploadedPaths.push(path);

   uploaded.push({
    name:item.name,
    type:item.type,
    path
   });
  }

  return uploaded;

 }catch(error){
  if(newlyUploadedPaths.length){
   await db.storage.from(BUCKET).remove(newlyUploadedPaths);
  }

  throw error;
 }
}

/* СОХРАНЕНИЕ ВОСПОМИНАНИЯ */
async function saveCurrent(){
 if(!requireAuth()||busy)return;

 const f=folders.find(x=>x.id===currentId);
 if(!f)return;

 const songUrl=$("#songUrl").value.trim();

 if(songUrl){
  try{
   const u=new URL(songUrl);
   if(!["http:","https:"].includes(u.protocol))throw new Error();
  }catch{
   toast("Проверь ссылку на песню.");
   return;
  }
 }

 setBusy(true);
 $("#saveBtn").textContent="Сохранение…";
 status($("#saveStatus"),"Сохраняем файлы и воспоминание…");

 let files;

 try{
  files=await uploadNewFiles();
 }catch(error){
  console.error(error);

  setBusy(false);
  $("#saveBtn").textContent="Сохранить воспоминание";

  status(
   $("#saveStatus"),
   "Ошибка загрузки: "+error.message,
   "error"
  );

  toast("Не удалось загрузить файлы.");
  return;
 }

 const updates={
  description:$("#dayText").value.trim(),
  song_url:songUrl||null,
  song_info:$("#songInfo").value.trim()||null,
  mood:$("#mood").value||null,
  weather:$("#weather").value||null,
  files
 };

 const {data,error}=await db.from("memories")
  .update(updates)
  .eq("id",currentId)
  .eq("user_id",currentUser.id)
  .select()
  .single();

 setBusy(false);
 $("#saveBtn").textContent="Сохранить воспоминание";

 if(error){
  console.error(error);

  status(
   $("#saveStatus"),
   "Ошибка сохранения: "+error.message,
   "error"
  );

  toast("Не удалось сохранить воспоминание.");
  return;
 }

 const index=folders.findIndex(x=>x.id===currentId);

 if(index!==-1){
  folders[index]=data;
 }

 currentFiles=(data.files||[])
  .map(x=>({...x,existing:true}));

 /* ОЧИСТКА ПОЛЕЙ ПОСЛЕ УСПЕШНОГО СОХРАНЕНИЯ */
 $("#dayText").value="";
 $("#songUrl").value="";
 $("#songInfo").value="";
 $("#mood").value="";
 $("#weather").value="";

 renderFiles();
 renderFolders();
 renderArchive();

 status(
  $("#saveStatus"),
  "Воспоминание успешно сохранено в облаке.",
  "success"
 );

 toast("Сохранено! Поля очищены.");
}

/* УДАЛЕНИЕ ПАПКИ */
async function deleteCurrent(){
 if(!requireAuth()||!currentId||busy)return;

 if(!confirm("Удалить эту папку и все её файлы?"))return;

 const f=folders.find(x=>x.id===currentId);
 if(!f)return;

 setBusy(true);

 const paths=(Array.isArray(f.files)?f.files:[])
  .map(x=>x.path)
  .filter(Boolean);

 if(paths.length){
  const {error:storageError}=await db.storage
   .from(BUCKET)
   .remove(paths);

  if(storageError){
   setBusy(false);
   toast("Ошибка удаления файлов: "+storageError.message);
   return;
  }
 }

 const {error}=await db.from("memories")
  .delete()
  .eq("id",currentId)
  .eq("user_id",currentUser.id);

 setBusy(false);

 if(error){
  toast("Не удалось удалить папку: "+error.message);
  return;
 }

 folders=folders.filter(x=>x.id!==currentId);

 closeFolder();
 currentId=null;
 currentFiles=[];

 renderFolders();
 renderArchive();

 toast("Папка удалена.");
}

/* АВТОРИЗАЦИЯ */
function openAuth(mode="login"){
 switchAuth(mode);
 $("#authModal").classList.add("open");
}

function closeModal(id){
 $("#"+id).classList.remove("open");
}

function switchAuth(mode){
 authMode=mode;

 $("#loginTab").classList.toggle("active",mode==="login");
 $("#registerTab").classList.toggle("active",mode==="register");

 $("#authTitle").textContent=
  mode==="login"?"Вход в аккаунт":"Создание аккаунта";

 $("#nameField").hidden=mode!=="register";
 $("#authName").required=mode==="register";

 $("#authPassword").autocomplete=
  mode==="login"?"current-password":"new-password";

 $("#authSubmit").textContent=
  mode==="login"?"Войти":"Зарегистрироваться";

 status($("#authMessage"),"");
}

$("#authForm").addEventListener("submit",async e=>{
 e.preventDefault();

 if(!db||busy)return;

 const email=$("#authEmail").value.trim().toLowerCase();
 const password=$("#authPassword").value;

 setBusy(true);

 status(
  $("#authMessage"),
  authMode==="login"?"Выполняется вход…":"Создаём аккаунт…"
 );

 let result;

 try{
  if(authMode==="register"){
   const name=$("#authName").value.trim();

   if(!name){
    setBusy(false);
    status($("#authMessage"),"Введи имя.","error");
    return;
   }

   result=await db.auth.signUp({
    email,
    password,
    options:{
     data:{display_name:name}
    }
   });

  }else{
   result=await db.auth.signInWithPassword({
    email,
    password
   });
  }

 }catch(error){
  setBusy(false);
  status($("#authMessage"),error.message,"error");
  return;
 }

 setBusy(false);

 if(result.error){
  status($("#authMessage"),result.error.message,"error");
  return;
 }

 if(authMode==="register"&&!result.data.session){
  status(
   $("#authMessage"),
   "Аккаунт создан. Подтверди почту, затем войди.",
   "success"
  );
  return;
 }

 $("#authModal").classList.remove("open");

 toast(authMode==="login"?"Ты вошёл в аккаунт.":"Аккаунт создан.");
});

/* ВЫХОД */
async function logout(){
 if(!db)return;

 const {error}=await db.auth.signOut();

 if(error){
  toast("Не удалось выйти: "+error.message);
  return;
 }

 currentUser=null;
 folders=[];
 currentId=null;
 currentFiles=[];

 updateInterface();

 toast("Ты вышел из аккаунта.");
}

/* ЗАКРЫТИЕ ОКОН */
document.querySelectorAll(".modal").forEach(m=>{
 m.addEventListener("click",e=>{
  if(e.target===m){
   m.classList.remove("open");
   document.body.style.overflow="";
  }
 });
});

document.addEventListener("keydown",e=>{
 if(e.key==="Escape"){
  document.querySelectorAll(".modal.open").forEach(m=>{
   m.classList.remove("open");
  });
  document.body.style.overflow="";
 }
});

/* ЗАПУСК */
async function init(){
 initPalette();

 if(!window.supabase?.createClient){
  toast("Не удалось загрузить Supabase. Проверь интернет.");
  return;
 }

 db=window.supabase.createClient(
  SUPABASE_URL,
  SUPABASE_KEY
 );

 const {data,error}=await db.auth.getSession();

 if(error)console.error(error);

 currentUser=data.session?.user||null;

 updateInterface();

 if(currentUser){
  await refreshFolders();
 }

 db.auth.onAuthStateChange((_event,session)=>{
  currentUser=session?.user||null;
  currentId=null;
  currentFiles=[];

  updateInterface();

  if(currentUser){
   setTimeout(()=>refreshFolders(),0);
  }
 });
}

init();
</script>

</body>
</html>
