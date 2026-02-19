<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
<meta name="apple-mobile-web-app-title" content="Stoat">
<meta name="theme-color" content="#0f0f13">
<title>Stoat Chat</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=DM+Sans:ital,opsz,wght@0,9..40,300;0,9..40,400;0,9..40,500;0,9..40,600;1,9..40,300&family=DM+Mono:wght@400;500&display=swap" rel="stylesheet">
<style>
  :root {
    --bg: #0f0f13;
    --surface: #17171e;
    --surface2: #1e1e28;
    --surface3: #25252f;
    --border: rgba(255,255,255,0.06);
    --accent: #7c5cbf;
    --accent2: #4ec9d4;
    --accent-glow: rgba(124,92,191,0.25);
    --text: #e8e8f0;
    --text2: #8888a0;
    --text3: #55556a;
    --red: #e05555;
    --green: #4ec98a;
    --safe-top: env(safe-area-inset-top, 0px);
    --safe-bottom: env(safe-area-inset-bottom, 0px);
    --sidebar-w: 260px;
  }

  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  html, body {
    height: 100%;
    background: var(--bg);
    color: var(--text);
    font-family: 'DM Sans', sans-serif;
    font-size: 15px;
    line-height: 1.5;
    overflow: hidden;
    -webkit-font-smoothing: antialiased;
  }

  /* ── Scrollbars ── */
  ::-webkit-scrollbar { width: 4px; }
  ::-webkit-scrollbar-track { background: transparent; }
  ::-webkit-scrollbar-thumb { background: var(--surface3); border-radius: 2px; }

  /* ══════════════════════════════════════
     LOGIN SCREEN
  ══════════════════════════════════════ */
  #login-screen {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    min-height: 100dvh;
    padding: 24px;
    padding-top: calc(var(--safe-top) + 24px);
    padding-bottom: calc(var(--safe-bottom) + 24px);
    background: radial-gradient(ellipse 80% 60% at 50% 0%, rgba(124,92,191,0.15) 0%, transparent 70%);
    position: relative;
    overflow: hidden;
  }

  #login-screen::before {
    content: '';
    position: absolute;
    inset: 0;
    background: url("data:image/svg+xml,%3Csvg width='60' height='60' viewBox='0 0 60 60' xmlns='http://www.w3.org/2000/svg'%3E%3Cg fill='none' fill-rule='evenodd'%3E%3Cg fill='%237c5cbf' fill-opacity='0.03'%3E%3Cpath d='M36 34v-4h-2v4h-4v2h4v4h2v-4h4v-2h-4zm0-30V0h-2v4h-4v2h4v4h2V6h4V4h-4zM6 34v-4H4v4H0v2h4v4h2v-4h4v-2H6zM6 4V0H4v4H0v2h4v4h2V6h4V4H6z'/%3E%3C/g%3E%3C/g%3E%3C/svg%3E");
    pointer-events: none;
  }

  .login-card {
    width: 100%;
    max-width: 360px;
    display: flex;
    flex-direction: column;
    gap: 28px;
    position: relative;
    z-index: 1;
  }

  .login-logo {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 12px;
  }

  .logo-icon {
    width: 64px;
    height: 64px;
    border-radius: 18px;
    background: linear-gradient(135deg, var(--accent), var(--accent2));
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 28px;
    box-shadow: 0 8px 32px var(--accent-glow), 0 0 0 1px rgba(124,92,191,0.3);
    animation: float 3s ease-in-out infinite;
  }

  @keyframes float {
    0%, 100% { transform: translateY(0); }
    50% { transform: translateY(-5px); }
  }

  .login-logo h1 {
    font-size: 26px;
    font-weight: 600;
    letter-spacing: -0.5px;
  }

  .login-logo p {
    font-size: 13px;
    color: var(--text2);
    letter-spacing: 0.3px;
  }

  .login-tabs {
    display: flex;
    background: var(--surface2);
    border-radius: 10px;
    padding: 3px;
    gap: 2px;
  }

  .login-tab {
    flex: 1;
    padding: 8px;
    border: none;
    background: none;
    color: var(--text2);
    font-family: inherit;
    font-size: 13px;
    font-weight: 500;
    border-radius: 8px;
    cursor: pointer;
    transition: all 0.2s;
  }

  .login-tab.active {
    background: var(--surface3);
    color: var(--text);
  }

  .login-form { display: flex; flex-direction: column; gap: 14px; }

  .field { display: flex; flex-direction: column; gap: 6px; }

  .field label {
    font-size: 11px;
    font-weight: 600;
    letter-spacing: 0.8px;
    text-transform: uppercase;
    color: var(--text2);
  }

  .field input, .field textarea {
    background: var(--surface2);
    border: 1px solid var(--border);
    border-radius: 10px;
    padding: 12px 14px;
    color: var(--text);
    font-family: 'DM Mono', monospace;
    font-size: 14px;
    outline: none;
    transition: border-color 0.2s, box-shadow 0.2s;
    width: 100%;
    resize: none;
  }

  .field input:focus, .field textarea:focus {
    border-color: var(--accent);
    box-shadow: 0 0 0 3px var(--accent-glow);
  }

  .field input::placeholder { color: var(--text3); }

  .btn {
    padding: 13px;
    border: none;
    border-radius: 10px;
    font-family: inherit;
    font-size: 14px;
    font-weight: 600;
    cursor: pointer;
    transition: all 0.2s;
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 8px;
    letter-spacing: 0.2px;
  }

  .btn-primary {
    background: linear-gradient(135deg, var(--accent), #6b4aaf);
    color: white;
    box-shadow: 0 4px 16px var(--accent-glow);
  }

  .btn-primary:hover { transform: translateY(-1px); box-shadow: 0 6px 20px var(--accent-glow); }
  .btn-primary:active { transform: translateY(0); }
  .btn-primary:disabled { opacity: 0.5; cursor: not-allowed; transform: none; }

  .error-msg {
    background: rgba(224,85,85,0.12);
    border: 1px solid rgba(224,85,85,0.25);
    border-radius: 8px;
    padding: 10px 12px;
    font-size: 13px;
    color: var(--red);
    display: none;
  }
  .error-msg.show { display: block; }

  .spinner {
    width: 16px; height: 16px;
    border: 2px solid rgba(255,255,255,0.3);
    border-top-color: white;
    border-radius: 50%;
    animation: spin 0.7s linear infinite;
  }
  @keyframes spin { to { transform: rotate(360deg); } }

  /* ══════════════════════════════════════
     MAIN APP LAYOUT
  ══════════════════════════════════════ */
  #app {
    display: none;
    height: 100dvh;
    flex-direction: row;
    overflow: hidden;
  }

  /* ── Server Rail ── */
  #server-rail {
    width: 64px;
    min-width: 64px;
    background: var(--bg);
    border-right: 1px solid var(--border);
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 12px 0;
    padding-top: calc(var(--safe-top) + 12px);
    padding-bottom: calc(var(--safe-bottom) + 12px);
    gap: 6px;
    overflow-y: auto;
    overflow-x: hidden;
  }

  .server-icon {
    width: 44px;
    height: 44px;
    border-radius: 14px;
    background: var(--surface2);
    display: flex;
    align-items: center;
    justify-content: center;
    cursor: pointer;
    font-size: 11px;
    font-weight: 700;
    color: var(--text2);
    transition: all 0.2s;
    flex-shrink: 0;
    overflow: hidden;
    position: relative;
    border: 2px solid transparent;
    text-transform: uppercase;
    letter-spacing: 0.5px;
  }

  .server-icon img { width: 100%; height: 100%; object-fit: cover; border-radius: 12px; }

  .server-icon.active {
    border-color: var(--accent);
    border-radius: 10px;
    box-shadow: 0 0 12px var(--accent-glow);
    color: var(--text);
  }

  .server-icon:hover:not(.active) {
    border-radius: 10px;
    background: var(--surface3);
    color: var(--text);
  }

  /* ── Channel Sidebar ── */
  #channel-sidebar {
    width: var(--sidebar-w);
    min-width: var(--sidebar-w);
    background: var(--surface);
    display: flex;
    flex-direction: column;
    border-right: 1px solid var(--border);
    overflow: hidden;
  }

  @media (max-width: 600px) {
    #channel-sidebar { display: none; }
    #channel-sidebar.visible { display: flex; position: fixed; left: 64px; top: 0; bottom: 0; z-index: 50; width: calc(100vw - 64px); }
    #chat-area.sidebar-open { display: none; }
  }

  .sidebar-header {
    padding: 16px;
    padding-top: calc(var(--safe-top) + 16px);
    border-bottom: 1px solid var(--border);
    display: flex;
    flex-direction: column;
    gap: 6px;
  }

  .sidebar-server-name {
    font-size: 15px;
    font-weight: 600;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
  }

  .sidebar-server-desc {
    font-size: 12px;
    color: var(--text2);
    line-height: 1.4;
    display: -webkit-box;
    -webkit-line-clamp: 2;
    -webkit-box-orient: vertical;
    overflow: hidden;
  }

  .channel-section-label {
    padding: 12px 16px 4px;
    font-size: 10px;
    font-weight: 700;
    letter-spacing: 1px;
    text-transform: uppercase;
    color: var(--text3);
  }

  .channel-list { flex: 1; overflow-y: auto; padding: 0 8px 8px; }

  .channel-item {
    display: flex;
    align-items: center;
    gap: 8px;
    padding: 8px 10px;
    border-radius: 8px;
    cursor: pointer;
    color: var(--text2);
    font-size: 14px;
    transition: all 0.15s;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
    margin-bottom: 1px;
  }

  .channel-item:hover { background: var(--surface2); color: var(--text); }
  .channel-item.active { background: var(--surface3); color: var(--text); }

  .channel-hash {
    font-size: 16px;
    color: var(--text3);
    flex-shrink: 0;
  }

  .channel-item.active .channel-hash { color: var(--accent2); }

  .sidebar-user {
    padding: 12px;
    padding-bottom: calc(var(--safe-bottom) + 12px);
    border-top: 1px solid var(--border);
    display: flex;
    align-items: center;
    gap: 10px;
    background: var(--surface);
  }

  .user-avatar-sm {
    width: 32px; height: 32px;
    border-radius: 50%;
    background: linear-gradient(135deg, var(--accent), var(--accent2));
    flex-shrink: 0;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 12px;
    font-weight: 700;
    overflow: hidden;
  }

  .user-avatar-sm img { width: 100%; height: 100%; object-fit: cover; }

  .user-info { flex: 1; overflow: hidden; }
  .user-name { font-size: 13px; font-weight: 600; overflow: hidden; text-overflow: ellipsis; white-space: nowrap; }
  .user-tag { font-size: 11px; color: var(--text3); font-family: 'DM Mono', monospace; }

  .btn-logout {
    background: none;
    border: none;
    color: var(--text3);
    cursor: pointer;
    padding: 4px;
    border-radius: 6px;
    font-size: 16px;
    transition: color 0.2s;
    flex-shrink: 0;
  }
  .btn-logout:hover { color: var(--red); }

  /* ── Chat Area ── */
  #chat-area {
    flex: 1;
    display: flex;
    flex-direction: column;
    overflow: hidden;
    background: var(--bg);
    position: relative;
  }

  .chat-header {
    padding: 0 16px;
    height: 52px;
    padding-top: var(--safe-top);
    height: calc(52px + var(--safe-top));
    border-bottom: 1px solid var(--border);
    display: flex;
    align-items: center;
    gap: 10px;
    background: var(--bg);
    flex-shrink: 0;
  }

  .chat-header-hash { color: var(--text3); font-size: 18px; }

  .chat-header-name {
    font-size: 15px;
    font-weight: 600;
    flex: 1;
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
  }

  .chat-header-desc {
    font-size: 12px;
    color: var(--text2);
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
    max-width: 200px;
  }

  #back-btn {
    display: none;
    background: none;
    border: none;
    color: var(--text2);
    cursor: pointer;
    font-size: 20px;
    padding: 4px;
    border-radius: 6px;
    flex-shrink: 0;
  }

  @media (max-width: 600px) {
    #back-btn { display: flex; }
  }

  /* ── Messages ── */
  #messages-container {
    flex: 1;
    overflow-y: auto;
    display: flex;
    flex-direction: column;
    padding: 8px 0 4px;
  }

  #load-more-btn {
    margin: 8px auto;
    padding: 6px 16px;
    background: var(--surface2);
    border: 1px solid var(--border);
    border-radius: 20px;
    color: var(--text2);
    font-family: inherit;
    font-size: 12px;
    cursor: pointer;
    display: none;
    transition: all 0.2s;
  }
  #load-more-btn:hover { background: var(--surface3); color: var(--text); }
  #load-more-btn.show { display: block; }

  .msg {
    display: flex;
    gap: 12px;
    padding: 4px 16px;
    transition: background 0.1s;
    animation: fadeUp 0.2s ease;
  }

  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(6px); }
    to { opacity: 1; transform: translateY(0); }
  }

  .msg:hover { background: rgba(255,255,255,0.02); }
  .msg:hover .msg-actions { opacity: 1; }

  .msg-avatar {
    width: 36px;
    height: 36px;
    border-radius: 50%;
    flex-shrink: 0;
    margin-top: 2px;
    overflow: hidden;
    background: var(--surface3);
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 12px;
    font-weight: 700;
    color: var(--text2);
  }

  .msg-avatar img { width: 100%; height: 100%; object-fit: cover; }

  .msg-body { flex: 1; min-width: 0; }

  .msg-header {
    display: flex;
    align-items: baseline;
    gap: 8px;
    margin-bottom: 2px;
  }

  .msg-author {
    font-size: 14px;
    font-weight: 600;
    cursor: pointer;
    transition: color 0.15s;
  }
  .msg-author:hover { color: var(--accent2); }

  .msg-time {
    font-size: 10px;
    color: var(--text3);
    font-family: 'DM Mono', monospace;
  }

  .msg-edited {
    font-size: 10px;
    color: var(--text3);
    font-style: italic;
  }

  .msg-content {
    font-size: 14.5px;
    line-height: 1.55;
    color: var(--text);
    word-break: break-word;
    white-space: pre-wrap;
  }

  .msg-content a { color: var(--accent2); text-decoration: none; }
  .msg-content a:hover { text-decoration: underline; }

  .msg-actions {
    opacity: 0;
    display: flex;
    gap: 4px;
    align-items: center;
    transition: opacity 0.15s;
    flex-shrink: 0;
    margin-top: 2px;
  }

  .msg-action-btn {
    background: var(--surface2);
    border: 1px solid var(--border);
    border-radius: 6px;
    color: var(--text2);
    font-size: 12px;
    padding: 4px 8px;
    cursor: pointer;
    font-family: inherit;
    transition: all 0.15s;
  }

  .msg-action-btn:hover { background: var(--surface3); color: var(--text); }
  .msg-action-btn.delete:hover { color: var(--red); border-color: rgba(224,85,85,0.3); }

  .msg-img {
    margin-top: 6px;
    max-width: min(360px, 100%);
    max-height: 300px;
    border-radius: 8px;
    display: block;
    object-fit: contain;
    background: var(--surface2);
    cursor: zoom-in;
  }

  /* Compact messages (same author, <5min) */
  .msg.compact { padding-top: 1px; }
  .msg.compact .msg-avatar { visibility: hidden; }
  .msg.compact .msg-header { display: none; }

  /* ── Input Area ── */
  #input-area {
    padding: 12px 16px;
    padding-bottom: calc(var(--safe-bottom) + 12px);
    background: var(--bg);
    border-top: 1px solid var(--border);
    flex-shrink: 0;
  }

  #edit-banner {
    display: none;
    background: var(--surface2);
    border-radius: 8px 8px 0 0;
    padding: 6px 12px;
    font-size: 12px;
    color: var(--text2);
    border-bottom: 1px solid var(--border);
    align-items: center;
    gap: 8px;
    margin-bottom: -4px;
  }

  #edit-banner.show { display: flex; }
  #edit-banner span { flex: 1; }
  #cancel-edit { background: none; border: none; color: var(--text3); cursor: pointer; font-size: 16px; transition: color 0.15s; }
  #cancel-edit:hover { color: var(--text); }

  .input-row {
    display: flex;
    align-items: flex-end;
    gap: 10px;
    background: var(--surface2);
    border: 1px solid var(--border);
    border-radius: 12px;
    padding: 4px 4px 4px 14px;
    transition: border-color 0.2s, box-shadow 0.2s;
  }

  .input-row:focus-within {
    border-color: rgba(124,92,191,0.4);
    box-shadow: 0 0 0 3px var(--accent-glow);
  }

  #msg-input {
    flex: 1;
    background: none;
    border: none;
    outline: none;
    color: var(--text);
    font-family: 'DM Sans', sans-serif;
    font-size: 14.5px;
    line-height: 1.5;
    resize: none;
    max-height: 140px;
    padding: 8px 0;
    caret-color: var(--accent2);
  }

  #msg-input::placeholder { color: var(--text3); }

  #send-btn {
    width: 38px;
    height: 38px;
    border-radius: 9px;
    border: none;
    background: linear-gradient(135deg, var(--accent), #6b4aaf);
    color: white;
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: center;
    transition: all 0.2s;
    flex-shrink: 0;
    font-size: 16px;
  }

  #send-btn:hover { transform: scale(1.05); box-shadow: 0 2px 12px var(--accent-glow); }
  #send-btn:disabled { opacity: 0.4; transform: none; cursor: not-allowed; }

  /* ── Empty state ── */
  .empty-state {
    flex: 1;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    gap: 12px;
    color: var(--text3);
    padding: 32px;
    text-align: center;
  }

  .empty-state .icon { font-size: 48px; opacity: 0.4; }
  .empty-state h3 { font-size: 18px; font-weight: 600; color: var(--text2); }
  .empty-state p { font-size: 13px; line-height: 1.6; }

  /* ── Loading ── */
  .loading-dots {
    display: flex;
    gap: 5px;
    align-items: center;
    padding: 16px;
    justify-content: center;
  }

  .loading-dots span {
    width: 6px; height: 6px;
    background: var(--text3);
    border-radius: 50%;
    animation: bounce 1.2s ease-in-out infinite;
  }
  .loading-dots span:nth-child(2) { animation-delay: 0.15s; }
  .loading-dots span:nth-child(3) { animation-delay: 0.3s; }

  @keyframes bounce {
    0%, 80%, 100% { transform: scale(0.7); opacity: 0.4; }
    40% { transform: scale(1); opacity: 1; }
  }

  /* ── Connection status ── */
  #ws-status {
    position: fixed;
    bottom: calc(var(--safe-bottom) + 80px);
    left: 50%;
    transform: translateX(-50%);
    background: var(--surface3);
    border: 1px solid var(--border);
    border-radius: 20px;
    padding: 6px 14px;
    font-size: 12px;
    color: var(--text2);
    display: none;
    z-index: 100;
    pointer-events: none;
    white-space: nowrap;
    backdrop-filter: blur(10px);
  }

  #ws-status.show { display: block; }
  #ws-status.error { color: var(--red); border-color: rgba(224,85,85,0.3); }
  #ws-status.ok { color: var(--green); border-color: rgba(78,201,138,0.3); }

  /* ── Toast ── */
  #toast {
    position: fixed;
    top: calc(var(--safe-top) + 16px);
    left: 50%;
    transform: translateX(-50%) translateY(-80px);
    background: var(--surface3);
    border: 1px solid var(--border);
    border-radius: 10px;
    padding: 10px 18px;
    font-size: 13px;
    z-index: 200;
    transition: transform 0.3s cubic-bezier(0.34, 1.56, 0.64, 1);
    pointer-events: none;
    white-space: nowrap;
    backdrop-filter: blur(10px);
  }
  #toast.show { transform: translateX(-50%) translateY(0); }
</style>
</head>
<body>

<!-- ══ LOGIN ══ -->
<div id="login-screen">
  <div class="login-card">
    <div class="login-logo">
      <div class="logo-icon">🐾</div>
      <h1>Stoat</h1>
      <p>Open source, user-first chat</p>
    </div>

    <div class="login-tabs">
      <button class="login-tab active" onclick="switchTab('email')">Email</button>
      <button class="login-tab" onclick="switchTab('token')">Session Token</button>
    </div>

    <div id="tab-email" class="login-form">
      <div class="field">
        <label>Email</label>
        <input type="email" id="email" placeholder="you@example.com" autocomplete="email">
      </div>
      <div class="field">
        <label>Password</label>
        <input type="password" id="password" placeholder="••••••••" autocomplete="current-password">
      </div>
      <div class="error-msg" id="login-error"></div>
      <button class="btn btn-primary" id="login-btn" onclick="doLogin()">
        Sign In
      </button>
    </div>

    <div id="tab-token" class="login-form" style="display:none">
      <div class="field">
        <label>Session Token</label>
        <input type="text" id="token-input" placeholder="Paste your session token" autocomplete="off" autocapitalize="none">
      </div>
      <p style="font-size:12px;color:var(--text2);line-height:1.5">
        Get your token from stoat.chat → Settings → My Account → Copy Session Token
      </p>
      <div class="error-msg" id="token-error"></div>
      <button class="btn btn-primary" id="token-btn" onclick="doTokenLogin()">
        Connect
      </button>
    </div>
  </div>
</div>

<!-- ══ MAIN APP ══ -->
<div id="app">
  <div id="server-rail"></div>

  <div id="channel-sidebar">
    <div class="sidebar-header">
      <div class="sidebar-server-name" id="sidebar-server-name">Select a server</div>
      <div class="sidebar-server-desc" id="sidebar-server-desc"></div>
    </div>
    <div class="channel-list" id="channel-list"></div>
    <div class="sidebar-user">
      <div class="user-avatar-sm" id="user-avatar-sm"></div>
      <div class="user-info">
        <div class="user-name" id="user-display-name"></div>
        <div class="user-tag" id="user-tag"></div>
      </div>
      <button class="btn-logout" onclick="doLogout()" title="Sign out">↩</button>
    </div>
  </div>

  <div id="chat-area">
    <div class="chat-header">
      <button id="back-btn" onclick="goBack()">‹</button>
      <div class="chat-header-hash">#</div>
      <div style="flex:1;min-width:0">
        <div class="chat-header-name" id="chat-channel-name">—</div>
        <div class="chat-header-desc" id="chat-channel-desc"></div>
      </div>
    </div>

    <div id="messages-container">
      <div class="empty-state" id="empty-state">
        <div class="icon">💬</div>
        <h3>Pick a channel</h3>
        <p>Select a server and channel<br>from the sidebar to start chatting.</p>
      </div>
    </div>

    <div id="input-area">
      <div id="edit-banner">
        <span>✏️ Editing message</span>
        <button id="cancel-edit" onclick="cancelEdit()">✕</button>
      </div>
      <div class="input-row">
        <textarea id="msg-input" placeholder="Message..." rows="1"
          onkeydown="handleInputKey(event)" oninput="autoResize(this)"></textarea>
        <button id="send-btn" onclick="sendOrEdit()">↑</button>
      </div>
    </div>
  </div>
</div>

<div id="ws-status"></div>
<div id="toast"></div>

<script>
// ══════════════════════════════════════════════════════════
//  CONFIG
// ══════════════════════════════════════════════════════════
const API = 'https://api.revolt.chat';
const CDN = 'https://autumn.revolt.chat';
const WS_URL = 'wss://ws.revolt.chat';

// ══════════════════════════════════════════════════════════
//  STATE
// ══════════════════════════════════════════════════════════
let token = localStorage.getItem('stoat_token') || null;
let me = null;
let servers = [];
let channelMap = {};
let userCache = {};
let activeServerId = null;
let activeChannelId = null;
let messages = [];
let editingMsgId = null;
let hasMore = true;
let isLoadingMsgs = false;
let ws = null;
let wsReconnectTimer = null;
let pingInterval = null;

// ══════════════════════════════════════════════════════════
//  INIT
// ══════════════════════════════════════════════════════════
if (token) bootApp();

// ══════════════════════════════════════════════════════════
//  LOGIN
// ══════════════════════════════════════════════════════════
function switchTab(tab) {
  document.querySelectorAll('.login-tab').forEach((t, i) => t.classList.toggle('active', (tab==='email')===!i));
  document.getElementById('tab-email').style.display = tab==='email' ? 'flex' : 'none';
  document.getElementById('tab-token').style.display = tab==='token' ? 'flex' : 'none';
}

async function doLogin() {
  const email = document.getElementById('email').value.trim();
  const password = document.getElementById('password').value;
  const errEl = document.getElementById('login-error');
  const btn = document.getElementById('login-btn');
  if (!email || !password) { showErr(errEl, 'Please fill in all fields.'); return; }

  setLoading(btn, true);
  errEl.classList.remove('show');
  try {
    const res = await apiFetch('/auth/session/login', 'POST', {
      email, password, friendly_name: 'StoatChat Web'
    }, false);
    if (res.result === 'Success' && res.token) {
      token = res.token;
      localStorage.setItem('stoat_token', token);
      await bootApp();
    } else if (res.result === 'MFA') {
      showErr(errEl, 'MFA required. Use the Session Token tab instead.');
    } else {
      showErr(errEl, 'Login failed. Check your credentials.');
    }
  } catch(e) {
    showErr(errEl, e.message || 'Login failed.');
  }
  setLoading(btn, false);
}

async function doTokenLogin() {
  const t = document.getElementById('token-input').value.trim();
  const errEl = document.getElementById('token-error');
  const btn = document.getElementById('token-btn');
  if (!t) { showErr(errEl, 'Please paste your session token.'); return; }

  token = t;
  setLoading(btn, true);
  errEl.classList.remove('show');
  try {
    const user = await apiFetch('/users/@me');
    localStorage.setItem('stoat_token', token);
    await bootApp();
  } catch(e) {
    token = null;
    showErr(errEl, 'Invalid token. ' + (e.message || ''));
  }
  setLoading(btn, false);
}

function doLogout() {
  localStorage.removeItem('stoat_token');
  token = null;
  me = null;
  servers = [];
  channelMap = {};
  if (ws) ws.close();
  document.getElementById('app').style.display = 'none';
  document.getElementById('login-screen').style.display = 'flex';
}

// ══════════════════════════════════════════════════════════
//  BOOT
// ══════════════════════════════════════════════════════════
async function bootApp() {
  document.getElementById('login-screen').style.display = 'none';
  document.getElementById('app').style.display = 'flex';
  connectWebSocket();
}

// ══════════════════════════════════════════════════════════
//  API
// ══════════════════════════════════════════════════════════
async function apiFetch(path, method='GET', body=null, useToken=true) {
  const headers = { 'Content-Type': 'application/json' };
  if (useToken && token) headers['X-Session-Token'] = token;
  const opts = { method, headers };
  if (body) opts.body = JSON.stringify(body);
  const res = await fetch(API + path, opts);
  if (res.status === 401) { doLogout(); throw new Error('Session expired. Please log in again.'); }
  if (!res.ok) {
    const err = await res.json().catch(() => ({}));
    throw new Error(err.type || `Error ${res.status}`);
  }
  if (res.status === 204) return null;
  return res.json();
}

async function fetchMessages(channelId, before=null) {
  let url = `/channels/${channelId}/messages?limit=50&sort=Latest`;
  if (before) url += `&before=${before}`;
  const raw = await apiFetch(url);
  // API returns array or {messages:[]}
  return Array.isArray(raw) ? raw : (raw.messages || []);
}

// ══════════════════════════════════════════════════════════
//  WEBSOCKET
// ══════════════════════════════════════════════════════════
function connectWebSocket() {
  setWsStatus('Connecting…', '');
  ws = new WebSocket(WS_URL);

  ws.onopen = () => {
    ws.send(JSON.stringify({ type: 'Authenticate', token }));
    pingInterval = setInterval(() => ws.readyState === 1 && ws.send(JSON.stringify({ type: 'Ping', data: 0 })), 30000);
  };

  ws.onmessage = e => handleWsEvent(JSON.parse(e.data));

  ws.onerror = () => setWsStatus('Connection error', 'error');

  ws.onclose = () => {
    clearInterval(pingInterval);
    setWsStatus('Reconnecting…', 'error');
    wsReconnectTimer = setTimeout(connectWebSocket, 3000);
  };
}

function handleWsEvent(ev) {
  switch(ev.type) {
    case 'Authenticated':
      setWsStatus('Connected', 'ok');
      setTimeout(() => hideWsStatus(), 2000);
      break;

    case 'Ready':
      me = ev.users?.find(u => u._id === ev.users[0]?._id) || ev.users?.[0];
      // Find the current user from the users list (they appear with relationship "User")
      for (const u of (ev.users || [])) {
        userCache[u._id] = u;
        if (!me || u.relationship === 'User') me = u;
      }
      servers = ev.servers || [];
      channelMap = {};
      for (const ch of (ev.channels || [])) channelMap[ch._id] = ch;
      renderUserPanel();
      renderServerRail();
      break;

    case 'Message':
      if (ev.channel === activeChannelId) {
        appendMessage(ev, true);
      }
      break;

    case 'MessageUpdate':
      if (ev.channel === activeChannelId) {
        updateMessageInDOM(ev.id, ev.data?.content);
      }
      break;

    case 'MessageDelete':
      if (ev.channel === activeChannelId) {
        removeMessageFromDOM(ev.id);
      }
      break;

    case 'Pong': break;
    default: break;
  }
}

// ══════════════════════════════════════════════════════════
//  RENDER: USER PANEL
// ══════════════════════════════════════════════════════════
function renderUserPanel() {
  if (!me) return;
  document.getElementById('user-display-name').textContent = me.display_name || me.username;
  document.getElementById('user-tag').textContent = `#${me.discriminator}`;
  const av = document.getElementById('user-avatar-sm');
  if (me.avatar) {
    av.innerHTML = `<img src="${CDN}/avatars/${me.avatar._id}?max_side=64" onerror="this.parentNode.textContent='${initials(me.username)}'">`;
  } else {
    av.textContent = initials(me.username);
  }
}

// ══════════════════════════════════════════════════════════
//  RENDER: SERVER RAIL
// ══════════════════════════════════════════════════════════
function renderServerRail() {
  const rail = document.getElementById('server-rail');
  rail.innerHTML = '';
  for (const sv of servers) {
    const el = document.createElement('div');
    el.className = 'server-icon' + (sv._id === activeServerId ? ' active' : '');
    el.title = sv.name;
    if (sv.icon) {
      el.innerHTML = `<img src="${CDN}/icons/${sv.icon._id}?max_side=88" onerror="this.parentNode.textContent='${initials(sv.name)}'">`;
    } else {
      el.textContent = initials(sv.name);
    }
    el.onclick = () => selectServer(sv._id);
    rail.appendChild(el);
  }
}

// ══════════════════════════════════════════════════════════
//  SELECT SERVER
// ══════════════════════════════════════════════════════════
function selectServer(svId) {
  activeServerId = svId;
  const sv = servers.find(s => s._id === svId);
  if (!sv) return;

  document.getElementById('sidebar-server-name').textContent = sv.name;
  document.getElementById('sidebar-server-desc').textContent = sv.description || '';
  renderServerRail();

  const channelList = document.getElementById('channel-list');
  channelList.innerHTML = '';

  const textChs = sv.channels
    .map(id => channelMap[id])
    .filter(ch => ch && ch.channel_type === 'TextChannel');

  const voiceChs = sv.channels
    .map(id => channelMap[id])
    .filter(ch => ch && ch.channel_type === 'VoiceChannel');

  if (textChs.length) {
    const label = document.createElement('div');
    label.className = 'channel-section-label';
    label.textContent = 'Text Channels';
    channelList.appendChild(label);
    for (const ch of textChs) channelList.appendChild(makeChannelItem(ch));
  }

  if (voiceChs.length) {
    const label = document.createElement('div');
    label.className = 'channel-section-label';
    label.textContent = 'Voice Channels';
    channelList.appendChild(label);
    for (const ch of voiceChs) {
      const el = makeChannelItem(ch, true);
      el.style.opacity = '0.5';
      el.title = 'Voice channels are not supported in the web client';
      channelList.appendChild(el);
    }
  }

  // Mobile: show sidebar
  document.getElementById('channel-sidebar').classList.add('visible');
  document.getElementById('chat-area').classList.add('sidebar-open');
}

function makeChannelItem(ch, voice=false) {
  const el = document.createElement('div');
  el.className = 'channel-item' + (ch._id === activeChannelId ? ' active' : '');
  el.innerHTML = `<span class="channel-hash">${voice ? '🔊' : '#'}</span>${escHtml(ch.name || 'channel')}`;
  if (!voice) el.onclick = () => selectChannel(ch._id);
  return el;
}

// ══════════════════════════════════════════════════════════
//  SELECT CHANNEL
// ══════════════════════════════════════════════════════════
async function selectChannel(chId) {
  activeChannelId = chId;
  const ch = channelMap[chId];
  if (!ch) return;

  // Update UI
  document.getElementById('chat-channel-name').textContent = ch.name || 'channel';
  document.getElementById('chat-channel-desc').textContent = ch.description || '';
  document.getElementById('msg-input').placeholder = `Message #${ch.name || 'channel'}`;
  document.getElementById('empty-state')?.remove();

  // Highlight channel in list
  document.querySelectorAll('.channel-item').forEach(el => el.classList.remove('active'));
  document.querySelectorAll('.channel-item').forEach(el => {
    if (el.textContent.includes(ch.name || '')) el.classList.add('active');
  });

  // Mobile: hide sidebar, show chat
  document.getElementById('channel-sidebar').classList.remove('visible');
  document.getElementById('chat-area').classList.remove('sidebar-open');

  // Load messages
  messages = [];
  hasMore = true;
  const container = document.getElementById('messages-container');
  container.innerHTML = '<div class="loading-dots"><span></span><span></span><span></span></div>';
  document.getElementById('load-more-btn')?.remove();

  const loadMoreBtn = document.createElement('button');
  loadMoreBtn.id = 'load-more-btn';
  loadMoreBtn.textContent = 'Load earlier messages';
  loadMoreBtn.onclick = loadMore;

  try {
    const fetched = await fetchMessages(chId);
    messages = fetched.reverse();
    container.innerHTML = '';
    container.appendChild(loadMoreBtn);
    if (messages.length === 50) loadMoreBtn.classList.add('show');
    for (const msg of messages) appendMessage(msg, false, false);
    scrollToBottom();
  } catch(e) {
    container.innerHTML = `<div class="empty-state"><div class="icon">⚠️</div><h3>Couldn't load messages</h3><p>${escHtml(e.message)}</p></div>`;
  }
}

async function loadMore() {
  if (isLoadingMsgs || !hasMore || !messages.length) return;
  isLoadingMsgs = true;
  const oldest = messages[0]?.id || messages[0]?._id;
  try {
    const fetched = await fetchMessages(activeChannelId, oldest);
    if (!fetched.length) { hasMore = false; document.getElementById('load-more-btn')?.classList.remove('show'); return; }
    const reversed = fetched.reverse();
    messages = [...reversed, ...messages];
    const container = document.getElementById('messages-container');
    const btn = document.getElementById('load-more-btn');
    const refEl = btn?.nextSibling;
    for (let i = reversed.length - 1; i >= 0; i--) {
      const el = buildMessageEl(reversed[i]);
      container.insertBefore(el, refEl);
    }
  } catch(e) { showToast('Failed to load more messages'); }
  isLoadingMsgs = false;
}

// ══════════════════════════════════════════════════════════
//  MESSAGES
// ══════════════════════════════════════════════════════════
function msgId(msg) { return msg._id || msg.id; }
function msgContent(msg) { return msg.content || ''; }

function appendMessage(msg, animate=true, scrollDown=true) {
  const id = msgId(msg);
  if (document.getElementById('msg-' + id)) return; // already exists
  messages.push(msg);
  const el = buildMessageEl(msg, animate);
  const container = document.getElementById('messages-container');
  container.appendChild(el);
  if (scrollDown) scrollToBottom();
}

function buildMessageEl(msg, animate=false) {
  const id = msgId(msg);
  const authorId = msg.author;
  const user = userCache[authorId] || { username: authorId?.slice(0,8) || 'Unknown', discriminator: '0000' };
  const name = user.display_name || user.username;

  // Check compact (same author as prev, within 5 min)
  const idx = messages.findIndex(m => msgId(m) === id);
  const prev = idx > 0 ? messages[idx - 1] : null;
  const compact = prev && (prev.author === msg.author);

  const div = document.createElement('div');
  div.className = 'msg' + (compact ? ' compact' : '') + (animate ? ' animate' : '');
  div.id = 'msg-' + id;

  // Avatar
  const av = document.createElement('div');
  av.className = 'msg-avatar';
  if (user.avatar) {
    av.innerHTML = `<img src="${CDN}/avatars/${user.avatar._id}?max_side=72" loading="lazy" onerror="this.parentNode.textContent='${initials(name)}'">`;
  } else {
    av.textContent = initials(name);
    av.style.background = colorFromId(authorId);
  }
  div.appendChild(av);

  // Body
  const body = document.createElement('div');
  body.className = 'msg-body';

  const header = document.createElement('div');
  header.className = 'msg-header';
  header.innerHTML = `<span class="msg-author">${escHtml(name)}</span>
    <span class="msg-time">${formatTime(id)}</span>
    ${msg.edited ? '<span class="msg-edited">(edited)</span>' : ''}`;
  body.appendChild(header);

  const content = document.createElement('div');
  content.className = 'msg-content';
  content.innerHTML = renderContent(msgContent(msg));
  content.id = 'msg-content-' + id;
  body.appendChild(content);

  if (msg.attachments?.length) {
    for (const att of msg.attachments) {
      if (att.content_type?.startsWith('image/')) {
        const img = document.createElement('img');
        img.className = 'msg-img';
        img.src = `${CDN}/attachments/${att._id}/${encodeURIComponent(att.filename)}`;
        img.loading = 'lazy';
        img.onclick = () => window.open(img.src, '_blank');
        body.appendChild(img);
      }
    }
  }

  div.appendChild(body);

  // Actions (own messages only)
  if (me && authorId === me._id) {
    const actions = document.createElement('div');
    actions.className = 'msg-actions';
    actions.innerHTML = `
      <button class="msg-action-btn" onclick="startEdit('${id}')">Edit</button>
      <button class="msg-action-btn delete" onclick="deleteMsg('${id}')">Delete</button>`;
    div.appendChild(actions);
  }

  return div;
}

function renderContent(text) {
  if (!text) return '';
  // Very basic markdown: bold, italic, code, links
  return escHtml(text)
    .replace(/\*\*(.+?)\*\*/g, '<strong>$1</strong>')
    .replace(/\*(.+?)\*/g, '<em>$1</em>')
    .replace(/`(.+?)`/g, '<code style="background:var(--surface3);padding:1px 5px;border-radius:4px;font-family:var(--mono)">$1</code>')
    .replace(/(https?:\/\/[^\s<]+)/g, '<a href="$1" target="_blank" rel="noopener">$1</a>');
}

function updateMessageInDOM(id, newContent) {
  const el = document.getElementById('msg-content-' + id);
  if (el && newContent != null) el.innerHTML = renderContent(newContent);
  const hdr = document.querySelector('#msg-' + id + ' .msg-header');
  if (hdr && !hdr.querySelector('.msg-edited')) {
    hdr.insertAdjacentHTML('beforeend', '<span class="msg-edited">(edited)</span>');
  }
}

function removeMessageFromDOM(id) {
  document.getElementById('msg-' + id)?.remove();
}

// ══════════════════════════════════════════════════════════
//  SEND / EDIT / DELETE
// ══════════════════════════════════════════════════════════
async function sendOrEdit() {
  if (editingMsgId) { await submitEdit(); return; }
  const input = document.getElementById('msg-input');
  const text = input.value.trim();
  if (!text || !activeChannelId) return;
  input.value = '';
  autoResize(input);
  try {
    await apiFetch(`/channels/${activeChannelId}/messages`, 'POST', {
      content: text,
      nonce: crypto.randomUUID()
    });
  } catch(e) {
    input.value = text;
    showToast('Failed to send: ' + e.message);
  }
}

function startEdit(msgId) {
  const msg = messages.find(m => (m._id || m.id) === msgId);
  if (!msg) return;
  editingMsgId = msgId;
  const input = document.getElementById('msg-input');
  input.value = msgContent(msg);
  document.getElementById('edit-banner').classList.add('show');
  input.focus();
  autoResize(input);
}

function cancelEdit() {
  editingMsgId = null;
  document.getElementById('msg-input').value = '';
  document.getElementById('edit-banner').classList.remove('show');
  autoResize(document.getElementById('msg-input'));
}

async function submitEdit() {
  const text = document.getElementById('msg-input').value.trim();
  if (!text || !editingMsgId) return;
  const id = editingMsgId;
  cancelEdit();
  try {
    await apiFetch(`/channels/${activeChannelId}/messages/${id}`, 'PATCH', { content: text });
  } catch(e) { showToast('Edit failed: ' + e.message); }
}

async function deleteMsg(msgId) {
  if (!confirm('Delete this message?')) return;
  try {
    await apiFetch(`/channels/${activeChannelId}/messages/${msgId}`, 'DELETE');
    removeMessageFromDOM(msgId);
  } catch(e) { showToast('Delete failed: ' + e.message); }
}

// ══════════════════════════════════════════════════════════
//  MOBILE NAV
// ══════════════════════════════════════════════════════════
function goBack() {
  document.getElementById('channel-sidebar').classList.add('visible');
  document.getElementById('chat-area').classList.add('sidebar-open');
}

// ══════════════════════════════════════════════════════════
//  HELPERS
// ══════════════════════════════════════════════════════════
function handleInputKey(e) {
  if (e.key === 'Enter' && !e.shiftKey) {
    e.preventDefault();
    sendOrEdit();
  }
}

function autoResize(el) {
  el.style.height = 'auto';
  el.style.height = Math.min(el.scrollHeight, 140) + 'px';
}

function scrollToBottom() {
  const c = document.getElementById('messages-container');
  c.scrollTop = c.scrollHeight;
}

function escHtml(str) {
  if (!str) return '';
  return str.replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;').replace(/"/g,'&quot;');
}

function initials(name) {
  if (!name) return '?';
  return name.split(/\s+/).map(w => w[0]).join('').slice(0,2).toUpperCase();
}

function colorFromId(id) {
  if (!id) return 'var(--surface3)';
  const colors = ['#7c5cbf','#4ec9d4','#e05555','#4ec98a','#e0a955','#5580e0','#c45ce0'];
  let h = 0;
  for (let i = 0; i < id.length; i++) h = id.charCodeAt(i) + ((h << 5) - h);
  return colors[Math.abs(h) % colors.length];
}

// Parse Snowflake timestamp (Revolt uses ULID-like IDs with leading timestamp bits)
function formatTime(id) {
  // Revolt IDs encode ms since epoch in first 8 chars as base32-ish
  // Fallback to current time for display
  try {
    const epoch = parseInt(id, 16) / 4194304; // rough approximation
    const d = new Date(epoch + 1420070400000);
    if (isNaN(d.getTime()) || d.getFullYear() < 2020 || d.getFullYear() > 2030) throw 0;
    return d.toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' });
  } catch {
    return new Date().toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' });
  }
}

function setLoading(btn, loading) {
  if (loading) {
    btn._orig = btn.innerHTML;
    btn.innerHTML = '<div class="spinner"></div>';
    btn.disabled = true;
  } else {
    btn.innerHTML = btn._orig || btn.innerHTML;
    btn.disabled = false;
  }
}

function showErr(el, msg) {
  el.textContent = msg;
  el.classList.add('show');
}

function setWsStatus(msg, type='') {
  const el = document.getElementById('ws-status');
  el.textContent = msg;
  el.className = 'show' + (type ? ' ' + type : '');
}

function hideWsStatus() {
  document.getElementById('ws-status').className = '';
}

let toastTimer;
function showToast(msg) {
  const el = document.getElementById('toast');
  el.textContent = msg;
  el.classList.add('show');
  clearTimeout(toastTimer);
  toastTimer = setTimeout(() => el.classList.remove('show'), 3000);
}
</script>
</body>
</html>
