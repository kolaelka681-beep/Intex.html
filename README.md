# Intex.html
<!doctype html>
<html lang="ru">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width,initial-scale=1,viewport-fit=cover,user-scalable=no">
<title>Перекуп 2.0</title>
<style>
:root{
  --paper:#f3efe4;--card:#fffdf6;--ink:#1c2236;--muted:#69708a;--line:#d8d0bb;
  --bar:#141c33;--wall:#22335a;--yellow:#f2c230;--green:#2a9a67;--red:#d3473d;--blue:#3566d0;
  --chip:#ebe5d3;--chipbad:#f6d9d5;--chipok:#d4ecdf;
}
@media (prefers-color-scheme:dark){
  :root{--paper:#121a2b;--card:#1b2540;--ink:#e8ebf5;--muted:#9aa3bd;--line:#2d3a5c;--chip:#27335a;--chipbad:#4a2a30;--chipok:#1f4437;--bar:#0b1120}
}
*{box-sizing:border-box;-webkit-tap-highlight-color:transparent}
html,body{margin:0;height:100%;background:#0b1120;font-family:"Segoe UI",Roboto,"Helvetica Neue",Arial,sans-serif;color:var(--ink)}
button{font:inherit;color:inherit;cursor:pointer}
#app{position:relative;max-width:480px;height:100vh;height:100dvh;margin:0 auto;display:flex;flex-direction:column;background:var(--paper);overflow:hidden}
#status{display:flex;justify-content:space-between;align-items:center;gap:8px;padding:9px 14px;font-size:13px;font-weight:700;background:var(--bar);color:#fff}
#status span{white-space:nowrap}
#screen{flex:1;overflow-y:auto;overscroll-behavior:contain;-webkit-overflow-scrolling:touch}
#app[data-mode=home] #screen,#app[data-mode=start] #screen{background-color:var(--wall);background-image:radial-gradient(rgba(255,255,255,.09) 1.2px,transparent 1.3px);background-size:18px 18px}
#nav{display:flex;justify-content:center;padding:8px 0 10px;background:var(--bar)}
#nav button{border:0;width:120px;height:6px;border-radius:6px;background:#5d6a8c;padding:0}
#toast{position:absolute;left:12px;right:12px;top:48px;z-index:50;padding:11px 14px;border-radius:12px;background:#fff;color:#1c2236;font-weight:600;font-size:14px;box-shadow:0 6px 24px rgba(0,0,0,.35);opacity:0;transform:translateY(-8px);transition:.2s;pointer-events:none}
#toast.on{opacity:1;transform:none}
#toast.bad{background:var(--red);color:#fff}
#toast.good{background:var(--green);color:#fff}
.home{padding:14px 14px 24px;color:#fff}
.widget{background:var(--card);color:var(--ink);border-radius:20px;padding:16px;margin-bottom:12px}
.widget .wc{font-weight:800;font-size:18px}
.widget .ws{color:var(--muted);font-size:13px}
.widget .wb{font-size:34px;font-weight:800;letter-spacing:-.02em;margin:6px 0 2px}
.goal{height:8px;border-radius:8px;background:var(--chip);overflow:hidden;margin-top:8px}
.goal i{display:block;height:100%;background:var(--green)}
.wallet{display:flex;flex-wrap:wrap;gap:6px;margin-bottom:12px}
.wallet span{background:rgba(255,255,255,.14);padding:5px 10px;border-radius:20px;font-size:13px;font-weight:600}
.wallet span.cur{background:var(--yellow);color:#1c2236}
.newsline{background:rgba(0,0,0,.28);border-radius:12px;padding:10px 12px;font-size:13px;margin-bottom:16px;min-height:40px}
.grid{display:grid;grid-template-columns:repeat(4,1fr);gap:16px 8px}
.app{background:none;border:0;display:flex;flex-direction:column;align-items:center;gap:6px;color:#fff;font-size:12px;font-weight:600;position:relative;padding:0}
.app .ic{width:62px;height:62px;border-radius:17px;display:grid;place-items:center;font-size:30px;box-shadow:0 3px 0 rgba(0,0,0,.25)}
.app .bd{position:absolute;top:-5px;right:2px;background:var(--red);color:#fff;border-radius:10px;font-size:11px;padding:1px 6px;font-weight:800}
.hdr{display:flex;gap:10px;align-items:center;padding:12px 14px;position:sticky;top:0;background:var(--paper);z-index:5;border-bottom:1px solid var(--line)}
.hdr h2{margin:0;font-size:20px;letter-spacing:-.01em}
.hdr .sub{font-size:12px;color:var(--muted)}
.back{border:0;background:var(--chip);width:36px;height:36px;border-radius:50%;font-size:22px;line-height:1;flex:none}
.pad{padding:14px}
.list{padding:12px 12px 24px;display:flex;flex-direction:column;gap:10px}
.sub{font-size:12px;color:var(--muted)}
.btn{border:1.5px solid var(--ink);background:var(--card);border-radius:12px;padding:9px 14px;font-weight:700;font-size:14px}
.btn.y{background:var(--yellow);color:#1c2236;border-color:#1c2236}
.btn.g{background:var(--green);color:#fff;border-color:var(--green)}
.btn.big{width:100%;padding:14px;font-size:16px}
.btn.sm{padding:6px 10px;font-size:13px}
.btn:disabled{opacity:.45}
.row{display:flex;gap:8px;align-items:center;flex-wrap:wrap}
.chips{display:flex;flex-wrap:wrap;gap:5px;margin:6px 0}
.chip{background:var(--chip);border-radius:8px;padding:3px 8px;font-size:12px;font-weight:600}
.chip.bad{background:var(--chipbad)}.chip.ok{background:var(--chipok)}.chip.q{border:1px dashed var(--muted);background:none}
.tag{display:flex;background:var(--card);border-radius:14px;border:1px solid var(--line);position:relative}
.tag .tl{flex:1;padding:12px;min-width:0}
.tag .tr{width:128px;flex:none;padding:12px 10px;border-left:2px dashed var(--line);display:flex;flex-direction:column;justify-content:center;gap:6px;align-items:stretch;text-align:center;position:relative}
.tag .tr::before,.tag .tr::after{content:"";position:absolute;left:-9px;width:16px;height:16px;border-radius:50%;background:var(--paper);border:1px solid var(--line)}
.tag .tr::before{top:-9px}.tag .tr::after{bottom:-9px}
.nm{font-weight:800;font-size:16px}
.pr{font-weight:800;font-size:18px}
.disc{font-size:12px;font-weight:800}
.disc.g{color:var(--green)}.disc.r{color:var(--red)}
.act{display:flex;justify-content:space-between;align-items:center;gap:10px;background:var(--card);border:1px solid var(--line);border-radius:14px;padding:12px;margin-top:10px}
.warn{background:var(--chipbad);padding:12px;border-radius:12px}
.box{background:var(--card);border:1px solid var(--line);border-radius:14px;padding:14px;margin-bottom:10px}
.tabs{display:flex;gap:8px;padding:10px 12px 0}
.tabs button{flex:1;border:1.5px solid var(--line);background:none;border-radius:10px;padding:8px;font-weight:700}
.tabs button.on{background:var(--ink);color:var(--paper);border-color:var(--ink)}
select,input,textarea{width:100%;font:inherit;padding:11px;border-radius:10px;border:1.5px solid var(--line);background:var(--card);color:var(--ink);margin:6px 0}
label{font-size:13px;font-weight:700}
table{width:100%;border-collapse:collapse;font-size:13px}
th,td{padding:7px 4px;text-align:right;border-bottom:1px solid var(--line)}
th:first-child,td:first-child{text-align:left}
td.hi{color:var(--green);font-weight:800}td.lo{color:var(--red);font-weight:800}
.prev{font-weight:800;font-size:18px;padding:6px 0 12px}
.start{padding:22px 16px 30px;color:#fff}
.start h1{font-size:40px;margin:6px 0 4px;letter-spacing:-.03em}
.start p{color:#c9d2ee;line-height:1.45}
.cities{display:grid;grid-template-columns:1fr 1fr;gap:8px;margin-top:14px}
.cities button{background:rgba(255,255,255,.12);border:1.5px solid rgba(255,255,255,.2);color:#fff;border-radius:12px;padding:11px;text-align:left;font-weight:700}
.cities button small{display:block;font-weight:500;color:#b9c3e3}
.cities button:active{background:var(--yellow);color:#1c2236}
.mode{display:grid;grid-template-columns:1fr;gap:8px;margin-top:12px}
.mode button{background:rgba(255,255,255,.1);border:2px solid rgba(255,255,255,.2);color:#fff;border-radius:14px;padding:14px;text-align:left;font-weight:700;font-size:15px}
.mode button b{font-size:16px}
.mode button small{display:block;font-weight:500;color:#b9c3e3;margin-top:3px}
.mode button.sel{background:var(--yellow);color:#1c2236;border-color:#fff}
.mode button.sel small{color:#3a3f52}
#overlay{position:absolute;inset:0;z-index:40;background:rgba(8,12,24,.88);display:none;align-items:center;justify-content:center;padding:14px;overflow-y:auto}
#overlay.on{display:flex}
.mg{position:relative;width:100%;max-width:400px;background:var(--card);border-radius:20px;padding:18px;text-align:center}
.mg h3{margin:0 0 4px;font-size:20px}
.mg p{margin:4px 0 12px;color:var(--muted);font-size:14px;line-height:1.4}
.flash{position:absolute;inset:0;border-radius:20px;display:grid;place-items:center;font-size:22px;font-weight:800;color:#fff}
.flash.ok{background:rgba(42,154,103,.95)}.flash.no{background:rgba(211,71,61,.95)}
.tbar{height:8px;background:var(--chip);border-radius:8px;overflow:hidden;margin:0 0 12px}
.tbar i{display:block;height:100%;width:100%;background:var(--blue)}
.board{position:relative;height:290px;background:var(--chip);border-radius:16px;margin-bottom:6px}
.screw{position:absolute;width:52px;height:52px;border-radius:50%;border:3px solid #7d869e;background:#b9c0d2;color:#1c2236;font-weight:800;font-size:18px;transition:transform .25s,opacity .25s}
.screw.out{transform:scale(.2) rotate(240deg);opacity:0;pointer-events:none}
.screw.bad{background:var(--red);color:#fff}
.track{position:relative;height:46px;background:var(--chip);border-radius:12px;margin:14px 0}
.zn{position:absolute;top:0;bottom:0;background:rgba(42,154,103,.55);border-radius:10px}
.mk{position:absolute;top:-5px;bottom:-5px;width:6px;margin-left:-3px;background:var(--ink);border-radius:3px}
.stat{font-size:14px;font-weight:700;margin:6px 0 12px}
.therm{position:relative;width:70px;height:240px;margin:0 auto 12px;background:var(--chip);border-radius:14px;overflow:hidden;border:2px solid var(--ink)}
.tf{position:absolute;left:0;right:0;bottom:0;background:#e8782a;height:5%}
.tz{position:absolute;left:0;right:0;background:rgba(42,154,103,.6)}
.tlin{position:absolute;left:0;right:0;bottom:92%;border-top:3px solid var(--red)}
.wipe{position:relative;width:240px;height:300px;margin:0 auto;background:var(--chip);border-radius:16px;overflow:hidden}
.wipe .ghost{position:absolute;inset:0;display:grid;place-items:center;font-size:150px}
.wipe canvas{position:absolute;inset:0;width:100%;height:100%;touch-action:none}
.chipgrid{display:grid;gap:8px;margin-bottom:12px}
.chipgrid button{border:1.5px solid var(--line);background:var(--card);border-radius:12px;padding:11px;text-align:left;font-size:14px;font-weight:600}
.chipgrid button.sel{background:var(--yellow);color:#1c2236;border-color:#1c2236}
.plane{font-size:44px;transition:transform 3s linear;display:inline-block}
.hagglebar{position:relative;height:60px;background:var(--chip);border-radius:12px;margin:12px 0;overflow:hidden}
.hagglebar .target{position:absolute;top:0;bottom:0;background:rgba(42,154,103,.55);border-radius:8px}
.hagglebar .needle{position:absolute;top:0;bottom:0;width:8px;margin-left:-4px;background:var(--red);border-radius:4px;transition:left .05s linear}
@media (prefers-reduced-motion:reduce){*{transition:none!important;animation:none!important}}
</style>
</head>
<body>
<div id="app" data-mode="start">
  <div id="status"></div>
  <div id="screen"></div>
  <div id="nav"><button data-a="home" aria-label="Домой"></button></div>
  <div id="toast"></div>
  <div id="overlay"></div>
</div>

<script>
'use strict';
const $=(s,r=document)=>r.querySelector(s);
const rnd=(a,b)=>a+Math.random()*(b-a);
const ri=(a,b)=>Math.floor(rnd(a,b+1));
const pick=a=>a[Math.floor(Math.random()*a.length)];
const clamp=(v,a,b)=>Math.max(a,Math.min(b,v));
const shuffle=a=>[...a].sort(()=>Math.random()-.5);
const esc=s=>String(s).replace(/[&<>"]/g,c=>({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;'}[c]));
const sleep=ms=>new Promise(r=>setTimeout(r,ms));

/* ---------- валюты ---------- */
const CUR={EUR:{sym:'€',rate:1},PLN:{sym:'zł',rate:4.3},CZK:{sym:'Kč',rate:25},BYN:{sym:'Br',rate:3.4},RUB:{sym:'₽',rate:100}};
const fmt=(n,c)=>{const s=Math.round(n).toLocaleString('ru-RU');return c==='EUR'?'€'+s:s+' '+CUR[c].sym};

/* ---------- режимы ---------- */
const MODES={
  easy:{n:'Лёгкий',start:600,priceMod:0.85,taxRate:0.06,desc:'600€ · цены −15% · налог 6%'},
  normal:{n:'Средний',start:300,priceMod:1.0,taxRate:0.10,desc:'300€ · обычные цены · налог 10%'},
  hard:{n:'Хард',start:150,priceMod:1.25,taxRate:0.14,desc:'150€ · цены +25% · налог 14%'}
};

/* ---------- города ---------- */
const CITIES=[
 {id:'minsk',name:'Минск',cur:'BYN',lat:53.9,lon:27.57,flag:'🇧🇾',mod:{phone:.88,cloth:.9}},
 {id:'brest',name:'Брест',cur:'BYN',lat:52.1,lon:23.7,flag:'🇧🇾',mod:{phone:.85,cloth:.84}},
 {id:'warsaw',name:'Варшава',cur:'PLN',lat:52.23,lon:21.01,flag:'🇵🇱',mod:{phone:1,cloth:1.05}},
 {id:'krakow',name:'Краков',cur:'PLN',lat:50.06,lon:19.94,flag:'🇵🇱',mod:{phone:.97,cloth:1}},
 {id:'katowice',name:'Катовице',cur:'PLN',lat:50.26,lon:19.02,flag:'🇵🇱',mod:{phone:.93,cloth:.92}},
 {id:'prague',name:'Прага',cur:'CZK',lat:50.08,lon:14.43,flag:'🇨🇿',mod:{phone:1.03,cloth:1}},
 {id:'berlin',name:'Берлин',cur:'EUR',lat:52.52,lon:13.4,flag:'🇩🇪',mod:{phone:1.12,cloth:1.15}},
 {id:'hamburg',name:'Гамбург',cur:'EUR',lat:53.55,lon:9.99,flag:'🇩🇪',mod:{phone:1.1,cloth:1.1}},
 {id:'nuremberg',name:'Нюрнберг',cur:'EUR',lat:49.45,lon:11.08,flag:'🇩🇪',mod:{phone:1.05,cloth:1}},
 {id:'paris',name:'Париж',cur:'EUR',lat:48.86,lon:2.35,flag:'🇫🇷',mod:{phone:1.15,cloth:1.4}},
 {id:'vilnius',name:'Вильнюс',cur:'EUR',lat:54.69,lon:25.28,flag:'🇱🇹',mod:{phone:.95,cloth:.98}},
 {id:'moscow',name:'Москва',cur:'RUB',lat:55.75,lon:37.62,flag:'🇷🇺',mod:{phone:1,cloth:1.1}},
 {id:'spb',name:'Санкт-Петербург',cur:'RUB',lat:59.93,lon:30.34,flag:'🇷🇺',mod:{phone:.98,cloth:1.05}},
 {id:'stalingrad',name:'Сталинград',cur:'RUB',lat:48.7,lon:44.5,flag:'🇷🇺',mod:{phone:.82,cloth:.8}}
];

/* ---------- PHONES: 85+ моделей ---------- */
const PHONES=[
 // РЕТРО
 {n:'Nokia 3310 (ретро)',base:55,t:1,i:'📟',rar:1.4},
 {n:'Nokia 8800 (раритет)',base:180,t:2,i:'📱',rar:1.5},
 {n:'Nokia N95 (раритет)',base:140,t:2,i:'📱',rar:1.5},
 {n:'Nokia 8110 (банан)',base:75,t:1,i:'📟',rar:1.4},
 {n:'Motorola RAZR V3',base:90,t:1,i:'📱',rar:1.4},
 {n:'Motorola StarTAC',base:200,t:2,i:'📱',rar:1.6},
 {n:'Sony Ericsson W880',base:70,t:1,i:'📱',rar:1.4},
 {n:'Sony Ericsson K750i',base:60,t:1,i:'📱',rar:1.3},
 {n:'Ericsson T28 (раритет)',base:220,t:2,i:'📱',rar:1.6},
 {n:'Ericsson T10 (раритет)',base:260,t:2,i:'📱',rar:1.7},
 {n:'Siemens S65',base:45,t:1,i:'📱',rar:1.3},
 {n:'BlackBerry 8700',base:110,t:2,i:'📱',rar:1.4},
 {n:'BlackBerry Bold 9000',base:150,t:2,i:'📱',rar:1.5},
 {n:'Palm Treo 650',base:130,t:2,i:'📱',rar:1.5},
 // БЮДЖЕТ
 {n:'iPhone 5s',base:50,t:1},{n:'iPhone 6',base:70,t:1},{n:'iPhone 6s',base:85,t:1},
 {n:'iPhone 7',base:95,t:1},{n:'iPhone 8',base:120,t:1},{n:'iPhone SE 2020',base:130,t:1},
 {n:'Redmi Note 10',base:80,t:1},{n:'Redmi Note 11',base:90,t:1},{n:'Redmi 10C',base:65,t:1},
 {n:'Redmi 9A',base:45,t:1},{n:'Poco X3 Pro',base:100,t:1},{n:'Poco M4 Pro',base:95,t:1},
 {n:'Samsung A32',base:110,t:1},{n:'Samsung A52',base:140,t:1},{n:'Samsung A13',base:70,t:1},
 {n:'Samsung A03',base:50,t:1},{n:'Realme 9 Pro',base:110,t:1},{n:'Realme C35',base:60,t:1},
 {n:'Realme 8',base:85,t:1},{n:'Honor 50 Lite',base:90,t:1},{n:'Honor X7',base:75,t:1},
 // СРЕДНИЙ
 {n:'iPhone X',base:170,t:2},{n:'iPhone XR',base:180,t:2},{n:'iPhone XS',base:200,t:2},
 {n:'iPhone 11',base:230,t:2},{n:'iPhone 11 Pro',base:280,t:2},{n:'iPhone SE 2022',base:250,t:2},
 {n:'Pixel 6',base:240,t:2},{n:'Pixel 6a',base:200,t:2},{n:'Pixel 7',base:280,t:2},
 {n:'Pixel 7a',base:260,t:2},{n:'Samsung S20',base:250,t:2},{n:'Samsung S21',base:300,t:2},
 {n:'Samsung S22',base:350,t:2},{n:'Samsung S21 FE',base:280,t:2},{n:'Samsung Note 20',base:320,t:2},
 {n:'OnePlus 9',base:260,t:2},{n:'OnePlus 10 Pro',base:300,t:2},{n:'OnePlus Nord 2',base:180,t:2},
 {n:'Xiaomi 12',base:310,t:2},{n:'Xiaomi 12X',base:250,t:2},{n:'Poco F4',base:220,t:2},
 {n:'Honor 70',base:260,t:2},{n:'Huawei P40',base:280,t:2},
 // ТОП
 {n:'iPhone 12',base:350,t:2},{n:'iPhone 12 Pro',base:420,t:2},{n:'iPhone 12 Pro Max',base:480,t:3},
 {n:'iPhone 13',base:450,t:3},{n:'iPhone 13 Pro',base:550,t:3},{n:'iPhone 13 Pro Max',base:600,t:3},
 {n:'iPhone 14',base:600,t:3},{n:'iPhone 14 Pro',base:680,t:3},{n:'iPhone 14 Pro Max',base:750,t:4},
 {n:'iPhone 15',base:750,t:4},{n:'iPhone 15 Pro',base:880,t:4},{n:'iPhone 15 Pro Max',base:1000,t:4},
 {n:'Galaxy S23',base:550,t:3},{n:'Galaxy S23 Ultra',base:750,t:4},{n:'Galaxy S23+',base:620,t:3},
 {n:'Galaxy S24',base:700,t:4},{n:'Galaxy S24 Ultra',base:950,t:4},
 {n:'Galaxy Z Flip 4',base:550,t:3},{n:'Galaxy Z Fold 5',base:900,t:4},{n:'Galaxy Z Flip 5',base:650,t:3},
 {n:'Xiaomi 13',base:480,t:3},{n:'Xiaomi 13 Pro',base:560,t:3},{n:'Xiaomi 13 Ultra',base:600,t:3},
 {n:'Xiaomi 14 Pro',base:720,t:4},{n:'OnePlus 11',base:500,t:3},
 {n:'Pixel 8',base:580,t:3},{n:'Pixel 8 Pro',base:720,t:4},{n:'Pixel Fold',base:1100,t:4},
 {n:'Huawei Mate 60 Pro',base:700,t:4},{n:'Honor Magic 5 Pro',base:550,t:3}
];

/* ---------- CLOTHES: 80+ позиций ---------- */
const CLOTHES=[
 // БЮДЖЕТ
 {n:'Футболка Nike',base:30,t:1,i:'👕'},{n:'Футболка Adidas',base:30,t:1,i:'👕'},
 {n:'Футболка Puma',base:25,t:1,i:'👕'},{n:'Футболка Reebok',base:25,t:1,i:'👕'},
 {n:'Худи Adidas',base:55,t:1,i:'🧥'},{n:'Худи Puma',base:50,t:1,i:'🧥'},
 {n:'Джинсы Levi’s 501',base:45,t:1,i:'👖'},{n:'Джинсы Wrangler',base:40,t:1,i:'👖'},
 {n:'Джинсы Lee',base:40,t:1,i:'👖'},{n:'Кепка New Era',base:30,t:1,i:'🧢'},
 {n:'Кепка Nike',base:25,t:1,i:'🧢'},{n:'Ремень Levi’s',base:35,t:1,i:'👔'},
 // СРЕДНИЙ
 {n:'Куртка Carhartt',base:110,t:2,i:'🧥'},{n:'Худи Carhartt',base:80,t:2,i:'🧥'},
 {n:'Nuptse The North Face',base:190,t:2,i:'🧥'},{n:'Куртка The North Face',base:160,t:2,i:'🧥'},
 {n:'Кроссовки Nike Dunk',base:150,t:2,i:'👟'},{n:'Кроссовки Nike Air Max 90',base:130,t:2,i:'👟'},
 {n:'Кроссовки Nike Air Force 1',base:120,t:2,i:'👟'},{n:'Кроссовки Adidas Samba',base:110,t:2,i:'👟'},
 {n:'Кроссовки Adidas Gazelle',base:100,t:2,i:'👟'},{n:'Кроссовки New Balance 550',base:140,t:2,i:'👟'},
 {n:'Кроссовки New Balance 990',base:170,t:2,i:'👟'},{n:'Кроссовки Asics Gel-Kayano',base:130,t:2,i:'👟'},
 {n:'Кроссовки Vans Old Skool',base:80,t:2,i:'👟'},{n:'Кроссовки Converse Chuck 70',base:85,t:2,i:'👟'},
 {n:'Очки Ray-Ban Aviator',base:120,t:2,i:'🕶'},{n:'Очки Ray-Ban Wayfarer',base:110,t:2,i:'🕶'},
 {n:'Очки Oakley Holbrook',base:100,t:2,i:'🕶'},
 {n:'Часы Casio G-Shock',base:100,t:2,i:'⌚'},{n:'Часы Casio Vintage',base:60,t:2,i:'⌚'},
 {n:'Часы Seiko 5',base:180,t:2,i:'⌚'},{n:'Часы Timex Weekender',base:50,t:2,i:'⌚'},
 // ПРЕМИУМ
 {n:'Худи Supreme',base:260,t:3,i:'🧥'},{n:'Куртка Stone Island',base:320,t:3,i:'🧥'},
 {n:'Худи Stone Island',base:280,t:3,i:'🧥'},{n:'Футболка Off-White',base:240,t:3,i:'👕'},
 {n:'Ремень Gucci',base:300,t:3,i:'👔'},{n:'Ремень Louis Vuitton',base:320,t:3,i:'👔'},
 {n:'Кроссовки Balenciaga',base:420,t:4,i:'👟'},{n:'Кроссовки Yeezy 350',base:380,t:3,i:'👟'},
 {n:'Кроссовки Jordan 1',base:300,t:3,i:'👟'},{n:'Кроссовки Jordan 4',base:450,t:4,i:'👟'},
 {n:'Кроссовки Off-White x Nike',base:600,t:4,i:'👟'},{n:'Кроссовки Travis Scott',base:700,t:4,i:'👟'},
 {n:'Худи BAPE',base:290,t:3,i:'🧥'},{n:'Куртка Moncler Maya',base:700,t:4,i:'🧥'},
 {n:'Пуховик Moncler',base:700,t:4,i:'🧥'},{n:'Куртка Canada Goose',base:650,t:4,i:'🧥'},
 {n:'Куртка Arc’teryx',base:550,t:4,i:'🧥'},{n:'Куртка Patagonia',base:280,t:3,i:'🧥'},
 {n:'Сумка Louis Vuitton',base:800,t:4,i:'👜'},{n:'Сумка Gucci Marmont',base:750,t:4,i:'👜'},
 {n:'Сумка Prada',base:650,t:4,i:'👜'},{n:'Сумка Chanel Classic',base:1200,t:4,i:'👜'},
 // ЛЮКС
 {n:'Часы Rolex Submariner',base:8000,t:4,i:'⌚',rar:1.2},
 {n:'Часы Omega Speedmaster',base:3500,t:4,i:'⌚',rar:1.15},
 {n:'Часы Cartier Santos',base:4000,t:4,i:'⌚',rar:1.15},
 {n:'Часы Tag Heuer Carrera',base:1800,t:4,i:'⌚',rar:1.1},
 {n:'Очки Cartier',base:600,t:4,i:'🕶'},{n:'Очки Tom Ford',base:250,t:3,i:'🕶'},
 {n:'Куртка Loro Piana',base:2500,t:4,i:'🧥',rar:1.15},
 {n:'Свитер Brunello Cucinelli',base:1800,t:4,i:'🧥',rar:1.15},
 {n:'Кроссовки Gucci Ace',base:600,t:4,i:'👟'},
 {n:'Кроссовки Dior B22',base:900,t:4,i:'👟'},
 {n:'Кроссовки Louis Vuitton',base:1000,t:4,i:'👟'}
];

/* ---------- дефекты ---------- */
const FAULT={
 screen:{n:'Разбит экран',pen:.28,part:.18,i:'📱',fix:'Заменить экран',game:'разборка и посадка дисплея'},
 battery:{n:'Села батарея',pen:.10,part:.06,i:'🔋',fix:'З
