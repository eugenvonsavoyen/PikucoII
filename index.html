(() => {
  'use strict';

  // Конфиг Firebase публичный по задумке — защищают данные правила базы (database.rules.json) и App Check.
  const firebaseConfig = {
    apiKey: "AIzaSyCfcm6SlBlkv9QGyXHWUEab5-BsSjav2Cs",
    authDomain: "pikuco1-fc72f.firebaseapp.com",
    databaseURL: "https://pikuco1-fc72f-default-rtdb.europe-west1.firebasedatabase.app",
    projectId: "pikuco1-fc72f",
    storageBucket: "pikuco1-fc72f.firebasestorage.app",
    messagingSenderId: "451713743393",
    appId: "1:451713743393:web:6d48e45f795a4a72528160",
    measurementId: "G-B2BQ1KSSQY"
  };

  const RECAPTCHA_SITE_KEY = '6Lf1wf4tAAAAABZNzERckMqsV4Ssz_pd9F99MpP8';
  const FB_URL = firebaseConfig.databaseURL;

  // Лимиты — должны совпадать с database.rules.json
  const LIM = { title: 150, desc: 400, qText: 500, aText: 200, eTitle: 150, eDesc: 1000, comment: 500, name: 40, image: 200000, payload: 900000 };
  const MODES = ['standard', 'time', 'survival', 'tournament', 'tree', 'diagram'];

  let appCheck = null;
  try {
    firebase.initializeApp(firebaseConfig);
    appCheck = firebase.appCheck();
    appCheck.activate(RECAPTCHA_SITE_KEY, true);
  } catch (e) {
    console.error("Ошибка инициализации Firebase / App Check:", e);
  }

  // ---------- Сеть ----------
  // Каждый запрос несёт ID-токен пользователя (?auth=...), чтобы правила базы знали, кто пишет (auth.uid).
  async function fbFetch(path, options = {}) {
    const url = new URL(FB_URL + path);
    const u = firebase.auth().currentUser;
    if (u) url.searchParams.set('auth', await u.getIdToken());
    const headers = { ...(options.headers || {}) };
    if (appCheck) {
      try { headers['X-Firebase-AppCheck'] = (await appCheck.getToken()).token; }
      catch (e) { console.warn('Не удалось получить токен App Check', e); }
    }
    return fetch(url.toString(), { ...options, headers });
  }

  async function fbGet(path) {
    const res = await fbFetch(path);
    if (!res.ok) throw Object.assign(new Error('HTTP ' + res.status), { status: res.status });
    return res.json();
  }

  async function fbWrite(path, method, data) {
    const opts = { method };
    if (data !== undefined) {
      opts.headers = { 'Content-Type': 'application/json' };
      opts.body = JSON.stringify(data);
    }
    const res = await fbFetch(path, opts);
    if (!res.ok) throw Object.assign(new Error('HTTP ' + res.status), { status: res.status });
    return res;
  }

  function writeErrorToast(e) {
    console.error(e);
    toast(e && (e.status === 401 || e.status === 403) ? 'Нет прав на это действие' : 'Ошибка сохранения', 'warn');
  }

  const enc = encodeURIComponent;

  // ---------- Очистка данных ----------
  // HTML не вырезаем: весь вывод экранируется через esc(), а старая регулярка портила текст вида "x < 5 и y > 3".
  const CENSOR = [/хуй/gi, /хуя/gi, /хуе/gi, /пизд/gi, /бля/gi, /еба/gi, /ёба/gi, /ебал/gi, /ебуч/gi, /сука/gi, /мразь/gi, /гандон/gi, /долбо[её]б/gi, /мудак/gi, /пидор/gi, /шлюх/gi];
  function cleanText(t, max) {
    if (t == null) return '';
    let r = String(t).replace(/[\u0000-\u0008\u000B\u000C\u000E-\u001F]/g, '');
    CENSOR.forEach(re => { r = r.replace(re, '***'); });
    return max ? r.slice(0, max) : r;
  }

  // Разрешаем только встроенные картинки data:image (никаких внешних ссылок-трекеров и SVG).
  const IMG_RE = /^data:image\/(png|jpeg|webp|gif);base64,[A-Za-z0-9+/=]+$/;
  function safeImg(s) {
    return typeof s === 'string' && s.length <= LIM.image && IMG_RE.test(s) ? s : null;
  }

  const EMOJIS = ['🦊','🐱','🐶','🐼','🐸','🐵','🐯','🦁','🐮','🐷','🐙','🦄','🦖','🐺','🦉','🦇','🐲','🐢','🐍','🦎','🐊','🐳','🐬','🦈','🐟','🦅','🦆','🦢','🐔','🐧','🦌','🦍','🐘','🐪','🦒','🦘','🐄','🐖','🐏','🐑','🐐','🦙'];

  const $ = (s, r = document) => r.querySelector(s);
  const $$ = (s, r = document) => Array.from(r.querySelectorAll(s));
  const uid = () => window.crypto && crypto.randomUUID ? crypto.randomUUID() : 'id' + Math.random().toString(36).slice(2) + Date.now().toString(36);
  const esc = s => String(s ?? '').replace(/[&<>"']/g, c => ({ '&': '&amp;', '<': '&lt;', '>': '&gt;', '"': '&quot;', "'": '&#39;' }[c]));
  const fmtTime = ms => { const s = Math.floor(ms / 1000), m = Math.floor(s / 60), ss = s % 60; return String(m).padStart(2, '0') + ':' + String(ss).padStart(2, '0'); };

  function toast(msg, type = '') { let el = document.getElementById('toast'); if (!el) { el = document.createElement('div'); el.id = 'toast'; document.body.appendChild(el); } el.textContent = msg; el.className = 'toast show ' + type; clearTimeout(el._t); el._t = setTimeout(() => el.classList.remove('show'), 3000); }

  const KEY = 'pikuco2';
  const store = {
    get(k, d) { try { const v = localStorage.getItem(KEY + '.' + k); if (!v) return d; return JSON.parse(v); } catch { return d; } },
    set(k, v) { try { localStorage.setItem(KEY + '.' + k, JSON.stringify(v)); } catch {} },
    del(k) { try { localStorage.removeItem(KEY + '.' + k); } catch {} }
  };
  store.del('user'); // старый профиль из localStorage больше не используется — личность берётся только из Firebase Auth

  // user: { id (Firebase uid), name, avatar, isGuest, email }
  const state = { tests: [], votes: {}, user: null, theme: store.get('theme', 'dark') };

  function newAnswer() { return { id: uid(), text: '', correct: false, nextId: null, points: {} }; }
  function newQuestion() { return { id: uid(), text: '', type: 'single', image: null, answers: [newAnswer(), newAnswer()] }; }
  function getTest(id) { return state.tests.find(t => t.id === id); }

  // ---------- Нормализация (данные из базы недоверенные) ----------
  function toArr(v) { return Array.isArray(v) ? v.filter(Boolean) : (v && typeof v === 'object' ? Object.values(v) : []); }
  function normPoints(p) {
    const out = {};
    if (p && typeof p === 'object') Object.entries(p).forEach(([k, v]) => { const n = Number(v); if (Number.isFinite(n)) out[k] = n; });
    return out;
  }
  function normTest(id, t) {
    t = t || {};
    return {
      id: String(id),
      title: String(t.title || 'Без названия'),
      description: String(t.description || ''),
      author: String(t.author || 'Аноним'),
      authorId: typeof t.authorId === 'string' ? t.authorId : null,
      createdAt: Number(t.createdAt) || Date.now(),
      mode: MODES.includes(t.mode) ? t.mode : 'standard',
      previewImage: safeImg(t.previewImage),
      isQuality: t.isQuality === true,
      stageSize: Number(t.stageSize) || undefined,
      categories: [],
      endings: toArr(t.endings).map(e => ({ id: String(e.id || uid()), title: String(e.title || ''), desc: String(e.desc || ''), image: safeImg(e.image) })),
      questions: toArr(t.questions).map(q => ({
        id: String(q.id || uid()),
        text: String(q.text || ''),
        type: q.type === 'multi' ? 'multi' : 'single',
        image: safeImg(q.image),
        answers: toArr(q.answers).map(a => ({
          id: String(a.id || uid()),
          text: String(a.text || ''),
          correct: a.correct === true,
          nextId: typeof a.nextId === 'string' ? a.nextId : null,
          points: normPoints(a.points)
        }))
      }))
    };
  }

  // Явный белый список полей — ровно то, что разрешают правила базы.
  function toPayload(t) {
    const isTournament = t.mode === 'tournament';
    const p = {
      id: t.id,
      title: cleanText(t.title, LIM.title).trim(),
      description: cleanText(t.description, LIM.desc),
      mode: MODES.includes(t.mode) ? t.mode : 'standard',
      authorId: state.user.id,
      author: state.user.name,
      createdAt: t.createdAt || Date.now(),
      questions: t.questions.map(q => ({
        id: q.id,
        text: cleanText(q.text, LIM.qText),
        type: q.type === 'multi' ? 'multi' : 'single',
        image: safeImg(q.image) || undefined,
        answers: isTournament ? undefined : (q.answers || []).map(a => ({
          id: a.id,
          text: cleanText(a.text, LIM.aText),
          correct: !!a.correct,
          nextId: a.nextId || undefined,
          points: Object.keys(a.points || {}).length ? normPoints(a.points) : undefined
        }))
      }))
    };
    if (t.mode === 'tree' || t.mode === 'diagram') {
      p.endings = (t.endings || []).map(e => ({ id: e.id, title: cleanText(e.title, LIM.eTitle), desc: cleanText(e.desc, LIM.eDesc), image: safeImg(e.image) || undefined }));
    }
    if (safeImg(t.previewImage)) p.previewImage = t.previewImage;
    if (t.stageSize) p.stageSize = Number(t.stageSize);
    if (t.isQuality === true) p.isQuality = true; // сохранить уже выданный знак; выдать новый клиент не может (правила)
    return p;
  }

  // ---------- Работа с базой ----------
  async function dbLoad() {
    try {
      const [tests, votes] = await Promise.all([
        fbGet('/tests.json'),
        fbGet('/votes.json').catch(() => ({}))
      ]);
      state.tests = Object.entries(tests || {}).map(([id, t]) => normTest(id, t)).sort((a, b) => b.createdAt - a.createdAt);
      state.votes = votes && typeof votes === 'object' ? votes : {};
      store.set('tests', state.tests);
    } catch (e) {
      console.warn('DB Load failed', e);
      state.tests = (store.get('tests', null) || []).map(t => normTest(t.id, t));
      toast('Нет связи с базой — показана сохранённая копия', 'warn');
    }
  }

  async function persistTest(t) {
    const p = toPayload(t);
    if (JSON.stringify(p).length > LIM.payload) {
      toast('Тест слишком большой (картинки). Удалите часть изображений.', 'warn');
      return null;
    }
    try {
      await fbWrite(`/tests/${enc(p.id)}.json`, 'PUT', p);
    } catch (e) {
      writeErrorToast(e);
      return null;
    }
    const saved = normTest(p.id, p);
    const idx = state.tests.findIndex(x => x.id === p.id);
    if (idx >= 0) state.tests[idx] = saved; else state.tests.unshift(saved);
    store.set('tests', state.tests);
    return saved;
  }

  async function persistDelete(id) {
    try {
      await fbWrite(`/comments/${enc(id)}.json`, 'DELETE');
      await fbWrite(`/votes/${enc(id)}.json`, 'DELETE');
      await fbWrite(`/tests/${enc(id)}.json`, 'DELETE');
    } catch (e) {
      writeErrorToast(e);
      return false;
    }
    state.tests = state.tests.filter(t => t.id !== id);
    delete state.votes[id];
    store.set('tests', state.tests);
    return true;
  }

  function voteCounts(id) {
    let likes = 0, dislikes = 0;
    Object.values(state.votes[id] || {}).forEach(v => { if (v === 'like') likes++; else if (v === 'dislike') dislikes++; });
    return { likes, dislikes };
  }
  function myVote(id) { return (state.votes[id] || {})[state.user.id] || null; }

  // ---------- Комментарии (отдельная ветка /comments, а не внутри теста) ----------
  async function loadComments(testId) {
    const data = await fbGet(`/comments/${enc(testId)}.json`);
    return Object.entries(data || {}).map(([id, c]) => ({
      id, authorId: String(c.authorId || ''), author: String(c.author || ''), text: String(c.text || ''), date: Number(c.date) || 0
    })).sort((a, b) => b.date - a.date);
  }

  async function postComment(testId, raw) {
    const text = cleanText(String(raw || '').trim(), LIM.comment);
    if (!text) { toast('Введите текст', 'warn'); return false; }
    const ts = { '.sv': 'timestamp' };
    try {
      // Атомарная запись комментария + метки времени для ограничения частоты (не чаще раза в 10 сек).
      await fbWrite('/.json', 'PATCH', {
        [`comments/${testId}/${uid()}`]: { authorId: state.user.id, author: state.user.name, text, date: ts },
        [`rate/${state.user.id}/comment`]: ts
      });
    } catch (e) {
      console.error(e);
      toast(e.status === 401 || e.status === 403 ? 'Не удалось отправить. Комментировать можно не чаще раза в 10 секунд.' : 'Ошибка отправки', 'warn');
      return false;
    }
    toast('Комментарий добавлен ✓', 'good');
    return true;
  }

  function commentsHTML(t, list, withForm) {
    const me = state.user.id;
    const owner = !!t && t.authorId === me;
    return `<h3>Комментарии (${list.length})</h3>
      ${withForm ? `<div style="margin-bottom:16px; padding-bottom:16px; border-bottom:1px solid var(--border)">
        <textarea class="input" id="c-text" rows="2" maxlength="${LIM.comment}" placeholder="Оставить отзыв..."></textarea>
        <button class="btn ghost sm" id="c-submit" style="margin-top:8px">Отправить</button>
      </div>` : ''}
      ${list.length ? list.map(c => `
        <div class="comment">
          ${(c.authorId === me || owner) ? `<button class="comment-del" data-del-comment="${esc(c.id)}" title="Удалить">✕</button>` : ''}
          <div class="row between" style="margin-bottom:4px">
            <b>${esc(c.author)}</b>
            <span class="muted small">${esc(new Date(c.date).toLocaleDateString())}</span>
          </div>
          <p style="margin:0;font-size:13px;white-space:pre-wrap">${esc(c.text)}</p>
        </div>`).join('') : '<p class="muted small">Пока нет комментариев.</p>'}`;
  }

  async function mountComments(testId, withForm) {
    const box = $('#comments-box');
    if (!box) return;
    let list;
    try { list = await loadComments(testId); }
    catch (e) { console.warn(e); box.innerHTML = '<h3>Комментарии</h3><p class="muted small">Не удалось загрузить.</p>'; return; }
    if (!box.isConnected) return;
    box.innerHTML = commentsHTML(getTest(testId), list, withForm);

    const sb = $('#c-submit', box);
    if (sb) sb.addEventListener('click', async () => {
      sb.disabled = true;
      const ok = await postComment(testId, $('#c-text', box).value);
      sb.disabled = false;
      if (ok) mountComments(testId, withForm);
    });

    $$('[data-del-comment]', box).forEach(b => b.addEventListener('click', async () => {
      if (!confirm('Удалить комментарий?')) return;
      try {
        await fbWrite(`/comments/${enc(testId)}/${enc(b.dataset.delComment)}.json`, 'DELETE');
        toast('Удалено', 'good');
        mountComments(testId, withForm);
      } catch (e) { writeErrorToast(e); }
    }));
  }

  async function updatePresence() {
    const countEl = $('#online-count');
    if (!countEl) return;
    try { countEl.textContent = Math.floor(Math.random() * 3) + 1; } catch (e) {}
  }

  // ---------- Аккаунты ----------
  // Гости — анонимные пользователи Firebase Auth: у них настоящий uid, который проверяют правила.
  // При регистрации анонимный аккаунт «повышается» до email, uid сохраняется — тесты гостя остаются его.
  function authErr(e, fallback) {
    const m = {
      'auth/email-already-in-use': 'Этот email уже зарегистрирован',
      'auth/credential-already-in-use': 'Этот email уже зарегистрирован',
      'auth/invalid-email': 'Некорректный email',
      'auth/weak-password': 'Слишком простой пароль',
      'auth/too-many-requests': 'Слишком много попыток, попробуйте позже',
      'auth/network-request-failed': 'Нет соединения'
    };
    return m[e && e.code] || fallback;
  }

  async function loadProfile(fu) {
    let p = null;
    try { p = await fbGet(`/users/${enc(fu.uid)}.json`); } catch (e) { console.warn(e); }
    const valid = p && typeof p.name === 'string' && p.name.trim();
    const legacy = p && Object.keys(p).some(k => k !== 'name' && k !== 'avatar'); // старые профили хранили email и т.п.
    if (!valid || legacy) {
      p = {
        name: valid ? cleanText(p.name, LIM.name) : (fu.isAnonymous ? 'Гость #' + (1000 + Math.floor(Math.random() * 9000)) : (cleanText((fu.email || 'user').split('@')[0], LIM.name) || 'user')),
        avatar: p && EMOJIS.includes(p.avatar) ? p.avatar : EMOJIS[Math.floor(Math.random() * EMOJIS.length)]
      };
      try { await fbWrite(`/users/${enc(fu.uid)}.json`, 'PUT', p); } catch (e) { console.warn(e); }
    }
    return {
      id: fu.uid,
      name: String(p.name).slice(0, LIM.name),
      avatar: EMOJIS.includes(p.avatar) ? p.avatar : EMOJIS[0],
      isGuest: fu.isAnonymous,
      email: fu.email || ''
    };
  }

  async function doRegister(email, password, displayName) {
    if (password.length < 8) { toast('Пароль — минимум 8 символов', 'warn'); return false; }
    try {
      const cred = firebase.auth.EmailAuthProvider.credential(email, password);
      const cur = firebase.auth().currentUser;
      const user = cur && cur.isAnonymous
        ? (await cur.linkWithCredential(cred)).user
        : (await firebase.auth().createUserWithEmailAndPassword(email, password)).user;
      await user.getIdToken(true);

      const name = cleanText(displayName || email.split('@')[0], LIM.name).trim() || 'user';
      await fbWrite(`/users/${enc(user.uid)}.json`, 'PUT', { name, avatar: state.user.avatar });
      state.user = { id: user.uid, name, avatar: state.user.avatar, isGuest: false, email: user.email || email };

      // Обновить имя автора в своих тестах (uid тот же — права остаются)
      for (const t of state.tests.filter(t => t.authorId === user.uid)) await persistTest(t);

      toast('Успешно!', 'good');
      return true;
    } catch (error) {
      console.error(error);
      toast(authErr(error, 'Ошибка регистрации'), 'warn');
      return false;
    }
  }

  async function doLogin(email, password) {
    try {
      await firebase.auth().signInWithEmailAndPassword(email, password);
      toast('Вы вошли!', 'good');
      return true; // состояние обновит onAuthStateChanged
    } catch (error) {
      console.error(error);
      toast(authErr(error, 'Неверный email или пароль'), 'warn');
      return false;
    }
  }

  function doLogout() {
    firebase.auth().signOut()
      .then(() => toast('Вы вышли'))
      .catch(error => { console.error(error); toast('Ошибка выхода', 'warn'); });
  }

  function applyTheme() { document.documentElement.dataset.theme = state.theme; }
  function toggleTheme() { state.theme = state.theme === 'dark' ? 'light' : 'dark'; store.set('theme', state.theme); applyTheme(); }

  // ---------- Роутинг ----------
  let play = null, playTimer = null, lastResult = null, draft = null;
  function render() {
    if (!state.user) return;
    if (playTimer) { clearInterval(playTimer); playTimer = null; }
    const path = (location.hash.replace(/^#/, '') || '/').replace(/\/+$/, '') || '/';
    const parts = path.split('?');
    const routePath = parts[0], params = new URLSearchParams(parts[1] || '');
    const routeParts = routePath.split('/').filter(Boolean);
    const route = routeParts[0] || 'home', param = routeParts[1] ? decodeURIComponent(routeParts[1]) : undefined;
    const app = $('#app');
    try {
      if (route === 'home') { app.innerHTML = viewHome(); bindHome(); }
      else if (route === 'test' && param) { app.innerHTML = viewTest(param); bindTest(param); }
      else if (route === 'play' && param) { startPlay(param); }
      else if (route === 'result') { app.innerHTML = viewResult(params); bindResult(); }
      else if (route === 'create') { startEditor(null); }
      else if (route === 'edit' && param) { startEditor(param); }
      else if (route === 'profile') { app.innerHTML = viewProfile(); bindProfile(); }
      else { app.innerHTML = '<div class="wrap"><h1>404</h1><a class="btn" href="#/">На главную</a></div>'; }
    } catch (e) {
      console.error(e);
      app.innerHTML = `<div class="wrap"><h1>Ошибка</h1><pre>${esc(e.message)}</pre><a class="btn" href="#/">На главную</a></div>`;
    }
    window.scrollTo({ top: 0 });
  }

  function testCard(t) {
    let m = '📝'; if (t.mode === 'time') m = '⏱'; if (t.mode === 'survival') m = '💀'; if (t.mode === 'tournament') m = '🏆'; if (t.mode === 'tree') m = '🌳'; if (t.mode === 'diagram') m = '📊';
    const { likes, dislikes } = voteCounts(t.id);
    const qImg = t.previewImage ? `<img src="${esc(t.previewImage)}" class="test-img">` : '';
    const qualityMark = t.isQuality ? `<span class="badge quality">⭐ Знак качества</span>` : '';
    return `<a class="card test-card" href="#/test/${enc(t.id)}">
      ${qImg}
      <div class="test-card-content">
        <div class="tc-top"><span class="badge">${m} ${t.questions.length} вопр.</span><span class="muted small">👍${likes} 👎${dislikes}</span></div>
        <h3>${esc(t.title)}</h3><p class="muted">${esc(t.description || 'Без описания')}</p>
        <div class="row between" style="margin-top:8px"><span class="tc-go">Пройти →</span><span class="muted small">${esc(t.author)}</span></div>
        ${qualityMark ? `<div style="margin-top:8px">${qualityMark}</div>` : ''}
      </div>
    </a>`;
  }

  function viewHome() {
    const totalQ = state.tests.reduce((s, t) => s + t.questions.length, 0);
    return `<section class="hero">
      <h1>Проходи. Создавай. <span class="grad">Делись.</span></h1>
      <p class="muted">Вы вошли как: <b>${esc(state.user.avatar)} ${esc(state.user.name)}</b></p>
      <div class="hero-actions">
        <a class="btn primary" href="#/create">+ Создать тест</a>
        ${state.user.isGuest ? `<a class="btn ghost" href="#/profile">Войти / Регистрация</a>` : ''}
      </div>
      <div class="stats"><div><b>${state.tests.length}</b><span>тестов</span></div><div><b>${totalQ}</b><span>вопросов</span></div></div>
    </section>
    <section class="wrap">
      <div class="row between" style="margin-top:24px"><h2>Все тесты</h2><input id="search" class="input" placeholder="Поиск…" maxlength="100" style="max-width:280px"></div>
      <div class="grid" id="test-grid">${state.tests.map(testCard).join('') || '<p class="muted">Пока нет тестов.</p>'}</div>
    </section>`;
  }
  function bindHome() {
    const s = $('#search'); if (s) s.addEventListener('input', () => {
      const q = s.value.trim().toLowerCase();
      const f = state.tests.filter(t => t.title.toLowerCase().includes(q) || t.description.toLowerCase().includes(q));
      $('#test-grid').innerHTML = f.map(testCard).join('') || '<p class="muted">Не найдено.</p>';
    });
  }

  function viewTest(id) {
    const t = getTest(id); if (!t) return `<div class="wrap"><h1>Не найден</h1><a class="btn" href="#/">Назад</a></div>`;
    const own = t.authorId === state.user.id;
    const { likes, dislikes } = voteCounts(t.id);
    const qImg = t.previewImage ? `<img src="${esc(t.previewImage)}" class="test-img" style="height:auto;max-height:300px;border-radius:12px;margin-bottom:16px;border:1px solid var(--border)">` : '';

    return `<div class="wrap wide">
      <a href="#/" class="muted small">← Назад</a>
      <div class="result-layout">
        <div class="result-main">
          <div class="card big">
            ${qImg}
            <div class="row"><span class="badge">${t.questions.length} вопр.</span>${t.isQuality ? '<span class="badge quality">⭐ Знак качества</span>' : ''}</div>
            <h1>${esc(t.title)}</h1>
            <p class="muted" style="white-space:pre-wrap">${esc(t.description)}</p>
            <p class="small muted">Автор: ${esc(t.author)}</p>
            <div class="row" style="margin-top:24px;gap:16px">
              <a class="btn primary" href="#/play/${enc(t.id)}">Начать</a>
              <span class="badge" style="margin-left:8px" title="Оценки доступны после прохождения">👍 ${likes} &nbsp; 👎 ${dislikes}</span>
              ${own ? `<a class="btn ghost" href="#/edit/${enc(t.id)}">Редактировать</a><button class="btn danger" id="del-test">Удалить</button>` : ''}
            </div>
          </div>
        </div>
        <div class="result-sidebar sidebar-sticky">
          <div class="sidebar-comments" id="comments-box"><h3>Комментарии</h3><p class="muted small">Загрузка…</p></div>
        </div>
      </div>
    </div>`;
  }

  function bindTest(id) {
    const d = $('#del-test'); if (d) d.addEventListener('click', async () => {
      if (!confirm('Удалить тест навсегда?')) return;
      if (await persistDelete(id)) location.hash = '#/';
    });
    if (getTest(id)) mountComments(id, true);
  }

  // ---------- Прохождение ----------
  function startPlay(id) {
    const t = getTest(id); if (!t) { location.hash = '#/'; return; }
    if (!t.questions.length) { toast('В тесте нет вопросов', 'warn'); location.hash = '#/test/' + enc(id); return; }
    play = { testId: id, index: 0, answers: {}, start: Date.now(), scores: {}, stageCorrect: 0 };

    if (t.mode === 'diagram') {
      play.scores = {};
      t.endings.forEach(e => play.scores[e.id] = 0);
    }

    if (t.mode === 'tree') {
      play.currentNodeId = t.questions[0].id;
      play.history = [play.currentNodeId];
    }

    if (t.mode === 'tournament') {
      if (t.questions.length < 2) { toast('Для турнира нужно минимум 2 варианта', 'warn'); location.hash = '#/test/' + enc(id); return; }
      play.roundItems = [...t.questions].sort(() => Math.random() - 0.5);
      play.winners = [];
      play.currentPair = [];
      play.bracketRound = 1;
      nextTournamentPair();
    } else {
      renderPlay();
    }

    if (t.mode !== 'tournament' && t.mode !== 'tree') {
      playTimer = setInterval(() => { const e = $('#timer'); if (e && play && t.mode !== 'time') e.textContent = fmtTime(Date.now() - play.start); }, 500);
    }
  }

  function nextTournamentPair() {
    if (play.roundItems.length < 2) {
      if (play.roundItems.length === 1) play.winners.push(play.roundItems.pop());
      if (play.winners.length === 1) {
        play.roundItems = [play.winners[0]];
        finishPlay();
        return;
      }
      play.roundItems = [...play.winners];
      play.winners = [];
      play.bracketRound++;
    }
    const a = play.roundItems.pop();
    const b = play.roundItems.pop();
    play.currentPair = [a, b];
    renderTournamentPlay();
  }

  function renderTournamentPlay() {
    const t = getTest(play.testId);
    const [a, b] = play.currentPair;
    $('#app').innerHTML = `<div class="wrap narrow">
      <div class="play-head"><a href="#/test/${enc(t.id)}" class="muted small">← Выйти</a><span class="badge">Раунд ${play.bracketRound}</span></div>
      <p class="muted small center" style="margin-bottom:24px">Выберите лучший вариант. Остальные вылетают.</p>
      <div class="tournament-container">
        <div class="tournament-item" data-aid="${esc(a.id)}">
          ${a.image ? `<img src="${esc(a.image)}">` : ''}
          <h3>${esc(a.text)}</h3>
        </div>
        <div class="tournament-item" data-aid="${esc(b.id)}">
          ${b.image ? `<img src="${esc(b.image)}">` : ''}
          <h3>${esc(b.text)}</h3>
        </div>
      </div>
    </div>`;
    $$('.tournament-item').forEach(el => {
      el.addEventListener('click', () => {
        const winner = play.currentPair.find(x => x.id === el.dataset.aid);
        play.winners.push(winner);
        nextTournamentPair();
      });
    });
  }

  function renderPlay() {
    const t = getTest(play.testId); if (!t) { play = null; location.hash = '#/'; return; }
    let q, total, pct, displayIndex;
    if (t.mode === 'tree') {
      q = t.questions.find(x => x.id === play.currentNodeId);
      if (!q) { finishPlay(); return; }
      total = play.history.length; displayIndex = total; pct = 100;
    } else {
      q = t.questions[play.index];
      if (!q) { finishPlay(); return; }
      total = t.questions.length; displayIndex = play.index + 1; pct = Math.round((play.index / total) * 100);
    }

    let nextBtn;
    if (t.mode === 'tree') nextBtn = `<button class="btn primary" id="next-step">Следующий шаг →</button>`;
    else nextBtn = play.index === total - 1 ? `<button class="btn primary" id="finish">Завершить</button>` : `<button class="btn primary" id="next">Далее →</button>`;

    $('#app').innerHTML = `<div class="wrap narrow">
      <div class="play-head"><a href="#/test/${enc(t.id)}" class="muted small">← Выйти</a><span id="timer">00:00</span></div>
      <div class="progress"><div class="bar" style="width:${t.mode === 'tree' ? 100 : pct}%"></div></div>
      <p class="muted small">${t.mode === 'tree' ? 'Шаг ' + displayIndex : 'Вопрос ' + displayIndex + ' из ' + total}</p>
      <div class="card">
        <h2>${esc(q.text)}</h2>
        ${q.image ? `<img src="${esc(q.image)}" class="q-img">` : ''}
        <div class="answers" id="answers">${q.answers.map(a => `<button class="answer" data-aid="${esc(a.id)}">${esc(a.text)}</button>`).join('')}</div>
      </div>
      <div class="row between" style="margin-top:16px">
        ${t.mode !== 'tree' ? `<button class="btn ghost" id="prev" ${play.index === 0 ? 'disabled' : ''}>← Назад</button>` : `<div></div>`}
        ${nextBtn}
      </div>
    </div>`;
    updateAnswerUI(); bindPlay();
  }

  function currentQuestion(t) { return t.mode === 'tree' ? t.questions.find(x => x.id === play.currentNodeId) : t.questions[play.index]; }

  function updateAnswerUI() {
    const t = getTest(play.testId);
    const q = currentQuestion(t);
    if (!q) return;
    const sel = play.answers[q.id] || [];
    $$('#answers .answer').forEach(b => b.classList.toggle('selected', sel.includes(b.dataset.aid)));
  }

  function goToResult(r) {
    lastResult = r;
    try { sessionStorage.setItem(KEY + '.result', JSON.stringify(r)); } catch {}
    play = null; location.hash = '#/result';
  }

  function bindPlay() {
    const t = getTest(play.testId);
    const q = currentQuestion(t);
    if (!q) return;

    const answersEl = $('#answers');
    if (answersEl) {
      answersEl.addEventListener('click', e => {
        const btn = e.target.closest('.answer'); if (!btn) return;
        const aid = btn.dataset.aid;
        if (q.type === 'single' || t.mode === 'tree') {
          play.answers[q.id] = [aid];
        } else {
          const arr = (play.answers[q.id] || []).slice();
          const i = arr.indexOf(aid);
          if (i >= 0) arr.splice(i, 1); else arr.push(aid);
          play.answers[q.id] = arr;
        }
        updateAnswerUI();
      });
    }

    const n = $('#next'), p = $('#prev'), f = $('#finish'), ns = $('#next-step');
    if (n) n.addEventListener('click', () => { play.index++; renderPlay(); });
    if (p) p.addEventListener('click', () => { play.index--; renderPlay(); });
    if (f) f.addEventListener('click', () => finishPlay());

    if (ns) {
      ns.addEventListener('click', () => {
        const selectedId = (play.answers[q.id] || [])[0];
        if (!selectedId) { toast('Выберите вариант ответа', 'warn'); return; }
        const ans = q.answers.find(a => a.id === selectedId);

        if (ans && ans.nextId) {
          if (ans.nextId.startsWith('E_')) {
            const endingId = ans.nextId.slice(2);
            const ending = t.endings.find(e => e.id === endingId);
            goToResult({ testId: t.id, title: t.title, mode: t.mode, ending: ending || { title: 'Конец', desc: '' }, time: Date.now() - play.start });
            return;
          } else if (ans.nextId.startsWith('Q_')) {
            const nextId = ans.nextId.slice(2);
            if (play.history.length > 500) { finishPlay(); return; } // защита от бесконечного цикла
            play.currentNodeId = nextId;
            play.history.push(nextId);
            renderPlay(); return;
          }
        }

        const currentIndex = t.questions.findIndex(x => x.id === q.id);
        if (currentIndex >= 0 && currentIndex < t.questions.length - 1) {
          play.currentNodeId = t.questions[currentIndex + 1].id;
          play.history.push(play.currentNodeId);
          renderPlay();
        } else {
          goToResult({ testId: t.id, title: t.title, mode: t.mode, ending: { title: 'Конец', desc: '' }, time: Date.now() - play.start });
        }
      });
    }
  }

  function finishPlay() {
    const t = getTest(play.testId);

    if (t.mode === 'tournament') {
      const winner = play.roundItems[0] || play.currentPair[0];
      goToResult({ testId: t.id, title: t.title, mode: t.mode, winner, time: Date.now() - play.start });
      return;
    }

    if (t.mode === 'tree') {
      goToResult({ testId: t.id, title: t.title, mode: t.mode, ending: { title: 'Конец', desc: 'Вы завершили прохождение.' }, time: Date.now() - play.start });
      return;
    }

    if (t.mode === 'diagram') {
      t.questions.forEach(q => {
        (play.answers[q.id] || []).forEach(aid => {
          const ans = q.answers.find(a => a.id === aid);
          if (ans) Object.entries(ans.points).forEach(([endId, val]) => {
            play.scores[endId] = (play.scores[endId] || 0) + Number(val);
          });
        });
      });
      let maxId = Object.keys(play.scores)[0], maxVal = -Infinity;
      Object.entries(play.scores).forEach(([id, val]) => { if (val > maxVal) { maxVal = val; maxId = id; } });
      const winnerEnding = t.endings.find(e => e.id === maxId) || { title: 'Нет данных', desc: '' };
      goToResult({ testId: t.id, title: t.title, mode: t.mode, scores: play.scores, winner: winnerEnding, time: Date.now() - play.start });
      return;
    }

    let correct = 0;
    const review = t.questions.map(q => {
      const sel = (play.answers[q.id] || []).slice().sort();
      const right = q.answers.filter(a => a.correct).map(a => a.id).sort();
      const ok = sel.length === right.length && sel.every((v, i) => v === right[i]);
      if (ok) correct++;
      return { q, sel, right, ok };
    });
    const total = t.questions.length, percent = total > 0 ? Math.round((correct / total) * 100) : 0;
    goToResult({ testId: t.id, title: t.title, mode: t.mode, correct, total, percent, review, time: Date.now() - play.start });
  }

  // ---------- Результат ----------
  function viewResult(params) {
    if (!lastResult) { try { lastResult = JSON.parse(sessionStorage.getItem(KEY + '.result')); } catch {} }
    const r = lastResult; if (!r) return `<div class="wrap"><p class="muted">Результат не найден.</p><a class="btn" href="#/">На главную</a></div>`;

    let main = '';
    if (r.mode === 'tree') {
      const img = safeImg(r.ending && r.ending.image);
      main = `<div class="card center">
        <p class="muted" style="margin-bottom:24px">Финал истории</p>
        ${img ? `<img src="${esc(img)}" style="max-width:100%;max-height:300px;border-radius:12px;margin:16px auto;display:block">` : ''}
        <h1 style="color:var(--accent)">${esc(r.ending.title)}</h1>
        <p style="font-size:16px;margin:24px 0;line-height:1.6;max-width:600px;margin-left:auto;margin-right:auto">${esc(r.ending.desc)}</p>
        <div class="row center" style="margin-top:24px">
          <button class="btn primary" id="share-result-link">🔗 Скопировать ссылку</button>
          <a class="btn ghost" href="#/">К тестам</a>
        </div>
      </div>`;
    } else if (r.mode === 'tournament') {
      const img = safeImg(r.winner && r.winner.image);
      main = `<div class="card center">
        <h1>Победитель турнира</h1>
        ${img ? `<img src="${esc(img)}" style="max-width:100%;max-height:300px;border-radius:12px;margin:16px auto;display:block">` : ''}
        <h2 style="color:var(--accent);margin-top:20px">${esc(r.winner.text)}</h2>
        <div class="row center" style="margin-top:24px">
          <button class="btn primary" id="share-result-link">🔗 Скопировать ссылку</button>
          <a class="btn ghost" href="#/">К тестам</a>
        </div>
      </div>`;
    } else if (r.mode === 'diagram') {
      main = `<div class="card center">
        <h1>Твой результат</h1>
        <p class="muted">${esc(r.title)}</p>
        <h2 style="color:var(--accent)">Ты — <span class="grad">${esc(r.winner.title)}</span>!</h2>
        ${r.winner.desc ? `<p style="margin:16px 0">${esc(r.winner.desc)}</p>` : ''}
        <div class="row center" style="margin-top:24px">
          <button class="btn primary" id="share-result-link">🔗 Ссылка</button>
          <a class="btn ghost" href="#/">К тестам</a>
        </div>
      </div>`;
    } else {
      const pct = Math.max(0, Math.min(100, Number(r.percent) || 0));
      const msg = pct >= 90 ? 'Блестяще! 🏆' : pct >= 70 ? 'Отлично! 🎉' : pct >= 50 ? 'Неплохо 💪' : 'Повтори 📚';
      main = `<div class="card center">
        <p class="muted">${esc(r.title)}</p>
        <div class="score-circle" style="--p:${pct}"><span>${pct}%</span></div>
        <h2>${msg}</h2>
        <p class="muted">Правильно ${esc(r.correct)} из ${esc(r.total)}</p>
        <div class="row center" style="margin-top:24px">
          <button class="btn primary" id="share-result-link">🔗 Ссылка</button>
          <button class="btn ghost" id="share-result-img">🖼 Картинка</button>
          <a class="btn ghost" href="#/">К тестам</a>
        </div>
        <div style="margin-top:32px; border-top:1px solid var(--border); padding-top:20px; max-width:400px; margin-left:auto; margin-right:auto; text-align:left">
          ${renderFeedbackForm(r.testId)}
        </div>
      </div>
      <h3>Разбор</h3>
      ${(r.review || []).map((it, i) => `<div class="card review ${it.ok ? 'ok' : 'bad'}">
        <div class="row between"><b>${i + 1}. ${esc(it.q.text)}</b><span class="badge ${it.ok ? 'good' : 'wrong'}">${it.ok ? '✓' : '✗'}</span></div>
        <p class="small"><span class="muted">Твой ответ:</span> ${it.sel.length ? it.sel.map(id => esc(it.q.answers.find(a => a.id === id)?.text || '')).join(', ') : '<i>нет ответа</i>'}</p>
        ${it.ok ? '' : `<p class="small"><span class="muted">Правильный ответ:</span> ${it.right.map(id => esc(it.q.answers.find(a => a.id === id)?.text || '')).join(', ')}</p>`}
      </div>`).join('')}`;
    }
    return `<div class="wrap wide"><div class="result-layout"><div class="result-main">${main}</div><div class="result-sidebar sidebar-sticky"><div class="sidebar-comments" id="comments-box"><h3>Комментарии</h3><p class="muted small">Загрузка…</p></div></div></div></div>`;
  }

  function renderFeedbackForm(testId) {
    const voted = myVote(testId);
    return `<div style="background:var(--panel2); padding:16px; border-radius:12px; border:1px solid var(--border)">
      <h3 style="margin-top:0;font-size:16px">Оценить тест</h3>
      <div class="row">
        <button class="btn ghost sm ${voted === 'like' ? 'active-vote' : ''}" data-vote="like">👍 Нравится</button>
        <button class="btn ghost sm ${voted === 'dislike' ? 'active-vote' : ''}" data-vote="dislike">👎 Не нравится</button>
      </div>
      <div style="margin-top:12px">
        <textarea class="input" id="fb-comment" rows="2" maxlength="${LIM.comment}" placeholder="Комментарий..."></textarea>
        <button class="btn ghost sm" id="fb-submit" style="margin-top:8px">Отправить</button>
      </div>
    </div>`;
  }

  function bindResult() {
    const r = lastResult; if (!r) return;

    const shareLink = $('#share-result-link'); if (shareLink) shareLink.addEventListener('click', () => {
      const base = location.origin + location.pathname;
      const url = r.mode === 'standard' || r.mode === 'time' || r.mode === 'survival'
        ? base + `#/result?id=${enc(r.testId)}&c=${enc(r.correct)}&t=${enc(r.total)}&time=${enc(r.time)}&p=${enc(r.percent)}`
        : base + `#/result?id=${enc(r.testId)}`;
      if (navigator.share) navigator.share({ title: 'Мой результат', text: `Я прошёл «${r.title}»!`, url }).catch(() => {});
      else navigator.clipboard.writeText(url).then(() => toast('Скопировано ✓', 'good'));
    });
    const shareImg = $('#share-result-img'); if (shareImg) shareImg.addEventListener('click', () => generateSharePoster(r));

    $$('[data-vote]').forEach(btn => {
      btn.addEventListener('click', async () => {
        const t = getTest(r.testId); if (!t) return;
        const type = btn.dataset.vote;
        const next = myVote(t.id) === type ? null : type;
        const path = `/votes/${enc(t.id)}/${enc(state.user.id)}.json`;
        try {
          if (next) await fbWrite(path, 'PUT', next); else await fbWrite(path, 'DELETE');
        } catch (e) { writeErrorToast(e); return; }
        state.votes[t.id] = state.votes[t.id] || {};
        if (next) state.votes[t.id][state.user.id] = next; else delete state.votes[t.id][state.user.id];
        $$('[data-vote]').forEach(b => b.classList.toggle('active-vote', b.dataset.vote === next));
        toast(next ? 'Оценка сохранена' : 'Оценка снята', 'good');
      });
    });

    const submitBtn = $('#fb-submit');
    if (submitBtn) {
      submitBtn.addEventListener('click', async () => {
        submitBtn.disabled = true;
        const ok = await postComment(r.testId, $('#fb-comment').value);
        submitBtn.disabled = false;
        if (ok) { $('#fb-comment').value = ''; mountComments(r.testId, false); }
      });
    }

    if (getTest(r.testId)) mountComments(r.testId, false);
    else { const box = $('#comments-box'); if (box) box.innerHTML = ''; }

    if (r.percent >= 70 && r.mode === 'standard') confetti();
  }

  function confetti() { const c = ['#a855f7','#ec4899','#22c55e','#f59e0b','#3b82f6']; for (let i = 0; i < 80; i++) { const d = document.createElement('div'); d.className = 'confetti'; d.style.left = Math.random() * 100 + 'vw'; d.style.background = c[i % c.length]; d.style.animationDelay = (Math.random() * 0.6) + 's'; document.body.appendChild(d); setTimeout(() => d.remove(), 3200); } }
  async function generateSharePoster(r) { const canvas = document.createElement('canvas'); canvas.width = 600; canvas.height = 800; const ctx = canvas.getContext('2d'); const grd = ctx.createLinearGradient(0, 0, 600, 800); grd.addColorStop(0, '#171225'); grd.addColorStop(1, '#2c2444'); ctx.fillStyle = grd; ctx.fillRect(0, 0, 600, 800); ctx.strokeStyle = '#a855f7'; ctx.lineWidth = 4; ctx.strokeRect(20, 20, 560, 760); ctx.fillStyle = '#ece9f5'; ctx.font = 'bold 36px sans-serif'; ctx.textAlign = 'center'; ctx.fillText('Пикуко 2', 300, 100); ctx.fillStyle = '#9b93b8'; ctx.font = '24px sans-serif'; ctx.fillText(String(r.title).substring(0, 30), 300, 160); if (r.mode === 'diagram' || r.mode === 'tournament') { ctx.fillStyle = '#22c55e'; ctx.font = 'bold 60px sans-serif'; ctx.fillText('Мой выбор:', 300, 300); ctx.fillStyle = '#ffffff'; ctx.font = 'bold 80px sans-serif'; ctx.fillText(String(r.winner.title || r.winner.text), 300, 400); } else { const cx = 300, cy = 380, radius = 140; ctx.beginPath(); ctx.arc(cx, cy, radius, 0, Math.PI * 2); ctx.strokeStyle = '#3b2a5c'; ctx.lineWidth = 20; ctx.stroke(); const endAngle = (Math.PI * 2) * (r.percent / 100) - Math.PI / 2; ctx.beginPath(); ctx.arc(cx, cy, radius, -Math.PI / 2, endAngle); ctx.strokeStyle = '#a855f7'; ctx.lineWidth = 20; ctx.stroke(); ctx.fillStyle = '#ffffff'; ctx.font = 'bold 80px sans-serif'; ctx.textAlign = 'center'; ctx.textBaseline = 'middle'; ctx.fillText(r.percent + '%', cx, cy); ctx.fillStyle = '#22c55e'; ctx.font = 'bold 36px sans-serif'; ctx.textBaseline = 'alphabetic'; ctx.fillText(`${r.correct} из ${r.total}`, 300, 620); } ctx.fillStyle = '#9b93b8'; ctx.font = '20px sans-serif'; ctx.fillText(`Время: ${fmtTime(r.time)}`, 300, 670); ctx.fillStyle = '#a855f7'; ctx.font = '18px sans-serif'; ctx.fillText('Попробуй и ты!', 300, 730); canvas.toBlob(async (blob) => { const file = new File([blob], 'pikuko-result.png', { type: 'image/png' }); if (navigator.canShare && navigator.canShare({ files: [file] })) { try { await navigator.share({ files: [file], title: 'Мой результат', text: `Мой результат в «${r.title}»!` }); } catch (e) {} } else { const url = URL.createObjectURL(blob); const a = document.createElement('a'); a.href = url; a.download = 'pikuko-result.png'; a.click(); URL.revokeObjectURL(url); toast('Сохранено ✓', 'good'); } }, 'image/png'); }

  // ---------- Редактор ----------
  function emptyDraft() {
    return { id: null, title: '', description: '', mode: 'standard', categories: [], endings: [], questions: [newQuestion()], previewImage: null };
  }

  function startEditor(id) {
    if (id) {
      const t = getTest(id);
      if (!t) { location.hash = '#/'; return; }
      if (t.authorId !== state.user.id) { toast('Это не ваш тест', 'warn'); location.hash = '#/test/' + enc(id); return; }
      draft = JSON.parse(JSON.stringify(t));
    } else {
      const saved = store.get('draft', null);
      if (saved && confirm('У вас есть незаконченный тест. Восстановить его?')) {
        draft = normTest(uid(), saved);
        draft.id = null;
        draft.createdAt = undefined;
      } else {
        store.del('draft');
        draft = emptyDraft();
      }
    }

    if (!draft.mode) draft.mode = 'standard';
    if (!Array.isArray(draft.endings)) draft.endings = [];
    if (draft.mode === 'diagram' && !draft.endings.length) draft.endings = [{ id: uid(), title: 'Результат 1', desc: '' }];
    if (draft.mode === 'tournament' && !draft.stageSize) draft.stageSize = 3;
    draft.questions.forEach(q => q.answers.forEach(a => { a.points = a.points || {}; }));

    renderEditor();
  }

  function saveDraftState() {
    if (draft && !draft.id) store.set('draft', draft);
  }

  // Загрузка и сжатие картинки; в тест попадает только проверенный data:image.
  function compressImage(file, cb) {
    if (!file) return;
    if (!/^image\/(png|jpeg|webp|gif)$/.test(file.type)) { toast('Поддерживаются PNG, JPEG, WebP, GIF', 'warn'); return; }
    toast('Сжимаем картинку...', 'warn');
    new Compressor(file, {
      quality: 0.6, maxWidth: 400, maxHeight: 400,
      success(res) {
        const reader = new FileReader();
        reader.onload = ev => {
          const img = safeImg(ev.target.result);
          if (!img) { toast('Картинка слишком большая или неподдерживаемого формата', 'warn'); return; }
          cb(img);
        };
        reader.readAsDataURL(res);
      },
      error(err) { console.error(err); toast('Не удалось обработать картинку', 'warn'); }
    });
  }

  function renderEditor() {
    const isDiagram = draft.mode === 'diagram';
    const isTree = draft.mode === 'tree';
    const isTournament = draft.mode === 'tournament';

    $('#app').innerHTML = `<div class="wrap narrow">
      <a href="#/" class="muted small" id="cancel-editor">← Отмена</a>
      <div class="row between" style="margin-top:8px"><h1 style="margin:0">${draft.id ? 'Редактирование' : 'Новый тест'}</h1><button class="btn primary" id="save">Сохранить</button></div>

      <label class="label">Название (макс. ${LIM.title} символов)</label>
      <input class="input" id="e-title" maxlength="${LIM.title}" value="${esc(draft.title)}">

      <label class="label">Описание (макс. ${LIM.desc} символов)</label>
      <textarea class="input" id="e-desc" rows="3" maxlength="${LIM.desc}">${esc(draft.description)}</textarea>

      <label class="label">Превью (обложка теста)</label>
      <div class="row">
        <input type="file" accept="image/png,image/jpeg,image/webp,image/gif" id="e-preview" style="display:none">
        <button class="btn ghost sm" data-pick="e-preview">📷 Загрузить обложку</button>
        ${draft.previewImage ? `<button class="btn danger sm" id="del-preview">Удалить обложку</button>` : ''}
      </div>
      ${draft.previewImage ? `<img src="${esc(draft.previewImage)}" style="max-height:150px;border-radius:12px;margin-top:12px;border:1px solid var(--border)">` : ''}

      <div class="row" style="margin-top:16px"><div style="flex:1"><label class="label">Режим</label><select class="input" id="e-mode">
        <option value="standard" ${draft.mode === 'standard' ? 'selected' : ''}>📝 Обычный</option>
        <option value="time" ${draft.mode === 'time' ? 'selected' : ''}>⏱ На время</option>
        <option value="survival" ${draft.mode === 'survival' ? 'selected' : ''}>💀 Выживание</option>
        <option value="tournament" ${draft.mode === 'tournament' ? 'selected' : ''}>🏆 Турнир</option>
        <option value="tree" ${draft.mode === 'tree' ? 'selected' : ''}>🌳 Древо</option>
        <option value="diagram" ${draft.mode === 'diagram' ? 'selected' : ''}>📊 Диаграмма</option>
      </select></div></div>

      ${(isDiagram || isTree) ? `
        <div style="margin-top:24px">
          <label class="label">Концовки / Результаты</label>
          <div id="endings-list">${renderEndingsHTML()}</div>
          <button class="btn ghost sm" id="add-ending" style="margin-top:8px">+ Добавить результат</button>
        </div>
      ` : ''}

      <div id="qlist" class="qlist" style="margin-top:24px"></div>
      <button class="btn ghost" id="add-q">+ Добавить ${isTournament ? 'вариант' : 'вопрос'}</button>

      <div class="row center" style="margin-top:32px;margin-bottom:64px">
        <button class="btn primary" id="save-bottom" style="min-width:200px">Сохранить</button>
      </div>
    </div>`;
    renderQuestions();

    $('#cancel-editor').addEventListener('click', () => {
      if (draft.id) return; // редактирование существующего теста — черновик не нужен
      if (confirm('Сохранить черновик, чтобы продолжить позже?')) saveDraftState();
      else store.del('draft');
    });

    $('#e-title').addEventListener('input', e => { draft.title = e.target.value.slice(0, LIM.title); saveDraftState(); });
    $('#e-desc').addEventListener('input', e => { draft.description = e.target.value.slice(0, LIM.desc); saveDraftState(); });

    $('#e-preview').addEventListener('change', e => {
      compressImage(e.target.files[0], img => {
        draft.previewImage = img;
        saveDraftState();
        renderEditor();
        toast('Обложка добавлена ✓', 'good');
      });
    });

    if ($('#del-preview')) $('#del-preview').addEventListener('click', () => {
      draft.previewImage = null;
      saveDraftState();
      renderEditor();
    });

    $('#e-mode').addEventListener('change', e => {
      draft.mode = MODES.includes(e.target.value) ? e.target.value : 'standard';
      if (draft.mode === 'diagram' && !draft.endings.length) draft.endings = [{ id: uid(), title: 'Результат 1', desc: '' }];
      saveDraftState();
      renderEditor();
    });

    if ($('#add-ending')) {
      $('#add-ending').addEventListener('click', () => {
        if (draft.endings.length >= 20) { toast('Максимум 20 результатов', 'warn'); return; }
        draft.endings.push({ id: uid(), title: 'Новый финал', desc: '' });
        saveDraftState();
        renderEditor();
      });
      bindEndings();
    }

    $('#add-q').addEventListener('click', () => {
      if (draft.questions.length >= 100) { toast('Максимум 100 вопросов', 'warn'); return; }
      draft.questions.push(newQuestion()); saveDraftState(); renderQuestions();
    });
    $('#save').addEventListener('click', saveDraft);
    $('#save-bottom').addEventListener('click', saveDraft);
    bindQuestions();
  }

  function renderEndingsHTML() {
    if (!draft.endings.length) return '<p class="muted small">Нет добавленных результатов.</p>';
    return draft.endings.map((e, i) => `
      <div class="ending-card" data-ei="${i}">
        <div class="row between" style="margin-bottom:8px">
          <b>Результат ${i + 1}</b>
          <button class="btn danger sm" data-act="del-ending">Удалить</button>
        </div>
        <input class="input" placeholder="Заголовок (например: Победа)" maxlength="${LIM.eTitle}" value="${esc(e.title)}" data-etitle style="margin-bottom:8px">
        <textarea class="input" placeholder="Текст концовки" maxlength="${LIM.eDesc}" data-edesc rows="2">${esc(e.desc)}</textarea>
        <div class="row" style="margin-top:8px">
          <input type="file" accept="image/png,image/jpeg,image/webp,image/gif" data-eimage style="display:none" id="eimg-${i}">
          <button class="btn ghost sm" data-pick="eimg-${i}">📷 Прикрепить картинку</button>
          ${e.image ? `<button class="btn danger sm" data-act="del-eimg">Удалить картинку</button>` : ''}
        </div>
        ${e.image ? `<img src="${esc(e.image)}" class="q-img" style="max-height:150px">` : ''}
      </div>
    `).join('');
  }

  function bindEndings() {
    const list = $('#endings-list');
    list.addEventListener('input', e => {
      const ei = e.target.closest('[data-ei]')?.dataset.ei;
      if (ei == null) return;
      const ending = draft.endings[ei];
      if (e.target.matches('[data-etitle]')) ending.title = e.target.value.slice(0, LIM.eTitle);
      if (e.target.matches('[data-edesc]')) ending.desc = e.target.value.slice(0, LIM.eDesc);
      saveDraftState();
    });
    list.addEventListener('change', e => {
      if (!e.target.matches('[data-eimage]')) return;
      const ei = +e.target.closest('[data-ei]').dataset.ei;
      compressImage(e.target.files[0], img => {
        draft.endings[ei].image = img;
        saveDraftState();
        renderEditor();
        toast('Картинка добавлена ✓', 'good');
      });
    });
    list.addEventListener('click', e => {
      const btn = e.target.closest('[data-act]');
      if (!btn) return;
      const ei = +btn.closest('[data-ei]').dataset.ei;
      if (btn.dataset.act === 'del-ending') {
        if (!confirm('Удалить результат?')) return;
        draft.endings.splice(ei, 1);
        saveDraftState();
        renderEditor();
      } else if (btn.dataset.act === 'del-eimg') {
        draft.endings[ei].image = null;
        saveDraftState();
        renderEditor();
      }
    });
  }

  function renderQuestions() { $('#qlist').innerHTML = draft.questions.map((q, i) => questionCard(q, i)).join(''); }

  function optionsHTML(list, cur) {
    return list.map(o => `<option value="${esc(o.v)}" ${o.v === cur ? 'selected' : ''}>${esc(o.l)}</option>`).join('');
  }

  function questionCard(q, qi) {
    const isTree = draft.mode === 'tree';
    const isDiagram = draft.mode === 'diagram';
    const isTournament = draft.mode === 'tournament';

    if (isTournament) {
      return `<div class="card q-card" data-qi="${qi}">
        <div class="row between"><b>Вариант ${qi + 1}</b><button class="btn danger sm" data-act="del-q">Удалить</button></div>
        <input class="input" style="margin-top:8px" data-qtext maxlength="${LIM.qText}" value="${esc(q.text)}" placeholder="Название предмета (например: Красноярск)">
        <div class="row" style="margin-top:8px">
          <input type="file" accept="image/png,image/jpeg,image/webp,image/gif" data-qimage style="display:none" id="img-${qi}">
          <button class="btn ghost sm" data-pick="img-${qi}">📷 Картинка</button>
          ${q.image ? `<button class="btn danger sm" data-act="del-img">Удалить</button>` : ''}
        </div>
        ${q.image ? `<img src="${esc(q.image)}" class="q-img" style="max-height:150px">` : ''}
      </div>`;
    }

    const treeTargets = isTree ? [
      { v: '', l: 'Следующий по порядку' },
      ...draft.questions.map((o, idx) => o.id !== q.id ? { v: 'Q_' + o.id, l: `Вопрос ${idx + 1}: ${o.text.substring(0, 15)}...` } : null).filter(Boolean),
      ...draft.endings.map(e => ({ v: 'E_' + e.id, l: 'Результат: ' + e.title }))
    ] : [];
    const diagramTargets = isDiagram ? [{ v: '', l: 'Без балла' }, ...draft.endings.map(e => ({ v: e.id, l: e.title }))] : [];

    return `<div class="card q-card" data-qi="${qi}">
      <div class="row between"><b>Вопрос ${qi + 1}</b><button class="btn danger sm" data-act="del-q">Удалить</button></div>
      <textarea class="input" data-qtext maxlength="${LIM.qText}" rows="2">${esc(q.text)}</textarea>
      <div class="row" style="margin-top:8px"><input type="file" accept="image/png,image/jpeg,image/webp,image/gif" data-qimage style="display:none" id="img-${qi}"><button class="btn ghost sm" data-pick="img-${qi}">📷 Картинка</button>${q.image ? `<button class="btn danger sm" data-act="del-img">Удалить</button>` : ''}</div>
      ${q.image ? `<img src="${esc(q.image)}" class="q-img" style="max-height:150px">` : ''}

      ${!isDiagram && !isTree ? `<div class="row"><select class="input" data-qtype style="max-width:220px"><option value="single" ${q.type === 'single' ? 'selected' : ''}>Один</option><option value="multi" ${q.type === 'multi' ? 'selected' : ''}>Несколько</option></select></div>` : ''}

      <div class="alist">
        ${q.answers.map((a, ai) => `<div class="arow" data-ai="${ai}">
          ${!isDiagram && !isTree ? `<button class="mark ${a.correct ? 'on' : ''}" data-act="correct">${a.correct ? '✓' : ''}</button>` : ''}
          <input class="input" data-atext maxlength="${LIM.aText}" value="${esc(a.text)}">
          ${isTree ? `<select class="input" data-anext style="max-width:250px;font-size:12px">${optionsHTML(treeTargets, a.nextId || '')}</select>` : ''}
          ${isDiagram ? `<select class="input" data-acat style="max-width:250px;font-size:12px">${optionsHTML(diagramTargets, Object.keys(a.points || {})[0] || '')}</select>` : ''}
          <button class="btn danger sm" data-act="del-a">✕</button>
        </div>`).join('')}
      </div>
      <button class="btn ghost sm" data-act="add-a" style="margin-top:10px">+ Ответ</button>
    </div>`;
  }

  function refreshQuestion(qi) { const el = $(`[data-qi="${qi}"]`, $('#qlist')); if (el) el.outerHTML = questionCard(draft.questions[qi], qi); }

  function bindQuestions() {
    const list = $('#qlist');
    list.addEventListener('input', e => {
      const qi = e.target.closest('[data-qi]')?.dataset.qi; if (qi == null) return;
      const q = draft.questions[qi], ai = e.target.closest('[data-ai]')?.dataset.ai;
      if (e.target.matches('[data-qtext]')) q.text = e.target.value.slice(0, LIM.qText);
      else if (e.target.matches('[data-atext]') && ai != null) q.answers[ai].text = e.target.value.slice(0, LIM.aText);
      saveDraftState();
    });
    list.addEventListener('change', e => {
      const qi = e.target.closest('[data-qi]')?.dataset.qi; if (qi == null) return;
      const q = draft.questions[qi], ai = e.target.closest('[data-ai]')?.dataset.ai;
      if (e.target.matches('[data-qimage]')) {
        compressImage(e.target.files[0], img => { q.image = img; saveDraftState(); refreshQuestion(qi); toast('Готово', 'good'); });
      } else if (e.target.matches('[data-qtype]')) {
        q.type = e.target.value === 'multi' ? 'multi' : 'single';
        if (q.type === 'single') { let seen = false; q.answers.forEach(a => { if (a.correct) { if (seen) a.correct = false; else seen = true; } }); }
        saveDraftState(); refreshQuestion(qi);
      } else if (e.target.matches('[data-anext]')) {
        q.answers[ai].nextId = e.target.value || null; saveDraftState();
      } else if (e.target.matches('[data-acat]')) {
        const endId = e.target.value;
        q.answers[ai].points = endId ? { [endId]: 1 } : {};
        saveDraftState();
      }
    });
    list.addEventListener('click', e => {
      const btn = e.target.closest('[data-act]'); if (!btn) return; e.preventDefault();
      const qi = +btn.closest('[data-qi]').dataset.qi, q = draft.questions[qi];
      const ai = btn.closest('[data-ai]') ? +btn.closest('[data-ai]').dataset.ai : null, act = btn.dataset.act;
      if (act === 'del-q') { if (draft.questions.length <= 1) { alert('Хотя бы 1'); return; } if (!confirm('Удалить?')) return; draft.questions.splice(qi, 1); saveDraftState(); renderQuestions(); }
      else if (act === 'add-a') { if (q.answers.length >= 20) { toast('Максимум 20 ответов', 'warn'); return; } q.answers.push(newAnswer()); saveDraftState(); refreshQuestion(qi); }
      else if (act === 'del-a') { if (q.answers.length <= 2) { alert('Минимум 2'); return; } q.answers.splice(ai, 1); saveDraftState(); refreshQuestion(qi); }
      else if (act === 'correct') { if (q.type === 'single') q.answers.forEach((a, i) => { a.correct = (i === ai); }); else q.answers[ai].correct = !q.answers[ai].correct; saveDraftState(); refreshQuestion(qi); }
      else if (act === 'del-img') { q.image = null; saveDraftState(); refreshQuestion(qi); }
    });
  }

  async function saveDraft() {
    if (!draft.title.trim()) { alert('Введите название'); return; }
    if (draft.mode === 'diagram' && !draft.endings.length) { alert('Добавьте хотя бы один результат'); return; }
    if (draft.mode === 'tournament' && draft.questions.length < 2) { alert('Для турнира нужно минимум 2 варианта'); return; }

    for (let i = 0; i < draft.questions.length; i++) {
      const q = draft.questions[i];
      if (!q.text.trim()) { alert(`${draft.mode === 'tournament' ? 'Вариант' : 'Вопрос'} ${i + 1}: нет текста`); return; }
      if (draft.mode !== 'tournament') {
        if (q.answers.length < 2) { alert(`Вопрос ${i + 1}: мало ответов`); return; }
        if (q.answers.some(a => !a.text.trim())) { alert(`Вопрос ${i + 1}: пустые ответы`); return; }
        if (draft.mode === 'standard' && !q.answers.some(a => a.correct)) { alert(`Вопрос ${i + 1}: нет верного`); return; }
      }
    }

    const isNew = !draft.id;
    const test = { ...draft, id: draft.id || uid(), createdAt: draft.createdAt || Date.now() };
    const btns = [$('#save'), $('#save-bottom')].filter(Boolean);
    btns.forEach(b => b.disabled = true);
    const saved = await persistTest(test);
    btns.forEach(b => b.disabled = false);
    if (!saved) return;
    if (isNew) store.del('draft');
    location.hash = '#/test/' + enc(saved.id);
  }

  // ---------- Профиль ----------
  function viewProfile() {
    const u = state.user;
    const mine = state.tests.filter(t => t.authorId === u.id);
    if (u.isGuest) {
      return `<div class="wrap narrow"><div class="card">
        <div class="row" style="margin-bottom:20px">
          <div class="avatar">${esc(u.avatar)}</div>
          <div>
            <h2 style="margin:0">${esc(u.name)}</h2>
            <p class="muted small" style="margin:0">Зарегистрируйтесь, чтобы сохранить тесты!</p>
          </div>
        </div>
        <div class="auth-tabs"><div class="auth-tab active" id="tab-login">Вход</div><div class="auth-tab" id="tab-register">Регистрация</div></div>
        <div id="form-login">
          <p class="muted small">При входе в существующий аккаунт тесты, созданные гостем, останутся у гостя. Чтобы их сохранить — зарегистрируйтесь.</p>
          <label class="label">Email</label><input class="input" id="auth-login" type="email" autocomplete="email" placeholder="you@example.com">
          <label class="label">Пароль</label><input class="input" id="auth-pass" type="password" autocomplete="current-password" placeholder="Пароль">
          <button class="btn primary" id="btn-login" style="margin-top:16px;width:100%">Войти</button>
        </div>
        <div id="form-register" style="display:none">
          <label class="label">Email</label><input class="input" id="reg-login" type="email" autocomplete="email" placeholder="you@example.com">
          <label class="label">Имя (Ник)</label><input class="input" id="reg-name" maxlength="${LIM.name}" placeholder="Ник">
          <label class="label">Пароль (мин. 8 символов)</label><input class="input" id="reg-pass" type="password" autocomplete="new-password" placeholder="Пароль">
          <button class="btn primary" id="btn-register" style="margin-top:16px;width:100%">Создать</button>
        </div>
        </div>
        <h3>Мои тесты (Гость)</h3><div class="grid">${mine.map(testCard).join('') || '<p class="muted">Пусто.</p>'}</div>
      </div>`;
    }
    return `<div class="wrap narrow">
      <div class="card">
        <div class="row between">
          <div class="row">
            <div class="avatar">${esc(u.avatar)}</div>
            <div>
              <h2 style="margin:0">${esc(u.name)}</h2>
              <p class="muted small" style="margin:0">Email: ${esc(u.email)}</p>
            </div>
          </div>
          <div class="row">
            <button class="btn ghost sm" id="btn-change-avatar">Сменить аватар</button>
            <button class="btn danger sm" id="btn-logout">Выйти</button>
          </div>
        </div>
        <div id="avatar-picker" style="display:none;margin-top:16px;padding-top:16px;border-top:1px solid var(--border)">
          <label class="label">Выбери животное:</label>
          <div class="emoji-grid">
            ${EMOJIS.map(e => `<button class="emoji-btn" data-emoji="${e}">${e}</button>`).join('')}
          </div>
        </div>
      </div>
      <h3>Мои тесты</h3>
      <div class="grid">${mine.map(testCard).join('') || '<p class="muted">Пусто.</p>'}</div>
    </div>`;
  }

  function bindProfile() {
    if (state.user.isGuest) {
      const tabLogin = $('#tab-login'), tabReg = $('#tab-register'), formLogin = $('#form-login'), formReg = $('#form-register');
      tabLogin.addEventListener('click', () => { tabLogin.classList.add('active'); tabReg.classList.remove('active'); formLogin.style.display = 'block'; formReg.style.display = 'none'; });
      tabReg.addEventListener('click', () => { tabReg.classList.add('active'); tabLogin.classList.remove('active'); formReg.style.display = 'block'; formLogin.style.display = 'none'; });

      $('#btn-login').addEventListener('click', async () => {
        const email = $('#auth-login').value.trim(), p = $('#auth-pass').value;
        if (!email || !p) { toast('Заполните поля', 'warn'); return; }
        await doLogin(email, p);
      });

      $('#btn-register').addEventListener('click', async () => {
        const email = $('#reg-login').value.trim(), n = $('#reg-name').value.trim(), p = $('#reg-pass').value;
        if (!email || !p) { toast('Заполните Email и пароль', 'warn'); return; }
        if (await doRegister(email, p, n || email.split('@')[0])) render();
      });
    } else {
      const picker = $('#avatar-picker');
      $('#btn-change-avatar').addEventListener('click', () => {
        picker.style.display = picker.style.display === 'none' ? 'block' : 'none';
      });

      $$('.emoji-btn').forEach(btn => {
        btn.addEventListener('click', async () => {
          const avatar = btn.dataset.emoji;
          if (!EMOJIS.includes(avatar)) return;
          try {
            await fbWrite(`/users/${enc(state.user.id)}.json`, 'PATCH', { avatar });
          } catch (e) { writeErrorToast(e); return; }
          state.user.avatar = avatar;
          toast('Аватар обновлен ✓', 'good');
          render();
        });
      });

      $('#btn-logout').addEventListener('click', () => {
        if (confirm('Вы собираетесь выйти из аккаунта. Вы уверены?')) doLogout();
      });
    }
  }

  // ---------- Старт ----------
  let booted = false;
  function hideLoader() { const l = document.getElementById('loading'); if (l) l.style.display = 'none'; }

  function init() {
    applyTheme();

    // Кнопки «выбрать файл» без inline onclick (совместимо со строгим CSP)
    document.addEventListener('click', e => {
      const b = e.target.closest('[data-pick]');
      if (!b) return;
      e.preventDefault();
      const inp = document.getElementById(b.dataset.pick);
      if (inp) inp.click();
    });

    const tt = $('#theme-toggle');
    if (tt) tt.addEventListener('click', toggleTheme);

    firebase.auth().onAuthStateChanged(async fu => {
      if (!fu) {
        try { await firebase.auth().signInAnonymously(); }
        catch (e) {
          console.error(e);
          hideLoader();
          toast('Не удалось подключиться к серверу', 'warn');
        }
        return; // onAuthStateChanged сработает ещё раз уже с анонимным пользователем
      }

      try { state.user = await loadProfile(fu); }
      catch (e) {
        console.warn('Не удалось загрузить профиль', e);
        state.user = { id: fu.uid, name: 'Гость', avatar: EMOJIS[0], isGuest: fu.isAnonymous, email: fu.email || '' };
      }

      if (!booted) {
        booted = true;
        await dbLoad();
        hideLoader();
        updatePresence();
        window.addEventListener('hashchange', render);
      }
      render();
    });
  }

  document.addEventListener('DOMContentLoaded', init);
})();
