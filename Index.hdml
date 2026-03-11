<!DOCTYPE html>
<html lang="hi">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no" />
  <meta name="theme-color" content="#0a0a0f" />
  <meta name="apple-mobile-web-app-capable" content="yes" />
  <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent" />
  <title>Zara AI v4.0</title>
  <link href="https://fonts.googleapis.com/css2?family=Sora:wght@300;400;600;700&family=Space+Mono&family=Orbitron:wght@400;700;900&family=Rajdhani:wght@300;400;600&display=swap" rel="stylesheet" />
  <style>
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
    :root {
      --bg: #0a0a0f; --surface: #0f0f1a; --accent: #00d4aa;
      --accent2: #0099ff; --warn: #ff6b6b; --yellow: #ffd93d;
      --text: #e8e8f0; --muted: rgba(255,255,255,0.3); --border: rgba(255,255,255,0.08);
    }
    body::before {
      content:''; position:fixed; inset:0; pointer-events:none; z-index:0;
      background:
        radial-gradient(ellipse 70% 50% at 15% 10%, rgba(0,212,170,0.07) 0%, transparent 60%),
        radial-gradient(ellipse 50% 40% at 85% 85%, rgba(0,153,255,0.07) 0%, transparent 60%);
    }
    html, body { height: 100%; background: var(--bg); color: var(--text); font-family: 'Sora', sans-serif; overflow: hidden; }
    #app { height: 100dvh; display: flex; flex-direction: column; max-width: 500px; margin: 0 auto; position: relative; z-index: 1; }

    /* HEADER */
    .header { padding: 14px 16px 12px; background: rgba(15,15,26,0.92); backdrop-filter: blur(20px); border-bottom: 1px solid var(--border); flex-shrink: 0; }
    .header-top { display: flex; align-items: center; gap: 12px; margin-bottom: 12px; }
    .avatar-wrap { position: relative; width: 44px; height: 44px; flex-shrink: 0; }
    .avatar-ring { position: absolute; inset: -2px; border-radius: 14px; background: conic-gradient(var(--accent), var(--accent2), var(--yellow), var(--accent)); animation: spin 4s linear infinite; }
    @keyframes spin { to { transform: rotate(360deg); } }
    .avatar { width: 44px; height: 44px; border-radius: 13px; background: var(--surface); display: flex; align-items: center; justify-content: center; position: absolute; inset: 2px; width: calc(100% - 4px); height: calc(100% - 4px); overflow: hidden; }
    .avatar svg { width: 30px; height: 30px; }
    .header-info h1 { font-size: 17px; font-weight: 700; letter-spacing: -0.3px; background: linear-gradient(90deg, var(--accent), var(--accent2)); -webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text; }
    .header-info p { font-size: 11px; color: var(--accent); font-family: 'Space Mono', monospace; margin-top: 2px; }
    .dot { width: 7px; height: 7px; background: #00ff9d; border-radius: 50%; display: inline-block; margin-right: 5px; box-shadow: 0 0 6px #00ff9d; animation: blink 2s infinite; }
    @keyframes blink { 0%,100%{opacity:1} 50%{opacity:0.4} }
    .header-actions { margin-left: auto; display: flex; gap: 7px; }
    .hbtn { width: 32px; height: 32px; border-radius: 9px; background: rgba(255,255,255,0.06); border: 1px solid var(--border); color: var(--muted); font-size: 14px; display: flex; align-items: center; justify-content: center; cursor: pointer; transition: all 0.2s; }
    .modes { display: flex; gap: 6px; }
    .mode-btn { flex: 1; padding: 7px 2px; border-radius: 10px; border: 1.5px solid var(--border); background: rgba(255,255,255,0.04); color: var(--muted); font-family: 'Sora', sans-serif; font-size: 11px; font-weight: 600; cursor: pointer; transition: all 0.2s; -webkit-tap-highlight-color: transparent; }
    .mode-btn.active-chat   { border-color: var(--accent); color: var(--accent); background: rgba(0,212,170,0.12); }
    .mode-btn.active-search { border-color: var(--warn);   color: var(--warn);   background: rgba(255,107,107,0.12); }
    .mode-btn.active-study  { border-color: var(--yellow); color: var(--yellow); background: rgba(255,217,61,0.12); }
    .mode-btn.active-voice  { border-color: #00c8ff; color: #00c8ff; background: rgba(0,200,255,0.12); }

    /* MEMORY BAR */
    .memory-bar { padding: 6px 16px; background: rgba(0,212,170,0.05); border-bottom: 1px solid var(--border); display: flex; align-items: center; gap: 8px; flex-shrink: 0; }
    .memory-dot { width: 6px; height: 6px; background: var(--accent); border-radius: 50%; animation: blink 2s infinite; }
    .memory-text { font-size: 10px; color: var(--accent); font-family: 'Space Mono', monospace; flex: 1; }
    .memory-count { font-size: 10px; color: var(--muted); font-family: 'Space Mono', monospace; }

    /* LANG CHIPS */
    .lang-row { display: flex; gap: 6px; padding: 7px 16px; border-bottom: 1px solid var(--border); background: rgba(15,15,26,0.7); flex-shrink: 0; overflow-x: auto; scrollbar-width: none; }
    .lang-row::-webkit-scrollbar { display: none; }
    .lang-chip { padding: 4px 10px; border-radius: 20px; font-size: 10px; font-weight: 600; cursor: pointer; border: 1px solid var(--border); color: var(--muted); transition: all 0.2s; font-family: 'Space Mono', monospace; white-space: nowrap; }
    .lang-chip.on { border-color: var(--accent); color: var(--accent); background: rgba(0,212,170,0.1); }
    .lang-chip.step.on { border-color: var(--yellow); color: var(--yellow); background: rgba(255,217,61,0.1); }
    .lang-chip.ex.on { border-color: var(--accent2); color: var(--accent2); background: rgba(0,153,255,0.1); }
    .lang-chip.mem.on { border-color: #ff6bff; color: #ff6bff; background: rgba(255,107,255,0.1); }

    /* API KEY SETUP */
    .api-setup { margin: 16px; padding: 16px; background: rgba(255,107,107,0.08); border: 1px solid rgba(255,107,107,0.25); border-radius: 14px; }
    .api-setup h3 { font-size: 13px; color: var(--warn); margin-bottom: 8px; }
    .api-setup p { font-size: 11px; color: var(--muted); margin-bottom: 10px; line-height: 1.5; }
    .api-input { width: 100%; background: rgba(255,255,255,0.06); border: 1px solid var(--border); border-radius: 10px; padding: 10px 12px; color: var(--text); font-family: 'Space Mono', monospace; font-size: 11px; outline: none; }
    .api-input:focus { border-color: var(--accent); }
    .api-save-btn { margin-top: 8px; width: 100%; padding: 10px; background: linear-gradient(135deg, var(--accent), var(--accent2)); border: none; border-radius: 10px; color: #000; font-weight: 700; font-size: 13px; cursor: pointer; }

    /* MESSAGES */
    .messages { flex: 1; overflow-y: auto; padding: 14px 14px 6px; display: flex; flex-direction: column; gap: 12px; -webkit-overflow-scrolling: touch; scrollbar-width: none; }
    .messages::-webkit-scrollbar { display: none; }
    .msg-row { display: flex; gap: 8px; animation: fadeUp 0.25s ease; }
    .msg-row.user { justify-content: flex-end; }
    .msg-row.assistant { justify-content: flex-start; align-items: flex-end; }
    .msg-av { width: 28px; height: 28px; border-radius: 8px; background: linear-gradient(135deg,var(--accent),var(--accent2)); display:flex;align-items:center;justify-content:center; font-size:13px; flex-shrink:0; }
    .bubble { max-width: 82%; padding: 10px 13px; border-radius: 16px; font-size: 14px; line-height: 1.6; }
    .bubble.user { background: linear-gradient(135deg, var(--accent), var(--accent2)); color: #000; border-bottom-right-radius: 4px; font-weight: 500; }
    .bubble.assistant { background: rgba(255,255,255,0.06); color: var(--text); border-bottom-left-radius: 4px; border: 1px solid var(--border); }
    .bubble.error { background: rgba(255,107,107,0.1); border-color: rgba(255,107,107,0.3); color: var(--warn); }
    .mode-tag { font-size: 10px; font-family: 'Space Mono', monospace; opacity: 0.45; margin-top: 4px; }
    .msg-time { font-size:10px; color:rgba(255,255,255,0.25); margin-top:4px; text-align:right; }

    /* MEMORY TAG */
    .memory-tag { display: inline-block; font-size: 9px; padding: 2px 8px; border-radius: 20px; background: rgba(255,107,255,0.1); border: 1px solid rgba(255,107,255,0.25); color: #ff6bff; margin-bottom: 6px; font-family: 'Space Mono', monospace; }

    /* TYPING */
    .typing-row { display: flex; justify-content: flex-start; animation: fadeUp 0.25s ease; gap:8px; align-items:flex-end; }
    .typing-bubble { background: rgba(255,255,255,0.06); border: 1px solid var(--border); border-radius: 16px; border-bottom-left-radius: 4px; padding: 12px 16px; display: flex; gap: 5px; align-items: center; }
    .dot-bounce { width: 7px; height: 7px; border-radius: 50%; background: var(--accent); animation: bounce 1s ease-in-out infinite; }
    .dot-bounce:nth-child(2) { animation-delay: 0.2s; }
    .dot-bounce:nth-child(3) { animation-delay: 0.4s; }

    /* INPUT */
    .input-area { padding: 10px 14px 22px; flex-shrink: 0; background: rgba(15,15,26,0.92); backdrop-filter:blur(20px); border-top:1px solid var(--border); }
    .input-row { display: flex; align-items: flex-end; gap: 10px; background: rgba(255,255,255,0.06); border: 1.5px solid var(--border); border-radius: 16px; padding: 10px 12px; transition: border-color 0.2s; }
    .input-row:focus-within { border-color: var(--accent); box-shadow: 0 0 0 3px rgba(0,212,170,0.08); }
    .input-row textarea { flex: 1; background: none; border: none; outline: none; color: #fff; font-family: 'Sora', sans-serif; font-size: 15px; resize: none; max-height: 90px; min-height: 22px; line-height: 1.5; -webkit-appearance: none; }
    .input-row textarea::placeholder { color: var(--muted); }
    .send-btn { width: 38px; height: 38px; border-radius: 11px; background: linear-gradient(135deg, var(--accent), var(--accent2)); border: none; cursor: pointer; display: flex; align-items: center; justify-content: center; font-size: 17px; flex-shrink: 0; transition: opacity 0.2s, transform 0.1s; -webkit-tap-highlight-color: transparent; box-shadow: 0 4px 12px rgba(0,212,170,0.3); }
    .send-btn:active { transform: scale(0.93); }
    .send-btn:disabled { opacity: 0.35; box-shadow:none; }
    .mic-btn { width: 38px; height: 38px; border-radius: 11px; background: rgba(255,255,255,0.06); border: 1px solid var(--border); color: var(--muted); font-size: 16px; display:flex;align-items:center;justify-content:center; cursor:pointer; flex-shrink:0; transition:all 0.2s; -webkit-tap-highlight-color:transparent; }
    .mic-btn.on { background:rgba(255,107,107,0.15); border-color:var(--warn); color:var(--warn); animation:micPulse 1s infinite; }
    @keyframes micPulse{0%,100%{box-shadow:0 0 0 0 rgba(255,107,107,0.4)}50%{box-shadow:0 0 0 7px rgba(255,107,107,0)}}
    .hint { text-align: center; font-size: 10px; color: rgba(255,255,255,0.18); margin-top: 7px; font-family: 'Space Mono', monospace; }

    /* VOICE PANEL */
    #voice-panel { display: none; flex-direction: column; align-items: center; justify-content: center; flex: 1; background: radial-gradient(ellipse at center, #001a2e 0%, #000 70%); position: relative; overflow: hidden; padding: 16px; }
    #voice-panel.active { display: flex; }
    #voice-panel::before, #voice-panel::after { content: ''; position: absolute; border-radius: 50%; border: 1px solid rgba(0,200,255,0.08); top: 50%; left: 50%; transform: translate(-50%, -50%); animation: pulse-ring 4s ease-in-out infinite; }
    #voice-panel::before { width: 320px; height: 320px; }
    #voice-panel::after  { width: 460px; height: 460px; animation-delay: 1.5s; }
    .j-title { font-family: 'Orbitron', monospace; color: #00c8ff; font-size: 1.3rem; letter-spacing: 6px; text-shadow: 0 0 20px rgba(0,200,255,0.9); margin-bottom: 2px; position: relative; z-index: 2; }
    .j-sub   { font-family: 'Rajdhani', sans-serif; color: rgba(0,200,255,0.4); font-size: 0.6rem; letter-spacing: 4px; margin-bottom: 14px; position: relative; z-index: 2; }
    #j-history { width: 100%; max-width: 440px; height: 200px; overflow-y: auto; background: rgba(0,15,35,0.85); border: 1px solid rgba(0,200,255,0.25); border-radius: 6px; padding: 10px; margin-bottom: 14px; position: relative; z-index: 2; scrollbar-width: thin; scrollbar-color: #00c8ff #001020; }
    #j-history::-webkit-scrollbar { width: 3px; }
    #j-history::-webkit-scrollbar-thumb { background: #00c8ff; border-radius: 2px; }
    .j-log-label { font-family: 'Orbitron', monospace; color: rgba(0,200,255,0.35); font-size: 0.48rem; letter-spacing: 3px; border-bottom: 1px solid rgba(0,200,255,0.15); padding-bottom: 5px; margin-bottom: 8px; }
    .jmsg { display: flex; flex-direction: column; margin-bottom: 10px; animation: fadeUp 0.3s ease; }
    .jmsg.ju { align-items: flex-end; }
    .jmsg.jb { align-items: flex-start; }
    .jlbl { font-family: 'Orbitron', monospace; font-size: 0.45rem; letter-spacing: 2px; color: rgba(0,200,255,0.45); margin-bottom: 3px; }
    .jbub { max-width: 88%; padding: 7px 11px; font-size: 0.82rem; line-height: 1.45; border-radius: 4px; }
    .ju .jbub { background: rgba(0,200,255,0.12); border: 1px solid rgba(0,200,255,0.35); color: #b0eeff; border-radius: 4px 4px 0 4px; }
    .jb .jbub { background: rgba(0,30,55,0.9); border: 1px solid rgba(0,200,255,0.18); color: #00d8ff; border-radius: 4px 4px 4px 0; text-shadow: 0 0 8px rgba(0,200,255,0.25); }
    .jtime { font-size: 0.48rem; color: rgba(0,200,255,0.28); margin-top: 2px; }
    .orb-wrap { position: relative; display: flex; align-items: center; justify-content: center; margin-bottom: 8px; z-index: 2; }
    .orb-ring { position: absolute; width: 88px; height: 88px; border-radius: 50%; border: 1px solid rgba(0,200,255,0.18); pointer-events: none; animation: orb-expand 2.2s ease-out infinite; }
    .orb-ring:nth-child(2) { animation-delay: 0.8s; }
    @keyframes orb-expand { 0% { transform: scale(0.9); opacity: 0.7; } 100% { transform: scale(2); opacity: 0; } }
    #j-mic-btn { width: 70px; height: 70px; border-radius: 50%; background: radial-gradient(circle at 35% 35%, rgba(0,200,255,0.25), rgba(0,40,70,0.95)); border: 2px solid rgba(0,200,255,0.55); cursor: pointer; display: flex; align-items: center; justify-content: center; font-size: 1.7rem; transition: all 0.3s; box-shadow: 0 0 18px rgba(0,200,255,0.25); outline: none; -webkit-tap-highlight-color: transparent; }
    #j-mic-btn.on { background: radial-gradient(circle at 35% 35%, rgba(255,60,60,0.35), rgba(70,0,0,0.95)); border-color: rgba(255,90,90,0.75); box-shadow: 0 0 28px rgba(255,60,60,0.45); animation: jlisten 0.9s ease-in-out infinite; }
    @keyframes jlisten { 0%,100% { transform: scale(1); } 50% { transform: scale(1.09); } }
    #j-status { margin-top: 8px; font-family: 'Orbitron', monospace; font-size: 0.56rem; letter-spacing: 3px; color: rgba(0,200,255,0.55); text-transform: uppercase; min-height: 16px; position: relative; z-index: 2; text-align: center; }
    .wave-bars { display: none; gap: 3px; align-items: center; height: 16px; margin-top: 6px; position: relative; z-index: 2; }
    .wave-bars.on { display: flex; }
    .wbar { width: 3px; background: #00c8ff; border-radius: 2px; animation: wave 0.8s ease-in-out infinite; }
    .wbar:nth-child(1){height:4px;} .wbar:nth-child(2){height:11px;animation-delay:.1s;} .wbar:nth-child(3){height:16px;animation-delay:.2s;} .wbar:nth-child(4){height:11px;animation-delay:.3s;} .wbar:nth-child(5){height:4px;animation-delay:.4s;}
    @keyframes wave { 0%,100%{transform:scaleY(0.5);} 50%{transform:scaleY(1);} }
    #j-clear-btn { background: transparent; border: 1px solid rgba(255,60,60,0.28); color: rgba(255,80,80,0.55); padding: 5px 14px; font-family: 'Orbitron', monospace; font-size: 0.48rem; letter-spacing: 2px; cursor: pointer; border-radius: 3px; margin-top: 8px; transition: all 0.3s; position: relative; z-index: 2; -webkit-tap-highlight-color: transparent; }

    /* ANIMATIONS */
    @keyframes bounce { 0%,80%,100%{transform:scale(0.7);opacity:0.5;} 40%{transform:scale(1.2);opacity:1;} }
    @keyframes fadeUp { from{opacity:0;transform:translateY(10px);} to{opacity:1;transform:translateY(0);} }
    @keyframes pulse-ring { 0%,100%{transform:translate(-50%,-50%) scale(1);opacity:0.4;} 50%{transform:translate(-50%,-50%) scale(1.06);opacity:0.9;} }

    /* QUICK PROMPTS */
    .quick-wrap { padding: 0 14px 10px; display:grid; grid-template-columns:1fr 1fr; gap:7px; }
    .qp { background:rgba(255,255,255,0.04); border:1px solid var(--border); border-radius:11px; padding:9px 10px; font-size:12px; color:var(--muted); cursor:pointer; text-align:left; font-family:'Sora',sans-serif; display:flex;align-items:center;gap:6px; transition:all 0.2s; -webkit-tap-highlight-color:transparent; }
    .qp:active { background:rgba(0,212,170,0.1); border-color:var(--accent); color:var(--accent); }

    /* STUDY BLOCK */
    .study-block { background:rgba(255,217,61,0.07); border:1px solid rgba(255,217,61,0.2); border-radius:10px; padding:9px 11px; margin-top:8px; }
    .study-block-title { font-size:10px; font-weight:700; color:var(--yellow); letter-spacing:.8px; text-transform:uppercase; margin-bottom:6px; }
    .spoint { display:flex; gap:7px; font-size:13px; color:rgba(255,255,255,0.75); margin-bottom:4px; line-height:1.5; }
    .spoint::before { content:'›'; color:var(--accent); font-weight:700; flex-shrink:0; }

    /* SEARCH RESULT */
    .search-result { background:rgba(255,107,107,0.06); border:1px solid rgba(255,107,107,0.18); border-radius:10px; padding:9px 11px; margin-top:8px; }
    .search-title { font-size:10px; font-weight:700; color:var(--warn); letter-spacing:.8px; text-transform:uppercase; margin-bottom:4px; }
  </style>
</head>
<body>
<div id="app">

  <!-- HEADER -->
  <div class="header">
    <div class="header-top">
      <div class="avatar-wrap">
        <div class="avatar-ring"></div>
        <div class="avatar">
          <svg viewBox="0 0 60 60" fill="none" xmlns="http://www.w3.org/2000/svg">
            <circle cx="30" cy="30" r="28" fill="url(#ag)"/>
            <ellipse cx="22" cy="26" rx="5" ry="6" fill="#00e5ff" opacity=".9"/>
            <ellipse cx="38" cy="26" rx="5" ry="6" fill="#00e5ff" opacity=".9"/>
            <ellipse cx="22" cy="27" rx="2.2" ry="3" fill="#0a0a0f"/>
            <ellipse cx="38" cy="27" rx="2.2" ry="3" fill="#0a0a0f"/>
            <circle cx="22.8" cy="25.5" r="1" fill="white"/>
            <circle cx="38.8" cy="25.5" r="1" fill="white"/>
            <path d="M19 38 Q30 46 41 38" stroke="#00d4aa" stroke-width="2.5" fill="none" stroke-linecap="round"/>
            <defs>
              <radialGradient id="ag" cx="50%" cy="40%" r="60%">
                <stop offset="0%" stop-color="#1a1a4e"/>
                <stop offset="100%" stop-color="#0a0a1a"/>
              </radialGradient>
            </defs>
          </svg>
        </div>
      </div>
      <div class="header-info">
        <h1>Zara AI v4.0</h1>
        <p><span class="dot"></span>Online • Real AI Powered</p>
      </div>
      <div class="header-actions">
        <div class="hbtn" title="Settings" onclick="showApiSetup()">⚙️</div>
        <div class="hbtn" onclick="clearChat()">🗑️</div>
      </div>
    </div>
    <div class="modes">
      <button class="mode-btn active-chat" data-mode="chat"   onclick="setMode('chat')">💬 Chat</button>
      <button class="mode-btn"             data-mode="search" onclick="setMode('search')">🔍 Search</button>
      <button class="mode-btn"             data-mode="study"  onclick="setMode('study')">📚 Study</button>
      <button class="mode-btn"             data-mode="voice"  onclick="setMode('voice')">🎙️ Voice</button>
    </div>
  </div>

  <!-- MEMORY BAR -->
  <div class="memory-bar" id="memoryBar">
    <div class="memory-dot"></div>
    <div class="memory-text" id="memoryText">🧠 Memory Active — Zara tumhe yaad rakhti hai!</div>
    <div class="memory-count" id="memoryCount">0 yaadein</div>
  </div>

  <!-- LANG CHIPS -->
  <div class="lang-row" id="langRow">
    <div class="lang-chip on" id="chip-bilingual" onclick="toggleChip('bilingual',this)">🌐 Bilingual</div>
    <div class="lang-chip step" id="chip-step" onclick="togg
