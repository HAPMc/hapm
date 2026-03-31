simple visa calculator. 90 days per 180 days

<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Шенгенский визовый калькулятор</title>
<style>
*{box-sizing:border-box;margin:0;padding:0;}
body{font-family:system-ui,-apple-system,sans-serif;background:#f5f5f3;color:#1a1a1a;padding:24px 16px;}
.wrap{max-width:860px;margin:0 auto;padding:1rem 0;}
h1{font-size:18px;font-weight:500;margin-bottom:1.5rem;color:#1a1a1a;}
.metrics{display:grid;grid-template-columns:repeat(3,1fr);gap:10px;margin-bottom:1.25rem;}
.metric{background:#ebebea;border-radius:8px;padding:14px 12px;}
.m-lbl{font-size:11px;color:#777;text-transform:uppercase;letter-spacing:0.06em;margin-bottom:6px;}
.m-val{font-size:32px;font-weight:500;line-height:1;}
.m-sub{font-size:12px;margin-top:3px;color:#777;}
.c-ok{color:#0F6E56;}.c-warn{color:#BA7517;}.c-over{color:#A32D2D;}

.prog-wrap{margin-bottom:1.25rem;}
.prog-bg{height:6px;background:#ebebea;border-radius:3px;overflow:hidden;border:0.5px solid rgba(0,0,0,0.1);}
.prog-fill{height:100%;border-radius:3px;transition:width 0.2s,background 0.2s;min-width:2px;}
.prog-labels{display:flex;justify-content:space-between;margin-top:3px;font-size:11px;color:#777;}

.sec-hd{font-size:11px;font-weight:500;color:#777;text-transform:uppercase;letter-spacing:0.06em;margin-bottom:8px;}
.tl-section{margin-bottom:1.25rem;}
.tl-bar{position:relative;height:56px;background:#ebebea;border-radius:8px;border:0.5px solid rgba(0,0,0,0.1);overflow:visible;user-select:none;}
.tl-dates{display:flex;justify-content:space-between;margin-top:4px;}
.tl-d{font-size:11px;color:#777;}

.seg{position:absolute;top:8px;height:40px;border-radius:5px;touch-action:none;cursor:grab;}
.seg:active{cursor:grabbing;opacity:0.95;}
.seg-inner{position:absolute;left:8px;right:8px;top:0;bottom:0;display:flex;align-items:center;justify-content:center;overflow:hidden;}
.seg-lbl{font-size:11px;color:rgba(255,255,255,0.95);font-weight:500;white-space:nowrap;pointer-events:none;}
.hndl{position:absolute;top:0;bottom:0;width:9px;cursor:ew-resize;z-index:2;}
.hndl:hover{background:rgba(255,255,255,0.3);}
.hndl-l{left:0;border-radius:5px 0 0 5px;}
.hndl-r{right:0;border-radius:0 5px 5px 0;}
.ck-line{position:absolute;top:-6px;bottom:-6px;width:2px;background:#D85A30;pointer-events:none;z-index:10;}
.ck-lbl{position:absolute;top:-20px;font-size:10px;color:#D85A30;transform:translateX(-50%);pointer-events:none;white-space:nowrap;}
.month-tick{position:absolute;top:0;bottom:0;width:0.5px;background:rgba(0,0,0,0.1);pointer-events:none;}
.month-lbl{position:absolute;top:-16px;font-size:10px;color:#777;transform:translateX(-50%);white-space:nowrap;}

.check-row{display:flex;align-items:center;gap:8px;margin-bottom:1.25rem;font-size:13px;color:#777;}
.check-row input[type=date]{border:0.5px solid rgba(0,0,0,0.2);border-radius:8px;padding:5px 8px;font:inherit;background:#fff;color:#1a1a1a;font-size:13px;}

.form-section{margin-bottom:1.25rem;}
.form-row{display:flex;gap:8px;flex-wrap:wrap;align-items:flex-end;}
.fgrp{display:flex;flex-direction:column;gap:4px;flex:1;min-width:130px;}
.flbl{font-size:12px;color:#777;}
input[type=date]{border:0.5px solid rgba(0,0,0,0.2);border-radius:8px;padding:6px 10px;font:inherit;background:#fff;color:#1a1a1a;font-size:13px;}
button{border:0.5px solid rgba(0,0,0,0.2);border-radius:8px;padding:6px 16px;font:inherit;background:#fff;color:#1a1a1a;cursor:pointer;font-size:13px;}
button:hover{background:#ebebea;}

.stays-section{margin-bottom:1.5rem;}
.stay-row{display:flex;align-items:center;gap:8px;padding:9px 12px;background:#ebebea;border-radius:8px;margin-bottom:6px;flex-wrap:wrap;}
.dot{width:10px;height:10px;border-radius:50%;flex-shrink:0;}
.stay-di{font-size:13px;flex:1;min-width:200px;}
.stay-di input[type=date]{border:none;background:none;font:inherit;color:#1a1a1a;font-size:13px;cursor:pointer;width:110px;padding:0;}
.stay-cnt{font-size:12px;color:#777;margin-right:2px;white-space:nowrap;}
.rm{background:none;border:0.5px solid rgba(0,0,0,0.15);color:#777;cursor:pointer;border-radius:4px;width:24px;height:24px;font-size:15px;display:flex;align-items:center;justify-content:center;flex-shrink:0;padding:0;}
.rm:hover{border-color:#E24B4A;color:#E24B4A;}
.empty-note{font-size:13px;color:#777;padding:8px 0;}

.warn-banner{background:#FAEEDA;border-radius:8px;padding:10px 14px;margin-bottom:1.25rem;font-size:13px;color:#633806;display:none;}
.over-banner{background:#FCEBEB;border-radius:8px;padding:10px 14px;margin-bottom:1.25rem;font-size:13px;color:#501313;display:none;}

/* Calendar */
.cal-section{margin-top:0.5rem;}
.cal-legend{display:flex;gap:12px;flex-wrap:wrap;margin-bottom:10px;align-items:center;}
.leg-item{display:flex;align-items:center;gap:5px;font-size:12px;color:#777;}
.leg-swatch{width:12px;height:12px;border-radius:3px;flex-shrink:0;}
.months-wrap{display:grid;grid-template-columns:repeat(auto-fit,minmax(200px,1fr));gap:16px;}
.cal-grid{display:grid;grid-template-columns:repeat(7,1fr);gap:3px;}
.cal-dow{font-size:11px;color:#777;text-align:center;padding:4px 0;font-weight:500;}
.cal-day{position:relative;aspect-ratio:1;display:flex;align-items:center;justify-content:center;border-radius:6px;font-size:12px;color:#1a1a1a;transition:background 0.1s;}
.cal-day.empty{pointer-events:none;}
.cal-day.out-win{color:#aaa;opacity:0.5;}
.cal-day.in-win{background:#ebebea;}
.cal-day.stay-day{color:#fff!important;font-weight:500;}
.cal-day:not(.empty):hover{outline:0.5px solid rgba(0,0,0,0.2);cursor:pointer;}
.cal-day-num{position:relative;z-index:1;pointer-events:none;}
.cal-tip{position:absolute;bottom:calc(100% + 4px);left:50%;transform:translateX(-50%);background:#fff;border:0.5px solid rgba(0,0,0,0.15);border-radius:6px;padding:4px 8px;font-size:11px;white-space:nowrap;color:#1a1a1a;z-index:99;display:none;pointer-events:none;box-shadow:0 2px 8px rgba(0,0,0,0.08);}
.cal-day:hover .cal-tip{display:block;}
</style>
</head>
<body>
<div class="wrap">
  <h1>Шенгенский визовый калькулятор — 90/180</h1>

  <div class="metrics">
    <div class="metric"><div class="m-lbl">Использовано</div><div class="m-val" id="days-used">0</div><div class="m-sub">из 90 дней</div></div>
    <div class="metric"><div class="m-lbl">Осталось</div><div class="m-val" id="days-rem">90</div><div class="m-sub">дней</div></div>
    <div class="metric"><div class="m-lbl">Статус</div><div class="m-val" id="status-val" style="font-size:20px;padding-top:6px;">ОК</div></div>
  </div>

  <div class="over-banner" id="over-banner">Лимит превышен! Вы провели более 90 дней в Шенгенской зоне в течение 180-дневного периода.</div>
  <div class="warn-banner" id="warn-banner">Внимание: использовано более 75 дней. Скоро достигнете лимита.</div>

  <div class="prog-wrap">
    <div class="prog-bg"><div class="prog-fill" id="prog-fill" style="width:0%;background:#1D9E75;"></div></div>
    <div class="prog-labels"><span>0</span><span>45</span><span>90 дней</span></div>
  </div>

  <div class="check-row">
    <span>Дата проверки:</span>
    <input type="date" id="check-date">
  </div>

  <div class="tl-section">
    <div class="sec-hd">180-дневное окно — бегунок</div>
    <div class="tl-bar" id="tl-bar"></div>
    <div class="tl-dates"><span class="tl-d" id="tl-s"></span><span class="tl-d" id="tl-m"></span><span class="tl-d" id="tl-e"></span></div>
  </div>

  <div class="form-section">
    <div class="sec-hd">Добавить поездку</div>
    <div class="form-row">
      <div class="fgrp"><span class="flbl">Дата въезда</span><input type="date" id="new-start"></div>
      <div class="fgrp"><span class="flbl">Дата выезда</span><input type="date" id="new-end"></div>
      <button onclick="addStay()" style="height:36px;align-self:flex-end;">+ Добавить</button>
    </div>
  </div>

  <div class="stays-section">
    <div class="sec-hd">Поездки</div>
    <div id="stays-list"><p class="empty-note">Поездки не добавлены.</p></div>
  </div>

  <div class="cal-section">
    <div class="sec-hd">Календарь — 180-дневное окно</div>
    <div class="cal-legend">
      <div class="leg-item"><div class="leg-swatch" style="background:#ebebea;border:0.5px solid rgba(0,0,0,0.1);"></div><span>В окне (вне поездки)</span></div>
      <div class="leg-item"><div class="leg-swatch" style="background:#1D9E75;"></div><span>Пребывание</span></div>
      <div class="leg-item"><div class="leg-swatch" style="border:1.5px solid #D85A30;background:none;"></div><span>Дата проверки</span></div>
    </div>
    <div class="months-wrap" id="cal-months"></div>
  </div>
</div>

<script>
const COLORS=['#1D9E75','#7F77DD','#378ADD','#D85A30','#D4537E','#BA7517'];
const MONTHS_RU=['Январь','Февраль','Март','Апрель','Май','Июнь','Июль','Август','Сентябрь','Октябрь','Ноябрь','Декабрь'];
const DOW=['Пн','Вт','Ср','Чт','Пт','Сб','Вс'];
let stays=[],nextId=1,checkDate=today0(),dragState=null;

function today0(){const d=new Date();d.setHours(0,0,0,0);return d;}
function ymd(d){return d.toISOString().slice(0,10);}
function fmtd(d){return d.toLocaleDateString('ru-RU',{day:'2-digit',month:'2-digit',year:'2-digit'});}
function winBounds(cd){const e=new Date(cd);e.setHours(0,0,0,0);const s=new Date(e);s.setDate(s.getDate()-179);return{s,e};}

function daysInWin(cd){
  const{s,e}=winBounds(cd);let tot=0;
  for(const st of stays){
    const a=new Date(Math.max(st.s,s)),b=new Date(Math.min(st.e,e));
    if(a<=b)tot+=Math.round((b-a)/864e5)+1;
  }return tot;
}
function stayLen(st){return Math.round((st.e-st.s)/864e5)+1;}
function getStayForDay(d){
  for(let i=0;i<stays.length;i++){const st=stays[i];if(d>=st.s&&d<=st.e)return{st,i};}return null;
}

function addStay(){
  const sv=document.getElementById('new-start').value,ev=document.getElementById('new-end').value;
  if(!sv||!ev){alert('Выберите обе даты');return;}
  const sd=new Date(sv);sd.setHours(0,0,0,0);
  const ed=new Date(ev);ed.setHours(0,0,0,0);
  if(sd>ed){alert('Дата въезда позже даты выезда');return;}
  stays.push({id:nextId++,s:sd,e:ed});render();
}
function removeStay(id){stays=stays.filter(x=>x.id!==id);render();}
function updateStay(id,field,val){
  const st=stays.find(x=>x.id===id);if(!st)return;
  const d=new Date(val);d.setHours(0,0,0,0);
  if(field==='s'&&d<=st.e)st.s=d;
  else if(field==='e'&&d>=st.s)st.e=d;
  render();
}

function render(){
  const used=daysInWin(checkDate),rem=Math.max(0,90-used),pct=Math.min(100,(used/90)*100);
  const cls=used>90?'c-over':used>75?'c-warn':'c-ok';
  el('days-used').textContent=used;el('days-used').className='m-val '+cls;
  el('days-rem').textContent=rem;el('days-rem').className='m-val '+cls;
  const sv=el('status-val');
  if(used>90){sv.textContent='Превышен';sv.className='m-val c-over';}
  else if(used>75){sv.textContent='Внимание';sv.className='m-val c-warn';}
  else{sv.textContent='ОК';sv.className='m-val c-ok';}
  const pf=el('prog-fill');
  pf.style.width=pct+'%';pf.style.background=used>90?'#A32D2D':used>75?'#BA7517':'#1D9E75';
  el('over-banner').style.display=used>90?'block':'none';
  el('warn-banner').style.display=(used>75&&used<=90)?'block':'none';
  renderTL();renderList();renderCalendar();
}

function renderTL(){
  const bar=el('tl-bar');bar.innerHTML='';
  const{s,e}=winBounds(checkDate);const span=e-s;
  function pct(d){return Math.max(0,Math.min(100,((d-s)/span)*100));}
  let mc=new Date(s);mc.setDate(1);mc.setMonth(mc.getMonth()+1);
  while(mc<=e){
    const p=pct(mc);
    const tick=mk('div','month-tick');tick.style.left=p+'%';
    const lbl=mk('div','month-lbl');lbl.style.left=p+'%';
    lbl.textContent=mc.toLocaleDateString('ru-RU',{month:'short'});
    bar.appendChild(tick);bar.appendChild(lbl);
    mc=new Date(mc);mc.setMonth(mc.getMonth()+1);
  }
  const ckp=pct(checkDate);
  const ckLine=mk('div','ck-line');ckLine.style.left=ckp+'%';
  const ckLbl=mk('div','ck-lbl');ckLbl.style.left=ckp+'%';ckLbl.textContent='сегодня';
  bar.appendChild(ckLbl);bar.appendChild(ckLine);
  stays.forEach((st,i)=>{
    const color=COLORS[i%COLORS.length];
    const ss=new Date(Math.max(st.s,s)),se=new Date(Math.min(st.e,e));
    if(ss>se)return;
    const lp=pct(ss),rp=pct(new Date(se.getTime()+864e5));
    const wp=Math.max(rp-lp,0.4);
    const seg=mk('div','seg');seg.style.left=lp+'%';seg.style.width=wp+'%';seg.style.background=color;seg.dataset.id=st.id;seg.dataset.type='move';
    const hl=mk('div','hndl hndl-l');hl.dataset.id=st.id;hl.dataset.type='left';
    const hr=mk('div','hndl hndl-r');hr.dataset.id=st.id;hr.dataset.type='right';
    const inner=mk('div','seg-inner');inner.dataset.id=st.id;inner.dataset.type='move';
    const lbl=mk('div','seg-lbl');lbl.textContent=stayLen(st)+'д';lbl.dataset.id=st.id;lbl.dataset.type='move';
    inner.appendChild(lbl);seg.appendChild(hl);seg.appendChild(inner);seg.appendChild(hr);bar.appendChild(seg);
  });
  el('tl-s').textContent=fmtd(s);
  el('tl-m').textContent=fmtd(new Date(s.getTime()+span/2));
  el('tl-e').textContent=fmtd(e);
}

function renderList(){
  const list=el('stays-list');
  if(!stays.length){list.innerHTML='<p class="empty-note">Поездки не добавлены.</p>';return;}
  list.innerHTML=stays.map((st,i)=>{
    const color=COLORS[i%COLORS.length];const len=stayLen(st);
    return`<div class="stay-row">
      <div class="dot" style="background:${color}"></div>
      <div class="stay-di">
        <input type="date" value="${ymd(st.s)}" onchange="updateStay(${st.id},'s',this.value)">
        <span style="color:#777">—</span>
        <input type="date" value="${ymd(st.e)}" onchange="updateStay(${st.id},'e',this.value)">
      </div>
      <span class="stay-cnt">${len} дн.</span>
      <button class="rm" onclick="removeStay(${st.id})">×</button>
    </div>`;
  }).join('');
}

function renderCalendar(){
  const{s:winS,e:winE}=winBounds(checkDate);
  const months=[];
  let cur=new Date(winS);cur.setDate(1);
  const last=new Date(winE);last.setDate(1);
  while(cur<=last){months.push(new Date(cur));cur.setMonth(cur.getMonth()+1);}
  const wrap=el('cal-months');wrap.innerHTML='';
  months.forEach(m=>wrap.appendChild(buildMonth(m,winS,winE)));
}

function buildMonth(m,winS,winE){
  const year=m.getFullYear(),month=m.getMonth();
  const container=mk('div','');container.style.cssText='min-width:0;';
  const hdr=mk('div','');
  hdr.style.cssText='font-size:13px;font-weight:500;color:#1a1a1a;margin-bottom:6px;text-align:center;';
  hdr.textContent=MONTHS_RU[month]+' '+year;container.appendChild(hdr);
  const grid=mk('div','cal-grid');
  DOW.forEach(d=>{const c=mk('div','cal-dow');c.textContent=d;grid.appendChild(c);});
  const firstDay=new Date(year,month,1);
  let dow=(firstDay.getDay()+6)%7;
  for(let i=0;i<dow;i++)grid.appendChild(mk('div','cal-day empty'));
  const daysInMonth=new Date(year,month+1,0).getDate();
  for(let d=1;d<=daysInMonth;d++){
    const date=new Date(year,month,d);date.setHours(0,0,0,0);
    const cell=mk('div','cal-day');
    const inWin=date>=winS&&date<=winE;
    const isCheck=date.getTime()===checkDate.getTime();
    const match=getStayForDay(date);
    if(!inWin)cell.classList.add('out-win');else cell.classList.add('in-win');
    if(match){cell.classList.add('stay-day');cell.style.background=COLORS[match.i%COLORS.length];}
    if(isCheck)cell.style.boxShadow='inset 0 0 0 2px #D85A30';
    if(inWin){
      const tip=mk('div','cal-tip');
      let txt=fmtd(date);
      if(match)txt+=` · Поездка ${match.i+1} (${stayLen(match.st)} дн.)`;
      if(isCheck)txt+=' · Дата проверки';
      tip.textContent=txt;cell.appendChild(tip);
    }
    const num=mk('div','cal-day-num');num.textContent=d;cell.appendChild(num);grid.appendChild(cell);
  }
  container.appendChild(grid);return container;
}

const bar=document.getElementById('tl-bar');
bar.addEventListener('mousedown',startDrag);
bar.addEventListener('touchstart',e=>{e.preventDefault();startDrag(e.touches[0]);},{passive:false});
function startDrag(e){
  const t=e.target;const id=parseInt(t.dataset.id);const type=t.dataset.type;
  if(!id||!type)return;
  const st=stays.find(x=>x.id===id);if(!st)return;
  dragState={id,type,startX:e.clientX,origS:new Date(st.s),origE:new Date(st.e),rect:bar.getBoundingClientRect()};
}
document.addEventListener('mousemove',onDrag);
document.addEventListener('touchmove',e=>{if(dragState){e.preventDefault();onDrag(e.touches[0]);}},{passive:false});
function onDrag(e){
  if(!dragState)return;
  const dx=e.clientX-dragState.startX;
  const pxPerDay=dragState.rect.width/179;
  const delta=Math.round(dx/pxPerDay);
  const st=stays.find(x=>x.id===dragState.id);if(!st)return;
  if(dragState.type==='move'){
    const ns=new Date(dragState.origS);ns.setDate(ns.getDate()+delta);
    const ne=new Date(dragState.origE);ne.setDate(ne.getDate()+delta);
    st.s=ns;st.e=ne;
  }else if(dragState.type==='left'){
    const ns=new Date(dragState.origS);ns.setDate(ns.getDate()+delta);
    if(ns<=st.e)st.s=ns;
  }else if(dragState.type==='right'){
    const ne=new Date(dragState.origE);ne.setDate(ne.getDate()+delta);
    if(ne>=st.s)st.e=ne;
  }
  render();
}
document.addEventListener('mouseup',()=>dragState=null);
document.addEventListener('touchend',()=>dragState=null);

const cdInp=document.getElementById('check-date');
cdInp.value=ymd(checkDate);
cdInp.addEventListener('change',()=>{const d=new Date(cdInp.value);d.setHours(0,0,0,0);checkDate=d;render();});

function el(id){return document.getElementById(id);}
function mk(tag,cls){const e=document.createElement(tag);e.className=cls;return e;}

// demo stays
const t=today0();
const s1=new Date(t);s1.setDate(s1.getDate()-45);
const e1=new Date(t);e1.setDate(e1.getDate()-20);
stays.push({id:nextId++,s:s1,e:e1});
const s2=new Date(t);s2.setDate(s2.getDate()-10);
const e2=new Date(t);e2.setDate(e2.getDate()-3);
stays.push({id:nextId++,s:s2,e:e2});
render();
</script>
</body>
</html>
