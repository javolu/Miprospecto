<!DOCTYPE html>

<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<meta name="theme-color" content="#0f1117">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
<meta name="apple-mobile-web-app-title" content="MiProspecto">
<title>MiProspecto</title>
<link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;600;700;800&display=swap" rel="stylesheet">
<style>
*{box-sizing:border-box;margin:0;padding:0;-webkit-tap-highlight-color:transparent}
:root{
  --bg:#0f1117;--card:#1a1f2e;--card2:#222840;--b:#2a3050;--b2:#3a4470;
  --blue:#4f8ef7;--green:#34d399;--orange:#fb923c;--red:#f87171;--yellow:#fbbf24;--purple:#a78bfa;
  --t:#e8ecf4;--t2:#8892b0;--t3:#4a5470;
}
html,body{height:100%;overflow:hidden;background:var(--bg);color:var(--t);font-family:'Plus Jakarta Sans',sans-serif;-webkit-text-size-adjust:100%}
body{max-width:430px;margin:0 auto;display:flex;flex-direction:column;height:100vh;height:100dvh}

/* ── SCREENS ── */
.scr{display:none;flex-direction:column;flex:1;overflow:hidden;min-height:0}
.scr.on{display:flex;flex-direction:column}

/* ── TOPBAR ── */
.tb{padding:14px 18px 10px;background:rgba(15,17,23,.96);backdrop-filter:blur(12px);border-bottom:1px solid var(–b);flex-shrink:0}
.tb-row{display:flex;align-items:center;justify-content:space-between;margin-bottom:10px}
.logo{font-weight:800;font-size:1rem;background:linear-gradient(135deg,var(–blue),var(–purple));-webkit-background-clip:text;-webkit-text-fill-color:transparent}
.tabs{display:flex;gap:6px;overflow-x:auto;scrollbar-width:none}
.tabs::-webkit-scrollbar{display:none}
.tab{flex-shrink:0;padding:5px 12px;border-radius:20px;font-size:.7rem;font-weight:700;cursor:pointer;border:1.5px solid var(–b);color:var(–t2);background:none;white-space:nowrap;transition:all .15s}
.tab.on{background:var(–blue);border-color:var(–blue);color:#fff}

/* ── SCROLL AREA ── */
.area{flex:1;overflow-y:auto;padding:14px 16px 10px;-webkit-overflow-scrolling:touch;min-height:0}
.area::-webkit-scrollbar{display:none}

/* ── NAV ── */
.nav{display:flex;background:rgba(15,17,23,.97);border-top:1px solid var(–b);padding:6px 0 18px;flex-shrink:0;position:relative;z-index:10}
.nb{flex:1;display:flex;flex-direction:column;align-items:center;gap:2px;padding:4px;cursor:pointer;color:var(–t3);font-size:.58rem;font-weight:700;border:none;background:none;font-family:‘Plus Jakarta Sans’,sans-serif;transition:color .15s}
.nb.on{color:var(–blue)}
.ni{font-size:1.15rem}

/* ── FAB ── */
.fab{position:fixed;bottom:76px;right:18px;width:54px;height:54px;border-radius:50%;background:linear-gradient(135deg,var(–blue),var(–purple));color:#fff;font-size:1.5rem;border:none;cursor:pointer;box-shadow:0 4px 20px rgba(79,142,247,.5);display:flex;align-items:center;justify-content:center;z-index:100;transition:transform .15s}
.fab:active{transform:scale(.9)}

/* ── STATS ── */
.stats{display:flex;gap:8px;margin-bottom:12px}
.st{flex:1;background:var(–card);border:1.5px solid var(–b);border-radius:12px;padding:10px;text-align:center}
.st-n{font-size:1.3rem;font-weight:800}
.st-l{font-size:.6rem;color:var(–t3);margin-top:2px;font-weight:600}

/* ── SEARCH ── */
.srch{position:relative;margin-bottom:12px}
.srch input{width:100%;background:var(–card);border:1.5px solid var(–b);border-radius:12px;padding:11px 14px 11px 40px;color:var(–t);font-family:‘Plus Jakarta Sans’,sans-serif;font-size:.84rem;outline:none;transition:border-color .2s}
.srch input:focus{border-color:var(–blue)}
.srch input::placeholder{color:var(–t3)}
.srch-ic{position:absolute;left:13px;top:50%;transform:translateY(-50%);font-size:.9rem;color:var(–t3);pointer-events:none}

/* ── PROSPECT CARD ── */
.pc{background:var(–card);border:1.5px solid var(–b);border-radius:14px;margin-bottom:9px;overflow:hidden;transition:border-color .2s}
.pc.open{border-color:var(–blue)}
.pc-h{padding:13px 15px;display:flex;align-items:center;gap:11px;cursor:pointer}
.av{width:42px;height:42px;border-radius:11px;display:flex;align-items:center;justify-content:center;font-weight:800;font-size:.95rem;flex-shrink:0}
.pi{flex:1;min-width:0}
.pn{font-weight:700;font-size:.87rem;white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
.ps{font-size:.68rem;color:var(–t2);margin-top:1px;white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
.pr{display:flex;flex-direction:column;align-items:flex-end;gap:4px;flex-shrink:0}
.badge{font-size:.58rem;font-weight:700;padding:3px 8px;border-radius:20px;border:1.5px solid currentColor;white-space:nowrap}
.chv{color:var(–t3);font-size:.75rem;transition:transform .2s}
.pc.open .chv{transform:rotate(180deg)}

/* ── CARD BODY ── */
.pc-b{display:none;padding:0 15px 13px;border-top:1px solid var(–b)}
.pc.open .pc-b{display:block}
.dg{display:flex;flex-direction:column;gap:6px;padding-top:11px}
.dr{display:flex;align-items:flex-start;gap:8px;font-size:.75rem}
.dl{color:var(–t3);font-size:.6rem;width:55px;flex-shrink:0;text-transform:uppercase;letter-spacing:.04em;padding-top:1px}
.dv{color:var(–t);flex:1;word-break:break-word}
.dv a{color:var(–blue);text-decoration:none}
.notebox{margin-top:7px;background:var(–bg);border-radius:9px;padding:9px 11px;font-size:.73rem;color:var(–t2);line-height:1.5;white-space:pre-wrap}

/* STATUS QUICK CHANGE */
.ss{display:flex;gap:5px;overflow-x:auto;scrollbar-width:none;margin-top:10px;padding-bottom:2px}
.ss::-webkit-scrollbar{display:none}
.sb{flex-shrink:0;padding:4px 10px;border-radius:20px;font-size:.63rem;font-weight:700;border:1.5px solid currentColor;cursor:pointer;background:none;font-family:‘Plus Jakarta Sans’,sans-serif;opacity:.45;transition:opacity .15s}
.sb.on{opacity:1}

/* ACTIONS */
.acts{display:flex;gap:6px;margin-top:11px;padding-top:10px;border-top:1px solid var(–b)}
.ac{flex:1;background:var(–card2);border:1.5px solid var(–b);border-radius:9px;padding:8px 3px;font-size:.68rem;font-weight:700;color:var(–t2);cursor:pointer;text-align:center;font-family:‘Plus Jakarta Sans’,sans-serif;transition:all .15s;display:flex;align-items:center;justify-content:center;gap:3px}
.ac:active{transform:scale(.95)}
.ac.call{border-color:var(–green);color:var(–green)}
.ac.mail{border-color:var(–blue);color:var(–blue)}
.ac.edit{border-color:var(–yellow);color:var(–yellow)}
.ac.del{border-color:var(–red);color:var(–red)}

/* ── EMPTY ── */
.empty{text-align:center;padding:48px 20px;color:var(–t3)}
.empty-i{font-size:2.5rem;opacity:.35;margin-bottom:10px}
.empty-t{font-weight:700;font-size:.95rem;color:var(–t2);margin-bottom:5px}
.empty-s{font-size:.75rem;line-height:1.55}

/* ── DISCOVER ── */
.tile{background:var(–card);border:1.5px solid var(–b);border-radius:14px;padding:13px 15px;margin-bottom:8px;display:flex;align-items:center;gap:11px}
.ti{flex:1;min-width:0}
.tn{font-weight:700;font-size:.85rem;white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
.tm{font-size:.67rem;color:var(–t2);margin-top:2px}
.tt{font-size:.58rem;font-weight:700;padding:2px 7px;border-radius:20px;background:rgba(79,142,247,.15);color:var(–blue);border:1px solid rgba(79,142,247,.3);display:inline-block;margin-top:4px}
.add{width:34px;height:34px;border-radius:9px;background:rgba(52,211,153,.1);border:1.5px solid var(–green);color:var(–green);font-size:1.1rem;display:flex;align-items:center;justify-content:center;flex-shrink:0;cursor:pointer;transition:all .15s;font-weight:700}
.add:active{transform:scale(.88)}
.add.done{opacity:.5;pointer-events:none}
.secs{display:flex;gap:5px;overflow-x:auto;scrollbar-width:none;margin-bottom:11px}
.secs::-webkit-scrollbar{display:none}

/* ── IMPORT ── */
.how{background:linear-gradient(135deg,rgba(52,211,153,.08),rgba(79,142,247,.08));border:1.5px solid rgba(52,211,153,.25);border-radius:14px;padding:13px 15px;margin-bottom:14px}
.how-t{font-size:.75rem;font-weight:700;color:var(–green);margin-bottom:6px}
.how-b{font-size:.72rem;color:var(–t2);line-height:1.65}
.lbl{display:block;font-size:.62rem;font-weight:700;color:var(–t3);text-transform:uppercase;letter-spacing:.06em;margin-bottom:5px}
.ta{width:100%;background:var(–card);border:1.5px solid var(–b);border-radius:12px;padding:11px 13px;color:var(–t);font-family:‘Plus Jakarta Sans’,system-ui,sans-serif;font-size:.82rem;outline:none;resize:vertical;min-height:160px;line-height:1.55;transition:border-color .2s}
.ta:focus{border-color:var(–blue)}
.ta::placeholder{color:var(–t3)}

/* ── OVERLAY / SHEET ── */
.ov{display:none;position:fixed;inset:0;background:rgba(0,0,0,.72);z-index:300;backdrop-filter:blur(4px);align-items:flex-end;justify-content:center}
.ov.on{display:flex}
.sh{width:100%;max-width:430px;background:#161b27;border-radius:22px 22px 0 0;border:1px solid var(–b);border-bottom:none;padding:14px 18px 38px;max-height:91dvh;overflow-y:auto}
.sh-h{width:34px;height:4px;background:var(–b2);border-radius:2px;margin:0 auto 16px}
.sh-t{font-weight:800;font-size:1rem;margin-bottom:16px}
.fg{margin-bottom:12px}
.inp{width:100%;background:var(–card);border:1.5px solid var(–b);border-radius:11px;padding:11px 13px;color:var(–t);font-family:‘Plus Jakarta Sans’,sans-serif;font-size:.84rem;outline:none;transition:border-color .2s;-webkit-appearance:none}
.inp:focus{border-color:var(–blue)}
.inp::placeholder{color:var(–t3)}
.row2{display:grid;grid-template-columns:1fr 1fr;gap:9px}
.sgrid{display:grid;grid-template-columns:repeat(3,1fr);gap:6px;margin-top:4px}
.so{border:1.5px solid var(–b);border-radius:9px;padding:8px 4px;text-align:center;font-size:.63rem;font-weight:700;cursor:pointer;color:var(–t3);font-family:‘Plus Jakarta Sans’,sans-serif;transition:all .15s}
.so.on{font-weight:800}
.so[data-v=new].on{border-color:var(–t2);color:var(–t2);background:rgba(136,146,176,.1)}
.so[data-v=contacted].on{border-color:var(–blue);color:var(–blue);background:rgba(79,142,247,.1)}
.so[data-v=pending].on{border-color:var(–orange);color:var(–orange);background:rgba(251,146,60,.1)}
.so[data-v=received].on{border-color:var(–green);color:var(–green);background:rgba(52,211,153,.1)}
.so[data-v=negotiating].on{border-color:var(–yellow);color:var(–yellow);background:rgba(251,191,36,.1)}
.so[data-v=closed].on{border-color:var(–green);color:var(–green);background:rgba(52,211,153,.15)}
.so[data-v=lost].on{border-color:var(–red);color:var(–red);background:rgba(248,113,113,.1)}

/* ── BUTTONS ── */
.btn{width:100%;margin-top:8px;background:linear-gradient(135deg,var(–blue),var(–purple));color:#fff;border:none;border-radius:13px;padding:14px;font-family:‘Plus Jakarta Sans’,sans-serif;font-weight:800;font-size:.88rem;cursor:pointer;transition:opacity .15s}
.btn:active{opacity:.8}
.btn-o{width:100%;margin-top:7px;background:none;color:var(–t3);border:1.5px solid var(–b);border-radius:13px;padding:12px;font-family:‘Plus Jakarta Sans’,sans-serif;font-size:.8rem;cursor:pointer}
.btn-g{width:100%;margin-top:8px;background:rgba(52,211,153,.12);color:var(–green);border:1.5px solid var(–green);border-radius:13px;padding:12px;font-family:‘Plus Jakarta Sans’,sans-serif;font-weight:700;font-size:.82rem;cursor:pointer}
.btn-g:active{opacity:.7}

/* ── IMPORT REVIEW CARDS ── */
.icard{background:var(–card);border:1.5px solid var(–b);border-radius:14px;padding:13px 14px;margin-bottom:9px}
.icard.skip{opacity:.35;border-style:dashed}
.icard-h{display:flex;align-items:center;justify-content:space-between;margin-bottom:9px;gap:8px}
.icard-n{font-weight:700;font-size:.86rem;flex:1;min-width:0;overflow:hidden;text-overflow:ellipsis;white-space:nowrap}
.itog{background:none;border:1.5px solid var(–b);border-radius:8px;padding:4px 9px;font-size:.62rem;font-weight:700;cursor:pointer;font-family:‘Plus Jakarta Sans’,sans-serif;color:var(–t3);white-space:nowrap;flex-shrink:0}
.itog.inc{border-color:var(–green);color:var(–green)}
.itog.exc{border-color:var(–red);color:var(–red)}
.irow{display:flex;gap:7px;margin-bottom:5px;align-items:center}
.ilbl{font-size:.6rem;color:var(–t3);text-transform:uppercase;letter-spacing:.04em;width:52px;flex-shrink:0}
.iinp{flex:1;background:#0f1117;border:1px solid var(–b);border-radius:7px;padding:6px 9px;color:var(–t);font-size:.75rem;font-family:‘Plus Jakarta Sans’,sans-serif;outline:none;min-width:0}
.iinp:focus{border-color:var(–blue)}

/* ── OPERACIONES ── */
.op-card{background:var(–card2);border:1px solid var(–b);border-radius:10px;padding:10px 12px;margin-bottom:7px;display:flex;align-items:center;gap:10px}
.op-div{font-size:.7rem;font-weight:800;padding:4px 9px;border-radius:8px;background:rgba(79,142,247,.15);color:var(–blue);flex-shrink:0;min-width:46px;text-align:center}
.op-info{flex:1;min-width:0}
.op-monto{font-size:.88rem;font-weight:800;color:var(–t)}
.op-meta{font-size:.65rem;color:var(–t3);margin-top:2px}
.op-del{background:none;border:none;color:var(–t3);font-size:.8rem;cursor:pointer;padding:4px;flex-shrink:0}
.op-del:active{color:var(–red)}
/* ── REPORT CARDS ── */
.rcard{background:var(–card);border:1.5px solid var(–b);border-radius:14px;padding:14px 16px;margin-bottom:10px}
.rcard-title{font-size:.65rem;font-weight:700;color:var(–t3);text-transform:uppercase;letter-spacing:.07em;margin-bottom:10px}
.rnum{font-size:1.6rem;font-weight:800;line-height:1}
.rsub{font-size:.68rem;color:var(–t3);margin-top:3px}
.rgrid{display:grid;grid-template-columns:1fr 1fr;gap:8px;margin-bottom:10px}
.rgrid3{display:grid;grid-template-columns:1fr 1fr 1fr;gap:8px;margin-bottom:10px}
.ritem{background:var(–card2);border-radius:10px;padding:10px 12px}
.rbar-wrap{margin-bottom:8px}
.rbar-label{display:flex;justify-content:space-between;font-size:.68rem;margin-bottom:4px}
.rbar-label span:first-child{color:var(–t2);overflow:hidden;text-overflow:ellipsis;white-space:nowrap;max-width:65%}
.rbar-label span:last-child{color:var(–t);font-weight:700;flex-shrink:0}
.rbar-track{height:6px;background:var(–b);border-radius:3px;overflow:hidden}
.rbar-fill{height:100%;border-radius:3px;background:linear-gradient(90deg,var(–blue),var(–purple));transition:width .4s}
/* ── DIVISA SELECTOR ── */
.so[data-d].on{border-color:var(–blue);color:var(–blue);background:rgba(79,142,247,.1)}

/* ── HEAT INDICATOR ── */
.heat{width:8px;height:8px;border-radius:50%;flex-shrink:0;margin-top:2px}
.heat-hot{background:#f87171;box-shadow:0 0 6px rgba(248,113,113,.7)}
.heat-warm{background:#fbbf24;box-shadow:0 0 6px rgba(251,191,36,.5)}
.heat-cold{background:#4a5470}

/* ── REMINDER BADGE ── */
.rem-badge{background:var(–orange);color:#000;font-size:.55rem;font-weight:800;padding:2px 6px;border-radius:20px;flex-shrink:0}
.rem-due{background:rgba(251,146,60,.12);border:1.5px solid rgba(251,146,60,.4);border-radius:10px;padding:8px 12px;margin-bottom:8px;display:flex;align-items:center;gap:8px;cursor:pointer}
.rem-due-label{font-size:.72rem;font-weight:600;color:var(–orange)}
.rem-due-sub{font-size:.65rem;color:var(–t3);margin-top:1px}

/* ── TODAY BANNER ── */
.today-banner{background:linear-gradient(135deg,rgba(251,146,60,.15),rgba(251,191,36,.1));border:1.5px solid rgba(251,146,60,.3);border-radius:12px;padding:10px 14px;margin-bottom:12px}
.today-title{font-size:.7rem;font-weight:700;color:var(–orange);margin-bottom:7px;display:flex;align-items:center;gap:6px}

/* ── LOG ENTRIES ── */
.log-entry{display:flex;gap:9px;padding:8px 0;border-bottom:1px solid var(–b)}
.log-entry:last-child{border-bottom:none}
.log-dot{width:8px;height:8px;border-radius:50%;background:var(–blue);flex-shrink:0;margin-top:5px}
.log-body{flex:1;min-width:0}
.log-txt{font-size:.76rem;color:var(–t);line-height:1.4}
.log-meta{font-size:.62rem;color:var(–t3);margin-top:2px}
.log-del{background:none;border:none;color:var(–t3);font-size:.75rem;cursor:pointer;flex-shrink:0;padding:2px 4px}

/* ── CONTACT TYPE CHIPS ── */
.ctype-grid{display:flex;gap:6px;flex-wrap:wrap;margin-top:4px}
.ct{padding:5px 11px;border-radius:20px;font-size:.67rem;font-weight:700;cursor:pointer;border:1.5px solid var(–b);color:var(–t3);background:none;transition:all .15s;font-family:inherit}
.ct.on{background:var(–blue);border-color:var(–blue);color:#fff}

/* ── TOAST ── */
.toast{position:fixed;bottom:84px;left:50%;transform:translateX(-50%) translateY(16px);background:var(–green);color:#000;font-weight:700;font-size:.76rem;padding:8px 18px;border-radius:20px;z-index:500;opacity:0;transition:all .28s;pointer-events:none;white-space:nowrap}
.toast.on{opacity:1;transform:translateX(-50%) translateY(0)}

/* ── SEC HEADER ── */
.sh2{font-size:.62rem;font-weight:700;color:var(–t3);text-transform:uppercase;letter-spacing:.09em;margin-bottom:9px;margin-top:2px}
</style>

</head>
<body>

<!-- ═══ PROSPECTOS ═══ -->

<div class="scr on" id="sP">
  <div class="tb">
    <div class="tb-row">
      <div class="logo">📋 MiProspecto</div>
      <div id="fecha" style="font-size:.62rem;color:var(--t3)"></div>
    </div>
    <div class="tabs" id="filtros"></div>
  </div>
  <div class="area">
    <div class="stats" id="stats"></div>
    <div class="srch"><span class="srch-ic">🔍</span><input id="buscar" placeholder="Buscar empresa, contacto..." type="search" autocomplete="off"></div>
    <div id="lista"></div>
  </div>
</div>

<!-- ═══ DESCUBRIR ═══ -->

<div class="scr" id="sD">
  <div class="tb">
    <div class="tb-row">
      <div class="logo">🏭 DENUE · INEGI</div>
      <div style="font-size:.62rem;color:var(--t3)">+5 millones de empresas MX</div>
    </div>
  </div>
  <div class="area">

```
<!-- BUSCADOR DENUE -->
<div style="background:linear-gradient(135deg,rgba(79,142,247,.1),rgba(52,211,153,.08));border:1.5px solid rgba(79,142,247,.25);border-radius:16px;padding:14px 16px;margin-bottom:14px">
  <div style="font-size:.72rem;font-weight:700;color:var(--blue2);margin-bottom:4px">🔎 Buscar en INEGI DENUE</div>
  <div style="font-size:.7rem;color:var(--t3);margin-bottom:10px">Datos reales de empresas registradas en México</div>
  <div style="display:flex;gap:7px;margin-bottom:8px">
    <div style="position:relative;flex:1">
      <input id="dInput" class="inp" placeholder="Giro o nombre ej: alimentos, automotriz..." type="text" style="padding-left:12px" onkeypress="if(event.key==='Enter')buscarDenue()">
    </div>
  </div>
  <div style="display:flex;gap:7px;margin-bottom:10px">
    <select id="dEstado" class="inp" style="flex:1;padding:10px 12px">
      <option value="14">Jalisco</option>
      <option value="01">Aguascalientes</option>
      <option value="02">Baja California</option>
      <option value="03">Baja California Sur</option>
      <option value="04">Campeche</option>
      <option value="05">Coahuila</option>
      <option value="06">Colima</option>
      <option value="07">Chiapas</option>
      <option value="08">Chihuahua</option>
      <option value="09">CDMX</option>
      <option value="10">Durango</option>
      <option value="11">Guanajuato</option>
      <option value="12">Guerrero</option>
      <option value="13">Hidalgo</option>
      <option value="15">Estado de México</option>
      <option value="16">Michoacán</option>
      <option value="17">Morelos</option>
      <option value="18">Nayarit</option>
      <option value="19">Nuevo León</option>
      <option value="20">Oaxaca</option>
      <option value="21">Puebla</option>
      <option value="22">Querétaro</option>
      <option value="23">Quintana Roo</option>
      <option value="24">San Luis Potosí</option>
      <option value="25">Sinaloa</option>
      <option value="26">Sonora</option>
      <option value="27">Tabasco</option>
      <option value="28">Tamaulipas</option>
      <option value="29">Tlaxcala</option>
      <option value="30">Veracruz</option>
      <option value="31">Yucatán</option>
      <option value="32">Zacatecas</option>
    </select>
    <button onclick="buscarDenue()" id="btnDenue" style="background:var(--blue);border:none;border-radius:10px;padding:10px 16px;color:#fff;font-weight:700;font-size:.8rem;cursor:pointer;font-family:'Plus Jakarta Sans',sans-serif;white-space:nowrap;transition:opacity .15s">Buscar</button>
  </div>
  <!-- Quick filters -->
  <div style="display:flex;gap:6px;overflow-x:auto;scrollbar-width:none;padding-bottom:2px" id="dQfiltros">
    <div class="chip" onclick="dQuick('manufactura')">Manufactura</div>
    <div class="chip" onclick="dQuick('alimentos')">Alimentos</div>
    <div class="chip" onclick="dQuick('automotriz')">Automotriz</div>
    <div class="chip" onclick="dQuick('quimica')">Química</div>
    <div class="chip" onclick="dQuick('textil')">Textil</div>
    <div class="chip" onclick="dQuick('plastico')">Plásticos</div>
    <div class="chip" onclick="dQuick('metal')">Metal</div>
    <div class="chip" onclick="dQuick('farmacia')">Farmacia</div>
  </div>
</div>

<!-- LOADING -->
<div id="dLoading" style="display:none;text-align:center;padding:20px;color:var(--t3);font-size:.78rem">
  <div style="width:22px;height:22px;border:2px solid rgba(79,142,247,.3);border-top-color:var(--blue);border-radius:50%;animation:spin .7s linear infinite;margin:0 auto 10px"></div>
  Consultando INEGI DENUE...
</div>

<!-- RESULTS -->
<div class="sh2" id="dTitulo" style="display:none"></div>
<div id="dLista"></div>

<!-- BASE INTERNA -->
<div class="sh2">Base interna</div>
<div class="srch" style="margin-bottom:10px"><span class="srch-ic">🔍</span><input id="dBuscar" placeholder="Buscar en base interna..." type="search" autocomplete="off"></div>
<div class="secs" id="sectores"></div>
<div id="dListaInterna"></div>
```

  </div>
</div>

<!-- ═══ IMPORTAR ═══ -->

<div class="scr" id="sI">
  <div class="tb">
    <div class="tb-row">
      <div class="logo">📩 Importar</div>
      <div style="font-size:.62rem;color:var(--t3)">Pega tu lista de correo</div>
    </div>
  </div>
  <div class="area">

```
<!-- RESPALDO -->
<div style="background:linear-gradient(135deg,rgba(52,211,153,.1),rgba(79,142,247,.08));border:1.5px solid rgba(52,211,153,.3);border-radius:14px;padding:14px 16px;margin-bottom:14px">
  <div style="font-size:.72rem;font-weight:700;color:var(--green);margin-bottom:10px">💾 Respaldo de datos</div>
  <div style="display:grid;grid-template-columns:1fr 1fr;gap:8px">
    <button class="btn-g" onclick="exportarRespaldo()" style="padding:11px 8px;font-size:.75rem">
      ⬇ Exportar respaldo
    </button>
    <label style="display:flex;align-items:center;justify-content:center;gap:6px;background:var(--card);border:1.5px solid var(--b);border-radius:10px;padding:11px 8px;font-size:.75rem;font-weight:700;color:var(--t2);cursor:pointer">
      ⬆ Importar respaldo
      <input type="file" id="fileRespaldo" accept=".json" onchange="importarRespaldo(this)" style="display:none">
    </label>
  </div>
  <div style="font-size:.65rem;color:var(--t3);margin-top:8px;line-height:1.5">
    Exporta un archivo .json con <b style="color:var(--t2)">todos tus datos</b> — prospectos, clientes, operaciones, contactos y recordatorios. Guárdalo en tu galería o Drive como respaldo.
  </div>
</div>

<div id="paso1">
  <div class="how">
    <div class="how-t">✨ ¿Cómo funciona?</div>
    <div class="how-b">
      1. Copia el texto de tu correo o lista<br>
      2. Pégalo aquí abajo<br>
      3. Toca "Extraer empresas"<br>
      4. Revisa y edita los datos<br>
      5. Toca "Agregar a prospectos"
    </div>
  </div>
  <div class="fg">
    <label class="lbl">Pega el texto aquí</label>
    <textarea class="ta" id="txtImport" placeholder="Funciona con cualquier formato. Ejemplos:
```

INGREDION MEXICO SA DE CV  3338849000
ALTA FIBRA SA DE CV  3310579112

— o correos completos con firma —

De: Juan García <juan@empresa.com>
Tel: 33 1234 5678
Empresa: Borda Industrial SA de CV”></textarea>
</div>
<button class="btn" id="btnExtraer" onclick="extraer()">🔍 Extraer empresas</button>
</div>

```
<div id="paso2" style="display:none">
  <div style="display:flex;align-items:center;justify-content:space-between;margin-bottom:12px">
    <div style="font-weight:700;font-size:.88rem" id="imp-titulo">Empresas detectadas</div>
    <button onclick="resetImport()" style="background:none;border:none;color:var(--t3);font-size:.72rem;cursor:pointer;font-family:'Plus Jakarta Sans',sans-serif">← Volver</button>
  </div>
  <div id="impCards"></div>
  <button class="btn-g" id="btnAgregar" onclick="agregarTodas()">✅ Agregar todas a prospectos</button>
  <button class="btn-o" onclick="resetImport()">Cancelar</button>
</div>
```

  </div>
</div>

<!-- ═══ CLIENTES ═══ -->

<div class="scr" id="sC">
  <div class="tb">
    <div class="tb-row">
      <div class="logo">🏆 Clientes</div>
      <div id="statsClientes" style="font-size:.62rem;color:var(--t3)"></div>
    </div>
  </div>
  <div class="area">
    <div class="srch"><span class="srch-ic">🔍</span><input id="buscarCliente" placeholder="Buscar cliente..." type="search" autocomplete="off"></div>
    <div id="listaClientes"></div>
  </div>
</div>

<!-- ═══ REPORTES ═══ -->

<div class="scr" id="sR">
  <div class="tb">
    <div class="tb-row">
      <div class="logo">📊 Reportes</div>
      <div style="font-size:.62rem;color:var(--t3)" id="rFecha"></div>
    </div>
    <div class="tabs">
      <div class="tab on" id="rtGeneral" onclick="setReporteTab('general')">General</div>
      <div class="tab" id="rtMensual" onclick="setReporteTab('mensual')">Por mes</div>
      <div class="tab" id="rtCliente" onclick="setReporteTab('cliente')">Por cliente</div>
    </div>
  </div>
  <div class="area" id="reporteArea"></div>
</div>

<!-- ═══ SHEET: NUEVA OPERACIÓN ═══ -->

<div class="ov" id="opOv" onclick="if(event.target===this)cerrarOp()">
  <div class="sh">
    <div class="sh-h"></div>
    <div class="sh-t" id="opTit">Nueva operación</div>
    <div class="fg">
      <label class="lbl">Fecha</label>
      <input class="inp" id="opFecha" type="date">
    </div>
    <div class="fg">
      <label class="lbl">Monto</label>
      <input class="inp" id="opMonto" type="number" placeholder="0.00" min="0" step="0.01">
    </div>
    <div class="fg">
      <label class="lbl">Divisa</label>
      <div style="display:grid;grid-template-columns:repeat(4,1fr);gap:7px;margin-top:4px" id="divisaGrid">
        <div class="so on" data-d="USD">🇺🇸 USD</div>
        <div class="so" data-d="EUR">🇪🇺 EUR</div>
        <div class="so" data-d="GBP">🇬🇧 GBP</div>
        <div class="so" data-d="CAD">🇨🇦 CAD</div>
      </div>
    </div>
    <div class="fg">
      <label class="lbl">Tipo de cambio (MXN)</label>
      <input class="inp" id="opTc" type="number" placeholder="Ej: 17.50" min="0" step="0.01">
    </div>
    <div class="fg">
      <label class="lbl">Notas de la operación</label>
      <input class="inp" id="opNotas" type="text" placeholder="Compra, venta, forward...">
    </div>
    <button class="btn" onclick="guardarOp()">Guardar operación</button>
    <button class="btn-o" onclick="cerrarOp()">Cancelar</button>
  </div>
</div>

<!-- ═══ FAB ═══ -->

<button class="fab" id="fab" onclick="abrirForm()">+</button>

<!-- ═══ NAV ═══ -->

<nav class="nav">
  <button class="nb on" id="nP" onclick="ir('P')"><span class="ni">📋</span>Prospectos <span id="remNavBadge" style="display:none;background:var(--orange);color:#000;font-size:.5rem;font-weight:800;padding:1px 5px;border-radius:10px;vertical-align:middle"></span></button>
  <button class="nb" id="nC" onclick="ir('C')"><span class="ni">🏆</span>Clientes</button>
  <button class="nb" id="nR" onclick="ir('R')"><span class="ni">📊</span>Reportes</button>
  <button class="nb" id="nD" onclick="ir('D')"><span class="ni">🔎</span>Descubrir</button>
  <button class="nb" id="nI" onclick="ir('I')"><span class="ni">📩</span>Importar</button>
</nav>

<!-- ═══ FORM OVERLAY ═══ -->

<div class="ov" id="formOv">
  <div class="sh">
    <div class="sh-h"></div>
    <div class="sh-t" id="formTit">Nuevo prospecto</div>
    <div class="fg"><label class="lbl">Empresa *</label><input class="inp" id="fE" placeholder="Nombre de la empresa" type="text"></div>
    <div class="row2">
      <div class="fg"><label class="lbl">Contacto</label><input class="inp" id="fC" placeholder="Nombre" type="text"></div>
      <div class="fg"><label class="lbl">Cargo</label><input class="inp" id="fCa" placeholder="Puesto" type="text"></div>
    </div>
    <div class="fg"><label class="lbl">Teléfono</label><input class="inp" id="fT" placeholder="+52 33 0000 0000" type="tel"></div>
    <div class="fg"><label class="lbl">Correo</label><input class="inp" id="fM" placeholder="correo@empresa.com" type="email"></div>
    <div class="fg"><label class="lbl">Página web</label><input class="inp" id="fW" placeholder="https://empresa.com" type="url"></div>
    <div class="fg"><label class="lbl">Sector</label><input class="inp" id="fS" placeholder="Manufactura, automotriz..." type="text"></div>
    <div class="fg">
      <label class="lbl">Estado</label>
      <div class="sgrid" id="sgrid">
        <div class="so on" data-v="new">🔘 Nuevo</div>
        <div class="so" data-v="contacted">📞 Contactado</div>
        <div class="so" data-v="pending">⏳ Esp.info</div>
        <div class="so" data-v="negotiating">🤝 Negociando</div>
        <div class="so" data-v="closed">🏆 Terminado</div>
        <div class="so" data-v="lost">❌ Perdido</div>
      </div>
    </div>
    <div class="fg" id="fUltOpGrp" style="display:none">
      <label class="lbl">Última operación</label>
      <input class="inp" id="fUltOp" type="date">
    </div>
    <div class="fg"><label class="lbl">Notas</label><textarea class="inp" id="fN" placeholder="Próximos pasos, detalles..." rows="3" style="resize:vertical;line-height:1.5"></textarea></div>
    <button class="btn" onclick="guardar()">Guardar prospecto</button>
    <button class="btn-o" onclick="cerrarForm()">Cancelar</button>
  </div>
</div>

<!-- ═══ SHEET: REGISTRO DE CONTACTO ═══ -->

<div class="ov" id="logOv" onclick="if(event.target===this)cerrarLog()">
  <div class="sh">
    <div class="sh-h"></div>
    <div class="sh-t" id="logTit">Registrar contacto</div>
    <div class="fg">
      <label class="lbl">Tipo de contacto</label>
      <div class="ctype-grid">
        <button class="ct on" data-ct="llamada">📞 Llamada</button>
        <button class="ct" data-ct="whatsapp">💬 WhatsApp</button>
        <button class="ct" data-ct="email">✉ Email</button>
        <button class="ct" data-ct="reunion">🤝 Reunión</button>
        <button class="ct" data-ct="otro">📝 Otro</button>
      </div>
    </div>
    <div class="fg">
      <label class="lbl">Resultado / Nota</label>
      <textarea class="inp" id="logNota" placeholder="Ej: Habló con el tesorero, interesado en forward a 30 días. Llamar el viernes..." rows="4" style="resize:vertical;line-height:1.5"></textarea>
    </div>
    <div class="fg">
      <label class="lbl">Fecha</label>
      <input class="inp" id="logFecha" type="date">
    </div>
    <button class="btn" onclick="guardarLog()">Guardar contacto</button>
    <button class="btn-o" onclick="cerrarLog()">Cancelar</button>
  </div>
</div>

<!-- ═══ SHEET: RECORDATORIO ═══ -->

<div class="ov" id="remOv" onclick="if(event.target===this)cerrarRem()">
  <div class="sh">
    <div class="sh-h"></div>
    <div class="sh-t" id="remTit">Agregar recordatorio</div>
    <div class="fg">
      <label class="lbl">¿Qué hay que hacer?</label>
      <input class="inp" id="remTexto" type="text" placeholder="Llamar, enviar propuesta, follow-up...">
    </div>
    <div class="fg">
      <label class="lbl">Fecha</label>
      <input class="inp" id="remFecha" type="date">
    </div>
    <div class="fg">
      <label class="lbl">Hora (opcional)</label>
      <input class="inp" id="remHora" type="time">
    </div>
    <div style="display:grid;grid-template-columns:1fr 1fr 1fr;gap:7px;margin-bottom:14px" id="remQuick">
      <button class="btn-o" onclick="setRemFecha(0)">Hoy</button>
      <button class="btn-o" onclick="setRemFecha(1)">Mañana</button>
      <button class="btn-o" onclick="setRemFecha(7)">En 7 días</button>
    </div>
    <button class="btn" onclick="guardarRem()">Guardar recordatorio</button>
    <button class="btn-o" onclick="cerrarRem()">Cancelar</button>
  </div>
</div>

<div class="toast" id="toast"></div>

<script>
"use strict";

// ═══════════════════════════════════════════
// CONSTANTES
// ═══════════════════════════════════════════
var KEY = 'mip_v3';

var ST = {
  new:         { l:'Nuevo',      c:'color:var(--t2)'    },
  contacted:   { l:'Contactado', c:'color:var(--blue)'  },
  pending:     { l:'Esp. info',  c:'color:var(--orange)'},
  negotiating: { l:'Negociando', c:'color:var(--yellow)'},
  closed:      { l:'Terminado',    c:'color:var(--green)' },
  lost:        { l:'Perdido',    c:'color:var(--red)'   }
};

var COLS = ['#4f8ef7','#34d399','#fb923c','#a78bfa','#f472b6','#38bdf8','#facc15'];

var SECS = ['Todos','Automotriz','Alimentos','Química','Acero/Metal','Electrónica','Embalaje','Textil','Construcción','Plásticos','Aeroespacial','Farmacéutica','Minería'];

var DB = [
  {n:'Vitro S.A.B. de C.V.',t:'81 8863 1200',w:'https://www.vitro.com',s:'Vidrio / Automotriz',c:'Monterrey, NL',tp:'Exportadora'},
  {n:'Nemak S.A.B. de C.V.',t:'81 8748 8000',w:'https://www.nemak.com',s:'Automotriz',c:'Monterrey, NL',tp:'Exportadora'},
  {n:'TREMEC S.A. de C.V.',t:'55 5726 4900',w:'https://www.tremec.com',s:'Transmisiones / Automotriz',c:'Querétaro, QRO',tp:'Exportadora'},
  {n:'Rassini S.A. de C.V.',t:'55 5280 0303',w:'https://www.rassini.com',s:'Fundición / Automotriz',c:'CDMX',tp:'Exportadora'},
  {n:'Bocar Group S.A. de C.V.',t:'55 5570 0100',w:'https://www.bocar.com.mx',s:'Autopartes',c:'CDMX',tp:'Exportadora'},
  {n:'GKN Driveline México',t:'44 2688 1000',w:'https://www.gknautomotive.com',s:'Autopartes / Automotriz',c:'Celaya, GTO',tp:'Exportadora'},
  {n:'Grupo Bimbo S.A.B. de C.V.',t:'55 5268 6600',w:'https://www.grupobimbo.com',s:'Alimentos / Panificación',c:'CDMX',tp:'Exportadora'},
  {n:'Gruma S.A.B. de C.V.',t:'81 8399 3300',w:'https://www.gruma.com',s:'Alimentos / Tortilla',c:'San Pedro, NL',tp:'Exportadora'},
  {n:'Lala Corporativo S.A. de C.V.',t:'71 8730 7300',w:'https://www.grupolala.com',s:'Lácteos / Alimentos',c:'Torreón, COAH',tp:'Exportadora'},
  {n:'Bachoco S.A.B. de C.V.',t:'74 5455 5333',w:'https://www.bachoco.com.mx',s:'Avicultura / Alimentos',c:'Celaya, GTO',tp:'Importadora'},
  {n:'Sigma Alimentos S.A. de C.V.',t:'81 8748 1111',w:'https://www.sigma-alimentos.com',s:'Alimentos procesados',c:'Monterrey, NL',tp:'Exportadora'},
  {n:'Grupo Idesa S.A. de C.V.',t:'55 5263 4040',w:'https://www.idesa.com',s:'Petroquímica / Química',c:'CDMX',tp:'Exportadora'},
  {n:'Mexichem S.A.B. de C.V.',t:'55 5279 8000',w:'https://www.mexichem.com',s:'Química / Cloro-Vinilo',c:'Tlalnepantla, EdoMex',tp:'Exportadora'},
  {n:'BASF Mexicana S.A. de C.V.',t:'55 5261 9700',w:'https://www.basf.com/mx',s:'Química',c:'Naucalpan, EdoMex',tp:'Importadora'},
  {n:'Bayer de México S.A. de C.V.',t:'55 5728 3000',w:'https://www.bayer.com.mx',s:'Química / Salud',c:'CDMX',tp:'Importadora'},
  {n:'Ternium México S.A. de C.V.',t:'81 8865 2500',w:'https://www.ternium.com.mx',s:'Acero/Metal',c:'Monterrey, NL',tp:'Exportadora'},
  {n:'Deacero S.A.P.I. de C.V.',t:'81 8888 7000',w:'https://www.deacero.com',s:'Acero/Metal / Alambre',c:'Monterrey, NL',tp:'Exportadora'},
  {n:'Condumex S.A. de C.V.',t:'55 5328 5600',w:'https://www.condumex.com.mx',s:'Cables / Acero/Metal',c:'CDMX',tp:'Exportadora'},
  {n:'Grupo Industrial Saltillo',t:'84 4411 1200',w:'https://www.gissab.com',s:'Metalmecánica / Acero/Metal',c:'Saltillo, COAH',tp:'Exportadora'},
  {n:'Flex México S.A. de C.V.',t:'66 4647 1400',w:'https://www.flex.com',s:'Electrónica / Manufactura',c:'Tijuana, BC',tp:'Exportadora'},
  {n:'Honeywell México S.A. de C.V.',t:'55 5259 1966',w:'https://www.honeywell.com/mx',s:'Electrónica industrial',c:'CDMX',tp:'Importadora'},
  {n:'Jabil Circuit de México',t:'66 4682 7000',w:'https://www.jabil.com',s:'Electrónica / Manufactura',c:'Guadalajara, JAL',tp:'Exportadora'},
  {n:'Sanmina México S.A. de C.V.',t:'66 4635 4800',w:'https://www.sanmina.com',s:'EMS / Electrónica',c:'Monterrey, NL',tp:'Exportadora'},
  {n:'Grupo Bio Pappel S.A.B.',t:'55 5227 4400',w:'https://www.biopappel.com',s:'Papel / Embalaje',c:'CDMX',tp:'Exportadora'},
  {n:'Smurfit Kappa México',t:'55 5278 7700',w:'https://www.smurfitkappa.com.mx',s:'Papel / Embalaje',c:'CDMX',tp:'Importadora'},
  {n:'Sealed Air de México',t:'55 5846 7200',w:'https://www.sealedair.com',s:'Empaques / Embalaje',c:'Naucalpan, EdoMex',tp:'Importadora'},
  {n:'Kaltex Group S.A. de C.V.',t:'55 5729 3000',w:'https://www.kaltex.com',s:'Textil / Confección',c:'CDMX',tp:'Exportadora'},
  {n:'Cemex S.A.B. de C.V.',t:'81 8888 8888',w:'https://www.cemex.com',s:'Cemento / Construcción',c:'Monterrey, NL',tp:'Exportadora'},
  {n:'Grupo Cementos de Chihuahua',t:'61 4432 2000',w:'https://www.gcc.com',s:'Cemento / Construcción',c:'Chihuahua, CHIH',tp:'Exportadora'},
  {n:'Grupo Lamosa S.A.B.',t:'81 8159 5200',w:'https://www.lamosa.com',s:'Cerámica / Construcción',c:'Monterrey, NL',tp:'Exportadora'},
  {n:'Alpla México S.A. de C.V.',t:'55 5386 1500',w:'https://www.alpla.com',s:'Plásticos / Envases',c:'Estado de México',tp:'Importadora'},
  {n:'Plastipak México S.A.',t:'81 8375 2000',w:'https://www.plastipak.com',s:'Plásticos / Envases PET',c:'Monterrey, NL',tp:'Importadora'},
  {n:'Honeywell Aerospace México',t:'66 4648 5000',w:'https://aerospace.honeywell.com',s:'Aeroespacial',c:'Mexicali, BC',tp:'Exportadora'},
  {n:'Safran México S.A. de C.V.',t:'44 2688 2200',w:'https://www.safran-group.com',s:'Aeroespacial',c:'Querétaro, QRO',tp:'Exportadora'},
  {n:'Bombardier Aerospace México',t:'33 3770 1000',w:'https://www.bombardier.com',s:'Aeroespacial',c:'Querétaro, QRO',tp:'Exportadora'},
  {n:'Laboratorios Pisa S.A.',t:'33 3669 6600',w:'https://www.pisa.com.mx',s:'Farmacéutica',c:'Guadalajara, JAL',tp:'Exportadora'},
  {n:'Asofarma S.A. de C.V.',t:'55 5260 5800',w:'https://www.asofarma.com.mx',s:'Farmacéutica',c:'CDMX',tp:'Importadora'},
  {n:'Grupo México S.A.B.',t:'55 1103 5000',w:'https://www.gmexico.com',s:'Minería / Cobre',c:'CDMX',tp:'Exportadora'},
  {n:'Industrias Peñoles S.A.B.',t:'55 5279 3000',w:'https://www.penoles.com.mx',s:'Minería / Metales',c:'CDMX',tp:'Exportadora'},
  {n:'Industrias Pirelli México',t:'55 5322 3000',w:'https://www.pirelli.com/mx',s:'Hule / Automotriz',c:'Guanajuato',tp:'Exportadora'}
];

// ═══════════════════════════════════════════
// STATE
// ═══════════════════════════════════════════
var prospectos = [];
var editId = null;
var filtroActivo = 'all';
var busqueda = '';
var statusSel = 'new';
var sectorActivo = 'Todos';
var dBusqueda = '';
var impItems = [];
var dbAgregados = {};

// ═══════════════════════════════════════════
// STORAGE
// ═══════════════════════════════════════════
function deduplicar() {
  var vistos = {};
  var antes = prospectos.length;
  prospectos = prospectos.filter(function(p) {
    // Normalize: uppercase, remove spaces and common suffixes for comparison
    var clave = p.empresa
      .toUpperCase()
      .replace(/\s+/g, ' ')
      .trim()
      .replace(/\bS\.?A\.?\s*(P\.?I\.?)?\s*(DE\s+C\.?V\.?)?\b/gi, '')
      .replace(/\bS\.?R\.?L\.?\s*(DE\s+C\.?V\.?)?\b/gi, '')
      .replace(/\bDE\s+C\.?V\.?\b/gi, '')
      .replace(/\s+/g, '')
      .trim();
    if (vistos[clave]) return false;
    vistos[clave] = true;
    return true;
  });
  var eliminados = antes - prospectos.length;
  if (eliminados > 0) {
    guardarDB();
    console.log('Deduplicados: ' + eliminados + ' duplicados eliminados');
  }
  return eliminados;
}

function cargar() {
  try { prospectos = JSON.parse(localStorage.getItem(KEY)) || []; }
  catch(e) { prospectos = []; }
  deduplicar();
}
function guardarDB() { localStorage.setItem(KEY, JSON.stringify(prospectos)); }

function yaExiste(nombre) {
  var clave = nombre.toUpperCase().replace(/\s+/g,' ').trim()
    .replace(/\bS\.?A\.?\s*(P\.?I\.?)?\s*(DE\s+C\.?V\.?)?\b/gi,'')
    .replace(/\bS\.?R\.?L\.?\s*(DE\s+C\.?V\.?)?\b/gi,'')
    .replace(/\bDE\s+C\.?V\.?\b/gi,'')
    .replace(/\s+/g,'').trim();
  return prospectos.some(function(p){
    var c2 = p.empresa.toUpperCase().replace(/\s+/g,' ').trim()
      .replace(/\bS\.?A\.?\s*(P\.?I\.?)?\s*(DE\s+C\.?V\.?)?\b/gi,'')
      .replace(/\bS\.?R\.?L\.?\s*(DE\s+C\.?V\.?)?\b/gi,'')
      .replace(/\bDE\s+C\.?V\.?\b/gi,'')
      .replace(/\s+/g,'').trim();
    return c2 === clave;
  });
}


// ═══════════════════════════════════════════
// HELPERS
// ═══════════════════════════════════════════
function uid() { return Date.now().toString(36) + Math.random().toString(36).slice(2); }

function esc(s) {
  return String(s || '').replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;').replace(/"/g,'&quot;');
}

function initials(n) {
  var parts = String(n || '').split(' ');
  var r = '';
  for (var i = 0; i < Math.min(2, parts.length); i++) {
    if (parts[i]) r += parts[i][0];
  }
  return r.toUpperCase() || '?';
}

function color(n) {
  var h = 0;
  var s = String(n || '');
  for (var i = 0; i < s.length; i++) h = (h * 31 + s.charCodeAt(i)) & 0xffff;
  return COLS[h % COLS.length];
}

function toast(msg, bg) {
  var t = document.getElementById('toast');
  t.textContent = msg;
  t.style.background = bg || 'var(--green)';
  t.style.color = (bg === 'var(--red)' || bg === 'var(--orange)') ? '#fff' : '#000';
  t.classList.add('on');
  setTimeout(function() { t.classList.remove('on'); }, 2400);
}

function sp(e) { if(e) e.stopPropagation(); }

// ═══════════════════════════════════════════
// NAVIGATION
// ═══════════════════════════════════════════
function ir(s) {
  document.querySelectorAll('.scr').forEach(function(el) { el.classList.remove('on'); });
  document.querySelectorAll('.nb').forEach(function(el) { el.classList.remove('on'); });
  document.getElementById('s' + s).classList.add('on');
  document.getElementById('n' + s).classList.add('on');
  document.getElementById('fab').style.display = s === 'P' ? 'flex' : 'none';
  if (s === 'C') renderClientes();
  if (s === 'R') renderReporte();
}

// ═══════════════════════════════════════════
// RENDER PROSPECTOS
// ═══════════════════════════════════════════
function filtrados() {
  return prospectos.filter(function(p) {
    if (p.status === 'closed') return false; // clients go to Clientes tab
    var mf = filtroActivo === 'all' || p.status === filtroActivo;
    var q = busqueda.toLowerCase();
    var ms = !q || [p.empresa, p.contacto, p.email, p.sector, p.tel].some(function(f) {
      return f && f.toLowerCase().indexOf(q) >= 0;
    });
    return mf && ms;
  }).sort(function(a,b){return a.empresa.localeCompare(b.empresa,'es',{sensitivity:'base'});});
}

function renderStats() {
  var prosp = prospectos.filter(function(p) { return p.status !== 'closed'; });
  var clientes = prospectos.filter(function(p) { return p.status === 'closed'; }).length;
  var pend = prosp.filter(function(p) { return p.status === 'pending'; }).length;
  var rems = recordatorios.filter(function(r) { return !r.done && r.fecha <= hoy(); }).length;
  document.getElementById('stats').innerHTML =
    '<div class="st"><div class="st-n">' + prosp.length + '</div><div class="st-l">Prospectos</div></div>' +
    '<div class="st"><div class="st-n" style="color:var(--green)">' + clientes + '</div><div class="st-l">Clientes</div></div>' +
    '<div class="st"><div class="st-n" style="color:var(--orange)">' + pend + '</div><div class="st-l">Esp. info</div></div>' +
    '<div class="st"><div class="st-n" style="color:' + (rems?'var(--orange)':'var(--t3)') + '">' + rems + '</div><div class="st-l">⏰ Hoy</div></div>';
}

function renderFiltros() {
  var html = '<div class="tab ' + (filtroActivo === 'all' ? 'on' : '') + '" onclick="setFiltro(\'all\')">Todos</div>';
  var keys = Object.keys(ST);
  for (var i = 0; i < keys.length; i++) {
    var k = keys[i];
    if (k === 'closed') continue; // skip — clients have their own tab
    var cnt = prospectos.filter(function(p) { return p.status === k; }).length;
    html += '<div class="tab ' + (filtroActivo === k ? 'on' : '') + '" onclick="setFiltro(\'' + k + '\')">' + ST[k].l + (cnt > 0 ? ' ' + cnt : '') + '</div>';
  }
  document.getElementById('filtros').innerHTML = html;
}

function setFiltro(f) { filtroActivo = f; renderLista(); }

function renderLista() {
  renderStats();
  renderFiltros();
  var data = filtrados();
  var el = document.getElementById('lista');
  var today = hoy();

  // TODAY BANNER — reminders due today or overdue
  var pendientes = recordatorios.filter(function(r) { return !r.done && r.fecha <= today; });
  var bannerHtml = '';
  if (pendientes.length) {
    bannerHtml += '<div class="today-banner">';
    bannerHtml += '<div class="today-title">⏰ ' + pendientes.length + ' recordatorio' + (pendientes.length !== 1 ? 's' : '') + ' pendiente' + (pendientes.length !== 1 ? 's' : '') + '</div>';
    pendientes.slice(0, 3).forEach(function(r) {
      var p = buscarProspecto(r.prospectoId);
      bannerHtml += '<div class="rem-due" onclick="toggle(\'' + r.prospectoId + '\')">';
      bannerHtml += '<div style="flex:1"><div class="rem-due-label">' + esc(r.texto) + '</div>';
      bannerHtml += '<div class="rem-due-sub">' + (p ? esc(p.empresa) : '') + (r.fecha < today ? ' · <span style="color:var(--red)">Vencido ' + fmtFecha(r.fecha) + '</span>' : ' · Hoy' + (r.hora ? ' ' + r.hora : '')) + '</div></div>';
      bannerHtml += '<button onclick="sp(event);completarRem(\'' + r.id + '\')" style="background:var(--green);border:none;border-radius:8px;padding:5px 10px;color:#000;font-size:.65rem;font-weight:700;cursor:pointer;font-family:inherit;flex-shrink:0">✓ Listo</button>';
      bannerHtml += '</div>';
    });
    bannerHtml += '</div>';
  }

  if (!data.length) {
    el.innerHTML = bannerHtml + '<div class="empty"><div class="empty-i">' + (busqueda ? '🔍' : '🏢') + '</div>' +
      '<div class="empty-t">' + (busqueda ? 'Sin resultados' : 'Sin prospectos') + '</div>' +
      '<div class="empty-s">' + (busqueda ? 'Intenta otro término' : 'Toca + para agregar o ve a Descubrir') + '</div></div>';
    return;
  }

  var html = bannerHtml;
  for (var i = 0; i < data.length; i++) {
    var p = data[i];
    var cl = color(p.empresa);
    var st = ST[p.status] || ST.new;
    var sub = p.contacto ? esc(p.contacto) + (p.cargo ? ' · ' + esc(p.cargo) : '') : (p.sector ? esc(p.sector) : '');

    // Heat level
    var heat = heatLevel(p);
    var heatClass = heat === 'hot' ? 'heat-hot' : heat === 'warm' ? 'heat-warm' : 'heat-cold';
    var heatTitle = heat === 'hot' ? 'Contactado recientemente' : heat === 'warm' ? 'Contactado hace 1-3 semanas' : 'Sin contacto reciente';

    // Pending reminders for this prospect
    var myRems = recordatorios.filter(function(r) { return r.prospectoId === p.id && !r.done; });
    var overdueRems = myRems.filter(function(r) { return r.fecha <= today; }).length;

    // Contact log for this prospect
    var myLogs = contactos.filter(function(c) { return c.prospectoId === p.id; });

    html += '<div class="pc" id="pc-' + p.id + '" onclick="toggle(\'' + p.id + '\')">';
    html += '<div class="pc-h">';
    html += '<div class="av" style="background:' + cl + '22;color:' + cl + ';border:2px solid ' + cl + '44">' + initials(p.empresa) + '</div>';
    html += '<div class="pi"><div class="pn">' + esc(p.empresa) + '</div><div class="ps">' + sub + '</div></div>';
    html += '<div class="pr">';
    html += '<div style="display:flex;align-items:center;gap:5px">';
    html += '<span class="badge" style="' + st.c + '">' + st.l + '</span>';
    if (overdueRems) html += '<span class="rem-badge">⏰' + overdueRems + '</span>';
    html += '</div>';
    html += '<div style="display:flex;align-items:center;gap:5px;margin-top:3px">';
    html += '<div class="heat ' + heatClass + '" title="' + heatTitle + '"></div>';
    if (myLogs.length) html += '<span style="font-size:.58rem;color:var(--t3)">' + myLogs.length + ' contacto' + (myLogs.length!==1?'s':'') + '</span>';
    html += '</div>';
    html += '</div>';
    html += '<span class="chv" style="margin-left:4px">▾</span>';
    html += '</div>';

    // BODY
    html += '<div class="pc-b">';
    html += '<div class="dg">';
    if (p.tel) html += '<div class="dr"><span class="dl">Tel</span><span class="dv"><a href="tel:' + esc(p.tel) + '">' + esc(p.tel) + '</a></span></div>';
    if (p.email) html += '<div class="dr"><span class="dl">Email</span><span class="dv"><a href="mailto:' + esc(p.email) + '">' + esc(p.email) + '</a></span></div>';
    if (p.web) html += '<div class="dr"><span class="dl">Web</span><span class="dv"><a href="' + esc(p.web) + '" target="_blank">' + esc(p.web.replace(/https?:\/\//, '')) + '</a></span></div>';
    if (p.sector) html += '<div class="dr"><span class="dl">Sector</span><span class="dv">' + esc(p.sector) + '</span></div>';
    if (p.notas) html += '<div class="notebox">' + esc(p.notas) + '</div>';
    html += '</div>';

    // REMINDERS for this prospect
    if (myRems.length) {
      html += '<div style="margin-top:10px;padding-top:9px;border-top:1px solid var(--b)">';
      html += '<div style="font-size:.62rem;font-weight:700;color:var(--t3);text-transform:uppercase;letter-spacing:.06em;margin-bottom:6px">⏰ Recordatorios</div>';
      myRems.forEach(function(r) {
        var isOver = r.fecha < today;
        html += '<div style="display:flex;align-items:center;gap:8px;padding:5px 0;border-bottom:1px solid var(--b)">';
        html += '<div style="flex:1"><div style="font-size:.74rem;color:' + (isOver?'var(--red)':'var(--t)') + '">' + esc(r.texto) + '</div>';
        html += '<div style="font-size:.62rem;color:var(--t3)">' + fmtFecha(r.fecha) + (r.hora?' '+r.hora:'') + (isOver?' · <span style="color:var(--red);font-weight:700">VENCIDO</span>':'') + '</div></div>';
        html += '<button onclick="sp(event);completarRem(\'' + r.id + '\')" style="background:rgba(52,211,153,.15);border:1px solid var(--green);border-radius:7px;padding:4px 9px;color:var(--green);font-size:.65rem;font-weight:700;cursor:pointer;font-family:inherit">✓</button>';
        html += '<button onclick="sp(event);borrarRem(\'' + r.id + '\')" style="background:none;border:none;color:var(--t3);font-size:.75rem;cursor:pointer;padding:2px 4px">✕</button>';
        html += '</div>';
      });
      html += '</div>';
    }

    // CONTACT LOG for this prospect
    if (myLogs.length) {
      html += '<div style="margin-top:10px;padding-top:9px;border-top:1px solid var(--b)">';
      html += '<div style="font-size:.62rem;font-weight:700;color:var(--t3);text-transform:uppercase;letter-spacing:.06em;margin-bottom:6px">📋 Historial de contactos</div>';
      myLogs.slice(0, 4).forEach(function(c) {
        html += '<div class="log-entry">';
        html += '<div class="log-dot" style="background:' + (c.tipo==='llamada'?'var(--blue)':c.tipo==='reunion'?'var(--green)':c.tipo==='whatsapp'?'#25d366':'var(--purple)') + '"></div>';
        html += '<div class="log-body"><div class="log-txt">' + (TIPO_ICON[c.tipo]||'📝') + ' ' + esc(c.nota) + '</div>';
        html += '<div class="log-meta">' + fmtFecha(c.fecha) + '</div></div>';
        html += '<button class="log-del" onclick="sp(event);borrarLog(\'' + c.id + '\')">✕</button>';
        html += '</div>';
      });
      if (myLogs.length > 4) html += '<div style="font-size:.63rem;color:var(--t3);text-align:right;padding-top:4px">+' + (myLogs.length-4) + ' más</div>';
      html += '</div>';
    }

    // Status quick change
    html += '<div class="ss">';
    var ks = Object.keys(ST);
    for (var j = 0; j < ks.length; j++) {
      var k = ks[j];
      html += '<button class="sb ' + (p.status===k?'on':'') + '" style="' + ST[k].c + '" onclick="qSt(event,\'' + p.id + '\',\'' + k + '\')">' + ST[k].l + '</button>';
    }
    html += '</div>';

    // Actions
    html += '<div class="acts">';
    if (p.tel) html += '<button class="ac call" onclick="sp(event);location.href=\'tel:' + esc(p.tel) + '\'">📞 Llamar</button>';
    html += '<button class="ac" style="border-color:var(--purple);color:var(--purple)" onclick="sp(event);abrirLog(\'' + p.id + '\')">📋 Contacto</button>';
    html += '<button class="ac" style="border-color:var(--orange);color:var(--orange)" onclick="sp(event);abrirRem(\'' + p.id + '\')">⏰ Recordar</button>';
    html += '<button class="ac edit" onclick="sp(event);editarCard(\'' + p.id + '\')">✏ Editar</button>';
    html += '<button class="ac del" onclick="sp(event);borrar(\'' + p.id + '\')">✕</button>';
    html += '</div></div></div>';
  }
  el.innerHTML = html;
}

function toggle(id) {
  var el = document.getElementById('pc-' + id);
  if (el) el.classList.toggle('open');
}

function qSt(e, id, status) {
  sp(e);
  for (var i = 0; i < prospectos.length; i++) {
    if (prospectos[i].id === id) { prospectos[i].status = status; break; }
  }
  guardarDB(); renderLista();
  if (status === 'closed') renderClientes();
  toast('Estado: ' + ST[status].l);
}

function borrar(id) {
  if (!confirm('¿Eliminar este prospecto?')) return;
  prospectos = prospectos.filter(function(p) { return p.id !== id; });
  guardarDB(); renderLista();
  toast('Eliminado', 'var(--red)');
}

// ═══════════════════════════════════════════
// FORM
// ═══════════════════════════════════════════
function abrirForm(pre) {
  editId = null; statusSel = 'new';
  document.getElementById('formTit').textContent = 'Nuevo prospecto';
  var ids = ['fE','fC','fCa','fT','fM','fW','fS','fN','fUltOp'];
  for (var i = 0; i < ids.length; i++) document.getElementById(ids[i]).value = '';
  if (pre) {
    if (pre.e) document.getElementById('fE').value = pre.e;
    if (pre.t) document.getElementById('fT').value = pre.t;
    if (pre.m) document.getElementById('fM').value = pre.m;
    if (pre.w) document.getElementById('fW').value = pre.w;
    if (pre.s) document.getElementById('fS').value = pre.s;
    if (pre.n) document.getElementById('fN').value = pre.n;
  }
  marcarStatus('new');
  document.getElementById('formOv').classList.add('on');
  setTimeout(function() { document.getElementById('fE').focus(); }, 300);
}

function cerrarForm() { document.getElementById('formOv').classList.remove('on'); }

function editarCard(id) {
  var p = null;
  for (var i = 0; i < prospectos.length; i++) { if (prospectos[i].id === id) { p = prospectos[i]; break; } }
  if (!p) return;
  editId = id; statusSel = p.status || 'new';
  document.getElementById('formTit').textContent = 'Editar';
  document.getElementById('fE').value = p.empresa || '';
  document.getElementById('fC').value = p.contacto || '';
  document.getElementById('fCa').value = p.cargo || '';
  document.getElementById('fT').value = p.tel || '';
  document.getElementById('fM').value = p.email || '';
  document.getElementById('fW').value = p.web || '';
  document.getElementById('fS').value = p.sector || '';
  document.getElementById('fN').value = p.notas || '';
  document.getElementById('fUltOp').value = p.ultOp || '';
  marcarStatus(statusSel);
  document.getElementById('formOv').classList.add('on');
}

function marcarStatus(v) {
  statusSel = v;
  document.querySelectorAll('.so').forEach(function(el) {
    el.classList.toggle('on', el.getAttribute('data-v') === v);
  });
  // Show/hide last operation date field
  document.getElementById('fUltOpGrp').style.display = v === 'closed' ? 'block' : 'none';
}

function guardar() {
  var emp = document.getElementById('fE').value.trim();
  if (!emp) { toast('Ingresa el nombre de la empresa', 'var(--orange)'); document.getElementById('fE').focus(); return; }
  var data = {
    id: editId || uid(),
    empresa: emp,
    contacto: document.getElementById('fC').value.trim(),
    cargo: document.getElementById('fCa').value.trim(),
    tel: document.getElementById('fT').value.trim(),
    email: document.getElementById('fM').value.trim(),
    web: document.getElementById('fW').value.trim(),
    sector: document.getElementById('fS').value.trim(),
    notas: document.getElementById('fN').value.trim(),
    ultOp: document.getElementById('fUltOp').value || '',
    status: statusSel,
    ts: editId ? (function() { for(var i=0;i<prospectos.length;i++) if(prospectos[i].id===editId) return prospectos[i].ts; return Date.now(); })() : Date.now()
  };
  if (editId) {
    for (var i = 0; i < prospectos.length; i++) { if (prospectos[i].id === editId) { prospectos[i] = data; break; } }
  } else {
    prospectos.unshift(data);
  }
  guardarDB(); renderLista();
  if (statusSel === 'closed') { renderClientes(); renderReporte(); }
  cerrarForm();
  toast(editId ? '✅ Guardado' : '✅ Prospecto agregado');
}

// status grid clicks
document.querySelectorAll('.so').forEach(function(el) {
  el.addEventListener('click', function() {
    marcarStatus(el.getAttribute('data-v'));
  });
});

// close overlay on backdrop click
document.getElementById('formOv').addEventListener('click', function(e) {
  if (e.target === this) cerrarForm();
});

// ═══════════════════════════════════════════
// DENUE · INEGI
// ═══════════════════════════════════════════
var DENUE_TOKEN = 'a0c16e50-32c9-44ca-bc45-3e3b7c580bbd';
var denuePage = 1;
var denueBusq = '';
var denueEst = '14';

function dQuick(q) {
  document.getElementById('dInput').value = q;
  buscarDenue();
}

function buscarDenue() {
  denueBusq = document.getElementById('dInput').value.trim() || 'manufactura';
  denueEst = document.getElementById('dEstado').value;
  denuePage = 1;
  document.getElementById('dLoading').style.display = 'block';
  document.getElementById('dLista').innerHTML = '';
  document.getElementById('dTitulo').style.display = 'none';
  document.getElementById('btnDenue').disabled = true;

  var url = 'https://www.inegi.org.mx/app/api/denue/v1/consulta/buscarEntidad/'
    + encodeURIComponent(denueBusq) + '/' + denueEst + '/1/20/' + DENUE_TOKEN;

  fetch(url)
    .then(function(r) { return r.json(); })
    .then(function(data) {
      document.getElementById('dLoading').style.display = 'none';
      document.getElementById('btnDenue').disabled = false;
      if (!data || !data.length) {
        document.getElementById('dTitulo').style.display = 'block';
        document.getElementById('dTitulo').textContent = '0 resultados en INEGI';
        document.getElementById('dLista').innerHTML = '<div class="empty"><div class="empty-i">🔍</div><div class="empty-t">Sin resultados</div><div class="empty-s">Intenta con otro término o estado</div></div>';
        return;
      }
      renderDenueResults(data);
    })
    .catch(function(err) {
      document.getElementById('dLoading').style.display = 'none';
      document.getElementById('btnDenue').disabled = false;
      document.getElementById('dTitulo').style.display = 'block';
      document.getElementById('dTitulo').textContent = 'Error de conexión';
      document.getElementById('dLista').innerHTML = '<div class="empty"><div class="empty-i">⚠️</div><div class="empty-t">Sin conexión</div><div class="empty-s">Verifica tu internet e intenta de nuevo</div></div>';
    });
}

function renderDenueResults(data) {
  // DENUE returns array of arrays: [id, nombre, razonSocial, actividad, personal, tipVial, nomVial, numExt, numInt, colonia, asentamiento, cp, entMunLoc, tel, email, web, tipo, lat, lon, ...]
  document.getElementById('dTitulo').style.display = 'block';
  document.getElementById('dTitulo').textContent = data.length + ' empresa' + (data.length !== 1 ? 's' : '') + ' en INEGI';
  var html = '';
  for (var i = 0; i < data.length; i++) {
    var r = data[i];
    // Field positions per DENUE API spec
    var nombre  = (r[1] || r[2] || '').trim();
    var act     = (r[3] || '').trim();
    var tel     = (r[13] || '').trim();
    var email   = (r[14] || '').trim();
    var web     = (r[15] || '').trim();
    var cp      = (r[11] || '').trim();
    var entidad = (r[12] || '').trim(); // "ENT,MUN,LOC"
    var ciudad  = entidad.split(',')[0] || '';

    if (!nombre) continue;
    // Clean name — remove razón social suffixes
    var nombreLimpio = nombre
      .replace(/\bS\.?A\.?\s*P\.?I\.?\s*(DE\s+C\.?V\.?)?\b/gi, '')
      .replace(/\bS\.?A\.?\s*(DE\s+C\.?V\.?)?\b/gi, '')
      .replace(/\bS\.?R\.?L\.?\s*(DE\s+C\.?V\.?)?\b/gi, '')
      .replace(/\bDE\s+C\.?V\.?\b/gi, '')
      .replace(/\s{2,}/g, ' ').trim();

    var did = 'dn_' + i + '_' + r[0];
    var existe = prospectos.some(function(p) { return p.empresa === nombreLimpio; });
    var webFmt = web && !web.match(/^https?:\/\//) ? 'https://' + web : web;

    html += '<div class="tile">';
    html += '<div class="ti">';
    html += '<div class="tn">' + esc(nombreLimpio) + '</div>';
    html += '<div class="tm">' + esc(act) + (ciudad ? ' · ' + esc(ciudad) : '') + '</div>';
    if (tel) html += '<div class="tm">📞 ' + esc(tel) + '</div>';
    html += '</div>';
    html += '<div class="add ' + (existe ? 'done' : '') + '" id="' + did + '" onclick="addDenue(this,\'' + esc(nombreLimpio) + '\',\'' + esc(tel) + '\',\'' + esc(email) + '\',\'' + esc(webFmt) + '\',\'' + esc(act) + '\',\'' + esc(ciudad) + '\')">' + (existe ? '✓' : '+') + '</div>';
    html += '</div>';
  }
  document.getElementById('dLista').innerHTML = html || '<div class="empty"><div class="empty-i">🔍</div><div class="empty-t">Sin resultados</div></div>';
}

function addDenue(btn, nombre, tel, email, web, sector, ciudad) {
  if (btn.classList.contains('done')) return;
  if (yaExiste(nombre)) { toast(nombre + ' ya está en prospectos', 'var(--orange)'); btn.textContent='✓'; btn.classList.add('done'); return; }
  prospectos.unshift({ id:uid(), empresa:nombre, contacto:'', cargo:'', tel:tel, email:email, web:web, sector:sector, notas: ciudad ? 'Ciudad: '+ciudad : '', status:'new', ts:Date.now() });
  guardarDB();
  renderLista();
  btn.textContent = '✓';
  btn.classList.add('done');
  toast('✅ ' + nombre + ' agregada');
}

// ═══════════════════════════════════════════
// DESCUBRIR (base interna)
// ═══════════════════════════════════════════
function renderSectors() {
  var html = '';
  for (var i = 0; i < SECS.length; i++) {
    html += '<div class="tab ' + (SECS[i] === sectorActivo ? 'on' : '') + '" onclick="setSector(\'' + SECS[i] + '\')">' + SECS[i] + '</div>';
  }
  document.getElementById('sectores').innerHTML = html;
}

function setSector(s) { sectorActivo = s; renderDescubrir(); }

function renderDescubrir() {
  renderSectors();
  var data = DB.filter(function(c) {
    var ms = sectorActivo === 'Todos' || c.s.toLowerCase().indexOf(sectorActivo.toLowerCase()) >= 0;
    var q = dBusqueda.toLowerCase();
    var mq = !q || c.n.toLowerCase().indexOf(q) >= 0 || c.s.toLowerCase().indexOf(q) >= 0 || c.c.toLowerCase().indexOf(q) >= 0;
    return ms && mq;
  });
  var listaEl = document.getElementById('dListaInterna');
  if (!data.length) {
    listaEl.innerHTML = '<div class="empty"><div class="empty-i">🔍</div><div class="empty-t">Sin resultados</div><div class="empty-s">Prueba otro sector o búsqueda</div></div>';
    return;
  }
  var html = '';
  for (var i = 0; i < data.length; i++) {
    var c = data[i];
    var aid = 'db_' + c.n.replace(/[^a-zA-Z0-9]/g, '_');
    var existe = prospectos.some(function(p) { return p.empresa === c.n; }) || dbAgregados[aid];
    html += '<div class="tile">';
    html += '<div class="ti"><div class="tn">' + esc(c.n) + '</div>';
    html += '<div class="tm">📍 ' + esc(c.c) + ' · ' + esc(c.s) + '</div>';
    html += '<span class="tt">' + esc(c.tp) + '</span></div>';
    html += '<div class="add ' + (existe ? 'done' : '') + '" id="' + aid + '" onclick="addDB(\'' + aid + '\')">' + (existe ? '✓' : '+') + '</div>';
    html += '</div>';
  }
  listaEl.innerHTML = html;
}


function addDB(aid) {
  var c = null;
  for (var i = 0; i < DB.length; i++) {
    if ('db_' + DB[i].n.replace(/[^a-zA-Z0-9]/g, '_') === aid) { c = DB[i]; break; }
  }
  if (!c) return;
  if (yaExiste(c.n)) { toast(c.n + ' ya está en prospectos', 'var(--orange)'); dbAgregados[aid]=true; var btn2=document.getElementById(aid); if(btn2){btn2.textContent='✓';btn2.classList.add('done');} return; }
  prospectos.unshift({ id:uid(), empresa:c.n, contacto:'', cargo:'', tel:c.t, email:'', web:c.w, sector:c.s, notas:'Ciudad: '+c.c+'\nTipo: '+c.tp, status:'new', ts:Date.now() });
  guardarDB();
  dbAgregados[aid] = true;
  var btn = document.getElementById(aid);
  if (btn) { btn.textContent = '✓'; btn.classList.add('done'); }
  renderLista();
  toast('✅ ' + c.n + ' agregada');
}

// ═══════════════════════════════════════════
// IMPORTAR — PARSER LOCAL
// ═══════════════════════════════════════════
function extraer() {
  var raw = document.getElementById('txtImport').value.trim();
  if (!raw) { toast('Pega el texto primero', 'var(--orange)'); return; }
  var items = parsearTexto(raw);
  if (!items.length) { toast('No se detectaron empresas. Agrega más datos.', 'var(--orange)'); return; }
  impItems = items;
  renderImpCards();
  document.getElementById('paso1').style.display = 'none';
  document.getElementById('paso2').style.display = 'block';
  document.getElementById('imp-titulo').textContent = items.length + ' empresa' + (items.length !== 1 ? 's' : '') + ' detectada' + (items.length !== 1 ? 's' : '');
}

function parsearTexto(texto) {
  var TEL = /(\(?\d{2,3}\)?[\s.\-]?\d{3,4}[\s.\-]?\d{4})/;
  var EMAIL = /([\w.+-]+@[\w-]+\.[\w.]{2,})/i;
  var WEB = /(https?:\/\/\S+|www\.\S+)/i;

  var lineas = texto.split('\n');
  var resultados = [];
  var vistos = {};

  for (var i = 0; i < lineas.length; i++) {
    var linea = lineas[i].trim();
    if (linea.length < 3) continue;

    var tel = '', email = '', web = '';
    var tm = linea.match(TEL); if (tm) tel = tm[1].trim();
    var em = linea.match(EMAIL); if (em) email = em[1].trim();
    var wm = linea.match(WEB); if (wm) web = wm[1].trim();

    // Remove extracted data from line to get company name
    var nombre = linea;
    if (tm) nombre = nombre.replace(tm[0], '');
    if (em) nombre = nombre.replace(em[0], '');
    if (wm) nombre = nombre.replace(wm[0], '');
    nombre = nombre.replace(/\s{2,}/g, ' ').replace(/^[\s\-–|,:;]+|[\s\-–|,:;]+$/g, '').trim();

    // Skip if name is too short or just numbers
    if (!nombre || nombre.length < 3 || /^\d+$/.test(nombre)) continue;

    // Normalize SA DE CV variants (without dots)
    nombre = nombre
      .replace(/\bSAPI\s+DE\s+CV\b/gi, '')
      .replace(/\bSA\s+DE\s+CV\b/gi, '')
      .replace(/\bSRL\s+DE\s+CV\b/gi, '')
      .replace(/\bS\.A\.P\.I\.\s+de\s+C\.V\./gi, '')
      .replace(/\bS\.A\.\s+de\s+C\.V\./gi, '')
      .replace(/\bS\.R\.L\.\s+de\s+C\.V\./gi, '')
      .replace(/\bS\.A\./gi, '')
      .replace(/\bS\.C\./gi, '')
      .replace(/\bSC\b/gi, '')
      .replace(/\bDE\s+CV\b/gi, '')
      // Remove any leftover digits (phone remnants)
      .replace(/\d[\d\s\-().]+/g, '')
      .replace(/\s{2,}/g, ' ')
      .replace(/^[\s\-–|,:;]+|[\s\-–|,:;]+$/g, '')
      .trim();

    var clave = nombre.toLowerCase().replace(/\s+/g, '');
    if (vistos[clave]) {
      // If same company, try to add missing data
      if (tel && !vistos[clave].tel) vistos[clave].tel = tel;
      if (email && !vistos[clave].email) vistos[clave].email = email;
      if (web && !vistos[clave].web) vistos[clave].web = web;
      continue;
    }

    var item = { empresa: nombre, contacto: '', cargo: '', tel: tel, email: email, web: web, sector: inferirSector(nombre), notas: '', _inc: true };
    vistos[clave] = item;
    resultados.push(item);
  }

  return resultados;
}

function inferirSector(txt) {
  var t = txt.toLowerCase();
  if (/automotriz|autopart|vehicul|motor|transmis/.test(t)) return 'Automotriz';
  if (/aliment|bebida|lácteo|dulce|confite|aceite vegetal/.test(t)) return 'Alimentos';
  if (/aceite|vegetal/.test(t)) return 'Alimentos / Aceites';
  if (/químic|petroquím|plástic|polimer/.test(t)) return 'Química';
  if (/acero|metal|fundic|herraje|alumini/.test(t)) return 'Acero/Metal';
  if (/electrón|circuito|cables|telecom/.test(t)) return 'Electrónica';
  if (/papel|cartón|embalaje|empaque/.test(t)) return 'Papel / Embalaje';
  if (/fibra|fibras/.test(t)) return 'Fibras / Materiales';
  if (/textil|confección|tela|ropa/.test(t)) return 'Textil';
  if (/construct|cemento|cerámic/.test(t)) return 'Construcción';
  if (/farmac|laboratorio|medicament/.test(t)) return 'Farmacéutica';
  if (/minería|mineral|extracción/.test(t)) return 'Minería';
  if (/industrial/.test(t)) return 'Industrial';
  if (/comerci|soluciones/.test(t)) return 'Comercial';
  return '';
}

function renderImpCards() {
  var n = impItems.filter(function(x) { return x._inc; }).length;
  document.getElementById('btnAgregar').textContent = '✅ Agregar ' + n + ' empresa' + (n !== 1 ? 's' : '') + ' a prospectos';
  var html = '';
  for (var i = 0; i < impItems.length; i++) {
    var x = impItems[i];
    html += '<div class="icard ' + (x._inc ? '' : 'skip') + '" id="ic-' + i + '">';
    html += '<div class="icard-h">';
    html += '<div class="icard-n">' + esc(x.empresa || 'Sin nombre') + '</div>';
    html += '<button class="itog ' + (x._inc ? 'inc' : 'exc') + '" onclick="togInc(' + i + ')">' + (x._inc ? '✓ Incluir' : '✕ Omitir') + '</button>';
    html += '</div>';
    html += irow('Empresa', 'empresa', i, x.empresa);
    html += irow('Teléfono', 'tel', i, x.tel);
    html += irow('Email', 'email', i, x.email);
    html += irow('Web', 'web', i, x.web);
    html += irow('Sector', 'sector', i, x.sector);
    html += '</div>';
  }
  document.getElementById('impCards').innerHTML = html;
}

function irow(label, campo, idx, val) {
  return '<div class="irow"><span class="ilbl">' + label + '</span>' +
    '<input class="iinp" value="' + esc(val) + '" ' +
    'oninput="impItems[' + idx + '][\'' + campo + '\']=this.value" ' +
    'placeholder="' + label + '..."></div>';
}

function togInc(i) {
  impItems[i]._inc = !impItems[i]._inc;
  renderImpCards();
}

function agregarTodas() {
  var agregar = impItems.filter(function(x) { return x._inc && x.empresa; });
  if (!agregar.length) { toast('Nada seleccionado', 'var(--orange)'); return; }
  var added = 0, dupes = 0;
  for (var i = 0; i < agregar.length; i++) {
    var x = agregar[i];
    if (yaExiste(x.empresa)) { dupes++; continue; }
    prospectos.unshift({ id:uid(), empresa:x.empresa, contacto:x.contacto||'', cargo:x.cargo||'', tel:x.tel||'', email:x.email||'', web:x.web||'', sector:x.sector||'', notas:x.notas||'', status:'new', ts:Date.now() });
    added++;
  }
  guardarDB(); renderLista();
  var msg = '✅ ' + added + ' empresa' + (added !== 1 ? 's' : '') + ' agregada' + (added !== 1 ? 's' : '');
  if (dupes) msg += ' · ' + dupes + ' duplicado' + (dupes !== 1 ? 's' : '') + ' omitido' + (dupes !== 1 ? 's' : '');
  toast(msg);
  resetImport();
  ir('P');
}

function resetImport() {
  impItems = [];
  document.getElementById('txtImport').value = '';
  document.getElementById('paso1').style.display = 'block';
  document.getElementById('paso2').style.display = 'none';
}

// ═══════════════════════════════════════════
// OPERACIONES
// ═══════════════════════════════════════════
var KEY_OPS = 'mip_ops_v1';
var operaciones = []; // [{id, clienteId, fecha, monto, divisa, tc, notas}]
var opClienteId = null;
var divisaSel = 'USD';

function cargarOps() {
  try { operaciones = JSON.parse(localStorage.getItem(KEY_OPS)) || []; } catch(e) { operaciones = []; }
}
function guardarOps() { localStorage.setItem(KEY_OPS, JSON.stringify(operaciones)); }

function abrirOp(clienteId) {
  opClienteId = clienteId;
  var p = prospectos.find(function(x){return x.id===clienteId;});
  document.getElementById('opTit').textContent = 'Nueva operación' + (p ? ' — ' + p.empresa : '');
  document.getElementById('opFecha').value = new Date().toISOString().slice(0,10);
  document.getElementById('opMonto').value = '';
  document.getElementById('opTc').value = '';
  document.getElementById('opNotas').value = '';
  divisaSel = 'USD';
  document.querySelectorAll('#divisaGrid .so').forEach(function(el){
    el.classList.toggle('on', el.getAttribute('data-d') === 'USD');
  });
  document.getElementById('opOv').classList.add('on');
  setTimeout(function(){ document.getElementById('opMonto').focus(); }, 300);
}
function cerrarOp() { document.getElementById('opOv').classList.remove('on'); }

document.querySelectorAll('#divisaGrid .so').forEach(function(el){
  el.addEventListener('click', function(){
    divisaSel = el.getAttribute('data-d');
    document.querySelectorAll('#divisaGrid .so').forEach(function(x){
      x.classList.toggle('on', x.getAttribute('data-d') === divisaSel);
    });
  });
});

function guardarOp() {
  var monto = parseFloat(document.getElementById('opMonto').value);
  var fecha = document.getElementById('opFecha').value;
  if (!monto || !fecha) { toast('Ingresa monto y fecha', 'var(--orange)'); return; }
  var tc = parseFloat(document.getElementById('opTc').value) || 0;
  var op = {
    id: uid(),
    clienteId: opClienteId,
    fecha: fecha,
    monto: monto,
    divisa: divisaSel,
    tc: tc,
    notas: document.getElementById('opNotas').value.trim()
  };
  operaciones.unshift(op);
  guardarOps();
  // Update ultOp on the client
  for (var i = 0; i < prospectos.length; i++) {
    if (prospectos[i].id === opClienteId) {
      if (!prospectos[i].ultOp || fecha > prospectos[i].ultOp) prospectos[i].ultOp = fecha;
      break;
    }
  }
  guardarDB();
  cerrarOp();
  renderClientes();
  toast('✅ Operación registrada');
}

function borrarOp(opId) {
  if (!confirm('¿Eliminar esta operación?')) return;
  operaciones = operaciones.filter(function(o){ return o.id !== opId; });
  guardarOps();
  renderClientes();
  renderReporte();
  toast('Operación eliminada', 'var(--red)');
}

function fmtMonto(m, d) {
  return d + ' ' + Number(m).toLocaleString('es-MX', {minimumFractionDigits:2, maximumFractionDigits:2});
}
function fmtFecha(f) {
  if (!f) return '';
  var d = new Date(f + 'T12:00:00');
  return d.toLocaleDateString('es-MX', {day:'2-digit', month:'short', year:'numeric'});
}

// ═══════════════════════════════════════════
// CLIENTES
// ═══════════════════════════════════════════
var busquedaCliente = '';

function renderClientes() {
  var clientes = prospectos.filter(function(p) { return p.status === 'closed'; })
    .filter(function(p) {
      var q = busquedaCliente.toLowerCase();
      return !q || [p.empresa, p.contacto, p.sector, p.tel].some(function(f){
        return f && f.toLowerCase().indexOf(q) >= 0;
      });
    })
    .sort(function(a,b){ return a.empresa.localeCompare(b.empresa,'es',{sensitivity:'base'}); });

  var totalOps = operaciones.length;
  var totalMxn = operaciones.reduce(function(s,o){ return s + (o.monto * (o.tc||1)); }, 0);
  document.getElementById('statsClientes').textContent =
    clientes.length + ' cliente' + (clientes.length!==1?'s':'') +
    (totalOps ? ' · ' + totalOps + ' ops' : '');

  if (!clientes.length) {
    document.getElementById('listaClientes').innerHTML =
      '<div class="empty"><div class="empty-i">🏆</div>' +
      '<div class="empty-t">Sin clientes aún</div>' +
      '<div class="empty-s">Marca un prospecto como "Cliente" y aparecerá aquí</div></div>';
    return;
  }

  var html = '';
  for (var i = 0; i < clientes.length; i++) {
    var p = clientes[i];
    var col = color(p.empresa);
    var ini = initials(p.empresa);
    var ops = operaciones.filter(function(o){ return o.clienteId === p.id; });
    var totalCli = ops.reduce(function(s,o){ return s + o.monto; }, 0);
    var ultOpFmt = p.ultOp ? fmtFecha(p.ultOp) : '';

    html += '<div class="pc" id="pc-'+p.id+'">';
    // Header
    html += '<div class="pc-h" onclick="toggle(\''+p.id+'\')">';
    html += '<div class="av" style="background:'+col+'22;color:'+col+';border:2px solid '+col+'44">'+ini+'</div>';
    html += '<div class="pi"><div class="pn">'+esc(p.empresa)+'</div>';
    html += '<div class="ps">'+(ops.length ? ops.length+' op'+(ops.length!==1?'s':'')+' · '+fmtMonto(totalCli, ops[0].divisa||'USD') : (p.sector?esc(p.sector):'Sin operaciones'))+'</div></div>';
    html += '<div class="pr">';
    html += '<span style="font-size:.6rem;font-weight:700;padding:3px 9px;border-radius:20px;border:1.5px solid var(--green);color:var(--green)">Terminado</span>';
    if (ultOpFmt) html += '<span style="font-size:.58rem;color:var(--t3)">'+ultOpFmt+'</span>';
    html += '</div>';
    html += '<span class="chv">▾</span>';
    html += '</div>';

    // Body
    html += '<div class="pc-b">';
    html += '<div class="dg">';
    if (p.tel) html += '<div class="dr"><span class="dl">Tel</span><span class="dv"><a href="tel:'+esc(p.tel)+'">'+esc(p.tel)+'</a></span></div>';
    if (p.email) html += '<div class="dr"><span class="dl">Email</span><span class="dv"><a href="mailto:'+esc(p.email)+'">'+esc(p.email)+'</a></span></div>';
    if (p.contacto) html += '<div class="dr"><span class="dl">Contacto</span><span class="dv">'+esc(p.contacto)+(p.cargo?' · '+esc(p.cargo):'')+'</span></div>';
    if (p.sector) html += '<div class="dr"><span class="dl">Sector</span><span class="dv">'+esc(p.sector)+'</span></div>';
    html += '</div>';

    // Operations history
    html += '<div style="margin-top:12px;padding-top:10px;border-top:1px solid var(--b)">';
    html += '<div style="display:flex;align-items:center;justify-content:space-between;margin-bottom:8px">';
    html += '<span style="font-size:.65rem;font-weight:700;color:var(--t3);text-transform:uppercase;letter-spacing:.06em">Historial de operaciones</span>';
    html += '<button onclick="sp(event);abrirOp(\''+p.id+'\')" style="background:var(--blue);border:none;border-radius:8px;padding:5px 12px;color:#fff;font-size:.7rem;font-weight:700;cursor:pointer;font-family:inherit">+ Nueva</button>';
    html += '</div>';

    if (ops.length) {
      for (var j = 0; j < ops.length; j++) {
        var o = ops[j];
        html += '<div class="op-card">';
        html += '<div class="op-div">'+esc(o.divisa)+'</div>';
        html += '<div class="op-info">';
        html += '<div class="op-monto">'+fmtMonto(o.monto, o.divisa)+'</div>';
        html += '<div class="op-meta">'+fmtFecha(o.fecha)+(o.tc?' · TC: '+o.tc:'')+(o.notas?' · '+esc(o.notas):'')+'</div>';
        html += '</div>';
        html += '<button class="op-del" onclick="sp(event);borrarOp(\''+o.id+'\')">✕</button>';
        html += '</div>';
      }
      // Total
      html += '<div style="background:rgba(52,211,153,.08);border:1px solid rgba(52,211,153,.2);border-radius:8px;padding:8px 12px;margin-top:4px;display:flex;justify-content:space-between;align-items:center">';
      html += '<span style="font-size:.65rem;color:var(--t3);font-weight:700">TOTAL</span>';
      html += '<span style="font-size:.85rem;font-weight:800;color:var(--green)">'+fmtMonto(totalCli, ops[0].divisa||'USD')+'</span>';
      html += '</div>';
    } else {
      html += '<div style="text-align:center;padding:12px;color:var(--t3);font-size:.75rem">Sin operaciones aún</div>';
    }
    html += '</div>'; // end ops section

    // Actions
    html += '<div class="acts" style="margin-top:10px;padding-top:10px;border-top:1px solid var(--b)">';
    if (p.tel) html += '<button class="ac call" onclick="sp(event);location.href=\'tel:'+esc(p.tel)+'\'">📞 Llamar</button>';
    if (p.email) html += '<button class="ac mail" onclick="sp(event);location.href=\'mailto:'+esc(p.email)+'\'">✉ Email</button>';
    html += '<button class="ac edit" onclick="sp(event);editarCard(\''+p.id+'\')">✏ Editar</button>';
    html += '</div>';
    html += '</div>'; // end pc-b
    html += '</div>'; // end pc
  }
  document.getElementById('listaClientes').innerHTML = html;
}

document.getElementById('buscarCliente').addEventListener('input', function() {
  busquedaCliente = this.value;
  renderClientes();
});

// ═══════════════════════════════════════════
// REPORTES
// ═══════════════════════════════════════════
var reporteTab = 'general';

function setReporteTab(t) {
  reporteTab = t;
  ['General','Mensual','Cliente'].forEach(function(x){
    document.getElementById('rt'+x).classList.toggle('on', t === x.toLowerCase());
  });
  renderReporte();
}

function renderReporte() {
  document.getElementById('rFecha').textContent = new Date().toLocaleDateString('es-MX',{day:'numeric',month:'short',year:'numeric'});
  if (reporteTab === 'general') renderReporteGeneral();
  else if (reporteTab === 'mensual') renderReporteMensual();
  else renderReporteCliente();
}

function renderReporteGeneral() {
  var clientes = prospectos.filter(function(p){return p.status==='closed';});
  var totalOps = operaciones.length;
  var divisas = {};
  operaciones.forEach(function(o){
    divisas[o.divisa] = (divisas[o.divisa]||0) + o.monto;
  });
  var totalMxn = operaciones.reduce(function(s,o){ return s+(o.monto*(o.tc||1)); },0);

  var html = '';

  // Summary cards
  html += '<div class="rgrid">';
  html += '<div class="rcard" style="margin-bottom:0"><div class="rcard-title">Clientes</div><div class="rnum">'+clientes.length+'</div><div class="rsub">activos</div></div>';
  html += '<div class="rcard" style="margin-bottom:0"><div class="rcard-title">Operaciones</div><div class="rnum">'+totalOps+'</div><div class="rsub">registradas</div></div>';
  html += '</div>';

  // Total by currency
  html += '<div class="rcard"><div class="rcard-title">Total operado por divisa</div>';
  if (!Object.keys(divisas).length) {
    html += '<div style="color:var(--t3);font-size:.78rem;text-align:center;padding:10px 0">Sin operaciones aún</div>';
  } else {
    Object.keys(divisas).forEach(function(d){
      html += '<div class="rbar-wrap">';
      html += '<div class="rbar-label"><span>'+d+'</span><span>'+fmtMonto(divisas[d],d)+'</span></div>';
      html += '</div>';
    });
    if (totalMxn > 0) {
      html += '<div style="margin-top:10px;padding-top:10px;border-top:1px solid var(--b);display:flex;justify-content:space-between;align-items:center">';
      html += '<span style="font-size:.65rem;color:var(--t3);font-weight:700">EQUIV. TOTAL MXN</span>';
      html += '<span style="font-size:.9rem;font-weight:800;color:var(--green)">$'+Number(totalMxn).toLocaleString('es-MX',{minimumFractionDigits:2,maximumFractionDigits:2})+'</span>';
      html += '</div>';
    }
  }
  html += '</div>';

  // Top clients
  html += '<div class="rcard"><div class="rcard-title">Top clientes por volumen</div>';
  var porCliente = {};
  operaciones.forEach(function(o){
    if (!porCliente[o.clienteId]) porCliente[o.clienteId] = {monto:0, divisa:o.divisa, ops:0};
    porCliente[o.clienteId].monto += o.monto;
    porCliente[o.clienteId].ops++;
  });
  var sorted = Object.keys(porCliente).sort(function(a,b){ return porCliente[b].monto - porCliente[a].monto; });
  if (!sorted.length) {
    html += '<div style="color:var(--t3);font-size:.78rem;text-align:center;padding:10px 0">Sin operaciones aún</div>';
  } else {
    var max = porCliente[sorted[0]].monto;
    sorted.slice(0,8).forEach(function(cid){
      var p = prospectos.find(function(x){return x.id===cid;}) || {empresa:'Desconocido'};
      var pct = max > 0 ? (porCliente[cid].monto/max*100) : 0;
      html += '<div class="rbar-wrap">';
      html += '<div class="rbar-label"><span>'+esc(p.empresa)+'</span><span>'+fmtMonto(porCliente[cid].monto, porCliente[cid].divisa)+'</span></div>';
      html += '<div class="rbar-track"><div class="rbar-fill" style="width:'+pct+'%"></div></div>';
      html += '</div>';
    });
  }
  html += '</div>';

  // Recent ops
  html += '<div class="rcard"><div class="rcard-title">Últimas operaciones</div>';
  if (!operaciones.length) {
    html += '<div style="color:var(--t3);font-size:.78rem;text-align:center;padding:10px 0">Sin operaciones aún</div>';
  } else {
    var recientes = operaciones.slice().sort(function(a,b){return b.fecha.localeCompare(a.fecha);}).slice(0,5);
    recientes.forEach(function(o){
      var p = prospectos.find(function(x){return x.id===o.clienteId;}) || {empresa:'?'};
      html += '<div class="op-card">';
      html += '<div class="op-div">'+esc(o.divisa)+'</div>';
      html += '<div class="op-info"><div class="op-monto">'+fmtMonto(o.monto,o.divisa)+'</div>';
      html += '<div class="op-meta">'+esc(p.empresa)+' · '+fmtFecha(o.fecha)+'</div></div>';
      html += '</div>';
    });
  }
  html += '</div>';

  document.getElementById('reporteArea').innerHTML = html;
}

function renderReporteMensual() {
  // Group by YYYY-MM
  var meses = {};
  operaciones.forEach(function(o){
    var m = o.fecha.slice(0,7);
    if (!meses[m]) meses[m] = {};
    meses[m][o.divisa] = (meses[m][o.divisa]||0) + o.monto;
  });
  var keys = Object.keys(meses).sort().reverse();

  var html = '';
  if (!keys.length) {
    html = '<div class="empty"><div class="empty-i">📅</div><div class="empty-t">Sin datos</div><div class="empty-s">Registra operaciones para ver el historial mensual</div></div>';
  } else {
    keys.forEach(function(m){
      var d = new Date(m + '-01T12:00:00');
      var label = d.toLocaleDateString('es-MX',{month:'long',year:'numeric'});
      html += '<div class="rcard">';
      html += '<div class="rcard-title">'+label+'</div>';
      var divs = meses[m];
      Object.keys(divs).forEach(function(d2){
        html += '<div style="display:flex;justify-content:space-between;align-items:center;padding:5px 0;border-bottom:1px solid var(--b)">';
        html += '<span style="font-size:.75rem;color:var(--t2)">'+d2+'</span>';
        html += '<span style="font-size:.82rem;font-weight:700;color:var(--t)">'+fmtMonto(divs[d2],d2)+'</span>';
        html += '</div>';
      });
      var opsDelMes = operaciones.filter(function(o){return o.fecha.slice(0,7)===m;}).length;
      html += '<div style="font-size:.65rem;color:var(--t3);margin-top:8px">'+opsDelMes+' operación'+(opsDelMes!==1?'es':'')+'</div>';
      html += '</div>';
    });
  }
  document.getElementById('reporteArea').innerHTML = html;
}

function renderReporteCliente() {
  var clientes = prospectos.filter(function(p){return p.status==='closed';})
    .sort(function(a,b){return a.empresa.localeCompare(b.empresa,'es',{sensitivity:'base'});});

  var html = '';
  if (!clientes.length) {
    html = '<div class="empty"><div class="empty-i">🏆</div><div class="empty-t">Sin clientes</div><div class="empty-s">Aún no tienes clientes registrados</div></div>';
  } else {
    clientes.forEach(function(p){
      var ops = operaciones.filter(function(o){return o.clienteId===p.id;})
        .sort(function(a,b){return b.fecha.localeCompare(a.fecha);});
      var col = color(p.empresa);
      html += '<div class="rcard">';
      html += '<div style="display:flex;align-items:center;gap:10px;margin-bottom:10px">';
      html += '<div class="av" style="width:36px;height:36px;border-radius:9px;font-size:.85rem;background:'+col+'22;color:'+col+';border:2px solid '+col+'44;display:flex;align-items:center;justify-content:center;font-weight:800">'+initials(p.empresa)+'</div>';
      html += '<div><div style="font-weight:700;font-size:.85rem">'+esc(p.empresa)+'</div>';
      html += '<div style="font-size:.65rem;color:var(--t3)">'+ops.length+' operación'+(ops.length!==1?'es':'')+(p.ultOp?' · Últ: '+fmtFecha(p.ultOp):'')+'</div></div>';
      html += '</div>';
      if (ops.length) {
        var divisas = {};
        ops.forEach(function(o){ divisas[o.divisa]=(divisas[o.divisa]||0)+o.monto; });
        Object.keys(divisas).forEach(function(d){
          html += '<div style="display:flex;justify-content:space-between;padding:5px 0;border-bottom:1px solid var(--b)">';
          html += '<span style="font-size:.72rem;color:var(--t2)">'+d+'</span>';
          html += '<span style="font-size:.78rem;font-weight:700;color:var(--green)">'+fmtMonto(divisas[d],d)+'</span>';
          html += '</div>';
        });
        // Last 3 ops
        html += '<div style="margin-top:8px">';
        ops.slice(0,3).forEach(function(o){
          html += '<div style="display:flex;justify-content:space-between;align-items:center;padding:4px 0;font-size:.7rem">';
          html += '<span style="color:var(--t3)">'+fmtFecha(o.fecha)+(o.notas?' · '+esc(o.notas):'')+'</span>';
          html += '<span style="color:var(--t);font-weight:600">'+fmtMonto(o.monto,o.divisa)+'</span>';
          html += '</div>';
        });
        if (ops.length > 3) html += '<div style="font-size:.65rem;color:var(--t3);text-align:right">+' + (ops.length-3)+' más</div>';
        html += '</div>';
      } else {
        html += '<div style="color:var(--t3);font-size:.75rem;text-align:center;padding:8px 0">Sin operaciones</div>';
      }
      html += '</div>';
    });
  }
  document.getElementById('reporteArea').innerHTML = html;
}

// ═══════════════════════════════════════════
// EVENT LISTENERS
// ═══════════════════════════════════════════
document.getElementById('buscar').addEventListener('input', function() {
  busqueda = this.value;
  renderLista();
});

document.getElementById('dBuscar').addEventListener('input', function() {
  dBusqueda = this.value;
  renderDescubrir();
});

// ═══════════════════════════════════════════
// LOG DE CONTACTOS
// ═══════════════════════════════════════════
var KEY_LOG = 'mip_log_v1';
var contactos = []; // [{id, prospectoId, tipo, nota, fecha}]
var logProspId = null;
var logTipo = 'llamada';

function cargarLog() {
  try { contactos = JSON.parse(localStorage.getItem(KEY_LOG)) || []; } catch(e) { contactos = []; }
}
function guardarLog_db() { localStorage.setItem(KEY_LOG, JSON.stringify(contactos)); }

function abrirLog(pid) {
  logProspId = pid;
  logTipo = 'llamada';
  var p = buscarProspecto(pid);
  document.getElementById('logTit').textContent = (p ? p.empresa : '') + ' — Registrar contacto';
  document.getElementById('logNota').value = '';
  document.getElementById('logFecha').value = hoy();
  document.querySelectorAll('.ct').forEach(function(el) {
    el.classList.toggle('on', el.getAttribute('data-ct') === 'llamada');
  });
  document.getElementById('logOv').classList.add('on');
  setTimeout(function() { document.getElementById('logNota').focus(); }, 300);
}
function cerrarLog() { document.getElementById('logOv').classList.remove('on'); }

document.querySelectorAll('.ct').forEach(function(el) {
  el.addEventListener('click', function() {
    logTipo = el.getAttribute('data-ct');
    document.querySelectorAll('.ct').forEach(function(x) { x.classList.toggle('on', x.getAttribute('data-ct') === logTipo); });
  });
});

function guardarLog() {
  var nota = document.getElementById('logNota').value.trim();
  var fecha = document.getElementById('logFecha').value;
  if (!nota) { toast('Escribe una nota del contacto', 'var(--orange)'); return; }
  var entry = { id: uid(), prospectoId: logProspId, tipo: logTipo, nota: nota, fecha: fecha || hoy() };
  contactos.unshift(entry);
  guardarLog_db();
  // Update lastContact on prospecto
  for (var i = 0; i < prospectos.length; i++) {
    if (prospectos[i].id === logProspId) {
      if (!prospectos[i].lastContact || entry.fecha >= prospectos[i].lastContact) {
        prospectos[i].lastContact = entry.fecha;
      }
      break;
    }
  }
  guardarDB();
  cerrarLog();
  renderLista();
  toast('✅ Contacto registrado');
}

function borrarLog(lid) {
  contactos = contactos.filter(function(c) { return c.id !== lid; });
  guardarLog_db();
  renderLista();
  toast('Eliminado', 'var(--red)');
}

var TIPO_ICON = { llamada:'📞', whatsapp:'💬', email:'✉', reunion:'🤝', otro:'📝' };

// ═══════════════════════════════════════════
// RECORDATORIOS
// ═══════════════════════════════════════════
var KEY_REM = 'mip_rem_v1';
var recordatorios = []; // [{id, prospectoId, texto, fecha, hora, done}]
var remProspId = null;

function cargarRem() {
  try { recordatorios = JSON.parse(localStorage.getItem(KEY_REM)) || []; } catch(e) { recordatorios = []; }
}
function guardarRem_db() { localStorage.setItem(KEY_REM, JSON.stringify(recordatorios)); }

function abrirRem(pid) {
  remProspId = pid;
  var p = buscarProspecto(pid);
  document.getElementById('remTit').textContent = (p ? p.empresa : '') + ' — Recordatorio';
  document.getElementById('remTexto').value = '';
  document.getElementById('remFecha').value = hoy();
  document.getElementById('remHora').value = '';
  document.getElementById('remOv').classList.add('on');
  setTimeout(function() { document.getElementById('remTexto').focus(); }, 300);
}
function cerrarRem() { document.getElementById('remOv').classList.remove('on'); }

function setRemFecha(dias) {
  var d = new Date();
  d.setDate(d.getDate() + dias);
  document.getElementById('remFecha').value = d.toISOString().slice(0, 10);
}

function guardarRem() {
  var texto = document.getElementById('remTexto').value.trim();
  var fecha = document.getElementById('remFecha').value;
  if (!texto || !fecha) { toast('Ingresa tarea y fecha', 'var(--orange)'); return; }
  recordatorios.push({
    id: uid(), prospectoId: remProspId,
    texto: texto, fecha: fecha,
    hora: document.getElementById('remHora').value || '',
    done: false
  });
  guardarRem_db();
  cerrarRem();
  renderLista();
  updateRemBadge();
  toast('⏰ Recordatorio guardado');
}

function completarRem(rid) {
  for (var i = 0; i < recordatorios.length; i++) {
    if (recordatorios[i].id === rid) { recordatorios[i].done = true; break; }
  }
  guardarRem_db();
  renderLista();
  updateRemBadge();
  toast('✅ Listo');
}

function borrarRem(rid) {
  recordatorios = recordatorios.filter(function(r) { return r.id !== rid; });
  guardarRem_db();
  renderLista();
  updateRemBadge();
}

function updateRemBadge() {
  var today = hoy();
  var vencidos = recordatorios.filter(function(r) { return !r.done && r.fecha <= today; }).length;
  var badge = document.getElementById('remNavBadge');
  if (badge) {
    badge.textContent = vencidos || '';
    badge.style.display = vencidos ? 'inline-block' : 'none';
  }
}

// ═══════════════════════════════════════════
// TEMPERATURA (HEAT)
// ═══════════════════════════════════════════
function heatLevel(p) {
  // Based on days since last contact log entry
  var logs = contactos.filter(function(c) { return c.prospectoId === p.id; });
  var lastDate = p.lastContact || null;
  if (logs.length) {
    logs.forEach(function(l) { if (!lastDate || l.fecha > lastDate) lastDate = l.fecha; });
  }
  if (!lastDate) return 'cold'; // never contacted
  var days = Math.floor((new Date(hoy()) - new Date(lastDate)) / 86400000);
  if (days <= 7) return 'hot';
  if (days <= 21) return 'warm';
  return 'cold';
}

// ═══════════════════════════════════════════
// UTILS
// ═══════════════════════════════════════════
function hoy() { return new Date().toISOString().slice(0, 10); }
function buscarProspecto(id) {
  for (var i = 0; i < prospectos.length; i++) { if (prospectos[i].id === id) return prospectos[i]; }
  return null;
}

// ═══════════════════════════════════════════
// RESPALDO
// ═══════════════════════════════════════════
function exportarRespaldo() {
  var backup = {
    version: 1,
    fecha: new Date().toISOString(),
    prospectos: prospectos,
    operaciones: operaciones,
    contactos: contactos,
    recordatorios: recordatorios
  };
  var json = JSON.stringify(backup, null, 2);
  var blob = new Blob([json], { type: 'application/json' });
  var url = URL.createObjectURL(blob);
  var a = document.createElement('a');
  var fecha = new Date().toISOString().slice(0, 10);
  a.href = url;
  a.download = 'miprospecto-respaldo-' + fecha + '.json';
  document.body.appendChild(a);
  a.click();
  document.body.removeChild(a);
  URL.revokeObjectURL(url);
  toast('✅ Respaldo descargado · ' + prospectos.length + ' prospectos guardados');
}

function importarRespaldo(input) {
  var file = input.files[0];
  if (!file) return;
  var reader = new FileReader();
  reader.onload = function(e) {
    try {
      var data = JSON.parse(e.target.result);
      if (!data.prospectos) { toast('Archivo inválido', 'var(--red)'); return; }
      var msg = '¿Restaurar respaldo del ' + (data.fecha ? data.fecha.slice(0,10) : 'archivo') + '?\n\n' +
        '• ' + (data.prospectos||[]).length + ' prospectos\n' +
        '• ' + (data.operaciones||[]).length + ' operaciones\n' +
        '• ' + (data.contactos||[]).length + ' contactos\n' +
        '• ' + (data.recordatorios||[]).length + ' recordatorios\n\n' +
        'Esto REEMPLAZARÁ todos tus datos actuales.';
      if (!confirm(msg)) { input.value = ''; return; }
      prospectos = data.prospectos || [];
      operaciones = data.operaciones || [];
      contactos = data.contactos || [];
      recordatorios = data.recordatorios || [];
      guardarDB();
      guardarOps();
      guardarLog_db();
      guardarRem_db();
      deduplicar();
      renderLista();
      renderClientes();
      updateRemBadge();
      input.value = '';
      toast('✅ Respaldo restaurado · ' + prospectos.length + ' prospectos cargados');
      ir('P');
    } catch(err) {
      toast('Error al leer el archivo', 'var(--red)');
    }
  };
  reader.readAsText(file);
}

// ═══════════════════════════════════════════
// INIT
// ═══════════════════════════════════════════
document.getElementById('fecha').textContent = new Date().toLocaleDateString('es-MX', { weekday:'short', day:'numeric', month:'short' });

// ── SEED DATA (first load only) ──
(function() {
  if (!localStorage.getItem('mip_v3')) {
    var seed = [{"id": "pre1001", "empresa": "INGREDION MEXICO", "contacto": "", "cargo": "", "tel": "33 3884 9000", "email": "", "web": "", "sector": "Alimentos", "notas": "Ciudad: Jalisco", "status": "new", "ts": 1776868036945, "lastContact": null, "ultOp": null}, {"id": "pre1002", "empresa": "SOLUCIONES INTELIGENTES EN ACEITE VEGETAL", "contacto": "", "cargo": "", "tel": "33 1350 7951", "email": "", "web": "", "sector": "Aceites / Alimentos", "notas": "Ciudad: Jalisco", "status": "new", "ts": 1776868035945, "lastContact": null, "ultOp": null}, {"id": "pre1003", "empresa": "ALTA FIBRA", "contacto": "", "cargo": "", "tel": "33 1057 9112", "email": "", "web": "", "sector": "Fibras / Materiales", "notas": "Ciudad: Jalisco", "status": "new", "ts": 1776868034945, "lastContact": null, "ultOp": null}, {"id": "pre1004", "empresa": "BORDA INDUSTRIAL", "contacto": "", "cargo": "", "tel": "33 3826 9035", "email": "", "web": "", "sector": "Industrial", "notas": "Ciudad: Jalisco", "status": "new", "ts": 1776868033945, "lastContact": null, "ultOp": null}, {"id": "pre1005", "empresa": "SUIZ COMERCIAL", "contacto": "", "cargo": "", "tel": "33 3823 2423", "email": "", "web": "", "sector": "Comercial", "notas": "Ciudad: Jalisco", "status": "new", "ts": 1776868032945, "lastContact": null, "ultOp": null}, {"id": "pre1006", "empresa": "EL ROSAL TAPATIO", "contacto": "", "cargo": "", "tel": "33 3898 4740", "email": "", "web": "", "sector": "Alimentos", "notas": "Ciudad: Jalisco", "status": "new", "ts": 1776868031945, "lastContact": null, "ultOp": null}, {"id": "pre1007", "empresa": "DULANDY DULCES", "contacto": "", "cargo": "", "tel": "33 3665 0000", "email": "", "web": "", "sector": "Alimentos", "notas": "Ciudad: Jalisco", "status": "new", "ts": 1776868030945, "lastContact": null, "ultOp": null}, {"id": "pre1008", "empresa": "INDUSTRIAS ALIMENTICIAS LA TAPATIA", "contacto": "", "cargo": "", "tel": "33 3619 4400", "email": "", "web": "", "sector": "Alimentos", "notas": "Ciudad: Jalisco", "status": "new", "ts": 1776868029945, "lastContact": null, "ultOp": null}, {"id": "pre1009", "empresa": "EMPACADORA NOEL", "contacto": "", "cargo": "", "tel": "33 3812 5500", "email": "", "web": "", "sector": "Alimentos", "notas": "Ciudad: Jalisco", "status": "new", "ts": 1776868028945, "lastContact": null, "ultOp": null}, {"id": "pre1010", "empresa": "PLASTICOS Y HULES DE OCCIDENTE", "contacto": "", "cargo": "", "tel": "33 3674 2200", "email": "", "web": "", "sector": "Plásticos", "notas": "Ciudad: Jalisco", "status": "new", "ts": 1776868027945, "lastContact": null, "ultOp": null}, {"id": "pre1011", "empresa": "HERRAJES Y ACCESORIOS DEL PACIFICO", "contacto": "", "cargo": "", "tel": "33 3812 3100", "email": "", "web": "", "sector": "Metal", "notas": "Ciudad: Jalisco", "status": "new", "ts": 1776868026945, "lastContact": null, "ultOp": null}, {"id": "pre1012", "empresa": "ARMETAL ROLADORAS", "contacto": "", "cargo": "", "tel": "33 3352 2640", "email": "", "web": "https://armetalmx.mx", "sector": "Maquinaria industrial", "notas": "Ciudad: Jalisco", "status": "new", "ts": 1776868025945, "lastContact": null, "ultOp": null}, {"id": "pre1013", "empresa": "METALURGICA TAPATIA", "contacto": "", "cargo": "", "tel": "33 3812 6100", "email": "", "web": "", "sector": "Acero/Metal", "notas": "Ciudad: Jalisco", "status": "new", "ts": 1776868024945, "lastContact": null, "ultOp": null}, {"id": "pre1014", "empresa": "CONFECCIONES JALISCO", "contacto": "", "cargo": "", "tel": "33 3812 4400", "email": "", "web": "", "sector": "Textil", "notas": "Ciudad: Jalisco", "status": "new", "ts": 1776868023945, "lastContact": null, "ultOp": null}, {"id": "pre1015", "empresa": "EMPAQUES INDUSTRIALES DE OCCIDENTE", "contacto": "", "cargo": "", "tel": "33 3688 0500", "email": "", "web": "", "sector": "Embalaje", "notas": "Ciudad: Jalisco", "status": "new", "ts": 1776868022945, "lastContact": null, "ultOp": null}, {"id": "pre1016", "empresa": "QUIMICA DEL OCCIDENTE", "contacto": "", "cargo": "", "tel": "33 3635 7800", "email": "", "web": "", "sector": "Química", "notas": "Ciudad: Jalisco", "status": "new", "ts": 1776868021945, "lastContact": null, "ultOp": null}, {"id": "pre1017", "empresa": "PLASTICOS CORONA", "contacto": "", "cargo": "", "tel": "33 3812 4200", "email": "", "web": "", "sector": "Plásticos", "notas": "Ciudad: Jalisco", "status": "new", "ts": 1776868020945, "lastContact": null, "ultOp": null}, {"id": "pre1018", "empresa": "CRISTALERIA JALISCO", "contacto": "", "cargo": "", "tel": "33 3812 5300", "email": "", "web": "", "sector": "Manufactura", "notas": "Ciudad: Jalisco", "status": "new", "ts": 1776868019945, "lastContact": null, "ultOp": null}, {"id": "pre1019", "empresa": "MAQUINARIA Y REFACCIONES DEL PACIFICO", "contacto": "", "cargo": "", "tel": "33 3812 6200", "email": "", "web": "", "sector": "Maquinaria", "notas": "Ciudad: Jalisco", "status": "new", "ts": 1776868018945, "lastContact": null, "ultOp": null}, {"id": "pre1020", "empresa": "ACEROS Y METALES DE JALISCO", "contacto": "", "cargo": "", "tel": "33 3812 3900", "email": "", "web": "", "sector": "Acero/Metal", "notas": "Ciudad: Jalisco", "status": "new", "ts": 1776868017945, "lastContact": null, "ultOp": null}, {"id": "pre1021", "empresa": "INDUSTRIAS TEXTILES TAPATIO", "contacto": "", "cargo": "", "tel": "33 3812 5100", "email": "", "web": "", "sector": "Textil", "notas": "Ciudad: Jalisco", "status": "new", "ts": 1776868016945, "lastContact": null, "ultOp": null}, {"id": "pre1022", "empresa": "JABIL CIRCUIT DE MEXICO", "contacto": "", "cargo": "", "tel": "33 3819 1300", "email": "", "web": "https://www.jabil.mx", "sector": "Manufactura electrónica", "notas": "Ciudad: Jalisco", "status": "new", "ts": 1776868015945, "lastContact": null, "ultOp": null}, {"id": "pre1023", "empresa": "FRESENIUS KABI MEXICO", "contacto": "", "cargo": "", "tel": "33 3540 7800", "email": "", "web": "https://www.fresenius-kabi.com/mx", "sector": "Farmacéutica", "notas": "Ciudad: Jalisco", "status": "new", "ts": 1776868014945, "lastContact": null, "ultOp": null}, {"id": "pre1024", "empresa": "GRUPO PISA", "contacto": "", "cargo": "", "tel": "33 3669 6600", "email": "", "web": "https://www.pisa.com.mx", "sector": "Farmacéutica", "notas": "Ciudad: Jalisco", "status": "new", "ts": 1776868013945, "lastContact": null, "ultOp": null}, {"id": "pre1025", "empresa": "CRISTALES AUTOMOTRICES DE JALISCO", "contacto": "", "cargo": "", "tel": "33 3812 4500", "email": "", "web": "", "sector": "Automotriz", "notas": "Ciudad: Jalisco", "status": "new", "ts": 1776868012945, "lastContact": null, "ultOp": null}, {"id": "pre1026", "empresa": "SPIROL DE MEXICO", "contacto": "", "cargo": "", "tel": "81 8386 2100", "email": "", "web": "", "sector": "Manufactura / Metal", "notas": "Ciudad: Nuevo León", "status": "new", "ts": 1776868011945, "lastContact": null, "ultOp": null}, {"id": "pre1027", "empresa": "BEST LINK SCRAP", "contacto": "", "cargo": "", "tel": "81 8386 5500", "email": "", "web": "", "sector": "Plásticos / Reciclaje", "notas": "Ciudad: Nuevo León", "status": "new", "ts": 1776868010945, "lastContact": null, "ultOp": null}, {"id": "pre1028", "empresa": "PLASTICOS Y HULES DEL NORTE", "contacto": "", "cargo": "", "tel": "81 8386 3300", "email": "", "web": "", "sector": "Plásticos", "notas": "Ciudad: Nuevo León", "status": "new", "ts": 1776868009945, "lastContact": null, "ultOp": null}, {"id": "pre1029", "empresa": "METALMECANICA REGIOMONTANA", "contacto": "", "cargo": "", "tel": "81 8386 4400", "email": "", "web": "", "sector": "Acero/Metal", "notas": "Ciudad: Nuevo León", "status": "new", "ts": 1776868008945, "lastContact": null, "ultOp": null}, {"id": "pre1030", "empresa": "ACEROS PROCESADOS DEL NORTE", "contacto": "", "cargo": "", "tel": "81 8336 2200", "email": "", "web": "", "sector": "Acero/Metal", "notas": "Ciudad: Nuevo León", "status": "new", "ts": 1776868007945, "lastContact": null, "ultOp": null}, {"id": "pre1031", "empresa": "EMPAQUES Y SOLUCIONES MONTERREY", "contacto": "", "cargo": "", "tel": "81 8386 6600", "email": "", "web": "", "sector": "Embalaje", "notas": "Ciudad: Nuevo León", "status": "new", "ts": 1776868006945, "lastContact": null, "ultOp": null}, {"id": "pre1032", "empresa": "HERRAJES INDUSTRIALES MONTERREY", "contacto": "", "cargo": "", "tel": "81 8386 7700", "email": "", "web": "", "sector": "Metal", "notas": "Ciudad: Nuevo León", "status": "new", "ts": 1776868005945, "lastContact": null, "ultOp": null}, {"id": "pre1033", "empresa": "QUIMICA ESPECIALIZADA DEL NORTE", "contacto": "", "cargo": "", "tel": "81 8386 8800", "email": "", "web": "", "sector": "Química", "notas": "Ciudad: Nuevo León", "status": "new", "ts": 1776868004945, "lastContact": null, "ultOp": null}, {"id": "pre1034", "empresa": "CONFECCIONES INDUSTRIALES REGIO", "contacto": "", "cargo": "", "tel": "81 8336 9900", "email": "", "web": "", "sector": "Textil", "notas": "Ciudad: Nuevo León", "status": "new", "ts": 1776868003945, "lastContact": null, "ultOp": null}, {"id": "pre1035", "empresa": "MAQUINARIA Y EQUIPO MONTERREY", "contacto": "", "cargo": "", "tel": "81 8336 1100", "email": "", "web": "", "sector": "Maquinaria", "notas": "Ciudad: Nuevo León", "status": "new", "ts": 1776868002945, "lastContact": null, "ultOp": null}, {"id": "pre1036", "empresa": "TRANSFORMACIONES METALICAS APODACA", "contacto": "", "cargo": "", "tel": "81 8386 2200", "email": "", "web": "", "sector": "Acero/Metal", "notas": "Ciudad: Nuevo León", "status": "new", "ts": 1776868001945, "lastContact": null, "ultOp": null}, {"id": "pre1037", "empresa": "EMBALAJES Y CONTENEDORES NORTE", "contacto": "", "cargo": "", "tel": "81 8386 3300", "email": "", "web": "", "sector": "Embalaje", "notas": "Ciudad: Nuevo León", "status": "new", "ts": 1776868000945, "lastContact": null, "ultOp": null}, {"id": "pre1038", "empresa": "INDUSTRIAS ALIMENTICIAS REGIO", "contacto": "", "cargo": "", "tel": "81 8336 4400", "email": "", "web": "", "sector": "Alimentos", "notas": "Ciudad: Nuevo León", "status": "new", "ts": 1776867999945, "lastContact": null, "ultOp": null}, {"id": "pre1039", "empresa": "COMPONENTES ELECTRONICOS MONTERREY", "contacto": "", "cargo": "", "tel": "81 8386 5500", "email": "", "web": "", "sector": "Electrónica", "notas": "Ciudad: Nuevo León", "status": "new", "ts": 1776867998945, "lastContact": null, "ultOp": null}, {"id": "pre1040", "empresa": "SOLUCIONES PLASTICAS DEL NORTE", "contacto": "", "cargo": "", "tel": "81 8336 6600", "email": "", "web": "", "sector": "Plásticos", "notas": "Ciudad: Nuevo León", "status": "new", "ts": 1776867997945, "lastContact": null, "ultOp": null}, {"id": "pre1041", "empresa": "INYECCIONES PLASTICAS DE QUERETARO", "contacto": "", "cargo": "", "tel": "44 2688 3300", "email": "", "web": "", "sector": "Plásticos", "notas": "Ciudad: Querétaro", "status": "new", "ts": 1776867996945, "lastContact": null, "ultOp": null}, {"id": "pre1042", "empresa": "INDUSTRIAS CAZEL", "contacto": "", "cargo": "", "tel": "44 2216 1020", "email": "", "web": "", "sector": "Industrial", "notas": "Ciudad: Querétaro", "status": "new", "ts": 1776867995945, "lastContact": null, "ultOp": null}, {"id": "pre1043", "empresa": "CORRUGADOS Y EMPAQUES QUERETARO", "contacto": "", "cargo": "", "tel": "44 2688 4400", "email": "", "web": "", "sector": "Embalaje", "notas": "Ciudad: Querétaro", "status": "new", "ts": 1776867994945, "lastContact": null, "ultOp": null}, {"id": "pre1044", "empresa": "ALUMINIUM INDUSTRIES CONSTRUCTA", "contacto": "", "cargo": "", "tel": "44 2688 1500", "email": "", "web": "", "sector": "Aluminio / Metal", "notas": "Ciudad: Querétaro", "status": "new", "ts": 1776867993945, "lastContact": null, "ultOp": null}, {"id": "pre1045", "empresa": "ACEROS Y METALES QUERETARO", "contacto": "", "cargo": "", "tel": "44 2688 2200", "email": "", "web": "", "sector": "Acero/Metal", "notas": "Ciudad: Querétaro", "status": "new", "ts": 1776867992945, "lastContact": null, "ultOp": null}, {"id": "pre1046", "empresa": "TRANSFORMACIONES INDUSTRIALES QRO", "contacto": "", "cargo": "", "tel": "44 2688 3300", "email": "", "web": "", "sector": "Industrial", "notas": "Ciudad: Querétaro", "status": "new", "ts": 1776867991945, "lastContact": null, "ultOp": null}, {"id": "pre1047", "empresa": "COMPONENTES AUTOMOTRICES QUERETARO", "contacto": "", "cargo": "", "tel": "44 2688 4400", "email": "", "web": "", "sector": "Automotriz", "notas": "Ciudad: Querétaro", "status": "new", "ts": 1776867990945, "lastContact": null, "ultOp": null}, {"id": "pre1048", "empresa": "QUIMICA INDUSTRIAL QUERETARO", "contacto": "", "cargo": "", "tel": "44 2216 5500", "email": "", "web": "", "sector": "Química", "notas": "Ciudad: Querétaro", "status": "new", "ts": 1776867989945, "lastContact": null, "ultOp": null}, {"id": "pre1049", "empresa": "HERRAJES Y TORNILLERIA QRO", "contacto": "", "cargo": "", "tel": "44 2688 6600", "email": "", "web": "", "sector": "Metal", "notas": "Ciudad: Querétaro", "status": "new", "ts": 1776867988945, "lastContact": null, "ultOp": null}, {"id": "pre1050", "empresa": "PLASTICOS Y MOLDES QUERETARO", "contacto": "", "cargo": "", "tel": "44 2688 7700", "email": "", "web": "", "sector": "Plásticos", "notas": "Ciudad: Querétaro", "status": "new", "ts": 1776867987945, "lastContact": null, "ultOp": null}, {"id": "pre1051", "empresa": "EMPAQUES FLEXIBLES QUERETARO", "contacto": "", "cargo": "", "tel": "44 2216 8800", "email": "", "web": "", "sector": "Embalaje", "notas": "Ciudad: Querétaro", "status": "new", "ts": 1776867986945, "lastContact": null, "ultOp": null}, {"id": "pre1052", "empresa": "METALMECANICA QUERETARO", "contacto": "", "cargo": "", "tel": "44 2688 9900", "email": "", "web": "", "sector": "Acero/Metal", "notas": "Ciudad: Querétaro", "status": "new", "ts": 1776867985945, "lastContact": null, "ultOp": null}, {"id": "pre1053", "empresa": "GRUPO BIMBO", "contacto": "", "cargo": "", "tel": "55 5268 6600", "email": "", "web": "https://www.grupobimbo.com", "sector": "Alimentos / Panificación", "notas": "Ciudad: CDMX", "status": "new", "ts": 1776867984945, "lastContact": null, "ultOp": null}, {"id": "pre1054", "empresa": "MEXICHEM", "contacto": "", "cargo": "", "tel": "55 5279 8000", "email": "", "web": "https://www.mexichem.com", "sector": "Química", "notas": "Ciudad: CDMX", "status": "new", "ts": 1776867983945, "lastContact": null, "ultOp": null}, {"id": "pre1055", "empresa": "GRUPO MODELO", "contacto": "", "cargo": "", "tel": "55 5283 5000", "email": "", "web": "", "sector": "Alimentos / Bebidas", "notas": "Ciudad: CDMX", "status": "new", "ts": 1776867982945, "lastContact": null, "ultOp": null}, {"id": "pre1056", "empresa": "SIGMA ALIMENTOS CDMX", "contacto": "", "cargo": "", "tel": "55 5340 7000", "email": "", "web": "https://www.sigma-alimentos.com", "sector": "Alimentos procesados", "notas": "Ciudad: CDMX", "status": "new", "ts": 1776867981945, "lastContact": null, "ultOp": null}, {"id": "pre1057", "empresa": "BASF MEXICANA", "contacto": "", "cargo": "", "tel": "55 5261 9700", "email": "", "web": "https://www.basf.com/mx", "sector": "Química", "notas": "Ciudad: CDMX", "status": "new", "ts": 1776867980945, "lastContact": null, "ultOp": null}, {"id": "pre1058", "empresa": "BAYER DE MEXICO", "contacto": "", "cargo": "", "tel": "55 5728 3000", "email": "", "web": "https://www.bayer.com.mx", "sector": "Química / Salud", "notas": "Ciudad: CDMX", "status": "new", "ts": 1776867979945, "lastContact": null, "ultOp": null}, {"id": "pre1059", "empresa": "CONDUMEX", "contacto": "", "cargo": "", "tel": "55 5328 5600", "email": "", "web": "https://www.condumex.com.mx", "sector": "Cables / Metal", "notas": "Ciudad: CDMX", "status": "new", "ts": 1776867978945, "lastContact": null, "ultOp": null}, {"id": "pre1060", "empresa": "KALTEX GROUP", "contacto": "", "cargo": "", "tel": "55 5729 3000", "email": "", "web": "https://www.kaltex.com", "sector": "Textil", "notas": "Ciudad: CDMX", "status": "new", "ts": 1776867977945, "lastContact": null, "ultOp": null}, {"id": "pre1061", "empresa": "GRUPO BIO PAPPEL", "contacto": "", "cargo": "", "tel": "55 5227 4400", "email": "", "web": "https://www.biopappel.com", "sector": "Papel / Embalaje", "notas": "Ciudad: CDMX", "status": "new", "ts": 1776867976945, "lastContact": null, "ultOp": null}, {"id": "pre1062", "empresa": "SMURFIT KAPPA MEXICO", "contacto": "", "cargo": "", "tel": "55 5278 7700", "email": "", "web": "https://www.smurfitkappa.com.mx", "sector": "Papel / Embalaje", "notas": "Ciudad: CDMX", "status": "new", "ts": 1776867975945, "lastContact": null, "ultOp": null}, {"id": "pre1063", "empresa": "INDUSTRIAS PENOLES", "contacto": "", "cargo": "", "tel": "55 5279 3000", "email": "", "web": "https://www.penoles.com.mx", "sector": "Minería / Metales", "notas": "Ciudad: CDMX", "status": "new", "ts": 1776867974945, "lastContact": null, "ultOp": null}, {"id": "pre1064", "empresa": "GRUPO MEXICO", "contacto": "", "cargo": "", "tel": "55 1103 5000", "email": "", "web": "https://www.gmexico.com", "sector": "Minería / Cobre", "notas": "Ciudad: CDMX", "status": "new", "ts": 1776867973945, "lastContact": null, "ultOp": null}, {"id": "pre1065", "empresa": "ASOFARMA", "contacto": "", "cargo": "", "tel": "55 5260 5800", "email": "", "web": "https://www.asofarma.com.mx", "sector": "Farmacéutica", "notas": "Ciudad: CDMX", "status": "new", "ts": 1776867972945, "lastContact": null, "ultOp": null}, {"id": "pre1066", "empresa": "SEALED AIR DE MEXICO", "contacto": "", "cargo": "", "tel": "55 5846 7200", "email": "", "web": "https://www.sealedair.com", "sector": "Empaques industriales", "notas": "Ciudad: CDMX", "status": "new", "ts": 1776867971945, "lastContact": null, "ultOp": null}, {"id": "pre1067", "empresa": "ALPLA MEXICO", "contacto": "", "cargo": "", "tel": "55 5386 1500", "email": "", "web": "https://www.alpla.com", "sector": "Plásticos / Envases", "notas": "Ciudad: CDMX", "status": "new", "ts": 1776867970945, "lastContact": null, "ultOp": null}];
    localStorage.setItem('mip_v3', JSON.stringify(seed));
  }
})();

cargar();
cargarOps();
cargarLog();
cargarRem();
renderLista();
renderDescubrir();
updateRemBadge();

</script>

</body>
</html>
