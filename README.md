
<!DOCTYPE html>
<html dir="rtl" lang="ar">
<head>
<meta charset="utf-8">
<link rel="manifest" href="manifest.json">
<meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover">
<title>توافقات الشاشات والبطاريات</title>
<link href="https://fonts.googleapis.com/css2?family=Tajawal:wght@400;600;700;800&display=swap" rel="stylesheet">
<style type="text/css">
:root{
  --dark:#000; --deep:#062f21;
  --accent:#10b981; --accent-l:#34d399; --sky:#0ea5e9;
  --glow:rgba(16,185,129,.6);
  --glass:rgba(5,15,10,.55);
  --glass-border:rgba(16,185,129,.25);
  --text:#f8fafc; --muted:#94a3b8;
  --font:'Tajawal','Segoe UI',Tahoma,sans-serif;
  --spring:cubic-bezier(.34,1.56,.64,1);
}
*{box-sizing:border-box;-webkit-tap-highlight-color:transparent}
html,body{width:100%;max-width:100vw;overflow-x:hidden;margin:0;padding:0}
body{
  font-family:var(--font);color:var(--text);direction:rtl;-webkit-font-smoothing:antialiased;
  background:radial-gradient(circle at 50% 40%,var(--deep) 0%,var(--dark) 100%) fixed;
  min-height:100vh;position:relative;
  padding-bottom:max(60px,env(safe-area-inset-bottom));padding-top:env(safe-area-inset-top);
}
#bg-canvas{position:fixed;inset:0;width:100%;height:100%;z-index:0;pointer-events:none}
.ambient-orbs{position:fixed;inset:0;z-index:0;overflow:hidden;pointer-events:none}
.orb{position:absolute;border-radius:50%;filter:blur(95px);opacity:.45;animation:drift 14s infinite alternate ease-in-out}
.orb-1{width:320px;height:320px;background:rgba(16,185,129,.26);top:-10%;left:-10%}
.orb-2{width:280px;height:280px;background:rgba(14,165,233,.16);bottom:-8%;right:-8%;animation-delay:-5s}
@keyframes drift{to{transform:translate(40px,-50px) scale(1.3)}}

.container{width:100%;max-width:480px;margin:0 auto;padding:20px;position:relative;z-index:10;animation:enter .9s cubic-bezier(.2,.8,.2,1) both}
@keyframes enter{from{opacity:0;transform:translateY(30px)}}

/* ---------- shared press physics ---------- */
.pr{
  --rx:0deg;--ry:0deg;--s:1;--bx:50%;--by:50%;
  position:relative;overflow:hidden;isolation:isolate;
  transform:perspective(700px) rotateX(var(--rx)) rotateY(var(--ry)) scale(var(--s));
  transition:transform .55s var(--spring),background .3s,border-color .3s,box-shadow .3s,color .3s;
  user-select:none;-webkit-user-select:none;touch-action:manipulation;outline:none;
}
.pr::after{ /* hover spotlight */
  content:"";position:absolute;inset:0;z-index:-1;pointer-events:none;opacity:0;transition:opacity .3s;
  background:radial-gradient(150px circle at var(--bx) var(--by),rgba(52,211,153,.26),transparent 70%);
}
.pr:hover::after{opacity:1}
.pr.pressed{--s:.93;transition:transform .12s ease-out,box-shadow .12s}
.pr:focus-visible{box-shadow:0 0 0 3px var(--deep),0 0 0 5px var(--accent-l)}
.ripple{position:absolute;z-index:0;border-radius:50%;pointer-events:none;
  background:radial-gradient(circle,rgba(255,255,255,.5),rgba(52,211,153,.35) 45%,transparent 70%);
  transform:scale(0);animation:rip .75s cubic-bezier(.2,.7,.3,1) forwards}
@keyframes rip{to{transform:scale(1);opacity:0}}
.shock{position:fixed;z-index:100;pointer-events:none;border-radius:50%;border:2px solid var(--accent-l);
  transform:translate(-50%,-50%) scale(0);animation:shock .8s cubic-bezier(.1,.7,.3,1) forwards}
@keyframes shock{to{transform:translate(-50%,-50%) scale(1);opacity:0;border-width:0}}
.spark{position:fixed;z-index:101;pointer-events:none;border-radius:50%}

/* ---------- top tabs ---------- */
.main-nav{
  position:relative;display:flex;gap:6px;margin:10px 0 24px;padding:6px;border-radius:20px;
  background:var(--glass);border:1px solid rgba(255,255,255,.08);
  -webkit-backdrop-filter:blur(12px);backdrop-filter:blur(12px);box-shadow:0 4px 18px rgba(0,0,0,.25);
}
.pill{
  position:absolute;top:6px;bottom:6px;left:0;width:0;border-radius:14px;z-index:0;
  background:rgba(16,185,129,.16);border:1px solid var(--accent);
  box-shadow:0 0 22px rgba(16,185,129,.28),inset 0 0 12px rgba(16,185,129,.14);
  transition:transform .5s var(--spring),width .5s var(--spring);
}
.main-tab{
  flex:1;position:relative;z-index:1;padding:13px 5px;text-align:center;cursor:pointer;
  font:700 15px var(--font);color:var(--muted);border-radius:14px;
  background:transparent;border:1px solid transparent;
}
.main-tab.active-section{color:var(--accent-l);text-shadow:0 0 12px rgba(16,185,129,.45)}
.main-tab::after{border-radius:14px}

/* ---------- brands ---------- */
.brands-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:8px;margin-bottom:24px}
.brand-btn{
  min-height:48px;padding:8px 4px;display:flex;align-items:center;justify-content:center;text-align:center;
  font:700 11px/1.3 var(--font);color:var(--muted);cursor:pointer;
  white-space:normal;word-break:break-word;border-radius:12px;
  background:rgba(255,255,255,.03);border:1px solid rgba(255,255,255,.08);
  -webkit-backdrop-filter:blur(5px);backdrop-filter:blur(5px);
  animation:pop .5s var(--spring) backwards;animation-delay:calc(var(--i,0)*45ms);
}
@keyframes pop{from{opacity:0;transform:scale(.7) translateY(10px)}}
.brand-btn:hover{border-color:rgba(16,185,129,.35);color:var(--text)}
.brand-btn.active{
  background:rgba(16,185,129,.2);color:var(--accent-l);border-color:var(--accent);
  box-shadow:0 0 16px rgba(16,185,129,.3),inset 0 0 10px rgba(16,185,129,.12);
}

/* ---------- search ---------- */
.search{position:relative;margin-bottom:24px}
.search svg.ico{position:absolute;right:18px;top:50%;width:20px;height:20px;margin-top:-10px;stroke:var(--muted);stroke-width:2.2;fill:none;stroke-linecap:round;stroke-linejoin:round;pointer-events:none;transition:stroke .3s,transform .4s var(--spring)}
.search:focus-within svg.ico{stroke:var(--accent-l);transform:scale(1.15) rotate(-8deg)}
.search-box{
  width:100%;padding:18px 52px 18px 48px;border-radius:16px;outline:none;
  border:1px solid rgba(255,255,255,.1);background:var(--glass);color:var(--text);
  font:500 16px var(--font);text-align:right;
  -webkit-backdrop-filter:blur(15px);backdrop-filter:blur(15px);box-shadow:inset 0 2px 10px rgba(0,0,0,.5);
  transition:border-color .3s,background .3s,box-shadow .3s,transform .5s var(--spring);
}
.search-box::placeholder{color:rgba(255,255,255,.4)}
.search-box:focus{
  border-color:var(--accent);background:rgba(16,185,129,.08);transform:scale(1.015);
  box-shadow:0 0 24px rgba(16,185,129,.25),inset 0 2px 10px rgba(0,0,0,.5);
}
.clear{
  position:absolute;left:10px;top:50%;width:34px;height:34px;margin-top:-17px;border-radius:50%;border:0;cursor:pointer;
  background:rgba(255,255,255,.07);color:var(--muted);font:700 20px/1 var(--font);
  display:flex;align-items:center;justify-content:center;
  opacity:0;transform:scale(.4);pointer-events:none;transition:opacity .25s,transform .4s var(--spring),background .2s;
}
.search.has .clear{opacity:1;transform:scale(1);pointer-events:auto}
.clear:active{transform:scale(.8);background:rgba(16,185,129,.3)}

/* ---------- result cards ---------- */
.card{
  margin-bottom:16px;padding:28px 18px 18px;border-radius:18px;cursor:pointer;
  background:var(--glass);border:1px solid var(--glass-border);border-right:4px solid var(--accent);
  box-shadow:0 10px 30px rgba(0,0,0,.4);
  -webkit-backdrop-filter:blur(20px);backdrop-filter:blur(20px);
  animation:cardin .55s cubic-bezier(.2,.8,.2,1) backwards;animation-delay:calc(var(--i,0)*60ms);
}
@keyframes cardin{from{opacity:0;transform:translateY(26px) scale(.97)}}
.card:hover{background:rgba(16,185,129,.1);border-color:rgba(16,185,129,.45)}
.card.pressed{--s:.97;box-shadow:inset 0 0 34px rgba(16,185,129,.3),0 10px 30px rgba(0,0,0,.4)}
.card::before{
  content:"📋 نقرة للنسخ";position:absolute;top:10px;left:15px;z-index:2;
  font-size:11px;font-weight:700;letter-spacing:.5px;color:var(--accent);opacity:.8;
}
.card.copied{animation:flash .7s ease}
@keyframes flash{30%{background:rgba(16,185,129,.35);box-shadow:0 0 36px var(--glow)}}
.d-list{display:flex;flex-wrap:wrap;gap:8px;justify-content:flex-start;margin-top:15px;position:relative;z-index:2}
.tag{
  padding:6px 12px;border-radius:10px;font-size:13px;font-weight:500;color:var(--muted);
  background:rgba(255,255,255,.04);border:1px solid rgba(255,255,255,.08);
  animation:pop .45s var(--spring) backwards;animation-delay:calc(var(--t,0)*22ms + var(--i,0)*60ms);
}
.tag.match{
  background:rgba(16,185,129,.15);color:var(--accent-l);border-color:var(--accent);font-weight:700;
  box-shadow:0 0 12px rgba(16,185,129,.22);
}
.empty{text-align:center;color:var(--muted);font-weight:700;margin-top:20px;animation:cardin .5s backwards}

/* ---------- toast ---------- */
#copy-toast{
  position:fixed;left:50%;bottom:max(40px,env(safe-area-inset-bottom));z-index:30000;
  padding:12px 24px;border-radius:50px;font:800 15px var(--font);color:#000;background:var(--accent);
  box-shadow:0 10px 40px rgba(16,185,129,.5);pointer-events:none;
  opacity:0;transform:translate(-50%,40px) scale(.8);transition:opacity .25s,transform .5s var(--spring);
}
#copy-toast.show{opacity:1;transform:translate(-50%,0) scale(1)}

/* ---------- back link ---------- */
.back{
  display:flex;align-items:center;justify-content:center;gap:10px;margin-top:28px;padding:16px;border-radius:16px;
  text-decoration:none;cursor:pointer;font:700 15px var(--font);color:var(--accent-l);
  background:rgba(16,185,129,.08);border:1px solid rgba(16,185,129,.35);
}
.back:hover{background:rgba(16,185,129,.14);box-shadow:0 0 24px rgba(16,185,129,.25)}
.back svg{width:20px;height:20px;stroke:currentColor;stroke-width:2.4;fill:none;stroke-linecap:round;stroke-linejoin:round;transition:transform .4s var(--spring)}
.back:hover svg{transform:translateX(5px)}

/* ads / update overlays stay hidden as in the original */
#smart-ad-box,#force-update-overlay,#fs-ad-overlay,#inf-upd-overlay,#inf-ad-overlay{
  display:none!important;opacity:0!important;visibility:hidden!important;pointer-events:none!important;
  z-index:-99999!important;height:0!important;width:0!important;overflow:hidden!important;
}
@media (prefers-reduced-motion:reduce){
  *,*::before,*::after{animation-duration:.01ms!important;animation-iteration-count:1!important;transition-duration:.01ms!important}
}
</style>
</head>

<body spellcheck="false">

<canvas id="bg-canvas"></canvas>
<div class="ambient-orbs"><div class="orb orb-1"></div><div class="orb orb-2"></div></div>

<!-- أكواد الإعلانات والتحديث (مخفية برمجياً) -->
<div id="inf-upd-overlay"><div class="inf-card-style"><p id="inf-upd-notes"></p></div></div>
<div id="inf-ad-overlay"><div class="inf-card-style"><p id="inf-ad-txt"></p><button id="inf-cp-btn"></button><span id="inf-ad-ph"></span></div></div>
<div id="smart-ad-box"><div id="smart-ad-content"></div></div>
<div id="copy-toast" role="status" aria-live="polite">تم نسخ البيانات 📋</div>

<div class="container">
  <div class="main-nav" id="mainNav">
    <div class="pill" id="pill"></div>
    <div class="main-tab pr active-section" id="btn-bat" onclick="window.setMode('batteries')">البطاريات</div>
    <div class="main-tab pr" id="btn-scr" onclick="window.setMode('screens')">الشاشات</div>
  </div>

  <div class="brands-grid" id="brandContainer"></div>

  <div class="search" id="searchWrap">
    <svg class="ico" viewBox="0 0 24 24"><circle cx="11" cy="11" r="7"/><line x1="21" y1="21" x2="16.65" y2="16.65"/></svg>
    <input class="search-box" id="searchInput" placeholder="ابحث عن توافق الموديل..." type="text" autocomplete="off">
    <button class="clear" id="clearBtn" type="button" aria-label="مسح البحث">×</button>
  </div>

  <div id="results"></div>

  <a href="ant.html" class="back pr">
    العودة إلى التوافقات
    <svg viewBox="0 0 24 24"><path d="M19 12H5M12 19l-7-7 7-7"/></svg>
  </a>
</div>

<script>
    // 1. مصفوفة الأجهزة الخاصة بك كاملة بدون أي نقصان
    const data = {
        batteries: {
            "Samsung": [
                { devices: ["Model : EB-BT710ABE", "A10s", "A11", "A20s", "A21"] },
                { devices: ["Model : EB-BA315ABY", "A31", "A32 4G", "A22 4G"] },
                { devices: ["Model : EB-BA505ABNU", "A20", "A30", "A30s", "A50", "A50s", "A5 2015"] },
                { devices: ["Model : EB-BA217ABY", "A21s", "A12", "A04s", "A13 4G", "A13 5G", "A02"] },
                { devices: ["Model : HQ-50s", "A03", "A03s", "A02", "A02s", "M02s", "M02", "F02s", "A22 5G", "A14 4G", "A04e"] },
                { devices: ["Model : WT-S-N28", "A05", "A05s"] },
                { devices: ["Model : WT-S-W1", "A04e", "A04", "M04", "A14 5G"] },
                { devices: ["Model : EB-BA336ABY", "A33 5G", "A53 5G"] },
                { devices: ["Model : EB-BA750ABU", "A10", "M10", "A7 ( 2018 )", "A6s", "A8s", "A9 PRO", "A60s"] },
                { devices: ["Model : EB-BM207ABY", "M20", "M20s", "M21", "M21s", "M30", "M30s", "M31", "F41"] },
                { devices: ["Model : BE-BA520ABE", "BE-BJ530ABE", "A5 2017 ( A520 )", "J5 2017 ( J530 )"] },
                { devices: ["Model : EB-BM526ABS", "A23", "M33", "M53 5G"] },
                { devices: ["Model : EB-BA426ABY", "EB-BM325ABN", "M32 4G", "A42 5G", "A32 5G", "A72"] },
                { devices: ["Model : EB-BA546ABY", "A25 5G", "A34 5G", "A35 5G", "A54 5G", "A55 5G"] },
                { devices: ["Model : EB-BG781ABY", "A52 4G", "A52 5G", "A52s 5G", "S20 FE"] },
                { devices: ["Model : BA566ASE", "A36 5G", "A56 5G"] }
            ],
            "Xiaomi": [ 
                { devices: ["Model : BM4P", "POCO X2", "POCO X2 Special Edition", "K30 4G", "K30 5G", "K30i 5G", "K30 5G Racing", "K30 5G Racing edition", "K30 5G Speed Edition", "Redmi K30", "K30i 4G"] },
                { devices: ["Model : BN56", "REDMI 9A", "Redmi 9C", "Redmi 9C NFC", "Redmi 9T", "Redmi 9AT", "POCO M2 PRO", "POCO C31", "POCO C3", "Redmi A1", "Redmi A1 Plus"] },
                { devices: ["Model : BM56", "POCO F3 GT", "K40"] },
                { devices: ["Model : BM4Q", "Redmi K30 Pro", "Poco F2 Pro"] },
                { devices: ["Model : BM4U", "Redmi K30 Ultra", "K30 Supreme Version"] },
                { devices: ["Model : BN54", "Redmi Note 9 5G", "Redmi 10X 4G"] },
                { devices: ["Model : BN53", "Note 9 PRO", "Note 10 Pro 4G"] },
                { devices: ["Model : BN51", "Redmi 8", "Redmi 8A"] },
                { devices: ["Model : BP41", "Redmi K20", "Redmi 9T"] },
                { devices: ["Model : BP40", "Redmi K20 PRO", "Redmi 9T PRO"] },
                { devices: ["Model : BN46", "Redmi 7", "NOTE 6", "NOTE 8", "NOTE 8T"] },
                { devices: ["Model : BN5Q", "Redmi 13C", "POCO C65", "POCO M6 5G"] },
                { devices: ["Model : BN5K", "Redmi 12C", "POCO C55", "Redmi 13C"] },
                { devices: ["Model : BM53", "mi 10T", "mi 10T PRO"] },
                { devices: ["Model : BN5H", "POCO M4 5G", "POCO M5", "Redmi 10E"] },
                { devices: ["Model : BM5J", "Mi 12T", "Mi 12T PRO", "K50 Ultra"] },
                { devices: ["Model : BP4K", "POCO X5 PRO 5G", "NOTE 12T", "NOTE 12 PRO"] },
                { devices: ["Model : BM5G", "POCO X4 GT", "NOTE 11T PRO", "K50i"] },
                { devices: ["Model : BM5V", "Note 13 Pro 5G", "POCO X6 5G"] },
                { devices: ["Model : BM5R", "Redmi 12 5G", "POCO M6 PRO 5G"] },
                { devices: ["Model : BN62", "Redmi Note 9 4G", "Redmi 9 Power", "Redmi 9T", "POCO M3"] },
                { devices: ["Model : BN57", "POCO X3", "POCO X3 PRO", "POCO X3 NFC"] },
                { devices: ["Model : BN5A", "NOTE 10 5G", "NOTE 11 5G", "Redmi 10 5G", "POCO M3 PRO 5G", "POCO F3 PRO 5G"] },
                { devices: ["Model : BM4Y", "POCO F3", "K40", "K40 PRO", "K40 PRO Plus", "K40 Ultra", "11x", "11x PRO"] },
                { devices: ["Model : BM5T", "NOTE 13 PRO 4G", "POCO M6 PRO 4G", "POCO X6 PRO 5G", "mi 13T"] },
                { devices: ["Model : BN5T", "Redmi 13", "POCO M6 4G"] },
                { devices: ["Model : BM5s", "Redmi K60 Ultra", "Redmi 13T PRO"] },
                { devices: ["Model : BN59", "NOTE 10", "NOTE 10s", "NOTE 10 PRO", "PDCO M5s"] },
                { devices: ["Model : BN5F", "Redmi A2", "Redmi A2 Plus", "POCO C51"] },
                { devices: ["Model : BP47", "Redmi 11i 5G", "Redmi Note 11 PRO Plus"] },
                { devices: ["Model : BM57", "POCO X3 GT", "Redmi Note 10 PRO ( china )"] },
                { devices: ["Model : BN5V", "POCO X7", "REDMI NOTE 14 PRO 5G"] },
                { devices: ["Model : BM5W", "POCO F6 PRO 5G", "XIAOMI 14T PRO", "Mi K70 PRO"] },
                { devices: ["Model : BN5X", "Redmi 14C", "POCO C75"] },
                { devices: ["Model : BN5E", "REDMI NOTE 11 PRO 5G", "REDMI NOTE 11 PRO", "REDMI NOTE 12 PRO 4G", "POCO X4 PRO 5G"] }
            ],
            "Infinix/Tecno/itel": [
                { devices: ["Model : BL-49FX", "HOT 8", "HOT 8 PRO", "HOT 8 Lite", "HOT 9", "HOT 9 Lite", "HOT 9 PRO", "NOTE 7 Lite", "HOT 10 Lite", "SMART 5", "SMART 5A", "SMART 6", "SMART 6 HD", "SMART 6 Plus", "NOTE 11s", "NOTE 10", "NOTE 10 PRO", "HOT 11s", "ZERO 5G", "HOT 12 PRO"] },
                { devices: ["Model : BL-51BX", "NOTE 8", "NOTE 8i", "HOT 10"] },
                { devices: ["Model : BL-49KX", "NOTE 11", "NOTE 12 PRO 5G", "NOTE 12", "NOTE 12 Turbo", "Note 12i"] },
                { devices: ["Model : BL-58BX", "HOT 9 Play", "HOT 10 Play", "HOT 11", "HOT 11 Play", "HOT 10i", "HOT 10s", "HOT 10T", "HOT 10s Play"] },
                { devices: ["Model : BL-39LT", "CAMON 12", "POP 3 Plus", "CAMON 12 Air", "SPARK 4", "SPARK 4 Lite"] },
                { devices: ["Model : BL-49JX", "NOTE 10 PRO", "NOTE 11 PRO", "NOTE 11s", "HOT 30", "Zero 5G 2023", "HOT 40 PRO", "HOT 50 PRO"] },
                { devices: ["Model : BL-49NX", "HOT 30i", "SMART 7 HD", "SMART 7", "SMART 7 Plus", "SMART 8 2024", "SMART 8 HD", "SMART 8 Plus", "SMART 8 PRO", "SMART 9", "SMART 9 HD", "Hot 40", "Hot 40i"] },
                { devices: ["Model : BL-49FT", "CAMON 15", "CAMON 15 Air", "SPARK 5", "SPARK 5 Air", "SPARK 5 PRO", "POP 4", "POP 4 Air", "SPARK 6 GO", "SPARK GO 2020", "itel Vision 3"] },
                { devices: ["Model : BL-49NT", "SPARK GO 2023", "POP 7 PRO", "SPARK GO 1", "SPARK GO 2024", "SMART 8"] },
                { devices: ["Model : BL-49OT", "CAMON 20", "CAMON 20 PRO 4G", "CAMON 20 PRO 5G", "CAMON 20 PRO Plus", "SPARK 20", "SPARK 20 PRO 4G", "SPARK 20 PRO 5G", "SPARK 20 PRO Plus"] },
                { devices: ["Model : BL-49LX", "HOT 12", "HOT 20s"] },
                { devices: ["Model : BL-49GT", "CAMON 17", "CAMON 17P", "CAMON 18T", "CAMON 18i", "CAMON 19 Neo", "SPARK 8P", "SPARK 9T", "SPARK 9 PRO"] },
                { devices: ["Model : BL-49NI", "itel 60", "itel A60s", "itel A70", "itel S23 4G", "itel Vision 5"] },
                { devices: ["Model : BL-49ST", "SPARK 10C", "SPARK 10 PRO", "SPARK 10 NFC", "SPARK 10 4G"] },
                { devices: ["Model : BL-5ABX", "HOT 50 4G", "HOT 50i"] },
                { devices: ["Model : BL-49TX", "infinix Note 30 5g", "infinix Note 30i", "infinix Note 30 Pro 5G"] },
                { devices: ["Model : BL-68AT", "Tecno POVA 2", "POVA 3"] },
                { devices: ["Model : BL-49PX", "Zero 30 4G", "ZERO 30 5G", "GT 10 Pro"] }
            ],
            "Honor": [ 
                { devices: ["Model : HB356687ECW", "HUAWEI P30 Lite", "HONOR 7X", "HONOR View 10", "MATE 10 Lite", "Nova 2 Plus"] },
                { devices: ["Model : HB366481ECW", "P9", "P Lite", "P9 Lite 2017", "P10 Lite", "P SMART", "P20 Lite", "Y6 2018", "Y6 Prime 2018", "Y7 2018", "Y7 Prime 2018", "Y7 Pro 2018", "HONOR 8", "P8 Lite 2017", "Nova 2 Lite", "Nova 3E", "HONOR 9 Lite"] },
                { devices: ["Model : HB405979ECW", "Y6 2019", "Y6 PRIME 2019", "Y6 PRO 2019", "Y5 2017", "Y5 PRIME 2018", "HONOR 6A", "HONOR 6C", "Y6 PRO 2017", "Y5 2019", "Y5 PRO", "Nova Lite 2019", "Y6 2017", "Y6s 2019", "HONOR 8A"] },
                { devices: ["Model : HB406689ECW", "Y9 2019", "Y7 2019", "Y7 PRIME", "Y7P 2020", "Y9 2018", "Nova 4"] },
                { devices: ["Model : HB416594EGW", "HONOR 90 LITE 5G", "HONOR X8A 2023", "HONOR X8B 2024", "HONOR X50i", "HONOR 200 Lite"] },
                { devices: ["Model : HB446486ECW", "Y9 PRIME 2019", "Y9s 2019", "Y9s 2020", "HONOR 9X", "HONOR 9X PRO", "P20 Lite", "Nova 5i", "Enjoy 10 Plus", "Y9P"] },
                { devices: ["Model : HB496590EFW", "HONOR X6 2022", "HONOR X7 2022", "HONOR X8 5G", "HONOR Play 20"] },
                { devices: ["Model : HB476489EFW", "HONOR 50", "HONOR 60 SE", "HUAWEI Nova 9"] },
                { devices: ["Model : HB536896EFW", "Enjoy 50", "Maimang 11", "Nova Y70"] },
                { devices: ["Model : HB486686ECW", "Enjoy 20 Plus", "Y9A"] },
                { devices: ["Model : HB526694EHW", "HONOR X9B 2024", "HONOR X50", "HONOR Magic 6 Lite 5G"] },
                { devices: ["Model : HB526488EEW", "P SMART 2021", "Y7a", "Y6P 2020", "Enjoy 20 SE", "HONOR 10X Lite", "Enjoy 20 SE"] },
                { devices: ["Model : HB5066A1EGW", "HONOR X7A 2023", "HONOR Play 40 Plus", "HONOR Play 7T"] },
                { devices: ["Model : HB506492EFW", "HONOR X9A", "HONOR Magic 5 Lite 5G"] },
                { devices: ["Model : HB5470A3EHW", "HUAWEI Nova Y91", "Enjoy 60x"] },
                { devices: ["Model : HB536378EEW", "HUAWEI P40 PRO", "MATE 40", "MATE 40E"] },
                { devices: ["Model : HB516578EFW", "HUAWEI P50", "HUAWEI P50E"] },
                { devices: ["Model : HB546779EGW", "HUAWEI MATE 50 PRO", "MATE 50 RS PORSCHE DESIGN"] },
                { devices: ["Model : HB426493EFW", "HONOR 50 SE", "HUAWEI Nova 9 SE", "HUAWEI Nova 10"] },
                { devices: ["Model : HB456493EGW", "HUAWEI NOVA 10SE", "HUAWEI NOVA 11SE", "HUAWEI NOVA 12SE", "HUAWEI NOVA 11"] },
                { devices: ["Model : HB506593EFW", "HUAWEI Nova 10 PRO", "HUAWEI NOVA 11 PRO", "HUAWEI NOVA 11 ULTRA"] },
                { devices: ["Model : HB496493EGW", "HUAWEI NOVA 11i", "HUAWEI Y90", "HUAWEI Enjoy 50 PRO", "HUAWEI Enjoy 60 PRO", "HUAWEI Enjoy 70 PRO"] },
                { devices: ["Model : HB506781EGW", "HUAWEI MATE 50", "HUAWEI MATE 50E"] },
                { devices: ["Model : HB516586EIW", "HONOR 300 PRO", "HONOR 300 ULTRA"] },
                { devices: ["Model : HB386589ECW", "HUAWEI P10 PLUS", "MATE 20 LITE", "MAIMANG 7", "HONOR VIEW 10", "HONOR V10", "HONOR 8X", "HONOR VIEW 10 LITE", "HONOR PLAY", "HONOR 20 Play", "HONOR 20", "NOVA 5T", "HONOR 9X LITE"] },
                { devices: ["Model : HB476594EGW", "HONOR X7c", "HONOR Play 9T", "HONOR 200 Smart", "HONOR X6b", "HONOR X6a"] }
            ],
            "Huawei": [ 
                { devices: ["Model : HB356687ECW", "HUAWEI P30 Lite", "HONOR 7X", "HONOR View 10", "MATE 10 Lite", "Nova 2 Plus"] },
                { devices: ["Model : HB366481ECW", "P9", "P Lite", "P9 Lite 2017", "P10 Lite", "P SMART", "P20 Lite", "Y6 2018", "Y6 Prime 2018", "Y7 2018", "Y7 Prime 2018", "Y7 Pro 2018", "HONOR 8", "P8 Lite 2017", "Nova 2 Lite", "Nova 3E", "HONOR 9 Lite"] },
                { devices: ["Model : HB405979ECW", "Y6 2019", "Y6 PRIME 2019", "Y6 PRO 2019", "Y5 2017", "Y5 PRIME 2018", "HONOR 6A", "HONOR 6C", "Y6 PRO 2017", "Y5 2019", "Y5 PRO", "Nova Lite 2019", "Y6 2017", "Y6s 2019", "HONOR 8A"] },
                { devices: ["Model : HB406689ECW", "Y9 2019", "Y7 2019", "Y7 PRIME", "Y7P 2020", "Y9 2018", "Nova 4"] },
                { devices: ["Model : HB416594EGW", "HONOR 90 LITE 5G", "HONOR X8A 2023", "HONOR X8B 2024", "HONOR X50i", "HONOR 200 Lite"] },
                { devices: ["Model : HB446486ECW", "Y9 PRIME 2019", "Y9s 2019", "Y9s 2020", "HONOR 9X", "HONOR 9X PRO", "P20 Lite", "Nova 5i", "Enjoy 10 Plus", "Y9P"] },
                { devices: ["Model : HB496590EFW", "HONOR X6 2022", "HONOR X7 2022", "HONOR X8 5G", "HONOR Play 20"] },
                { devices: ["Model : HB476489EFW", "HONOR 50", "HONOR 60 SE", "HUAWEI Nova 9"] },
                { devices: ["Model : HB536896EFW", "Enjoy 50", "Maimang 11", "Nova Y70"] },
                { devices: ["Model : HB486686ECW", "Enjoy 20 Plus", "Y9A"] },
                { devices: ["Model : HB526694EHW", "HONOR X9B 2024", "HONOR X50", "HONOR Magic 6 Lite 5G"] },
                { devices: ["Model : HB526488EEW", "P SMART 2021", "Y7a", "Y6P 2020", "Enjoy 20 SE", "HONOR 10X Lite", "Enjoy 20 SE"] },
                { devices: ["Model : HB5066A1EGW", "HONOR X7A 2023", "HONOR Play 40 Plus", "HONOR Play 7T"] },
                { devices: ["Model : HB506492EFW", "HONOR X9A", "HONOR Magic 5 Lite 5G"] },
                { devices: ["Model : HB5470A3EHW", "HUAWEI Nova Y91", "Enjoy 60x"] },
                { devices: ["Model : HB536378EEW", "HUAWEI P40 PRO", "MATE 40", "MATE 40E"] },
                { devices: ["Model : HB516578EFW", "HUAWEI P50", "HUAWEI P50E"] },
                { devices: ["Model : HB546779EGW", "HUAWEI MATE 50 PRO", "MATE 50 RS PORSCHE DESIGN"] },
                { devices: ["Model : HB426493EFW", "HONOR 50 SE", "HUAWEI Nova 9 SE", "HUAWEI Nova 10"] },
                { devices: ["Model : HB456493EGW", "HUAWEI NOVA 10SE", "HUAWEI NOVA 11SE", "HUAWEI NOVA 12SE", "HUAWEI NOVA 11"] },
                { devices: ["Model : HB506593EFW", "HUAWEI Nova 10 PRO", "HUAWEI NOVA 11 PRO", "HUAWEI NOVA 11 ULTRA"] },
                { devices: ["Model : HB496493EGW", "HUAWEI NOVA 11i", "HUAWEI Y90", "HUAWEI Enjoy 50 PRO", "HUAWEI Enjoy 60 PRO", "HUAWEI Enjoy 70 PRO"] },
                { devices: ["Model : HB506781EGW", "HUAWEI MATE 50", "HUAWEI MATE 50E"] },
                { devices: ["Model : HB516586EIW", "HONOR 300 PRO", "HONOR 300 ULTRA"] },
                { devices: ["Model : HB386589ECW", "HUAWEI P10 PLUS", "MATE 20 LITE", "MAIMANG 7", "HONOR VIEW 10", "HONOR V10", "HONOR 8X", "HONOR VIEW 10 LITE", "HONOR PLAY", "HONOR 20 Play", "HONOR 20", "NOVA 5T", "HONOR 9X LITE"] },
                { devices: ["Model : HB476594EGW", "HONOR X7c", "HONOR Play 9T", "HONOR 200 Smart", "HONOR X6b", "HONOR X6a"] }
            ],
            "Vivo": [ 
                { devices: ["Model : B-O5", "Y3s 2021", "Y11s 2021", "Y12s 2021", "Y20 2021", "Y33 2021", "Y12a", "Y20a", "Y20i", "Y20t", "Y20s", "Y20g", "Y53s 4G"] }
            ],
            "Oppo": [ 
                { devices: ["Model : BLP877", "Realme 8i", "C30", "C31", "C33", "C35 2020", "V20", "V30"] },
                { devices: ["Model : BLP757", "Realme 6", "6i", "6s", "6 PRO"] },
                { devices: ["Model : BLP729", "REALME 5", "REALME 5i", "REALME 5s", "REALME C3", "REALME C11 2020", "REALME C21", "REALME C21y", "REALME C20"] },
                { devices: ["Model : BLP819", "Reno 5 4G", "Reno 5 Lite", "Reno 5Z"] },
                { devices: ["Model : BLP841", "Realme 8", "Q3", "Q3i"] },
                { devices: ["Model : BLP857", "Realme GT Neo", "Q3 PRO"] },
                { devices: ["Model : BLP805", "OPPO A16", "A16s", "A16k", "A32", "A33 2020", "A53", "A53s", "A54 4G", "A54s", "A74 5G", "A93 5G"] },
                { devices: ["Model : BLP797", "OPPO A73 5G", "OPPO A72 5G"] },
                { devices: ["Model : P883", "Realme 9", "Realme 8s 5G", "Realme 8 5G"] },
                { devices: ["Model : BLP809", "REALME GT MASTER", "GT MASTER EDITION", "Realme Q2 PRO"] },
                { devices: ["Model : BLPA51", "Realme GT 6T", "Realme GT 6", "Realme GT Neo 6 SE"] },
                { devices: ["Model : BLPA35", "Realme 12 PRO", "Realme 12 PRO Plus"] },
                { devices: ["Model : BLPA17", "Realme C65", "Realme C67 4G", "Realme 12 5G"] },
                { devices: ["Model : BLP911", "Realme 9i", "Realme 9 PRO"] },
                { devices: ["Model : BLP875", "Realme C55 4G", "Realme Narzo 50 4G", "Realme Narzo 50 5G"] },
                { devices: ["Model : BLP793", "Realme C12", "Realme C15", "Realme C25", "Realme C25s", "Realme Narzo 20", "Realme Narzo 30A"] },
                { devices: ["Model : BLP885", "OPPO A76", "OPPO A96 4G"] },
                { devices: ["Model : BLB21", "Realme C61 4G", "Realme Note 60", "Realme Note 60x"] }
            ],
            "Realme": [ 
                { devices: ["Model : BLP877", "Realme 8i", "C30", "C31", "C33", "C35 2020", "V20", "V30"] },
                { devices: ["Model : BLP757", "Realme 6", "6i", "6s", "6 PRO"] },
                { devices: ["Model : BLP729", "REALME 5", "REALME 5i", "REALME 5s", "REALME C3", "REALME C11 2020", "REALME C21", "REALME C21y", "REALME C20"] },
                { devices: ["Model : BLP819", "Reno 5 4G", "Reno 5 Lite", "Reno 5Z"] },
                { devices: ["Model : BLP841", "Realme 8", "Q3", "Q3i"] },
                { devices: ["Model : BLP857", "Realme GT Neo", "Q3 PRO"] },
                { devices: ["Model : BLP805", "OPPO A16", "A16s", "A16k", "A32", "A33 2020", "A53", "A53s", "A54 4G", "A54s", "A74 5G", "A93 5G"] },
                { devices: ["Model : BLP797", "OPPO A73 5G", "OPPO A72 5G"] },
                { devices: ["Model : P883", "Realme 9", "Realme 8s 5G", "Realme 8 5G"] },
                { devices: ["Model : BLP809", "REALME GT MASTER", "GT MASTER EDITION", "Realme Q2 PRO"] },
                { devices: ["Model : BLPA51", "Realme GT 6T", "Realme GT 6", "Realme GT Neo 6 SE"] },
                { devices: ["Model : BLPA35", "Realme 12 PRO", "Realme 12 PRO Plus"] },
                { devices: ["Model : BLPA17", "Realme C65", "Realme C67 4G", "Realme 12 5G"] },
                { devices: ["Model : BLP911", "Realme 9i", "Realme 9 PRO"] },
                { devices: ["Model : BLP875", "Realme C55 4G", "Realme Narzo 50 4G", "Realme Narzo 50 5G"] },
                { devices: ["Model : BLP793", "Realme C12", "Realme C15", "Realme C25", "Realme C25s", "Realme Narzo 20", "Realme Narzo 30A"] },
                { devices: ["Model : BLP885", "OPPO A76", "OPPO A96 4G"] },
                { devices: ["Model : BLB21", "Realme C61 4G", "Realme Note 60", "Realme Note 60x"] }
            ]
        },
        screens: {
            "Samsung": [ 
                { devices: ["A10E", "A20E"] },
                { devices: ["GALAXY A12 (A125)", "GALAXY A12s (A127)", "GALAXY M12 (M125)", "GALAXY M12s (M127)", "GALAXY A02 (A025)", "GALAXY M02 (M025)", "GALAXY F12 (F125)", "GALAXY A32 5G (A326)", "GALAXY M32 5G (M326)"] },
                { devices: ["A02s", "A03", "A03s", "M02s", "A04E", "M04", "F04"] },
                { devices: ["A5 2020", "A7 2019"] },
                { devices: ["A11", "M11"] },
                { devices: ["A10", "M10"] },
                { devices: ["A13 4G", "M13", "F13", "A23 4G", "M23", "M33"] },
                { devices: ["A51", "M31s"] },
                { devices: ["G530", "G531", "G532"] },
                { devices: ["J4 Plus", "J6 Plus", "J4 Core"] },
                { devices: ["J8", "A6 Plus"] },
                { devices: ["M30", "M30s", "M21", "M21s", "M31", "F41"] },
                { devices: ["A13 5G", "A04s"] },
                { devices: ["A30", "A50", "A50s", "بصمة الاصبع*"] },
                { devices: ["M10s 2019", "A20 2019"] },
                { devices: ["A22 5G", "A22s 5G", "F42 5G"] },
                { devices: ["M52", "M53"] },
                { devices: ["A52", "A52 5G", "A52s"] },
                { devices: ["M51", "A71"] },
                { devices: ["M62", "F62", "With Frame also"] },
                { devices: ["A15 4G", "A15 5G", "M15", "F15"] },
                { devices: ["A16", "M16 5G", "F16 5G", "A26 5G"] },
                { devices: ["A14", "M14 5G", "F14 5G"] },
                { devices: ["A24 4G", "A25 5G", "M34 5G", "F34 5G"] },
                { devices: ["A06 5G", "M06 5G"] },
                { devices: ["A60", "M40"] },
                { devices: ["A56 5G", "A36 5G"] },
                { devices: ["SAMSUNG A35 5G", "SAMSUNG A55 5G"] }
            ],
            "Xiaomi": [ 
                { devices: ["POCO F5 5G", "Redmi NOTE 12 Turbo", "Redmi Note 13 5G"] },
                { devices: ["Note 13 PRO 4G", "Redmi Note 14s", "POCO M6 PRO 4G"] },
                { devices: ["NOTE 13 PRO Plus 5G", "NOTE 14 PRO 5G", "NOTE 14 PRO Plus 5G", "POCO X7 5G"] },
                { devices: ["NOTE 12 4G", "NOTE 12 5G", "POCO X5"] },
                { devices: ["NOTE 12 PRO 5G", "NOTE 12 PRO Plus 5G", "POCO X5 PRO"] },
                { devices: ["NOTE 10 PRO 4G", "NOTE 10 PRO MAX", "NOTE 11 PRO 5G", "NOTE 11 PRO Plus 5G", "NOTE 12 PRO 4G", "POCO X4 PRO 4G", "POCO X4 PRO 5G"] },
                { devices: ["NOTE 10 4G", "NOTE 10s", "POCO M5s"] },
                { devices: ["NOTE 11 4G", "NOTE 11s 4G", "NOTE 12S", "POCO M4 PRO 4G"] },
                { devices: ["NOTE 11 5G", "NOTE 11T", "NOTE 11s", "NOTE 11T 5G", "POCO M4 PRO 5G"] },
                { devices: ["NOTE 10 E", "Redmi 10 5G", "11 PRIME", "NOTE 11R", "POCO M4 5G", "POCO M5 4G"] },
                { devices: ["NOTE 10T 5G", "NOTE 10 5G", "POCO M3 PRO", "NOTE 11se"] },
                { devices: ["NOTE 10 PRO 5G", "POCO X3 GT"] },
                { devices: ["NOTE 9T", "NOTE 9 5G"] },
                { devices: ["NOTE 9", "10X"] },
                { devices: ["Redmi NOTE 9s", "Redmi NOTE 9 PRO 4G", "POCO M2 PRO"] },
                { devices: ["NOTE 7", "NOTE 7s", "NOTE 7 PRO"] },
                { devices: ["POCO X4 GT", "NOTE 11T PRO", "NOTE 11T PRO Plus", "NOTE 12T PRO", "K50i"] },
                { devices: ["Redmi A3", "A3 Plus", "A3X", "POCO C61"] },
                { devices: ["A1", "A1 Plus", "A2", "A2 Plus", "POCO C50", "POCO C51"] },
                { devices: ["Redmi 13C", "Redmi 13R", "POCO C65", "POCO M6 5G"] },
                { devices: ["Redmi 12", "Note 12R", "POCO M6 PRO 5G", "Redmi 13 4G", "Redmi 13 5G"] },
                { devices: ["Redmi 10 4G", "Redmi 10 2022", "Redmi Note 11", "Redmi 10 Prime"] },
                { devices: ["Redmi 10X PRO", "10X 5G"] },
                { devices: ["Redmi 10C", "10 Power", "12C", "11A", "POCO C40", "POCO C55"] },
                { devices: ["Redmi 9A", "Redmi 9C", "Redmi 9AT", "Redmi 9i", "Redmi 10A", "POCO C3", "POCO C31"] },
                { devices: ["Redmi 9", "9 Prime", "POCO M2"] },
                { devices: ["Redmi 8", "8A"] },
                { devices: ["Redmi K70E", "POCO X6 PRO 5G", "POCO F6", "TURBO 3"] },
                { devices: ["Redmi K60", "K60 PRO"] },
                { devices: ["Redmi K50 Gaming", "POCO F4 GT"] },
                { devices: ["Redmi K50", "K50 PRO", "K60E"] },
                { devices: ["POCO F3 GT", "Redmi K40 Gaming"] },
                { devices: ["Redmi K30", "K30i", "POCO F2", "POCO X2", "POCO X2 PRO"] },
                { devices: ["Mi 13 Lite", "Mi 12 Lite NE", "Mi Civi 2"] },
                { devices: ["Mi 12T", "12T PRO"] },
                { devices: ["Xiaomi 11T", "Xiaomi 11T PRO"] },
                { devices: ["Mi 11 Lite 4G", "Mi 11 Lite 5G", "Mi 11 Lite NE 5G"] },
                { devices: ["Mi CC9 PRO", "NOTE 10", "NOTE 10 Lite"] },
                { devices: ["Mi 10T", "Mi 10T PRO 5G", "Redmi K30s"] },
                { devices: ["Mi 10", "Mi 10 PRO"] },
                { devices: ["Mi 9T", "9T PRO", "Redmi K20", "K20 PRO"] },
                { devices: ["Mi 9 Lite", "CC9"] },
                { devices: ["POCO M3", "Redmi 9T", "NOTE 9 4G", "9 Power"] },
                { devices: ["POCO X3", "POCO X3 PRO", "POCO X3 NFC", "POCO X3 PRO NFC", "Redmi NOTE 9 PRO 5G", "Mi 10T Lite"] },
                { devices: ["POCO F3", "F3 PRO", "POCO F4", "Mi 11i", "11x", "Redmi K40", "K40s", "K40 PRO", "K40 PRO Plus", "BlackShark 4", "4 PRO", "4s", "4s PRO", "BlackShark 5", "5 RS"] },
                { devices: ["Redmi K30 PRO", "K30 PRO Zoom", "POCO F2 PRO"] },
                { devices: ["Redmi 6 PRO", "Mi A2 Lite"] },
                { devices: ["Redmi 6", "6A"] },
                { devices: ["Redmi NOTE 5", "NOTE 5 PRO"] },
                { devices: ["Mi 6x", "A2"] },
                { devices: ["Mi 5x", "A1"] },
                { devices: ["BlackShark 2", "2 PRO"] },
                { devices: ["mi 12", "12s", "12x"] },
                { devices: ["POCO C75", "POCO M7 5G", "Redmi 14C 4G", "Redmi 14R 5G", "Redmi A3 PRO", "Redmi A4 5G"] },
                { devices: ["POCO C71 4G", "Redmi A5 4G", "Redmi A5 5G"] },
                { devices: ["xiaomi K70", "xiaomi K70 Ultra", "Mi 14T", "Mi 14T PRO"] },
                { devices: ["Redmi NOTE 13 4G", "Redmi NOTE 14 4G", "Redmi NOTE 14 5G", "POCO M7 PRO"] },
                { devices: ["POCO X6 5G", "Note 13 PRO 5G"] },
                { devices: ["Mi 13T", "Mi 13T PRO", "Mi K60 Ultra"] },
                { devices: ["POCO X7 PRO", "Redmi Turbo 4"] },
                { devices: ["Redmi 15C 4G", "Redmi 15C 5G", "POCO C85 4G"] },
                { devices: ["Xiaomi K50 Ultra", "Xiaomi 12T", "Xiaomi 12T PRO"] },
                { devices: ["Poco F7 5G", "Redmi Turbo 4 Pro 5G", "Xiaomi 15T 5G"] },
                { devices: ["POCO F6 PRO 5G", "Redmi K70", "Redmi K70 PRO"] },
                { devices: ["POCO F7 PRO", "POCO F7 Ultra", "Redmi K80 5G", "Redmi K80 PRO 5G"] }
            ],
            "Infinix/Tecno/itel": [ 
                { devices: ["SPARK 9 PRO", "HOT 11", "SPARK 8T", "SPARK 8P", "SPARK 8 Plus", "itel Vision 5 Plus", "S18 PRO"] },
                { devices: ["SPARK 7", "SMART 5 PRO", "HOT 10L", "SPARK 7T", "POP 5P", "itel P37"] },
                { devices: ["CAMON 20", "CAMON 20 PRO 4G", "CAMON 20 PRO 5G", "NOTE 30 VIP", "NOTE 30 PRO", "GT 10 PRO", "GT 10 PRO Plus", "CAMON 20 PRIMER"] },
                { devices: ["CAMON 19 ( Mondrian )", "CAMON 19 PRO"] },
                { devices: ["CAMON 19", "CAMON 19 Neo", "CAMON 18", "CAMON 18P", "CAMON 18T", "SPARK 8 PRO", "HOT 11s", "POVA Neo 5G", "HOT 20s", "HOT 20 PRO", "ZERO 5G 2023", "CAMON 17P", "CAMON 17 PREMIER"] },
                { devices: ["CAMON 15", "CAMON 15 Air", "HOT 9", "HOT 9 PRO", "SPARK 5", "SPARK 5 PRO", "Note 7 Lite", "S5", "S5 Lite"] },
                { devices: ["CAMON 12 Air", "S5", "S5 Lite"] },
                { devices: ["CAMON 11s", "SMART 3 Plus", "S4"] },
                { devices: ["CAMON 11", "CAMON 11 PRO"] },
                { devices: ["POVA 4 PRO", "ZERO 20"] },
                { devices: ["SPARK 8", "itel A49", "itel A58", "itel A58 PRO", "itel S17"] },
                { devices: ["SPARK 4 Air", "SPARK GO 2019"] },
                { devices: ["CAMON 17", "CAMON 18i", "SPARK 7 PRO", "Vision 2"] },
                { devices: ["HOT 12", "HOT 12 Play", "HOT 12 Play NFC", "Tecno POVA NEO 2", "Tecno POVA NEO 3", "Tecno POVA 4", "NOTE 12i", "HOT 20", "HOT 20 Play", "HOT 30 Play", "itel P40 Plus"] },
                { devices: ["HOT 12i", "HOT 20i", "SMART 6 HD", "Condor Nova 60"] },
                { devices: ["CAMON 16", "SPARK 6 2020", "POVA", "NOTE 8i", "Note 10L", "HOT 10"] },
                { devices: ["HOT 10 Play", "HOT 11 Play", "POVA Neo", "itel P37 PRO", "Vision 2 Plus"] },
                { devices: ["HOT 10s", "HOT 10T", "SMART 6 Plus", "itel P38 PRO", "SPARK 7P", "Vision 3"] },
                { devices: ["HOT 8", "HOT 8 Lite", "HOT 8 PRO", "CAMON 12", "SPARK 4"] },
                { devices: ["NOTE 11", "NOTE 12 4G", "NOTE 12 5G", "NOTE 12i 2022", "NOTE 12 PRO", "NOTE 12 PRO 5G", "NOTE 12 TURBO", "NOTE 30i", "TCL 30 Plus"] },
                { devices: ["ZERO 6", "ZERO 6 PRO"] },
                { devices: ["NOTE 10", "NOTE 11s", "NOTE 11 PRO", "NOTE 11i", "POVA 2", "POVA 3", "POVA 5G"] },
                { devices: ["itel S15", "S15 PRO"] },
                { devices: ["itel A16", "A33"] },
                { devices: ["itel A15", "F1"] },
                { devices: ["SPARK GO 2023", "POP 7", "POP 7 PRO 2023", "SMART 7 HD", "SMART 7", "SPARK 10", "SPARK 10C", "itel A50", "itel A50s", "itel A60", "itel A90", "itel A60s", "itel A70", "itel A05s", "itel P40", "Hot 30i", "SMART 7 Plus", "itel S23", "itel P55 5G", "itel POWER 55", "ZTE Blade A34 4G", "ZTE Blade A54 4G"] },
                { devices: ["SMART 8", "SMART 8 HD", "SMART 8 PRO", "SMART 8 Plus", "HOT 40i", "SPARK GO 2024", "SPARK 20", "SPARK 20C", "POP 8", "itel P55 Plus", "itel P55", "itel P55T", "POWER 50", "itel A70s", "itel S24", "itel RS4", "ZTE Blade A75 4G", "ZTE Blade V60 Smart", "ZTE V60 Vita", "ZTE Axon 60 Lite"] },
                { devices: ["CAMON 18 PREMIER", "ZERO X", "ZERO X PRO"] },
                { devices: ["HOT 10 Lite", "SMART 5", "SMART 5A", "Vision 2s", "itel S16", "P36 PRO Lite", "SMART 6", "itel Vision 1 Plus", "SPARK Go 2020", "Spark 6 Go", "SPARK GO 2021", "itel Vision 1 PRO"] },
                { devices: ["SPARK 9", "SPARK 9T", "SPARK 8C", "itel Vision 3", "itel S18"] },
                { devices: ["ZERO 8", "ZERO 8i", "CAMON 16 PREMIER"] },
                { devices: ["SPARK GO 2022", "POP 5 PRO", "POP 5 Lite", "SMART 6"] },
                { devices: ["SPARK 5 Air", "SPARK 6 Air", "POUVOIR 4", "POUVOIR 4 PRO", "POWER 2"] },
                { devices: ["SMART 4", "SMART 4C", "SPARK 4 Lite", "POP 3 Plus", "SPARK GO Plus"] },
                { devices: ["S5 PRO", "CAMON 15 PRIMER", "CAMON 15 PRO"] },
                { devices: ["SMART HD 2021", "itel P36 Play", "Vision 1"] },
                { devices: ["SPARK GO 1", "SPARK GO 1S", "POP 9 5G", "SPARK 30 5G", "SPARK 30C", "HOT 50 5G", "HOT 50i", "Note 50s 5G", "SMART 9", "SMART 9 HD", "itel P65", "itel P65 Plus", "itel P67", "itel A80", "itel A95 5G", "itel POWER 70", "POVA 6 Neo 5G", "ZTE Blade V70", "ZTE V70 Vita", "ZTE V70 Design", "ZTE nubia Music 2", "ZTE nubia Focus 2", "ZTE AXON 70 Lite"] },
                { devices: ["NOTE 30", "HOT 30", "SPARK 10 PRO", "POVA 5", "POVA 5 PRO 5G", "HOT 40X 5G", "HOT 40", "HOT 40 PRO", "SPARK 20 PRO", "POVA 6 Neo 4G", "Note 40X 5G", "Benco S1 PRO"] },
                { devices: ["HOT 9 Play", "SMART 4 Plus"] },
                { devices: ["ZERO 30 4G", "ZERO 30 5G", "ZERO 30 PRO", "itel S23 Plus"] },
                { devices: ["Infinix Note 40s", "Infinix Note 40 PRO", "Infinix NOTE 40 PRO Plus", "SPARK 20s Plus", "SPARK 20 PRO Plus", "itel S25 Ultra", "Zero 40 Ultra", "HOT 50 PRO Plus 4G", "Note 50s 5G", "CAMON 30s", "CAMON 30s PRO", "CAMON 40 PRO 5G"] },
                { devices: ["CAMON 17 PRO", "ZERO X Neo"] },
                { devices: ["POP 6 PRO", "HOT 12 PRO"] },
                { devices: ["CAMON 30", "CAMON 30 5G", "NOTE 40 5G", "POVA 6", "POVA 6 PRO 5G"] },
                { devices: ["GT 20 PRO", "NOTE 40", "CAMON 30 PRO 5G", "CAMON 40 4G", "NOTE 50 4G", "NOTE 50 PRO 4G", "NOTE 50 PRO Plus 5G"] },
                { devices: ["HOT 50 PRO 4G", "SPARK 30 PRO", "itel S25"] },
                { devices: ["Note 12 5G", "Note 30i", "Note 12 2023", "Note 12i 2022", "Note 12 PRO 5G", "Note 12", "Note 20 PRO", "Note 11", "Note 12"] },
                { devices: ["HOT 50 4G", "SPARK 30 4G", "POVA 7 5G"] },
                { devices: ["Infinix Zero 40 5G", "Infinix Note 40s 4G", "Infinix Note 40 PRO 4G", "CAMON 40 PRO 4G", "CAMON 30s"] },
                { devices: ["SMART 10", "SMART 10 HD", "SMART 10 Plus", "SMART 10 PRO", "POP 10", "POP 10 PRO", "HOT 60 5G", "HOT 60i", "SPARK 40", "SPARK 40C", "SPARK 40T", "SPARK GO 2"] },
                { devices: ["Infinix GT 30 PRO", "SPARK 40 PRO", "HOT 60 PRO", "POVA 7 PRO"] },
                { devices: ["ZTE A36", "ZTE A56"] },
                { devices: ["Hot 60 PRO Plus", "Spark 40 PRO Plus"] },
                { devices: ["ZTE Blade V30", "ZTE Blade V40"] },
                { devices: ["ZTE V50 Design 4G", "ZTE Axon 50 Lite"] },
                { devices: ["ZTE Blade A73 4G", "ZTE V50 Smart"] },
                { devices: ["ZTE V40 Design 4G", "ZTE V50 Design 5G", "ZTE V41 Vita 5G"] },
                { devices: ["ZTE Blade V60", "ZTE Nubia V60"] },
                { devices: ["ZTE Blade A35 4G", "ZTE Blade A55 4G"] },
                { devices: ["ZTE Blade A75 5G", "ZTE Nubia Music"] },
                { devices: ["ZTE Red Magic 6 5G", "ZTE Red Magic 6 PRO 5G"] },
                { devices: ["ZTE Red Magic 7 PRO 5G", "ZTE Red Magic 7s PRO"] },
                { devices: ["ZTE Red Magic 7 5G", "ZTE Red Magic 7s 5G"] },
                { devices: ["ZTE Red Magic 6s 5G", "ZTE Red Magic 6s PRO"] },
                { devices: ["itel A06", "itel A50C"] }
            ],
            "Honor": [ 
                { devices: ["HONOR 10 Lite", "20 Lite", "20i", "10i", "P SMART 2019", "P SMART 2020"] },
                { devices: ["HONOR 8X", "View 10 Lite", "9X Lite"] },
                { devices: ["HONOR X5C 4G", "HONOR X5C plus 4G"] },
                { devices: ["HONOR 20", "20 PRO", "20S", "Nova 5T"] },
                { devices: ["HONOR 50 Lite", "HONOR X20", "Nova 8i"] },
                { devices: ["HONOR 30 Lite", "Enjoy Z", "Enjoy 20 PRO"] },
                { devices: ["HONOR 30s", "Nova 7 SE", "P40 Lite 5G"] },
                { devices: ["HONOR 9i", "HONOR 9N"] },
                { devices: ["HONOR 8 PRO", "V9"] },
                { devices: ["HONOR 8 Lite", "Nova Lite"] },
                { devices: ["HONOR MAGIC 5 Lite", "X40", "X9A 2023"] },
                { devices: ["HONOR X40 GT", "HONOR X9 2022", "HONOR X30 5G", "MAGIC 4 Lite"] },
                { devices: ["HONOR X8 2022", "X30i", "X40i", "Play 6T PRO 4G", "Play 7T PRO"] },
                { devices: ["HONOR X8B", "HONOR X8C 4G", "X50i Plus", "HONOR X60i 5G", "HONOR 200 Lite", "HONOR Play 8T PRO", "HONOR 9T PRO"] },
                { devices: ["HONOR X8A", "HONOR 90 Lite", "HONOR X50i"] },
                { devices: ["HONOR X7 2022", "Play 6T", "Play 30 Plus"] },
                { devices: ["HONOR X6A 2023", "HONOR X5 Plus", "HONOR X5B", "HONOR X5B Plus", "HONOR Play 40", "HONOR Play 40C", "HONOR Play 40S 5G"] },
                { devices: ["HONOR X10", "X10 PRO", "Y9A", "Enjoy 20 Plus"] },
                { devices: ["HONOR V10", "View 10"] },
                { devices: ["HONOR X8 5G", "X8A 5G", "70 Lite", "Play 30", "X6 2022", "X6s"] },
                { devices: ["HONOR Play 3", "P40 Lite E", "Y7P 2020", "9C", "Play 4T", "Enjoy 10"] },
                { devices: ["HONOR Y6-2 ( Y6 II )", "5A"] },
                { devices: ["Y9 PRIME 2019", "P SMART Z", "Y9s 2019 ( الحجم )*"] },
                { devices: ["HUAWEI Y9s 2019", "HONOR 9X 2019", "HONOR 9X PRO", "P SMART PRO 2019"] },
                { devices: ["Y9 2019", "9P", "Enjoy 9 Plus", "Y8s"] },
                { devices: ["HUAWEI 7s", "P SMART", "P SMART 2018"] },
                { devices: ["P30 Lite", "Nova 4e"] },
                { devices: ["P20 Lite", "Nova 3e"] },
                { devices: ["Y6 PRO 2019", "Y6 2019", "Y6 PRIME 2019", "Y6s 2019", "HONOR 8A"] },
                { devices: ["MATE 40 Lite", "Play 4", "Maimang 9"] },
                { devices: ["MATE 30 Lite", "Nova 5i PRO"] },
                { devices: ["MATE 10 Lite", "Nova 2i", "Maimang 6"] },
                { devices: ["MATE 9 Lite", "HONOR 6X", "GR5 2017"] },
                { devices: ["HUAWEI P60", "HUAWEI P60 PRO"] },
                { devices: ["P10 selfie", "Nova 2 Plus"] },
                { devices: ["P9 Lite SMART", "6C", "6s"] },
                { devices: ["P9 Lite Mini", "Y6 PRO 2017", "Enjoy 7"] },
                { devices: ["P8 Lite 2017", "P9 Lite 2017", "HONOR 8 Lite", "Nova Lite", "HUAWEI GR3 2017"] },
                { devices: ["HUAWEI P SMART 2021", "Y7A", "X10 Lite", "Enjoy 20se"] },
                { devices: ["NOVA Y91", "Enjoy 60X"] },
                { devices: ["Nova Y90", "Enjoy 50 PRO"] },
                { devices: ["Nova Y70", "Y70 Plus", "Y71", "Enjoy 50", "Enjoy 60", "Enjoy 60s", "Maimang 11"] },
                { devices: ["Nova Y60", "Enjoy 20", "Play 5t"] },
                { devices: ["Nova 6", "V30"] },
                { devices: ["Nova 9 SE", "HONOR 50 SE", "Nova 11i"] },
                { devices: ["Nova 8 PRO", "V40"] },
                { devices: ["Nova 7", "HONOR 30"] },
                { devices: ["Nova 5", "Nova 5 PRO"] },
                { devices: ["Nova 5i", "P20 Lite 2019", "Nova 6 SE", "P40 Lite", "Nova 7i"] },
                { devices: ["Nova 4", "View 20"] },
                { devices: ["Nova 3i", "Nova 3", "Mate 20 Lite", "P SMART plus 2018"] },
                { devices: ["Y8P 2020", "Y8P", "Play 4T PRO", "HONOR 30i", "Enjoy 10s"] },
                { devices: ["Y6P 2020", "9A", "Enjoy 10E"] },
                { devices: ["Y5P 2020", "HONOR 9S"] },
                { devices: ["Y9 2018", "Enjoy 8 Plus"] },
                { devices: ["Y7 Prime 2019", "Y7 2019", "Y7 PRO 2019", "Enjoy 9"] },
                { devices: ["Y7 Prime 2018", "Y7 2018", "Nova 2 Lite", "HONOR 7C", "Enjoy 8"] },
                { devices: ["Y7 Prime", "Nova Lite Plus", "Y7 2017", "Enjoy 7 Plus"] },
                { devices: ["Y6 2018", "HONOR 7A"] },
                { devices: ["Y6 2017", "Y6 2017", "Y5-3 ( Y5 III )", "HONOR 6 Play"] },
                { devices: ["Y5 2019", "HONOR 8s", "Play 8"] },
                { devices: ["Y5 Prime 2018", "Y5 2018", "HONOR 7s", "Play 7"] },
                { devices: ["HONOR X9B 2024", "HONOR X50", "HONOR X50 PRO", "HONOR X50 GT", "MAGIC 6 Lite"] },
                { devices: ["HONOR 50", "NOVA 9"] },
                { devices: ["Nova 10 se", "Nova 11 se", "Nova 12 se"] },
                { devices: ["Nova 12 PRO", "Nova 12 Ultra"] },
                { devices: ["Nova 10 PRO", "Nova 11 PRO"] },
                { devices: ["HONOR X7B", "HONOR Play 8T", "HONOR Play 50 Plus", "HONOR 90 SMART", "HONOR 200 SMART"] },
                { devices: ["HONOR X7A 2023", "HONOR Play 40 Plus", "HONOR Play 7t"] },
                { devices: ["Play 50", "Play 50M", "X6B 2024"] },
                { devices: ["HONOR X9C", "HONOR X60 PRO", "HONOR Magic 70 Lite", "HONOR 300 GT"] },
                { devices: ["HONOR X7C", "HONOR Play 9t", "HONOR Play 60 Plus"] },
                { devices: ["HUAWEI Nova Y61", "Enjoy 50z", "Huawei Maimang A20"] },
                { devices: ["HONOR Nova 12s", "HONOR Nova 12 Vitality", "HONOR Nova 11"] },
                { devices: ["HONOR X9C SMART", "HONOR X60"] },
                { devices: ["HONOR PLAY 60", "HONOR X6C", "CW 60m"] },
                { devices: ["HONOR 50 PRO", "HONOR Nova 9 PRO"] },
                { devices: ["HUAWEI MATE 40 PRO", "HUAWEI MATE 40 PRO Plus", "HUAWEI MATE 40 RS"] },
                { devices: ["HUAWEI NOVA 10SE", "HUAWEI NOVA 11SE", "HUAWEI NOVA 12SE"] },
                { devices: ["HUAWEI NOVA 9SE", "HUAWEI NOVA 11i"] },
                { devices: ["HUAWEI NOVA 12i", "HUAWEI Enjoy 50 PRO", "HUAWEI Enjoy 70 PRO"] },
                { devices: ["HUAWEI NOVA 12", "HUAWEI NOVA 13"] },
                { devices: ["HUAWEI NOVA 12 PRO", "HUAWEI NOVA 13 PRO"] },
                { devices: ["Honor X7D 4G", "Honor 400 Smart", "Honor Play 10C 5G", "HONOR Play 70 Plus"] },
                { devices: ["HONOR 400 Lite", "HONOR X70i 5G"] },
                { devices: ["HONOR X9D", "HONOR X70"] },
                { devices: ["HUAWEI MatePad T10", "HONOR Pad X8 Lite", "HONOR Pad X6"] },
                { devices: ["HONOR X9D", "HONOR Magic 8 Lite"] }
            ],
            "Huawei": [ 
                { devices: ["HONOR 10 Lite", "20 Lite", "20i", "10i", "P SMART 2019", "P SMART 2020"] },
                { devices: ["HONOR 8X", "View 10 Lite", "9X Lite"] },
                { devices: ["HONOR X5C 4G", "HONOR X5C plus 4G"] },
                { devices: ["HONOR 20", "20 PRO", "20S", "Nova 5T"] },
                { devices: ["HONOR 50 Lite", "HONOR X20", "Nova 8i"] },
                { devices: ["HONOR 30 Lite", "Enjoy Z", "Enjoy 20 PRO"] },
                { devices: ["HONOR 30s", "Nova 7 SE", "P40 Lite 5G"] },
                { devices: ["HONOR 9i", "HONOR 9N"] },
                { devices: ["HONOR 8 PRO", "V9"] },
                { devices: ["HONOR 8 Lite", "Nova Lite"] },
                { devices: ["HONOR MAGIC 5 Lite", "X40", "X9A 2023"] },
                { devices: ["HONOR X40 GT", "HONOR X9 2022", "HONOR X30 5G", "MAGIC 4 Lite"] },
                { devices: ["HONOR X8 2022", "X30i", "X40i", "Play 6T PRO 4G", "Play 7T PRO"] },
                { devices: ["HONOR X8B", "HONOR X8C 4G", "X50i Plus", "HONOR X60i 5G", "HONOR 200 Lite", "HONOR Play 8T PRO", "HONOR 9T PRO"] },
                { devices: ["HONOR X8A", "HONOR 90 Lite", "HONOR X50i"] },
                { devices: ["HONOR X7 2022", "Play 6T", "Play 30 Plus"] },
                { devices: ["HONOR X6A 2023", "HONOR X5 Plus", "HONOR X5B", "HONOR X5B Plus", "HONOR Play 40", "HONOR Play 40C", "HONOR Play 40S 5G"] },
                { devices: ["HONOR X10", "X10 PRO", "Y9A", "Enjoy 20 Plus"] },
                { devices: ["HONOR V10", "View 10"] },
                { devices: ["HONOR X8 5G", "X8A 5G", "70 Lite", "Play 30", "X6 2022", "X6s"] },
                { devices: ["HONOR Play 3", "P40 Lite E", "Y7P 2020", "9C", "Play 4T", "Enjoy 10"] },
                { devices: ["HONOR Y6-2 ( Y6 II )", "5A"] },
                { devices: ["Y9 PRIME 2019", "P SMART Z", "Y9s 2019 ( الحجم )*"] },
                { devices: ["HUAWEI Y9s 2019", "HONOR 9X 2019", "HONOR 9X PRO", "P SMART PRO 2019"] },
                { devices: ["Y9 2019", "9P", "Enjoy 9 Plus", "Y8s"] },
                { devices: ["HUAWEI 7s", "P SMART", "P SMART 2018"] },
                { devices: ["P30 Lite", "Nova 4e"] },
                { devices: ["P20 Lite", "Nova 3e"] },
                { devices: ["Y6 PRO 2019", "Y6 2019", "Y6 PRIME 2019", "Y6s 2019", "HONOR 8A"] },
                { devices: ["MATE 40 Lite", "Play 4", "Maimang 9"] },
                { devices: ["MATE 30 Lite", "Nova 5i PRO"] },
                { devices: ["MATE 10 Lite", "Nova 2i", "Maimang 6"] },
                { devices: ["MATE 9 Lite", "HONOR 6X", "GR5 2017"] },
                { devices: ["HUAWEI P60", "HUAWEI P60 PRO"] },
                { devices: ["P10 selfie", "Nova 2 Plus"] },
                { devices: ["P9 Lite SMART", "6C", "6s"] },
                { devices: ["P9 Lite Mini", "Y6 PRO 2017", "Enjoy 7"] },
                { devices: ["P8 Lite 2017", "P9 Lite 2017", "HONOR 8 Lite", "Nova Lite", "HUAWEI GR3 2017"] },
                { devices: ["HUAWEI P SMART 2021", "Y7A", "X10 Lite", "Enjoy 20se"] },
                { devices: ["NOVA Y91", "Enjoy 60X"] },
                { devices: ["Nova Y90", "Enjoy 50 PRO"] },
                { devices: ["Nova Y70", "Y70 Plus", "Y71", "Enjoy 50", "Enjoy 60", "Enjoy 60s", "Maimang 11"] },
                { devices: ["Nova Y60", "Enjoy 20", "Play 5t"] },
                { devices: ["Nova 6", "V30"] },
                { devices: ["Nova 9 SE", "HONOR 50 SE", "Nova 11i"] },
                { devices: ["Nova 8 PRO", "V40"] },
                { devices: ["Nova 7", "HONOR 30"] },
                { devices: ["Nova 5", "Nova 5 PRO"] },
                { devices: ["Nova 5i", "P20 Lite 2019", "Nova 6 SE", "P40 Lite", "Nova 7i"] },
                { devices: ["Nova 4", "View 20"] },
                { devices: ["Nova 3i", "Nova 3", "Mate 20 Lite", "P SMART plus 2018"] },
                { devices: ["Y8P 2020", "Y8P", "Play 4T PRO", "HONOR 30i", "Enjoy 10s"] },
                { devices: ["Y6P 2020", "9A", "Enjoy 10E"] },
                { devices: ["Y5P 2020", "HONOR 9S"] },
                { devices: ["Y9 2018", "Enjoy 8 Plus"] },
                { devices: ["Y7 Prime 2019", "Y7 2019", "Y7 PRO 2019", "Enjoy 9"] },
                { devices: ["Y7 Prime 2018", "Y7 2018", "Nova 2 Lite", "HONOR 7C", "Enjoy 8"] },
                { devices: ["Y7 Prime", "Nova Lite Plus", "Y7 2017", "Enjoy 7 Plus"] },
                { devices: ["Y6 2018", "HONOR 7A"] },
                { devices: ["Y6 2017", "Y6 2017", "Y5-3 ( Y5 III )", "HONOR 6 Play"] },
                { devices: ["Y5 2019", "HONOR 8s", "Play 8"] },
                { devices: ["Y5 Prime 2018", "Y5 2018", "HONOR 7s", "Play 7"] },
                { devices: ["HONOR X9B 2024", "HONOR X50", "HONOR X50 PRO", "HONOR X50 GT", "MAGIC 6 Lite"] },
                { devices: ["HONOR 50", "NOVA 9"] },
                { devices: ["Nova 10 se", "Nova 11 se", "Nova 12 se"] },
                { devices: ["Nova 12 PRO", "Nova 12 Ultra"] },
                { devices: ["Nova 10 PRO", "Nova 11 PRO"] },
                { devices: ["HONOR X7B", "HONOR Play 8T", "HONOR Play 50 Plus", "HONOR 90 SMART", "HONOR 200 SMART"] },
                { devices: ["HONOR X7A 2023", "HONOR Play 40 Plus", "HONOR Play 7t"] },
                { devices: ["Play 50", "Play 50M", "X6B 2024"] },
                { devices: ["HONOR X9C", "HONOR X60 PRO", "HONOR Magic 70 Lite", "HONOR 300 GT"] },
                { devices: ["HONOR X7C", "HONOR Play 9t", "HONOR Play 60 Plus"] },
                { devices: ["HUAWEI Nova Y61", "Enjoy 50z", "Huawei Maimang A20"] },
                { devices: ["HONOR Nova 12s", "HONOR Nova 12 Vitality", "HONOR Nova 11"] },
                { devices: ["HONOR X9C SMART", "HONOR X60"] },
                { devices: ["HONOR PLAY 60", "HONOR X6C", "CW 60m"] },
                { devices: ["HONOR 50 PRO", "HONOR Nova 9 PRO"] },
                { devices: ["HUAWEI MATE 40 PRO", "HUAWEI MATE 40 PRO Plus", "HUAWEI MATE 40 RS"] },
                { devices: ["HUAWEI NOVA 10SE", "HUAWEI NOVA 11SE", "HUAWEI NOVA 12SE"] },
                { devices: ["HUAWEI NOVA 9SE", "HUAWEI NOVA 11i"] },
                { devices: ["HUAWEI NOVA 12i", "HUAWEI Enjoy 50 PRO", "HUAWEI Enjoy 70 PRO"] },
                { devices: ["HUAWEI NOVA 12", "HUAWEI NOVA 13"] },
                { devices: ["HUAWEI NOVA 12 PRO", "HUAWEI NOVA 13 PRO"] },
                { devices: ["Honor X7D 4G", "Honor 400 Smart", "Honor Play 10C 5G", "HONOR Play 70 Plus"] },
                { devices: ["HONOR 400 Lite", "HONOR X70i 5G"] },
                { devices: ["HONOR X9D", "HONOR X70"] },
                { devices: ["HUAWEI MatePad T10", "HONOR Pad X8 Lite", "HONOR Pad X6"] },
                { devices: ["HONOR X9D", "HONOR Magic 8 Lite"] }
            ],
            "Vivo": [ 
                { devices: ["V5", "V5s", "Y67"] },
                { devices: ["Y100", "T2 5G"] },
                { devices: ["Y90", "Y93", "Y91", "Y91i", "Y91C", "Y95", "Y1s"] },
                { devices: ["Y97", "V11", "V11i", "Z3", "Z3i"] },
                { devices: ["Y85", "V9", "V9 PRO", "Z1", "Z1i"] },
                { devices: ["Y81", "Y83"] },
                { devices: ["Y75", "V7"] },
                { devices: ["Y71", "Y71A", "Y71s", "Y73 5G"] },
                { devices: ["Y79", "V7 Plus"] },
                { devices: ["Y67", "V5"] },
                { devices: ["Y65", "Y66", "V5 Lite"] },
                { devices: ["Y21T", "Y31", "Y31s", "Y33s", "Y33T", "Y35 2022", "Y51 2020", "Y51A", "Y52s", "Y53s 5G", "Y55 5G", "Y55s", "Y56 5G", "Y72 5G", "Y72T", "Y73T", "Y74s", "Y75 5G", "Y76 5G", "Y76s", "Y77 5G", "Y77e", "T1 5G", "Z6x", "Z6 Lite", "Z3", "Z5x", "U3", "U3x", "T2x 5G"] },
                { devices: ["Y27 5G", "Y27s", "Y36 4G", "Y36 5G"] },
                { devices: ["Y17s", "Y22", "Y22s 2020", "Y28 5G", "Y33T", "Y36i", "Y36m"] },
                { devices: ["Y20", "Y20s", "Y20g", "Y20a", "Y20i", "Y15s", "Y15A", "Y12s", "Y12A", "Y10", "Y01", "Y11s", "Y21s"] },
                { devices: ["Y19", "Y5s", "U3"] },
                { devices: ["Y3", "Y3s", "Y11", "Y12", "Y15", "Y17 ( 2019 )"] },
                { devices: ["V15", "S1"] },
                { devices: ["Y21", "Y21S", "Y21T", "Y33s", "Y02s", "Y32", "Y025", "Y1", "Y16"] },
                { devices: ["Y30", "Y30i"] },
                { devices: ["vivo V20", "vivo V20 se"] },
                { devices: ["vivo X60", "vivo X60T", "vivo X70", "vivo X70T"] },
                { devices: ["Y28 4G", "Y38 5G"] },
                { devices: ["vivo V11", "V11 PRO", "X23", "X21s ( OLED )"] },
                { devices: ["Y7s", "Y9s", "S1", "S1 Prime", "S1 PRO", "Z5", "Z1x", "IQOO Neo", "V17 ( Russia )"] },
                { devices: ["vivo Y04", "Y19E", "Y29E", "Y29S"] },
                { devices: ["vivo v30", "vivo v30 pro", "vivo S17", "vivo S17P", "vivo S17T", "vivo x90 PRO", "vivo v29", "vivo v29 PRO", "vivo x70 PRO Plus", "vivo x80 PRO"] },
                { devices: ["vivo V27", "vivo S16", "vivo Y78 Plus", "vivo V29 Lite", "vivo V29e", "vivo Y100", "vivo Y200 PRO"] },
                { devices: ["vivo V20", "vivo V23E 4G", "vivo V23E 5G", "vivo Y73 4G 2021", "vivo S7T 5G"] }
            ],
            "Oppo": [ 
                { devices: ["F19", "F19 PRO", "F19 PRO Plus", "A96 5G", "Reno 4 SE 5G", "Reno 5F", "Reno 5Z", "Reno 5 Lite", "Reno 6 Lite", "Reno 6Z 5G", "Reno 7Z", "Reno 8 Lite", "Realme 8", "Realme 8 PRO", "Realme 7 PRO", "oppo X7", "oppo V15", "oppo Q2 PRO 5G", "oppo A94 4G", "oppo A94 5G", "oppo A95 4G", "oppo A95 5G", "oppo A74 4G"] },
                { devices: ["Reno 7z 5G", "Reno 8z 5G", "Reno 6 Lite 4G", "Reno 8 Lite", "F19 4G", "F19s 4G", "F21s PRO 5G", "Realme 8 4G"] },
                { devices: ["OPPO A72 5G", "A73 5G", "A53 5G", "Realme 7 5G", "Realme 7", "Narzo 30 PRO 5G"] },
                { devices: ["OPPO A52", "A72", "A92"] },
                { devices: ["OPPO A55 5G", "A56 5G", "V11", "V11s"] },
                { devices: ["OPPO A5s", "OPPO A7", "OPPO A12", "Realme 3", "Realme 3i"] },
                { devices: ["OPPO A57 4G", "OPPO A57 5G", "OPPO A57s", "OPPO A77 4G", "OPPO A77 5G", "OPPO A77s", "OPPO A97", "OPPO A38 5G", "OPPO A17 4G", "OPPO A17K", "OPPO A18", "OPPO A38", "OPPO A58 5G", "OPPO A1", "OPPO A1x", "OPPO A2x", "OPPO A2m", "OPPO A58x", "OPPO A78", "OPPO A56s", "OPPO A57e", "OPPO K10 5G", "OnePlus Nord N300 5G", "OnePlus N20 se"] },
                { devices: ["OPPO A76 4G", "A36 4G"] },
                { devices: ["OPPO A16", "A16s", "A16k", "A16 2021", "A53s", "A55 5G", "A56 5G", "A54s", "Realme C25", "C25s", "Narzo 50A"] },
                { devices: ["OPPO A15", "A15s", "A35", "Realme C11 2020", "C12", "C15", "Narzo 30A", "Narzo 20", "Narzo 20a"] },
                { devices: ["OPPO AX7", "AX5s"] },
                { devices: ["OPPO A1k", "Realme C2"] },
                { devices: ["OPPO A11", "A11x", "A5 2020", "A9 2020", "A31 2020", "A51", "Realme 5", "5i", "5s", "6i", "C3", "C3i", "Narzo 10A", "Narzo 20A"] },
                { devices: ["OPPO Reno 10", "Reno 10 PRO"] },
                { devices: ["OPPO Reno 6 PRO", "6 PRO 5G"] },
                { devices: ["OPPO A3s", "A5", "Realme 2", "C1"] },
                { devices: ["Realme C65 4G", "Realme C65 5G", "Realme C63 5G", "Realme C75 5G", "Realme C73 5G", "Realme C75x", "OPPO A40", "OPPO A40M", "OPPO A60", "OPPO A80", "Realme V60", "Realme V60S", "Realme V60 Pro", "Realme K12x 5G", "Narzo N65", "Realme 12X 4G", "Realme 14X 5G", "OPPO A3i 5G", "OPPO A3 Vitality", "OPPO A3 4G", "OPPO A3 5G", "OPPO A3X 4G", "OPPO A3X 5G", "OPPO A3 Pro", "OPPO A5 Vitality 5G", "OPPO A5 Pro 4G", "OPPO A5 Pro 5G"] },
                { devices: ["Realme 9i 5G", "Realme 10 5G", "Realme 10s 5G"] },
                { devices: ["Realme C53", "C51", "Narzo N53", "Realme Note 50", "Realme C60"] },
                { devices: ["Realme C35", "Narzo 50A Prime", "Realme Prime C3", "Realme Prime C5"] },
                { devices: ["Y67", "V5"] },
                { devices: ["Y71", "Y71a", "Y71s", "Y73"] },
                { devices: ["Y85", "Y85a", "V9", "Z1", "Z1i", "Z3x"] },
                { devices: ["Y75", "V7"] },
                { devices: ["Y79", "V7 Plus"] },
                { devices: ["Y81", "Y81i", "Y83", "Y83s"] },
                { devices: ["A83", "A1"] },
                { devices: ["Y21", "Y21s", "Y21T", "Y02s", "Y16"] },
                { devices: ["Y11s", "Y12s", "Y15s", "Y20", "Y20i"] },
                { devices: ["Realme XT", "X2", "OPPO K5", "OPPO Reno Z"] },
                { devices: ["F11", "A9", "A9x"] },
                { devices: ["Realme C31", "C33s"] },
                { devices: ["OPPO Reno 11F", "K12", "F25 PRO", "OnePlus Nord CE4"] },
                { devices: ["OnePlus 10R", "Realme GT Neo 3", "oppo Reno 8 Pro Plus", "oppo Reno 8 Pro", "OnePlus 10R", "Realme GT2 Explorer Master", "OnePlus 12", "OnePlus Ace"] },
                { devices: ["Reno 7 se", "Realme 9 PRO Plus", "F21pro 4G", "F21s pro 4G", "OnePlus Nord CE 2 5G", "Reno8 4G", "Reno8 5G", "Find X5 Lite", "Reno 7 4G", "Realme Narzo 50Pro", "Realme 9 4G", "Realme 10 4G", "Reno 8T", "Reno8 5G", "A78 4G", "Realme 11"] },
                { devices: ["Nord N200 5G", "oppo A74 5G", "oppo A54 5G", "oppo A93 5G", "Nord N200 5G"] },
                { devices: ["OnePlus Nord N100", "oppo A11s", "oppo A54 4G", "Realme 7i", "OPPO A33", "oppo A55 4G", "oppo A53", "Realme C17", "oppo A33 (2020)", "oppo A32", "oppo A53s", "A51 2021", "A51 2020"] },
                { devices: ["OnePlus 9RT 5G", "Realme GT Neo2", "Realme Q5 Pro", "Realme GT2", "oppo K10 Pro", "oppo Reno 8 Pro (China)", "Realme GT Neo 3T", "OnePlus 9RT 5G"] },
                { devices: ["OnePlus Nord 5G", "OnePlus Z 5G", "OnePlus 8 Nord 5G"] },
                { devices: ["OPPO Reno 5 PRO", "OPPO Find X3", "Find X3 PRO", "OnePlus 9 PRO"] },
                { devices: ["OnePlus Nord CE 5G", "OPPO Reno 5 4G", "Reno 5 5G", "Reno 6 4G", "Reno 6 5G", "K9 Pro", "Realme X7 MAX 5G", "Realme GT 5G", "Realme GT Neo", "Realme Q3 Pro 5G", "Reno 5K 5G", "Oppo K9", "OPPO Find X3 Lite", "OnePlus Nord 2T 5G", "Reno 5G", "Reno 7 5G", "Realme GT Neo Flash", "GT MASTER EDITION", "OnePlus Nord 2 5G"] },
                { devices: ["Y35 Plus", "Y35m Plus", "Y27", "Y36 5G"] },
                { devices: ["Y35", "Y55s"] },
                { devices: ["Realme C63 4G", "Realme C61", "Realme Note 60", "Note 60x", "Narzo N61", "Narzo N63"] },
                { devices: ["Realme C75 4G", "Realme P3X 5G", "Realme 13 5G", "Realme C67 4G", "Realme 12 5G", "Realme 12X 5G", "Narzo 70X 5G"] },
                { devices: ["OnePlus 8", "OPPO Reno 4 PRO"] },
                { devices: ["Oppo Reno 14F 5G", "OPPO A6 Pro", "OPPO F31 Pro 5G", "Realme 15T 5G"] },
                { devices: ["Realme 12 Plus 5G", "Realme Narzo 70 5G", "Realme Narzo 70 PRO 5G", "Realme P1 5G"] },
                { devices: ["ONEPLUS NORD CE 4 LITE 5G", "REALME 12 4G", "REALME 13 4G", "REALME 13 Plus", "REALME 13 PRO", "REALME 14", "REALME 14T", "OPPO Reno 12F 4G"] },
                { devices: ["Realme C85", "OPPO A6X", "Realme 15X 5G"] },
                { devices: ["Realme GT 8 5G", "Realme GT 8 PRO 5G"] },
                { devices: ["Realme GT 5 PRO", "Realme GT 6 5G", "OPPO Find X7 5G", "OnePlus 12R"] },
                { devices: ["Realme GT 7 5G", "Realme Neo 7 SE 5G", "Realme Neo 7 Turbo 5G"] },
                { devices: ["Realme GT 3 5G", "Realme GT 5", "Realme GT Neo 5 5G", "Realme GT Neo 5 SE 5G", "OnePlus Nord 3 5G", "OnePlus Ace 2V 5G"] }
            ],
            "Realme": [ 
                { devices: ["F19", "F19 PRO", "F19 PRO Plus", "A96 5G", "Reno 4 SE 5G", "Reno 5F", "Reno 5Z", "Reno 5 Lite", "Reno 6 Lite", "Reno 6Z 5G", "Reno 7Z", "Reno 8 Lite", "Realme 8", "Realme 8 PRO", "Realme 7 PRO", "oppo X7", "oppo V15", "oppo Q2 PRO 5G", "oppo A94 4G", "oppo A94 5G", "oppo A95 4G", "oppo A95 5G", "oppo A74 4G"] },
                { devices: ["OPPO Reno 4 4G", "Reno 4 Lite", "Reno 4 F", "A93 4G", "F17 PRO"] },
                { devices: ["OPPO A73 4C 2020", "A91", "F15", "F17", "Reno 3"] },
                { devices: ["OPPO F9", "F9 PRO", "A7x", "Realme 2 PRO"] },
                { devices: ["OPPO F7", "A3"] },
                { devices: ["OPPO F3", "A77s"] },
                { devices: ["OPPO A59", "F1s"] },
                { devices: ["Realme 9 5G", "9 PRO", "K9s", "CE 2 Lite"] },
                { devices: ["Realme 8", "Realme 8 5G", "Narzo 30 5G", "V13", "Q13", "Q3i", "A93s"] },
                { devices: ["Realme 8i", "Realme 9i", "Narzo 50", "K10 4G", "A96 4G (India)"] },
                { devices: ["Realme 6 PRO", "OPPO A92s", "Reno 4z"] },
                { devices: ["Realme 6", "6s", "7 4G", "Narzo 30 4G", "Narzo 20 PRO"] },
                { devices: ["Realme 3 PRO", "Realme 5 PRO", "Realme X Lite", "Realme Q"] },
                { devices: ["Realme C30", "C30s", "C30F", "C33", "Narzo 50i Prime"] },
                { devices: ["Realme C11 2021", "C20", "C21", "Narzo 50i"] },
                { devices: ["Realme C21y", "Realme C25y"] },
                { devices: ["Realme GT Neo", "GT Neo 5G"] },
                { devices: ["Realme C55", "Realme C67 5G", "Realme 11 5G", "Realme 11x 5G", "A1 2023", "Narzo N55", "Narzo 60x 5G", "Realme K11x", "OPPO A58 4G", "OPPO A79 5G", "OPPO A98 5G", "OPPO F23 5G", "OnePlus Nord N30 5G", "OnePlus N30 SE 5G", "OnePlus Nord 60x", "OPPO V50", "OPPO V50s"] },
                { devices: ["Realme 11 PRO Plus", "Realme 11 PRO", "Reno 10", "Reno 9", "Reno 8T 5G", "Realme 12 PRO", "Realme 12 PRO Plus 5G"] },
                { devices: ["Reno 2F", "Reno 2Z", "Reno K3"] },
                { devices: ["Reno 7z 5G", "Reno 8z 5G", "Reno 6 Lite 4G", "Reno 8 Lite", "F19 4G", "F19s 4G", "F21s PRO 5G", "Realme 8 4G"] },
                { devices: ["OPPO A72 5G", "A73 5G", "A53 5G", "Realme 7 5G", "Realme 7", "Narzo 30 PRO 5G"] },
                { devices: ["OPPO A52", "A72", "A92"] },
                { devices: ["OPPO A55 5G", "A56 5G", "V11", "V11s"] },
                { devices: ["OPPO A5s", "OPPO A7", "OPPO A12", "Realme 3", "Realme 3i"] },
                { devices: ["OPPO A57 4G", "OPPO A57 5G", "OPPO A57s", "OPPO A77 4G", "OPPO A77 5G", "OPPO A77s", "OPPO A97", "OPPO A38 5G", "OPPO A17 4G", "OPPO A17K", "OPPO A18", "OPPO A38", "OPPO A58 5G", "OPPO A1", "OPPO A1x", "OPPO A2x", "OPPO A2m", "OPPO A58x", "OPPO A78", "OPPO A56s", "OPPO A57e", "OPPO K10 5G", "OnePlus Nord N300 5G", "OnePlus N20 se"] },
                { devices: ["OPPO A76 4G", "A36 4G"] },
                { devices: ["OPPO A16", "A16s", "A16k", "A16 2021", "A53s", "A55 5G", "A56 5G", "A54s", "Realme C25", "C25s", "Narzo 50A"] },
                { devices: ["OPPO A15", "A15s", "A35", "Realme C11 2020", "C12", "C15", "Narzo 30A", "Narzo 20", "Narzo 20a"] },
                { devices: ["OPPO AX7", "AX5s"] },
                { devices: ["OPPO A1k", "Realme C2"] },
                { devices: ["OPPO A11", "A11x", "A5 2020", "A9 2020", "A31 2020", "A51", "Realme 5", "5i", "5s", "6i", "C3", "C3i", "Narzo 10A", "Narzo 20A"] },
                { devices: ["OPPO Reno 10", "Reno 10 PRO"] },
                { devices: ["OPPO Reno 6 PRO", "6 PRO 5G"] },
                { devices: ["OPPO A3s", "A5", "Realme 2", "C1"] },
                { devices: ["Realme C65 4G", "Realme C65 5G", "Realme C63 5G", "Realme C75 5G", "Realme C73 5G", "Realme C75x", "OPPO A40", "OPPO A40M", "OPPO A60", "OPPO A80", "Realme V60", "Realme V60S", "Realme V60 Pro", "Realme K12x 5G", "Narzo N65", "Realme 12X 4G", "Realme 14X 5G", "OPPO A3i 5G", "OPPO A3 Vitality", "OPPO A3 4G", "OPPO A3 5G", "OPPO A3X 4G", "OPPO A3X 5G", "OPPO A3 Pro", "OPPO A5 Vitality 5G", "OPPO A5 Pro 4G", "OPPO A5 Pro 5G"] },
                { devices: ["Realme 9i 5G", "Realme 10 5G", "Realme 10s 5G"] },
                { devices: ["Realme C53", "C51", "Narzo N53", "Realme Note 50", "Realme C60"] },
                { devices: ["Realme C35", "Narzo 50A Prime", "Realme Prime C3", "Realme Prime C5"] },
                { devices: ["Y67", "V5"] },
                { devices: ["Y71", "Y71a", "Y71s", "Y73"] },
                { devices: ["Y85", "Y85a", "V9", "Z1", "Z1i", "Z3x"] },
                { devices: ["Y75", "V7"] },
                { devices: ["Y79", "V7 Plus"] },
                { devices: ["Y81", "Y81i", "Y83", "Y83s"] },
                { devices: ["A83", "A1"] },
                { devices: ["Y21", "Y21s", "Y21T", "Y02s", "Y16"] },
                { devices: ["Y11s", "Y12s", "Y15s", "Y20", "Y20i"] },
                { devices: ["Realme XT", "X2", "OPPO K5", "OPPO Reno Z"] },
                { devices: ["F11", "A9", "A9x"] },
                { devices: ["Realme C31", "C33s"] },
                { devices: ["OPPO Reno 11F", "K12", "F25 PRO", "OnePlus Nord CE4"] },
                { devices: ["OnePlus 10R", "Realme GT Neo 3", "oppo Reno 8 Pro Plus", "oppo Reno 8 Pro", "OnePlus 10R", "Realme GT2 Explorer Master", "OnePlus 12", "OnePlus Ace"] },
                { devices: ["Reno 7 se", "Realme 9 PRO Plus", "F21pro 4G", "F21s pro 4G", "OnePlus Nord CE 2 5G", "Reno8 4G", "Reno8 5G", "Find X5 Lite", "Reno 7 4G", "Realme Narzo 50Pro", "Realme 9 4G", "Realme 10 4G", "Reno 8T", "Reno8 5G", "A78 4G", "Realme 11"] },
                { devices: ["Nord N200 5G", "oppo A74 5G", "oppo A54 5G", "oppo A93 5G", "Nord N200 5G"] },
                { devices: ["OnePlus Nord N100", "oppo A11s", "oppo A54 4G", "Realme 7i", "OPPO A33", "oppo A55 4G", "oppo A53", "Realme C17", "oppo A33 (2020)", "oppo A32", "oppo A53s", "A51 2021", "A51 2020"] },
                { devices: ["OnePlus 9RT 5G", "Realme GT Neo2", "Realme Q5 Pro", "Realme GT2", "oppo K10 Pro", "oppo Reno 8 Pro (China)", "Realme GT Neo 3T", "OnePlus 9RT 5G"] },
                { devices: ["OnePlus Nord 5G", "OnePlus Z 5G", "OnePlus 8 Nord 5G"] },
                { devices: ["OPPO Reno 5 PRO", "OPPO Find X3", "Find X3 PRO", "OnePlus 9 PRO"] },
                { devices: ["OnePlus Nord CE 5G", "OPPO Reno 5 4G", "Reno 5 5G", "Reno 6 4G", "Reno 6 5G", "K9 Pro", "Realme X7 MAX 5G", "Realme GT 5G", "Realme GT Neo", "Realme Q3 Pro 5G", "Reno 5K 5G", "Oppo K9", "OPPO Find X3 Lite", "OnePlus Nord 2T 5G", "Reno 5G", "Reno 7 5G", "Realme GT Neo Flash", "GT MASTER EDITION", "OnePlus Nord 2 5G"] },
                { devices: ["Y35 Plus", "Y35m Plus", "Y27", "Y36 5G"] },
                { devices: ["Y35", "Y55s"] },
                { devices: ["Realme C63 4G", "Realme C61", "Realme Note 60", "Note 60x", "Narzo N61", "Narzo N63"] },
                { devices: ["Realme C75 4G", "Realme P3X 5G", "Realme 13 5G", "Realme C67 4G", "Realme 12 5G", "Realme 12X 5G", "Narzo 70X 5G"] },
                { devices: ["OnePlus 8", "OPPO Reno 4 PRO"] },
                { devices: ["Oppo Reno 14F 5G", "OPPO A6 Pro", "OPPO F31 Pro 5G", "Realme 15T 5G"] },
                { devices: ["Realme 12 Plus 5G", "Realme Narzo 70 5G", "Realme Narzo 70 PRO 5G", "Realme P1 5G"] },
                { devices: ["ONEPLUS NORD CE 4 LITE 5G", "REALME 12 4G", "REALME 13 4G", "REALME 13 Plus", "REALME 13 PRO", "REALME 14", "REALME 14T", "OPPO Reno 12F 4G"] },
                { devices: ["Realme C85", "OPPO A6X", "Realme 15X 5G"] },
                { devices: ["Realme GT 8 5G", "Realme GT 8 PRO 5G"] },
                { devices: ["Realme GT 5 PRO", "Realme GT 6 5G", "OPPO Find X7 5G", "OnePlus 12R"] },
                { devices: ["Realme GT 7 5G", "Realme Neo 7 SE 5G", "Realme Neo 7 Turbo 5G"] },
                { devices: ["Realme GT 3 5G", "Realme GT 5", "Realme GT Neo 5 5G", "Realme GT Neo 5 SE 5G", "OnePlus Nord 3 5G", "OnePlus Ace 2V 5G"] }
            ]
        }
    };

    // 2. منطق التطبيق - مع ربط جميع الدوال بالجذر (window) لكي لا يتم حجبها
    let currentMode = 'batteries';
    let currentBrand = "Samsung";
    const reduce = matchMedia('(prefers-reduced-motion: reduce)').matches;
    const COLORS = ['#10b981','#34d399','#6ee7b7','#0ea5e9','#ffffff'];

    function movePill(){
        const a = document.querySelector('.main-tab.active-section'), p = document.getElementById('pill');
        if(!a) return;
        p.style.width = a.offsetWidth + 'px';
        p.style.transform = 'translateX(' + a.offsetLeft + 'px)';
    }

    window.setMode = function(mode) {
        currentMode = mode;
        document.getElementById('btn-bat').classList.toggle('active-section', mode === 'batteries');
        document.getElementById('btn-scr').classList.toggle('active-section', mode === 'screens');
        currentBrand = Object.keys(data[currentMode])[0];
        movePill();
        window.setupBrands();
        window.render();
    };

    window.setupBrands = function() {
        const container = document.getElementById('brandContainer');
        container.innerHTML = '';
        Object.keys(data[currentMode]).forEach((brand, i) => {
            const b = document.createElement('div');
            b.className = 'brand-btn pr' + (brand === currentBrand ? ' active' : '');
            b.style.setProperty('--i', i);
            b.textContent = brand;
            b.setAttribute('role', 'button'); b.tabIndex = 0;
            b.addEventListener('click', () => window.changeBrand(b, brand));
            b.addEventListener('keydown', e => { if(e.key === 'Enter' || e.key === ' '){ e.preventDefault(); window.changeBrand(b, brand); } });
            container.appendChild(b);
        });
    };

    window.changeBrand = function(el, brand) {
        currentBrand = brand;
        document.querySelectorAll('.brand-btn').forEach(btn => btn.classList.remove('active'));
        el.classList.add('active');
        window.render();
    };

    window.render = function() {
        const input = document.getElementById('searchInput');
        const query = input.value.toLowerCase().trim();
        const resultsDiv = document.getElementById('results');
        document.getElementById('searchWrap').classList.toggle('has', input.value.length > 0);

        if (query === "") { resultsDiv.innerHTML = ""; return; }
        resultsDiv.innerHTML = "";
        let found = false, n = 0;

        data[currentMode][currentBrand].forEach(item => {
            const isMatch = item.devices.some(d => d.toLowerCase().includes(query));
            if (isMatch) {
                found = true;
                const card = document.createElement('div');
                card.className = 'card pr';
                card.style.setProperty('--i', Math.min(n++, 8));
                const list = document.createElement('div');
                list.className = 'd-list';
                item.devices.forEach((d, ti) => {
                    const tag = document.createElement('span');
                    tag.className = 'tag' + (d.toLowerCase().includes(query) ? ' match' : '');
                    tag.style.setProperty('--t', Math.min(ti, 14));
                    tag.textContent = d;
                    list.appendChild(tag);
                });
                card.appendChild(list);
                card.dataset.copy = item.devices.join(', ');
                resultsDiv.appendChild(card);
            }
        });

        if (!found) resultsDiv.innerHTML = `<p class="empty">لا توجد نتائج في هذا القسم</p>`;
    };

    /* ---------- search input ---------- */
    document.getElementById('searchInput').addEventListener('input', () => window.render());
    document.getElementById('clearBtn').addEventListener('click', () => {
        const i = document.getElementById('searchInput'); i.value = ''; window.render(); i.focus(); buzz(8);
    });

    /* ---------- effects ---------- */
    function buzz(ms){ try{ navigator.vibrate && navigator.vibrate(ms); }catch(_){} }
    function ripple(el, e){
        const r = el.getBoundingClientRect(), s = Math.max(r.width, r.height)*2.4, n = document.createElement('span');
        n.className = 'ripple';
        n.style.cssText = 'width:'+s+'px;height:'+s+'px;left:'+(e.clientX-r.left-s/2)+'px;top:'+(e.clientY-r.top-s/2)+'px';
        el.appendChild(n); setTimeout(() => n.remove(), 800);
    }
    function burst(x, y, n, power){
        if(reduce) return;
        const ring = document.createElement('div'); ring.className = 'shock';
        const rs = power*2.2; ring.style.cssText = 'left:'+x+'px;top:'+y+'px;width:'+rs+'px;height:'+rs+'px';
        document.body.appendChild(ring); setTimeout(() => ring.remove(), 850);
        for(let i=0;i<n;i++){
            const s = document.createElement('i'); s.className = 'spark';
            const sz = 4+Math.random()*6, c = COLORS[i%COLORS.length];
            s.style.cssText = 'left:'+x+'px;top:'+y+'px;width:'+sz+'px;height:'+sz+'px;background:'+c+';box-shadow:0 0 10px '+c;
            document.body.appendChild(s);
            const a = Math.random()*6.283, d = power*(.5+Math.random()*.9);
            s.animate([
                {transform:'translate(-50%,-50%) scale(1)',opacity:1},
                {transform:'translate(calc(-50% + '+Math.cos(a)*d+'px),calc(-50% + '+(Math.sin(a)*d+power*.5)+'px)) scale(0)',opacity:0}
            ],{duration:600+Math.random()*500,easing:'cubic-bezier(.1,.8,.3,1)'}).onfinish = () => s.remove();
        }
    }

    /* press physics (delegated): tilt toward the press point + ripple */
    let cur = null;
    function release(){
        if(!cur) return;
        cur.classList.remove('pressed'); cur.style.setProperty('--rx','0deg'); cur.style.setProperty('--ry','0deg'); cur = null;
    }
    document.addEventListener('pointermove', e => {
        const el = e.target.closest && e.target.closest('.pr');
        if(!el) return;
        const r = el.getBoundingClientRect();
        el.style.setProperty('--bx', (e.clientX-r.left)+'px'); el.style.setProperty('--by', (e.clientY-r.top)+'px');
    });
    document.addEventListener('pointerdown', e => {
        if(e.button > 0) return;
        const el = e.target.closest && e.target.closest('.pr');
        if(!el) return;
        const r = el.getBoundingClientRect(), amt = el.classList.contains('card') ? 5 : 14;
        if(!reduce){
            el.style.setProperty('--ry', (((e.clientX-r.left)/r.width-.5)*-amt)+'deg');
            el.style.setProperty('--rx', (((e.clientY-r.top)/r.height-.5)*amt)+'deg');
        }
        cur = el; el.classList.add('pressed'); ripple(el, e); buzz(10);
        if(el.classList.contains('main-tab')) burst(e.clientX, e.clientY, 8, 60);
        else if(el.classList.contains('brand-btn')) burst(e.clientX, e.clientY, 6, 45);
    });
    ['pointerup','pointercancel'].forEach(ev => document.addEventListener(ev, release));

    /* ---------- copy on card click ---------- */
    function copyText(t){
        if(navigator.clipboard && window.isSecureContext) return navigator.clipboard.writeText(t);
        return new Promise((ok, no) => {
            const ta = document.createElement('textarea'); ta.value = t; ta.style.cssText = 'position:fixed;opacity:0';
            document.body.appendChild(ta); ta.select();
            try{ document.execCommand('copy') ? ok() : no(); }catch(err){ no(err); }
            ta.remove();
        });
    }
    let toastT;
    document.getElementById('results').addEventListener('click', e => {
        const card = e.target.closest('.card');
        if(!card) return;
        copyText(card.dataset.copy).then(() => {
            card.classList.remove('copied'); void card.offsetWidth; card.classList.add('copied');
            burst(e.clientX, e.clientY, 16, 100); buzz([15,30,15]);
            const t = document.getElementById('copy-toast');
            t.classList.add('show'); clearTimeout(toastT); toastT = setTimeout(() => t.classList.remove('show'), 1800);
        }).catch(() => {});
    });

    /* ---------- background network ---------- */
    (function(){
        const cv = document.getElementById('bg-canvas'), cx = cv.getContext('2d'); let W, H, pts = [], mouse = {x:-999,y:-999};
        function size(){
            const d = Math.min(devicePixelRatio||1, 2); W = innerWidth; H = innerHeight;
            cv.width = W*d; cv.height = H*d; cx.setTransform(d,0,0,d,0,0);
            const n = Math.min(70, Math.floor(W*H/18000)); pts = [];
            for(let i=0;i<n;i++) pts.push({x:Math.random()*W,y:Math.random()*H,vx:(Math.random()-.5)*.35,vy:(Math.random()-.5)*.35,r:Math.random()*1.6+.6});
        }
        function frame(){
            cx.clearRect(0,0,W,H);
            for(let i=0;i<pts.length;i++){
                const p = pts[i], dx = p.x-mouse.x, dy = p.y-mouse.y, dd = dx*dx+dy*dy;
                if(dd<14000){ const f = (1-dd/14000)*.6, l = Math.sqrt(dd||1); p.vx += dx/l*f*.12; p.vy += dy/l*f*.12; }
                p.vx *= .99; p.vy *= .99; p.x += p.vx; p.y += p.vy;
                if(p.x<0||p.x>W) p.vx *= -1; if(p.y<0||p.y>H) p.vy *= -1;
                cx.beginPath(); cx.arc(p.x,p.y,p.r,0,6.283); cx.fillStyle = 'rgba(52,211,153,.7)'; cx.fill();
                for(let j=i+1;j<pts.length;j++){
                    const q = pts[j], ax = p.x-q.x, ay = p.y-q.y, d2 = ax*ax+ay*ay;
                    if(d2<12000){ cx.strokeStyle = 'rgba(16,185,129,'+(0.2*(1-d2/12000))+')'; cx.lineWidth = 1; cx.beginPath(); cx.moveTo(p.x,p.y); cx.lineTo(q.x,q.y); cx.stroke(); }
                }
            }
            if(!document.hidden) requestAnimationFrame(frame);
        }
        size(); addEventListener('resize', size);
        if(!reduce){
            frame();
            document.addEventListener('visibilitychange', () => { if(!document.hidden) frame(); });
            addEventListener('pointermove', e => { mouse.x = e.clientX; mouse.y = e.clientY; });
        }
    })();

    // 3. التنفيذ المباشر فور قراءة الكود بدون انتظار (لتخطي الكاش ومشاكل الاستضافة)
    window.setupBrands();
    window.render();
    movePill();
    addEventListener('resize', movePill);
    if(document.fonts && document.fonts.ready) document.fonts.ready.then(movePill);
    </script>
<script type="module" src="https://static.cloudflareinsights.com/beacon.min.js/v4bc70e2c01a94c73b74392e4234840661791215815920" integrity="sha512-L0ha0OXavK/8okipN9F8BtP84dg9DUhPERbBXzwI6dgTA55d2+yweo3pn5CSFYs45/r8md2+xvUPtTdvTNRfjA==" data-cf-beacon='{"version":"2024.11.0","token":"f989edb4bc01435799993ae901521137","r":1,"spa":2}' crossorigin="anonymous"></script>
</body>
</html>
