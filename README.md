<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>GitHub Profile Preview</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@400;500&family=Mona+Sans:wght@300;400;500;600&display=swap');

  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  :root {
    --bg: #0d1117;
    --surface: #161b22;
    --border: #21262d;
    --border-subtle: #1c2128;
    --text: #e6edf3;
    --text-muted: #7d8590;
    --text-dim: #484f58;
    --accent: #58a6ff;
    --accent-green: #3fb950;
    --accent-purple: #bc8cff;
    --accent-orange: #ffa657;
  }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: 'Mona Sans', -apple-system, sans-serif;
    font-size: 14px;
    line-height: 1.6;
    min-height: 100vh;
    padding: 32px 16px;
  }

  .github-shell {
    max-width: 980px;
    margin: 0 auto;
    display: grid;
    grid-template-columns: 260px 1fr;
    gap: 24px;
    align-items: start;
  }

  /* Sidebar */
  .sidebar {
    display: flex;
    flex-direction: column;
    gap: 16px;
  }

  .avatar-wrap {
    position: relative;
  }

  .avatar {
    width: 100%;
    aspect-ratio: 1;
    border-radius: 50%;
    background: linear-gradient(135deg, #1c2128 0%, #21262d 100%);
    border: 1px solid var(--border);
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 72px;
    font-weight: 600;
    color: var(--text-muted);
    letter-spacing: -2px;
    overflow: hidden;
  }

  .avatar-inner {
    width: 100%;
    height: 100%;
    background: linear-gradient(135deg, #161b22 0%, #0d1117 60%, #1c2128 100%);
    display: flex;
    align-items: center;
    justify-content: center;
    font-family: 'JetBrains Mono', monospace;
    font-size: 56px;
    color: #3fb950;
    text-shadow: 0 0 40px rgba(63,185,80,0.3);
  }

  .sidebar-name {
    font-size: 20px;
    font-weight: 600;
    color: var(--text);
    line-height: 1.25;
  }

  .sidebar-handle {
    font-size: 16px;
    font-weight: 300;
    color: var(--text-muted);
    margin-top: 2px;
  }

  .sidebar-bio {
    font-size: 13px;
    color: var(--text);
    line-height: 1.5;
  }

  .sidebar-meta {
    display: flex;
    flex-direction: column;
    gap: 6px;
  }

  .meta-item {
    display: flex;
    align-items: center;
    gap: 8px;
    font-size: 13px;
    color: var(--text-muted);
  }

  .meta-item svg {
    width: 16px;
    height: 16px;
    flex-shrink: 0;
    opacity: 0.6;
  }

  .meta-link {
    color: var(--accent);
    text-decoration: none;
  }

  .meta-link:hover { text-decoration: underline; }

  .follow-btn {
    width: 100%;
    padding: 5px 16px;
    background: #21262d;
    border: 1px solid rgba(240,246,252,0.1);
    border-radius: 6px;
    color: var(--text);
    font-size: 13px;
    font-weight: 500;
    cursor: pointer;
    text-align: center;
    transition: background 0.15s, border-color 0.15s;
  }

  .follow-btn:hover { background: #30363d; border-color: rgba(240,246,252,0.2); }

  /* Main content */
  .main {
    min-width: 0;
  }

  .readme-card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 6px;
    overflow: hidden;
  }

  .readme-header {
    display: flex;
    align-items: center;
    gap: 8px;
    padding: 10px 16px;
    border-bottom: 1px solid var(--border);
    background: rgba(22, 27, 34, 0.8);
  }

  .readme-header svg { color: var(--text-muted); width: 16px; height: 16px; }

  .readme-header-text {
    font-size: 12px;
    font-weight: 600;
    color: var(--text-muted);
    letter-spacing: 0.02em;
  }

  .readme-body {
    padding: 24px 32px;
  }

  /* Markdown styles */
  .md h1 {
    font-size: 28px;
    font-weight: 600;
    color: var(--text);
    border-bottom: 1px solid var(--border);
    padding-bottom: 12px;
    margin-bottom: 16px;
    letter-spacing: -0.5px;
  }

  .md h3 {
    font-size: 16px;
    font-weight: 600;
    color: var(--text);
    margin: 24px 0 12px;
    padding-bottom: 6px;
    border-bottom: 1px solid var(--border-subtle);
  }

  .md p {
    color: #8b949e;
    margin-bottom: 12px;
    font-size: 14px;
    line-height: 1.65;
  }

  .md strong {
    color: var(--text);
    font-weight: 600;
  }

  .md blockquote {
    border-left: 3px solid var(--accent);
    padding: 4px 0 4px 16px;
    margin-bottom: 16px;
  }

  .md blockquote p {
    color: var(--text-muted);
    font-size: 13px;
    margin: 0;
  }

  .md blockquote a {
    color: var(--accent);
    text-decoration: none;
    font-weight: 500;
  }

  .md blockquote a:hover { text-decoration: underline; }

  .md hr {
    border: none;
    border-top: 1px solid var(--border);
    margin: 24px 0;
  }

  .md a { color: var(--accent); text-decoration: none; }
  .md a:hover { text-decoration: underline; }

  .md em { color: var(--text-muted); font-style: normal; font-size: 13px; }

  .md pre {
    background: #0d1117;
    border: 1px solid var(--border);
    border-radius: 6px;
    padding: 16px;
    overflow-x: auto;
    margin-bottom: 12px;
    font-family: 'JetBrains Mono', monospace;
    font-size: 12.5px;
    line-height: 1.7;
    color: #8b949e;
  }

  .focus-grid {
    display: grid;
    gap: 0;
    background: #0d1117;
    border: 1px solid var(--border);
    border-radius: 6px;
    overflow: hidden;
    margin-bottom: 12px;
  }

  .focus-row {
    display: grid;
    grid-template-columns: 160px 1fr;
    gap: 0;
    border-bottom: 1px solid var(--border-subtle);
    padding: 11px 16px;
    transition: background 0.1s;
  }

  .focus-row:last-child { border-bottom: none; }
  .focus-row:hover { background: rgba(255,255,255,0.02); }

  .focus-label {
    font-family: 'JetBrains Mono', monospace;
    font-size: 12px;
    color: var(--accent-green);
    font-weight: 500;
    padding-right: 16px;
    white-space: nowrap;
  }

  .focus-desc {
    font-family: 'JetBrains Mono', monospace;
    font-size: 12px;
    color: #8b949e;
    line-height: 1.5;
  }

  .stack-grid {
    background: #0d1117;
    border: 1px solid var(--border);
    border-radius: 6px;
    padding: 14px 16px;
    margin-bottom: 12px;
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 4px 24px;
  }

  .stack-row {
    display: flex;
    align-items: baseline;
    gap: 8px;
    font-family: 'JetBrains Mono', monospace;
    font-size: 12px;
    color: #8b949e;
    padding: 3px 0;
  }

  .stack-dot {
    color: var(--accent-purple);
    font-size: 14px;
    line-height: 1;
  }

  .open-to {
    display: flex;
    gap: 8px;
    flex-wrap: wrap;
    margin-top: 4px;
  }

  .tag {
    padding: 3px 10px;
    border-radius: 20px;
    font-size: 12px;
    font-weight: 500;
    border: 1px solid;
  }

  .tag-blue { color: var(--accent); border-color: rgba(88,166,255,0.25); background: rgba(88,166,255,0.06); }
  .tag-green { color: var(--accent-green); border-color: rgba(63,185,80,0.25); background: rgba(63,185,80,0.06); }
  .tag-orange { color: var(--accent-orange); border-color: rgba(255,166,87,0.25); background: rgba(255,166,87,0.06); }

  /* Stats row */
  .stats-row {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 12px;
    margin-bottom: 16px;
  }

  .stat-card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 6px;
    padding: 16px;
    text-align: center;
  }

  .stat-num {
    font-size: 24px;
    font-weight: 600;
    color: var(--text);
    font-family: 'JetBrains Mono', monospace;
    letter-spacing: -1px;
  }

  .stat-label {
    font-size: 11px;
    color: var(--text-muted);
    margin-top: 2px;
    text-transform: uppercase;
    letter-spacing: 0.05em;
  }

  /* Contribution graph placeholder */
  .contrib-card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 6px;
    padding: 16px;
    margin-top: 16px;
  }

  .contrib-title {
    font-size: 12px;
    color: var(--text-muted);
    margin-bottom: 12px;
  }

  .contrib-grid {
    display: grid;
    grid-template-columns: repeat(52, 1fr);
    gap: 3px;
  }

  .contrib-cell {
    aspect-ratio: 1;
    border-radius: 2px;
    background: #161b22;
  }

  .contrib-cell.l1 { background: #0e4429; }
  .contrib-cell.l2 { background: #006d32; }
  .contrib-cell.l3 { background: #26a641; }
  .contrib-cell.l4 { background: #39d353; }

  .bottom-meta {
    margin-top: 20px;
    font-size: 13px;
    color: var(--text-muted);
  }

  .bottom-meta a { color: var(--accent); text-decoration: none; }
  .bottom-meta a:hover { text-decoration: underline; }
</style>
</head>
<body>

<div class="github-shell">

  <!-- Sidebar -->
  <aside class="sidebar">
    <div class="avatar-wrap">
      <div class="avatar">
        <div class="avatar-inner">SK</div>
      </div>
    </div>

    <div>
      <div class="sidebar-name">Seb Kirchner</div>
      <div class="sidebar-handle">Sebkir123</div>
    </div>

    <button class="follow-btn">Follow</button>

    <p class="sidebar-bio">Co-founder & CTO · MambaHR · NYC. Building AI-native enterprise software.</p>

    <div class="sidebar-meta">
      <div class="meta-item">
        <svg viewBox="0 0 16 16" fill="currentColor"><path d="M1.5 14.25c0 .138.112.25.25.25H4v-1.25a.75.75 0 0 1 .75-.75h2.5a.75.75 0 0 1 .75.75v1.25h2.25a.25.25 0 0 0 .25-.25V1.75a.25.25 0 0 0-.25-.25h-8.5a.25.25 0 0 0-.25.25Zm3.75-6a.75.75 0 0 1 .75-.75h1a.75.75 0 0 1 .75.75v1a.75.75 0 0 1-.75.75H6a.75.75 0 0 1-.75-.75Zm.75-3.25a.75.75 0 0 0 0 1.5h1a.75.75 0 0 0 0-1.5Z"/></svg>
        MambaHR
      </div>
      <div class="meta-item">
        <svg viewBox="0 0 16 16" fill="currentColor"><path d="M8 0a8 8 0 1 1 0 16A8 8 0 0 1 8 0ZM1.5 8a6.5 6.5 0 1 0 13 0 6.5 6.5 0 0 0-13 0Z"/></svg>
        New York City
      </div>
      <div class="meta-item">
        <svg viewBox="0 0 16 16" fill="currentColor"><path d="M7.775 3.275a.75.75 0 0 0 1.06 1.06l1.25-1.25a2 2 0 1 1 2.83 2.83l-2.5 2.5a2 2 0 0 1-2.83 0 .75.75 0 0 0-1.06 1.06 3.5 3.5 0 0 0 4.95 0l2.5-2.5a3.5 3.5 0 0 0-4.95-4.95l-1.25 1.25Zm-4.69 9.64a2 2 0 0 1 0-2.83l2.5-2.5a2 2 0 0 1 2.83 0 .75.75 0 0 0 1.06-1.06 3.5 3.5 0 0 0-4.95 0l-2.5 2.5a3.5 3.5 0 0 0 4.95 4.95l1.25-1.25a.75.75 0 0 0-1.06-1.06l-1.25 1.25a2 2 0 0 1-2.83 0Z"/></svg>
        <a href="#" class="meta-link">mambaHR.com</a>
      </div>
    </div>
  </aside>

  <!-- Main -->
  <main class="main">

    <div class="readme-card">
      <div class="readme-header">
        <svg viewBox="0 0 16 16" fill="currentColor"><path d="M0 1.75A.75.75 0 0 1 .75 1h4.253c1.227 0 2.317.59 3 1.501A3.743 3.743 0 0 1 11.006 1h4.245a.75.75 0 0 1 .75.75v10.5a.75.75 0 0 1-.75.75h-4.507a2.25 2.25 0 0 0-1.591.659l-.622.621a.75.75 0 0 1-1.06 0l-.622-.621A2.25 2.25 0 0 0 5.258 13H.75a.75.75 0 0 1-.75-.75Zm7.251 10.324.004-5.073-.003-2.203A2.25 2.25 0 0 0 5.003 2.5H1.5v9h3.757a3.75 3.75 0 0 1 1.994.574ZM8.755 4.75l-.004 7.322a3.752 3.752 0 0 1 1.992-.572H14.5v-9h-3.495a2.25 2.25 0 0 0-2.25 2.25Z"/></svg>
        <span class="readme-header-text">Sebkir123 / README.md</span>
      </div>

      <div class="readme-body md">

        <h1>Seb Kirchner</h1>

        <blockquote>
          <p>Co-founder &amp; CTO · <a href="#">MambaHR</a> · NYC</p>
        </blockquote>

        <p>Building AI-native enterprise software. Previously led data mesh architecture and AI-driven CRM at a <strong>$600B+ Swiss cantonal bank</strong>, serving thousands of users in production.</p>

        <p>CS @ CU Boulder (M.S.) + Euro-FH Hamburg (B.S.) — parallel, both 2026.</p>

        <hr>

        <h3>Currently</h3>

        <p>Rethinking HR software from the interface up. The insight: <strong>HR software has a UI problem disguised as a features problem.</strong></p>

        <p>MambaHR is a chat-first HRIS — multi-tenant Supabase/PostgreSQL with pgvector semantic search, AI agents that surface workforce insights, and a hybrid integration layer across Workday, BambooHR, and Rippling.</p>

        <hr>

        <h3>Focus</h3>

        <div class="focus-grid">
          <div class="focus-row">
            <span class="focus-label">AI Agents</span>
            <span class="focus-desc">Context-preserving, multi-step workflows. RAG + semantic retrieval in production.</span>
          </div>
          <div class="focus-row">
            <span class="focus-label">Multi-tenant SaaS</span>
            <span class="focus-desc">Row-level security, tenant isolation, compliance-first architecture.</span>
          </div>
          <div class="focus-row">
            <span class="focus-label">Data Mesh</span>
            <span class="focus-desc">Domain-oriented data products. Built it. Shipped it. It runs.</span>
          </div>
          <div class="focus-row">
            <span class="focus-label">Enterprise APIs</span>
            <span class="focus-desc">OAuth, webhooks, versioning. The unglamorous stuff that makes it work.</span>
          </div>
        </div>

        <hr>

        <h3>Stack</h3>

        <div class="stack-grid">
          <div class="stack-row"><span class="stack-dot">·</span> TypeScript / Python / SQL</div>
          <div class="stack-row"><span class="stack-dot">·</span> Next.js / React / Flutter</div>
          <div class="stack-row"><span class="stack-dot">·</span> PostgreSQL / pgvector / Redis</div>
          <div class="stack-row"><span class="stack-dot">·</span> Supabase / Docker / Kubernetes</div>
          <div class="stack-row"><span class="stack-dot">·</span> OpenAI / Claude / LangChain / RAG</div>
          <div class="stack-row"><span class="stack-dot">·</span> Finch / Workday / Rippling</div>
        </div>

        <hr>

        <h3>Open to</h3>

        <div class="open-to">
          <span class="tag tag-blue">Technical partnerships</span>
          <span class="tag tag-green">Seed round discussions</span>
          <span class="tag tag-orange">Investor conversations</span>
        </div>

        <div class="bottom-meta" style="margin-top:20px;">
          <em><a href="#">LinkedIn</a> · New York City</em>
        </div>

      </div>
    </div>

    <!-- Contribution graph -->
    <div class="contrib-card">
      <div class="contrib-title">934 contributions in the last year</div>
      <div class="contrib-grid" id="contrib"></div>
    </div>

  </main>
</div>

<script>
  // Generate a realistic-looking contribution graph
  const grid = document.getElementById('contrib');
  const levels = [null, 'l1', 'l2', 'l3', 'l4'];
  const weights = [0.35, 0.25, 0.2, 0.12, 0.08];

  function weightedRandom() {
    const r = Math.random();
    let sum = 0;
    for (let i = 0; i < weights.length; i++) {
      sum += weights[i];
      if (r < sum) return levels[i];
    }
    return null;
  }

  for (let i = 0; i < 52 * 7; i++) {
    const cell = document.createElement('div');
    cell.className = 'contrib-cell';
    const level = weightedRandom();
    if (level) cell.classList.add(level);
    grid.appendChild(cell);
  }
</script>

</body>
</html>
