<!doctype html>
<html>
<head>
  <meta charset="utf-8">
  <title>Spiritualism Tool ☌</title>
  <style>
    body { font-family: system-ui, sans-serif; margin: 2rem; line-height: 1.6; }
    textarea { width: 100%; height: 120px; margin-bottom: 1rem; }
    button { padding: 0.5rem 1rem; margin-top: 0.5rem; }
    #screen { margin-top: 1.5rem; font-size: 1.2rem; white-space: pre-wrap; border:1px solid #ccc; padding:1rem; border-radius:8px; min-height:6rem; }
    .cursor { display:inline-block; width:0.6ch; background:#000; animation: blink 1s steps(1) infinite; }
    @keyframes blink { 50% { background: transparent } }
  </style>
</head>
<body>
  <h1>Octahedron ☌ Text-Emerge Tool</h1>
  <p>Paste a monologue, press play, and watch it appear word by word with your voice.</p>
  <textarea id="txt" placeholder="Paste your monologue here…"></textarea><br>
  <label>Speed (ms/char): <input id="spd" type="number" value="40"></label><br>
  <button id="play">Play</button>
  <div id="screen"></div>

  <script>
    document.getElementById('play').onclick = async () => {
      const txt = document.getElementById('txt').value;
      const spd = Math.max(1, +document.getElementById('spd').value || 40);
      const scr = document.getElementById('screen');
      scr.textContent = '';
      for (let i=0; i<txt.length; i++) {
        scr.textContent += txt[i];
        await new Promise(r => setTimeout(r, spd));
      }
      scr.insertAdjacentHTML('beforeend','<span class="cursor"></span>');
    };
  </script>
</body>
</html>
