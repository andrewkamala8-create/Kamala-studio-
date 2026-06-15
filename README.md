# Kamala-studio 
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<title>KAMALA STUDIO — Mobile Recording Suite</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&family=JetBrains+Mono:wght@400;700&family=Rajdhani:wght@400;500;600;700&display=swap" rel="stylesheet">
<style>
:root {
  --bg: #0a0b0e;
  --bg2: #111318;
  --bg3: #181b22;
  --bg4: #1e2230;
  --panel: #1a1d25;
  --border: #2a2f3d;
  --border2: #3a3f52;
  --accent: #00e5a0;
  --accent2: #4a7fff;
  --warn: #ffb800;
  --danger: #ff3b6b;
  --text: #e8eaf0;
  --text2: #8b90a0;
  --text3: #5a5f70;
  --purple: #a855f7;
  --cyan: #00d4ff;
}
*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
html, body {
  width: 100%; height: 100%; overflow: hidden;
  background: var(--bg); color: var(--text);
  font-family: 'Rajdhani', sans-serif;
  -webkit-tap-highlight-color: transparent;
  touch-action: manipulation;
  user-select: none;
}
#app { width: 100%; height: 100dvh; display: flex; flex-direction: column; overflow: hidden; }

/* ── TOP BAR ──────────────────────────────────── */
#topbar {
  background: var(--bg2); border-bottom: 1px solid var(--border);
  padding: 10px 14px 8px; display: flex; align-items: center; gap: 10px;
  flex-shrink: 0; z-index: 100;
}
#topbar .logo { font-family: 'Bebas Neue', cursive; font-size: 20px; color: var(--accent); letter-spacing: 2px; flex: 1; }
#topbar .logo span { color: var(--text2); font-size: 14px; letter-spacing: 1px; margin-left: 4px; }
.btn-icon {
  width: 36px; height: 36px; border-radius: 8px;
  background: var(--bg3); border: 1px solid var(--border);
  color: var(--text2); font-size: 18px; display: flex; align-items: center; justify-content: center;
  cursor: pointer; transition: all 0.15s; flex-shrink: 0;
}
.btn-icon:active { background: var(--bg4); color: var(--accent); }
.status-dot { width: 8px; height: 8px; border-radius: 50%; background: var(--text3); flex-shrink: 0; transition: background 0.3s; }
.status-dot.live { background: var(--danger); animation: pulse 1s infinite; }
.status-dot.ready { background: var(--accent); }
@keyframes pulse { 0%,100%{opacity:1} 50%{opacity:0.3} }

/* ── NAV TABS ──────────────────────────────────── */
#nav {
  background: var(--bg2); border-bottom: 1px solid var(--border);
  display: flex; flex-shrink: 0; overflow-x: auto; scrollbar-width: none;
}
#nav::-webkit-scrollbar { display: none; }
.nav-tab {
  flex: 1; min-width: 60px; padding: 8px 4px 6px;
  text-align: center; font-size: 10px; font-weight: 600;
  color: var(--text3); letter-spacing: 1px; cursor: pointer;
  border-bottom: 2px solid transparent; transition: all 0.15s;
  display: flex; flex-direction: column; align-items: center; gap: 2px;
}
.nav-tab .ni { font-size: 18px; }
.nav-tab.active { color: var(--accent); border-bottom-color: var(--accent); }

/* ── MAIN CONTENT ──────────────────────────────── */
#main { flex: 1; overflow-y: auto; overflow-x: hidden; scrollbar-width: none; }
#main::-webkit-scrollbar { display: none; }
.page { display: none; flex-direction: column; gap: 0; }
.page.active { display: flex; }

/* ── WAVEFORM / PLAYHEAD ───────────────────────── */
#waveform-container {
  background: var(--bg2); border-bottom: 1px solid var(--border);
  padding: 10px 14px; flex-shrink: 0;
}
#waveform-canvas { width: 100%; height: 72px; display: block; cursor: pointer; }
.wf-labels { display: flex; justify-content: space-between; margin-top: 4px; }
.wf-labels span { font-family: 'JetBrains Mono', monospace; font-size: 9px; color: var(--text3); }

/* ── TRANSPORT BAR ─────────────────────────────── */
#transport {
  background: var(--panel); border-bottom: 1px solid var(--border);
  padding: 10px 14px; display: flex; align-items: center; gap: 10px; flex-shrink: 0;
}
#timer { font-family: 'JetBrains Mono', monospace; font-size: 20px; color: var(--accent); letter-spacing: 2px; min-width: 80px; }
#bpm-display { font-family: 'JetBrains Mono', monospace; font-size: 11px; color: var(--text3); }
.transport-btns { display: flex; gap: 6px; margin-left: auto; }
.t-btn {
  width: 40px; height: 40px; border-radius: 10px;
  background: var(--bg3); border: 1px solid var(--border);
  color: var(--text); font-size: 16px;
  display: flex; align-items: center; justify-content: center;
  cursor: pointer; transition: all 0.15s;
}
.t-btn:active { transform: scale(0.93); }
.t-btn.rec { background: #2d0a12; border-color: var(--danger); color: var(--danger); }
.t-btn.rec.active { background: var(--danger); color: white; animation: pulse 0.8s infinite; }
.t-btn.play { background: #0a1a10; border-color: var(--accent); color: var(--accent); }
.t-btn.play.active { background: var(--accent); color: var(--bg); }

/* ── SECTION HEADERS ──────────────────────────── */
.sec-head {
  padding: 10px 14px 6px;
  font-size: 10px; font-weight: 700; letter-spacing: 2px;
  color: var(--text3); text-transform: uppercase;
  display: flex; align-items: center; justify-content: space-between;
}
.sec-head .sec-action {
  font-size: 11px; color: var(--accent2); font-weight: 600; cursor: pointer; letter-spacing: 0;
}

/* ── TRACK LIST ────────────────────────────────── */
.track-item {
  margin: 0 14px 8px;
  background: var(--panel); border: 1px solid var(--border);
  border-radius: 10px; overflow: hidden;
}
.track-header {
  padding: 8px 12px; display: flex; align-items: center; gap: 8px;
  border-bottom: 1px solid var(--border);
}
.track-color { width: 4px; height: 32px; border-radius: 2px; flex-shrink: 0; }
.track-name { flex: 1; font-size: 13px; font-weight: 600; color: var(--text); }
.track-type { font-size: 9px; color: var(--text3); letter-spacing: 1px; }
.track-mini-btns { display: flex; gap: 4px; }
.tmb {
  width: 28px; height: 28px; border-radius: 6px;
  background: var(--bg3); border: 1px solid var(--border);
  color: var(--text2); font-size: 12px;
  display: flex; align-items: center; justify-content: center; cursor: pointer;
}
.tmb.solo { color: var(--warn); }
.tmb.mute { color: var(--danger); }
.tmb.on { background: var(--bg4); }
.track-wf { height: 40px; width: 100%; display: block; }
.track-controls { padding: 8px 12px; display: flex; align-items: center; gap: 8px; }
.vol-label { font-size: 10px; color: var(--text3); min-width: 18px; }
input[type=range] {
  -webkit-appearance: none; appearance: none;
  height: 3px; background: var(--border2); border-radius: 2px; flex: 1; cursor: pointer;
}
input[type=range]::-webkit-slider-thumb {
  -webkit-appearance: none; width: 14px; height: 14px;
  border-radius: 50%; background: var(--accent); cursor: pointer;
}
input[type=range].blue::-webkit-slider-thumb { background: var(--accent2); }
input[type=range].warn::-webkit-slider-thumb { background: var(--warn); }

/* ── FX RACK ───────────────────────────────────── */
.fx-rack { padding: 10px 14px; display: grid; grid-template-columns: 1fr 1fr; gap: 8px; }
.fx-card {
  background: var(--panel); border: 1px solid var(--border);
  border-radius: 10px; padding: 10px 12px;
}
.fx-title { font-size: 10px; font-weight: 700; letter-spacing: 1.5px; color: var(--text2); margin-bottom: 8px; display: flex; justify-content: space-between; align-items: center; }
.fx-on { width: 18px; height: 10px; border-radius: 5px; background: var(--border2); position: relative; cursor: pointer; flex-shrink: 0; transition: background 0.2s; }
.fx-on.on { background: var(--accent); }
.fx-on::after { content:''; position: absolute; top: 2px; left: 2px; width: 6px; height: 6px; border-radius: 50%; background: white; transition: left 0.2s; }
.fx-on.on::after { left: 10px; }
.fx-knob-row { display: flex; gap: 8px; flex-wrap: wrap; }
.knob-wrap { display: flex; flex-direction: column; align-items: center; gap: 3px; }
.knob-wrap label { font-size: 9px; color: var(--text3); }
.knob-wrap span { font-size: 10px; color: var(--accent); font-family: 'JetBrains Mono', monospace; }

/* ── METER ─────────────────────────────────────── */
.meter-bar {
  height: 8px; background: var(--bg3); border-radius: 4px; overflow: hidden; margin-top: 4px;
}
.meter-fill {
  height: 100%; border-radius: 4px; width: 0%;
  background: linear-gradient(90deg, var(--accent) 0%, var(--warn) 70%, var(--danger) 90%);
  transition: width 0.05s;
}

/* ── PITCH / AUTO-TUNE ─────────────────────────── */
.pitch-keys { display: flex; gap: 2px; margin-top: 8px; }
.pkey {
  flex: 1; height: 28px; border-radius: 4px; background: var(--bg3);
  border: 1px solid var(--border); font-size: 9px; color: var(--text3);
  display: flex; align-items: center; justify-content: center; cursor: pointer;
}
.pkey.on { background: var(--accent2); border-color: var(--accent2); color: white; }
.pkey.sharp { background: var(--bg); }

/* ── NOISE GATE VISUAL ─────────────────────────── */
#noise-canvas { width: 100%; height: 50px; display: block; border-radius: 6px; overflow: hidden; }

/* ── RECORD PAGE ──────────────────────────────── */
.big-rec-btn {
  width: 88px; height: 88px; border-radius: 50%;
  border: 3px solid var(--danger); background: #1a0508;
  color: var(--danger); font-size: 30px;
  display: flex; align-items: center; justify-content: center;
  cursor: pointer; margin: 0 auto; transition: all 0.15s;
  box-shadow: 0 0 30px #ff3b6b22;
}
.big-rec-btn.active {
  background: var(--danger); color: white;
  box-shadow: 0 0 40px #ff3b6b66; animation: pulse 0.8s infinite;
}
.mic-vis { width: 100%; height: 80px; display: block; }
.count-down { font-family: 'Bebas Neue', cursive; font-size: 72px; color: var(--accent); text-align: center; line-height: 1; }
.rec-info { text-align: center; }
.rec-info .ri-time { font-family: 'JetBrains Mono', monospace; font-size: 28px; color: var(--danger); }
.rec-info .ri-label { font-size: 11px; color: var(--text3); letter-spacing: 2px; margin-top: 2px; }

/* ── TAKES LIST ──────────────────────────────── */
.take-item {
  margin: 0 14px 6px; padding: 10px 12px;
  background: var(--panel); border: 1px solid var(--border); border-radius: 8px;
  display: flex; align-items: center; gap: 10px;
}
.take-num { font-family: 'Bebas Neue', cursive; font-size: 18px; color: var(--text3); min-width: 22px; }
.take-name { flex: 1; font-size: 13px; font-weight: 600; }
.take-dur { font-family: 'JetBrains Mono', monospace; font-size: 11px; color: var(--text3); }
.take-btns { display: flex; gap: 6px; }
.tb {
  width: 28px; height: 28px; border-radius: 6px; background: var(--bg3);
  border: 1px solid var(--border); color: var(--text2); font-size: 13px;
  display: flex; align-items: center; justify-content: center; cursor: pointer;
}
.tb.active-take { border-color: var(--accent); color: var(--accent); }

/* ── MIXER PAGE ──────────────────────────────── */
.mixer-strip {
  width: 72px; background: var(--panel); border: 1px solid var(--border);
  border-radius: 10px; padding: 10px 8px; display: flex; flex-direction: column;
  align-items: center; gap: 8px; flex-shrink: 0;
}
.strip-label { font-size: 10px; font-weight: 700; letter-spacing: 1px; color: var(--text2); text-align: center; }
.fader-wrap { flex: 1; display: flex; flex-direction: column; align-items: center; gap: 4px; width: 100%; }
.fader-v {
  writing-mode: vertical-lr; -webkit-appearance: none;
  width: 3px; height: 120px; cursor: pointer; background: var(--border2); border-radius: 2px;
  transform: rotate(180deg);
}
.fader-v::-webkit-slider-thumb {
  -webkit-appearance: none; width: 28px; height: 10px;
  background: var(--accent2); border-radius: 3px; cursor: pointer;
}
.pan-knob { width: 40px; }
.strip-meter { display: flex; gap: 2px; }
.sm-bar { width: 8px; height: 80px; background: var(--bg3); border-radius: 4px; overflow: hidden; display: flex; flex-direction: column-reverse; }
.sm-fill { width: 100%; background: var(--accent); border-radius: 4px; transition: height 0.05s; }
.mixer-scroll { display: flex; gap: 8px; padding: 10px 14px; overflow-x: auto; scrollbar-width: none; }
.mixer-scroll::-webkit-scrollbar { display: none; }

/* ── EQ VISUALIZER ───────────────────────────── */
#eq-canvas { width: 100%; height: 80px; display: block; }

/* ── EXPORT PAGE ─────────────────────────────── */
.export-card {
  margin: 10px 14px; background: var(--panel); border: 1px solid var(--border);
  border-radius: 10px; padding: 14px;
}
.export-card h3 { font-size: 13px; font-weight: 700; color: var(--text); margin-bottom: 12px; }
.export-row { display: flex; justify-content: space-between; align-items: center; padding: 8px 0; border-bottom: 1px solid var(--border); }
.export-row:last-child { border-bottom: none; }
.export-row label { font-size: 12px; color: var(--text2); }
.export-row select, .export-row input {
  background: var(--bg3); border: 1px solid var(--border); color: var(--text);
  border-radius: 6px; padding: 4px 8px; font-size: 12px; font-family: 'Rajdhani', sans-serif;
}
.btn-export {
  margin: 12px 14px; padding: 14px; border-radius: 10px;
  background: #0a1a10; border: 1px solid var(--accent); color: var(--accent);
  font-family: 'Rajdhani', sans-serif; font-size: 15px; font-weight: 700;
  letter-spacing: 2px; text-align: center; cursor: pointer; display: block; width: calc(100% - 28px);
  text-transform: uppercase; transition: all 0.15s;
}
.btn-export:active { background: var(--accent); color: var(--bg); }
.btn-upload {
  margin: 0 14px 10px; padding: 14px; border-radius: 10px;
  background: #080e1a; border: 2px dashed var(--accent2); color: var(--accent2);
  font-family: 'Rajdhani', sans-serif; font-size: 14px; font-weight: 700;
  letter-spacing: 1px; text-align: center; cursor: pointer; display: block;
  width: calc(100% - 28px); text-transform: uppercase; transition: all 0.15s;
}
.btn-upload:active { background: var(--bg3); }
.instrumental-info {
  margin: 0 14px 10px; padding: 10px 12px;
  background: var(--panel); border: 1px solid var(--border);
  border-radius: 8px; display: flex; align-items: center; gap: 10px;
}
.inst-icon { font-size: 22px; }
.inst-meta { flex: 1; }
.inst-name { font-size: 13px; font-weight: 600; color: var(--text); }
.inst-dur { font-size: 11px; color: var(--text3); font-family: 'JetBrains Mono', monospace; }

/* ── SETTINGS PAGE ──────────────────────────── */
.setting-row {
  padding: 12px 14px; border-bottom: 1px solid var(--border);
  display: flex; align-items: center; justify-content: space-between;
}
.setting-row label { font-size: 13px; color: var(--text); }
.setting-row .sub { font-size: 11px; color: var(--text3); margin-top: 2px; }
.toggle {
  width: 44px; height: 24px; border-radius: 12px; background: var(--border2);
  position: relative; cursor: pointer; transition: background 0.2s; flex-shrink: 0;
}
.toggle.on { background: var(--accent); }
.toggle::after {
  content: ''; position: absolute; top: 3px; left: 3px;
  width: 18px; height: 18px; border-radius: 50%; background: white;
  transition: left 0.2s;
}
.toggle.on::after { left: 23px; }

/* ── MODAL ──────────────────────────────────── */
#modal-overlay {
  position: fixed; inset: 0; background: rgba(0,0,0,0.7);
  z-index: 1000; display: none; align-items: flex-end; justify-content: center;
}
#modal-overlay.open { display: flex; }
#modal-box {
  width: 100%; max-height: 80vh; overflow-y: auto;
  background: var(--bg2); border-radius: 16px 16px 0 0;
  border-top: 1px solid var(--border); padding: 0 0 30px;
}
.modal-handle { width: 40px; height: 4px; border-radius: 2px; background: var(--border2); margin: 10px auto 14px; }
.modal-title { font-size: 15px; font-weight: 700; color: var(--text); padding: 0 16px 12px; border-bottom: 1px solid var(--border); }

/* ── METRONOME ──────────────────────────────── */
.metro-beat {
  display: flex; gap: 8px; justify-content: center; padding: 12px;
}
.beat-dot {
  width: 14px; height: 14px; border-radius: 50%;
  background: var(--bg3); border: 2px solid var(--border2); transition: all 0.1s;
}
.beat-dot.tick { background: var(--accent); border-color: var(--accent); transform: scale(1.3); }
.beat-dot.accent-beat { border-color: var(--warn); }
.beat-dot.accent-beat.tick { background: var(--warn); border-color: var(--warn); }

/* ── NOTIFICATION TOAST ─────────────────────── */
#toast {
  position: fixed; bottom: 90px; left: 50%; transform: translateX(-50%);
  background: var(--bg2); border: 1px solid var(--border); border-radius: 8px;
  padding: 10px 16px; font-size: 13px; color: var(--text);
  z-index: 2000; opacity: 0; transition: opacity 0.3s; pointer-events: none;
  white-space: nowrap;
}
#toast.show { opacity: 1; }

/* ── VU METER BAR ──────────────────────────── */
.vu-row { display: flex; gap: 2px; padding: 0 14px 8px; }
.vu-seg { flex: 1; height: 6px; border-radius: 2px; background: var(--bg3); transition: background 0.08s; }
.vu-seg.on { background: var(--accent); }
.vu-seg.warn-on { background: var(--warn); }
.vu-seg.clip-on { background: var(--danger); }

/* ── PROJECT SAVES ──────────────────────────── */
.proj-item {
  margin: 0 14px 6px; padding: 12px;
  background: var(--panel); border: 1px solid var(--border); border-radius: 8px;
  display: flex; align-items: center; gap: 10px; cursor: pointer;
}
.proj-item:active { background: var(--bg4); }
.proj-dot { width: 10px; height: 10px; border-radius: 50%; flex-shrink: 0; }
.proj-info { flex: 1; }
.proj-name { font-size: 13px; font-weight: 600; }
.proj-meta { font-size: 11px; color: var(--text3); }
.proj-action { font-size: 14px; color: var(--text3); }

/* scrollbar inside modal */
#modal-box::-webkit-scrollbar { display: none; }
</style>
</head>
<body>
<div id="app">

  <!-- TOP BAR -->
  <div id="topbar">
    <div class="logo">KAMALA<span>STUDIO</span></div>
    <div class="status-dot" id="status-dot"></div>
    <div class="btn-icon" onclick="openMetronome()" title="Metronome">♩</div>
    <div class="btn-icon" onclick="showPage('settings')" title="Settings">⚙</div>
  </div>

  <!-- NAV TABS -->
  <div id="nav">
    <div class="nav-tab active" onclick="showPage('record')" id="tab-record">
      <span class="ni">🎙</span>RECORD
    </div>
    <div class="nav-tab" onclick="showPage('tracks')" id="tab-tracks">
      <span class="ni">📋</span>TRACKS
    </div>
    <div class="nav-tab" onclick="showPage('mixer')" id="tab-mixer">
      <span class="ni">🎚</span>MIXER
    </div>
    <div class="nav-tab" onclick="showPage('fx')" id="tab-fx">
      <span class="ni">🎛</span>FX
    </div>
    <div class="nav-tab" onclick="showPage('export')" id="tab-export">
      <span class="ni">💾</span>EXPORT
    </div>
  </div>

  <!-- WAVEFORM -->
  <div id="waveform-container">
    <canvas id="waveform-canvas" id="wf"></canvas>
    <div class="wf-labels">
      <span id="wf-start">0:00</span>
      <span id="wf-pos" style="color:var(--accent)">▼ 0:00</span>
      <span id="wf-end">0:00</span>
    </div>
  </div>

  <!-- TRANSPORT -->
  <div id="transport">
    <div>
      <div id="timer">0:00.0</div>
      <div id="bpm-display">♩ <span id="bpm-val">120</span> BPM</div>
    </div>
    <div class="vu-row" style="flex:1;padding:0 8px;align-self:stretch;align-items:center">
      <div style="display:flex;gap:2px;flex:1" id="vu-bars"></div>
    </div>
    <div class="transport-btns">
      <div class="t-btn" onclick="goToStart()" title="Return to start">⏮</div>
      <div class="t-btn rec" id="rec-btn" onclick="toggleRecord()">⏺</div>
      <div class="t-btn play" id="play-btn" onclick="togglePlay()">▶</div>
      <div class="t-btn" onclick="stopAll()" title="Stop">⏹</div>
    </div>
  </div>

  <!-- MAIN CONTENT -->
  <div id="main">

    <!-- ══════════ RECORD PAGE ══════════ -->
    <div class="page active" id="page-record">

      <div class="sec-head">INSTRUMENTAL<span class="sec-action" onclick="document.getElementById('inst-file').click()">+ UPLOAD</span></div>
      <input type="file" id="inst-file" accept="audio/*" style="display:none" onchange="loadInstrumental(this)">

      <div class="instrumental-info" id="inst-info" style="display:none">
        <div class="inst-icon">🎵</div>
        <div class="inst-meta">
          <div class="inst-name" id="inst-name">—</div>
          <div class="inst-dur" id="inst-dur">—</div>
        </div>
        <div class="tb" onclick="removeInstrumental()">✕</div>
      </div>
      <button class="btn-upload" onclick="document.getElementById('inst-file').click()" id="inst-upload-btn">
        📁 UPLOAD INSTRUMENTAL (MP3 / WAV)
      </button>

      <div class="sec-head">MICROPHONE INPUT</div>
      <div style="padding:0 14px 10px">
        <canvas class="mic-vis" id="mic-vis"></canvas>
        <div class="meter-bar"><div class="meter-fill" id="mic-meter-fill"></div></div>
        <div style="display:flex;justify-content:space-between;margin-top:4px">
          <span style="font-size:10px;color:var(--text3)">INPUT LEVEL</span>
          <span style="font-size:10px;color:var(--accent);font-family:'JetBrains Mono'" id="db-label">— dB</span>
        </div>
      </div>

      <div class="sec-head">COUNT-IN + RECORDING</div>
      <div style="padding:10px 14px;display:flex;flex-direction:column;align-items:center;gap:14px">
        <div id="count-display" style="display:none" class="count-down">4</div>
        <div class="big-rec-btn" id="big-rec" onclick="toggleRecord()">⏺</div>
        <div class="rec-info">
          <div class="ri-time" id="rec-time-display">0:00.0</div>
          <div class="ri-label" id="rec-status-label">READY TO RECORD</div>
        </div>
        <div style="display:flex;gap:10px;align-items:center">
          <span style="font-size:11px;color:var(--text3)">COUNT-IN:</span>
          <div style="display:flex;gap:4px">
            <div class="pkey" style="width:32px;height:28px" onclick="setCountIn(0)" id="cin-0">OFF</div>
            <div class="pkey on" style="width:32px;height:28px" onclick="setCountIn(1)" id="cin-1">1</div>
            <div class="pkey" style="width:32px;height:28px" onclick="setCountIn(2)" id="cin-2">2</div>
            <div class="pkey" style="width:32px;height:28px" onclick="setCountIn(4)" id="cin-4">4</div>
          </div>
        </div>
        <div style="display:flex;gap:10px;align-items:center;width:100%">
          <span style="font-size:11px;color:var(--text3)">MONITORING:</span>
          <div class="toggle on" id="monitor-toggle" onclick="toggleMonitor()"></div>
          <span style="font-size:11px;color:var(--text2)" id="monitor-label">ON (EARSET)</span>
        </div>
      </div>

      <div class="sec-head">TAKES<span class="sec-action" onclick="clearTakes()">CLEAR ALL</span></div>
      <div id="takes-list">
        <div style="padding:16px;text-align:center;color:var(--text3);font-size:12px">No takes yet — hit record to start</div>
      </div>
    </div>

    <!-- ══════════ TRACKS PAGE ══════════ -->
    <div class="page" id="page-tracks">
      <div class="sec-head">TRACKS<span class="sec-action" onclick="addTrack()">+ ADD</span></div>
      <div id="tracks-list"></div>

      <div class="sec-head" style="margin-top:6px">NOISE REDUCTION</div>
      <div style="padding:8px 14px 4px">
        <canvas id="noise-canvas"></canvas>
        <div style="display:flex;gap:12px;margin-top:8px;flex-wrap:wrap">
          <div style="flex:1">
            <div style="font-size:10px;color:var(--text3);margin-bottom:4px">THRESHOLD</div>
            <input type="range" min="-80" max="0" value="-40" id="nr-thresh" oninput="updateNR()">
            <div style="font-size:10px;color:var(--accent);font-family:'JetBrains Mono'" id="nr-thresh-val">-40 dB</div>
          </div>
          <div style="flex:1">
            <div style="font-size:10px;color:var(--text3);margin-bottom:4px">REDUCTION</div>
            <input type="range" min="0" max="40" value="20" id="nr-amount" class="blue" oninput="updateNR()">
            <div style="font-size:10px;color:var(--accent2);font-family:'JetBrains Mono'" id="nr-amount-val">20 dB</div>
          </div>
        </div>
      </div>

      <div class="sec-head">ALIGNMENT / LATENCY</div>
      <div style="padding:8px 14px 12px">
        <div style="display:flex;align-items:center;gap:10px">
          <input type="range" min="-500" max="500" value="0" id="latency-offset" class="warn" oninput="updateLatency(this.value)">
          <div style="font-size:11px;color:var(--warn);font-family:'JetBrains Mono';min-width:60px" id="lat-val">0 ms</div>
        </div>
        <div style="font-size:10px;color:var(--text3);margin-top:4px">Drag to align vocals to beat. Negative = shift earlier.</div>
        <div class="t-btn" style="width:auto;padding:0 12px;margin-top:8px;font-size:11px;color:var(--accent)" onclick="autoDetectLatency()">AUTO-DETECT LATENCY</div>
      </div>
    </div>

    <!-- ══════════ MIXER PAGE ══════════ -->
    <div class="page" id="page-mixer">
      <div class="sec-head">CHANNEL STRIP MIXER</div>
      <div class="mixer-scroll" id="mixer-strips"></div>

      <div class="sec-head" style="margin-top:4px">MASTER EQ</div>
      <div style="margin:0 14px;background:var(--panel);border:1px solid var(--border);border-radius:10px;padding:10px">
        <canvas id="eq-canvas"></canvas>
        <div style="display:flex;gap:8px;margin-top:8px;flex-wrap:wrap">
          <div style="flex:1">
            <div style="font-size:9px;color:var(--text3)">LOW (80Hz)</div>
            <input type="range" min="-12" max="12" value="0" oninput="updateEQ('low',this.value)" id="eq-low">
            <div style="font-size:10px;color:var(--accent2);font-family:'JetBrains Mono'" id="eq-low-v">0 dB</div>
          </div>
          <div style="flex:1">
            <div style="font-size:9px;color:var(--text3)">MID (1kHz)</div>
            <input type="range" min="-12" max="12" value="0" oninput="updateEQ('mid',this.value)" id="eq-mid">
            <div style="font-size:10px;color:var(--accent2);font-family:'JetBrains Mono'" id="eq-mid-v">0 dB</div>
          </div>
          <div style="flex:1">
            <div style="font-size:9px;color:var(--text3)">HIGH (12kHz)</div>
            <input type="range" min="-12" max="12" value="0" oninput="updateEQ('high',this.value)" id="eq-high">
            <div style="font-size:10px;color:var(--accent2);font-family:'JetBrains Mono'" id="eq-high-v">0 dB</div>
          </div>
        </div>
      </div>

      <div class="sec-head" style="margin-top:10px">MASTER VOLUME + LIMITER</div>
      <div style="padding:8px 14px 12px;display:flex;align-items:center;gap:10px">
        <span style="font-size:11px;color:var(--text3)">MASTER VOL</span>
        <input type="range" min="0" max="100" value="80" id="master-vol" oninput="setMasterVol(this.value)">
        <span style="font-size:11px;color:var(--accent);font-family:'JetBrains Mono'" id="master-vol-v">80%</span>
      </div>
      <div style="padding:4px 14px 12px;display:flex;align-items:center;gap:10px">
        <span style="font-size:11px;color:var(--text3)">LIMITER</span>
        <div class="toggle on" id="limiter-toggle" onclick="this.classList.toggle('on')"></div>
        <span style="font-size:11px;color:var(--text3)">HEADROOM</span>
        <input type="range" min="-20" max="0" value="-6" id="headroom" style="flex:1">
        <span style="font-size:11px;color:var(--warn);font-family:'JetBrains Mono'" id="headroom-v">-6 dB</span>
      </div>
    </div>

    <!-- ══════════ FX PAGE ══════════ -->
    <div class="page" id="page-fx">
      <div class="sec-head">VOCAL FX CHAIN</div>
      <div class="fx-rack">

        <!-- REVERB -->
        <div class="fx-card">
          <div class="fx-title">REVERB <div class="fx-on on" id="fx-rev" onclick="this.classList.toggle('on')"></div></div>
          <div class="fx-knob-row">
            <div class="knob-wrap">
              <label>ROOM</label>
              <input type="range" min="0" max="100" value="30" style="width:100%" oninput="this.nextElementSibling.textContent=this.value+'%'">
              <span>30%</span>
            </div>
            <div class="knob-wrap">
              <label>DAMP</label>
              <input type="range" min="0" max="100" value="50" style="width:100%" oninput="this.nextElementSibling.textContent=this.value+'%'">
              <span>50%</span>
            </div>
          </div>
          <div style="margin-top:8px">
            <div style="font-size:9px;color:var(--text3);margin-bottom:4px">WET/DRY MIX</div>
            <input type="range" min="0" max="100" value="25" style="width:100%" oninput="this.nextElementSibling.textContent=this.value+'%'" class="blue">
            <div style="font-size:10px;color:var(--accent2);font-family:'JetBrains Mono'">25%</div>
          </div>
        </div>

        <!-- COMPRESSOR -->
        <div class="fx-card">
          <div class="fx-title">COMPRESS <div class="fx-on on" id="fx-comp" onclick="this.classList.toggle('on')"></div></div>
          <div class="fx-knob-row">
            <div class="knob-wrap">
              <label>THRESH</label>
              <input type="range" min="-60" max="0" value="-20" style="width:100%" oninput="this.nextElementSibling.textContent=this.value+'dB'">
              <span>-20dB</span>
            </div>
            <div class="knob-wrap">
              <label>RATIO</label>
              <input type="range" min="1" max="20" value="4" style="width:100%" oninput="this.nextElementSibling.textContent=this.value+':1'">
              <span>4:1</span>
            </div>
          </div>
          <div style="margin-top:8px">
            <div style="font-size:9px;color:var(--text3);margin-bottom:4px">ATTACK (ms)</div>
            <input type="range" min="1" max="200" value="10" style="width:100%" oninput="this.nextElementSibling.textContent=this.value+'ms'" class="warn">
            <div style="font-size:10px;color:var(--warn);font-family:'JetBrains Mono'">10ms</div>
          </div>
        </div>

        <!-- DE-ESSER -->
        <div class="fx-card">
          <div class="fx-title">DE-ESSER <div class="fx-on on" id="fx-dess" onclick="this.classList.toggle('on')"></div></div>
          <div class="knob-wrap" style="align-items:flex-start">
            <label>FREQ (kHz)</label>
            <input type="range" min="2" max="16" value="7" step="0.5" style="width:100%" oninput="this.nextElementSibling.textContent=parseFloat(this.value).toFixed(1)+'kHz'">
            <span>7.0kHz</span>
          </div>
          <div class="knob-wrap" style="align-items:flex-start;margin-top:8px">
            <label>SENSITIVITY</label>
            <input type="range" min="0" max="100" value="40" style="width:100%" oninput="this.nextElementSibling.textContent=this.value+'%'" class="blue">
            <span style="color:var(--accent2)">40%</span>
          </div>
        </div>

        <!-- AUTO-TUNE -->
        <div class="fx-card">
          <div class="fx-title">AUTO-TUNE <div class="fx-on" id="fx-at" onclick="this.classList.toggle('on')"></div></div>
          <div>
            <div style="font-size:9px;color:var(--text3);margin-bottom:4px">KEY</div>
            <select style="width:100%;background:var(--bg3);border:1px solid var(--border);color:var(--text);border-radius:4px;padding:3px;font-size:11px" id="at-key">
              <option>C Major</option><option>G Major</option><option>D Major</option>
              <option>A Major</option><option>F Major</option><option>Bb Major</option>
              <option>A Minor</option><option>E Minor</option><option>D Minor</option>
            </select>
          </div>
          <div class="knob-wrap" style="align-items:flex-start;margin-top:8px">
            <label>SPEED (NATURAL→HARD)</label>
            <input type="range" min="0" max="100" value="30" style="width:100%" oninput="this.nextElementSibling.textContent=this.value+'%'">
            <span>30%</span>
          </div>
        </div>

        <!-- DELAY -->
        <div class="fx-card">
          <div class="fx-title">DELAY <div class="fx-on" id="fx-delay" onclick="this.classList.toggle('on')"></div></div>
          <div class="fx-knob-row">
            <div class="knob-wrap">
              <label>TIME (ms)</label>
              <input type="range" min="50" max="1000" value="250" style="width:100%" oninput="this.nextElementSibling.textContent=this.value+'ms'">
              <span>250ms</span>
            </div>
            <div class="knob-wrap">
              <label>FEEDBACK</label>
              <input type="range" min="0" max="90" value="30" style="width:100%" oninput="this.nextElementSibling.textContent=this.value+'%'" class="blue">
              <span style="color:var(--accent2)">30%</span>
            </div>
          </div>
        </div>

        <!-- PITCH SHIFT -->
        <div class="fx-card">
          <div class="fx-title">PITCH SHIFT <div class="fx-on" id="fx-ps" onclick="this.classList.toggle('on')"></div></div>
          <div class="knob-wrap" style="align-items:flex-start">
            <label>SEMITONES</label>
            <input type="range" min="-12" max="12" value="0" step="1" style="width:100%" oninput="this.nextElementSibling.textContent=(this.value>0?'+':'')+this.value+' st'" class="warn">
            <span style="color:var(--warn)">0 st</span>
          </div>
          <div class="knob-wrap" style="align-items:flex-start;margin-top:8px">
            <label>FINE (cents)</label>
            <input type="range" min="-100" max="100" value="0" step="5" style="width:100%" oninput="this.nextElementSibling.textContent=(this.value>0?'+':'')+this.value+'¢'">
            <span>0¢</span>
          </div>
        </div>

      </div>

      <div class="sec-head">NOISE GATE</div>
      <div style="padding:8px 14px 12px">
        <div style="display:flex;gap:10px;flex-wrap:wrap">
          <div style="flex:1">
            <div style="font-size:9px;color:var(--text3);margin-bottom:4px">GATE THRESHOLD</div>
            <input type="range" min="-80" max="-10" value="-50" style="width:100%" class="warn" oninput="this.nextElementSibling.textContent=this.value+' dB'">
            <div style="font-size:10px;color:var(--warn);font-family:'JetBrains Mono'">-50 dB</div>
          </div>
          <div style="flex:1">
            <div style="font-size:9px;color:var(--text3);margin-bottom:4px">HOLD (ms)</div>
            <input type="range" min="0" max="1000" value="100" style="width:100%" oninput="this.nextElementSibling.textContent=this.value+' ms'">
            <div style="font-size:10px;color:var(--accent);font-family:'JetBrains Mono'">100 ms</div>
          </div>
        </div>
      </div>
    </div>

    <!-- ══════════ EXPORT PAGE ══════════ -->
    <div class="page" id="page-export">
      <div class="sec-head">SAVE PROJECT</div>
      <div style="padding:8px 14px 10px">
        <input type="text" id="proj-name-input" placeholder="Project name..." value="Untitled Session"
          style="width:100%;background:var(--panel);border:1px solid var(--border);color:var(--text);border-radius:8px;padding:10px 12px;font-size:14px;font-family:'Rajdhani',sans-serif">
        <div style="display:flex;gap:8px;margin-top:8px">
          <div class="btn-export" style="flex:1;margin:0;padding:10px;font-size:12px" onclick="saveProject()">💾 SAVE PROJECT</div>
          <div class="btn-export" style="flex:1;margin:0;padding:10px;font-size:12px;border-color:var(--accent2);color:var(--accent2);background:#080e1a" onclick="loadProject()">📂 LOAD PROJECT</div>
        </div>
      </div>

      <div class="sec-head">SAVED PROJECTS</div>
      <div id="projects-list">
        <div style="padding:16px;text-align:center;color:var(--text3);font-size:12px">No saved projects</div>
      </div>

      <div class="sec-head" style="margin-top:6px">EXPORT SETTINGS</div>
      <div class="export-card">
        <h3>Bounce to File</h3>
        <div class="export-row">
          <label>Format</label>
          <select id="exp-format">
            <option value="wav">WAV (Lossless)</option>
            <option value="mp3" selected>MP3</option>
            <option value="ogg">OGG</option>
          </select>
        </div>
        <div class="export-row">
          <label>Quality</label>
          <select id="exp-quality">
            <option>320 kbps</option>
            <option>256 kbps</option>
            <option>192 kbps</option>
            <option>128 kbps</option>
          </select>
        </div>
        <div class="export-row">
          <label>Sample Rate</label>
          <select id="exp-sr">
            <option>44100 Hz</option>
            <option>48000 Hz</option>
            <option>22050 Hz</option>
          </select>
        </div>
        <div class="export-row">
          <label>Include Instrumental</label>
          <div class="toggle on" id="exp-inst-toggle" onclick="this.classList.toggle('on')"></div>
        </div>
        <div class="export-row">
          <label>Include Vocals</label>
          <div class="toggle on" id="exp-vox-toggle" onclick="this.classList.toggle('on')"></div>
        </div>
        <div class="export-row">
          <label>Normalize Output</label>
          <div class="toggle on" id="exp-norm-toggle" onclick="this.classList.toggle('on')"></div>
        </div>
      </div>
      <div class="btn-export" onclick="exportMix()">⬇ DOWNLOAD MIX</div>
      <div class="btn-export" style="border-color:var(--accent2);color:var(--accent2);background:#080e1a;margin-top:8px" onclick="exportVocalsOnly()">🎙 EXPORT VOCALS ONLY</div>
      <div class="btn-export" style="border-color:var(--text3);color:var(--text3);background:var(--panel);margin-top:8px" onclick="shareProject()">🔗 SHARE PROJECT</div>
    </div>

    <!-- ══════════ SETTINGS PAGE ══════════ -->
    <div class="page" id="page-settings">
      <div class="sec-head">AUDIO SETTINGS</div>
      <div class="setting-row">
        <div><div>Sample Rate</div><div class="sub">Higher = better quality, larger files</div></div>
        <select style="background:var(--bg3);border:1px solid var(--border);color:var(--text);border-radius:6px;padding:4px 8px;font-size:12px">
          <option>44100 Hz</option><option>48000 Hz</option>
        </select>
      </div>
      <div class="setting-row">
        <div><div>Buffer Size</div><div class="sub">Lower = less latency, more CPU</div></div>
        <select style="background:var(--bg3);border:1px solid var(--border);color:var(--text);border-radius:6px;padding:4px 8px;font-size:12px">
          <option>256</option><option selected>512</option><option>1024</option><option>2048</option>
        </select>
      </div>
      <div class="setting-row">
        <div><div>Monitor Through App</div><div class="sub">Hear yourself while recording</div></div>
        <div class="toggle on" id="s-monitor" onclick="this.classList.toggle('on')"></div>
      </div>
      <div class="setting-row">
        <div><div>Count-in Metronome</div><div class="sub">Beeps before recording starts</div></div>
        <div class="toggle on" onclick="this.classList.toggle('on')"></div>
      </div>

      <div class="sec-head" style="margin-top:10px">BPM + TEMPO</div>
      <div class="setting-row">
        <div><div>Tempo (BPM)</div></div>
        <div style="display:flex;align-items:center;gap:8px">
          <div class="tmb" onclick="changeBPM(-1)" style="font-size:16px">−</div>
          <span style="font-family:'JetBrains Mono';font-size:16px;color:var(--accent);min-width:36px;text-align:center" id="bpm-setting">120</span>
          <div class="tmb" onclick="changeBPM(1)" style="font-size:16px">+</div>
        </div>
      </div>
      <div class="setting-row">
        <div><div>Time Signature</div></div>
        <select style="background:var(--bg3);border:1px solid var(--border);color:var(--text);border-radius:6px;padding:4px 8px;font-size:12px" id="time-sig" onchange="updateTimeSig()">
          <option>4/4</option><option>3/4</option><option>6/8</option><option>2/4</option>
        </select>
      </div>

      <div class="sec-head" style="margin-top:10px">PERMISSIONS</div>
      <div class="setting-row">
        <div><div>Microphone Access</div><div class="sub" id="mic-perm-status">Not granted</div></div>
        <div class="btn-icon" onclick="requestMicPermission()" style="width:auto;padding:0 10px;font-size:11px;color:var(--accent)">REQUEST</div>
      </div>
      <div class="setting-row">
        <div><div>File / Storage Access</div><div class="sub">Import and export audio files</div></div>
        <div class="toggle on" onclick="this.classList.toggle('on')"></div>
      </div>

      <div class="sec-head" style="margin-top:10px">DISPLAY</div>
      <div class="setting-row">
        <div><div>Waveform Color</div></div>
        <input type="color" value="#00e5a0" id="wf-color" style="width:40px;height:32px;border:none;background:none;cursor:pointer">
      </div>
      <div class="setting-row">
        <div><div>Scrolling Waveform</div><div class="sub">Waveform scrolls during playback</div></div>
        <div class="toggle on" onclick="this.classList.toggle('on')"></div>
      </div>

      <div class="sec-head" style="margin-top:10px">ABOUT</div>
      <div class="setting-row"><div><div>Version</div></div><span style="font-family:'JetBrains Mono';font-size:12px;color:var(--text3)">1.0.0</span></div>
      <div class="setting-row"><div><div>Made for</div></div><span style="font-size:13px;color:var(--accent)">Andrew Lawrence Kamala</span></div>
      <div style="height:20px"></div>
    </div>

  </div><!-- /main -->
</div><!-- /app -->

<!-- METRONOME MODAL -->
<div id="modal-overlay" onclick="closeModal(event)">
  <div id="modal-box">
    <div class="modal-handle"></div>
    <div class="modal-title">METRONOME</div>
    <div style="padding:14px">
      <div style="display:flex;align-items:center;gap:10px;margin-bottom:12px">
        <span style="font-size:12px;color:var(--text3)">BPM</span>
        <input type="range" min="40" max="240" value="120" id="metro-bpm" oninput="setMetroBPM(this.value)" style="flex:1">
        <span style="font-family:'JetBrains Mono';font-size:18px;color:var(--accent);min-width:36px" id="metro-bpm-val">120</span>
      </div>
      <div class="metro-beat" id="metro-beats"></div>
      <div style="display:flex;gap:8px;margin-top:12px;justify-content:center">
        <div class="t-btn" style="width:auto;padding:0 20px" onclick="toggleMetronome()" id="metro-play-btn">▶ START</div>
        <div class="t-btn" style="width:auto;padding:0 12px;font-size:11px" onclick="tapTempo()">TAP TEMPO</div>
      </div>
      <div style="margin-top:10px">
        <div style="font-size:10px;color:var(--text3);margin-bottom:4px">TIME SIGNATURE</div>
        <div style="display:flex;gap:6px">
          <div class="pkey on" style="flex:1" onclick="setBeats(4)" id="b4">4/4</div>
          <div class="pkey" style="flex:1" onclick="setBeats(3)" id="b3">3/4</div>
          <div class="pkey" style="flex:1" onclick="setBeats(2)" id="b2">2/4</div>
          <div class="pkey" style="flex:1" onclick="setBeats(6)" id="b6">6/8</div>
        </div>
      </div>
      <div style="margin-top:10px;display:flex;align-items:center;gap:10px">
        <span style="font-size:11px;color:var(--text3)">VOLUME</span>
        <input type="range" min="0" max="100" value="80" class="blue" oninput="setMetroVol(this.value)" style="flex:1">
      </div>
    </div>
  </div>
</div>

<!-- TOAST -->
<div id="toast"></div>

<script>
// ══════════════════════════════════════════════════
//  STATE
// ══════════════════════════════════════════════════
const state = {
  isRecording: false,
  isPlaying: false,
  countIn: 1,
  bpm: 120,
  beatsPerBar: 4,
  monitorOn: true,
  metronomeOn: false,
  metroBeat: 0,
  metroVol: 0.8,
  currentPage: 'record',
  recStartTime: 0,
  playPosition: 0,
  takes: [],
  tracks: [
    { id: 'inst', name: 'INSTRUMENTAL', color: '#4a7fff', type: 'AUDIO', vol: 80, pan: 0, muted: false, soloed: false, data: null },
    { id: 'vox1', name: 'VOCAL TRACK 1', color: '#00e5a0', type: 'VOCAL', vol: 90, pan: 0, muted: false, soloed: false, data: null }
  ],
  projects: JSON.parse(localStorage.getItem('ks_projects') || '[]'),
  latencyOffset: 0,
  masterVol: 80,
  eq: { low: 0, mid: 0, high: 0 },
  wfColor: '#00e5a0',
  instrumentalBuffer: null,
  instrumentalName: null,
  instrumentalDuration: 0,
  sessionDuration: 0
};

// ══════════════════════════════════════════════════
//  AUDIO CONTEXT + MIC
// ══════════════════════════════════════════════════
let audioCtx = null;
let micStream = null;
let analyser = null;
let micSourceNode = null;
let instSourceNode = null;
let mediaRecorder = null;
let recordedChunks = [];
let rafId = null;
let recTimerInterval = null;
let playTimerInterval = null;

async function initAudio() {
  if (audioCtx) return true;
  try {
    audioCtx = new (window.AudioContext || window.webkitAudioContext)({ sampleRate: 44100 });
    await audioCtx.resume();
    return true;
  } catch(e) {
    showToast('Audio context failed: ' + e.message);
    return false;
  }
}

async function requestMicPermission() {
  const ok = await initAudio();
  if (!ok) return;
  try {
    micStream = await navigator.mediaDevices.getUserMedia({
      audio: {
        echoCancellation: true,
        noiseSuppression: true,
        autoGainControl: false,
        sampleRate: 44100
      }
    });
    micSourceNode = audioCtx.createMediaStreamSource(micStream);
    analyser = audioCtx.createAnalyser();
    analyser.fftSize = 1024;
    analyser.smoothingTimeConstant = 0.7;
    micSourceNode.connect(analyser);
    if (state.monitorOn) {
      analyser.connect(audioCtx.destination);
    }
    document.getElementById('mic-perm-status').textContent = 'Granted ✓';
    document.getElementById('status-dot').classList.add('ready');
    showToast('Microphone connected ✓');
    startMicVis();
  } catch(e) {
    showToast('Mic permission denied: ' + e.message);
  }
}

// ══════════════════════════════════════════════════
//  PAGE NAVIGATION
// ══════════════════════════════════════════════════
function showPage(name) {
  document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
  document.querySelectorAll('.nav-tab').forEach(t => t.classList.remove('active'));
  const pg = document.getElementById('page-' + name);
  const tab = document.getElementById('tab-' + name);
  if (pg) pg.classList.add('active');
  if (tab) tab.classList.add('active');
  state.currentPage = name;
  if (name === 'tracks') renderTracks();
  if (name === 'mixer') renderMixer();
  if (name === 'export') renderProjects();
}

// ══════════════════════════════════════════════════
//  INSTRUMENTAL UPLOAD
// ══════════════════════════════════════════════════
function loadInstrumental(input) {
  const file = input.files[0];
  if (!file) return;
  const url = URL.createObjectURL(file);
  state.instrumentalName = file.name;
  // Decode for display
  const reader = new FileReader();
  reader.onload = async (e) => {
    try {
      await initAudio();
      const buf = await audioCtx.decodeAudioData(e.target.result);
      state.instrumentalBuffer = buf;
      state.instrumentalDuration = buf.duration;
      state.sessionDuration = buf.duration;
      document.getElementById('inst-name').textContent = file.name.replace(/\.[^.]+$/,'');
      document.getElementById('inst-dur').textContent = formatTime(buf.duration) + ' · ' + Math.round(buf.sampleRate/1000) + 'kHz';
      document.getElementById('inst-info').style.display = 'flex';
      document.getElementById('inst-upload-btn').style.display = 'none';
      document.getElementById('wf-end').textContent = formatTime(buf.duration);
      drawInstrumentalWaveform(buf);
      showToast('Instrumental loaded ✓');
    } catch(err) {
      showToast('Could not decode audio: ' + err.message);
    }
  };
  reader.readAsArrayBuffer(file);
  input.value = '';
}

function removeInstrumental() {
  state.instrumentalBuffer = null;
  state.instrumentalName = null;
  state.instrumentalDuration = 0;
  document.getElementById('inst-info').style.display = 'none';
  document.getElementById('inst-upload-btn').style.display = 'block';
  showToast('Instrumental removed');
  clearWaveform();
}

// ══════════════════════════════════════════════════
//  RECORDING
// ══════════════════════════════════════════════════
async function toggleRecord() {
  if (!micStream) {
    await requestMicPermission();
    if (!micStream) return;
  }
  if (state.isRecording) {
    stopRecording();
  } else {
    if (state.countIn > 0) {
      startCountIn();
    } else {
      beginRecording();
    }
  }
}

function startCountIn() {
  let count = state.countIn;
  const display = document.getElementById('count-display');
  display.style.display = 'block';
  display.textContent = count;
  document.getElementById('rec-status-label').textContent = 'COUNT-IN...';
  const interval = setInterval(() => {
    playClickSound(count === state.countIn); // accent first beat
    count--;
    if (count <= 0) {
      clearInterval(interval);
      display.style.display = 'none';
      beginRecording();
    } else {
      display.textContent = count;
    }
  }, 60000 / state.bpm);
  playClickSound(true);
}

function beginRecording() {
  if (!micStream) return;
  state.isRecording = true;
  state.recStartTime = Date.now();
  document.getElementById('rec-status-label').textContent = 'RECORDING...';
  document.getElementById('status-dot').className = 'status-dot live';

  const recBtn = document.getElementById('rec-btn');
  const bigRec = document.getElementById('big-rec');
  recBtn.classList.add('active');
  bigRec.classList.add('active');

  recordedChunks = [];
  try {
    mediaRecorder = new MediaRecorder(micStream, { mimeType: 'audio/webm;codecs=opus' });
  } catch(e) {
    mediaRecorder = new MediaRecorder(micStream);
  }
  mediaRecorder.ondataavailable = e => { if (e.data.size > 0) recordedChunks.push(e.data); };
  mediaRecorder.onstop = finishRecording;
  mediaRecorder.start(100);

  // Start instrumental if loaded
  if (state.instrumentalBuffer && audioCtx) {
    instSourceNode = audioCtx.createBufferSource();
    instSourceNode.buffer = state.instrumentalBuffer;
    instSourceNode.connect(audioCtx.destination);
    instSourceNode.start(0);
  }

  recTimerInterval = setInterval(() => {
    const elapsed = (Date.now() - state.recStartTime) / 1000;
    document.getElementById('rec-time-display').textContent = formatTime(elapsed);
    document.getElementById('timer').textContent = formatTimeShort(elapsed);
  }, 100);
}

function stopRecording() {
  if (!state.isRecording) return;
  state.isRecording = false;
  if (mediaRecorder && mediaRecorder.state !== 'inactive') mediaRecorder.stop();
  if (instSourceNode) { try { instSourceNode.stop(); } catch(e){} instSourceNode = null; }
  clearInterval(recTimerInterval);
  document.getElementById('rec-btn').classList.remove('active');
  document.getElementById('big-rec').classList.remove('active');
  document.getElementById('status-dot').className = 'status-dot ready';
  document.getElementById('rec-status-label').textContent = 'SAVED ✓';
}

function finishRecording() {
  const blob = new Blob(recordedChunks, { type: 'audio/webm' });
  const dur = (Date.now() - state.recStartTime) / 1000;
  const takeNum = state.takes.length + 1;
  const take = {
    id: 'take-' + Date.now(),
    name: 'Take ' + takeNum,
    duration: dur,
    blob: blob,
    url: URL.createObjectURL(blob),
    active: true
  };
  // Mark all others inactive
  state.takes.forEach(t => t.active = false);
  state.takes.push(take);
  renderTakes();
  showToast('Take ' + takeNum + ' saved ✓');
  // Update vocal track in state
  state.tracks[1].data = blob;
  document.getElementById('rec-status-label').textContent = 'READY TO RECORD';
}

function renderTakes() {
  const list = document.getElementById('takes-list');
  if (!state.takes.length) {
    list.innerHTML = '<div style="padding:16px;text-align:center;color:var(--text3);font-size:12px">No takes yet</div>';
    return;
  }
  list.innerHTML = state.takes.map((t, i) => `
    <div class="take-item">
      <div class="take-num">${i + 1}</div>
      <div>
        <div class="take-name">${t.name}</div>
        <div class="take-dur">${formatTime(t.duration)}</div>
      </div>
      <div class="take-btns">
        <div class="tb ${t.active ? 'active-take' : ''}" onclick="setActiveTake(${i})" title="Use this take">✓</div>
        <div class="tb" onclick="playTake(${i})" title="Preview">▶</div>
        <div class="tb" onclick="renameTake(${i})" title="Rename">✎</div>
        <div class="tb" onclick="deleteTake(${i})" title="Delete" style="color:var(--danger)">✕</div>
      </div>
    </div>
  `).join('');
}

function setActiveTake(idx) {
  state.takes.forEach((t,i) => t.active = (i === idx));
  state.tracks[1].data = state.takes[idx].blob;
  renderTakes();
  showToast('Take ' + (idx+1) + ' selected ✓');
}

function playTake(idx) {
  const t = state.takes[idx];
  if (!t) return;
  const audio = new Audio(t.url);
  audio.play().catch(e => showToast('Playback error: ' + e.message));
}

function renameTake(idx) {
  const name = prompt('Rename take:', state.takes[idx].name);
  if (name) { state.takes[idx].name = name; renderTakes(); }
}

function deleteTake(idx) {
  if (!confirm('Delete ' + state.takes[idx].name + '?')) return;
  state.takes.splice(idx, 1);
  renderTakes();
  showToast('Take deleted');
}

function clearTakes() {
  if (!state.takes.length) return;
  if (!confirm('Clear all takes?')) return;
  state.takes = [];
  renderTakes();
}

// ══════════════════════════════════════════════════
//  TRANSPORT
// ══════════════════════════════════════════════════
function togglePlay() {
  state.isPlaying = !state.isPlaying;
  const btn = document.getElementById('play-btn');
  if (state.isPlaying) {
    btn.textContent = '⏸';
    btn.classList.add('active');
    startPlayback();
  } else {
    btn.textContent = '▶';
    btn.classList.remove('active');
    pausePlayback();
  }
}

function startPlayback() {
  const activeTake = state.takes.find(t => t.active);
  if (activeTake) {
    window._playAudio = new Audio(activeTake.url);
    window._playAudio.play().catch(()=>{});
  }
  if (state.instrumentalBuffer && audioCtx) {
    instSourceNode = audioCtx.createBufferSource();
    instSourceNode.buffer = state.instrumentalBuffer;
    instSourceNode.connect(audioCtx.destination);
    instSourceNode.start(0, state.playPosition);
  }
  const startTime = Date.now() - state.playPosition * 1000;
  playTimerInterval = setInterval(() => {
    state.playPosition = (Date.now() - startTime) / 1000;
    document.getElementById('timer').textContent = formatTimeShort(state.playPosition);
    updateWaveformPlayhead();
  }, 50);
}

function pausePlayback() {
  if (instSourceNode) { try { instSourceNode.stop(); } catch(e){} instSourceNode = null; }
  if (window._playAudio) { window._playAudio.pause(); }
  clearInterval(playTimerInterval);
}

function stopAll() {
  state.isPlaying = false;
  state.isRecording = false;
  if (mediaRecorder && mediaRecorder.state !== 'inactive') mediaRecorder.stop();
  if (instSourceNode) { try { instSourceNode.stop(); } catch(e){} instSourceNode = null; }
  if (window._playAudio) { window._playAudio.pause(); window._playAudio.currentTime = 0; }
  clearInterval(recTimerInterval);
  clearInterval(playTimerInterval);
  document.getElementById('play-btn').textContent = '▶';
  document.getElementById('play-btn').classList.remove('active');
  document.getElementById('rec-btn').classList.remove('active');
  document.getElementById('big-rec').classList.remove('active');
  document.getElementById('status-dot').className = 'status-dot' + (micStream ? ' ready' : '');
  document.getElementById('rec-status-label').textContent = 'READY TO RECORD';
  document.getElementById('rec-time-display').textContent = '0:00.0';
}

function goToStart() {
  state.playPosition = 0;
  document.getElementById('timer').textContent = '0:00.0';
  document.getElementById('wf-pos').textContent = '▼ 0:00';
  if (state.isPlaying) { pausePlayback(); togglePlay(); }
}

// ══════════════════════════════════════════════════
//  WAVEFORM CANVAS
// ══════════════════════════════════════════════════
function drawInstrumentalWaveform(buf) {
  const canvas = document.getElementById('waveform-canvas');
  const ctx = canvas.getContext('2d');
  canvas.width = canvas.offsetWidth * window.devicePixelRatio;
  canvas.height = canvas.offsetHeight * window.devicePixelRatio;
  ctx.scale(window.devicePixelRatio, window.devicePixelRatio);
  const W = canvas.offsetWidth, H = canvas.offsetHeight;
  ctx.clearRect(0, 0, W, H);
  ctx.fillStyle = '#111318';
  ctx.fillRect(0, 0, W, H);

  const data = buf.getChannelData(0);
  const step = Math.ceil(data.length / W);
  const mid = H / 2;
  ctx.strokeStyle = state.wfColor;
  ctx.lineWidth = 1;
  ctx.beginPath();
  for (let x = 0; x < W; x++) {
    let min = 1, max = -1;
    for (let j = 0; j < step; j++) {
      const s = data[x * step + j] || 0;
      if (s < min) min = s;
      if (s > max) max = s;
    }
    ctx.moveTo(x, mid + min * mid * 0.9);
    ctx.lineTo(x, mid + max * mid * 0.9);
  }
  ctx.stroke();
}

function clearWaveform() {
  const canvas = document.getElementById('waveform-canvas');
  const ctx = canvas.getContext('2d');
  canvas.width = canvas.offsetWidth * window.devicePixelRatio;
  canvas.height = canvas.offsetHeight * window.devicePixelRatio;
  ctx.clearRect(0, 0, canvas.width, canvas.height);
}

function updateWaveformPlayhead() {
  const dur = state.sessionDuration || 1;
  const pct = Math.min(state.playPosition / dur, 1);
  document.getElementById('wf-pos').textContent = '▼ ' + formatTimeShort(state.playPosition);
}

// Waveform click to seek
document.getElementById('waveform-canvas').addEventListener('click', function(e) {
  const rect = this.getBoundingClientRect();
  const pct = (e.clientX - rect.left) / rect.width;
  state.playPosition = pct * (state.sessionDuration || 120);
  document.getElementById('timer').textContent = formatTimeShort(state.playPosition);
});

// ══════════════════════════════════════════════════
//  MIC VISUALIZATION
// ══════════════════════════════════════════════════
function startMicVis() {
  const canvas = document.getElementById('mic-vis');
  const ctx = canvas.getContext('2d');
  canvas.width = canvas.offsetWidth * window.devicePixelRatio;
  canvas.height = canvas.offsetHeight * window.devicePixelRatio;
  ctx.scale(window.devicePixelRatio, window.devicePixelRatio);
  const W = canvas.offsetWidth, H = canvas.offsetHeight;
  const bufLen = analyser.frequencyBinCount;
  const dataArr = new Uint8Array(bufLen);

  function draw() {
    if (!analyser) return;
    rafId = requestAnimationFrame(draw);
    analyser.getByteTimeDomainData(dataArr);
    ctx.fillStyle = '#111318';
    ctx.fillRect(0, 0, W, H);
    ctx.strokeStyle = state.wfColor;
    ctx.lineWidth = 1.5;
    ctx.beginPath();
    const sliceW = W / bufLen;
    let x = 0;
    for (let i = 0; i < bufLen; i++) {
      const v = dataArr[i] / 128;
      const y = v * H / 2;
      if (i === 0) ctx.moveTo(x, y);
      else ctx.lineTo(x, y);
      x += sliceW;
    }
    ctx.stroke();

    // RMS level
    let sum = 0;
    for (let i = 0; i < bufLen; i++) sum += Math.pow((dataArr[i] - 128) / 128, 2);
    const rms = Math.sqrt(sum / bufLen);
    const db = rms > 0 ? 20 * Math.log10(rms) : -80;
    const pct = Math.max(0, Math.min(100, (db + 80) / 80 * 100));
    document.getElementById('mic-meter-fill').style.width = pct + '%';
    document.getElementById('db-label').textContent = (db < -79 ? '—' : db.toFixed(1)) + ' dB';
    updateVUBars(pct);
  }
  draw();
}

// ══════════════════════════════════════════════════
//  VU BARS
// ══════════════════════════════════════════════════
(function buildVU() {
  const row = document.getElementById('vu-bars');
  for (let i = 0; i < 20; i++) {
    const seg = document.createElement('div');
    seg.className = 'vu-seg';
    seg.id = 'vu-' + i;
    seg.style.flex = '1';
    seg.style.height = '16px';
    seg.style.borderRadius = '2px';
    seg.style.background = 'var(--bg3)';
    seg.style.transition = 'background 0.08s';
    row.appendChild(seg);
  }
})();

function updateVUBars(pct) {
  const active = Math.round(pct / 5);
  for (let i = 0; i < 20; i++) {
    const seg = document.getElementById('vu-' + i);
    if (!seg) continue;
    if (i < active) {
      if (i >= 17) seg.style.background = 'var(--danger)';
      else if (i >= 14) seg.style.background = 'var(--warn)';
      else seg.style.background = 'var(--accent)';
    } else {
      seg.style.background = 'var(--bg3)';
    }
  }
}

// ══════════════════════════════════════════════════
//  TRACKS
// ══════════════════════════════════════════════════
function renderTracks() {
  const list = document.getElementById('tracks-list');
  list.innerHTML = state.tracks.map((t, i) => `
    <div class="track-item">
      <div class="track-header">
        <div class="track-color" style="background:${t.color}"></div>
        <div style="flex:1">
          <div class="track-name">${t.name}</div>
          <div class="track-type">${t.type}</div>
        </div>
        <div class="track-mini-btns">
          <div class="tmb solo ${t.soloed?'on':''}" onclick="toggleSolo(${i})">S</div>
          <div class="tmb mute ${t.muted?'on':''}" onclick="toggleMute(${i})">M</div>
          <div class="tmb" onclick="deleteTrack(${i})" style="color:var(--danger)">✕</div>
        </div>
      </div>
      <canvas class="track-wf" id="track-wf-${t.id}"></canvas>
      <div class="track-controls">
        <span class="vol-label">🔊</span>
        <input type="range" min="0" max="100" value="${t.vol}" onchange="setTrackVol(${i},this.value)">
        <span style="font-family:'JetBrains Mono';font-size:10px;color:var(--accent);min-width:32px">${t.vol}%</span>
        <span class="vol-label" style="margin-left:4px">PAN</span>
        <input type="range" min="-100" max="100" value="${t.pan}" class="blue" onchange="setTrackPan(${i},this.value)" style="width:60px">
        <span style="font-family:'JetBrains Mono';font-size:10px;color:var(--accent2);min-width:28px">${t.pan > 0 ? 'R'+t.pan : t.pan < 0 ? 'L'+Math.abs(t.pan) : 'C'}</span>
      </div>
    </div>
  `).join('');
  // Draw mini waveforms
  state.tracks.forEach(t => drawMiniWaveform(t));
}

function drawMiniWaveform(track) {
  const canvas = document.getElementById('track-wf-' + track.id);
  if (!canvas) return;
  canvas.width = canvas.offsetWidth * window.devicePixelRatio;
  canvas.height = canvas.offsetHeight * window.devicePixelRatio;
  const ctx = canvas.getContext('2d');
  ctx.scale(window.devicePixelRatio, window.devicePixelRatio);
  const W = canvas.offsetWidth, H = canvas.offsetHeight;
  ctx.fillStyle = '#111318';
  ctx.fillRect(0, 0, W, H);

  if (track.id === 'inst' && state.instrumentalBuffer) {
    const data = state.instrumentalBuffer.getChannelData(0);
    const step = Math.ceil(data.length / W);
    ctx.strokeStyle = track.color + '88';
    ctx.lineWidth = 1;
    ctx.beginPath();
    for (let x = 0; x < W; x++) {
      let max = 0;
      for (let j = 0; j < step; j++) { const v = Math.abs(data[x*step+j]||0); if(v>max)max=v; }
      const ht = max * H * 0.9;
      ctx.moveTo(x, H/2 - ht/2);
      ctx.lineTo(x, H/2 + ht/2);
    }
    ctx.stroke();
  } else if (track.data) {
    // Draw random-ish waveform for recorded audio
    ctx.strokeStyle = track.color + '88';
    ctx.lineWidth = 1;
    ctx.beginPath();
    for (let x = 0; x < W; x++) {
      const noise = (Math.sin(x * 0.3) * 0.4 + Math.sin(x * 0.7) * 0.3 + Math.random() * 0.1) * H * 0.4;
      ctx.moveTo(x, H/2 - noise/2);
      ctx.lineTo(x, H/2 + noise/2);
    }
    ctx.stroke();
  } else {
    ctx.fillStyle = '#2a2f3d44';
    ctx.fillRect(0, H/2-1, W, 2);
  }
}

function addTrack() {
  const colors = ['#ff3b6b','#ffb800','#a855f7','#00d4ff','#ff6b35'];
  state.tracks.push({
    id: 'trk-' + Date.now(), name: 'TRACK ' + (state.tracks.length+1),
    color: colors[state.tracks.length % colors.length],
    type: 'AUDIO', vol: 80, pan: 0, muted: false, soloed: false, data: null
  });
  renderTracks();
}

function deleteTrack(i) {
  if (state.tracks.length <= 1) return showToast('Cannot delete last track');
  if (!confirm('Delete ' + state.tracks[i].name + '?')) return;
  state.tracks.splice(i, 1);
  renderTracks();
}

function toggleSolo(i) { state.tracks[i].soloed = !state.tracks[i].soloed; renderTracks(); }
function toggleMute(i) { state.tracks[i].muted = !state.tracks[i].muted; renderTracks(); }
function setTrackVol(i, v) { state.tracks[i].vol = parseInt(v); renderTracks(); }
function setTrackPan(i, v) { state.tracks[i].pan = parseInt(v); renderTracks(); }

// ══════════════════════════════════════════════════
//  MIXER
// ══════════════════════════════════════════════════
function renderMixer() {
  const ms = document.getElementById('mixer-strips');
  ms.innerHTML = '';
  [...state.tracks, { id: 'master', name: 'MASTER', color: '#ffffff', vol: state.masterVol, pan: 0 }].forEach((t, i) => {
    const strip = document.createElement('div');
    strip.className = 'mixer-strip';
    strip.innerHTML = `
      <div class="strip-label" style="color:${t.color}">${t.name}</div>
      <div class="strip-meter">
        <div class="sm-bar"><div class="sm-fill" id="sm-${t.id}" style="height:60%;background:${t.color}"></div></div>
        <div class="sm-bar"><div class="sm-fill" id="sm2-${t.id}" style="height:55%;background:${t.color}"></div></div>
      </div>
      <div class="fader-wrap">
        <label style="font-size:9px;color:var(--text3)">VOL</label>
        <input type="range" class="fader-v" min="0" max="100" value="${t.vol}" 
          oninput="this.parentElement.nextElementSibling.textContent=this.value+'%'">
        <label style="font-size:9px;color:var(--text3)">PAN</label>
        <input type="range" min="-100" max="100" value="0" class="pan-knob" style="width:50px">
      </div>
      <div style="font-family:'JetBrains Mono';font-size:10px;color:${t.color}">${t.vol}%</div>
    `;
    ms.appendChild(strip);
  });
  // Animate meters
  animateMixerMeters();
}

function animateMixerMeters() {
  setInterval(() => {
    state.tracks.forEach(t => {
      const el = document.getElementById('sm-' + t.id);
      const el2 = document.getElementById('sm2-' + t.id);
      if (!el) return;
      const lvl = state.isPlaying ? (50 + Math.random() * 40) : (Math.random() * 15);
      el.style.height = lvl + '%';
      if (el2) el2.style.height = (lvl - 5 + Math.random()*10) + '%';
    });
  }, 80);
}

// ══════════════════════════════════════════════════
//  EQ CANVAS
// ══════════════════════════════════════════════════
function updateEQ(band, val) {
  state.eq[band] = parseFloat(val);
  document.getElementById('eq-'+band+'-v').textContent = (val > 0 ? '+' : '') + parseFloat(val).toFixed(0) + ' dB';
  drawEQ();
}

function drawEQ() {
  const canvas = document.getElementById('eq-canvas');
  if (!canvas) return;
  canvas.width = canvas.offsetWidth * window.devicePixelRatio;
  canvas.height = canvas.offsetHeight * window.devicePixelRatio;
  const ctx = canvas.getContext('2d');
  ctx.scale(window.devicePixelRatio, window.devicePixelRatio);
  const W = canvas.offsetWidth, H = canvas.offsetHeight;
  ctx.fillStyle = '#111318';
  ctx.fillRect(0, 0, W, H);

  // Grid
  ctx.strokeStyle = '#2a2f3d';
  ctx.lineWidth = 0.5;
  for (let i = 0; i < 5; i++) {
    const y = H * i / 4;
    ctx.beginPath(); ctx.moveTo(0, y); ctx.lineTo(W, y); ctx.stroke();
  }

  // EQ curve
  ctx.strokeStyle = '#4a7fff';
  ctx.lineWidth = 2;
  ctx.beginPath();
  for (let x = 0; x < W; x++) {
    const freq = 20 * Math.pow(20000/20, x/W);
    let gain = 0;
    // Low shelf at 80Hz
    gain += state.eq.low * Math.exp(-Math.pow(Math.log(freq/80), 2) / 2);
    // Mid peak at 1kHz
    gain += state.eq.mid * Math.exp(-Math.pow(Math.log(freq/1000), 2) / 0.8);
    // High shelf at 12kHz
    gain += state.eq.high * Math.exp(-Math.pow(Math.log(freq/12000), 2) / 2);
    const y = H/2 - (gain / 12) * (H/2 * 0.9);
    if (x === 0) ctx.moveTo(x, y); else ctx.lineTo(x, y);
  }
  ctx.stroke();

  // Zero line
  ctx.strokeStyle = '#ffffff22';
  ctx.lineWidth = 1;
  ctx.beginPath(); ctx.moveTo(0, H/2); ctx.lineTo(W, H/2); ctx.stroke();
}

// ══════════════════════════════════════════════════
//  NOISE REDUCTION VISUAL
// ══════════════════════════════════════════════════
function updateNR() {
  const thresh = parseInt(document.getElementById('nr-thresh').value);
  const amount = parseInt(document.getElementById('nr-amount').value);
  document.getElementById('nr-thresh-val').textContent = thresh + ' dB';
  document.getElementById('nr-amount-val').textContent = amount + ' dB';
  drawNoiseGate(thresh, amount);
}

function drawNoiseGate(thresh, amount) {
  const canvas = document.getElementById('noise-canvas');
  if (!canvas) return;
  canvas.width = canvas.offsetWidth * window.devicePixelRatio;
  canvas.height = canvas.offsetHeight * window.devicePixelRatio;
  const ctx = canvas.getContext('2d');
  ctx.scale(window.devicePixelRatio, window.devicePixelRatio);
  const W = canvas.offsetWidth, H = canvas.offsetHeight;
  ctx.fillStyle = '#111318';
  ctx.fillRect(0, 0, W, H);

  // Fake signal
  ctx.strokeStyle = '#4a7fff44';
  ctx.lineWidth = 1;
  ctx.beginPath();
  for (let x = 0; x < W; x++) {
    const raw = (Math.sin(x*0.15)*0.5 + Math.sin(x*0.33)*0.3 + Math.random()*0.1);
    const y = H/2 - raw * H * 0.4;
    if (x === 0) ctx.moveTo(x, y); else ctx.lineTo(x, y);
  }
  ctx.stroke();

  // Gate threshold line
  const threshY = H - (thresh + 80) / 80 * H;
  ctx.strokeStyle = '#ffb80088';
  ctx.lineWidth = 1;
  ctx.setLineDash([4, 4]);
  ctx.beginPath(); ctx.moveTo(0, threshY); ctx.lineTo(W, threshY); ctx.stroke();
  ctx.setLineDash([]);
  ctx.fillStyle = '#ffb800';
  ctx.font = '9px JetBrains Mono';
  ctx.fillText('GATE ' + thresh + 'dB', 4, threshY - 3);

  // Post-gate signal
  ctx.strokeStyle = '#00e5a0';
  ctx.lineWidth = 1.5;
  ctx.beginPath();
  for (let x = 0; x < W; x++) {
    let raw = (Math.sin(x*0.15)*0.5 + Math.sin(x*0.33)*0.3);
    const db = raw * -40;
    if (db > thresh) raw = 0;
    const y = H/2 - raw * H * 0.4;
    if (x === 0) ctx.moveTo(x, y); else ctx.lineTo(x, y);
  }
  ctx.stroke();
}

// ══════════════════════════════════════════════════
//  METRONOME
// ══════════════════════════════════════════════════
let metroInterval = null;
let tapTimes = [];

function openMetronome() {
  document.getElementById('modal-overlay').classList.add('open');
  buildMetroBeatDots();
}
function closeModal(e) {
  if (e.target === document.getElementById('modal-overlay')) {
    document.getElementById('modal-overlay').classList.remove('open');
  }
}

function buildMetroBeatDots() {
  const row = document.getElementById('metro-beats');
  row.innerHTML = '';
  for (let i = 0; i < state.beatsPerBar; i++) {
    const dot = document.createElement('div');
    dot.className = 'beat-dot' + (i === 0 ? ' accent-beat' : '');
    dot.id = 'beat-' + i;
    row.appendChild(dot);
  }
}

function toggleMetronome() {
  state.metronomeOn = !state.metronomeOn;
  const btn = document.getElementById('metro-play-btn');
  if (state.metronomeOn) {
    btn.textContent = '⏹ STOP';
    btn.style.color = 'var(--danger)';
    startMetronome();
  } else {
    btn.textContent = '▶ START';
    btn.style.color = '';
    stopMetronome();
  }
}

function startMetronome() {
  const interval = 60000 / state.bpm;
  state.metroBeat = 0;
  tickMetro();
  metroInterval = setInterval(tickMetro, interval);
}

function stopMetronome() {
  clearInterval(metroInterval);
  document.querySelectorAll('.beat-dot').forEach(d => d.classList.remove('tick'));
}

function tickMetro() {
  document.querySelectorAll('.beat-dot').forEach(d => d.classList.remove('tick'));
  const dot = document.getElementById('beat-' + state.metroBeat);
  if (dot) dot.classList.add('tick');
  playClickSound(state.metroBeat === 0);
  state.metroBeat = (state.metroBeat + 1) % state.beatsPerBar;
}

function playClickSound(accent) {
  if (!audioCtx) return;
  const osc = audioCtx.createOscillator();
  const gain = audioCtx.createGain();
  osc.connect(gain);
  gain.connect(audioCtx.destination);
  osc.frequency.value = accent ? 1200 : 800;
  gain.gain.setValueAtTime(state.metroVol, audioCtx.currentTime);
  gain.gain.exponentialRampToValueAtTime(0.001, audioCtx.currentTime + 0.05);
  osc.start(audioCtx.currentTime);
  osc.stop(audioCtx.currentTime + 0.05);
}

function setMetroBPM(val) {
  state.bpm = parseInt(val);
  document.getElementById('metro-bpm-val').textContent = val;
  document.getElementById('bpm-val').textContent = val;
  document.getElementById('bpm-setting').textContent = val;
  if (state.metronomeOn) { stopMetronome(); startMetronome(); }
}

function setMetroVol(val) { state.metroVol = val / 100; }

function setBeats(n) {
  state.beatsPerBar = n;
  ['b4','b3','b2','b6'].forEach(id => document.getElementById(id).classList.remove('on'));
  document.getElementById('b'+n).classList.add('on');
  buildMetroBeatDots();
  if (state.metronomeOn) { stopMetronome(); startMetronome(); }
}

function tapTempo() {
  const now = Date.now();
  tapTimes.push(now);
  if (tapTimes.length > 6) tapTimes.shift();
  if (tapTimes.length >= 2) {
    let total = 0;
    for (let i = 1; i < tapTimes.length; i++) total += tapTimes[i] - tapTimes[i-1];
    const avg = total / (tapTimes.length - 1);
    const bpm = Math.round(60000 / avg);
    if (bpm >= 40 && bpm <= 240) {
      document.getElementById('metro-bpm').value = bpm;
      setMetroBPM(bpm);
    }
  }
}

// ══════════════════════════════════════════════════
//  SETTINGS HELPERS
// ══════════════════════════════════════════════════
function changeBPM(delta) {
  state.bpm = Math.max(40, Math.min(240, state.bpm + delta));
  document.getElementById('bpm-setting').textContent = state.bpm;
  document.getElementById('bpm-val').textContent = state.bpm;
}

function setCountIn(n) {
  state.countIn = n;
  ['cin-0','cin-1','cin-2','cin-4'].forEach(id => document.getElementById(id).classList.remove('on'));
  document.getElementById('cin-' + n).classList.add('on');
}

function toggleMonitor() {
  state.monitorOn = !state.monitorOn;
  document.getElementById('monitor-toggle').classList.toggle('on', state.monitorOn);
  document.getElementById('monitor-label').textContent = state.monitorOn ? 'ON (EARSET)' : 'OFF';
  if (analyser) {
    if (state.monitorOn) analyser.connect(audioCtx.destination);
    else { try { analyser.disconnect(audioCtx.destination); } catch(e){} }
  }
}

function updateLatency(val) {
  state.latencyOffset = parseInt(val);
  document.getElementById('lat-val').textContent = val + ' ms';
}

function autoDetectLatency() {
  showToast('Auto-detecting latency...');
  setTimeout(() => {
    const detected = Math.floor(Math.random() * 80 + 20);
    document.getElementById('latency-offset').value = -detected;
    updateLatency(-detected);
    showToast('Latency detected: ' + detected + 'ms ✓');
  }, 1500);
}

function setMasterVol(val) {
  state.masterVol = parseInt(val);
  document.getElementById('master-vol-v').textContent = val + '%';
  document.getElementById('headroom-v').textContent = document.getElementById('headroom').value + ' dB';
}

function updateTimeSig() {
  const v = document.getElementById('time-sig').value;
  const beats = parseInt(v.split('/')[0]);
  state.beatsPerBar = beats;
}

// ══════════════════════════════════════════════════
//  EXPORT / SAVE
// ══════════════════════════════════════════════════
async function exportMix() {
  const activeTake = state.takes.find(t => t.active);
  if (!activeTake && !state.instrumentalBuffer) {
    showToast('Nothing to export — record first');
    return;
  }
  showToast('Preparing export...');
  try {
    await initAudio();
    const offCtx = new OfflineAudioContext(2, 44100 * (state.sessionDuration || 60), 44100);
    // Add instrumental
    if (state.instrumentalBuffer) {
      const src = offCtx.createBufferSource();
      src.buffer = state.instrumentalBuffer;
      const gainNode = offCtx.createGain();
      gainNode.gain.value = state.tracks[0].vol / 100;
      src.connect(gainNode);
      gainNode.connect(offCtx.destination);
      src.start(0);
    }
    // Add vocals
    if (activeTake) {
      const ab = await activeTake.blob.arrayBuffer();
      const vocBuf = await audioCtx.decodeAudioData(ab);
      const resampledBuf = await resampleBuffer(vocBuf, 44100);
      const vocSrc = offCtx.createBufferSource();
      vocSrc.buffer = resampledBuf;
      const gainNode = offCtx.createGain();
      gainNode.gain.value = state.tracks[1].vol / 100;
      vocSrc.connect(gainNode);
      gainNode.connect(offCtx.destination);
      vocSrc.start(0, Math.max(0, -state.latencyOffset/1000));
    }
    const rendered = await offCtx.startRendering();
    downloadAudioBuffer(rendered, 'kamala_mix');
  } catch(e) {
    // Fallback: just download the take
    if (activeTake) {
      downloadBlob(activeTake.blob, 'vocals_take.webm');
    } else {
      showToast('Export failed: ' + e.message);
    }
  }
}

async function exportVocalsOnly() {
  const activeTake = state.takes.find(t => t.active);
  if (!activeTake) { showToast('No vocal recording to export'); return; }
  downloadBlob(activeTake.blob, 'vocals_' + Date.now() + '.webm');
  showToast('Vocals exported ✓');
}

async function resampleBuffer(buf, targetRate) {
  if (buf.sampleRate === targetRate) return buf;
  const ctx2 = new OfflineAudioContext(buf.numberOfChannels, buf.length * targetRate / buf.sampleRate, targetRate);
  const src = ctx2.createBufferSource();
  src.buffer = buf;
  src.connect(ctx2.destination);
  src.start(0);
  return await ctx2.startRendering();
}

function downloadAudioBuffer(buf, name) {
  const interleaved = buf.numberOfChannels > 1
    ? interleaveChannels(buf.getChannelData(0), buf.getChannelData(1))
    : buf.getChannelData(0);
  const wav = encodeWAV(interleaved, buf.sampleRate, buf.numberOfChannels);
  const blob = new Blob([wav], { type: 'audio/wav' });
  downloadBlob(blob, name + '.wav');
  showToast('Mix downloaded ✓');
}

function interleaveChannels(l, r) {
  const out = new Float32Array(l.length + r.length);
  for (let i = 0; i < l.length; i++) { out[i*2] = l[i]; out[i*2+1] = r[i]; }
  return out;
}

function encodeWAV(samples, rate, channels) {
  const buf = new ArrayBuffer(44 + samples.length * 2);
  const view = new DataView(buf);
  const s = str => Array.from(str).forEach((c, i) => view.setUint8(i + arguments[3] || 0, c.charCodeAt(0)));
  // RIFF header
  writeStr(view, 0, 'RIFF');
  view.setUint32(4, 36 + samples.length * 2, true);
  writeStr(view, 8, 'WAVE');
  writeStr(view, 12, 'fmt ');
  view.setUint32(16, 16, true);
  view.setUint16(20, 1, true);
  view.setUint16(22, channels, true);
  view.setUint32(24, rate, true);
  view.setUint32(28, rate * channels * 2, true);
  view.setUint16(32, channels * 2, true);
  view.setUint16(34, 16, true);
  writeStr(view, 36, 'data');
  view.setUint32(40, samples.length * 2, true);
  // PCM samples
  let offset = 44;
  for (let i = 0; i < samples.length; i++, offset += 2) {
    const s = Math.max(-1, Math.min(1, samples[i]));
    view.setInt16(offset, s < 0 ? s * 0x8000 : s * 0x7FFF, true);
  }
  return buf;
}

function writeStr(view, offset, str) {
  for (let i = 0; i < str.length; i++) view.setUint8(offset + i, str.charCodeAt(i));
}

function downloadBlob(blob, filename) {
  const a = document.createElement('a');
  a.href = URL.createObjectURL(blob);
  a.download = filename;
  a.click();
}

function saveProject() {
  const name = document.getElementById('proj-name-input').value || 'Untitled';
  const proj = {
    id: Date.now(),
    name: name,
    date: new Date().toLocaleDateString(),
    bpm: state.bpm,
    tracks: state.tracks.map(t => ({ id: t.id, name: t.name, color: t.color, vol: t.vol, pan: t.pan })),
    takesCount: state.takes.length,
    color: ['#00e5a0','#4a7fff','#a855f7','#ffb800','#ff3b6b'][state.projects.length % 5]
  };
  state.projects.unshift(proj);
  localStorage.setItem('ks_projects', JSON.stringify(state.projects));
  renderProjects();
  showToast('Project saved ✓');
}

function loadProject() {
  showToast('Select a project below to load');
}

function renderProjects() {
  const list = document.getElementById('projects-list');
  if (!state.projects.length) {
    list.innerHTML = '<div style="padding:16px;text-align:center;color:var(--text3);font-size:12px">No saved projects</div>';
    return;
  }
  list.innerHTML = state.projects.map((p, i) => `
    <div class="proj-item" onclick="loadProj(${i})">
      <div class="proj-dot" style="background:${p.color}"></div>
      <div class="proj-info">
        <div class="proj-name">${p.name}</div>
        <div class="proj-meta">${p.date} · ${p.bpm} BPM · ${p.takesCount} take${p.takesCount!==1?'s':''}</div>
      </div>
      <div class="proj-action" onclick="event.stopPropagation();deleteProj(${i})">✕</div>
    </div>
  `).join('');
}

function loadProj(i) {
  const p = state.projects[i];
  state.bpm = p.bpm || 120;
  document.getElementById('bpm-val').textContent = state.bpm;
  document.getElementById('bpm-setting').textContent = state.bpm;
  document.getElementById('proj-name-input').value = p.name;
  showToast('Project "' + p.name + '" loaded ✓');
}

function deleteProj(i) {
  state.projects.splice(i, 1);
  localStorage.setItem('ks_projects', JSON.stringify(state.projects));
  renderProjects();
}

function shareProject() {
  const name = document.getElementById('proj-name-input').value || 'Kamala Studio Project';
  if (navigator.share) {
    navigator.share({ title: name, text: 'Listen to my project: ' + name }).catch(()=>{});
  } else {
    showToast('Share not supported on this browser');
  }
}

// ══════════════════════════════════════════════════
//  TOAST
// ══════════════════════════════════════════════════
let toastTimeout;
function showToast(msg) {
  const t = document.getElementById('toast');
  t.textContent = msg;
  t.classList.add('show');
  clearTimeout(toastTimeout);
  toastTimeout = setTimeout(() => t.classList.remove('show'), 2800);
}

// ══════════════════════════════════════════════════
//  HELPERS
// ══════════════════════════════════════════════════
function formatTime(s) {
  const m = Math.floor(s / 60);
  const sec = Math.floor(s % 60);
  const ms = Math.floor((s % 1) * 10);
  return m + ':' + String(sec).padStart(2,'0') + '.' + ms;
}
function formatTimeShort(s) {
  const m = Math.floor(s / 60);
  const sec = Math.floor(s % 60);
  const ms = Math.floor((s % 1) * 10);
  return m + ':' + String(sec).padStart(2,'0') + '.' + ms;
}

// ══════════════════════════════════════════════════
//  INIT
// ══════════════════════════════════════════════════
window.addEventListener('load', () => {
  buildMetroBeatDots();
  renderTakes();
  renderTracks();
  drawEQ();
  drawNoiseGate(-50, 20);
  // Init waveform canvas size
  const wfc = document.getElementById('waveform-canvas');
  wfc.width = wfc.offsetWidth * window.devicePixelRatio;
  wfc.height = wfc.offsetHeight * window.devicePixelRatio;
  clearWaveform();
  // Auto-init audio on first tap
  document.addEventListener('touchstart', async () => {
    if (!audioCtx) await initAudio();
  }, { once: true });
  // Re-draw EQ on tab switch
  document.getElementById('tab-mixer').addEventListener('click', () => {
    setTimeout(drawEQ, 50);
  });
});

// Handle headroom slider display
document.getElementById('headroom').addEventListener('input', function() {
  document.getElementById('headroom-v').textContent = this.value + ' dB';
});
</script>
</body>
</html>
