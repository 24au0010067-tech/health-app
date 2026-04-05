<!DOCTYPE html>
<html lang="en" data-theme="dark">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>VitaQuest RPG</title>
<link href="https://fonts.googleapis.com/css2?family=Press+Start+2P&family=Exo+2:wght@300;400;500;600;700;800;900&family=Share+Tech+Mono&display=swap" rel="stylesheet"/>
<style>
/* ════════════════════════════════════════
   VitaQuest RPG — style.css
   FULL GAME UI AESTHETIC
════════════════════════════════════════ */

/* ── RESET ── */
*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
html { font-size: 16px; scroll-behavior: smooth; }

/* ── FONT SHORTHAND ── */
.pixel-font { font-family: 'Press Start 2P', monospace; }

/* ════════════════════════════════════════
   CSS VARIABLES
════════════════════════════════════════ */
:root {
  --bg:        #060b18;
  --bg2:       #0b1225;
  --bg3:       #111b35;
  --panel:     rgba(8,14,28,0.95);
  --panel2:    rgba(12,20,38,0.9);
  --border:    rgba(0,255,255,0.18);
  --border2:   rgba(0,255,255,0.5);
  --text:      #e8f0ff;
  --text2:     #7a90b8;
  --text3:     #3a4a6a;
  --cyan:      #00ffff;
  --cyan2:     #00b8cc;
  --gold:      #ffd60a;
  --gold2:     #c4a000;
  --fire:      #ff6b00;
  --green:     #39ff14;
  --green2:    #1fa800;
  --red:       #ff2244;
  --purple:    #bf5af2;
  --pink:      #ff006e;
  --hp-color:  #39ff14;
  --xp-color:  #00ffff;
  --glow-c:    0 0 20px rgba(0,255,255,0.6);
  --glow-g:    0 0 20px rgba(255,214,10,0.7);
  --glow-r:    0 0 16px rgba(255,34,68,0.6);
  --glow-p:    0 0 20px rgba(191,90,242,0.6);
  --shadow:    0 8px 40px rgba(0,0,0,0.9);
  --panel-border: 1px solid var(--border);
  --corner-size: 12px;
}
[data-theme="light"] {
  --bg:        #e8eeff;
  --bg2:       #d4daf5;
  --bg3:       #c8d0ee;
  --panel:     rgba(240,244,255,0.97);
  --panel2:    rgba(230,236,255,0.95);
  --border:    rgba(80,100,200,0.25);
  --border2:   rgba(80,100,200,0.6);
  --text:      #0a1030;
  --text2:     #3a4870;
  --text3:     #8090c0;
  --cyan:      #0088aa;
  --gold:      #c48000;
  --fire:      #d44000;
  --green:     #008800;
  --red:       #cc0033;
  --purple:    #7700cc;
  --glow-c:    0 0 16px rgba(0,136,170,0.3);
}

/* ════════════════════════════════════════
   BODY & GLOBAL
════════════════════════════════════════ */
body {
  background: var(--bg);
  color: var(--text);
  font-family: 'Exo 2', sans-serif;
  overflow-x: hidden;
  cursor: default;
  transition: background 0.4s, color 0.3s;
  min-height: 100vh;
}

/* BACKGROUND CANVAS — always behind everything */
.bg-canvas {
  position: fixed; inset: 0; z-index: 0;
  width: 100vw; height: 100vh;
  pointer-events: none;
}

.screen { position: relative; z-index: 1; }
.hidden { display: none !important; }

/* ════════════════════════════════════════
   RPG PANEL — Pixel-art corner brackets
════════════════════════════════════════ */
.rpg-panel {
  position: relative;
  background: var(--panel);
  border: 1px solid var(--border);
  border-radius: 4px;
  padding: 20px;
  box-shadow: 0 4px 30px rgba(0,0,0,0.7), inset 0 1px 0 rgba(255,255,255,0.04);
  transition: border-color 0.3s, box-shadow 0.3s;
}
.rpg-panel:hover { border-color: var(--border2); }

/* Corner decorators */
.rpc {
  position: absolute;
  width: var(--corner-size);
  height: var(--corner-size);
  border-color: var(--cyan);
  border-style: solid;
  border-width: 0;
  z-index: 2;
}
.rpc.tl { top: -1px; left: -1px; border-top-width: 2px; border-left-width: 2px; border-radius: 3px 0 0 0; }
.rpc.tr { top: -1px; right: -1px; border-top-width: 2px; border-right-width: 2px; border-radius: 0 3px 0 0; }
.rpc.bl { bottom: -1px; left: -1px; border-bottom-width: 2px; border-left-width: 2px; border-radius: 0 0 0 3px; }
.rpc.br { bottom: -1px; right: -1px; border-bottom-width: 2px; border-right-width: 2px; border-radius: 0 0 3px 0; }

/* Panel title */
.rpg-panel-title {
  font-size: 0.6rem;
  color: var(--cyan);
  letter-spacing: 2px;
  margin-bottom: 16px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  text-shadow: 0 0 8px var(--cyan);
}

/* ════════════════════════════════════════
   BUTTONS
════════════════════════════════════════ */
.rpg-btn {
  position: relative; overflow: hidden;
  padding: 12px 24px;
  border: 1px solid var(--cyan);
  border-radius: 3px;
  background: rgba(0,255,255,0.08);
  color: var(--cyan);
  cursor: pointer;
  font-size: 0.7rem;
  transition: all 0.2s;
  display: inline-flex; align-items: center; justify-content: center;
  text-shadow: 0 0 8px var(--cyan);
  box-shadow: inset 0 0 20px rgba(0,255,255,0.05);
}
.rpg-btn:hover {
  background: rgba(0,255,255,0.2);
  box-shadow: var(--glow-c);
  transform: translateY(-2px);
}
.rpg-btn:active { transform: translateY(0); }
.rpg-btn.primary {
  background: linear-gradient(135deg, rgba(0,255,255,0.25), rgba(0,100,180,0.3));
  border-color: var(--cyan);
  color: var(--cyan);
}
.rpg-btn.primary:hover { box-shadow: var(--glow-c), 0 4px 20px rgba(0,0,0,0.5); }
.rpg-btn.sm-btn { padding: 8px 16px; font-size: 0.6rem; }
.rpg-btn.danger { border-color: var(--red); color: var(--red); background: rgba(255,34,68,0.1); text-shadow: 0 0 8px var(--red); }
.rpg-btn.danger:hover { background: rgba(255,34,68,0.25); box-shadow: var(--glow-r); }
.btn-sheen {
  position: absolute; top: 0; left: -100%; width: 60%; height: 100%;
  background: linear-gradient(90deg, transparent, rgba(255,255,255,0.15), transparent);
  transform: skewX(-20deg);
  animation: sheen 3s ease-in-out infinite;
}
@keyframes sheen { 0%,65%{ left:-100%; } 100%{ left:220%; } }
.full-w { width: 100%; }
.mt8 { margin-top: 8px; }

/* ════════════════════════════════════════
   INPUTS
════════════════════════════════════════ */
.rpg-input {
  width: 100%; padding: 10px 14px;
  background: rgba(0,255,255,0.05);
  border: 1px solid var(--border);
  border-radius: 3px;
  color: var(--text);
  font-family: 'Share Tech Mono', monospace;
  font-size: 0.9rem;
  outline: none;
  transition: border 0.2s, box-shadow 0.2s;
  margin-bottom: 10px;
}
.rpg-input:focus { border-color: var(--cyan); box-shadow: 0 0 10px rgba(0,255,255,0.3); }
.rpg-input-wrap { position: relative; margin-bottom: 14px; }
.rpg-input-wrap input { padding-left: 36px; width: 100%; }
.rpg-input-wrap input { padding: 12px 14px 12px 36px; background: rgba(0,255,255,0.06); border: 1px solid var(--border); border-radius: 3px; color: var(--text); font-family: 'Share Tech Mono', monospace; font-size: 0.95rem; outline: none; transition: all 0.2s; }
.rpg-input-wrap input:focus { border-color: var(--cyan); box-shadow: 0 0 14px rgba(0,255,255,0.3); }
.inp-icon { position: absolute; left: 12px; top: 50%; transform: translateY(-50%); font-size: 1rem; }
.rpg-select {
  padding: 10px 12px;
  background: rgba(0,255,255,0.05);
  border: 1px solid var(--border);
  border-radius: 3px;
  color: var(--text);
  font-family: 'Press Start 2P', monospace;
  font-size: 0.6rem;
  outline: none;
  cursor: pointer;
  margin-bottom: 10px;
  transition: border 0.2s;
}
.rpg-select:focus { border-color: var(--cyan); }
.rpg-slider { width: 100%; accent-color: var(--cyan); }

/* ════════════════════════════════════════
   LOGIN SCREEN
════════════════════════════════════════ */
#login-screen {
  min-height: 100vh;
  display: flex; align-items: center; justify-content: center;
}
.login-wrap {
  display: flex; flex-direction: column; align-items: center; gap: 32px;
  max-width: 420px; width: 100%; padding: 20px;
}
.login-logo-area { text-align: center; }
.login-emblem {
  position: relative; width: 120px; height: 140px;
  margin: 0 auto 20px; display: flex; align-items: center; justify-content: center;
}
.emblem-ring {
  position: absolute; border-radius: 50%;
  border: 1px solid var(--cyan);
  animation: ringRotate 4s linear infinite;
}
.emblem-ring.r1 { width: 100px; height: 100px; border-color: rgba(0,255,255,0.5); animation-duration: 6s; }
.emblem-ring.r2 { width: 120px; height: 120px; border-color: rgba(0,255,255,0.25); animation-duration: 10s; animation-direction: reverse; }
.emblem-ring.r3 { width: 140px; height: 140px; border-color: rgba(0,255,255,0.12); animation-duration: 15s; }
@keyframes ringRotate {
  from { transform: rotate(0deg); }
  to   { transform: rotate(360deg); }
}
.login-title {
  font-size: 2rem; letter-spacing: 6px; line-height: 1.2; margin-bottom: 10px;
  color: var(--text); text-shadow: 0 0 30px rgba(0,255,255,0.5);
}
.title-accent { color: var(--cyan); text-shadow: 0 0 20px var(--cyan); }
.login-sub { color: var(--text2); font-family: 'Exo 2', sans-serif; font-size: 0.85rem; letter-spacing: 3px; margin-bottom: 8px; }
.login-version { font-size: 0.55rem; color: var(--text3); letter-spacing: 2px; margin-top: 6px; }
.login-panel { width: 100%; padding: 28px; }
.field-label { font-size: 0.55rem; color: var(--cyan); letter-spacing: 2px; display: block; margin-bottom: 8px; text-shadow: 0 0 6px var(--cyan); }
.login-field { margin-bottom: 20px; }
.login-error { padding: 10px 14px; background: rgba(255,34,68,0.12); border: 1px solid var(--red); border-radius: 3px; color: var(--red); font-size: 0.6rem; margin-bottom: 14px; text-shadow: 0 0 8px var(--red); text-align: center; }
.login-btn { width: 100%; margin-top: 4px; padding: 14px; }
.login-hint { font-size: 0.5rem; color: var(--text3); text-align: center; margin-top: 14px; letter-spacing: 1px; }

/* ════════════════════════════════════════
   TOP HUD
════════════════════════════════════════ */
.top-hud {
  position: fixed; top: 0; left: 0; right: 0; z-index: 200;
  height: 60px;
  background: rgba(4,8,20,0.95);
  border-bottom: 1px solid var(--border);
  backdrop-filter: blur(12px);
  display: flex; align-items: center; justify-content: space-between;
  padding: 0 16px;
  box-shadow: 0 2px 20px rgba(0,0,0,0.8), 0 1px 0 rgba(0,255,255,0.1);
}
.hud-left { display: flex; align-items: center; gap: 12px; }
#hud-avatar-canvas { border: 1px solid var(--cyan); border-radius: 4px; box-shadow: var(--glow-c); }
.hud-bars-col { display: flex; flex-direction: column; gap: 4px; }
.hud-name { font-size: 0.55rem; color: var(--gold); letter-spacing: 2px; text-shadow: 0 0 8px var(--gold); margin-bottom: 2px; }
.hud-bar-row { display: flex; align-items: center; gap: 6px; }
.bar-lbl { font-size: 0.5rem; min-width: 18px; }
.hp-c  { color: var(--hp-color); text-shadow: 0 0 6px var(--hp-color); }
.xp-c  { color: var(--xp-color); text-shadow: 0 0 6px var(--xp-color); }
.hud-bar-track { width: 100px; height: 7px; background: rgba(255,255,255,0.08); border-radius: 2px; overflow: hidden; border: 1px solid rgba(255,255,255,0.06); }
.hud-bar-inner { height: 100%; border-radius: 2px; transition: width 0.6s cubic-bezier(.23,1,.32,1); }
.hp-bar { background: linear-gradient(90deg, var(--green2), var(--hp-color)); box-shadow: 0 0 6px var(--hp-color); }
.xp-bar-h { background: linear-gradient(90deg, var(--cyan2), var(--cyan)); box-shadow: 0 0 6px var(--cyan); }
.bar-val { font-size: 0.5rem; color: var(--text2); min-width: 28px; }
.hud-center { display: flex; flex-direction: column; align-items: center; gap: 4px; }
.level-badge {
  display: flex; align-items: baseline; gap: 4px;
  background: linear-gradient(135deg, rgba(255,214,10,0.15), rgba(255,214,10,0.05));
  border: 1px solid rgba(255,214,10,0.5); border-radius: 4px;
  padding: 4px 12px; box-shadow: var(--glow-g);
}
.lv-tag { font-size: 0.5rem; color: var(--gold); }
.lv-num { font-size: 1.1rem; color: var(--gold); text-shadow: 0 0 12px var(--gold); line-height: 1; }
.hud-class { font-size: 0.5rem; color: var(--cyan); letter-spacing: 3px; text-shadow: 0 0 6px var(--cyan); }
.hud-right { display: flex; align-items: center; gap: 10px; }
.hud-pill { display: flex; align-items: center; gap: 6px; padding: 5px 12px; background: rgba(255,255,255,0.05); border: 1px solid var(--border); border-radius: 20px; }
.fire-pill { border-color: rgba(255,107,0,0.4); }
.fire-pill .pixel-font { font-size: 0.55rem; color: var(--fire); }
.sword-pill .pixel-font { font-size: 0.55rem; color: var(--cyan); }
.hud-btn { background: none; border: none; cursor: pointer; font-size: 1.1rem; opacity: 0.7; transition: opacity 0.2s, transform 0.2s; padding: 4px; }
.hud-btn:hover { opacity: 1; transform: scale(1.2); }
.red-btn:hover { color: var(--red); }

/* ════════════════════════════════════════
   GAME WORLD
════════════════════════════════════════ */
.game-world {
  margin-top: 60px;
  min-height: calc(100vh - 60px - 72px);
  padding: 20px;
  overflow-y: auto;
  padding-bottom: 90px;
}

/* ── HEX BACKGROUND PATTERN (per page) ── */
.page-bg-hex {
  position: fixed; inset: 60px 0 72px 0;
  pointer-events: none; z-index: 0;
  background-image: 
    radial-gradient(circle at 20% 30%, rgba(0,255,255,0.04) 0%, transparent 50%),
    radial-gradient(circle at 80% 70%, rgba(191,90,242,0.04) 0%, transparent 50%);
  background-size: 60px 52px;
}
.purple-bg { background-image: radial-gradient(circle at 30% 40%, rgba(191,90,242,0.07) 0%, transparent 50%), radial-gradient(circle at 70% 60%, rgba(0,255,255,0.04) 0%, transparent 50%); }
.blue-bg   { background-image: radial-gradient(circle at 50% 30%, rgba(0,100,255,0.08) 0%, transparent 50%); }
.green-bg  { background-image: radial-gradient(circle at 30% 60%, rgba(57,255,20,0.06) 0%, transparent 50%); }
.cyan-bg   { background-image: radial-gradient(circle at 60% 30%, rgba(0,255,255,0.07) 0%, transparent 50%); }
.gold-bg   { background-image: radial-gradient(circle at 50% 40%, rgba(255,214,10,0.07) 0%, transparent 50%); }

.gpage { display: none; position: relative; z-index: 1; animation: pageIn 0.35s cubic-bezier(.23,1,.32,1) both; }
.gpage.active { display: block; }
@keyframes pageIn { from { opacity:0; transform: translateY(18px); } to { opacity:1; transform: translateY(0); } }

/* ════════════════════════════════════════
   HERO BANNER
════════════════════════════════════════ */
.hero-banner {
  position: relative; overflow: hidden;
  padding: 20px 24px; margin-bottom: 20px;
  background: linear-gradient(90deg, rgba(0,255,255,0.06) 0%, transparent 100%);
  border: 1px solid var(--border);
  border-radius: 4px;
  border-left: 3px solid var(--cyan);
}
.hero-greet { font-size: 0.75rem; color: var(--cyan); text-shadow: 0 0 12px var(--cyan); letter-spacing: 3px; }
.hero-greet-sub { color: var(--text2); font-size: 0.9rem; margin-top: 6px; }
.banner-runes { position: absolute; right: 20px; top: 50%; transform: translateY(-50%); display: flex; gap: 12px; }
.rune-char { font-size: 1.5rem; opacity: 0.15; animation: runePulse 3s ease-in-out infinite; }
.rune-char:nth-child(2) { animation-delay: 1s; }
.rune-char:nth-child(3) { animation-delay: 2s; }
@keyframes runePulse { 0%,100%{ opacity:.08; transform:scale(1); } 50%{ opacity:.25; transform:scale(1.1); } }

/* ════════════════════════════════════════
   DASHBOARD LAYOUT
════════════════════════════════════════ */
.dash-layout {
  display: grid;
  grid-template-columns: 190px 1fr 1fr;
  grid-template-rows: auto auto auto;
  gap: 16px;
}
.ava-card { grid-row: 1 / 3; display: flex; flex-direction: column; align-items: center; text-align: center; }
.stat-orbs-wrap { grid-column: 2 / 4; display: grid; grid-template-columns: repeat(4,1fr); gap: 12px; }
.dash-quests { grid-column: 2; }
.ai-panel    { grid-column: 3; }
.vitals-panel { grid-column: 1 / 3; }
.badges-panel { grid-column: 3; }

/* ── AVATAR MINI CARD ── */
.ava-mini-stage { position: relative; margin: 12px 0; display: flex; align-items: center; justify-content: center; }
.ava-glow-ring {
  position: absolute; width: 120px; height: 120px; border-radius: 50%;
  background: radial-gradient(circle, rgba(0,255,255,0.12) 0%, transparent 70%);
  animation: glowPulse 2.5s ease-in-out infinite;
}
@keyframes glowPulse { 0%,100%{ transform:scale(.9); opacity:.6; } 50%{ transform:scale(1.1); opacity:1; } }
.ava-class-tag { font-size: 0.55rem; color: var(--cyan); letter-spacing: 2px; margin: 4px 0; text-shadow: 0 0 8px var(--cyan); }
.ava-lv-tag { font-size: 0.7rem; color: var(--gold); text-shadow: 0 0 10px var(--gold); border: 1px solid rgba(255,214,10,0.4); border-radius: 20px; padding: 2px 12px; margin: 4px 0; }
.mini-xp-wrap { width: 100%; margin-top: 8px; }
.mini-xp-track { height: 10px; background: rgba(255,255,255,0.06); border-radius: 2px; overflow: hidden; border: 1px solid var(--border); }
.mini-xp-inner { height: 100%; background: linear-gradient(90deg, var(--cyan2), var(--cyan)); box-shadow: 0 0 8px var(--cyan); transition: width 0.8s cubic-bezier(.23,1,.32,1); }
.mini-xp-text { font-size: 0.5rem; color: var(--text2); margin-top: 4px; }

/* ── STAT ORBS ── */
.stat-orb {
  position: relative; overflow: hidden;
  display: flex; flex-direction: column; align-items: center; justify-content: center;
  padding: 16px 12px;
  border: 1px solid var(--border);
  border-radius: 4px;
  background: var(--panel2);
  cursor: pointer;
  transition: all 0.25s;
  text-align: center;
}
.stat-orb:hover { transform: translateY(-4px) scale(1.03); }
.orb-glow { position: absolute; inset: 0; opacity: 0; transition: opacity 0.3s; border-radius: 4px; }
.stat-orb:hover .orb-glow { opacity: 1; }
.orb-icon { font-size: 1.6rem; margin-bottom: 6px; }
.orb-val { font-size: 1.1rem; line-height: 1; margin-bottom: 4px; }
.orb-label { font-family: 'Exo 2', sans-serif; font-size: 0.7rem; color: var(--text2); font-weight: 600; letter-spacing: 1px; }
.c-cyan { border-color: rgba(0,255,255,0.3); }
.c-cyan .orb-val { color: var(--cyan); text-shadow: 0 0 10px var(--cyan); }
.c-cyan .orb-glow { background: radial-gradient(circle, rgba(0,255,255,0.12) 0%, transparent 70%); }
.c-cyan:hover { border-color: var(--cyan); box-shadow: var(--glow-c); }
.c-gold { border-color: rgba(255,214,10,0.3); }
.c-gold .orb-val { color: var(--gold); text-shadow: 0 0 10px var(--gold); }
.c-gold .orb-glow { background: radial-gradient(circle, rgba(255,214,10,0.12) 0%, transparent 70%); }
.c-gold:hover { border-color: var(--gold); box-shadow: var(--glow-g); }
.c-fire { border-color: rgba(255,107,0,0.3); }
.c-fire .orb-val { color: var(--fire); text-shadow: 0 0 10px var(--fire); }
.c-fire .orb-glow { background: radial-gradient(circle, rgba(255,107,0,0.12) 0%, transparent 70%); }
.c-fire:hover { border-color: var(--fire); box-shadow: 0 0 20px rgba(255,107,0,0.5); }
.c-green { border-color: rgba(57,255,20,0.3); }
.c-green .orb-val { color: var(--green); text-shadow: 0 0 10px var(--green); }
.c-green .orb-glow { background: radial-gradient(circle, rgba(57,255,20,0.12) 0%, transparent 70%); }
.c-green:hover { border-color: var(--green); box-shadow: 0 0 20px rgba(57,255,20,0.4); }

/* ── DASH QUESTS PANEL ── */
.dash-quest-list { display: flex; flex-direction: column; gap: 8px; max-height: 220px; overflow-y: auto; margin-bottom: 10px; }
.dash-qi {
  display: flex; align-items: center; gap: 10px;
  padding: 8px 12px;
  background: var(--panel2);
  border: 1px solid var(--border);
  border-radius: 3px;
  transition: border-color 0.2s;
}
.dash-qi:hover { border-color: var(--border2); }
.dash-qi input[type=checkbox] { accent-color: var(--green); width: 16px; height: 16px; cursor: pointer; }
.dash-qi-name { flex: 1; font-size: 0.88rem; font-weight: 500; }
.dash-qi.done .dash-qi-name { text-decoration: line-through; color: var(--text2); }
.dash-qi-xp { font-family: 'Share Tech Mono', monospace; font-size: 0.75rem; color: var(--gold); }
.qcount { background: var(--cyan); color: #000; border-radius: 20px; padding: 1px 8px; font-size: 0.5rem; }

/* ── AI TIPS ── */
.ai-tips { display: flex; flex-direction: column; gap: 10px; }
.ai-tip {
  display: flex; gap: 10px; align-items: flex-start;
  padding: 10px 12px;
  background: rgba(191,90,242,0.06);
  border: 1px solid rgba(191,90,242,0.2);
  border-left: 3px solid var(--purple);
  border-radius: 3px;
  font-size: 0.85rem;
  animation: tipIn 0.4s ease;
}
@keyframes tipIn { from { opacity:0; transform:translateX(10px); } to { opacity:1; transform:translateX(0); } }
.tip-ico { font-size: 1rem; flex-shrink: 0; }

/* ── VITALS GRID ── */
.vitals-grid { display: grid; grid-template-columns: repeat(6,1fr); gap: 10px; }
.vital-item { text-align: center; padding: 10px 6px; background: var(--panel2); border: 1px solid var(--border); border-radius: 3px; }
.vital-ico { font-size: 1.3rem; display: block; margin-bottom: 4px; }
.vital-val { font-family: 'Share Tech Mono', monospace; font-size: 0.85rem; color: var(--text); font-weight: bold; }
.vital-lbl { font-size: 0.65rem; color: var(--text2); margin-top: 2px; }
.vital-bar { height: 3px; background: rgba(255,255,255,0.08); border-radius: 2px; margin-top: 5px; overflow: hidden; }
.vital-bar-fill { height: 100%; border-radius: 2px; transition: width 0.7s; }

/* ── BADGES ── */
.badges-row { display: flex; flex-wrap: nowrap; gap: 10px; overflow-x: auto; }
.badges-row.wrap { flex-wrap: wrap; }
.badge-chip {
  display: flex; flex-direction: column; align-items: center; gap: 4px;
  min-width: 64px; padding: 10px 10px;
  background: var(--panel2);
  border: 1px solid var(--border);
  border-radius: 3px;
  transition: all 0.3s;
  animation: chipIn 0.4s ease;
  flex-shrink: 0;
}
@keyframes chipIn { from { transform:scale(0.6); opacity:0; } to { transform:scale(1); opacity:1; } }
.badge-chip:hover { transform: translateY(-4px); border-color: var(--gold); box-shadow: var(--glow-g); }
.badge-chip.locked { opacity: 0.3; filter: grayscale(0.8); }
.badge-ico { font-size: 1.6rem; }
.badge-name { font-family: 'Press Start 2P', monospace; font-size: 0.45rem; color: var(--gold); text-align: center; }

/* ════════════════════════════════════════
   AVATAR PAGE
════════════════════════════════════════ */
.page-header-banner {
  text-align: center; padding: 14px;
  background: linear-gradient(90deg, transparent, rgba(0,255,255,0.05), transparent);
  border-top: 1px solid var(--border); border-bottom: 1px solid var(--border);
  margin-bottom: 20px;
}
.page-header-banner .pixel-font { font-size: 0.7rem; color: var(--cyan); letter-spacing: 4px; text-shadow: 0 0 12px var(--cyan); }

.ava-page-layout { display: grid; grid-template-columns: 360px 1fr; gap: 16px; }
.ava-main-panel { display: flex; flex-direction: column; align-items: center; }
.ava-big-stage { position: relative; display: flex; flex-direction: column; align-items: center; margin: 16px 0; }
.orbit-ring {
  position: absolute; border-radius: 50%;
  border: 1px solid rgba(0,255,255,0.2);
  animation: orbitSpin 6s linear infinite;
  pointer-events: none;
}
.or1 { width: 230px; height: 140px; top: 50%; left: 50%; transform: translate(-50%,-50%); animation-duration: 8s; }
.or2 { width: 270px; height: 160px; top: 50%; left: 50%; transform: translate(-50%,-50%); animation-duration: 12s; animation-direction: reverse; border-color: rgba(191,90,242,0.15); }
@keyframes orbitSpin { from{transform:translate(-50%,-50%) rotate(0deg);} to{transform:translate(-50%,-50%) rotate(360deg);} }
.ava-nameplate { text-align: center; margin-top: 8px; }
.ava-big-class { font-size: 0.65rem; color: var(--cyan); text-shadow: 0 0 10px var(--cyan); letter-spacing: 3px; }
.ava-big-lv { font-size: 0.6rem; color: var(--gold); margin-top: 4px; }
.ava-xp-block { width: 100%; margin-top: 12px; }
.ava-xp-lbl { font-size: 0.5rem; color: var(--text2); letter-spacing: 2px; margin-bottom: 6px; }
.rpg-xp-bar { height: 14px; background: rgba(255,255,255,0.06); border-radius: 2px; overflow: hidden; border: 1px solid var(--border); position: relative; }
.rpg-xp-inner { height: 100%; background: linear-gradient(90deg, var(--cyan2), var(--cyan), rgba(255,255,255,0.8)); box-shadow: 0 0 10px var(--cyan); transition: width 0.8s cubic-bezier(.23,1,.32,1); }
.ava-xp-nums { font-size: 0.5rem; color: var(--text2); margin-top: 5px; }
.evo-chain-block { width: 100%; margin-top: 16px; border-top: 1px solid var(--border); padding-top: 16px; }
.evo-chain-title { font-size: 0.5rem; color: var(--text2); letter-spacing: 2px; margin-bottom: 10px; }
.evo-chain { display: flex; gap: 6px; flex-wrap: wrap; justify-content: center; }
.evo-node {
  display: flex; flex-direction: column; align-items: center; gap: 4px;
  padding: 8px; border: 1px solid var(--border); border-radius: 3px;
  opacity: 0.35; transition: all 0.3s; min-width: 56px; cursor: default;
}
.evo-node.active { opacity: 1; border-color: var(--cyan); background: rgba(0,255,255,0.08); box-shadow: var(--glow-c); }
.evo-node.past { opacity: 0.7; border-color: var(--gold); }
.evo-icon { font-size: 1.2rem; }
.evo-name { font-family: 'Press Start 2P', monospace; font-size: 0.45rem; color: var(--text2); }
.ava-side-panels { display: flex; flex-direction: column; gap: 16px; }
.ava-perks { display: flex; flex-direction: column; gap: 8px; }
.perk-row { display: flex; align-items: center; gap: 10px; padding: 8px 12px; background: rgba(191,90,242,0.07); border: 1px solid rgba(191,90,242,0.2); border-radius: 3px; font-size: 0.88rem; }
.ava-history { display: flex; flex-direction: column; gap: 8px; }
.hist-row { display: flex; align-items: center; gap: 10px; padding: 8px 12px; background: var(--panel2); border: 1px solid var(--border); border-radius: 3px; font-size: 0.85rem; }
.hist-time { margin-left: auto; font-family: 'Share Tech Mono', monospace; font-size: 0.75rem; color: var(--text2); }

/* ════════════════════════════════════════
   TASKS PAGE
════════════════════════════════════════ */
.tasks-wrap { max-width: 900px; margin: 0 auto; }
.add-task-panel { margin-bottom: 16px; }
.add-task-form { display: flex; gap: 10px; flex-wrap: wrap; }
.add-task-form .rpg-input { flex: 1; min-width: 200px; margin-bottom: 0; }
.add-task-form .rpg-select { margin-bottom: 0; }
.quest-tabs { display: flex; gap: 8px; margin-bottom: 16px; flex-wrap: wrap; }
.qtab {
  padding: 8px 16px; font-size: 0.55rem; background: var(--panel2);
  border: 1px solid var(--border); border-radius: 3px;
  color: var(--text2); cursor: pointer; transition: all 0.2s;
}
.qtab.active { background: rgba(0,255,255,0.12); color: var(--cyan); border-color: var(--cyan); text-shadow: 0 0 6px var(--cyan); }
.quests-list { display: flex; flex-direction: column; gap: 12px; }
.quest-card {
  display: flex; align-items: center; gap: 14px;
  padding: 14px 18px;
  background: var(--panel);
  border: 1px solid var(--border);
  border-radius: 3px;
  transition: all 0.25s;
  animation: cardIn 0.3s ease;
  position: relative; overflow: hidden;
}
.quest-card::before {
  content: ''; position: absolute; left: 0; top: 0; bottom: 0; width: 3px;
  background: var(--cyan);
  transition: opacity 0.3s;
}
.quest-card.daily::before  { background: var(--cyan); }
.quest-card.weekly::before { background: var(--purple); }
.quest-card.custom::before { background: var(--fire); }
@keyframes cardIn { from{opacity:0;transform:translateX(-12px);} to{opacity:1;transform:translateX(0);} }
.quest-card:hover { border-color: var(--border2); transform: translateX(6px); }
.quest-card.done { opacity: 0.55; }
.quest-card.done .quest-name { text-decoration: line-through; color: var(--text2); }
.quest-cb { width: 20px; height: 20px; accent-color: var(--green); cursor: pointer; flex-shrink: 0; }
.quest-info { flex: 1; }
.quest-name { font-size: 0.95rem; font-weight: 600; margin-bottom: 4px; }
.quest-meta { display: flex; gap: 10px; align-items: center; }
.quest-type-tag { font-family: 'Press Start 2P', monospace; font-size: 0.45rem; padding: 2px 8px; border-radius: 2px; border: 1px solid; }
.quest-type-tag.daily  { color: var(--cyan); border-color: var(--cyan); }
.quest-type-tag.weekly { color: var(--purple); border-color: var(--purple); }
.quest-type-tag.custom { color: var(--fire); border-color: var(--fire); }
.quest-xp-tag { font-family: 'Share Tech Mono', monospace; font-size: 0.75rem; color: var(--gold); text-shadow: 0 0 6px var(--gold); }
.quest-actions { display: flex; gap: 6px; }
.q-act-btn { background: none; border: none; cursor: pointer; font-size: 0.9rem; padding: 6px 8px; border-radius: 3px; transition: background 0.2s; opacity: 0.6; }
.q-act-btn:hover { background: var(--panel2); opacity: 1; }

/* ════════════════════════════════════════
   HEALTH PAGE
════════════════════════════════════════ */
.health-wrap { max-width: 1000px; margin: 0 auto; }
.health-2col { display: grid; grid-template-columns: 1fr 1fr; gap: 16px; margin-bottom: 16px; }
.health-fields { display: flex; flex-direction: column; gap: 12px; }
.h-row { display: flex; align-items: center; gap: 12px; }
.h-ico { font-size: 1.2rem; width: 26px; flex-shrink: 0; }
.h-row label { min-width: 90px; color: var(--text2); font-size: 0.9rem; }
.h-row .rpg-input { flex: 1; margin-bottom: 0; }
.mood-row .rpg-input { flex: 1; }
.mood-val { font-family: 'Press Start 2P', monospace; font-size: 1rem; color: var(--cyan); min-width: 26px; text-shadow: 0 0 8px var(--cyan); }
.goals-status { display: flex; flex-direction: column; gap: 12px; }
.goal-row { display: flex; align-items: center; gap: 10px; }
.goal-ico { font-size: 1.2rem; width: 24px; }
.goal-lbl { min-width: 90px; font-size: 0.85rem; color: var(--text2); }
.goal-track { flex: 1; height: 10px; background: rgba(255,255,255,0.07); border-radius: 2px; overflow: hidden; border: 1px solid var(--border); }
.goal-fill { height: 100%; border-radius: 2px; transition: width 0.7s cubic-bezier(.23,1,.32,1); }
.goal-pct { font-family: 'Press Start 2P', monospace; font-size: 0.5rem; min-width: 40px; text-align: right; }
.health-history { max-height: 400px; overflow-y: auto; display: flex; flex-direction: column; gap: 10px; }
.hlog-entry { padding: 12px 16px; background: var(--panel2); border: 1px solid var(--border); border-radius: 3px; }
.hlog-date { font-family: 'Press Start 2P', monospace; font-size: 0.5rem; color: var(--cyan); margin-bottom: 8px; }
.hlog-data { display: flex; gap: 16px; flex-wrap: wrap; }
.hlog-metric { font-size: 0.82rem; }
.hlog-metric span { color: var(--text2); }

/* ════════════════════════════════════════
   ANALYTICS
════════════════════════════════════════ */
.charts-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 16px; }
.chart-panel canvas { width: 100%; }
.span2 { grid-column: 1 / 3; }

/* ════════════════════════════════════════
   LEADERBOARD
════════════════════════════════════════ */
.lb-wrap { max-width: 700px; margin: 0 auto; }
.lb-list { display: flex; flex-direction: column; gap: 10px; }
.lb-row {
  display: flex; align-items: center; gap: 14px;
  padding: 14px 18px;
  background: var(--panel2);
  border: 1px solid var(--border);
  border-radius: 3px;
  transition: all 0.2s;
}
.lb-row:hover { border-color: var(--border2); transform: translateX(6px); }
.lb-row.me-row { border-color: rgba(0,255,255,0.4); background: rgba(0,255,255,0.06); }
.lb-rank { font-family: 'Press Start 2P', monospace; font-size: 0.8rem; min-width: 32px; }
.lb-rank.gold-r  { color: var(--gold); text-shadow: 0 0 8px var(--gold); }
.lb-rank.silv-r  { color: #c0c0c0; }
.lb-rank.bron-r  { color: #cd7f32; }
.lb-ava  { font-size: 1.5rem; }
.lb-name { flex: 1; font-weight: 700; font-size: 0.95rem; }
.lb-lv   { font-family: 'Press Start 2P', monospace; font-size: 0.5rem; color: var(--cyan); }
.lb-xp   { font-family: 'Share Tech Mono', monospace; font-size: 0.9rem; color: var(--gold); }
.me-tag  { font-family: 'Press Start 2P', monospace; font-size: 0.45rem; color: var(--cyan); margin-left: 6px; }

/* ════════════════════════════════════════
   SETTINGS
════════════════════════════════════════ */
.settings-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 16px; max-width: 900px; margin: 0 auto; }
.setting-row { display: flex; align-items: center; justify-content: space-between; padding: 8px 0; }
.set-lbl { font-size: 0.55rem; color: var(--text2); letter-spacing: 2px; }
.rpg-toggle { position: relative; display: inline-block; width: 50px; height: 26px; }
.rpg-toggle input { opacity: 0; width: 0; height: 0; }
.toggle-track { position: absolute; inset: 0; background: var(--panel2); border: 1px solid var(--border); border-radius: 26px; cursor: pointer; transition: all 0.3s; }
.toggle-track::before { content:''; position:absolute; width:18px; height:18px; left:4px; top:3px; background: var(--text3); border-radius:50%; transition:0.3s; }
input:checked + .toggle-track { background: rgba(0,255,255,0.15); border-color: var(--cyan); }
input:checked + .toggle-track::before { transform: translateX(24px); background: var(--cyan); box-shadow: 0 0 8px var(--cyan); }
.goals-form-grid { display: flex; flex-direction: column; gap: 10px; }
.danger-zone { border-color: rgba(255,34,68,0.3); }
.danger-title { color: var(--red) !important; text-shadow: 0 0 8px var(--red) !important; }
.danger-txt { font-size: 0.85rem; color: var(--text2); }

/* ════════════════════════════════════════
   BOTTOM HOTBAR
════════════════════════════════════════ */
.hotbar {
  position: fixed; bottom: 0; left: 0; right: 0; z-index: 200;
  height: 72px;
  background: rgba(4,8,20,0.98);
  border-top: 1px solid var(--border);
  backdrop-filter: blur(16px);
  box-shadow: 0 -2px 30px rgba(0,0,0,0.9), 0 -1px 0 rgba(0,255,255,0.08);
}
.hotbar-glow-bar { height: 1px; background: linear-gradient(90deg, transparent, var(--cyan), transparent); opacity: 0.3; }
.hotbar-slots { display: flex; align-items: center; justify-content: space-around; height: calc(100% - 1px); padding: 0 8px; }
.hslot {
  position: relative; overflow: visible;
  display: flex; flex-direction: column; align-items: center; justify-content: center; gap: 3px;
  padding: 6px 8px; min-width: 52px; height: 58px;
  background: transparent; border: 1px solid transparent;
  border-radius: 4px; cursor: pointer;
  transition: all 0.2s;
}
.hslot:hover { border-color: var(--border); background: rgba(0,255,255,0.06); transform: translateY(-3px); }
.hslot.active { border-color: rgba(0,255,255,0.4); background: rgba(0,255,255,0.1); }
.hslot-glow { position: absolute; inset: 0; border-radius: 4px; opacity: 0; background: radial-gradient(circle, rgba(0,255,255,0.15), transparent); transition: opacity 0.3s; pointer-events: none; }
.hslot.active .hslot-glow, .hslot:hover .hslot-glow { opacity: 1; }
.hslot-icon { font-size: 1.3rem; transition: transform 0.2s; }
.hslot:hover .hslot-icon { transform: scale(1.2); }
.hslot.active .hslot-icon { filter: drop-shadow(0 0 6px var(--cyan)); }
.hslot-lbl { font-size: 0.42rem; color: var(--text2); transition: color 0.2s; }
.hslot.active .hslot-lbl { color: var(--cyan); text-shadow: 0 0 6px var(--cyan); }

/* CENTER HEALTH BUTTON */
.center-slot {
  border-color: rgba(255,34,68,0.3);
  background: rgba(255,34,68,0.07);
  width: 64px; height: 64px;
  border-radius: 50% !important;
  border-width: 2px;
  transform: translateY(-8px);
  box-shadow: 0 4px 20px rgba(0,0,0,0.8);
}
.center-slot:hover { transform: translateY(-14px); border-color: var(--red) !important; box-shadow: 0 0 20px rgba(255,34,68,0.6); }
.center-slot.active { border-color: var(--red) !important; box-shadow: 0 0 20px rgba(255,34,68,0.5); background: rgba(255,34,68,0.15); }
.center-slot-ring {
  position: absolute; inset: -4px; border-radius: 50%;
  border: 1px solid rgba(255,34,68,0.3);
  animation: centerRingPulse 2s ease-in-out infinite;
}
@keyframes centerRingPulse { 0%,100%{transform:scale(1);opacity:.4;} 50%{transform:scale(1.15);opacity:.8;} }
.center-icon { font-size: 1.5rem; }
.center-slot .hslot-lbl { font-size: 0.38rem; }

/* ════════════════════════════════════════
   LEVEL UP OVERLAY
════════════════════════════════════════ */
.levelup-overlay {
  position: fixed; inset: 0; z-index: 999;
  display: flex; align-items: center; justify-content: center;
  background: rgba(0,0,0,0.92);
  animation: luFadeIn 0.3s ease;
}
.levelup-overlay.hidden { display: none; }
@keyframes luFadeIn { from{opacity:0;} to{opacity:1;} }
.lu-bg-flash { position: absolute; inset: 0; background: var(--gold); opacity: 0; animation: bgFlash 0.6s ease-out 0.1s; pointer-events: none; }
@keyframes bgFlash { 0%{opacity:.6;} 100%{opacity:0;} }
.lu-box {
  position: relative; z-index: 2; text-align: center;
  padding: 48px 60px; max-width: 400px; width: 90%;
  background: rgba(8,12,28,0.98);
  border: 2px solid var(--gold);
  border-radius: 6px;
  box-shadow: var(--glow-g), 0 20px 80px rgba(0,0,0,0.95);
  animation: luBoxIn 0.5s cubic-bezier(.23,1,.32,1);
}
@keyframes luBoxIn { from{transform:scale(.3);opacity:0;} to{transform:scale(1);opacity:1;} }
.lu-rings { position: absolute; inset: -20px; pointer-events: none; }
.lu-ring { position: absolute; border-radius: 50%; border: 1px solid var(--gold); opacity: 0; animation: luRingExpand 2s ease-out infinite; }
.lr1 { inset: 20px; animation-delay: 0s; }
.lr2 { inset: 0; animation-delay: 0.4s; }
.lr3 { inset: -20px; animation-delay: 0.8s; }
@keyframes luRingExpand { 0%{opacity:.8;transform:scale(.6);} 100%{opacity:0;transform:scale(1.3);} }
.lu-title { font-size: 1.2rem; color: var(--gold); text-shadow: 0 0 30px var(--gold); letter-spacing: 6px; margin-bottom: 12px; animation: luTitlePulse 1s ease-in-out infinite; }
@keyframes luTitlePulse { 0%,100%{text-shadow:0 0 30px var(--gold);} 50%{text-shadow:0 0 60px var(--gold), 0 0 100px var(--gold);} }
.lu-lvnum { font-size: 4.5rem; color: var(--cyan); text-shadow: 0 0 40px var(--cyan); line-height: 1; margin-bottom: 6px; animation: luNumIn 0.6s cubic-bezier(.23,1,.32,1) 0.3s both; }
@keyframes luNumIn { from{transform:scale(3);opacity:0;} to{transform:scale(1);opacity:1;} }
.lu-classname { font-size: 0.65rem; color: var(--purple); letter-spacing: 5px; margin: 8px 0 16px; text-shadow: 0 0 10px var(--purple); }
.lu-perks { display: flex; flex-direction: column; gap: 6px; margin: 12px 0 20px; }
.lu-perk { font-size: 0.82rem; color: var(--text); padding: 6px 12px; background: rgba(191,90,242,0.1); border: 1px solid rgba(191,90,242,0.3); border-radius: 3px; }
.lu-confetti { position: absolute; inset: 0; pointer-events: none; z-index: 1; }
.confetti-piece { position: absolute; width: 8px; height: 8px; border-radius: 2px; animation: confettiFall linear forwards; }
@keyframes confettiFall {
  0%{ top:-10px; opacity:1; }
  100%{ top:110%; opacity:0; transform:rotate(720deg) translateX(var(--drift)); }
}

/* ════════════════════════════════════════
   FLOATING DAMAGE NUMBERS
════════════════════════════════════════ */
.dmg-layer { position: fixed; inset: 0; z-index: 998; pointer-events: none; }
.dmg-num {
  position: absolute;
  font-family: 'Press Start 2P', monospace;
  font-size: 1.1rem;
  color: var(--gold);
  text-shadow: 0 0 12px var(--gold), 0 2px 4px rgba(0,0,0,0.8);
  pointer-events: none;
  white-space: nowrap;
  animation: dmgFloat 1.6s cubic-bezier(.23,1,.32,1) forwards;
}
@keyframes dmgFloat {
  0%   { opacity: 1; transform: translateY(0) scale(1); }
  30%  { opacity: 1; transform: translateY(-30px) scale(1.3); }
  100% { opacity: 0; transform: translateY(-80px) scale(0.7); }
}

/* ════════════════════════════════════════
   NOTIFICATION TOAST
════════════════════════════════════════ */
.notif-toast {
  position: fixed; top: 70px; right: 20px; z-index: 997;
  animation: notifSlide 0.4s cubic-bezier(.23,1,.32,1);
}
.notif-inner {
  display: flex; align-items: center; gap: 10px;
  padding: 12px 18px;
  background: rgba(8,14,28,0.97);
  border: 1px solid var(--purple);
  border-radius: 4px;
  box-shadow: var(--glow-p);
  max-width: 320px;
}
.notif-ico { font-size: 1.3rem; }
.notif-msg { font-size: 0.55rem; color: var(--text); letter-spacing: 1px; }
@keyframes notifSlide { from{opacity:0;transform:translateX(30px);} to{opacity:1;transform:translateX(0);} }

/* ════════════════════════════════════════
   MODALS
════════════════════════════════════════ */
.modal-bg {
  position: fixed; inset: 0; z-index: 500;
  display: flex; align-items: center; justify-content: center;
  background: rgba(0,0,0,0.8); backdrop-filter: blur(8px);
}
.modal-box {
  min-width: 340px; max-width: 460px; width: 90%;
  animation: luBoxIn 0.35s cubic-bezier(.23,1,.32,1);
}
.modal-btns { display: flex; gap: 10px; justify-content: flex-end; margin-top: 12px; }

/* ════════════════════════════════════════
   SCROLLBAR
════════════════════════════════════════ */
::-webkit-scrollbar { width: 5px; height: 5px; }
::-webkit-scrollbar-track { background: transparent; }
::-webkit-scrollbar-thumb { background: var(--border2); border-radius: 3px; }

/* ════════════════════════════════════════
   SCREEN SHAKE
════════════════════════════════════════ */
@keyframes screenShake {
  0%,100%{transform:translate(0,0);}
  10%{transform:translate(-4px,2px);}
  20%{transform:translate(4px,-2px);}
  30%{transform:translate(-3px,3px);}
  40%{transform:translate(3px,-1px);}
  50%{transform:translate(-2px,2px);}
  60%{transform:translate(2px,-3px);}
  70%{transform:translate(-1px,1px);}
  80%{transform:translate(1px,0);}
  90%{transform:translate(-1px,-1px);}
}
.shake { animation: screenShake 0.5s ease; }

/* ════════════════════════════════════════
   LIGHT THEME OVERRIDES
════════════════════════════════════════ */
[data-theme="light"] .top-hud { background: rgba(20,28,70,0.98); }
[data-theme="light"] .hotbar  { background: rgba(20,28,70,0.98); }
[data-theme="light"] .rpg-panel { box-shadow: 0 4px 20px rgba(0,0,40,0.15); }
[data-theme="light"] .rpc { border-color: var(--cyan); }

/* ════════════════════════════════════════
   RESPONSIVE
════════════════════════════════════════ */
@media(max-width:1100px){
  .dash-layout { grid-template-columns: 180px 1fr; }
  .stat-orbs-wrap { grid-column: 2; }
  .vitals-panel { grid-column: 1 / 3; }
  .badges-panel { grid-column: 1 / 3; }
  .ava-page-layout { grid-template-columns: 1fr; }
  .ava-main-panel { max-width: 400px; margin: 0 auto; }
  .charts-grid { grid-template-columns: 1fr; }
  .span2 { grid-column: 1; }
  .settings-grid { grid-template-columns: 1fr; }
}
@media(max-width:768px){
  .dash-layout { grid-template-columns: 1fr; }
  .ava-card { grid-row: auto; flex-direction: row; align-items: center; text-align: left; gap: 16px; }
  .stat-orbs-wrap { grid-column: 1; grid-template-columns: repeat(2,1fr); }
  .dash-quests, .ai-panel, .vitals-panel, .badges-panel { grid-column: 1; }
  .health-2col { grid-template-columns: 1fr; }
  .vitals-grid { grid-template-columns: repeat(3,1fr); }
  .hud-center { display: none; }
  .hotbar-slots { gap: 4px; }
  .hslot { min-width: 40px; padding: 4px; }
  .hslot-lbl { display: none; }
  .center-slot { width: 54px; height: 54px; }
}
@media(max-width:480px){
  .login-wrap { padding: 16px; }
  .login-title { font-size: 1.4rem; }
  .lu-box { padding: 32px 20px; }
  .lu-lvnum { font-size: 3rem; }
  .stat-orbs-wrap { grid-template-columns: repeat(2,1fr); }
  .vitals-grid { grid-template-columns: repeat(2,1fr); }
}
</style>
<body>

<!-- GLOBAL PARTICLE CANVAS -->
<canvas id="bg-canvas" class="bg-canvas"></canvas>

<!-- ═══════════════════════════════════
  LOGIN SCREEN
═══════════════════════════════════ -->
<div id="login-screen" class="screen">
  <div class="login-wrap">
    <div class="login-logo-area">
      <div class="login-emblem">
        <canvas id="login-avatar-canvas" width="100" height="120"></canvas>
        <div class="emblem-ring r1"></div>
        <div class="emblem-ring r2"></div>
        <div class="emblem-ring r3"></div>
      </div>
      <h1 class="login-title pixel-font">VITA<span class="title-accent">QUEST</span></h1>
      <p class="login-sub">⚔ &nbsp; YOUR HEALTH. YOUR LEGEND. &nbsp; ⚔</p>
      <div class="login-version pixel-font">RPG HEALTH TRACKER v2.0</div>
    </div>

    <div class="rpg-panel login-panel">
      <div class="rpc tl"></div><div class="rpc tr"></div><div class="rpc bl"></div><div class="rpc br"></div>
      <div class="rpg-panel-title pixel-font">— ENTER YOUR REALM —</div>

      <div class="login-field">
        <label class="pixel-font field-label">HERO ID</label>
        <div class="rpg-input-wrap">
          <span class="inp-icon">⚔</span>
          <input type="text" id="login-user" placeholder="admin" autocomplete="off"/>
        </div>
      </div>
      <div class="login-field">
        <label class="pixel-font field-label">SECRET RUNE</label>
        <div class="rpg-input-wrap">
          <span class="inp-icon">🔮</span>
          <input type="password" id="login-pass" placeholder="••••••••"/>
        </div>
      </div>

      <div id="login-error" class="login-error hidden">
        <span class="pixel-font">✗ INVALID CREDENTIALS</span>
      </div>

      <button class="rpg-btn primary login-btn" onclick="doLogin()">
        <span class="pixel-font">▶ BEGIN QUEST</span>
        <div class="btn-sheen"></div>
      </button>
      <p class="login-hint pixel-font">admin / 12345678</p>
    </div>
  </div>
</div>

<!-- ═══════════════════════════════════
  GAME SCREEN
═══════════════════════════════════ -->
<div id="game-screen" class="screen hidden">

  <!-- TOP HUD -->
  <header class="top-hud">
    <div class="hud-left">
      <canvas id="hud-avatar-canvas" width="36" height="44"></canvas>
      <div class="hud-bars-col">
        <div class="hud-name pixel-font" id="hud-name">ADMIN</div>
        <div class="hud-bar-row">
          <span class="bar-lbl pixel-font hp-c">HP</span>
          <div class="hud-bar-track"><div id="hud-hp" class="hud-bar-inner hp-bar"></div></div>
          <span class="bar-val pixel-font" id="hud-hp-v">100</span>
        </div>
        <div class="hud-bar-row">
          <span class="bar-lbl pixel-font xp-c">XP</span>
          <div class="hud-bar-track"><div id="hud-xp" class="hud-bar-inner xp-bar-h"></div></div>
          <span class="bar-val pixel-font" id="hud-xp-v">0</span>
        </div>
      </div>
    </div>

    <div class="hud-center">
      <div class="level-badge">
        <div class="pixel-font lv-tag">LV</div>
        <div class="pixel-font lv-num" id="hud-level">1</div>
      </div>
      <div class="pixel-font hud-class" id="hud-class">NOVICE</div>
    </div>

    <div class="hud-right">
      <div class="hud-pill fire-pill"><span>🔥</span><span class="pixel-font" id="hud-streak">0</span></div>
      <div class="hud-pill sword-pill"><span>⚔</span><span class="pixel-font" id="hud-tasks">0</span></div>
      <button class="hud-btn" onclick="toggleTheme()" id="theme-btn">🌙</button>
      <button class="hud-btn red-btn" onclick="doLogout()">⏻</button>
    </div>
  </header>

  <!-- PAGE CONTAINER -->
  <main class="game-world" id="game-world">

    <!-- DASHBOARD -->
    <section id="page-dashboard" class="gpage active">
      <div class="page-bg-hex"></div>
      <div class="hero-banner">
        <div class="hero-banner-content">
          <div class="pixel-font hero-greet" id="hero-greet">WELCOME BACK, HERO!</div>
          <div class="hero-greet-sub" id="hero-sub">Your legend continues...</div>
        </div>
        <div class="banner-runes" id="banner-runes"></div>
      </div>

      <div class="dash-layout">
        <!-- Avatar Card -->
        <div class="rpg-panel ava-card">
          <div class="rpc tl"></div><div class="rpc tr"></div><div class="rpc bl"></div><div class="rpc br"></div>
          <div class="rpg-panel-title pixel-font">YOUR HERO</div>
          <div class="ava-mini-stage">
            <div class="ava-glow-ring" id="dash-glow"></div>
            <canvas id="dash-ava" width="110" height="140"></canvas>
          </div>
          <div class="pixel-font ava-class-tag" id="dash-class">NOVICE</div>
          <div class="ava-lv-tag pixel-font">LV <span id="dash-lv">1</span></div>
          <div class="mini-xp-wrap">
            <div class="mini-xp-track"><div id="dash-xp-bar" class="mini-xp-inner"></div></div>
            <div class="pixel-font mini-xp-text" id="dash-xp-text">0/100</div>
          </div>
        </div>

        <!-- Stat Orbs -->
        <div class="stat-orbs-wrap">
          <div class="stat-orb c-cyan" onclick="navigate('tasks')">
            <div class="orb-glow"></div>
            <div class="orb-icon">⚡</div>
            <div class="pixel-font orb-val" id="orb-xp">0</div>
            <div class="orb-label">XP</div>
          </div>
          <div class="stat-orb c-gold" onclick="navigate('avatar')">
            <div class="orb-glow"></div>
            <div class="orb-icon">🌟</div>
            <div class="pixel-font orb-val" id="orb-lv">1</div>
            <div class="orb-label">LEVEL</div>
          </div>
          <div class="stat-orb c-fire" onclick="navigate('tasks')">
            <div class="orb-glow"></div>
            <div class="orb-icon">🔥</div>
            <div class="pixel-font orb-val" id="orb-streak">0</div>
            <div class="orb-label">STREAK</div>
          </div>
          <div class="stat-orb c-green" onclick="navigate('tasks')">
            <div class="orb-glow"></div>
            <div class="orb-icon">✓</div>
            <div class="pixel-font orb-val" id="orb-done">0</div>
            <div class="orb-label">QUESTS</div>
          </div>
        </div>

        <!-- Today Quests -->
        <div class="rpg-panel dash-quests">
          <div class="rpc tl"></div><div class="rpc tr"></div><div class="rpc bl"></div><div class="rpc br"></div>
          <div class="rpg-panel-title pixel-font">TODAY'S QUESTS <span class="qcount pixel-font" id="qcount">0/0</span></div>
          <div id="dash-quest-list" class="dash-quest-list"></div>
          <button class="rpg-btn sm-btn mt8" onclick="navigate('tasks')"><span class="pixel-font">ALL QUESTS →</span></button>
        </div>

        <!-- AI Advisor -->
        <div class="rpg-panel ai-panel">
          <div class="rpc tl"></div><div class="rpc tr"></div><div class="rpc bl"></div><div class="rpc br"></div>
          <div class="rpg-panel-title pixel-font">🤖 AI ADVISOR</div>
          <div id="ai-tips" class="ai-tips"></div>
        </div>

        <!-- Vitals -->
        <div class="rpg-panel vitals-panel">
          <div class="rpc tl"></div><div class="rpc tr"></div><div class="rpc bl"></div><div class="rpc br"></div>
          <div class="rpg-panel-title pixel-font">VITALS</div>
          <div id="vitals-grid" class="vitals-grid"></div>
        </div>

        <!-- Badges -->
        <div class="rpg-panel badges-panel">
          <div class="rpc tl"></div><div class="rpc tr"></div><div class="rpc bl"></div><div class="rpc br"></div>
          <div class="rpg-panel-title pixel-font">ACHIEVEMENTS</div>
          <div id="dash-badges" class="badges-row"></div>
        </div>
      </div>
    </section>

    <!-- AVATAR PAGE -->
    <section id="page-avatar" class="gpage hidden">
      <div class="page-bg-hex purple-bg"></div>
      <div class="page-header-banner"><div class="pixel-font">⚔ YOUR CHARACTER ⚔</div></div>
      <div class="ava-page-layout">
        <div class="rpg-panel ava-main-panel">
          <div class="rpc tl"></div><div class="rpc tr"></div><div class="rpc bl"></div><div class="rpc br"></div>
          <div class="rpg-panel-title pixel-font">CHARACTER SCREEN</div>
          <div class="ava-big-stage">
            <div class="orbit-ring or1"></div><div class="orbit-ring or2"></div>
            <canvas id="main-ava" width="190" height="240"></canvas>
            <div class="ava-nameplate">
              <div class="pixel-font ava-big-class" id="ava-big-class">NOVICE</div>
              <div class="pixel-font ava-big-lv">LEVEL <span id="ava-big-lv">1</span></div>
            </div>
          </div>
          <div class="ava-xp-block">
            <div class="pixel-font ava-xp-lbl">XP PROGRESS</div>
            <div class="rpg-xp-bar"><div id="ava-xp-fill" class="rpg-xp-inner"></div></div>
            <div class="pixel-font ava-xp-nums" id="ava-xp-nums">0 / 100</div>
          </div>
          <div class="evo-chain-block">
            <div class="pixel-font evo-chain-title">EVOLUTION PATH</div>
            <div id="evo-chain" class="evo-chain"></div>
          </div>
        </div>
        <div class="ava-side-panels">
          <div class="rpg-panel">
            <div class="rpc tl"></div><div class="rpc tr"></div><div class="rpc bl"></div><div class="rpc br"></div>
            <div class="rpg-panel-title pixel-font">CLASS PERKS</div>
            <div id="ava-perks" class="ava-perks"></div>
          </div>
          <div class="rpg-panel">
            <div class="rpc tl"></div><div class="rpc tr"></div><div class="rpc bl"></div><div class="rpc br"></div>
            <div class="rpg-panel-title pixel-font">EARNED BADGES</div>
            <div id="ava-badges" class="badges-row wrap"></div>
          </div>
          <div class="rpg-panel">
            <div class="rpc tl"></div><div class="rpc tr"></div><div class="rpc bl"></div><div class="rpc br"></div>
            <div class="rpg-panel-title pixel-font">LEVEL HISTORY</div>
            <div id="ava-history" class="ava-history"></div>
          </div>
        </div>
      </div>
    </section>

    <!-- TASKS PAGE -->
    <section id="page-tasks" class="gpage hidden">
      <div class="page-bg-hex blue-bg"></div>
      <div class="page-header-banner"><div class="pixel-font">⚔ QUEST BOARD ⚔</div></div>
      <div class="tasks-wrap">
        <div class="rpg-panel add-task-panel">
          <div class="rpc tl"></div><div class="rpc tr"></div><div class="rpc bl"></div><div class="rpc br"></div>
          <div class="rpg-panel-title pixel-font">+ NEW QUEST</div>
          <div class="add-task-form">
            <input type="text" id="task-name-input" class="rpg-input" placeholder="Quest name..." maxlength="60"/>
            <select id="task-type-select" class="rpg-select">
              <option value="daily">DAILY</option>
              <option value="weekly">WEEKLY</option>
              <option value="custom">CUSTOM</option>
            </select>
            <select id="task-xp-select" class="rpg-select">
              <option value="10">10 XP — EASY</option>
              <option value="25">25 XP — MEDIUM</option>
              <option value="50">50 XP — HARD</option>
              <option value="100">100 XP — EPIC</option>
            </select>
            <button class="rpg-btn primary" onclick="addTask()"><span class="pixel-font">POST QUEST</span></button>
          </div>
        </div>
        <div class="quest-tabs">
          <button class="qtab active pixel-font" onclick="filterTasks('all',this)">ALL</button>
          <button class="qtab pixel-font" onclick="filterTasks('daily',this)">DAILY</button>
          <button class="qtab pixel-font" onclick="filterTasks('weekly',this)">WEEKLY</button>
          <button class="qtab pixel-font" onclick="filterTasks('custom',this)">CUSTOM</button>
          <button class="qtab pixel-font" onclick="filterTasks('done',this)">DONE</button>
        </div>
        <div id="tasks-container" class="quests-list"></div>
      </div>
    </section>

    <!-- HEALTH PAGE -->
    <section id="page-health" class="gpage hidden">
      <div class="page-bg-hex green-bg"></div>
      <div class="page-header-banner"><div class="pixel-font">❤ VITAL CHAMBER ❤</div></div>
      <div class="health-wrap">
        <div class="health-2col">
          <div class="rpg-panel health-form-panel">
            <div class="rpc tl"></div><div class="rpc tr"></div><div class="rpc bl"></div><div class="rpc br"></div>
            <div class="rpg-panel-title pixel-font">LOG TODAY</div>
            <div class="health-fields">
              <div class="h-row"><span class="h-ico">👟</span><label>Steps</label><input type="number" id="h-steps" class="rpg-input" placeholder="8000"/></div>
              <div class="h-row"><span class="h-ico">🔥</span><label>Calories</label><input type="number" id="h-calories" class="rpg-input" placeholder="500"/></div>
              <div class="h-row"><span class="h-ico">😴</span><label>Sleep hrs</label><input type="number" id="h-sleep" class="rpg-input" placeholder="7.5" step="0.5"/></div>
              <div class="h-row"><span class="h-ico">💧</span><label>Water gl.</label><input type="number" id="h-water" class="rpg-input" placeholder="8"/></div>
              <div class="h-row"><span class="h-ico">⚖</span><label>Weight kg</label><input type="number" id="h-weight" class="rpg-input" placeholder="72" step="0.1"/></div>
              <div class="h-row mood-row">
                <span class="h-ico">😊</span><label>Mood</label>
                <input type="range" id="h-mood" min="1" max="10" value="5" class="rpg-slider" oninput="document.getElementById('mood-v').textContent=this.value"/>
                <span class="pixel-font mood-val" id="mood-v">5</span>
              </div>
            </div>
            <button class="rpg-btn primary full-w mt8" onclick="logHealth()"><span class="pixel-font">⚡ LOG & EARN XP</span></button>
          </div>
          <div class="rpg-panel goals-panel">
            <div class="rpc tl"></div><div class="rpc tr"></div><div class="rpc bl"></div><div class="rpc br"></div>
            <div class="rpg-panel-title pixel-font">GOAL STATUS</div>
            <div id="goals-status" class="goals-status"></div>
          </div>
        </div>
        <div class="rpg-panel history-panel">
          <div class="rpc tl"></div><div class="rpc tr"></div><div class="rpc bl"></div><div class="rpc br"></div>
          <div class="rpg-panel-title pixel-font">HEALTH LOG</div>
          <div id="health-history" class="health-history"></div>
        </div>
      </div>
    </section>

    <!-- ANALYTICS PAGE -->
    <section id="page-analytics" class="gpage hidden">
      <div class="page-bg-hex cyan-bg"></div>
      <div class="page-header-banner"><div class="pixel-font">📊 WAR ROOM 📊</div></div>
      <div class="charts-grid">
        <div class="rpg-panel chart-panel"><div class="rpc tl"></div><div class="rpc tr"></div><div class="rpc bl"></div><div class="rpc br"></div><div class="rpg-panel-title pixel-font">⚡ XP HISTORY</div><canvas id="chart-xp" height="170"></canvas></div>
        <div class="rpg-panel chart-panel"><div class="rpc tl"></div><div class="rpc tr"></div><div class="rpc bl"></div><div class="rpc br"></div><div class="rpg-panel-title pixel-font">👟 STEPS</div><canvas id="chart-steps" height="170"></canvas></div>
        <div class="rpg-panel chart-panel"><div class="rpc tl"></div><div class="rpc tr"></div><div class="rpc bl"></div><div class="rpc br"></div><div class="rpg-panel-title pixel-font">💧 WATER</div><canvas id="chart-water" height="170"></canvas></div>
        <div class="rpg-panel chart-panel"><div class="rpc tl"></div><div class="rpc tr"></div><div class="rpc bl"></div><div class="rpc br"></div><div class="rpg-panel-title pixel-font">😴 SLEEP</div><canvas id="chart-sleep" height="170"></canvas></div>
        <div class="rpg-panel chart-panel"><div class="rpc tl"></div><div class="rpc tr"></div><div class="rpc bl"></div><div class="rpc br"></div><div class="rpg-panel-title pixel-font">😊 MOOD</div><canvas id="chart-mood" height="170"></canvas></div>
        <div class="rpg-panel chart-panel"><div class="rpc tl"></div><div class="rpc tr"></div><div class="rpc bl"></div><div class="rpc br"></div><div class="rpg-panel-title pixel-font">🔥 CALORIES</div><canvas id="chart-calories" height="170"></canvas></div>
        <div class="rpg-panel chart-panel span2"><div class="rpc tl"></div><div class="rpc tr"></div><div class="rpc bl"></div><div class="rpc br"></div><div class="rpg-panel-title pixel-font">✓ QUEST COMPLETION</div><canvas id="chart-tasks" height="90"></canvas></div>
      </div>
    </section>

    <!-- LEADERBOARD PAGE -->
    <section id="page-leaderboard" class="gpage hidden">
      <div class="page-bg-hex gold-bg"></div>
      <div class="page-header-banner"><div class="pixel-font">🏆 HALL OF HEROES 🏆</div></div>
      <div class="lb-wrap">
        <div class="rpg-panel lb-panel">
          <div class="rpc tl"></div><div class="rpc tr"></div><div class="rpc bl"></div><div class="rpc br"></div>
          <div id="leaderboard-list" class="lb-list"></div>
        </div>
      </div>
    </section>

    <!-- SETTINGS PAGE -->
    <section id="page-settings" class="gpage hidden">
      <div class="page-bg-hex"></div>
      <div class="page-header-banner"><div class="pixel-font">⚙ GAME SETTINGS ⚙</div></div>
      <div class="settings-grid">
        <div class="rpg-panel">
          <div class="rpc tl"></div><div class="rpc tr"></div><div class="rpc bl"></div><div class="rpc br"></div>
          <div class="rpg-panel-title pixel-font">APPEARANCE</div>
          <div class="setting-row"><span class="pixel-font set-lbl">DARK / LIGHT</span><label class="rpg-toggle"><input type="checkbox" id="theme-cb" onchange="toggleTheme()"/><span class="toggle-track"></span></label></div>
        </div>
        <div class="rpg-panel">
          <div class="rpc tl"></div><div class="rpc tr"></div><div class="rpc bl"></div><div class="rpc br"></div>
          <div class="rpg-panel-title pixel-font">NOTIFICATIONS</div>
          <div class="setting-row"><span class="pixel-font set-lbl">REMINDERS</span><label class="rpg-toggle"><input type="checkbox" id="notif-cb" onchange="toggleNotifications()"/><span class="toggle-track"></span></label></div>
          <button class="rpg-btn sm-btn mt8" onclick="testNotification()"><span class="pixel-font">TEST ALERT</span></button>
        </div>
        <div class="rpg-panel">
          <div class="rpc tl"></div><div class="rpc tr"></div><div class="rpc bl"></div><div class="rpc br"></div>
          <div class="rpg-panel-title pixel-font">DAILY GOALS</div>
          <div class="goals-form-grid">
            <div class="h-row"><label>Steps</label><input type="number" id="goal-steps" class="rpg-input" value="10000"/></div>
            <div class="h-row"><label>Water (gl)</label><input type="number" id="goal-water" class="rpg-input" value="8"/></div>
            <div class="h-row"><label>Sleep (hr)</label><input type="number" id="goal-sleep" class="rpg-input" value="8"/></div>
            <div class="h-row"><label>Calories</label><input type="number" id="goal-calories" class="rpg-input" value="500"/></div>
          </div>
          <button class="rpg-btn primary mt8" onclick="saveGoals()"><span class="pixel-font">SAVE GOALS</span></button>
        </div>
        <div class="rpg-panel danger-zone">
          <div class="rpc tl"></div><div class="rpc tr"></div><div class="rpc bl"></div><div class="rpc br"></div>
          <div class="rpg-panel-title pixel-font danger-title">⚠ DANGER ZONE</div>
          <p class="danger-txt">Erase ALL progress, quests, and health data permanently.</p>
          <button class="rpg-btn danger mt8" onclick="confirmReset()"><span class="pixel-font">RESET ALL DATA</span></button>
        </div>
      </div>
    </section>

  </main>

  <!-- BOTTOM GAME HOTBAR NAV -->
  <nav class="hotbar">
    <div class="hotbar-glow-bar"></div>
    <div class="hotbar-slots">
      <button class="hslot active" id="nav-dashboard" onclick="navigate('dashboard')">
        <div class="hslot-glow"></div>
        <div class="hslot-icon">🏠</div>
        <div class="pixel-font hslot-lbl">HOME</div>
      </button>
      <button class="hslot" id="nav-avatar" onclick="navigate('avatar')">
        <div class="hslot-glow"></div>
        <div class="hslot-icon">🧙</div>
        <div class="pixel-font hslot-lbl">HERO</div>
      </button>
      <button class="hslot" id="nav-tasks" onclick="navigate('tasks')">
        <div class="hslot-glow"></div>
        <div class="hslot-icon">⚔</div>
        <div class="pixel-font hslot-lbl">QUESTS</div>
      </button>
      <button class="hslot center-slot" id="nav-health" onclick="navigate('health')">
        <div class="hslot-glow"></div>
        <div class="center-slot-ring"></div>
        <div class="hslot-icon center-icon">❤</div>
        <div class="pixel-font hslot-lbl">VITALS</div>
      </button>
      <button class="hslot" id="nav-analytics" onclick="navigate('analytics')">
        <div class="hslot-glow"></div>
        <div class="hslot-icon">📊</div>
        <div class="pixel-font hslot-lbl">STATS</div>
      </button>
      <button class="hslot" id="nav-leaderboard" onclick="navigate('leaderboard')">
        <div class="hslot-glow"></div>
        <div class="hslot-icon">🏆</div>
        <div class="pixel-font hslot-lbl">RANKS</div>
      </button>
      <button class="hslot" id="nav-settings" onclick="navigate('settings')">
        <div class="hslot-glow"></div>
        <div class="hslot-icon">⚙</div>
        <div class="pixel-font hslot-lbl">CONFIG</div>
      </button>
    </div>
  </nav>

</div><!-- /game-screen -->

<!-- ═══ OVERLAYS ═══ -->

<!-- LEVEL UP -->
<div id="levelup-overlay" class="levelup-overlay hidden">
  <div class="lu-bg-flash" id="lu-flash"></div>
  <div class="lu-box">
    <div class="lu-rings"><div class="lu-ring lr1"></div><div class="lu-ring lr2"></div><div class="lu-ring lr3"></div></div>
    <div class="pixel-font lu-title">LEVEL UP!</div>
    <div class="pixel-font lu-lvnum" id="lu-lvnum">2</div>
    <div class="pixel-font lu-classname" id="lu-classname">WARRIOR</div>
    <canvas id="lu-ava" width="140" height="180"></canvas>
    <div id="lu-perks" class="lu-perks"></div>
    <button class="rpg-btn primary" onclick="closeLevelUp()"><span class="pixel-font">▶ CONTINUE</span></button>
  </div>
  <div id="lu-confetti" class="lu-confetti"></div>
</div>

<!-- FLOATING DAMAGE NUMBERS -->
<div id="dmg-layer" class="dmg-layer"></div>

<!-- NOTIFICATION TOAST -->
<div id="notif-toast" class="notif-toast hidden">
  <div class="notif-inner">
    <span class="notif-ico">📬</span>
    <span class="pixel-font notif-msg" id="notif-msg">Drink water!</span>
  </div>
</div>

<!-- EDIT MODAL -->
<div id="edit-modal" class="modal-bg hidden" onclick="modalBgClick(event,'edit-modal')">
  <div class="rpg-panel modal-box">
    <div class="rpc tl"></div><div class="rpc tr"></div><div class="rpc bl"></div><div class="rpc br"></div>
    <div class="rpg-panel-title pixel-font">✏ EDIT QUEST</div>
    <input type="text" id="edit-name" class="rpg-input" placeholder="Quest name..."/>
    <select id="edit-type" class="rpg-select"><option value="daily">DAILY</option><option value="weekly">WEEKLY</option><option value="custom">CUSTOM</option></select>
    <select id="edit-xp" class="rpg-select"><option value="10">10 XP — EASY</option><option value="25">25 XP — MEDIUM</option><option value="50">50 XP — HARD</option><option value="100">100 XP — EPIC</option></select>
    <div class="modal-btns">
      <button class="rpg-btn sm-btn" onclick="closeEditModal()"><span class="pixel-font">CANCEL</span></button>
      <button class="rpg-btn primary" onclick="saveEditTask()"><span class="pixel-font">SAVE</span></button>
    </div>
  </div>
</div>

<!-- RESET MODAL -->
<div id="reset-modal" class="modal-bg hidden" onclick="modalBgClick(event,'reset-modal')">
  <div class="rpg-panel modal-box">
    <div class="rpc tl"></div><div class="rpc tr"></div><div class="rpc bl"></div><div class="rpc br"></div>
    <div class="rpg-panel-title pixel-font danger-title">⚠ RESET EVERYTHING?</div>
    <p class="danger-txt" style="margin-bottom:20px">ALL progress, quests, and XP will be permanently erased.</p>
    <div class="modal-btns">
      <button class="rpg-btn sm-btn" onclick="document.getElementById('reset-modal').classList.add('hidden')"><span class="pixel-font">CANCEL</span></button>
      <button class="rpg-btn danger" onclick="resetAllData()"><span class="pixel-font">WIPE ALL</span></button>
    </div>
  </div>
</div>
<script>
/* ════════════════════════════════════════
   VitaQuest RPG — script.js
   Particle engine, avatar, game logic
════════════════════════════════════════ */
'use strict';

/* ──────────────────────────────────────
   CONSTANTS
────────────────────────────────────── */
const CREDS = { user: 'admin', pass: '12345678' };

const CLASSES = [
  { min:0,   max:4,   name:'NOVICE',   icon:'🌱', color:'#39ff14', aura:'rgba(57,255,20,0.3)',  perks:['Basic stamina','Quest tracker active'] },
  { min:5,   max:9,   name:'WARRIOR',  icon:'🗡️', color:'#00ffff', aura:'rgba(0,255,255,0.35)', perks:['+10% XP from tasks','Streak bonuses unlocked'] },
  { min:10,  max:19,  name:'GUARDIAN', icon:'🛡️', color:'#bf5af2', aura:'rgba(191,90,242,0.4)', perks:['Health XP bonuses','Custom quests unlocked'] },
  { min:20,  max:39,  name:'CHAMPION', icon:'⚡', color:'#ffd60a', aura:'rgba(255,214,10,0.4)',  perks:['Epic quest XP ×2','Leaderboard ranked'] },
  { min:40,  max:99,  name:'ARCHMAGE', icon:'🔮', color:'#ff006e', aura:'rgba(255,0,110,0.4)',  perks:['All bonuses active','Particle aura unlocked'] },
  { min:100, max:9999,name:'LEGEND',   icon:'🌟', color:'#ffffff', aura:'rgba(255,255,255,0.5)',perks:['Legendary status','Permanent XP ×3'] },
];

const LEVEL_XP = [0,100,250,450,700,1000,1400,1900,2500,3200,
  4000,5000,6200,7600,9200,11000,13000,15500,18000,21000,25000];

const BADGES = [
  {id:'first_task',  ico:'⚔️',  name:'FIRST QUEST',  chk:s=>s.totalDone>=1},
  {id:'ten_tasks',   ico:'📜',  name:'QUESTER',      chk:s=>s.totalDone>=10},
  {id:'fifty_tasks', ico:'🏅',  name:'TASK MASTER',  chk:s=>s.totalDone>=50},
  {id:'hydrated',    ico:'💧',  name:'HYDRATED',     chk:s=>s.maxWater>=8},
  {id:'milemaker',   ico:'👟',  name:'MILEMAKER',    chk:s=>s.maxSteps>=10000},
  {id:'deep_sleep',  ico:'😴',  name:'DEEP DREAMER', chk:s=>s.maxSleep>=8},
  {id:'streak3',     ico:'🔥',  name:'ON FIRE',      chk:s=>s.streak>=3},
  {id:'streak7',     ico:'🗓️', name:'WEEK WARRIOR', chk:s=>s.streak>=7},
  {id:'streak30',    ico:'🦾',  name:'IRON WILL',    chk:s=>s.streak>=30},
  {id:'lv5',         ico:'🗡️', name:'WARRIOR BORN', chk:s=>s.level>=5},
  {id:'lv10',        ico:'🛡️', name:'GUARDIAN',     chk:s=>s.level>=10},
  {id:'lv20',        ico:'⚡',  name:'CHAMPION',     chk:s=>s.level>=20},
  {id:'logs5',       ico:'❤️',  name:'VITAL SIGNS',  chk:s=>s.healthLogs>=5},
  {id:'mood10',      ico:'😊',  name:'EUPHORIC',     chk:s=>s.maxMood>=10},
  {id:'lv2',         ico:'⬆️', name:'RISING STAR',  chk:s=>s.level>=2},
];

const MOCK_BOARD = [
  {name:'ZeroKnight', ava:'⚔️', level:42, xp:15200},
  {name:'HelioRune',  ava:'🔮', level:38, xp:12800},
  {name:'VitaStar',   ava:'🌟', level:35, xp:11400},
  {name:'IronClad',   ava:'🛡️', level:29, xp:8900},
  {name:'NebulaX',    ava:'⚡', level:25, xp:6700},
  {name:'SprintFox',  ava:'🦊', level:18, xp:4200},
  {name:'ByteHero',   ava:'🤖', level:12, xp:2800},
];

/* ──────────────────────────────────────
   STATE
────────────────────────────────────── */
let state = null;
let editingId = null;
let taskFilter = 'all';
let notifEnabled = false;
let notifTimer = null;

/* ─ Particle Engine state ─ */
let particles = [];
let bgRaf = null;
let bgCanvas, bgCtx;

/* ─ Avatar animation ─ */
let avaRaf = null;
let avaTime = 0;
let avaTargets = []; // { id, w, h, mini }

/* ──────────────────────────────────────
   DEFAULT STATE
────────────────────────────────────── */
function defaultState() {
  return {
    level:1, xp:0, streak:0, lastDate:null,
    totalDone:0, healthLogs:0,
    maxWater:0, maxSteps:0, maxSleep:0, maxMood:0,
    badges:[], history:[], tasks:defaultTasks(),
    healthData:[], xpHistory:[],
    goals:{steps:10000,water:8,sleep:8,calories:500},
    settings:{theme:'dark',notif:false},
  };
}
function defaultTasks() {
  return [
    {id:uid(),name:'Morning Workout',     type:'daily', xp:25, done:false, ts:Date.now()},
    {id:uid(),name:'Drink 8 glasses water',type:'daily',xp:10, done:false, ts:Date.now()},
    {id:uid(),name:'Walk 10,000 Steps',   type:'daily', xp:25, done:false, ts:Date.now()},
    {id:uid(),name:'Sleep 8 hours',       type:'daily', xp:15, done:false, ts:Date.now()},
    {id:uid(),name:'Weekly meal prep',    type:'weekly',xp:50, done:false, ts:Date.now()},
    {id:uid(),name:'Meditate 10 min',     type:'custom',xp:10, done:false, ts:Date.now()},
  ];
}
const uid = () => Math.random().toString(36).substr(2,9);
const today = () => new Date().toISOString().split('T')[0];
const clamp = (v,a,b) => Math.min(b,Math.max(a,v));
const esc = s => String(s).replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;');

/* ──────────────────────────────────────
   STORAGE
────────────────────────────────────── */
function save() { localStorage.setItem('vq2_state',JSON.stringify(state)); }
function load() {
  try { const r=localStorage.getItem('vq2_state'); if(r){state=JSON.parse(r);return true;} } catch{}
  return false;
}

/* ──────────────────────────────────────
   PARTICLE BG ENGINE
────────────────────────────────────── */
function initParticles() {
  bgCanvas = document.getElementById('bg-canvas');
  bgCtx = bgCanvas.getContext('2d');
  resizeBg();
  window.addEventListener('resize', resizeBg);
  spawnInitialParticles();
  bgLoop();
}

function resizeBg() {
  bgCanvas.width  = window.innerWidth;
  bgCanvas.height = window.innerHeight;
}

function spawnInitialParticles() {
  particles = [];
  const count = Math.min(80, Math.floor(window.innerWidth / 20));
  for (let i = 0; i < count; i++) spawnParticle(true);
}

function spawnParticle(initial=false) {
  const colors = ['rgba(0,255,255,0.7)','rgba(191,90,242,0.7)','rgba(255,214,10,0.5)','rgba(57,255,20,0.5)','rgba(255,0,110,0.6)'];
  const c = colors[Math.floor(Math.random()*colors.length)];
  particles.push({
    x: Math.random() * window.innerWidth,
    y: initial ? Math.random() * window.innerHeight : window.innerHeight + 5,
    vx: (Math.random()-0.5)*0.4,
    vy: -(0.2 + Math.random()*0.5),
    size: 1 + Math.random()*2,
    color: c,
    life: 1,
    decay: 0.0015 + Math.random()*0.003,
    twinkle: Math.random()*Math.PI*2,
    twinkleSpeed: 0.02 + Math.random()*0.04,
  });
}

function bgLoop() {
  const W = bgCanvas.width, H = bgCanvas.height;
  bgCtx.clearRect(0,0,W,H);

  // Dark vignette
  const isDark = document.documentElement.getAttribute('data-theme') !== 'light';
  if (isDark) {
    const vg = bgCtx.createRadialGradient(W/2,H/2,0,W/2,H/2,Math.max(W,H)*0.7);
    vg.addColorStop(0,'rgba(6,11,24,0)');
    vg.addColorStop(1,'rgba(2,4,12,0.7)');
    bgCtx.fillStyle = vg;
    bgCtx.fillRect(0,0,W,H);
  }

  // Draw hex grid (very subtle)
  drawHexGrid(bgCtx, W, H);

  // Particles
  particles = particles.filter(p => p.life > 0);
  particles.forEach(p => {
    p.x += p.vx; p.y += p.vy;
    p.life -= p.decay;
    p.twinkle += p.twinkleSpeed;
    const alpha = p.life * (0.5 + 0.5*Math.sin(p.twinkle));
    bgCtx.beginPath();
    bgCtx.arc(p.x, p.y, p.size, 0, Math.PI*2);
    bgCtx.fillStyle = p.color.replace(')',`,${alpha})`).replace('rgba(','rgba(');
    bgCtx.fill();
    // Small glow
    if (p.size > 1.5) {
      bgCtx.beginPath();
      bgCtx.arc(p.x, p.y, p.size*2.5, 0, Math.PI*2);
      bgCtx.fillStyle = p.color.replace(')',`,${alpha*0.15})`).replace('rgba(','rgba(');
      bgCtx.fill();
    }
  });

  // Spawn new particles
  if (Math.random() < 0.3) spawnParticle();

  bgRaf = requestAnimationFrame(bgLoop);
}

function drawHexGrid(ctx, W, H) {
  const isDark = document.documentElement.getAttribute('data-theme') !== 'light';
  if (!isDark) return;
  const size = 40, w = size*2, h = Math.sqrt(3)*size;
  ctx.strokeStyle = 'rgba(0,255,255,0.025)';
  ctx.lineWidth = 0.5;
  for (let row = -1; row < H/h + 1; row++) {
    for (let col = -1; col < W/w + 1; col++) {
      const x = col*w*1.5 + (row%2===0 ? 0 : w*0.75);
      const y = row*h;
      ctx.beginPath();
      for (let i=0;i<6;i++) {
        const angle = Math.PI/180 * (60*i - 30);
        const px = x + size * Math.cos(angle);
        const py = y + size * Math.sin(angle);
        i===0 ? ctx.moveTo(px,py) : ctx.lineTo(px,py);
      }
      ctx.closePath();
      ctx.stroke();
    }
  }
}

/* Burst particles on XP gain */
function burstParticles(x, y, count=20) {
  const colors = ['rgba(255,214,10,0.9)','rgba(0,255,255,0.9)','rgba(191,90,242,0.9)'];
  for (let i=0;i<count;i++) {
    const angle = (Math.PI*2/count)*i + Math.random()*0.5;
    const speed = 1 + Math.random()*3;
    const c = colors[Math.floor(Math.random()*colors.length)];
    particles.push({
      x,y,
      vx: Math.cos(angle)*speed,
      vy: Math.sin(angle)*speed - 2,
      size: 2 + Math.random()*3,
      color: c,
      life: 1,
      decay: 0.015 + Math.random()*0.02,
      twinkle: 0, twinkleSpeed: 0.05,
    });
  }
}

/* ──────────────────────────────────────
   AVATAR DRAWING ENGINE
────────────────────────────────────── */
function startAvatarLoop() {
  stopAvatarLoop();
  function loop(ts) {
    avaTime = ts/1000;
    avaTargets.forEach(t => {
      const canvas = document.getElementById(t.id);
      if (canvas) drawAvatar(canvas, t.w, t.h, t.mini, avaTime);
    });
    avaRaf = requestAnimationFrame(loop);
  }
  avaRaf = requestAnimationFrame(loop);
}
function stopAvatarLoop() { if(avaRaf){ cancelAnimationFrame(avaRaf); avaRaf=null; } }
function registerAvatar(id,w,h,mini) {
  avaTargets = avaTargets.filter(t=>t.id!==id);
  avaTargets.push({id,w,h,mini});
}
function unregisterAvatar(id) { avaTargets = avaTargets.filter(t=>t.id!==id); }

function drawAvatar(canvas, W, H, mini, t) {
  if (!canvas) return;
  const ctx = canvas.getContext('2d');
  ctx.clearRect(0,0,W,H);
  const cls = getClass(state.level);
  const bob = Math.sin(t*2)*(mini?1.5:4);
  const breathe = 1 + Math.sin(t*1.5)*0.015;
  const cx = W/2, cy = H/2 + bob;
  const s = mini ? 0.18 : (W/100)*0.44;

  ctx.save();
  ctx.translate(cx, cy);
  ctx.scale(breathe, breathe);

  if (mini) {
    // Simple glowing circle with icon
    ctx.shadowColor = cls.color;
    ctx.shadowBlur = 10;
    ctx.beginPath();
    ctx.arc(0,0,16,0,Math.PI*2);
    ctx.fillStyle = cls.color+'55';
    ctx.fill();
    ctx.strokeStyle = cls.color;
    ctx.lineWidth = 1.5;
    ctx.stroke();
    ctx.shadowBlur = 0;
    ctx.font = `${mini?16:20}px sans-serif`;
    ctx.textAlign = 'center'; ctx.textBaseline = 'middle';
    ctx.fillText(cls.icon, 0, 1);
    ctx.restore();
    return;
  }

  const sc = s * 100;

  /* ── AURA GLOW ── */
  ctx.shadowColor = cls.color;
  ctx.shadowBlur = 20 + Math.sin(t*3)*6;

  /* ── LEGS ── */
  const legSway = Math.sin(t*2)*sc*0.04;
  ctx.fillStyle = adjustColor(cls.color,-0.6);
  // left leg
  ctx.save(); ctx.translate(-sc*.18, sc*.6); ctx.rotate(legSway*.01);
  rRect(ctx,-sc*.13,0,sc*.24,sc*.5,sc*.06); ctx.fill(); ctx.restore();
  // right leg
  ctx.save(); ctx.translate(sc*.18, sc*.6); ctx.rotate(-legSway*.01);
  rRect(ctx,-sc*.11,0,sc*.24,sc*.5,sc*.06); ctx.fill(); ctx.restore();

  /* ── BOOTS ── */
  ctx.fillStyle = '#1a1a2e';
  ctx.save(); ctx.translate(-sc*.18, sc*1.08); rRect(ctx,-sc*.15,.0,sc*.28,sc*.12,sc*.04); ctx.fill(); ctx.restore();
  ctx.save(); ctx.translate(sc*.18, sc*1.08); rRect(ctx,-sc*.13,0,sc*.28,sc*.12,sc*.04); ctx.fill(); ctx.restore();

  /* ── TORSO ── */
  ctx.shadowBlur = 12;
  ctx.fillStyle = adjustColor(cls.color,-0.35);
  rRect(ctx,-sc*.35,-sc*.22,sc*.7,sc*.82,sc*.12); ctx.fill();

  /* ── CHEST ARMOR ── */
  const grad = ctx.createLinearGradient(-sc*.25,-sc*.2,sc*.25,sc*.45);
  grad.addColorStop(0, cls.color+'ee'); grad.addColorStop(1, cls.color+'55');
  ctx.fillStyle = grad;
  rRect(ctx,-sc*.26,-sc*.17,sc*.52,sc*.48,sc*.08); ctx.fill();

  /* ── ARMOR LINES ── */
  ctx.strokeStyle = 'rgba(255,255,255,0.25)'; ctx.lineWidth = 1.5;
  ctx.beginPath(); ctx.moveTo(-sc*.15,-sc*.05); ctx.lineTo(-sc*.15,sc*.25); ctx.stroke();
  ctx.beginPath(); ctx.moveTo(sc*.15,-sc*.05); ctx.lineTo(sc*.15,sc*.25); ctx.stroke();
  ctx.beginPath(); ctx.moveTo(-sc*.2,sc*.1); ctx.lineTo(sc*.2,sc*.1); ctx.stroke();

  /* ── CLASS ICON ── */
  ctx.shadowBlur = 0;
  ctx.font = `bold ${sc*.38}px sans-serif`;
  ctx.textAlign='center'; ctx.textBaseline='middle';
  ctx.fillText(cls.icon, 0, sc*.06);

  /* ── BELT ── */
  ctx.fillStyle = '#0a0a1a';
  rRect(ctx,-sc*.36,sc*.26,sc*.72,sc*.1,sc*.04); ctx.fill();
  ctx.fillStyle = cls.color;
  ctx.beginPath(); ctx.arc(0,sc*.31,sc*.06,0,Math.PI*2); ctx.fill();

  /* ── ARMS ── */
  const armSway = Math.sin(t*2)*0.12;
  ctx.fillStyle = adjustColor(cls.color,-0.3);
  // Left arm
  ctx.save(); ctx.translate(-sc*.42,-sc*.1); ctx.rotate(-0.15 + armSway);
  rRect(ctx,-sc*.1,0,sc*.19,sc*.52,sc*.08); ctx.fill(); ctx.restore();
  // Right arm
  ctx.save(); ctx.translate(sc*.42,-sc*.1); ctx.rotate(0.15 - armSway);
  rRect(ctx,-sc*.09,0,sc*.19,sc*.52,sc*.08); ctx.fill(); ctx.restore();

  // Gauntlets
  ctx.fillStyle = adjustColor(cls.color,0.1);
  ctx.save(); ctx.translate(-sc*.42,sc*.36); rRect(ctx,-sc*.12,0,sc*.22,sc*.18,sc*.06); ctx.fill(); ctx.restore();
  ctx.save(); ctx.translate(sc*.42,sc*.36); rRect(ctx,-sc*.11,0,sc*.22,sc*.18,sc*.06); ctx.fill(); ctx.restore();

  /* ── HEAD ── */
  const headY = -sc*.72;
  ctx.shadowBlur = 8;
  // Neck
  ctx.fillStyle = '#f5d5b5';
  rRect(ctx,-sc*.1,headY+sc*.52,sc*.2,sc*.12,sc*.04); ctx.fill();
  // Head
  ctx.fillStyle = '#f5d5b5';
  ctx.beginPath(); ctx.ellipse(0,headY,sc*.26,sc*.28,0,0,Math.PI*2); ctx.fill();
  // Helmet
  ctx.fillStyle = cls.color;
  ctx.beginPath();
  ctx.ellipse(0,headY-sc*.05,sc*.3,sc*.2,0,Math.PI,0);
  ctx.fill();
  // Helmet visor
  ctx.fillStyle = adjustColor(cls.color,-0.2);
  rRect(ctx,-sc*.22,headY-sc*.12,sc*.44,sc*.08,sc*.03); ctx.fill();
  // Helmet crest
  ctx.fillStyle = cls.color+'cc';
  ctx.beginPath(); ctx.moveTo(-sc*.08,headY-sc*.22); ctx.lineTo(0,headY-sc*.38); ctx.lineTo(sc*.08,headY-sc*.22); ctx.fill();

  /* ── FACE ── */
  ctx.shadowBlur = 0;
  // Blink logic
  const blink = Math.sin(t*0.3) > 0.94;
  const ey = headY - sc*.02;
  const eyH = blink ? sc*.015 : sc*.08;
  ctx.fillStyle = '#1a1a3e';
  ctx.beginPath(); ctx.ellipse(-sc*.1,ey,sc*.07,eyH,0,0,Math.PI*2); ctx.fill();
  ctx.beginPath(); ctx.ellipse(sc*.1,ey,sc*.07,eyH,0,0,Math.PI*2); ctx.fill();
  if (!blink) {
    // eye iris
    ctx.fillStyle = cls.color+'cc';
    ctx.beginPath(); ctx.ellipse(-sc*.1,ey,sc*.04,sc*.05,0,0,Math.PI*2); ctx.fill();
    ctx.beginPath(); ctx.ellipse(sc*.1,ey,sc*.04,sc*.05,0,0,Math.PI*2); ctx.fill();
    // pupil
    ctx.fillStyle = '#000';
    ctx.beginPath(); ctx.arc(-sc*.1,ey,sc*.02,0,Math.PI*2); ctx.fill();
    ctx.beginPath(); ctx.arc(sc*.1,ey,sc*.02,0,Math.PI*2); ctx.fill();
    // shine
    ctx.fillStyle = '#fff';
    ctx.beginPath(); ctx.arc(-sc*.08,ey-sc*.02,sc*.015,0,Math.PI*2); ctx.fill();
    ctx.beginPath(); ctx.arc(sc*.12,ey-sc*.02,sc*.015,0,Math.PI*2); ctx.fill();
  }
  // Smile
  ctx.strokeStyle = '#c07050'; ctx.lineWidth = sc*.022; ctx.lineCap='round';
  ctx.beginPath(); ctx.arc(0,headY+sc*.1,sc*.09,0.2,Math.PI-0.2); ctx.stroke();

  /* ── HIGH-LEVEL ORBITING PARTICLES ── */
  if (state.level >= 10) {
    const pCount = Math.min(8, Math.floor(state.level/5));
    for (let i=0;i<pCount;i++) {
      const angle = t*1.5 + (Math.PI*2/pCount)*i;
      const rx = sc*1.1, ry = sc*.55;
      const px = Math.cos(angle)*rx, py = Math.sin(angle)*ry - sc*.1;
      const ps = sc*.07 + Math.sin(t*4+i)*sc*.02;
      ctx.shadowColor = cls.color; ctx.shadowBlur = 8;
      ctx.beginPath(); ctx.arc(px,py,ps,0,Math.PI*2);
      ctx.fillStyle = cls.color+'cc'; ctx.fill();
    }
    ctx.shadowBlur = 0;
  }

  /* ── WEAPON GLOW (level 20+) ── */
  if (state.level >= 20) {
    ctx.save();
    ctx.translate(sc*.55, sc*.05);
    ctx.rotate(-0.3 + Math.sin(t*2)*0.1);
    ctx.shadowColor = cls.color; ctx.shadowBlur = 15;
    ctx.fillStyle = cls.color+'bb';
    rRect(ctx,-sc*.05,-sc*.6,sc*.1,sc*.7,sc*.03); ctx.fill();
    ctx.fillStyle = cls.color;
    rRect(ctx,-sc*.08,-sc*.62,sc*.16,sc*.08,sc*.03); ctx.fill(); // crossguard
    ctx.restore();
  }

  ctx.shadowBlur = 0;
  ctx.restore();
}

/* helpers */
function rRect(ctx,x,y,w,h,r) {
  ctx.beginPath();
  if (ctx.roundRect) { ctx.roundRect(x,y,w,h,r); return; }
  ctx.moveTo(x+r,y); ctx.lineTo(x+w-r,y); ctx.quadraticCurveTo(x+w,y,x+w,y+r);
  ctx.lineTo(x+w,y+h-r); ctx.quadraticCurveTo(x+w,y+h,x+w-r,y+h);
  ctx.lineTo(x+r,y+h); ctx.quadraticCurveTo(x,y+h,x,y+h-r);
  ctx.lineTo(x,y+r); ctx.quadraticCurveTo(x,y,x+r,y);
  ctx.closePath();
}
function adjustColor(hex,amount) {
  const num = parseInt(hex.replace('#',''),16);
  const r = clamp(Math.round(((num>>16)&0xff)*(1+amount)),0,255);
  const g = clamp(Math.round(((num>>8)&0xff)*(1+amount)),0,255);
  const b = clamp(Math.round((num&0xff)*(1+amount)),0,255);
  return `rgb(${r},${g},${b})`;
}

/* ──────────────────────────────────────
   AUTH
────────────────────────────────────── */
function doLogin() {
  const u = document.getElementById('login-user').value.trim();
  const p = document.getElementById('login-pass').value;
  const err = document.getElementById('login-error');
  if (u===CREDS.user && p===CREDS.pass) {
    err.classList.add('hidden');
    localStorage.setItem('vq2_loggedin','1');
    showGame();
  } else {
    err.classList.remove('hidden');
    document.getElementById('login-pass').value='';
    document.getElementById('login-pass').focus();
    // shake
    document.getElementById('login-error').parentElement.classList.add('shake');
    setTimeout(()=>document.getElementById('login-error').parentElement.classList.remove('shake'),600);
  }
}
function doLogout() {
  localStorage.removeItem('vq2_loggedin');
  document.getElementById('game-screen').classList.add('hidden');
  document.getElementById('login-screen').classList.remove('hidden');
  stopAvatarLoop();
}

document.addEventListener('DOMContentLoaded', () => {
  initParticles();
  // Login avatar
  registerAvatar('login-avatar-canvas',100,120,false);
  startAvatarLoop();
  // Enter key
  ['login-pass','login-user'].forEach(id=>{
    document.getElementById(id).addEventListener('keydown',e=>{if(e.key==='Enter')doLogin();});
  });
  // Check existing session
  if (localStorage.getItem('vq2_loggedin')==='1') showGame();
  // Daily reset check
  checkDailyReset();
});

/* ──────────────────────────────────────
   SHOW GAME
────────────────────────────────────── */
function showGame() {
  document.getElementById('login-screen').classList.add('hidden');
  document.getElementById('game-screen').classList.remove('hidden');

  if (!load()) { state=defaultState(); save(); }

  document.documentElement.setAttribute('data-theme', state.settings.theme||'dark');
  syncThemeCheckbox();
  checkStreak();
  applyPenalty();

  // Register avatars
  registerAvatar('hud-avatar-canvas',36,44,true);
  registerAvatar('dash-ava',110,140,false);
  startAvatarLoop();

  renderAll();
  updateGreeting();
}

/* ──────────────────────────────────────
   STREAK & PENALTY
────────────────────────────────────── */
function checkStreak() {
  const td=today(), last=state.lastDate;
  if (!last) { state.lastDate=td; save(); return; }
  const diff = daysBetween(last,td);
  if (diff>1) { state.streak=0; }
  state.lastDate=td; save();
}
function applyPenalty() {
  const last=state.lastDate;
  if (!last) return;
  const diff=daysBetween(last,today());
  if (diff>1) { state.xp=Math.max(0,state.xp-Math.min(diff*10,100)); save(); }
}
function daysBetween(d1,d2) {
  return Math.floor((new Date(d2)-new Date(d1))/86400000);
}
function bumpStreak() {
  if (state.lastDate===today()) return;
  state.streak++;
  state.lastDate=today();
  save(); updateHUD();
}

/* ──────────────────────────────────────
   XP & LEVELS
────────────────────────────────────── */
function addXP(amount, x, y) {
  const oldLv = state.level;
  state.xp += amount;
  // XP history
  const td=today();
  const last=state.xpHistory[state.xpHistory.length-1];
  if (last&&last.date===td) last.xp=state.xp;
  else state.xpHistory.push({date:td,xp:state.xp});
  if (state.xpHistory.length>30) state.xpHistory.shift();
  recalcLevel();
  save();
  updateHUD();
  // Floating damage number
  showDmgNum(amount, x, y);
  // Burst
  if (x&&y) burstParticles(x,y,15);
  // Level up
  if (state.level>oldLv) setTimeout(()=>showLevelUp(state.level),500);
  checkBadges();
}
function recalcLevel() {
  let lv=1;
  for (let i=1;i<LEVEL_XP.length;i++) { if(state.xp>=LEVEL_XP[i]) lv=i+1; else break; }
  state.level=lv;
}
function xpProgress() {
  const cur=LEVEL_XP[Math.min(state.level-1,LEVEL_XP.length-1)]||0;
  const nxt=LEVEL_XP[Math.min(state.level,LEVEL_XP.length-1)]||LEVEL_XP[LEVEL_XP.length-1];
  const pct=clamp((state.xp-cur)/(nxt-cur)*100,0,100);
  return {current:state.xp-cur,needed:nxt-cur,pct};
}
function getClass(lv) { return CLASSES.find(c=>lv>=c.min&&lv<=c.max)||CLASSES[0]; }

/* ──────────────────────────────────────
   FLOATING DAMAGE NUMBER
────────────────────────────────────── */
function showDmgNum(amount, x, y) {
  const layer = document.getElementById('dmg-layer');
  const el = document.createElement('div');
  el.className = 'dmg-num';
  el.textContent = '+'+amount+' XP';
  // Position near button or default to right side
  const px = x ? x : (window.innerWidth - 160);
  const py = y ? y : (window.innerHeight / 2);
  el.style.left = (px - 40) + 'px';
  el.style.top = (py - 20) + 'px';
  layer.appendChild(el);
  setTimeout(()=>el.remove(), 1700);
}

/* ──────────────────────────────────────
   LEVEL UP
────────────────────────────────────── */
function showLevelUp(lv) {
  const cls = getClass(lv);
  document.getElementById('lu-lvnum').textContent = lv;
  document.getElementById('lu-classname').textContent = cls.name;
  document.getElementById('lu-perks').innerHTML = cls.perks.map(p=>`<div class="lu-perk">✓ ${p}</div>`).join('');

  // Draw avatar in level up screen
  registerAvatar('lu-ava',140,180,false);
  const ovl = document.getElementById('levelup-overlay');
  ovl.classList.remove('hidden');

  // Screen shake
  document.getElementById('game-world').classList.add('shake');
  setTimeout(()=>document.getElementById('game-world').classList.remove('shake'),600);

  // Confetti
  spawnConfetti(cls.color);

  // Add to history
  state.history.push({date:today(), class:cls.name, level:lv});
  save();
}
function closeLevelUp() {
  document.getElementById('levelup-overlay').classList.add('hidden');
  unregisterAvatar('lu-ava');
  renderAll();
}
function spawnConfetti(primaryColor) {
  const container = document.getElementById('lu-confetti');
  container.innerHTML='';
  const colors = [primaryColor,'#ffd60a','#00ffff','#bf5af2','#ff006e','#39ff14'];
  for (let i=0;i<60;i++) {
    const el=document.createElement('div');
    el.className='confetti-piece';
    el.style.cssText=`
      left:${Math.random()*100}%;
      background:${colors[Math.floor(Math.random()*colors.length)]};
      width:${4+Math.random()*8}px;
      height:${4+Math.random()*8}px;
      --drift:${(Math.random()-0.5)*200}px;
      animation-duration:${1.5+Math.random()*2}s;
      animation-delay:${Math.random()*0.5}s;
      border-radius:${Math.random()>0.5?'50%':'2px'};
    `;
    container.appendChild(el);
  }
}

/* ──────────────────────────────────────
   BADGES
────────────────────────────────────── */
function checkBadges() {
  let changed=false;
  BADGES.forEach(b=>{ if(!state.badges.includes(b.id)&&b.chk(state)){ state.badges.push(b.id); changed=true; } });
  if(changed){ save(); renderBadgesAll(); }
}
function renderBadgesAll() { renderBadgeContainer('dash-badges'); renderBadgeContainer('ava-badges'); }
function renderBadgeContainer(id) {
  const el=document.getElementById(id); if(!el) return;
  el.innerHTML=BADGES.map(b=>{
    const earned=state.badges.includes(b.id);
    return `<div class="badge-chip ${earned?'':'locked'}" title="${b.name}"><div class="badge-ico">${b.ico}</div><div class="badge-name">${b.name}</div></div>`;
  }).join('');
}

/* ──────────────────────────────────────
   NAVIGATION
────────────────────────────────────── */
function navigate(page) {
  // Pages
  document.querySelectorAll('.gpage').forEach(p=>{ p.classList.remove('active'); p.classList.add('hidden'); });
  const pg = document.getElementById('page-'+page);
  if (!pg) return;
  pg.classList.remove('hidden');
  // force reflow for animation
  void pg.offsetWidth;
  pg.classList.add('active');

  // Hotbar
  document.querySelectorAll('.hslot').forEach(b=>b.classList.remove('active'));
  const nb = document.getElementById('nav-'+page);
  if (nb) nb.classList.add('active');

  // Unregister page-specific avatars
  unregisterAvatar('main-ava');
  unregisterAvatar('dash-ava');

  // Page renders
  if (page==='dashboard')   { registerAvatar('dash-ava',110,140,false); renderDashboard(); }
  if (page==='avatar')      { registerAvatar('main-ava',190,240,false); renderAvatarPage(); }
  if (page==='tasks')       renderTasks();
  if (page==='health')      renderHealth();
  if (page==='analytics')   setTimeout(renderAnalytics,50);
  if (page==='leaderboard') renderLeaderboard();
  if (page==='settings')    renderSettings();
}

/* ──────────────────────────────────────
   RENDER ALL
────────────────────────────────────── */
function renderAll() {
  updateHUD();
  renderDashboard();
}

/* ──────────────────────────────────────
   HUD
────────────────────────────────────── */
function updateHUD() {
  document.getElementById('hud-level').textContent = state.level;
  document.getElementById('hud-class').textContent = getClass(state.level).name;
  document.getElementById('hud-streak').textContent = state.streak;
  document.getElementById('hud-tasks').textContent = state.totalDone;
  // HP = clamp(100 - missed penalty, 1, 100)
  const hp = clamp(100 - Math.max(0,(state.streak>0?0:(100-state.xp/10))),10,100);
  document.getElementById('hud-hp').style.width = hp+'%';
  document.getElementById('hud-hp-v').textContent = Math.round(hp);
  const prog = xpProgress();
  document.getElementById('hud-xp').style.width = prog.pct+'%';
  document.getElementById('hud-xp-v').textContent = state.xp;
}

/* ──────────────────────────────────────
   DASHBOARD
────────────────────────────────────── */
function renderDashboard() {
  const cls = getClass(state.level);
  const prog = xpProgress();

  // Stat orbs
  document.getElementById('orb-xp').textContent = state.xp;
  document.getElementById('orb-lv').textContent = state.level;
  document.getElementById('orb-streak').textContent = state.streak;
  document.getElementById('orb-done').textContent = state.totalDone;

  // Avatar card
  document.getElementById('dash-class').textContent = cls.name;
  document.getElementById('dash-lv').textContent = state.level;
  document.getElementById('dash-xp-bar').style.width = prog.pct+'%';
  document.getElementById('dash-xp-text').textContent = `${prog.current}/${prog.needed}`;

  // Aura color
  const glow = document.getElementById('dash-glow');
  if (glow) glow.style.background = `radial-gradient(circle, ${cls.aura} 0%, transparent 70%)`;

  // Quests
  renderDashQuests();
  // AI
  renderAI();
  // Vitals
  renderVitals();
  // Badges
  renderBadgesAll();
}

function renderDashQuests() {
  const list = state.tasks.filter(t=>t.type==='daily'||t.type==='weekly');
  const done = list.filter(t=>t.done).length;
  document.getElementById('qcount').textContent = `${done}/${list.length}`;
  const el = document.getElementById('dash-quest-list');
  if (!list.length) { el.innerHTML='<div style="color:var(--text2);font-size:.85rem;padding:8px">No quests yet — add some!</div>'; return; }
  el.innerHTML = list.slice(0,6).map(t=>`
    <div class="dash-qi ${t.done?'done':''}">
      <input type="checkbox" ${t.done?'checked':''} onchange="dashCheck('${t.id}',this.checked,event)"/>
      <div class="dash-qi-name">${esc(t.name)}</div>
      <div class="dash-qi-xp">${t.xp}⚡</div>
    </div>
  `).join('');
}

function dashCheck(id, checked, e) {
  const t = state.tasks.find(t=>t.id===id); if(!t) return;
  const rect = e.target.getBoundingClientRect();
  if (checked && !t.done) {
    t.done=true; state.totalDone++;
    addXP(t.xp, rect.left, rect.top);
    bumpStreak();
  } else if (!checked && t.done) {
    t.done=false; state.totalDone=Math.max(0,state.totalDone-1);
    state.xp=Math.max(0,state.xp-t.xp); recalcLevel(); updateHUD();
  }
  save(); renderDashQuests();
}

/* AI ADVISOR */
function renderAI() {
  const tips = getAITips();
  document.getElementById('ai-tips').innerHTML = tips.map(t=>`
    <div class="ai-tip"><span class="tip-ico">${t.ico}</span><span>${t.msg}</span></div>
  `).join('');
}
function getAITips() {
  const tips=[], g=state.goals, d=state.healthData[state.healthData.length-1];
  if (!d) { return [{ico:'📝',msg:'Log your health data to receive personalized tips!'}]; }
  if (d.water<g.water)    tips.push({ico:'💧',msg:`Drink more water! You had ${d.water}/${g.water} glasses today.`});
  if (d.steps<g.steps)    tips.push({ico:'👟',msg:`Only ${d.steps.toLocaleString()} steps. Hit ${g.steps.toLocaleString()} for full XP!`});
  if (d.sleep<g.sleep)    tips.push({ico:'😴',msg:`${d.sleep}h sleep. Aim for ${g.sleep}h to recharge HP fully.`});
  if (d.mood<=4)          tips.push({ico:'😔',msg:'Low mood detected. Take a walk or meditate for a mood buff!'});
  if (d.calories<200)     tips.push({ico:'🔥',msg:'Low calorie burn. Even a 15-min workout counts!'});
  if (state.streak===0)   tips.push({ico:'🔥',msg:'Start a streak! Complete at least one quest today.'});
  if (state.streak>=7)    tips.push({ico:'🏆',msg:`${state.streak}-day streak! You are unstoppable!`});
  if (d.water>=g.water)   tips.push({ico:'✅',msg:'Hydration goal achieved! Your body is thriving.'});
  if (d.steps>=g.steps)   tips.push({ico:'🎯',msg:`Steps goal crushed — ${d.steps.toLocaleString()} steps!`});
  if (!tips.length) tips.push({ico:'⚡',msg:'You are performing excellently! Keep up the heroic effort!'});
  return tips.slice(0,4);
}

/* VITALS */
function renderVitals() {
  const d=state.healthData[state.healthData.length-1], g=state.goals;
  const metrics=[
    {ico:'👟',lbl:'Steps',    val:d?.steps||0,    goal:g.steps,    unit:'',    color:'#00ffff'},
    {ico:'🔥',lbl:'Calories', val:d?.calories||0, goal:g.calories, unit:'kcal',color:'#ff6b00'},
    {ico:'😴',lbl:'Sleep',    val:d?.sleep||0,     goal:g.sleep,    unit:'h',   color:'#bf5af2'},
    {ico:'💧',lbl:'Water',    val:d?.water||0,     goal:g.water,    unit:'gl',  color:'#00bcd4'},
    {ico:'⚖',lbl:'Weight',   val:d?.weight||'--', goal:null,       unit:'kg',  color:'#39ff14'},
    {ico:'😊',lbl:'Mood',     val:d?.mood||0,      goal:10,         unit:'/10', color:'#ffd60a'},
  ];
  document.getElementById('vitals-grid').innerHTML = metrics.map(m=>{
    const pct = m.goal ? clamp((m.val/m.goal)*100,0,100) : 0;
    const disp = typeof m.val==='number' ? (m.lbl==='Steps'?m.val.toLocaleString():m.val) : m.val;
    return `
      <div class="vital-item">
        <span class="vital-ico">${m.ico}</span>
        <div class="vital-val">${disp}${typeof m.val==='number'&&m.val?m.unit:''}</div>
        <div class="vital-lbl">${m.lbl}</div>
        ${m.goal?`<div class="vital-bar"><div class="vital-bar-fill" style="width:${pct}%;background:${m.color}"></div></div>`:''}
      </div>
    `;
  }).join('');
}

function updateGreeting() {
  const h=new Date().getHours();
  const g = h<12?'☀ GOOD MORNING':h<17?'🌤 GOOD AFTERNOON':'🌙 GOOD EVENING';
  document.getElementById('hero-greet').textContent = g+', HERO!';
  document.getElementById('hero-sub').textContent = 'Your adventure continues. Complete quests to grow stronger.';
  // Rune decorations
  const runes=['⚡','🔮','⚔','🌟','🛡'];
  const el=document.getElementById('banner-runes');
  if(el) el.innerHTML=runes.map(r=>`<span class="rune-char">${r}</span>`).join('');
}

/* ──────────────────────────────────────
   AVATAR PAGE
────────────────────────────────────── */
function renderAvatarPage() {
  const cls=getClass(state.level), prog=xpProgress();
  document.getElementById('ava-big-class').textContent = cls.name;
  document.getElementById('ava-big-lv').textContent = state.level;
  document.getElementById('ava-xp-fill').style.width = prog.pct+'%';
  document.getElementById('ava-xp-nums').textContent = `${prog.current} / ${prog.needed} XP`;

  // Perks
  document.getElementById('ava-perks').innerHTML = cls.perks.map(p=>`<div class="perk-row">✓ ${p}</div>`).join('');

  // Evo chain
  document.getElementById('evo-chain').innerHTML = CLASSES.map(c=>{
    let clas='evo-node';
    if (state.level>=c.min&&state.level<=c.max) clas+=' active';
    else if (state.level>c.max) clas+=' past';
    return `<div class="${clas}"><div class="evo-icon">${c.icon}</div><div class="evo-name pixel-font">${c.name}</div></div>`;
  }).join('');

  // History
  const hEl=document.getElementById('ava-history');
  if (!state.history.length) {
    hEl.innerHTML='<div style="color:var(--text2);font-size:.85rem">No level-ups recorded yet.</div>';
  } else {
    hEl.innerHTML=[...state.history].reverse().slice(0,6).map(h=>`
      <div class="hist-row">
        <span>${getClass(h.level).icon}</span>
        <span>Reached <strong>${h.class}</strong> (Level ${h.level})</span>
        <span class="hist-time">${h.date}</span>
      </div>
    `).join('');
  }
  renderBadgeContainer('ava-badges');
}

/* ──────────────────────────────────────
   TASKS
────────────────────────────────────── */
function addTask() {
  const name=document.getElementById('task-name-input').value.trim();
  if (!name) { alert('Quest name required!'); return; }
  const type=document.getElementById('task-type-select').value;
  const xp=parseInt(document.getElementById('task-xp-select').value);
  state.tasks.push({id:uid(),name,type,xp,done:false,ts:Date.now()});
  save();
  document.getElementById('task-name-input').value='';
  renderTasks();
  renderDashQuests();
}
function filterTasks(f,btn) {
  taskFilter=f;
  document.querySelectorAll('.qtab').forEach(b=>b.classList.remove('active'));
  if(btn) btn.classList.add('active');
  renderTasks();
}
function renderTasks() {
  let list=[...state.tasks];
  if(taskFilter==='daily')  list=list.filter(t=>t.type==='daily');
  if(taskFilter==='weekly') list=list.filter(t=>t.type==='weekly');
  if(taskFilter==='custom') list=list.filter(t=>t.type==='custom');
  if(taskFilter==='done')   list=list.filter(t=>t.done);
  const el=document.getElementById('tasks-container');
  if (!list.length) { el.innerHTML='<div style="text-align:center;padding:40px;color:var(--text2)">No quests found. Post a new one above!</div>'; return; }
  el.innerHTML=list.map(t=>`
    <div class="quest-card ${t.type} ${t.done?'done':''}">
      <input class="quest-cb" type="checkbox" ${t.done?'checked':''} onchange="toggleTask('${t.id}',this.checked,event)"/>
      <div class="quest-info">
        <div class="quest-name">${esc(t.name)}</div>
        <div class="quest-meta">
          <span class="quest-type-tag ${t.type}">${t.type.toUpperCase()}</span>
          <span class="quest-xp-tag">+${t.xp} XP ⚡</span>
        </div>
      </div>
      <div class="quest-actions">
        ${!t.done?`<button class="q-act-btn" onclick="openEdit('${t.id}')">✏️</button>`:''}
        <button class="q-act-btn" onclick="deleteTask('${t.id}')">🗑️</button>
      </div>
    </div>
  `).join('');
}
function toggleTask(id, checked, e) {
  const t=state.tasks.find(t=>t.id===id); if(!t) return;
  const rect=e.target.getBoundingClientRect();
  if (checked&&!t.done) {
    t.done=true; state.totalDone++;
    addXP(t.xp,rect.left,rect.top);
    bumpStreak();
  } else if(!checked&&t.done) {
    t.done=false; state.totalDone=Math.max(0,state.totalDone-1);
    state.xp=Math.max(0,state.xp-t.xp); recalcLevel(); updateHUD();
  }
  save(); renderTasks(); renderDashQuests();
}
function deleteTask(id) { state.tasks=state.tasks.filter(t=>t.id!==id); save(); renderTasks(); renderDashQuests(); }
function openEdit(id) {
  editingId=id;
  const t=state.tasks.find(t=>t.id===id); if(!t) return;
  document.getElementById('edit-name').value=t.name;
  document.getElementById('edit-type').value=t.type;
  document.getElementById('edit-xp').value=t.xp;
  document.getElementById('edit-modal').classList.remove('hidden');
}
function closeEditModal() { editingId=null; document.getElementById('edit-modal').classList.add('hidden'); }
function saveEditTask() {
  const t=state.tasks.find(t=>t.id===editingId); if(!t) return;
  t.name=document.getElementById('edit-name').value.trim()||t.name;
  t.type=document.getElementById('edit-type').value;
  t.xp=parseInt(document.getElementById('edit-xp').value);
  save(); closeEditModal(); renderTasks(); renderDashQuests();
}
function modalBgClick(e,id) { if(e.target===document.getElementById(id)) document.getElementById(id).classList.add('hidden'); }

/* ──────────────────────────────────────
   HEALTH
────────────────────────────────────── */
function logHealth() {
  const steps=parseInt(document.getElementById('h-steps').value)||0;
  const cal  =parseInt(document.getElementById('h-calories').value)||0;
  const sleep=parseFloat(document.getElementById('h-sleep').value)||0;
  const water=parseInt(document.getElementById('h-water').value)||0;
  const wt   =parseFloat(document.getElementById('h-weight').value)||0;
  const mood =parseInt(document.getElementById('h-mood').value)||5;
  const entry={date:today(),steps,calories:cal,sleep,water,weight:wt,mood};
  const idx=state.healthData.findIndex(d=>d.date===today());
  if(idx>=0) state.healthData[idx]=entry; else state.healthData.push(entry);
  if(state.healthData.length>30) state.healthData.shift();
  state.maxWater=Math.max(state.maxWater||0,water);
  state.maxSteps=Math.max(state.maxSteps||0,steps);
  state.maxSleep=Math.max(state.maxSleep||0,sleep);
  state.maxMood =Math.max(state.maxMood||0,mood);
  state.healthLogs++;
  const g=state.goals;
  let xp=5;
  if(steps>=g.steps) xp+=20;
  if(water>=g.water) xp+=10;
  if(sleep>=g.sleep) xp+=15;
  if(cal>=g.calories) xp+=10;
  if(mood>=8) xp+=5;
  const btn=document.querySelector('.health-form-panel .rpg-btn');
  const rect=btn?btn.getBoundingClientRect():{left:200,top:400};
  addXP(xp,rect.left,rect.top);
  bumpStreak(); checkBadges(); save();
  ['h-steps','h-calories','h-sleep','h-water','h-weight'].forEach(id=>document.getElementById(id).value='');
  document.getElementById('h-mood').value=5;
  document.getElementById('mood-v').textContent='5';
  renderHealth(); renderVitals(); renderAI();
}
function renderHealth() { renderGoals(); renderHealthHistory(); }
function renderGoals() {
  const d=state.healthData[state.healthData.length-1], g=state.goals;
  const rows=[
    {ico:'👟',lbl:'Steps',    val:d?.steps||0,    goal:g.steps,    color:'#00ffff'},
    {ico:'💧',lbl:'Water',    val:d?.water||0,     goal:g.water,    color:'#00bcd4'},
    {ico:'😴',lbl:'Sleep',    val:d?.sleep||0,     goal:g.sleep,    color:'#bf5af2'},
    {ico:'🔥',lbl:'Calories', val:d?.calories||0,  goal:g.calories, color:'#ff6b00'},
  ];
  document.getElementById('goals-status').innerHTML=rows.map(r=>{
    const pct=clamp((r.val/r.goal)*100,0,100), done=pct>=100;
    return `
      <div class="goal-row">
        <span class="goal-ico">${r.ico}</span>
        <span class="goal-lbl">${r.lbl}</span>
        <div class="goal-track"><div class="goal-fill" style="width:${pct}%;background:${done?'#39ff14':r.color};box-shadow:${done?'0 0 8px #39ff14':'none'}"></div></div>
        <span class="goal-pct" style="color:${done?'#39ff14':'var(--text2)'}">${done?'✓':Math.round(pct)+'%'}</span>
      </div>
    `;
  }).join('');
}
function renderHealthHistory() {
  const el=document.getElementById('health-history');
  const data=[...state.healthData].reverse();
  if(!data.length){el.innerHTML='<div style="color:var(--text2);text-align:center;padding:20px">No entries yet. Log your first vitals!</div>';return;}
  el.innerHTML=data.map(d=>`
    <div class="hlog-entry">
      <div class="hlog-date">📅 ${d.date}</div>
      <div class="hlog-data">
        <div class="hlog-metric"><span>Steps: </span>${d.steps.toLocaleString()}</div>
        <div class="hlog-metric"><span>Sleep: </span>${d.sleep}h</div>
        <div class="hlog-metric"><span>Water: </span>${d.water}gl</div>
        <div class="hlog-metric"><span>Cal: </span>${d.calories}kcal</div>
        <div class="hlog-metric"><span>Wt: </span>${d.weight||'--'}kg</div>
        <div class="hlog-metric"><span>Mood: </span>${d.mood}/10</div>
      </div>
    </div>
  `).join('');
}

/* ──────────────────────────────────────
   ANALYTICS — Custom Canvas Charts
────────────────────────────────────── */
function renderAnalytics() {
  const d=state.healthData.slice(-7);
  const lbl=d.map(x=>new Date(x.date).toLocaleDateString('en',{weekday:'short'}));
  const xlbl=state.xpHistory.slice(-7).map(x=>new Date(x.date).toLocaleDateString('en',{weekday:'short'}));
  drawBar('chart-xp',    state.xpHistory.slice(-7).map(x=>x.xp), xlbl, '#00ffff');
  drawBar('chart-steps', d.map(x=>x.steps),    lbl, '#00ffff');
  drawBar('chart-water', d.map(x=>x.water),    lbl, '#00bcd4');
  drawLine('chart-sleep',d.map(x=>x.sleep),    lbl, '#bf5af2');
  drawLine('chart-mood', d.map(x=>x.mood),     lbl, '#ffd60a');
  drawBar('chart-calories',d.map(x=>x.calories),lbl,'#ff6b00');
  drawTaskBar('chart-tasks');
}

function chartColors() {
  const dark=document.documentElement.getAttribute('data-theme')==='dark';
  return { grid:dark?'rgba(255,255,255,0.06)':'rgba(0,0,0,0.07)', text:dark?'#4a5a80':'#5060a0', bg:dark?'#0b1225':'#f0f4ff' };
}
function drawBar(id,vals,lbls,color) {
  const c=document.getElementById(id); if(!c) return;
  const W=c.offsetWidth||400, H=c.height; c.width=W;
  const ctx=c.getContext('2d'); ctx.clearRect(0,0,W,H);
  const tc=chartColors();
  if(!vals||!vals.length){ctx.fillStyle=tc.text;ctx.font='12px Exo 2';ctx.textAlign='center';ctx.fillText('No data yet',W/2,H/2);return;}
  const pad={t:24,r:16,b:36,l:48};
  const cW=W-pad.l-pad.r, cH=H-pad.t-pad.b;
  const max=Math.max(...vals,1);
  const bW=cW/vals.length*0.55, gap=cW/vals.length;
  for(let i=0;i<=4;i++){
    const y=pad.t+cH-(cH/4)*i;
    ctx.strokeStyle=tc.grid; ctx.lineWidth=1;
    ctx.beginPath(); ctx.moveTo(pad.l,y); ctx.lineTo(pad.l+cW,y); ctx.stroke();
    ctx.fillStyle=tc.text; ctx.font='9px Share Tech Mono'; ctx.textAlign='right';
    const v=Math.round((max/4)*i); ctx.fillText(v>999?(v/1000).toFixed(1)+'k':v,pad.l-4,y+3);
  }
  vals.forEach((v,i)=>{
    const x=pad.l+gap*i+(gap-bW)/2;
    const bH=(v/max)*cH; const y=pad.t+cH-bH;
    const g=ctx.createLinearGradient(0,y,0,y+bH);
    g.addColorStop(0,color); g.addColorStop(1,color+'33');
    ctx.fillStyle=g;
    ctx.beginPath();
    if(ctx.roundRect) ctx.roundRect(x,y,bW,bH,3); else ctx.rect(x,y,bW,bH);
    ctx.fill();
    ctx.shadowColor=color; ctx.shadowBlur=6;
    ctx.fill();
    ctx.shadowBlur=0;
    ctx.fillStyle=color; ctx.font='bold 9px Share Tech Mono'; ctx.textAlign='center';
    if(v>0) ctx.fillText(v>999?(v/1000).toFixed(1)+'k':v,x+bW/2,y-4);
    ctx.fillStyle=tc.text; ctx.font='9px Exo 2'; ctx.textAlign='center';
    ctx.fillText(lbls[i]||'',x+bW/2,pad.t+cH+18);
  });
}
function drawLine(id,vals,lbls,color) {
  const c=document.getElementById(id); if(!c) return;
  const W=c.offsetWidth||400, H=c.height; c.width=W;
  const ctx=c.getContext('2d'); ctx.clearRect(0,0,W,H);
  const tc=chartColors();
  if(!vals||vals.length<2){ctx.fillStyle=tc.text;ctx.font='12px Exo 2';ctx.textAlign='center';ctx.fillText('Not enough data',W/2,H/2);return;}
  const pad={t:24,r:16,b:36,l:48};
  const cW=W-pad.l-pad.r, cH=H-pad.t-pad.b;
  const max=Math.max(...vals,1);
  const step=cW/(vals.length-1);
  for(let i=0;i<=4;i++){
    const y=pad.t+cH-(cH/4)*i;
    ctx.strokeStyle=tc.grid; ctx.lineWidth=1;
    ctx.beginPath(); ctx.moveTo(pad.l,y); ctx.lineTo(pad.l+cW,y); ctx.stroke();
    ctx.fillStyle=tc.text; ctx.font='9px Share Tech Mono'; ctx.textAlign='right';
    ctx.fillText(((max/4)*i).toFixed(1),pad.l-4,y+3);
  }
  // Area
  ctx.beginPath();
  vals.forEach((v,i)=>{ const x=pad.l+step*i, y=pad.t+cH-(v/max)*cH; i===0?ctx.moveTo(x,y):ctx.lineTo(x,y); });
  ctx.lineTo(pad.l+step*(vals.length-1),pad.t+cH); ctx.lineTo(pad.l,pad.t+cH); ctx.closePath();
  const ag=ctx.createLinearGradient(0,pad.t,0,pad.t+cH);
  ag.addColorStop(0,color+'55'); ag.addColorStop(1,color+'00');
  ctx.fillStyle=ag; ctx.fill();
  // Line
  ctx.beginPath();
  vals.forEach((v,i)=>{ const x=pad.l+step*i, y=pad.t+cH-(v/max)*cH; i===0?ctx.moveTo(x,y):ctx.lineTo(x,y); });
  ctx.strokeStyle=color; ctx.lineWidth=2; ctx.lineJoin='round'; ctx.shadowColor=color; ctx.shadowBlur=8; ctx.stroke(); ctx.shadowBlur=0;
  // Dots
  vals.forEach((v,i)=>{
    const x=pad.l+step*i, y=pad.t+cH-(v/max)*cH;
    ctx.beginPath(); ctx.arc(x,y,4,0,Math.PI*2);
    ctx.fillStyle=color; ctx.shadowColor=color; ctx.shadowBlur=8; ctx.fill(); ctx.shadowBlur=0;
    ctx.strokeStyle=tc.bg; ctx.lineWidth=2; ctx.stroke();
    ctx.fillStyle=tc.text; ctx.font='9px Exo 2'; ctx.textAlign='center';
    ctx.fillText(lbls[i]||'',x,pad.t+cH+18);
  });
}
function drawTaskBar(id) {
  const c=document.getElementById(id); if(!c) return;
  const W=c.offsetWidth||800, H=c.height; c.width=W;
  const ctx=c.getContext('2d'); ctx.clearRect(0,0,W,H);
  const done=state.tasks.filter(t=>t.done).length, total=state.tasks.length;
  const pct=total>0?(done/total)*100:0;
  const pad=32, bH=32, bY=(H-bH)/2;
  ctx.fillStyle='rgba(255,255,255,0.05)';
  if(ctx.roundRect) ctx.roundRect(pad,bY,W-pad*2,bH,6); else ctx.rect(pad,bY,W-pad*2,bH);
  ctx.fill();
  const fW=(W-pad*2)*(pct/100);
  if(fW>0){
    const g=ctx.createLinearGradient(pad,0,pad+fW,0);
    g.addColorStop(0,'#00ffff'); g.addColorStop(1,'#bf5af2');
    ctx.fillStyle=g; ctx.shadowColor='#00ffff'; ctx.shadowBlur=10;
    if(ctx.roundRect) ctx.roundRect(pad,bY,fW,bH,6); else ctx.rect(pad,bY,fW,bH);
    ctx.fill(); ctx.shadowBlur=0;
  }
  ctx.fillStyle='#ffffff'; ctx.font='bold 11px Press Start 2P'; ctx.textAlign='center';
  ctx.fillText(`${done} / ${total} QUESTS (${Math.round(pct)}%)`,W/2,bY+bH/2+4);
}

/* ──────────────────────────────────────
   LEADERBOARD
────────────────────────────────────── */
function renderLeaderboard() {
  const me={name:'YOU (ADMIN)',ava:'⚔️',level:state.level,xp:state.xp,isMe:true};
  const board=[...MOCK_BOARD,me].sort((a,b)=>b.xp-a.xp).slice(0,10);
  const rnkClass=['gold-r','silv-r','bron-r'];
  const rnkIco=['👑','🥈','🥉'];
  document.getElementById('leaderboard-list').innerHTML=board.map((p,i)=>`
    <div class="lb-row ${p.isMe?'me-row':''}">
      <div class="lb-rank ${rnkClass[i]||''}">${i<3?rnkIco[i]:'#'+(i+1)}</div>
      <div class="lb-ava">${p.ava}</div>
      <div class="lb-name">${esc(p.name)}${p.isMe?'<span class="me-tag"> ◄ YOU</span>':''}</div>
      <div class="lb-lv">LV ${p.level}</div>
      <div class="lb-xp">${p.xp.toLocaleString()} XP</div>
    </div>
  `).join('');
}

/* ──────────────────────────────────────
   SETTINGS
────────────────────────────────────── */
function renderSettings() {
  document.getElementById('goal-steps').value   =state.goals.steps;
  document.getElementById('goal-water').value   =state.goals.water;
  document.getElementById('goal-sleep').value   =state.goals.sleep;
  document.getElementById('goal-calories').value=state.goals.calories;
  syncThemeCheckbox();
  const nc=document.getElementById('notif-cb'); if(nc) nc.checked=state.settings.notif;
}
function saveGoals() {
  state.goals.steps   =parseInt(document.getElementById('goal-steps').value)||10000;
  state.goals.water   =parseInt(document.getElementById('goal-water').value)||8;
  state.goals.sleep   =parseFloat(document.getElementById('goal-sleep').value)||8;
  state.goals.calories=parseInt(document.getElementById('goal-calories').value)||500;
  save();
  showDmgNum(0); // feedback
  const el=document.querySelector('.settings-grid .rpg-btn.primary');
  const rect=el?el.getBoundingClientRect():{left:300,top:300};
  burstParticles(rect.left,rect.top,8);
  alert('Goals saved!');
}
function confirmReset() { document.getElementById('reset-modal').classList.remove('hidden'); }
function resetAllData() {
  localStorage.removeItem('vq2_state');
  state=defaultState(); save();
  document.getElementById('reset-modal').classList.add('hidden');
  renderAll();
  navigate('dashboard');
}

/* ──────────────────────────────────────
   THEME
────────────────────────────────────── */
function toggleTheme() {
  const cur=document.documentElement.getAttribute('data-theme');
  const nxt=cur==='dark'?'light':'dark';
  document.documentElement.setAttribute('data-theme',nxt);
  state.settings.theme=nxt; save();
  syncThemeCheckbox();
  if(document.getElementById('page-analytics').classList.contains('active')) setTimeout(renderAnalytics,50);
}
function syncThemeCheckbox() {
  const cb=document.getElementById('theme-cb'); if(cb) cb.checked=document.documentElement.getAttribute('data-theme')==='light';
  const btn=document.getElementById('theme-btn'); if(btn) btn.textContent=document.documentElement.getAttribute('data-theme')==='dark'?'🌙':'☀️';
}

/* ──────────────────────────────────────
   NOTIFICATIONS
────────────────────────────────────── */
function toggleNotifications() {
  notifEnabled=document.getElementById('notif-cb').checked;
  state.settings.notif=notifEnabled; save();
  if(notifEnabled){ requestNotifPerm(); startNotif(); } else stopNotif();
}
function requestNotifPerm() { if('Notification'in window&&Notification.permission==='default') Notification.requestPermission(); }
function startNotif() { stopNotif(); notifTimer=setInterval(sendNotif,30*60*1000); }
function stopNotif()  { if(notifTimer){clearInterval(notifTimer);notifTimer=null;} }
function sendNotif() {
  const msgs=['💧 Drink a glass of water now!','👟 Take a walk to hit your steps goal!','😴 Plan for 8 hours of sleep tonight.','⚡ Complete a quest to earn XP!','🔥 Keep your streak — log health today!'];
  const msg=msgs[Math.floor(Math.random()*msgs.length)];
  if('Notification'in window&&Notification.permission==='granted'){
    new Notification('VitaQuest RPG',{body:msg});
  } else showNotifToast(msg);
}
function testNotification() { sendNotif(); }
function showNotifToast(msg) {
  const t=document.getElementById('notif-toast');
  document.getElementById('notif-msg').textContent=msg;
  t.classList.remove('hidden');
  setTimeout(()=>t.classList.add('hidden'),4000);
}

/* ──────────────────────────────────────
   DAILY RESET
────────────────────────────────────── */
function checkDailyReset() {
  const last=localStorage.getItem('vq2_reset'), td=today();
  if(last!==td){
    if(state){ state.tasks.forEach(t=>{ if(t.type==='daily') t.done=false; }); if(new Date().getDay()===1) state.tasks.forEach(t=>{ if(t.type==='weekly') t.done=false; }); save(); }
    localStorage.setItem('vq2_reset',td);
  }
}

/* ──────────────────────────────────────
   KEYBOARD SHORTCUTS
────────────────────────────────────── */
document.addEventListener('keydown',e=>{
  if(e.key==='Escape'){
    closeEditModal();
    document.getElementById('reset-modal').classList.add('hidden');
    closeLevelUp();
  }
});

/* ──────────────────────────────────────
   RESIZE
────────────────────────────────────── */
let rzTimer;
window.addEventListener('resize',()=>{
  clearTimeout(rzTimer);
  rzTimer=setTimeout(()=>{
    resizeBg();
    if(document.getElementById('page-analytics').classList.contains('active')) renderAnalytics();
  },200);
});
</script>
</body></html>
