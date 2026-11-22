
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
  .share-panel {
  margin-top: 25px;
  padding-top: 20px;
  border-top: 1px solid var(--border);
}
.share-list {
  display: grid;
  gap: 9px;
  margin-top: 12px;
}
.share-item {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 10px;
  padding: 10px;
  background: #f5f7f8;
  border-radius: 7px;
  font-size: 12px;
  overflow-wrap: anywhere;
}
.shared-label {
  display: inline-block;
  margin-top: 7px;
  padding: 4px 8px;
  background: #e9eef2;
  color: var(--primary);
  border-radius: 5px;
  font-size: 10px;
  font-weight: 700;
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
    <button class="btn" id="heroLoginButton" onclick="openAuth()">Войти в аккаунт</button>
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
      <div class="actions">
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
   <div class="section-heading" style="margin-top:55px">
  <div class="eyebrow">03 / SHARED MEMORIES</div>
  <h2>Со мной поделились</h2>
  <p>Воспоминания, которыми поделились другие пользователи.</p>
</div>
<div class="archive-grid" id="sharedArchiveGrid">
  <p class="empty">Пока с вами никто не поделился воспоминаниями.</p>
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
let sharedMemories = [];
let myShares = [];
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

  const { data, error } = await supabaseClient
    .from("memories")
    .select("*")
    .order("created_at", { ascending: false });

  if (error) {
    toast("Не удалось загрузить воспоминания");
    console.error(error);
    return;
  }

  folders = data || [];

  const { data: receivedShares, error: receivedError } =
    await supabaseClient
      .from("memory_shares")
      .select("memory_id, owner_id, created_at")
      .eq("shared_with", currentUser.id);

  if (receivedError) {
    console.error(receivedError);
  }

  const sharedIds = (receivedShares || []).map(item => item.memory_id);

  if (sharedIds.length) {
    const { data: sharedData, error: sharedError } =
      await supabaseClient
        .from("memories")
        .select("*")
        .in("id", sharedIds);

    if (sharedError) {
      console.error(sharedError);
    }

    sharedMemories = (sharedData || []).map(memory => ({
      ...memory,
      isShared: true
    }));
  } else {
    sharedMemories = [];
  }

  renderFolders();
  renderArchive();
  renderSharedArchive();

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

$("#archiveGrid").addEventListener("click", async event => {
  const card = event.target.closest("[data-memory]");
  if (!card) return;

  const folder = folders.find(item => item.id === card.dataset.memory);
  if (!folder) return;

  await showMemory(folder);
});
  $("#sharedArchiveGrid").addEventListener("click", async event => {
  const card = event.target.closest("[data-shared-memory]");
  if (!card) return;

  const memory = sharedMemories.find(
    item => item.id === card.dataset.sharedMemory
  );

  if (memory) await showMemory(memory);
});
async function shareCurrentMemory() {
  if (!currentUser || !currentId) {
    toast("Сначала выберите воспоминание");
    return;
  }

  const email = $("#shareEmail").value.trim().toLowerCase();

  if (!email) {
    toast("Введите электронную почту");
    return;
  }

  const button = document.querySelector(
    ".share-panel button"
  );

  button.disabled = true;
  button.textContent = "Отправка...";

  try {
    const { error } = await supabaseClient.rpc(
      "share_memory_with_email",
      {
        p_memory_id: currentId,
        p_email: email
      }
    );

    if (error) throw error;

    $("#shareEmail").value = "";

    toast("Доступ успешно предоставлен");
    await loadMyShares();
  } catch (error) {
    console.error(error);
    toast(error.message || "Не удалось поделиться");
  } finally {
    button.disabled = false;
    button.textContent = "Поделиться воспоминанием";
  }
}

async function loadMyShares() {
  if (!currentUser || !currentId) return;

  const { data, error } = await supabaseClient
    .from("memory_shares")
    .select("*")
    .eq("memory_id", currentId)
    .eq("owner_id", currentUser.id);

  if (error) {
    console.error(error);
    return;
  }

  myShares = data || [];
  renderMyShares();
}

function renderMyShares() {
  const container = $("#shareList");
  if (!container) return;

  if (!myShares.length) {
    container.innerHTML =
      '<p style="font-size:12px;color:var(--muted)">Доступ пока никому не предоставлен.</p>';
    return;
  }

  container.innerHTML = myShares.map(share => `
    <div class="share-item">
      <span>${escapeHTML(share.shared_email)}</span>
      <button
        class="btn small danger"
        type="button"
        data-revoke="${share.id}">
        Отозвать
      </button>
    </div>
  `).join("");
}

$("#shareList").addEventListener("click", async event => {
  const button = event.target.closest("[data-revoke]");
  if (!button) return;

  if (!confirm("Отозвать доступ к этому воспоминанию?")) return;

  button.disabled = true;

  const { error } = await supabaseClient.rpc(
    "revoke_memory_share",
    {
      p_share_id: button.dataset.revoke
    }
  );

  if (error) {
    console.error(error);
    toast("Не удалось отозвать доступ");
    button.disabled = false;
    return;
  }

  toast("Доступ отозван");
  await loadMyShares();
});

async function renderSharedArchive() {
  const container = $("#sharedArchiveGrid");
  if (!container) return;

  if (!currentUser || !sharedMemories.length) {
    container.innerHTML =
      '<p class="empty">Пока с вами никто не поделился воспоминаниями.</p>';
    return;
  }

  const cards = await Promise.all(
    sharedMemories.map(async memory => {
      const photo = (memory.files || []).find(file =>
        file.type?.startsWith("image/")
      );

      const imageUrl = photo
        ? await getFileUrl(photo.path)
        : "";

      return `
        <article class="day-card" data-shared-memory="${memory.id}">
          <div class="day-cover"
            style="${
              imageUrl
                ? `background-image:url('${imageUrl}')`
                : `background-color:${escapeHTML(memory.color)}`
            }">
            ${imageUrl ? "" : "▤"}
          </div>
          <div class="day-info">
            <h3>${escapeHTML(memory.name)}</h3>
            <p>${formatDate(memory.created_at)}</p>
            <span class="shared-label">ДОСТУП ПО ССЫЛКЕ</span>
            <div class="day-preview">
              ${escapeHTML((memory.description || "Воспоминание").slice(0, 100))}
            </div>
          </div>
        </article>
      `;
    })
  );

  container.innerHTML = cards.join("");
}
  async function showMemory(folder) {
  $("#memoryTitle").textContent = folder.name;
  $("#memoryDate").textContent = formatDate(folder.created_at);
  $("#memoryText").textContent = folder.description || "Описание отсутствует.";
  $("#memoryMood").textContent = folder.mood ? "Настроение: " + folder.mood : "";
  $("#memorySong").textContent = folder.song_info ? "Музыка: " + folder.song_info : "";

  const photo = (folder.files || []).find(file =>
    file.type?.startsWith("image/")
  );

  const photoUrl = photo ? await getFileUrl(photo.path) : "";

  $("#memoryPhoto").style.backgroundImage =
    photoUrl ? `url("${photoUrl}")` : "";

  $("#memoryPhoto").textContent =
    photoUrl ? "" : "ARTTECH GENESIS";

  const media = await Promise.all(
    (folder.files || []).map(async file => {
      const url = await getFileUrl(file.path);

      if (file.type?.startsWith("image/"))
        return `<img src="${url}" alt="">`;

      if (file.type?.startsWith("video/"))
        return `<video src="${url}" controls></video>`;

      if (file.type?.startsWith("audio/"))
        return `<audio src="${url}" controls></audio>`;

      return "";
    })
  );

  const song = folder.song_url
    ? `<a href="${escapeHTML(folder.song_url)}" target="_blank" rel="noopener" class="btn small">Открыть музыку</a>`
    : "";

  $("#memoryFiles").innerHTML = media.join("") + song;
  $("#memoryModal").classList.add("open");
}
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

 $("#heroLoginButton").hidden = !!currentUser;
}

supabaseClient.auth.onAuthStateChange((event, session) => {
 currentUser = session?.user || null;
 updateUser();

 if (event === "INITIAL_SESSION" || event === "SIGNED_IN") {
  if (currentUser) {
   setTimeout(() => loadMemories(), 0);
  }
 }

 if (event === "SIGNED_OUT") {
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
