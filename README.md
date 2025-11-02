<!doctype html>
<html lang="kk">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Ardak — Киім дүкені</title>
<link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@400;700&family=Playfair+Display:wght@400;700&display=swap" rel="stylesheet">
<style>
:root{
  --accent: linear-gradient(90deg,#ff6b6b,#ffb86b);
  --bg:#faf7f5;
  --card:#fff;
  --muted:#6b6b6b;
  --shadow:0 6px 18px rgba(0,0,0,0.08);
}
body{margin:0;font-family:'Montserrat',sans-serif;background:var(--bg);color:#111;}
.container{width:calc(100% - 32px);max-width:1100px;margin:0 auto;}
header{background:#fff;position:sticky;top:0;border-bottom:1px solid #eee;z-index:10;}
.header-inner{display:flex;justify-content:space-between;align-items:center;padding:14px 0;}
.logo svg{height:48px;width:auto;}
.nav{display:flex;gap:12px;}
.nav a{color:#333;text-decoration:none;font-weight:600;}
.nav a:hover{color:#ff6b6b;}
.cart-btn{background:var(--accent);border:none;color:#fff;padding:8px 14px;border-radius:8px;cursor:pointer;font-weight:700;}
.cart-btn span{background:rgba(0,0,0,0.15);padding:3px 6px;border-radius:6px;margin-left:6px;}
.hero{background:linear-gradient(180deg,rgba(255,107,107,0.08),transparent);padding:50px 0;text-align:center;}
.hero h1{font-family:'Playfair Display',serif;font-size:36px;margin-bottom:10px;}
.hero p{color:var(--muted);margin-bottom:20px;}
.btn-primary{background:var(--accent);color:#fff;border:none;padding:12px 18px;border-radius:12px;cursor:pointer;font-weight:700;text-decoration:none;}
.catalog{padding:30px 0;}
.catalog h2{text-align:center;margin-bottom:16px;}
.filters{display:flex;justify-content:center;flex-wrap:wrap;gap:12px;margin-bottom:16px;}
.filters input,.filters select{padding:8px 10px;border:1px solid #ddd;border-radius:8px;}
.grid{display:grid;gap:18px;grid-template-columns:repeat(auto-fill,minmax(220px,1fr));}
.card{background:var(--card);border-radius:12px;box-shadow:var(--shadow);padding:12px;display:flex;flex-direction:column;gap:10px;}
.card img{width:100%;height:260px;object-fit:cover;border-radius:10px;}
.card h3{margin:0;font-size:18px;}
.card .price{font-weight:700;}
.card .meta{color:var(--muted);font-size:14px;}
.cart-panel{position:fixed;right:20px;top:90px;width:320px;max-width:90vw;background:#fff;border-radius:12px;padding:12px;box-shadow:0 22px 50px rgba(0,0,0,0.15);display:none;flex-direction:column;gap:10px;}
.cart-panel.open{display:flex;}
.cart-item{display:flex;gap:10px;align-items:center;}
.cart-item img{width:60px;height:60px;object-fit:cover;border-radius:8px;}
.cart-footer{display:flex;justify-content:space-between;align-items:center;margin-top:10px;}
footer{background:#fff;border-top:1px solid #eee;text-align:center;padding:20px;margin-top:30px;color:#666;}
@media(max-width:720px){.hero h1{font-size:26px;}}
</style>
</head>
<body>

<header>
  <div class="container header-inner">
    <div class="logo">
      <svg xmlns="http://www.w3.org/2000/svg" width="160" height="50" viewBox="0 0 320 80">
        <defs>
          <linearGradient id="g" x1="0" x2="1">
            <stop offset="0" stop-color="#ff6b6b"/>
            <stop offset="1" stop-color="#ffb86b"/>
          </linearGradient>
          <style>
            .brand{font-family:'Montserrat',sans-serif;font-weight:700;fill:url(#g);font-size:32px;}
            .icon{fill:none;stroke:url(#g);stroke-width:3;stroke-linecap:round;stroke-linejoin:round;}
          </style>
        </defs>
        <g transform="translate(0,8)">
          <path class="icon" d="M40 48 L20 48 C20 48 18 48 18 42 C18 36 29 30 40 30 C51 30 62 36 62 42 C62 48 60 48 60 48 L40 48" />
          <path class="icon" d="M40 12 C40 6 34 4 30 6 C26 8 28 14 28 14" />
        </g>
        <text x="90" y="50" class="brand">Ardak</text>
      </svg>
    </div>
    <nav class="nav">
      <a href="#catalog">Каталог</a>
      <a href="#about">Біз туралы</a>
      <a href="mailto:ardak@example.com">Байланыс</a>
    </nav>
    <button class="cart-btn" id="cartToggle">🛒 <span id="cartCount">0</span></button>
  </div>
</header>

<section class="hero">
  <div class="container">
    <h1>Ardak — сәнді көйлектер бренді</h1>
    <p>Қолдан тігілген сапалы көйлектер. Сенімді жеткізу және сүйіспеншілікпен жасалған стиль.</p>
    <a href="#catalog" class="btn-primary">Каталогқа өту</a>
  </div>
</section>

<section class="catalog container" id="catalog">
  <h2>Таңдаулы көйлектер</h2>
  <div class="filters">
    <input id="search" placeholder="Іздеу...">
    <select id="priceFilter">
      <option value="all">Барлығы</option>
      <option value="0-50">0 — 50 000 ₸</option>
      <option value="50-100">50 000 — 100 000 ₸</option>
      <option value="100+">100 000 ₸+</option>
    </select>
  </div>
  <div id="productsGrid" class="grid"></div>
</section>

<section id="about" class="container">
  <h2>Біз туралы</h2>
  <p>Ardak — сән мен сапаны үйлестіретін жас қазақстандық бренд. Әрбір көйлек сүйіспеншілікпен және ұқыптылықпен тігіледі.</p>
</section>

<div class="cart-panel" id="cartPanel">
  <h3>Себет</h3>
  <div id="cartItems"></div>
  <div class="cart-footer">
    <strong id="cartTotal">0 ₸</strong>
    <button class="btn-primary" id="checkoutBtn">Сатып алу</button>
  </div>
</div>

<footer>
  © Ardak — 2025. Барлық құқық қорғалған.
</footer>

<script>
const products=[
{id:'p1',title:'Элегантты кешкі көйлек',price:85000,img:'https://images.unsplash.com/photo-1520975911609-1f6b3d5f2c2b?w=800'},
{id:'p2',title:'Күнделікті жеңіл көйлек',price:42000,img:'https://images.unsplash.com/photo-1514996937319-344454492b37?w=800'},
{id:'p3',title:'Шаңырақ стильді көйлек',price:65000,img:'https://images.unsplash.com/photo-1549208910-3f42c5f9a7d9?w=800'},
{id:'p4',title:'Романтикалық көйлек',price:98000,img:'https://images.unsplash.com/photo-1491553895911-0055eca6402d?w=800'}
];
const q=s=>document.querySelector(s);
let cart={};
const money=n=>n.toLocaleString('ru-RU')+' ₸';
function renderProducts(list){
const grid=q('#productsGrid');grid.innerHTML='';
list.forEach(p=>{
const card=document.createElement('div');
card.className='card';
card.innerHTML=`
<img src="${p.img}" alt="${p.title}">
<h3>${p.title}</h3>
<div class="price">${money(p.price)}</div>
<button class="btn-primary" onclick="addToCart('${p.id}')">Себетке қосу</button>`;
grid.appendChild(card);
});
}
function addToCart(id){cart[id]=(cart[id]||0)+1;saveCart();renderCart();}
function removeFromCart(id){delete cart[id];saveCart();renderCart();}
function saveCart(){localStorage.setItem('ardak_cart',JSON.stringify(cart));}
function loadCart(){cart=JSON.parse(localStorage.getItem('ardak_cart')||'{}');}
function renderCart(){
const box=q('#cartItems');box.innerHTML='';let total=0;const ids=Object.keys(cart);
if(ids.length==0){box.innerHTML='<p>Себет бос</p>';}
else ids.forEach(id=>{
const p=products.find(x=>x.id==id);const qty=cart[id];total+=p.price*qty;
const div=document.createElement('div');div.className='cart-item';
div.innerHTML=`<img src="${p.img}"><div><strong>${p.title}</strong><br>${money(p.price)} × ${qty} = ${money(p.price*qty)}<br>
<button onclick="removeFromCart('${id}')">Жою</button></div>`;box.appendChild(div);
});
q('#cartTotal').textContent=money(total);q('#cartCount').textContent=Object.values(cart).reduce((a,b)=>a+b,0);
}
q('#cartToggle').onclick=()=>q('#cartPanel').classList.toggle('open');
q('#checkoutBtn').onclick=()=>{
if(Object.keys(cart).length==0)return alert('Себет бос!');
let body='Ardak тапсырыс:%0A%0A';let total=0;
for(const id in cart){const p=products.find(x=>x.id==id);body+=${p.title} × ${cart[id]} = ${p.price*cart[id]} ₸%0A;total+=p.price*cart[id];}
body+=%0AЖалпы: ${total} ₸;
window.location.href=mailto:ardak@example.com?subject=Тапсырыс&body=${body};
};
q('#search').oninput=filter; q('#priceFilter').onchange=filter;
function filter(){
const text=q('#search').value.toLowerCase(),price=q('#priceFilter').value;
let f=products.filter(p=>{
let ok=p.title.toLowerCase().includes(text);
if(price=='0-50')ok&=p.price<=50000;
if(price=='50-100')ok&=p.price>50000&&p.price<=100000;
if(price=='100+')ok&=p.price>100000;
return ok;
});renderProducts(f);
}
loadCart();renderProducts(products);renderCart();
</script>
</body>
</html>
