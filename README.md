<!doctype html>
<html lang="en">
<head>
<meta charset="utf-8"/>
<meta name="viewport" content="width=device-width,initial-scale=1"/>
<title>Octahedron ☌ Alphabetic Square — All-Axis Event Projection</title>
<style>
:root{
  --bg:#0e1017; --panel:#141827; --panel2:#0e1322; --ink:#e7ebf5; --muted:#9aa3b2;
  --line:#242b42; --accent:#67e8f9; --accent2:#a78bfa; --good:#34d399; --warn:#f59e0b; --bad:#ef4444;
  --radius:14px; --shadow:0 10px 24px rgba(0,0,0,.32);
}
*{box-sizing:border-box}
html,body{height:100%}
body{margin:0; background:linear-gradient(180deg,var(--bg),#0a0c14 60%); color:var(--ink);
  font:14.5px/1.45 system-ui,-apple-system,Segoe UI,Roboto,Ubuntu,Cantarell,Noto Sans,Arial}
.wrap{max-width:1300px; margin:22px auto 36px; padding:0 16px}
header{display:flex; align-items:center; justify-content:space-between; gap:12px; margin-bottom:14px}
h1{margin:0; font-size:20px; letter-spacing:.2px} .sub{color:var(--muted); font-size:13px}
.grid{display:grid; grid-template-columns: 1fr 360px; gap:16px}
@media (max-width:1160px){.grid{grid-template-columns:1fr}}
.card{background:linear-gradient(180deg,var(--panel),var(--panel2)); border:1px solid #1f2337;
  border-radius:var(--radius); box-shadow:var(--shadow)}
.toolbar{padding:12px; display:grid; gap:10px; grid-template-columns: repeat(4, minmax(160px,1fr));
  border-bottom:1px solid #1f2337; border-radius:var(--radius) var(--radius) 0 0}
@media (max-width:960px){.toolbar{grid-template-columns:1fr 1fr}}
.group{display:flex; gap:8px; align-items:center}
select,input,button,textarea{background:#111526; color:var(--ink); border:1px solid #263053; border-radius:10px; padding:8px 10px; font:inherit}
select:focus,input:focus,textarea:focus{outline:none; border-color:#3b82f6}
.btn{cursor:pointer; background:linear-gradient(180deg,#1b2546,#151a2a); border-color:#2c365a}
.board{padding:12px}
.board-inner{position:relative; border:1px solid #20253a; border-radius:12px; padding:10px; background:linear-gradient(180deg,#111629,#0e1324)}
.canvas-row{display:grid; grid-template-columns:1fr; gap:10px}
.main-canvas{width:100%; height:auto; display:block}
.mini-grid{display:grid; grid-template-columns: repeat(3, 1fr); gap:8px}
.mini{background:#0e1426; border:1px solid #20263a; border-radius:10px; padding:6px}
.mini h4{margin:4px 6px 6px; font-size:12px; color:var(--muted)}
.side-pickers{display:grid; grid-template-columns: repeat(4,1fr); gap:8px; padding:10px; border-top:1px solid #1f2337}
.picker{border:1px solid #20263a; border-radius:12px; padding:8px}
.picker h3{margin:0 0 8px; font-size:13px}
.ticks{display:flex; flex-wrap:wrap; gap:4px}
.tick{width:22px; height:22px; display:grid; place-items:center; background:#131a30; border:1px solid #2a3252; border-radius:6px; cursor:pointer; user-select:none}
.tick:hover{border-color:#3a4470} .tick.active{border-color:var(--accent); outline:1px solid #35d6ff; background:#0f1a26}
.legend{padding:10px 12px; border-top:1px solid #1f2337; color:var(--muted); font-size:12.5px; border-radius:0 0 var(--radius) var(--radius)}
.panel{padding:12px; display:grid; gap:12px}
.panel h3{margin:2px 0 0; font-size:14px}
.pills{display:flex; flex-wrap:wrap; gap:6px}
.pill{display:inline-block; padding:2px 8px; border:1px solid #273055; border-radius:999px; font-size:12px; color:#cfe3ff}
.events{max-height:340px; overflow:auto; border:1px solid #1d2338; border-radius:10px}
table{width:100%; border-collapse:collapse; font-size:13px}
th,td{padding:8px 10px; border-bottom:1px solid #192033; text-align:left}
th{position:sticky; top:0; background:#12172a; z-index:1}
.mono{font-family:ui-monospace,SFMono-Regular,Menlo,Consolas,"Liberation Mono","Courier New",monospace}
.right{text-align:right}
.small{font-size:12px} .muted{color:var(--muted)}
hr.sep{border:none; border-top:1px solid #1f2337; margin:2px 0}
.kv{display:grid; grid-template-columns: 120px 1fr; gap:6px; font-size:13px}
.stat{display:flex; align-items:center; justify-content:space-between; gap:10px; padding:6px 8px; border:1px solid #1f2337; border-radius:10px}
.stat b{font-weight:700}
.bad{color:#fecaca} .good{color:#bbf7d0}
</style>
</head>
<body>
<div class="wrap">
  <header>
    <div>
      <h1>Octahedron ☌ Alphabetic Square — All-Axis Event Projection</h1>
      <div class="sub">Four planes (Mass, Momentum, Velocity, Time). A–Z per plane. One click → the same event appears on every pair-plot.</div>
    </div>
    <div class="sub">Self-contained • Offline • No libs</div>
  </header>

  <div class="grid">
    <!-- LEFT: canvases -->
    <section class="card">
      <div class="toolbar">
        <div class="group">
          <label class="small muted">Main X</label>
          <select id="mainX">
            <option>Mass</option><option>Momentum</option><option selected>Velocity</option><option>Time</option>
          </select>
        </div>
        <div class="group">
          <label class="small muted">Main Y</label>
          <select id="mainY">
            <option selected>Mass</option><option>Momentum</option><option>Velocity</option><option>Time</option>
          </select>
        </div>
        <div class="group">
          <label class="small muted">Value mode</label>
          <select id="mode">
            <option selected>Octahedron — Protonic (m=p+t; E=p+v+t)</option>
            <option>Custom JS: f(i,j,k,l)</option>
          </select>
        </div>
        <div class="group">
          <input id="expr" class="mono" title="JS expression using i,j,k,l (0..25)"
                 value="(i+1)*(j+1) + (k+1)+(l+1)"/>
        </div>
        <div class="group">
          <button id="btnPNG" class="btn">Export main PNG</button>
          <button id="btnJSON" class="btn">Export JSON</button>
          <button id="btnClear" class="btn">Clear events</button>
        </div>
      </div>

      <div class="board">
        <div class="board-inner">
          <div class="canvas-row">
            <canvas id="main" class="main-canvas" width="900" height="900" aria-label="Main grid"></canvas>
            <div class="mini-grid">
              <div class="mini"><h4 id="hMM">Mass × Momentum</h4><canvas id="cMM" width="320" height="320"></canvas></div>
              <div class="mini"><h4 id="hMV">Mass × Velocity</h4><canvas id="cMV" width="320" height="320"></canvas></div>
              <div class="mini"><h4 id="hMT">Mass × Time</h4><canvas id="cMT" width="320" height="320"></canvas></div>
              <div class="mini"><h4 id="hPV">Momentum × Velocity</h4><canvas id="cPV" width="320" height="320"></canvas></div>
              <div class="mini"><h4 id="hPT">Momentum × Time</h4><canvas id="cPT" width="320" height="320"></canvas></div>
              <div class="mini"><h4 id="hVT">Velocity × Time</h4><canvas id="cVT" width="320" height="320"></canvas></div>
            </div>
          </div>
        </div>
      </div>

      <div class="side-pickers">
        <div class="picker">
          <h3>Mass</h3><div id="ticksM" class="ticks"></div>
        </div>
        <div class="picker">
          <h3>Momentum</h3><div id="ticksP" class="ticks"></div>
        </div>
        <div class="picker">
          <h3>Velocity</h3><div id="ticksV" class="ticks"></div>
        </div>
        <div class="picker">
          <h3>Time</h3><div id="ticksT" class="ticks"></div>
        </div>
      </div>

      <div class="legend">
        Click anywhere on the main grid to create an **event**. The same event is projected onto all six pair-plots.
        Mode “Octahedron — Protonic” uses your equations <span class="mono">m=p+t</span>, <span class="mono">p=m+v+t</span>,
        <span class="mono">v=m+p+t</span>, <span class="mono">E=p+v+t</span> on normalized A–Z indices.
      </div>
    </section>

    <!-- RIGHT: inspector / events -->
    <aside class="card panel">
      <div>
        <h3>Current selections</h3>
        <div class="pills">
          <span class="pill" id="badgeM">M: A</span>
          <span class="pill" id="badgeP">Mo: A</span>
          <span class="pill" id="badgeV">V: A</span>
          <span class="pill" id="badgeT">T: A</span>
        </div>
        <div class="kv mono" style="margin-top:8px">
          <span class="muted">Main mapping</span><span id="badgeMap">Velocity ⟂ Mass</span>
          <span class="muted">Value mode</span><span id="badgeMode">Octahedron — Protonic</span>
        </div>
      </div>

      <div>
        <h3>Event inspector</h3>
        <div class="stat mono"><span>Letters</span><b id="evtLetters">A,A,A,A</b></div>
        <div class="stat mono"><span>Indices (0..25)</span><b id="evtIdx">0,0,0,0</b></div>
        <div class="stat mono"><span>Normalized (0..1)</span><b id="evtNorm">0,0,0,0</b></div>
        <hr class="sep"/>
        <div class="stat mono"><span>m = p + t</span><b id="ev_m" class="good">0.0000</b></div>
        <div class="stat mono"><span>p = m + v + t</span><b id="ev_p" class="good">0.0000</b></div>
        <div class="stat mono"><span>v = m + p + t</span><b id="ev_v" class="good">0.0000</b></div>
        <div class="stat mono"><span>E_event = p + v + t</span><b id="ev_E" class="good">0.0000</b></div>
        <div class="small muted">Numbers use normalized A–Z (A=0 … Z=1). Clamp at 1 for display.</div>
      </div>

      <div>
        <h3>Events</h3>
        <div class="events">
          <table>
            <thead><tr><th>#</th><th>Letters (M,Mo,V,T)</th><th class="right">Value</th><th>Actions</th></tr></thead>
            <tbody id="evBody"></tbody>
          </table>
        </div>
        <div class="small muted">Each event stores four letters, indices, normalized values, and the computed scalar.</div>
      </div>
    </aside>
  </div>
</div>

<script>
(() => {
  // ======== Core sets ========
  const LETTERS = Array.from({length:26}, (_,i)=>String.fromCharCode(65+i)); // A..Z
  const PLANES = ["Mass","Momentum","Velocity","Time"];

  // ======== State ========
  const S = {
    sel: { Mass:0, Momentum:0, Velocity:0, Time:0 }, // indices 0..25 for each plane
    mapX: "Velocity",
    mapY: "Mass",
    mode: "Octahedron",
    expr: "(i+1)*(j+1) + (k+1)+(l+1)",
    events: [],
    lastEvent: null
  };

  // ======== DOM ========
  const main = document.getElementById("main");
  const ctxMain = main.getContext("2d");
  const miniPairs = [
    {id:"cMM", titleEl:"hMM", x:"Mass", y:"Momentum"},
    {id:"cMV", titleEl:"hMV", x:"Mass", y:"Velocity"},
    {id:"cMT", titleEl:"hMT", x:"Mass", y:"Time"},
    {id:"cPV", titleEl:"hPV", x:"Momentum", y:"Velocity"},
    {id:"cPT", titleEl:"hPT", x:"Momentum", y:"Time"},
    {id:"cVT", titleEl:"hVT", x:"Velocity", y:"Time"},
  ].map(p=>{
    p.canvas = document.getElementById(p.id);
    p.ctx = p.canvas.getContext("2d");
    p.title = document.getElementById(p.titleEl);
    return p;
  });

  // Controls
  const mainX = document.getElementById("mainX");
  const mainY = document.getElementById("mainY");
  const mode = document.getElementById("mode");
  const expr = document.getElementById("expr");
  const btnPNG = document.getElementById("btnPNG");
  const btnJSON = document.getElementById("btnJSON");
  const btnClear = document.getElementById("btnClear");
  const ticksM = document.getElementById("ticksM");
  const ticksP = document.getElementById("ticksP");
  const ticksV = document.getElementById("ticksV");
  const ticksT = document.getElementById("ticksT");

  // Badges
  const badgeM = document.getElementById("badgeM");
  const badgeP = document.getElementById("badgeP");
  const badgeV = document.getElementById("badgeV");
  const badgeT = document.getElementById("badgeT");
  const badgeMap = document.getElementById("badgeMap");
  const badgeMode = document.getElementById("badgeMode");

  // Inspector
  const evLetters = document.getElementById("evtLetters");
  const evIdx = document.getElementById("evtIdx");
  const evNorm = document.getElementById("evtNorm");
  const ev_m = document.getElementById("ev_m");
  const ev_p = document.getElementById("ev_p");
  const ev_v = document.getElementById("ev_v");
  const ev_E = document.getElementById("ev_E");
  const evBody = document.getElementById("evBody");

  // ======== Utils ========
  const clamp = (x,a,b)=> Math.max(a, Math.min(b,x));
  const norm = i => i/25; // A..Z → 0..1
  const denorm = u => clamp(Math.round(u*25),0,25);

  function colorScale(v,minV,maxV){
    if (!isFinite(v)) return "#212844";
    if (maxV===minV) return "#67e8f9";
    const t = (v-minV)/(maxV-minV);
    const r = Math.round(40 + 215*t);
    const g = Math.round(180 + 50*(1-t));
    const b = Math.round(255 - 155*t);
    return `rgb(${r},${g},${b})`;
  }

  function compileExpr(s){
    try{ return new Function("i","j","k","l","return ("+s+");"); }
    catch(e){ console.warn("Bad expression; fallback", e); return (i,j,k,l)=>(i+1)*(j+1)+(k+1)+(l+1); }
  }

  // ======== Octahedron Protonic evaluator ========
  // Using your equations on normalized indices (uM,uP,uV,uT in 0..1)
  function octahedronScalar(i,j,k,l, xPlane, yPlane){
    // i,j are grid coords on (xPlane,yPlane); k,l are the other planes' fixed indices
    const idx = {
      [xPlane]: i,
      [yPlane]: j,
      ...otherIndexMap(xPlane,yPlane,k,l)
    };
    const uM = norm(idx.Mass), uP = norm(idx.Momentum), uV = norm(idx.Velocity), uT = norm(idx.Time);

    // Protonic relations (working theory map on normalized ledger)
    // m = p + t ; p = m + v + t ; v = m + p + t ; E = p + v + t
    // We display clamped sums; for color scalar choose E_event as representative.
    const m_hat = clamp(uP + uT, 0, 1);
    const p_hat = clamp(uM + uV + uT, 0, 1);
    const v_hat = clamp(uM + uP + uT, 0, 1);
    const E_event = clamp(uP + uV + uT, 0, 1);

    return {scalar: E_event, m_hat, p_hat, v_hat, uM,uP,uV,uT};
  }

  function otherIndexMap(x,y,k,l){
    const rest = PLANES.filter(p=>p!==x && p!==y);
    const o = {}; o[rest[0]] = k; o[rest[1]] = l; return o;
  }

  // ======== Rendering ========
  function renderTicks(host, planeKey){
    host.innerHTML = "";
    LETTERS.forEach((L,idx)=>{
      const div = document.createElement("div");
      div.className = "tick" + (S.sel[planeKey]===idx ? " active":"");
      div.textContent = L;
      div.title = planeKey + " = " + L;
      div.addEventListener("click", ()=>{
        S.sel[planeKey] = idx;
        updateBadges();
        renderAll();
      });
      host.appendChild(div);
    });
  }

  function drawGrid(canvas, xPlane, yPlane, showEventMarkers=true){
    const ctx = canvas.getContext("2d");
    const N = 26;
    // HiDPI fit (canvas already has fixed px size; we'll draw into it)
    const W = canvas.width, H = canvas.height;
    const cw = W/N, ch = H/N;

    // Precompute values for color normalization
    let minV= Infinity, maxV = -Infinity;
    const vals = new Float32Array(N*N);
    const fCustom = compileExpr(S.expr);

    // Other planes fixed indices when sweeping x/y
    const others = PLANES.filter(p=>p!==xPlane && p!==yPlane);
    const k = S.sel[others[0]];
    const l = S.sel[others[1]];

    let t=0;
    for(let j=0;j<N;j++){
      for(let i=0;i<N;i++){
        let val;
        if (S.mode==="Octahedron"){
          val = octahedronScalar(i,j,k,l,xPlane,yPlane).scalar;
        } else {
          val = Number(fCustom(i,j,k,l));
        }
        vals[t++] = val;
        if (isFinite(val)){ if (val<minV) minV=val; if (val>maxV) maxV=val; }
      }
    }

    // Background
    const grad = ctx.createLinearGradient(0,0,0,H);
    grad.addColorStop(0,"#12192b"); grad.addColorStop(1,"#0f1526");
    ctx.fillStyle = grad; ctx.fillRect(0,0,W,H);

    // Cells
    t=0;
    for(let j=0;j<N;j++){
      for(let i=0;i<N;i++){
        const col = colorScale(vals[t++], minV, maxV);
        ctx.fillStyle = col;
        ctx.fillRect(i*cw, j*ch, cw, ch);
      }
    }

    // Grid lines
    ctx.strokeStyle = "rgba(255,255,255,.06)"; ctx.lineWidth = 1;
    for(let i=0;i<=N;i++){
      const x = Math.round(i*cw)+.5, y = Math.round(i*ch)+.5;
      ctx.beginPath(); ctx.moveTo(x,0); ctx.lineTo(x,H); ctx.stroke();
      ctx.beginPath(); ctx.moveTo(0,y); ctx.lineTo(W,y); ctx.stroke();
    }

    // Axis letters (bottom/left)
    ctx.fillStyle = "rgba(230,233,242,.8)";
    ctx.font = "12px ui-monospace, SFMono-Regular, Menlo, Consolas, monospace";
    ctx.textAlign = "center"; ctx.textBaseline = "top";
    for(let i=0;i<N;i++){ ctx.fillText(LETTERS[i], i*cw + cw/2, H-16); }
    ctx.save(); ctx.translate(12, H/2); ctx.rotate(-Math.PI/2);
    for(let j=0;j<N;j++){ ctx.fillText(LETTERS[j], 0, -H/2 + j*ch + ch/2); }
    ctx.restore();

    // Event markers
    if (showEventMarkers){
      for(const ev of S.events){
        const ix = ev.idx[xPlane], iy = ev.idx[yPlane];
        const cx = (ix+0.5)*cw, cy = (iy+0.5)*ch;
        ctx.beginPath(); ctx.arc(cx,cy, Math.max(4,Math.min(cw,ch)/4), 0, Math.PI*2);
        ctx.fillStyle = "rgba(255,255,255,.95)"; ctx.fill();
        ctx.lineWidth = 2; ctx.strokeStyle = "#00e7ff"; ctx.stroke();
      }
    }

    // Last event crosshairs (to spotlight "same event" everywhere)
    if (S.lastEvent){
      const ix = S.lastEvent.idx[xPlane], iy = S.lastEvent.idx[yPlane];
      ctx.strokeStyle = "rgba(255,255,255,.18)"; ctx.lineWidth = 2;
      ctx.beginPath(); ctx.moveTo(ix*cw, 0); ctx.lineTo(ix*cw, H); ctx.stroke();
      ctx.beginPath(); ctx.moveTo(0, iy*ch); ctx.lineTo(W, iy*ch); ctx.stroke();
    }
  }

  function renderAll(){
    // Main
    drawGrid(main, S.mapX, S.mapY, true);
    // Minis
    for (const p of miniPairs){
      p.title.textContent = `${p.x} × ${p.y}`;
      drawGrid(p.canvas, p.x, p.y, false);
    }
    renderEvents();
    updateInspector(S.lastEvent || makeCurrentSelectionEvent());
  }

  function updateBadges(){
    badgeM.textContent = "M: " + LETTERS[S.sel.Mass];
    badgeP.textContent = "Mo: " + LETTERS[S.sel.Momentum];
    badgeV.textContent = "V: " + LETTERS[S.sel.Velocity];
    badgeT.textContent = "T: " + LETTERS[S.sel.Time];
    badgeMap.textContent = `${S.mapX} ⟂ ${S.mapY}`;
    badgeMode.textContent = S.mode==="Octahedron" ? "Octahedron — Protonic" : "Custom f(i,j,k,l)";
  }

  // ======== Events list / inspector ========
  function makeCurrentSelectionEvent(){
    const idx = {...S.sel};
    const letters = Object.fromEntries(Object.entries(idx).map(([k,v])=>[k, LETTERS[v]]));
    const u = {Mass:norm(idx.Mass), Momentum:norm(idx.Momentum), Velocity:norm(idx.Velocity), Time:norm(idx.Time)};
    const e = {id: "current", idx, letters, u, value: scalarAt(idx)};
    return e;
  }

  function scalarAt(idx){
    // compute scalar based on current mode for the main mapping, but independent of x/y choice
    const planes = PLANES;
    const kmap = Object.fromEntries(planes.map(p=>[p, idx[p]]));
    if (S.mode==="Octahedron"){
      const {scalar} = octahedronScalar(kmap[S.mapX], kmap[S.mapY],
        ...PLANES.filter(p=>p!==S.mapX && p!==S.mapY).map(p=>kmap[p]), S.mapX, S.mapY);
      return scalar;
    } else {
      const f = compileExpr(S.expr);
      const order = [S.mapX, S.mapY, ...PLANES.filter(p=>p!==S.mapX && p!==S.mapY)];
      const args = order.map(p=>kmap[p]);
      return Number(f(...args));
    }
  }

  function renderEvents(){
    evBody.innerHTML = "";
    S.events.forEach((ev,idx)=>{
      const tr = document.createElement("tr");
      tr.innerHTML = `
        <td>${idx+1}</td>
        <td class="mono">${ev.letters.Mass}, ${ev.letters.Momentum}, ${ev.letters.Velocity}, ${ev.letters.Time}</td>
        <td class="right mono">${Number.isFinite(ev.value) ? ev.value.toFixed(4) : '<span class="bad">NaN</span>'}</td>
        <td>
          <button class="btn small" data-act="goto" data-id="${ev.id}">Go-to</button>
          <button class="btn small" data-act="del" data-id="${ev.id}">Delete</button>
        </td>`;
      evBody.appendChild(tr);
    });

    evBody.querySelectorAll("button").forEach(b=>{
      const act = b.getAttribute("data-act"), id = b.getAttribute("data-id");
      b.addEventListener("click", ()=>{
        if (act==="del"){
          S.events = S.events.filter(e=>e.id!==id);
          if (S.lastEvent && S.lastEvent.id===id) S.lastEvent=null;
          renderAll();
        } else if (act==="goto"){
          const e = S.events.find(x=>x.id===id);
          if (!e) return;
          S.sel = {...e.idx}; // set all four planes to this event's indices
          S.lastEvent = e;
          updateBadges(); renderAll();
        }
      });
    });
  }

  function updateInspector(e){
    const ev = e || makeCurrentSelectionEvent();
    evLetters.textContent = `${ev.letters.Mass}, ${ev.letters.Momentum}, ${ev.letters.Velocity}, ${ev.letters.Time}`;
    evIdx.textContent = `${ev.idx.Mass}, ${ev.idx.Momentum}, ${ev.idx.Velocity}, ${ev.idx.Time}`;
    evNorm.textContent = `${ev.u.Mass.toFixed(2)}, ${ev.u.Momentum.toFixed(2)}, ${ev.u.Velocity.toFixed(2)}, ${ev.u.Time.toFixed(2)}`;

    const uM=ev.u.Mass, uP=ev.u.Momentum, uV=ev.u.Velocity, uT=ev.u.Time;
    const mh = clamp(uP + uT, 0, 1);
    const ph = clamp(uM + uV + uT, 0, 1);
    const vh = clamp(uM + uP + uT, 0, 1);
    const Eh = clamp(uP + uV + uT, 0, 1);

    ev_m.textContent = mh.toFixed(4);
    ev_p.textContent = ph.toFixed(4);
    ev_v.textContent = vh.toFixed(4);
    ev_E.textContent = Eh.toFixed(4);
  }

  // ======== Interaction ========
  function addEventAt(ix, iy){
    // ix/iy are on (mapX,mapY). Other planes use current selections.
    const others = PLANES.filter(p=>p!==S.mapX && p!==S.mapY);
    const idx = {...S.sel};
    idx[S.mapX] = clamp(ix,0,25);
    idx[S.mapY] = clamp(iy,0,25);

    const letters = Object.fromEntries(Object.entries(idx).map(([k,v])=>[k, LETTERS[v]]));
    const u = Object.fromEntries(Object.entries(idx).map(([k,v])=>[k, norm(v)]));
    const value = scalarAt(idx);
    const ev = {id: Date.now()+"-"+Math.random().toString(16).slice(2), idx, letters, u, value};
    S.events.push(ev);
    S.lastEvent = ev;
    renderAll();
  }

  main.addEventListener("click", (e)=>{
    const rect = main.getBoundingClientRect();
    const x = (e.clientX - rect.left) * (main.width/rect.width);
    const y = (e.clientY - rect.top) * (main.height/rect.height);
    const N=26, cw=main.width/N, ch=main.height/N;
    const ix = Math.floor(x/cw), iy = Math.floor(y/ch);
    addEventAt(ix,iy);
  });

  // Controls wiring
  mainX.value = S.mapX; mainY.value = S.mapY;
  mainX.addEventListener("change", ()=>{ S.mapX = mainX.value; if (S.mapX===S.mapY){ // avoid same
      const idx = (PLANES.indexOf(S.mapY)+1)%4; S.mapY = PLANES[idx]; mainY.value = S.mapY; }
    updateBadges(); renderAll(); });
  mainY.addEventListener("change", ()=>{ S.mapY = mainY.value; if (S.mapY===S.mapX){
      const idx = (PLANES.indexOf(S.mapX)+1)%4; S.mapX = PLANES[idx]; mainX.value = S.mapX; }
    updateBadges(); renderAll(); });

  mode.addEventListener("change", ()=>{
    S.mode = mode.value.startsWith("Octahedron") ? "Octahedron" : "Custom";
    updateBadges(); renderAll();
  });
  expr.addEventListener("change", ()=>{ S.expr = expr.value.trim() || "(i+1)*(j+1)+(k+1)+(l+1)"; renderAll(); });

  btnPNG.addEventListener("click", ()=>{
    const link = document.createElement("a");
    link.download = "octahedron_main.png";
    link.href = main.toDataURL("image/png");
    link.click();
  });

  btnJSON.addEventListener("click", ()=>{
    const payload = {sel:S.sel, mapX:S.mapX, mapY:S.mapY, mode:S.mode, expr:S.expr, events:S.events};
    const blob = new Blob([JSON.stringify(payload,null,2)],{type:"application/json"});
    const url = URL.createObjectURL(blob);
    const a = document.createElement("a"); a.href=url; a.download="octahedron_ledger.json"; a.click();
    URL.revokeObjectURL(url);
  });

  btnClear.addEventListener("click", ()=>{ S.events=[]; S.lastEvent=null; renderAll(); });

  // ======== Init ========
  renderTicks(ticksM,"Mass");
  renderTicks(ticksP,"Momentum");
  renderTicks(ticksV,"Velocity");
  renderTicks(ticksT,"Time");
  updateBadges();
  renderAll();

  // HiDPI responsive sizing for main canvas
  function resizeMain(){
    const dpr = window.devicePixelRatio || 1;
    const display = Math.min(main.parentElement.clientWidth-20, 900);
    main.style.width = display+"px"; main.style.height = display+"px";
    main.width = Math.round(display*dpr); main.height = Math.round(display*dpr);
    renderAll();
  }
  resizeMain();
  window.addEventListener("resize", resizeMain);

  // Power users: expose loader
  window.loadLedger = function(jsonLike){
    try{
      const data = typeof jsonLike==="string" ? JSON.parse(jsonLike) : jsonLike;
      if (data.sel) S.sel = data.sel;
      if (data.mapX) S.mapX = data.mapX;
      if (data.mapY) S.mapY = data.mapY;
      if (data.mode) S.mode = data.mode;
      if (data.expr) { S.expr = data.expr; expr.value = S.expr; }
      if (Array.isArray(data.events)) S.events = data.events;
      mainX.value = S.mapX; mainY.value = S.mapY;
      updateBadges(); renderAll();
      console.log("%cLoaded Octahedron ledger.","color:#34d399");
    }catch(err){ console.error("loadLedger failed:", err); }
  };

})();
</script>
</body>
</html>
