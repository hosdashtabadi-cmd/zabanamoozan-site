# zabanamoozan-site
<!DOCTYPE html>

<html lang="fa" dir="rtl">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>پرتال زبان‌آموزان — ورود و مدیریت</title>
  <style>
    :root { --brand: #2e63f6; --muted: #6b7280; }
    * { box-sizing: border-box; }
    body { font-family: Tahoma, Arial, sans-serif; background: #f3f6fb; margin: 0; color: #111; }
    .wrap { max-width: 980px; margin: 28px auto; padding: 18px; }
    header { background: var(--brand); color: #fff; padding: 18px 20px; border-radius: 12px; }
    header h1 { margin: 0; font-size: 20px; }
    .grid { display: flex; gap: 20px; margin-top: 18px; }
    .card { background: #fff; border-radius: 12px; padding: 18px; box-shadow: 0 6px 18px rgba(20,20,60,0.06); flex: 1; }
    label { display: block; margin-bottom: 8px; color: var(--muted); }
    input, select, button { width: 100%; padding: 10px; border-radius: 8px; border: 1px solid #d1d5db; font-size: 15px; }
    button { background: var(--brand); color: #fff; border: none; cursor: pointer; }
    .muted { color: var(--muted); font-size: 13px; }
    .hidden { display: none; }
    .row { display: flex; gap: 12px; }
    .row > * { flex: 1; }
    .small { font-size: 13px; padding: 8px; }
    table { width: 100%; border-collapse: collapse; margin-top: 12px; }
    th, td { padding: 8px; border-bottom: 1px solid #eee; text-align: right; }
    .actions button { margin-left: 6px; padding: 6px 8px; font-size: 13px; }
    .ok { background: #10b981; }
    .danger { background: #ef4444; }
    footer { margin-top: 22px; text-align: center; color: var(--muted); font-size: 13px; }
    .notice { background: #eff6ff; border: 1px solid #dbeafe; padding: 10px; border-radius: 8px; color: #0f172a; }
  </style>
</head>
<body>
  <div class="wrap">
    <header>
      <h1>پرتال زبان‌آموزان — سامانه ورود و مدیریت</h1>
    </header>

```
<div class="grid">
  <div class="card" style="max-width:420px">
    <h3>ورود / ثبت‌نام</h3>
    <p class="muted">برای تست: مدیر: admin / 0000 — زبان‌آموز نمونه: student / 1234</p>
    <label for="mode">عملیات</label>
    <select id="mode">
      <option value="login">ورود</option>
      <option value="register">ثبت‌نام زبان‌آموز</option>
      <option value="admin-login">ورود مدیر</option>
    </select>
    <div id="form-area" style="margin-top:12px"></div>
    <div style="margin-top:12px"><button id="submitBtn">ادامه</button></div>
    <div class="notice" style="margin-top:14px">
      این نسخه بدون پایگاه‌داده سرور ساخته شده و از <strong>localStorage</strong> مرورگر برای ذخیره‌سازی کاربران استفاده می‌کند. برای انتشار روی اینترنت راهنمایی می‌دهم.
    </div>
  </div>

  <div class="card" id="dashboard">
    <div id="welcome">
      <h3>خوش آمدید</h3>
      <p class="muted">پس از ورود، پنل مناسب (زبان‌آموز یا مدیر) در این‌جا نمایش داده می‌شود.</p>
    </div>

    <div id="studentPanel" class="hidden">
      <h3>پنل زبان‌آموز</h3>
      <p>نام کاربری: <strong id="stuName"></strong></p>
      <p class="muted">در این نسخه می‌توانید اطلاعات پایه را ببینید و از سیستم خارج شوید.</p>
      <div style="margin-top:12px"><button id="logoutStudent" class="small">خروج</button></div>
    </div>

    <div id="adminPanel" class="hidden">
      <h3>پنل مدیریت</h3>
      <p class="muted">مدیر می‌تواند کاربران را مشاهده، حذف یا رمز عبور جدید تعیین کند.</p>
      <div style="margin-top:12px"><button id="logoutAdmin" class="small">خروج مدیر</button></div>
      <h4 style="margin-top:16px">لیست زبان‌آموزان</h4>
      <table id="usersTable"><thead><tr><th>نام کاربری</th><th>عملیات</th></tr></thead><tbody></tbody></table>
      <div style="margin-top:12px">
        <h4>افزودن زبان‌آموز دستی</h4>
        <div class="row">
          <input id="newUser" placeholder="نام کاربری" />
          <input id="newPass" placeholder="رمز (مثلاً: 1234)" />
        </div>
        <div style="margin-top:8px"><button id="addUserBtn">افزودن</button></div>
      </div>
    </div>
  </div>
</div>

<footer>© 2025 زبان‌آموزان — این نسخه محلی (local) است. برای انتشار به لینک عمومی، راهنمایی خواسته شده را بگو.</footer>
```

  </div>

<script>
const STORAGE_KEY='zaban_users_v1';
const defaultUsers=[{username:'admin',password:'0000',role:'admin'},{username:'student',password:'1234',role:'student'}];
function loadUsers(){try{const raw=localStorage.getItem(STORAGE_KEY);if(!raw){localStorage.setItem(STORAGE_KEY,JSON.stringify(defaultUsers));return defaultUsers;}return JSON.parse(raw);}catch(e){localStorage.setItem(STORAGE_KEY,JSON.stringify(defaultUsers));return defaultUsers;}}
function saveUsers(list){localStorage.setItem(STORAGE_KEY,JSON.stringify(list));}
let users=loadUsers();
const modeSelect=document.getElementById('mode');
const formArea=document.getElementById('form-area');
const submitBtn=document.getElementById('submitBtn');
const studentPanel=document.getElementById('studentPanel');
const adminPanel=document.getElementById('adminPanel');
const welcome=document.getElementById('welcome');
const stuName=document.getElementById('stuName');
const usersTable=document.querySelector('#usersTable tbody');
const newUserInput=document.getElementById('newUser');
const newPassInput=document.getElementById('newPass');
let currentUser=null;
function renderForm(){const mode=modeSelect.value;formArea.innerHTML='';if(mode==='login'){formArea.innerHTML=`<label>نام کاربری</label><input id="f_user" type="text" placeholder="نام کاربری" /><label>رمز عبور</label><input id="f_pass" type="password" placeholder="رمز" /><p class="muted">اگر حساب ندارید، از قسمت ثبت‌نام استفاده کنید.</p>`;}else if(mode==='register'){formArea.innerHTML=`<label>انتخاب نام کاربری</label><input id="f_user" type="text" placeholder="نام کاربری دلخواه" /><label>رمز عبور</label><input id="f_pass" type="password" placeholder="رمز عبور" /><p class="muted">پس از ثبت‌نام، می‌توانید با همان اطلاعات وارد شوید.</p>`;}else if(mode==='admin-login'){formArea.innerHTML=`<label>نام کاربری مدیر</label><input id="f_user" type="text" placeholder="admin" /><label>رمز مدیر</label><input id="f_pass" type="password" placeholder="0000" />`;}}
modeSelect.addEventListener('change',renderForm);renderForm();
submitBtn.addEventListener('click',()=>{const mode=modeSelect.value;const u=document.getElementById('f_user')?.value?.trim();const p=document.getElementById('f_pass')?.value||'';if(!u||!p){alert('نام کاربری و رمز را وارد کنید.');return;}if(mode==='register'){if(users.some(x=>x.username===u)){alert('این نام کاربری قبلاً وجود دارد.');return;}users.push({username:u,password:p,role:'student'});saveUsers(users);alert('ثبت‌نام با موفقیت انجام شد. اکنون وارد شوید.');modeSelect.value='login';renderForm();return;}const found=users.find(x=>x.username===u&&x.password===p);if(!found){alert('نام کاربری یا رمز اشتباه است.');return;}currentUser=found;showPanelFor(found);});
function showPanelFor(user){welcome.classList.add('hidden');if(user.role==='student'){studentPanel.classList.remove('hidden');adminPanel.classList.add('hidden');stuName.textContent=user.username;}else if(user.role==='admin'){adminPanel.classList.remove('hidden');studentPanel.classList.add('hidden');renderUsersTable();}persistSession();}
document.getElementById('logoutStudent').addEventListener('click',()=>{currentUser=null;studentPanel.classList.add('hidden');welcome.classList.remove('hidden');persistSession();});
document.getElementById('logoutAdmin').addEventListener('click',()=>{currentUser=null;adminPanel.classList.add('hidden');welcome.classList.remove('hidden');persistSession();});
function renderUsersTable(){usersTable.innerHTML='';users.filter(u=>u.role==='student').forEach(u=>{const tr=document.createElement('tr');tr.innerHTML=`<td>${u.username}</td><td class="actions"></td>`;const actions=tr.querySelector('.actions');const del=document.createElement('button');del.className='danger';del.textContent='حذف';del.onclick=()=>{if(confirm('آیا حذف شود؟')){users=users.filter(x=>x.username!==u.username);saveUsers(users);renderUsersTable();}};const reset=document.createElement('button');reset.className='ok';reset.textContent='ریست رمز';reset.onclick=()=>{const np=prompt('رمز جدید برای '+u.username,'1234');if(np){users=users.map(x=>x.username===u.username?{...x,password:np}:x);saveUsers(users);alert('رمز تغییر کرد.');renderUsersTable();}};actions.appendChild(reset);actions.appendChild(del);usersTable.appendChild(tr);});}
document.getElementById('addUserBtn').addEventListener('click',()=>{const nu=newUserInput.value.trim();const np=newPassInput.value.trim();if(!nu||!np){alert('نام کاربری و رمز را وارد کنید.');return;}if(users.some(x=>x.username===nu)){alert('این نام کاربری قبلاً وجود دارد.');return;}users.push({username:nu,password:np,role:'student'});saveUsers(users);newUserInput.value='';newPassInput.value='';renderUsersTable();alert('زبان‌آموز اضافه شد.');});
(function tryAutoLogin(){const saved=sessionStorage.getItem('zaban_current');if(saved){const u=JSON.parse(saved);const found=users.find(x=>x.username===u.username&&x.role===u.role);if(found){currentUser=found;showPanelFor(found);}}})();
function persistSession(){if(currentUser)sessionStorage.setItem('zaban_current',JSON.stringify({username:currentUser.username,role:currentUser.role}));else sessionStorage.removeItem('zaban_current');}
</script>

</body>
</html>
