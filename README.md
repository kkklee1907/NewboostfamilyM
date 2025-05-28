<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>NewboostfamilyM</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Orbitron&display=swap');
  body, html {
    margin: 0; padding: 0; height: 100%;
    font-family: 'Orbitron', sans-serif;
    background: url('https://images.unsplash.com/photo-1506744038136-46273834b3fb?ixlib=rb-4.0.3&auto=format&fit=crop&w=1920&q=80') no-repeat center center fixed;
    background-size: cover;
    color: #e0e0e0;
    overflow-x: hidden;
  }
  header {
    background: rgba(0,0,0,0.7);
    padding: 1rem;
    text-align: center;
    font-size: 2.5rem;
    font-weight: bold;
    letter-spacing: 0.15em;
    color: #ffd700;
    text-shadow: 0 0 8px #ffd700;
  }
  #welcome-message {
    background: rgba(0,0,0,0.8);
    padding: 15px;
    margin: 1rem auto;
    max-width: 700px;
    border-radius: 10px;
    font-size: 1.4rem;
    text-align: center;
    display: none;
    color: #aaf;
  }
  nav {
    background: rgba(0,0,0,0.6);
    display: flex;
    justify-content: center;
    gap: 1rem;
    padding: 0.8rem 0;
    flex-wrap: wrap;
  }
  nav button {
    background: #222;
    border: none;
    padding: 0.7rem 1.5rem;
    border-radius: 8px;
    color: #ffd700;
    font-weight: 700;
    cursor: pointer;
    transition: 0.3s;
  }
  nav button:hover {
    background: #ffd700;
    color: #222;
  }
  main {
    max-width: 900px;
    margin: 1rem auto 3rem;
    background: rgba(0,0,0,0.75);
    border-radius: 12px;
    padding: 1rem;
    min-height: 400px;
    color: #eee;
    overflow-y: auto;
  }
  /* Chat area */
  #chat {
    height: 300px;
    overflow-y: auto;
    background: #111;
    padding: 10px;
    border-radius: 10px;
    margin-bottom: 1rem;
    font-size: 0.9rem;
  }
  #chat p {
    margin: 5px 0;
  }
  #chat input, #chat button {
    padding: 8px;
    font-size: 1rem;
  }
  #chat input {
    width: 80%;
    border-radius: 6px;
    border: none;
  }
  #chat button {
    border-radius: 6px;
    border: none;
    background: #ffd700;
    color: #222;
    font-weight: bold;
    cursor: pointer;
    width: 18%;
  }
  /* Photo battle and uploads */
  .gallery {
    display: flex;
    flex-wrap: wrap;
    gap: 10px;
    justify-content: center;
  }
  .gallery img {
    width: 150px;
    height: 100px;
    object-fit: cover;
    border-radius: 8px;
    border: 2px solid #444;
    cursor: pointer;
    transition: transform 0.3s ease;
  }
  .gallery img:hover {
    transform: scale(1.05);
    border-color: #ffd700;
  }
  /* Upload input */
  #upload-section {
    margin: 1rem 0;
  }
  #upload-section input[type="file"] {
    display: block;
    margin: 0.5rem 0;
  }
  #upload-section button {
    padding: 10px 20px;
    background: #ffd700;
    border: none;
    border-radius: 8px;
    cursor: pointer;
    font-weight: 700;
    color: #222;
  }
  /* Ideas and words */
  #ideas, #words {
    min-height: 120px;
    background: #222;
    border-radius: 10px;
    padding: 1rem;
    margin-top: 1rem;
    overflow-y: auto;
    font-size: 1rem;
  }
  #ideas p, #words p {
    margin: 0.3rem 0;
  }
  /* Animations container */
  #animation-container {
    position: fixed;
    top: 0; left: 0; right: 0; bottom: 0;
    pointer-events: none;
    z-index: 1;
  }
  .robot, .smurf, .ai-girl {
    position: absolute;
    bottom: 10px;
    width: 60px;
    height: 60px;
    user-select: none;
  }
  /* Smurf style */
  .smurf {
    background: url('https://i.imgur.com/VJX5Uqg.png') no-repeat center/contain;
  }
  /* Robot style */
  .robot {
    background: url('https://i.imgur.com/IV6D3Td.png') no-repeat center/contain;
  }
  /* AI girl */
  .ai-girl {
    width: 150px;
    height: 150px;
    bottom: 40px;
    background: url('https://i.imgur.com/tT6aPfo.png') no-repeat center/contain;
    animation: float 4s ease-in-out infinite;
  }
  /* Galaxy background for AI girl animation */
  #galaxy-bg {
    position: fixed;
    top: 0; left: 0; width: 100%; height: 100%;
    background: radial-gradient(circle at center, #0b0033, #000000);
    opacity: 0;
    pointer-events: none;
    z-index: 0;
    transition: opacity 2s ease;
  }
  #galaxy-bg.active {
    opacity: 0.7;
  }
  /* Floating animation */
  @keyframes float {
    0%, 100% { transform: translateY(0px);}
    50% { transform: translateY(-20px);}
  }
</style>
</head>
<body>
<header>NewboostfamilyM</header>

<div id="welcome-message"></div>

<nav>
  <button data-section="chat">Общий чат</button>
  <button data-section="photo-battle">Фото батл</button>
  <button data-section="best-photos">Лучшие фото</button>
  <button data-section="uploads">Загрузки от посетителей</button>
  <button data-section="ideas-battle">Баттл идей</button>
  <button data-section="words">Слова</button>
</nav>

<main>
  <section id="chat" class="content-section" style="display:none;">
    <div id="chat-messages" style="height: 260px; overflow-y: auto; background:#111; padding: 10px; border-radius: 8px; margin-bottom: 10px;"></div>
    <input type="text" id="chat-input" placeholder="Напиши сообщение..." />
    <button id="chat-send">Отправить</button>
  </section>

  <section id="photo-battle" class="content-section" style="display:none;">
    <div class="gallery" id="photo-battle-gallery"></div>
    <div id="upload-section">
      <input type="file" id="photo-battle-upload" accept="image/*" />
      <button id="upload-photo-battle">Загрузить фото для батла</button>
    </div>
  </section>

  <section id="best-photos" class="content-section" style="display:none;">
    <div class="gallery" id="best-photos-gallery"></div>
  </section>

  <section id="uploads" class="content-section" style="display:none;">
    <div class="gallery" id="uploads-gallery"></div>
    <div id="upload-section">
      <input type="file" id="uploads-upload" accept="image/*,video/*" />
      <button id="upload-uploads">Загрузить фото/видео</button>
    </div>
  </section>

  <section id="ideas-battle" class="content-section" style="display:none;">
    <div id="ideas"></div>
    <input type="text" id="ideas-input" placeholder="Предложи идею..." />
    <button id="ideas-send">Отправить идею</button>
  </section>

  <section id="words" class="content-section" style="display:none;">
    <div id="words"></div>
    <input type="text" id="words-input" placeholder="Добавь слово..." />
    <button id="words-send">Отправить слово</button>
  </section>
</main>

<div id="animation-container"></div>
<div id="galaxy-bg"></div>

<script>
  // Visitors counter using localStorage (fake counter for demo)
  if(!localStorage.getItem('visitorCount')){
    localStorage.setItem('visitorCount', '1');
  } else {
    let count = parseInt(localStorage.getItem('visitorCount'));
    localStorage.setItem('visitorCount', (count + 1).toString());
  }

  // Show welcome message first visit from this IP (simulate by localStorage)
  if(!localStorage.getItem('visited')){
    localStorage.setItem('visited', 'true');
    const welcome = document.getElementById('welcome-message');
    welcome.textContent = 'Вас приветствует Semen+ETS Matilda';
    welcome.style.display = 'block';
    setTimeout(() => {
      welcome.style.display = 'none';
      showSection('chat');
      startFirstAnimation();
    }, 4000);
  } else {
    showSection('chat');
    startSecondAnimation();
  }

  // Navigation buttons
  const buttons = document.querySelectorAll('nav button');
  buttons.forEach(btn => {
    btn.addEventListener('click', () => {
      showSection(btn.dataset.section);
    });
  });

  function showSection(id){
    document.querySelectorAll('.content-section').forEach(sec => {
      sec.style.display = 'none';
    });
    const section = document.getElementById(id);
    if(section) section.style.display = 'block';
  }

  // Chat functionality (simple, local only)
  const chatMessages = document.getElementById('chat-messages');
  const chatInput = document.getElementById('chat-input');
  const chatSend = document.getElementById('chat-send');

  chatSend.addEventListener('click', () => {
    const msg = chatInput.value.trim();
    if(msg){
      addChatMessage('Пользователь', msg);
      chatInput.value = '';
    }
  });

  function addChatMessage(user, text){
    const p = document.createElement('p');
    p.textContent = `${user}: ${text}`;
    chatMessages.appendChild(p);
    chatMessages.scrollTop = chatMessages.scrollHeight;
  }

  // Photo battle uploads & gallery
  const photoBattleGallery = document.getElementById('photo-battle-gallery');
  const photoBattleUpload = document.getElementById('photo-battle-upload');
  const uploadPhotoBattle = document.getElementById('upload-photo-battle');

  let photoBattleImages = [];

  uploadPhotoBattle.addEventListener('click', () => {
    const file = photoBattleUpload.files[0];
    if(!file){
      alert('Выберите фото');
      return;
    }
    if(!validateImage(file)){
      alert('Фото не соответствует правилам (запрет +18, животная еда, аморальный контент)');
      return;
    }
    const reader = new FileReader();
    reader.onload = e => {
      photoBattleImages.push(e.target.result);
      renderGallery(photoBattleGallery, photoBattleImages);
      photoBattleUpload.value = '';
    };
    reader.readAsDataURL(file);
  });

  // Best photos gallery (static demo)
  const bestPhotosGallery = document.getElementById('best-photos-gallery');
  const bestPhotos = [
    'https://images.unsplash.com/photo-1503023345310-bd7c1de61c7d?auto=format&fit=crop&w=400&q=60',
    'https://images.unsplash.com/photo-1494526585095-c41746248156?auto=format&fit=crop&w=400&q=60',
    'https://images.unsplash.com/photo-1486308510493-cf5e3f57c99b?auto=format&fit=crop&w=400&q=60',
  ];
  renderGallery(bestPhotosGallery, bestPhotos);

  // Uploads gallery & upload
  const uploadsGallery = document.getElementById('uploads-gallery');
  const uploadsUpload = document.getElementById('uploads-upload');
  const uploadUploadsBtn = document.getElementById('upload-uploads');

  let visitorUploads = [];

  uploadUploadsBtn.addEventListener('click', () => {
    const file = uploadsUpload.files[0];
    if(!file){
      alert('Выберите файл');
      return;
    }
    if(!validateImage(file) && !validateVideo(file)){
      alert('Файл не соответствует правилам (запрет +18, животная еда, аморальный контент)');
      return;
    }
    const reader = new FileReader();
    reader.onload = e => {
      visitorUploads.push(e.target.result);
      renderGallery(uploadsGallery, visitorUploads);
      uploadsUpload.value = '';
    };
    reader.readAsDataURL(file);
  });

  // Ideas battle section
  const ideasDiv = document.getElementById('ideas');
  const ideasInput = document.getElementById('ideas-input');
  const ideasSend = document.getElementById('ideas-send');

  ideasSend.addEventListener('click', () => {
    const idea = ideasInput.value.trim();
    if(idea){
      addIdea(idea);
      ideasInput.value = '';
    }
  });

  function addIdea(text){
    const p = document.createElement('p');
    p.textContent = text;
    ideasDiv.appendChild(p);
    ideasDiv.scrollTop = ideasDiv.scrollHeight;
  }

  // Words section
  const wordsDiv = document.getElementById('words');
  const wordsInput = document.getElementById('words-input');
  const wordsSend = document.getElementById('words-send');

  wordsSend.addEventListener('click', () => {
    const word = wordsInput.value.trim();
    if(word){
      addWord(word);
      wordsInput.value = '';
    }
  });

  function addWord(text){
    const p = document.createElement('p');
    p.textContent = text;
    wordsDiv.appendChild(p);
    wordsDiv.scrollTop = wordsDiv.scrollHeight;
  }

  // Gallery render function
  function renderGallery(container, images){
    container.innerHTML = '';
    images.forEach(src => {
      const img = document.createElement('img');
      img.src = src;
      container.appendChild(img);
    });
  }

  // Content validation (basic placeholder)
  // Фильтры: запрет +18, запрет животной еды, запрет аморальных контентов
  // В этой демо-версии проверка по имени файла и типу (можно доработать на сервере)
  function validateImage(file){
    const forbiddenWords = ['18', 'sex', 'porno', 'meat', 'fish', 'chicken', 'beef', 'pork', 'animal', 'blood', 'kill', 'amoral', 'drugs'];
    const name = file.name.toLowerCase();
    for(const w of forbiddenWords){
      if(name.includes(w)) return false;
    }
    // Проверяем расширения изображения
    const validTypes = ['image/jpeg', 'image/png', 'image/gif', 'image/webp'];
    if(!validTypes.includes(file.type)) return false;
    return true;
  }
  function validateVideo(file){
    const forbiddenWords = ['18', 'sex', 'porno', 'meat', 'fish', 'chicken', 'beef', 'pork', 'animal', 'blood', 'kill', 'amoral', 'drugs'];
    const name = file.name.toLowerCase();
    for(const w of forbiddenWords){
      if(name.includes(w)) return false;
    }
    const validTypes = ['video/mp4', 'video/webm', 'video/ogg'];
    if(!validTypes.includes(file.type)) return false;
    return true;
  }

  // Animations
  const animationContainer = document.getElementById('animation-container');

  // First visit animation: robots + smurfs running from side to side
  function startFirstAnimation(){
    animationContainer.innerHTML = '';
    for(let i=0; i<3; i++){
      createRunner('robot', i*200, 1);
      createRunner('smurf', i*220 + 100, -1);
    }
  }
  function createRunner(type, startX, direction){
    const elem = document.createElement('div');
    elem.classList.add(type);
    elem.style.bottom = '20px';
    elem.style.left = startX + 'px';
    animationContainer.appendChild(elem);
    let pos = startX;
    let speed = 2 * direction;
    function move(){
      pos += speed;
      if(pos > window.innerWidth) pos = -60;
      if(pos < -60) pos = window.innerWidth;
      elem.style.left = pos + 'px';
      requestAnimationFrame(move);
    }
    move();
  }

  // Second animation: AI girl + galaxy background
  function startSecondAnimation(){
    animationContainer.innerHTML = '';
    const galaxy = document.getElementById('galaxy-bg');
    galaxy.classList.add('active');
    const aiGirl = document.createElement('div');
    aiGirl.classList.add('ai-girl');
    animationContainer.appendChild(aiGirl);
  }
</script>
</body>
</html>
