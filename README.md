<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>ath1t.github.io — Thio CLI Portfolio</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="preconnect" href="https://fonts.googleapis.com" />
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&family=JetBrains+Mono:wght@400;500;600;700&display=swap" rel="stylesheet" />
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.2/css/all.min.css" />
    <script>
      tailwind.config = {
        theme: {
          extend: {
            fontFamily: {
              mono: ['"JetBrains Mono"', 'ui-monospace', 'SFMono-Regular', 'Menlo', 'Monaco', 'Consolas', 'monospace'],
              sans: ['"Inter"', 'system-ui', 'sans-serif']
            },
            colors: {
              'term-bg': '#0b1020',
              'term-header': '#111827',
              'term-chip': '#121a2b',
              'term-chipHover': '#1a2337',
              'term-border': '#2a3447',
              'term-text': '#e6edf3',
              'term-muted': '#8b949e',
              'term-green': '#3fb950',
              'term-cyan': '#58a6ff',
              'term-purple': '#bc8cff',
              'term-red': '#ff7b72',
              'term-yellow': '#d29922'
            }
          }
        }
      };
    </script>
    <style>
      :root {
        color-scheme: dark;
      }
      body {
        font-family: "JetBrains Mono", ui-monospace, SFMono-Regular, monospace;
        background: radial-gradient(circle at top, rgba(63,185,80,0.12), transparent 30%), #0b1020;
      }
      .no-scrollbar::-webkit-scrollbar { display: none; }
      .no-scrollbar { -ms-overflow-style: none; scrollbar-width: none; }
      .terminal-glow {
        box-shadow: 0 0 0 1px rgba(42,52,71,0.8), 0 24px 80px rgba(0,0,0,0.45);
      }
      body.crt-enabled .crt::before {
        content: "";
        position: absolute;
        inset: 0;
        background: linear-gradient(rgba(255,255,255,0.035), rgba(255,255,255,0.015));
        background-size: 100% 4px;
        pointer-events: none;
        z-index: 30;
      }
      #terminal-window { position: relative; }
      input[type="text"] { appearance: none; }
    </style>
  </head>
  <body class="min-h-screen text-term-text antialiased flex flex-col">
    <div class="mx-auto w-full max-w-6xl px-3 py-4 sm:px-4 sm:py-6 lg:px-6 flex-1 flex flex-col">
      <div id="terminal-window" class="crt terminal-glow relative overflow-hidden rounded-xl border border-term-border bg-term-bg/95 flex flex-col flex-1 min-h-[82vh] max-h-[90vh]">
        <!-- Top Window Bar -->
        <header class="flex items-center justify-between border-b border-term-border bg-term-header/80 px-3 py-2.5 sm:px-4 shrink-0">
          <div class="flex items-center space-x-2">
            <span class="w-3 h-3 rounded-full bg-[#ff5f56] inline-block"></span>
            <span class="w-3 h-3 rounded-full bg-[#ffbd2e] inline-block"></span>
            <span class="w-3 h-3 rounded-full bg-[#27c93f] inline-block"></span>
          </div>

          <div class="flex min-w-0 items-center space-x-2 text-xs sm:text-sm text-term-muted font-medium truncate px-2">
            <i class="fa-solid fa-terminal text-term-green text-xs"></i>
            <span class="truncate">thio@ath1t.github.io: ~ (zsh)</span>
          </div>

          <div class="flex items-center space-x-2">
            <span id="gh-sync-badge" title="GitHub API sync status" class="hidden sm:inline-flex items-center gap-1.5 text-[11px] bg-term-chip text-term-muted border border-term-border px-2 py-0.5 rounded-md">
              <i class="fa-brands fa-github text-term-text"></i>
              <span id="gh-sync-text">syncing...</span>
            </span>
            <span id="toast-badge" class="hidden text-[11px] bg-term-green/20 text-term-green border border-term-green/40 px-2 py-0.5 rounded-md transition-opacity">
              Copied!
            </span>
            <button id="crt-toggle" type="button" aria-pressed="false" title="Toggle Retro CRT Scanlines"
              class="flex items-center space-x-1.5 text-xs px-2.5 py-1 rounded-md border border-term-border bg-term-chip hover:bg-term-chipHover text-term-muted hover:text-term-text transition cursor-pointer">
              <span id="crt-indicator" class="w-2 h-2 rounded-full bg-term-muted transition-colors"></span>
              <span class="font-medium">CRT</span>
            </button>
          </div>
        </header>

        <!-- Quick Command Bar -->
        <nav aria-label="Quick commands" class="bg-term-header/70 border-b border-term-border px-3 py-2 flex items-center gap-1.5 overflow-x-auto no-scrollbar shrink-0 z-20 select-none">
          <span class="text-[11px] text-term-muted mr-1 shrink-0 hidden sm:inline">Quick:</span>
          <button type="button" data-cmd="help" class="quick-chip shrink-0 px-2.5 py-1 rounded-md text-xs bg-term-chip hover:bg-term-chipHover text-term-cyan border border-term-border/80 transition active:scale-95">help</button>
          <button type="button" data-cmd="github" class="quick-chip shrink-0 px-2.5 py-1 rounded-md text-xs bg-term-chip hover:bg-term-chipHover text-term-green border border-term-border/80 transition active:scale-95">github</button>
          <button type="button" data-cmd="repos" class="quick-chip shrink-0 px-2.5 py-1 rounded-md text-xs bg-term-chip hover:bg-term-chipHover text-term-cyan border border-term-border/80 transition active:scale-95">repos</button>
          <button type="button" data-cmd="projects" class="quick-chip shrink-0 px-2.5 py-1 rounded-md text-xs bg-term-chip hover:bg-term-chipHover text-term-green border border-term-border/80 transition active:scale-95">projects</button>
          <button type="button" data-cmd="cat about.md" class="quick-chip shrink-0 px-2.5 py-1 rounded-md text-xs bg-term-chip hover:bg-term-chipHover text-term-purple border border-term-border/80 transition active:scale-95">cat about.md</button>
          <button type="button" data-cmd="neofetch" class="quick-chip shrink-0 px-2.5 py-1 rounded-md text-xs bg-term-chip hover:bg-term-chipHover text-term-yellow border border-term-border/80 transition active:scale-95">neofetch</button>
          <button type="button" data-cmd="contact" class="quick-chip shrink-0 px-2.5 py-1 rounded-md text-xs bg-term-chip hover:bg-term-chipHover text-term-cyan border border-term-border/80 transition active:scale-95">contact</button>
          <button type="button" data-cmd="clear" class="quick-chip shrink-0 px-2.5 py-1 rounded-md text-xs bg-term-chip hover:bg-term-chipHover text-term-red border border-term-border/80 transition active:scale-95">clear</button>
        </nav>

        <!-- Scrollable Terminal Output -->
        <section id="terminal-body" class="flex-1 overflow-y-auto p-3.5 sm:p-5 text-xs sm:text-sm leading-relaxed space-y-3 cursor-text select-text" tabindex="-1">
          <div id="output-container" class="space-y-3.5"></div>

          <div id="input-row" class="flex flex-wrap items-center pt-0.5">
            <span class="prompt-label shrink-0 mr-2 font-semibold select-none">
              <span class="text-term-green">thio</span><span class="text-term-muted">@</span><span class="text-term-cyan">ath1t.github.io</span><span class="text-term-muted">:</span><span class="text-term-purple">~</span><span class="text-term-text">$</span>
            </span>

            <div class="relative flex-1 min-w-[160px]">
              <input id="cli-input" type="text" autocomplete="off" autocapitalize="off" spellcheck="false" placeholder="Type 'help' or click a command..." class="w-full bg-transparent text-term-text caret-term-green outline-none placeholder-term-muted/60" aria-label="Terminal command input" />
            </div>
          </div>

          <div id="autocomplete-hint" class="hidden text-[11px] text-term-muted"></div>
        </section>

        <!-- Mobile Touch Helper Keys -->
        <footer class="sm:hidden border-t border-term-border bg-term-header/90 px-3 py-1.5 flex items-center justify-between text-xs text-term-muted shrink-0">
          <span>Touch keys:</span>
          <div class="flex items-center gap-2">
            <button id="mobile-tab-btn" type="button" class="px-2.5 py-1 rounded bg-term-chip border border-term-border text-term-text">Tab</button>
            <button id="mobile-up-btn" type="button" class="px-2.5 py-1 rounded bg-term-chip border border-term-border text-term-text">↑</button>
            <button id="mobile-down-btn" type="button" class="px-2.5 py-1 rounded bg-term-chip border border-term-border text-term-text">↓</button>
          </div>
        </footer>
      </div>
    </div>

    <script>
      (() => {
        const terminalBody = document.getElementById('terminal-body');
        const outputContainer = document.getElementById('output-container');
        const cliInput = document.getElementById('cli-input');
        const autocompleteHint = document.getElementById('autocomplete-hint');
        const toastBadge = document.getElementById('toast-badge');
        const ghSyncText = document.getElementById('gh-sync-text');
        const crtToggle = document.getElementById('crt-toggle');
        const crtIndicator = document.getElementById('crt-indicator');

        if (!terminalBody || !outputContainer || !cliInput) return;

        const shellState = {
          history: [],
          historyIndex: -1,
          cwd: '/home/thio',
          user: 'thio',
          host: 'ath1t.github.io'
        };

        const USER_DATA = {
          name: 'Thio',
          username: 'ath1t',
          host: 'ath1t.github.io',
          role: 'Self-taught programmer building Python CLI tools, automation, and FFmpeg workflows.',
          githubUrl: 'https://github.com/ath1t',
          mysubUrl: 'https://ath1t-mysub.vercel.app',
          location: 'Yangon, Myanmar (UTC+6:30)'
        };

        const FALLBACK_GITHUB_PROFILE = {
          login: 'ath1t',
          name: 'Thio',
          avatar_url: 'https://avatars.githubusercontent.com/u/100000000?v=4',
          html_url: 'https://github.com/ath1t',
          bio: 'Self-taught programmer building Python CLI tools, automated proxy/data pipelines, and FFmpeg workflows.',
          public_repos: 6,
          followers: 12,
          following: 18,
          created_at: '2022-04-10T00:00:00Z',
          location: 'Yangon, Myanmar',
          blog: 'https://ath1t.github.io',
          _source: 'fallback'
        };

        const FALLBACK_GITHUB_REPOS = [
          {
            name: 'mysub',
            full_name: 'ath1t/mysub',
            html_url: 'https://github.com/ath1t/mysub',
            homepage: 'https://ath1t-mysub.vercel.app',
            description: 'Automated proxy and subscription node aggregator powered by scheduled Python workers and GitHub Actions.',
            language: 'Python',
            stargazers_count: 14,
            forks_count: 3,
            updated_at: '2026-11-10T10:00:00Z'
          },
          {
            name: 'ath1t.github.io',
            full_name: 'ath1t/ath1t.github.io',
            html_url: 'https://github.com/ath1t/ath1t.github.io',
            homepage: 'https://ath1t.github.io',
            description: 'Interactive browser-based terminal emulator and CLI portfolio with live GitHub API integration.',
            language: 'JavaScript',
            stargazers_count: 5,
            forks_count: 1,
            updated_at: '2026-11-17T08:00:00Z'
          },
          {
            name: 'ffmpeg-sub-pipeline',
            full_name: 'ath1t/ffmpeg-sub-pipeline',
            html_url: 'https://github.com/ath1t',
            homepage: '',
            description: 'CLI toolkit for batch FFmpeg encoding, loudness normalization, and automated .srt/.ass subtitle styling.',
            language: 'Python',
            stargazers_count: 8,
            forks_count: 2,
            updated_at: '2026-10-24T14:20:00Z'
          }
        ];

        const FALLBACK_GITHUB_EVENTS = [
          {
            type: 'PushEvent',
            repo: { name: 'ath1t/mysub' },
            created_at: '2026-11-16T18:30:00Z',
            payload: { commits: [{ message: 'chore(sync): update aggregated node health metrics' }] }
          },
          {
            type: 'PushEvent',
            repo: { name: 'ath1t/ath1t.github.io' },
            created_at: '2026-11-17T08:15:00Z',
            payload: { commits: [{ message: 'feat(cli): add live GitHub REST API commands' }] }
          }
        ];

        const ghStore = {
          profile: { ...FALLBACK_GITHUB_PROFILE },
          repos: [...FALLBACK_GITHUB_REPOS],
          events: [...FALLBACK_GITHUB_EVENTS],
          status: 'initializing',
          lastFetched: null
        };

        const CACHE_KEY = 'ath1t_gh_cache_v1';
        const CACHE_TTL_MS = 10 * 60 * 1000;

        function escapeHTML(value) {
          if (value === null || value === undefined) return '';
          return String(value).replace(/[&<>"']/g, (match) => ({
            '&': '&amp;',
            '<': '&lt;',
            '>': '&gt;',
            '"': '&quot;',
            "'": '&#39;'
          }[match]));
        }

        function safeSessionStorageGet() {
          try {
            const raw = sessionStorage.getItem(CACHE_KEY);
            return raw ? JSON.parse(raw) : null;
          } catch {
            return null;
          }
        }

        function safeSessionStorageSet(payload) {
          try {
            sessionStorage.setItem(CACHE_KEY, JSON.stringify(payload));
          } catch {
            // Ignore storage quota/privacy issues.
          }
        }

        function showToast(message) {
          if (!toastBadge) return;
          toastBadge.textContent = message;
          toastBadge.classList.remove('hidden');
          clearTimeout(window._toastTimer);
          window._toastTimer = setTimeout(() => toastBadge.classList.add('hidden'), 2000);
        }

        window.copyToClipboard = function (text, label) {
          const tempInput = document.createElement('textarea');
          tempInput.value = text;
          tempInput.style.position = 'fixed';
          tempInput.style.opacity = '0';
          document.body.appendChild(tempInput);
          tempInput.select();
          try {
            document.execCommand('copy');
            showToast(label ? `Copied ${label}` : 'Copied!');
          } catch {
            showToast('Copy failed');
          }
          document.body.removeChild(tempInput);
        };

        function updateSyncBadge(statusText, isLive) {
          if (!ghSyncText) return;
          ghSyncText.textContent = statusText;
          const badge = document.getElementById('gh-sync-badge');
          if (!badge) return;
          badge.classList.remove('text-term-muted', 'text-term-green', 'text-term-yellow');
          badge.classList.add(isLive ? 'text-term-green' : 'text-term-yellow');
        }

        function formatRelativeDate(isoString) {
          if (!isoString) return 'recently';
          const date = new Date(isoString);
          if (Number.isNaN(date.getTime())) return 'recently';
          const diffSec = Math.floor((Date.now() - date.getTime()) / 1000);
          if (diffSec < 60) return 'just now';
          const diffMin = Math.floor(diffSec / 60);
          if (diffMin < 60) return `${diffMin}m ago`;
          const diffHr = Math.floor(diffMin / 60);
          if (diffHr < 24) return `${diffHr}h ago`;
          const diffDays = Math.floor(diffHr / 24);
          if (diffDays < 30) return `${diffDays}d ago`;
          return date.toLocaleDateString('en-US', { month: 'short', day: 'numeric', year: 'numeric' });
        }

        function getLangColor(lang) {
          const colors = {
            Python: '#3572A5',
            JavaScript: '#f1e05a',
            TypeScript: '#3178c6',
            HTML: '#e34c26',
            CSS: '#563d7c',
            Shell: '#89e051',
            Go: '#00ADD8',
            Rust: '#dea584'
          };
          return colors[lang] || '#8b949e';
        }

        async function hydrateGitHubData(forceRefresh = false) {
          try {
            if (!forceRefresh) {
              const cached = safeSessionStorageGet();
              if (cached && Date.now() - cached.timestamp < CACHE_TTL_MS) {
                ghStore.profile = cached.profile || ghStore.profile;
                ghStore.repos = cached.repos || ghStore.repos;
                ghStore.events = cached.events || ghStore.events;
                ghStore.status = 'cached';
                ghStore.lastFetched = new Date(cached.timestamp).toLocaleTimeString();
                updateSyncBadge('gh: cached', true);
                return ghStore;
              }
            }

            updateSyncBadge('syncing...', false);
            const controller = new AbortController();
            const timeout = setTimeout(() => controller.abort(), 8000);
            const headers = { Accept: 'application/vnd.github.v3+json' };

            const [profileRes, reposRes, eventsRes] = await Promise.all([
              fetch('https://api.github.com/users/ath1t', { headers, signal: controller.signal }),
              fetch('https://api.github.com/users/ath1t/repos?sort=updated&per_page=10', { headers, signal: controller.signal }),
              fetch('https://api.github.com/users/ath1t/events/public?per_page=5', { headers, signal: controller.signal })
            ]);
            clearTimeout(timeout);

            if (profileRes.status === 403 || profileRes.status === 429) {
              ghStore.status = 'rate-limited/fallback';
              updateSyncBadge('gh: rate limited', false);
              return ghStore;
            }

            if (!profileRes.ok) throw new Error(`GitHub API HTTP ${profileRes.status}`);

            const profileJson = await profileRes.json();
            const reposJson = reposRes.ok ? await reposRes.json() : FALLBACK_GITHUB_REPOS;
            const eventsJson = eventsRes.ok ? await eventsRes.json() : FALLBACK_GITHUB_EVENTS;

            ghStore.profile = { ...FALLBACK_GITHUB_PROFILE, ...profileJson, _source: 'live' };
            ghStore.repos = Array.isArray(reposJson) && reposJson.length ? reposJson : FALLBACK_GITHUB_REPOS;
            ghStore.events = Array.isArray(eventsJson) && eventsJson.length ? eventsJson : FALLBACK_GITHUB_EVENTS;
            ghStore.status = 'live';
            ghStore.lastFetched = new Date().toLocaleTimeString();

            safeSessionStorageSet({
              timestamp: Date.now(),
              profile: ghStore.profile,
              repos: ghStore.repos,
              events: ghStore.events
            });

            updateSyncBadge(`gh: ${ghStore.profile.public_repos} repos`, true);
            return ghStore;
          } catch {
            ghStore.status = 'offline/fallback';
            updateSyncBadge('gh: cached/offline', false);
            return ghStore;
          }
        }

        function renderGitHubProfileCard() {
          const p = ghStore.profile;
          const joinedDate = p.created_at
            ? new Date(p.created_at).toLocaleDateString('en-US', { month: 'short', year: 'numeric' })
            : '2022';
          const statusPill = ghStore.status === 'live' || ghStore.status === 'cached'
            ? `<span class="text-[11px] px-2 py-0.5 rounded bg-term-green/15 text-term-green border border-term-green/40">API: ${escapeHTML(ghStore.status)}</span>`
            : `<span class="text-[11px] px-2 py-0.5 rounded bg-term-yellow/15 text-term-yellow border border-term-yellow/40">API: fallback</span>`;

          return `
            <div class="border border-term-border/90 bg-term-header/45 rounded-lg p-3.5 sm:p-4 max-w-3xl space-y-3">
              <div class="flex flex-wrap items-center justify-between gap-2 border-b border-term-border/60 pb-2.5">
                <div class="flex items-center gap-3">
                  <img src="${escapeHTML(p.avatar_url)}" alt="${escapeHTML(p.login)} avatar" onerror="this.onerror=null;this.src='https://placehold.co/64x64/161b22/3fb950?text=AT';" class="w-11 h-11 rounded-full border border-term-green/60 bg-term-bg object-cover shrink-0" />
                  <div>
                    <div class="flex items-center gap-2">
                      <span class="text-term-text font-bold text-sm sm:text-base">${escapeHTML(p.name || 'Thio')}</span>
                      <a href="${escapeHTML(p.html_url)}" target="_blank" rel="noopener noreferrer" class="text-term-cyan hover:underline text-xs sm:text-sm font-medium">@${escapeHTML(p.login)}</a>
                    </div>
                    <div class="text-xs text-term-muted">Joined GitHub ${joinedDate} • ${escapeHTML(p.location || USER_DATA.location)}</div>
                  </div>
                </div>
                ${statusPill}
              </div>
              <p class="text-xs sm:text-sm text-term-text">${escapeHTML(p.bio || USER_DATA.role)}</p>
              <div class="grid grid-cols-3 gap-2 pt-0.5">
                <div class="bg-term-bg/80 border border-term-border/70 rounded-md p-2 text-center">
                  <div class="text-term-green font-bold text-sm sm:text-base">${Number(p.public_repos) || 0}</div>
                  <div class="text-[11px] text-term-muted">Public Repos</div>
                </div>
                <div class="bg-term-bg/80 border border-term-border/70 rounded-md p-2 text-center">
                  <div class="text-term-cyan font-bold text-sm sm:text-base">${Number(p.followers) || 0}</div>
                  <div class="text-[11px] text-term-muted">Followers</div>
                </div>
                <div class="bg-term-bg/80 border border-term-border/70 rounded-md p-2 text-center">
                  <div class="text-term-purple font-bold text-sm sm:text-base">${Number(p.following) || 0}</div>
                  <div class="text-[11px] text-term-muted">Following</div>
                </div>
              </div>
              <div class="flex flex-wrap items-center justify-between gap-2 pt-1 text-xs border-t border-term-border/50">
                <div class="flex flex-wrap gap-3">
                  <a href="${escapeHTML(p.html_url)}" target="_blank" rel="noopener noreferrer" class="text-term-cyan hover:underline font-medium"><i class="fa-brands fa-github mr-1"></i>github.com/${escapeHTML(p.login)}</a>
                  <button type="button" onclick="runQuickCmd('github repos')" class="text-term-green hover:underline">→ list repos</button>
                  <button type="button" onclick="runQuickCmd('github activity')" class="text-term-yellow hover:underline">→ recent activity</button>
                </div>
                <button type="button" onclick="runQuickCmd('github refresh')" class="text-[11px] text-term-muted hover:text-term-text underline">Refresh API</button>
              </div>
            </div>
          `;
        }

        function renderGitHubReposList() {
          const repos = ghStore.repos.slice(0, 8);
          const markup = repos.map((repo) => {
            const lang = repo.language || 'Code';
            const color = getLangColor(lang);
            const liveBadge = repo.homepage
              ? `<a href="${escapeHTML(repo.homepage)}" target="_blank" rel="noopener noreferrer" class="inline-flex items-center gap-1 text-[11px] px-2 py-0.5 rounded bg-term-green/15 text-term-green border border-term-green/40"><i class="fa-solid fa-arrow-up-right-from-square text-[9px]"></i> Live</a>`
              : '';
            return `
              <div class="border border-term-border/85 bg-term-header/40 hover:border-term-cyan/60 transition rounded-lg p-3 space-y-1.5">
                <div class="flex flex-wrap items-center justify-between gap-2">
                  <a href="${escapeHTML(repo.html_url)}" target="_blank" rel="noopener noreferrer" class="text-term-cyan hover:underline font-bold text-xs sm:text-sm flex items-center gap-1.5">
                    <i class="fa-regular fa-folder-open text-term-green"></i>
                    <span>${escapeHTML(repo.full_name || `ath1t/${repo.name}`)}</span>
                  </a>
                  <div class="flex items-center gap-2">
                    ${liveBadge}
                    <span class="text-[11px] text-term-yellow"><i class="fa-solid fa-star text-[10px] mr-0.5"></i>${Number(repo.stargazers_count) || 0}</span>
                  </div>
                </div>
                <p class="text-xs text-term-text">${escapeHTML(repo.description || 'Repository by @ath1t')}</p>
                <div class="flex flex-wrap items-center gap-x-4 gap-y-1 text-[11px] text-term-muted pt-0.5">
                  <span class="inline-flex items-center gap-1.5">
                    <span class="w-2.5 h-2.5 rounded-full inline-block" style="background-color: ${color};"></span>
                    <span>${escapeHTML(lang)}</span>
                  </span>
                  <span><i class="fa-solid fa-code-fork mr-1"></i>${Number(repo.forks_count) || 0}</span>
                  <span>Updated ${formatRelativeDate(repo.updated_at)}</span>
                </div>
              </div>
            `;
          }).join('');

          return `
            <div class="space-y-2.5 max-w-3xl">
              <div class="flex items-center justify-between text-xs text-term-muted">
                <span>Public repositories for <span class="text-term-cyan font-semibold">@ath1t</span> (sorted by recently updated):</span>
                <span>${repos.length} shown</span>
              </div>
              <div class="grid grid-cols-1 gap-2.5">${markup}</div>
            </div>
          `;
        }

        function renderGitHubActivity() {
          const events = ghStore.events.slice(0, 5);
          if (!events.length) {
            return '<div class="text-xs text-term-muted">No recent public GitHub events found for @ath1t.</div>';
          }

          const markup = events.map((ev) => {
            const repoName = ev.repo && ev.repo.name ? ev.repo.name : 'ath1t/repo';
            const timeRel = formatRelativeDate(ev.created_at);
            let actionSummary = ev.type ? ev.type.replace('Event', '') : 'Activity';
            let detailMsg = '';

            if (ev.type === 'PushEvent' && ev.payload && Array.isArray(ev.payload.commits) && ev.payload.commits.length > 0) {
              actionSummary = `Pushed ${ev.payload.commits.length} commit(s) to`;
              detailMsg = ev.payload.commits[0].message || '';
            } else if (ev.type === 'CreateEvent') {
              actionSummary = `Created ${(ev.payload && ev.payload.ref_type) || 'repository'} in`;
            } else if (ev.type === 'WatchEvent') {
              actionSummary = 'Starred';
            }

            return `
              <div class="flex flex-col sm:flex-row sm:items-center justify-between gap-1 py-2 border-b border-term-border/50 last:border-b-0 text-xs">
                <div class="space-y-0.5">
                  <div>
                    <span class="text-term-green font-semibold">●</span>
                    <span class="text-term-text ml-1">${escapeHTML(actionSummary)}</span>
                    <a href="https://github.com/${escapeHTML(repoName)}" target="_blank" rel="noopener noreferrer" class="text-term-cyan hover:underline font-medium ml-1">${escapeHTML(repoName)}</a>
                  </div>
                  ${detailMsg ? `<div class="pl-4 text-term-muted font-mono truncate max-w-xl">↳ "${escapeHTML(detailMsg)}"</div>` : ''}
                </div>
                <span class="text-[11px] text-term-muted shrink-0 pl-4 sm:pl-0">${timeRel}</span>
              </div>
            `;
          }).join('');

          return `
            <div class="border border-term-border/80 bg-term-header/40 rounded-lg p-3.5 max-w-3xl space-y-1">
              <div class="text-xs font-semibold text-term-purple pb-1.5 border-b border-term-border/60 flex items-center justify-between">
                <span><i class="fa-solid fa-wave-square mr-1.5"></i>Recent Public GitHub Activity (@ath1t)</span>
                <span class="text-[11px] font-normal text-term-muted">events/public</span>
              </div>
              <div>${markup}</div>
            </div>
          `;
        }

        const FEATURED_PROJECTS = [
          {
            name: 'MySub Proxy Aggregator (ath1t/mysub)',
            tag: 'Python • GitHub Actions • Vercel',
            desc: 'Automated proxy and subscription node aggregator that fetches, deduplicates, latency-tests, and publishes clean endpoints on a scheduled CI/CD cycle.',
            repo: 'https://github.com/ath1t/mysub',
            live: 'https://ath1t-mysub.vercel.app',
            highlight: 'Zero-server architecture powered by automated Python workers.'
          },
          {
            name: 'FFmpeg & Subtitle Automation Suite',
            tag: 'Python • FFmpeg • Media Pipeline',
            desc: 'CLI toolkit for video production: batch transcoding, loudness normalization, subtitle timing, and style automation.',
            repo: 'https://github.com/ath1t',
            live: '',
            highlight: 'Cuts multi-hour rendering and subtitling prep down to one command.'
          },
          {
            name: 'CLI Developer Utilities & Scrapers',
            tag: 'Python • Bash • Rich TUI',
            desc: 'Collection of terminal utilities for JSON/YAML extraction, archive management, and system diagnostics.',
            repo: 'https://github.com/ath1t',
            live: '',
            highlight: 'Built for speed, portability, and minimal dependencies.'
          }
        ];

        const VIRTUAL_FILES = {
          'about.md': () => `
            <div class="border border-term-border/80 bg-term-header/40 rounded-lg p-3.5 sm:p-4 space-y-2.5 max-w-3xl">
              <div class="flex items-center justify-between border-b border-term-border/60 pb-2">
                <span class="text-term-purple font-bold"># about.md</span>
                <span class="text-[11px] text-term-muted">Markdown • 1.3 KB</span>
              </div>
              <p class="text-term-text">Hey! I'm <span class="text-term-green font-semibold">${escapeHTML(ghStore.profile.name || 'Thio')}</span> (<a href="https://github.com/ath1t" target="_blank" rel="noopener noreferrer" class="text-term-cyan underline">@ath1t</a>), a self-taught programmer focused on building practical tools that remove repetitive work.</p>
              <p class="text-term-text">My work sits at the intersection of <span class="text-term-yellow">Python &amp; CLI automation</span>, resilient network/proxy tooling, and video production pipelines. I enjoy turning multi-step manual tasks into clean terminal commands.</p>
              <div class="pt-1 text-xs text-term-muted flex flex-wrap gap-x-4 gap-y-1">
                <span><i class="fa-solid fa-terminal text-term-green mr-1.5"></i>Philosophy: automate everything twice-done</span>
                <span><i class="fa-brands fa-github text-term-cyan mr-1.5"></i>Public repos: ${ghStore.profile.public_repos}</span>
              </div>
            </div>
          `,
          'readme.md': () => `
            <div class="border border-term-border/80 bg-term-header/40 rounded-lg p-4 sm:p-5 space-y-3 max-w-3xl overflow-x-auto text-xs sm:text-sm">
              <div class="flex items-center justify-between border-b border-term-border/60 pb-2.5">
                <span class="text-term-green font-bold text-sm sm:text-base"># README.md — ath1t/ath1t.github.io</span>
                <span class="text-[11px] text-term-muted">Markdown • Live CLI Portfolio</span>
              </div>
              
              <div class="space-y-2 text-term-text">
                <div class="flex flex-wrap gap-2 items-center py-1">
                  <span class="px-2 py-0.5 rounded bg-term-green/20 text-term-green text-[11px] border border-term-green/40">Status: Active</span>
                  <span class="px-2 py-0.5 rounded bg-term-cyan/20 text-term-cyan text-[11px] border border-term-cyan/40">GitHub Pages</span>
                  <span class="px-2 py-0.5 rounded bg-term-purple/20 text-term-purple text-[11px] border border-term-purple/40">Zero Backend</span>
                </div>
                
                <h3 class="text-term-cyan font-bold text-sm pt-1">🚀 Interactive Browser-Based Terminal Portfolio</h3>
                <p class="text-term-muted">Welcome to the source code for my personal portfolio hosted at <a href="https://ath1t.github.io" target="_blank" rel="noopener noreferrer" class="text-term-cyan underline">ath1t.github.io</a>. Built entirely with vanilla JavaScript, Tailwind CSS, and live GitHub REST API integration.</p>
                
                <h3 class="text-term-yellow font-bold text-sm pt-2">✨ Core Features</h3>
                <ul class="list-disc pl-5 space-y-1 text-term-muted">
                  <li><strong class="text-term-text">Zsh Terminal Emulator:</strong> Fully interactive CLI supporting command history (<kbd class="bg-term-chip px-1 rounded">↑</kbd>/<kbd class="bg-term-chip px-1 rounded">↓</kbd>), Tab auto-completion, and custom command flags.</li>
                  <li><strong class="text-term-text">Live GitHub API Sync:</strong> Fetches profile metrics, public repositories, and commit event streams dynamically with <code class="text-term-cyan">sessionStorage</code> caching.</li>
                  <li><strong class="text-term-text">Virtual File System:</strong> Inspect files with <button type="button" onclick="runQuickCmd('cat about.md')" class="text-term-purple underline">cat about.md</button>, <button type="button" onclick="runQuickCmd('cat github.json')" class="text-term-cyan underline">cat github.json</button>, and <button type="button" onclick="runQuickCmd('cat skills.json')" class="text-term-yellow underline">cat skills.json</button>.</li>
                  <li><strong class="text-term-text">Responsive &amp; CRT Mode:</strong> Mobile-friendly touch helper keys alongside an optional retro CRT scanline overlay toggle.</li>
                </ul>

                <h3 class="text-term-purple font-bold text-sm pt-2">💻 Quick Start Commands</h3>
                <div class="bg-term-bg/90 border border-term-border rounded p-2.5 font-mono text-xs text-term-green space-y-1">
                  <div>$ help</div>
                  <div>$ github profile</div>
                  <div>$ repos</div>
                  <div>$ projects</div>
                  <div>$ neofetch</div>
                </div>
              </div>
            </div>
          `,
          'skills.json': () => `
            <div class="border border-term-border/80 bg-term-header/40 rounded-lg p-3.5 sm:p-4 max-w-3xl overflow-x-auto">
              <div class="flex items-center justify-between border-b border-term-border/60 pb-2 mb-2">
                <span class="text-term-yellow font-bold">skills.json</span>
                <span class="text-[11px] text-term-muted">JSON • Validated</span>
              </div>
              <pre class="text-xs sm:text-sm leading-relaxed text-term-text"><code>{
  "languages": ["Python", "Bash / Zsh", "JavaScript (ES6+)", "HTML / CSS"],
  "automation_and_cli": ["AsyncIO & aiohttp", "GitHub Actions", "Web scraping & proxy aggregation", "argparse / Typer / Rich TUI"],
  "video_and_media": ["FFmpeg batch encoding", "SRT / ASS subtitle workflows", "yt-dlp media automation", "Audio/video mastering"],
  "environment": {"os": "Linux / Windows WSL2", "editor": "VS Code / Neovim", "version_control": "Git & GitHub (@ath1t)"}
}</code></pre>
            </div>
          `,
          'github.json': () => {
            const topRepoNames = ghStore.repos.slice(0, 5).map((r) => `"${escapeHTML(r.name)}"`).join(', ');
            const joinedYear = ghStore.profile.created_at ? new Date(ghStore.profile.created_at).getFullYear() : 2022;
            return `
              <div class="border border-term-border/80 bg-term-header/40 rounded-lg p-3.5 sm:p-4 max-w-3xl overflow-x-auto">
                <div class="flex items-center justify-between border-b border-term-border/60 pb-2 mb-2">
                  <span class="text-term-cyan font-bold">github.json</span>
                  <span class="text-[11px] text-term-muted">Source: api.github.com/users/ath1t (${escapeHTML(ghStore.status)})</span>
                </div>
                <pre class="text-xs sm:text-sm leading-relaxed text-term-text"><code>{
  "login": "${escapeHTML(ghStore.profile.login)}",
  "name": "${escapeHTML(ghStore.profile.name || 'Thio')}",
  "html_url": "${escapeHTML(ghStore.profile.html_url)}",
  "public_repos": ${Number(ghStore.profile.public_repos) || 0},
  "followers": ${Number(ghStore.profile.followers) || 0},
  "following": ${Number(ghStore.profile.following) || 0},
  "member_since": ${joinedYear},
  "top_repositories": [${topRepoNames}]
}</code></pre>
              </div>
            `;
          }
        };

        function scrollToBottom() {
          requestAnimationFrame(() => {
            terminalBody.scrollTo({
              top: terminalBody.scrollHeight,
              behavior: 'smooth'
            });
          });
        }

        function appendOutput(rawCommand, htmlContent, showPrompt = true) {
          const wrapper = document.createElement('div');
          wrapper.className = 'output-entry space-y-1.5';

          if (showPrompt) {
            const header = document.createElement('div');
            header.className = 'flex items-center flex-wrap gap-2';
            header.innerHTML = `
              <span class="font-semibold select-none">
                <span class="text-term-green">thio</span><span class="text-term-muted">@</span><span class="text-term-cyan">ath1t.github.io</span><span class="text-term-muted">:</span><span class="text-term-purple">~</span><span class="text-term-text">$</span>
              </span>
              <span class="text-term-text font-medium break-all">${escapeHTML(rawCommand)}</span>
            `;
            wrapper.appendChild(header);
          }

          if (htmlContent) {
            const bodyDiv = document.createElement('div');
            bodyDiv.className = 'pl-0 sm:pl-1 text-term-text';
            bodyDiv.innerHTML = htmlContent;
            wrapper.appendChild(bodyDiv);
          }

          outputContainer.appendChild(wrapper);
          scrollToBottom();
        }

        const COMMANDS = {
          help: () => `
            <div class="border border-term-border/80 bg-term-header/30 rounded-lg p-3.5 max-w-3xl space-y-2.5">
              <div class="text-term-cyan font-semibold">Available Terminal Commands:</div>
              <div class="grid grid-cols-1 sm:grid-cols-2 gap-x-6 gap-y-1.5 text-xs sm:text-sm">
                <div><button type="button" onclick="runQuickCmd('github')" class="text-term-green hover:underline font-semibold">github</button> <span class="text-term-muted">(or gh) — Live GitHub profile card</span></div>
                <div><button type="button" onclick="runQuickCmd('repos')" class="text-term-green hover:underline font-semibold">repos</button> <span class="text-term-muted">— Live @ath1t public repositories</span></div>
                <div><button type="button" onclick="runQuickCmd('activity')" class="text-term-green hover:underline font-semibold">activity</button> <span class="text-term-muted">— Recent GitHub commit feed</span></div>
                <div><button type="button" onclick="runQuickCmd('projects')" class="text-term-green hover:underline font-semibold">projects</button> <span class="text-term-muted">— Featured tools &amp; live apps</span></div>
                <div><button type="button" onclick="runQuickCmd('whoami')" class="text-term-green hover:underline font-semibold">whoami</button> <span class="text-term-muted">— Developer identity &amp; summary</span></div>
                <div><button type="button" onclick="runQuickCmd('neofetch')" class="text-term-green hover:underline font-semibold">neofetch</button> <span class="text-term-muted">— ASCII art &amp; live GitHub stats</span></div>
                <div><button type="button" onclick="runQuickCmd('ls -la')" class="text-term-green hover:underline font-semibold">ls</button> <span class="text-term-muted">— List directory files (-l, -a)</span></div>
                <div><button type="button" onclick="runQuickCmd('cat readme.md')" class="text-term-green hover:underline font-semibold">cat readme.md</button> <span class="text-term-muted">— Project documentation</span></div>
                <div><button type="button" onclick="runQuickCmd('cat about.md')" class="text-term-green hover:underline font-semibold">cat about.md</button> <span class="text-term-muted">— Read developer bio</span></div>
                <div><button type="button" onclick="runQuickCmd('cat skills.json')" class="text-term-green hover:underline font-semibold">cat skills.json</button> <span class="text-term-muted">— View technical stack</span></div>
                <div><button type="button" onclick="runQuickCmd('contact')" class="text-term-green hover:underline font-semibold">contact</button> <span class="text-term-muted">— GitHub, MySub &amp; links</span></div>
                <div><button type="button" onclick="runQuickCmd('clear')" class="text-term-green hover:underline font-semibold">clear</button> <span class="text-term-muted">— Clear terminal screen</span></div>
              </div>
              <div class="pt-1 border-t border-term-border/50 text-xs text-term-muted">
                Subcommands: <code class="text-term-cyan">github profile</code>, <code class="text-term-cyan">github repos</code>, <code class="text-term-cyan">github activity</code>, <code class="text-term-cyan">github refresh</code>.
              </div>
            </div>
          `,

          github: (args) => {
            const sub = (args[0] || 'profile').toLowerCase();
            if (sub === 'profile' || sub === 'info') return renderGitHubProfileCard();
            if (sub === 'repos' || sub === 'repo' || sub === 'ls') return renderGitHubReposList();
            if (sub === 'activity' || sub === 'events' || sub === 'log') return renderGitHubActivity();
            if (sub === 'refresh' || sub === 'sync') {
              hydrateGitHubData(true).then(() => {
                appendOutput('github refresh [async]', `<div class="text-term-green text-xs">✓ Synced latest GitHub metadata for <span class="font-semibold">@ath1t</span> (${ghStore.profile.public_repos} public repos).</div>`, false);
              });
              return `<div class="text-term-muted text-xs">Fetching fresh profile, repositories, and events from <span class="text-term-cyan">api.github.com/users/ath1t</span>...</div>`;
            }
            return `<span class="text-term-red">github: unknown subcommand '${escapeHTML(sub)}'</span><br><span class="text-term-muted text-xs">Usage: github [profile | repos | activity | refresh]</span>`;
          },

          gh: (args) => COMMANDS.github(args),
          repos: () => renderGitHubReposList(),
          activity: () => renderGitHubActivity(),

          whoami: () => `
            <div class="space-y-1">
              <div class="text-term-green font-bold text-sm sm:text-base">${escapeHTML(ghStore.profile.name || 'Thio')} (@${escapeHTML(ghStore.profile.login)})</div>
              <div class="text-term-text">${escapeHTML(ghStore.profile.bio || USER_DATA.role)}</div>
              <div class="text-xs text-term-muted">
                GitHub: <a href="https://github.com/ath1t" target="_blank" rel="noopener noreferrer" class="text-term-cyan underline">github.com/ath1t</a> (${ghStore.profile.public_repos} public repos • ${ghStore.profile.followers} followers) — Run <button type="button" onclick="runQuickCmd('github')" class="text-term-green underline">github</button> for full card.
              </div>
            </div>
          `,

          ls: (args) => {
            const showHidden = args.includes('-a') || args.includes('-la') || args.includes('-al');
            const detailed = args.includes('-l') || args.includes('-la') || args.includes('-al');

            if (detailed) {
              return `
                <div class="font-mono text-xs sm:text-sm space-y-1 text-term-text">
                  <div class="text-term-muted">total 36</div>
                  ${showHidden ? `
                  <div><span class="text-term-muted">drwxr-xr-x  5 thio staff  160 Nov 17 15:08</span> <span class="text-term-cyan font-semibold">.</span></div>
                  <div><span class="text-term-muted">drwxr-xr-x  9 thio staff  288 Nov 17 15:08</span> <span class="text-term-cyan font-semibold">..</span></div>
                  <div><span class="text-term-muted">-rw-r--r--  1 thio staff  412 Nov 17 15:08</span> <span class="text-term-muted">.zshrc</span></div>
                  ` : ''}
                  <div><span class="text-term-muted">-rw-r--r--  1 thio staff 1320 Nov 17 15:08</span> <button type="button" onclick="runQuickCmd('cat about.md')" class="text-term-purple hover:underline font-medium">about.md</button></div>
                  <div><span class="text-term-muted">-rw-r--r--  1 thio staff 2140 Nov 17 15:08</span> <button type="button" onclick="runQuickCmd('cat readme.md')" class="text-term-green hover:underline font-medium">readme.md</button></div>
                  <div><span class="text-term-muted">-rw-r--r--  1 thio staff  840 Nov 17 15:08</span> <button type="button" onclick="runQuickCmd('cat github.json')" class="text-term-cyan hover:underline font-medium">github.json</button></div>
                  <div><span class="text-term-muted">-rw-r--r--  1 thio staff  980 Nov 17 15:08</span> <button type="button" onclick="runQuickCmd('cat skills.json')" class="text-term-yellow hover:underline font-medium">skills.json</button></div>
                  <div><span class="text-term-muted">drwxr-xr-x  3 thio staff   96 Nov 17 15:08</span> <button type="button" onclick="runQuickCmd('projects')" class="text-term-green hover:underline font-semibold">projects/</button></div>
                  <div><span class="text-term-muted">drwxr-xr-x  ${ghStore.repos.length} thio staff  256 Nov 17 15:08</span> <button type="button" onclick="runQuickCmd('repos')" class="text-term-green hover:underline font-semibold">repos/</button></div>
                  <div><span class="text-term-muted">-rwxr-xr-x  1 thio staff  512 Nov 17 15:08</span> <button type="button" onclick="runQuickCmd('contact')" class="text-term-cyan hover:underline font-medium">contact.sh*</button></div>
                </div>
              `;
            }

            return `
              <div class="flex flex-wrap gap-x-6 gap-y-2 font-medium">
                ${showHidden ? '<span class="text-term-cyan">.</span> <span class="text-term-cyan">..</span> <span class="text-term-muted">.zshrc</span>' : ''}
                <button type="button" onclick="runQuickCmd('cat about.md')" class="text-term-purple hover:underline">about.md</button>
                <button type="button" onclick="runQuickCmd('cat readme.md')" class="text-term-green hover:underline">readme.md</button>
                <button type="button" onclick="runQuickCmd('cat github.json')" class="text-term-cyan hover:underline">github.json</button>
                <button type="button" onclick="runQuickCmd('cat skills.json')" class="text-term-yellow hover:underline">skills.json</button>
                <button type="button" onclick="runQuickCmd('projects')" class="text-term-green hover:underline font-semibold">projects/</button>
                <button type="button" onclick="runQuickCmd('repos')" class="text-term-green hover:underline font-semibold">repos/</button>
                <button type="button" onclick="runQuickCmd('contact')" class="text-term-cyan hover:underline">contact.sh*</button>
              </div>
            `;
          },

          cat: (args) => {
            if (!args.length) {
              return `<span class="text-term-red">cat: missing file operand</span><br><span class="text-term-muted text-xs">Try: <button type="button" onclick="runQuickCmd('cat about.md')" class="text-term-purple underline">cat about.md</button>, <button type="button" onclick="runQuickCmd('cat github.json')" class="text-term-cyan underline">cat github.json</button>, or <button type="button" onclick="runQuickCmd('cat skills.json')" class="text-term-yellow underline">cat skills.json</button></span>`;
            }
            const target = args[0].toLowerCase();
            if (VIRTUAL_FILES[target]) return VIRTUAL_FILES[target]();
            if (target === 'projects' || target === 'projects/') {
              return `<span class="text-term-yellow">cat: projects/: Is a directory.</span> Run <button type="button" onclick="runQuickCmd('projects')" class="text-term-green underline">projects</button> instead.`;
            }
            if (target === 'repos' || target === 'repos/') {
              return `<span class="text-term-yellow">cat: repos/: Is a directory.</span> Run <button type="button" onclick="runQuickCmd('repos')" class="text-term-green underline">repos</button> instead.`;
            }
            if (target === 'contact.sh' || target === 'contact') return COMMANDS.contact();
            return `<span class="text-term-red">cat: ${escapeHTML(args[0])}: No such file or directory</span>`;
          },

          projects: () => {
            const merged = [...FEATURED_PROJECTS];
            ghStore.repos.forEach((repo) => {
              const slug = repo.name.toLowerCase();
              if (slug !== 'mysub' && merged.length < 6) {
                merged.push({
                  name: `${repo.name} (GitHub Repo)`,
                  tag: `${repo.language || 'Code'} • ★ ${Number(repo.stargazers_count) || 0}`,
                  desc: repo.description || 'Public repository maintained by @ath1t on GitHub.',
                  repo: repo.html_url,
                  live: repo.homepage || '',
                  highlight: `Last updated ${formatRelativeDate(repo.updated_at)} on GitHub.`
                });
              }
            });

            const cards = merged.map((p, idx) => `
              <div class="border border-term-border/90 bg-term-header/45 hover:border-term-green/60 transition rounded-lg p-3.5 space-y-2">
                <div class="flex flex-wrap items-center justify-between gap-2">
                  <div class="flex items-center gap-2">
                    <span class="text-term-green font-bold">[0${idx + 1}]</span>
                    <h3 class="text-term-cyan font-bold text-sm sm:text-base">${escapeHTML(p.name)}</h3>
                  </div>
                  <span class="text-[11px] px-2 py-0.5 rounded bg-term-chip text-term-purple border border-term-border">${escapeHTML(p.tag)}</span>
                </div>
                <p class="text-term-text text-xs sm:text-sm">${escapeHTML(p.desc)}</p>
                <div class="flex flex-wrap items-center justify-between gap-2 pt-1 text-xs">
                  <span class="text-term-muted"><i class="fa-solid fa-bolt text-term-yellow mr-1"></i>${escapeHTML(p.highlight)}</span>
                  <div class="flex items-center gap-3">
                    ${p.live ? `
                    <a href="${escapeHTML(p.live)}" target="_blank" rel="noopener noreferrer" class="inline-flex items-center gap-1 text-term-cyan hover:underline font-medium">
                      <i class="fa-solid fa-globe"></i>
                      <span>Live App</span>
                    </a>` : ''}
                    <a href="${escapeHTML(p.repo)}" target="_blank" rel="noopener noreferrer" class="inline-flex items-center gap-1.5 text-term-green hover:underline font-medium">
                      <i class="fa-brands fa-github"></i>
                      <span>Source</span>
                      <i class="fa-solid fa-arrow-up-right-from-square text-[10px]"></i>
                    </a>
                  </div>
                </div>
              </div>
            `).join('');

            return `
              <div class="space-y-3 max-w-3xl">
                <div class="text-term-muted text-xs">Showing ${merged.length} featured projects &amp; live GitHub repositories (<button type="button" onclick="runQuickCmd('repos')" class="text-term-cyan underline">view all repos</button>):</div>
                ${cards}
              </div>
            `;
          },

          contact: () => `
            <div class="border border-term-border/80 bg-term-header/40 rounded-lg p-3.5 sm:p-4 max-w-2xl space-y-3">
              <div class="text-term-cyan font-semibold flex items-center gap-2">
                <i class="fa-solid fa-satellite-dish text-term-green"></i>
                <span>Connect with Thio (@ath1t)</span>
              </div>
              <div class="space-y-2 text-xs sm:text-sm">
                <div class="flex flex-wrap items-center justify-between gap-2 p-2 rounded bg-term-bg/70 border border-term-border/60">
                  <div class="flex items-center gap-2.5">
                    <i class="fa-brands fa-github text-term-text text-base"></i>
                    <span class="text-term-muted">GitHub:</span>
                    <a href="https://github.com/ath1t" target="_blank" rel="noopener noreferrer" class="text-term-cyan hover:underline font-medium">https://github.com/ath1t</a>
                  </div>
                  <button type="button" onclick="copyToClipboard('https://github.com/ath1t', 'GitHub URL')" class="text-[11px] px-2 py-0.5 rounded bg-term-chip hover:bg-term-chipHover text-term-muted hover:text-term-text border border-term-border transition">Copy</button>
                </div>
                <div class="flex flex-wrap items-center justify-between gap-2 p-2 rounded bg-term-bg/70 border border-term-border/60">
                  <div class="flex items-center gap-2.5">
                    <i class="fa-solid fa-network-wired text-term-purple text-base"></i>
                    <span class="text-term-muted">MySub Live:</span>
                    <a href="https://ath1t-mysub.vercel.app" target="_blank" rel="noopener noreferrer" class="text-term-purple hover:underline font-medium">https://ath1t-mysub.vercel.app</a>
                  </div>
                  <button type="button" onclick="copyToClipboard('https://ath1t-mysub.vercel.app', 'MySub URL')" class="text-[11px] px-2 py-0.5 rounded bg-term-chip hover:bg-term-chipHover text-term-muted hover:text-term-text border border-term-border transition">Copy</button>
                </div>
                <div class="flex flex-wrap items-center justify-between gap-2 p-2 rounded bg-term-bg/70 border border-term-border/60">
                  <div class="flex items-center gap-2.5">
                    <i class="fa-solid fa-globe text-term-green text-base"></i>
                    <span class="text-term-muted">Portfolio:</span>
                    <a href="https://ath1t.github.io" target="_blank" rel="noopener noreferrer" class="text-term-green hover:underline font-medium">https://ath1t.github.io</a>
                  </div>
                  <button type="button" onclick="copyToClipboard('https://ath1t.github.io', 'Portfolio URL')" class="text-[11px] px-2 py-0.5 rounded bg-term-chip hover:bg-term-chipHover text-term-muted hover:text-term-text border border-term-border transition">Copy</button>
                </div>
              </div>
              <div class="text-xs text-term-muted">Open to collaborating on Python CLI tools, automated scrapers, and FFmpeg media workflows.</div>
            </div>
          `,

          neofetch: () => {
            const asciiArt = [
              '  ████████╗██╗  ██╗██╗ ██████╗ ',
              '  ╚══██╔══╝██║  ██║██║██╔═══██╗',
              '     ██║   ███████║██║██║   ██║',
              '     ██║   ██╔══██║██║██║   ██║',
              '     ██║   ██║  ██║██║╚██████╔╝',
              '     ╚═╝   ╚═╝  ╚═╝╚═╝ ╚═════╝ ',
              '      [ ath1t // automation ]  '
            ].join('\n');

            return `
              <div class="flex flex-col md:flex-row items-start md:items-center gap-4 md:gap-7 py-1 max-w-3xl">
                <pre class="text-term-green font-bold text-[11px] sm:text-xs leading-tight select-none shrink-0">${asciiArt}</pre>
                <div class="space-y-1 text-xs sm:text-sm">
                  <div><span class="text-term-green font-bold">thio</span><span class="text-term-muted">@</span><span class="text-term-cyan font-bold">ath1t.github.io</span></div>
                  <div class="text-term-muted">-----------------------------</div>
                  <div><span class="text-term-cyan font-semibold">OS:</span> WebTermOS x86_64 (GitHub Pages)</div>
                  <div><span class="text-term-cyan font-semibold">GitHub:</span> <a href="https://github.com/ath1t" target="_blank" rel="noopener noreferrer" class="underline hover:text-term-green">github.com/ath1t</a> (${Number(ghStore.profile.public_repos) || 0} repos • ${Number(ghStore.profile.followers) || 0} followers)</div>
                  <div><span class="text-term-cyan font-semibold">Role:</span> Self-Taught Programmer</div>
                  <div><span class="text-term-cyan font-semibold">Focus:</span> Python, CLI Automation &amp; Video Prod</div>
                  <div><span class="text-term-cyan font-semibold">Shell:</span> zsh 5.9 (interactive-cli)</div>
                  <div><span class="text-term-cyan font-semibold">Packages:</span> python3, ffmpeg, yt-dlp, git</div>
                  <div><span class="text-term-cyan font-semibold">Location:</span> ${escapeHTML(ghStore.profile.location || USER_DATA.location)}</div>
                  <div class="pt-1.5 flex items-center gap-1.5">
                    <span class="w-3.5 h-3.5 rounded-sm bg-[#ff7b72]"></span>
                    <span class="w-3.5 h-3.5 rounded-sm bg-[#3fb950]"></span>
                    <span class="w-3.5 h-3.5 rounded-sm bg-[#d29922]"></span>
                    <span class="w-3.5 h-3.5 rounded-sm bg-[#58a6ff]"></span>
                    <span class="w-3.5 h-3.5 rounded-sm bg-[#bc8cff]"></span>
                    <span class="w-3.5 h-3.5 rounded-sm bg-[#e6edf3]"></span>
                  </div>
                </div>
              </div>
            `;
          },

          echo: (args) => `<div class="text-term-text break-words">${escapeHTML(args.join(' '))}</div>`,
          date: () => `<div class="text-term-cyan">${escapeHTML(new Date().toString())}</div>`,
          clear: () => {
            outputContainer.innerHTML = '';
            return null;
          }
        };

        function executeCommand(rawInput) {
          try {
            const trimmed = String(rawInput || '').trim();
            if (autocompleteHint) autocompleteHint.classList.add('hidden');

            if (!trimmed) {
              appendOutput('', null, true);
              return;
            }

            if (shellState.history[shellState.history.length - 1] !== trimmed) {
              shellState.history.push(trimmed);
            }
            shellState.historyIndex = shellState.history.length;

            const parts = trimmed.split(/\s+/);
            const cmd = parts[0].toLowerCase();
            const args = parts.slice(1);

            if (cmd === 'clear') {
              COMMANDS.clear();
              return;
            }

            if (Object.prototype.hasOwnProperty.call(COMMANDS, cmd)) {
              const result = COMMANDS[cmd](args);
              appendOutput(trimmed, result, true);
            } else {
              const errorHtml = `
                <div class="text-term-red">zsh: command not found: <span class="font-semibold">${escapeHTML(parts[0])}</span></div>
                <div class="text-xs text-term-muted">Type <button type="button" onclick="runQuickCmd('help')" class="text-term-cyan underline">help</button> to see all supported commands.</div>
              `;
              appendOutput(trimmed, errorHtml, true);
            }
          } catch (err) {
            appendOutput(String(rawInput || ''), `<div class="text-term-red text-xs">Runtime error: ${escapeHTML(err && err.message ? err.message : 'Unexpected command failure')}</div>`, true);
          }
        }

        window.runQuickCmd = function (cmd) {
          cliInput.value = '';
          executeCommand(cmd);
          cliInput.focus();
        };

        function handleTabComplete() {
          const currentVal = cliInput.value;
          const parts = currentVal.split(/\s+/);
          const availableCmds = Object.keys(COMMANDS);
          const availableFiles = ['about.md', 'readme.md', 'github.json', 'skills.json', 'projects/', 'repos/', 'contact.sh'];
          const githubSubs = ['profile', 'repos', 'activity', 'refresh'];

          if (parts.length <= 1) {
            const partial = parts[0].toLowerCase();
            const matches = availableCmds.filter((c) => c.startsWith(partial));
            if (matches.length === 1) {
              const needsSpace = ['cat', 'echo', 'github', 'gh'].includes(matches[0]);
              cliInput.value = matches[0] + (needsSpace ? ' ' : '');
              if (autocompleteHint) autocompleteHint.classList.add('hidden');
            } else if (matches.length > 1 && autocompleteHint) {
              autocompleteHint.textContent = 'Suggestions: ' + matches.join('   ');
              autocompleteHint.classList.remove('hidden');
              scrollToBottom();
            }
          } else if (parts[0].toLowerCase() === 'cat') {
            const partialFile = parts[1].toLowerCase();
            const matches = availableFiles.filter((f) => f.toLowerCase().startsWith(partialFile));
            if (matches.length === 1) {
              cliInput.value = `cat ${matches[0]}`;
              if (autocompleteHint) autocompleteHint.classList.add('hidden');
            } else if (matches.length > 1 && autocompleteHint) {
              autocompleteHint.textContent = 'Files: ' + matches.join('   ');
              autocompleteHint.classList.remove('hidden');
              scrollToBottom();
            }
          } else if (parts[0].toLowerCase() === 'github' || parts[0].toLowerCase() === 'gh') {
            const partialSub = parts[1].toLowerCase();
            const matches = githubSubs.filter((s) => s.startsWith(partialSub));
            if (matches.length === 1) {
              cliInput.value = `${parts[0]} ${matches[0]}`;
              if (autocompleteHint) autocompleteHint.classList.add('hidden');
            } else if (matches.length > 1 && autocompleteHint) {
              autocompleteHint.textContent = 'Subcommands: ' + matches.join('   ');
              autocompleteHint.classList.remove('hidden');
              scrollToBottom();
            }
          }
        }

        function navigateHistory(direction) {
          if (!shellState.history.length) return;
          if (direction === 'up') {
            if (shellState.historyIndex > 0) shellState.historyIndex--;
            cliInput.value = shellState.history[shellState.historyIndex] || '';
          } else if (direction === 'down') {
            if (shellState.historyIndex < shellState.history.length - 1) {
              shellState.historyIndex++;
              cliInput.value = shellState.history[shellState.historyIndex] || '';
            } else {
              shellState.historyIndex = shellState.history.length;
              cliInput.value = '';
            }
          }
          if (autocompleteHint) autocompleteHint.classList.add('hidden');
        }

        cliInput.addEventListener('input', () => {
          if (autocompleteHint) autocompleteHint.classList.add('hidden');
        });

        cliInput.addEventListener('keydown', (e) => {
          if (e.key === 'Enter') {
            e.preventDefault();
            const val = cliInput.value;
            cliInput.value = '';
            executeCommand(val);
          } else if (e.key === 'ArrowUp') {
            e.preventDefault();
            navigateHistory('up');
          } else if (e.key === 'ArrowDown') {
            e.preventDefault();
            navigateHistory('down');
          } else if (e.key === 'Tab') {
            e.preventDefault();
            handleTabComplete();
          } else if (e.ctrlKey && e.key.toLowerCase() === 'l') {
            e.preventDefault();
            COMMANDS.clear();
          }
        });

        terminalBody.addEventListener('click', (e) => {
          if (e.target.closest('button') || e.target.closest('a')) return;
          const selection = window.getSelection();
          if (selection && selection.toString().length > 0) return;
          cliInput.focus();
        });

        document.querySelectorAll('.quick-chip').forEach((btn) => {
          btn.addEventListener('click', () => {
            const cmd = btn.getAttribute('data-cmd');
            if (cmd) window.runQuickCmd(cmd);
          });
        });

        const tabBtn = document.getElementById('mobile-tab-btn');
        const upBtn = document.getElementById('mobile-up-btn');
        const downBtn = document.getElementById('mobile-down-btn');
        if (tabBtn) tabBtn.addEventListener('click', () => { handleTabComplete(); cliInput.focus(); });
        if (upBtn) upBtn.addEventListener('click', () => { navigateHistory('up'); cliInput.focus(); });
        if (downBtn) downBtn.addEventListener('click', () => { navigateHistory('down'); cliInput.focus(); });

        if (crtToggle) {
          crtToggle.addEventListener('click', () => {
            const isPressed = crtToggle.getAttribute('aria-pressed') === 'true';
            const nextState = !isPressed;
            crtToggle.setAttribute('aria-pressed', String(nextState));
            document.body.classList.toggle('crt-enabled', nextState);
            if (crtIndicator) {
              crtIndicator.classList.toggle('bg-term-green', nextState);
              crtIndicator.classList.toggle('bg-term-muted', !nextState);
            }
          });
        }

        (async () => {
          const welcomeBanner = `
            <div class="text-xs sm:text-sm text-term-muted pb-1 border-b border-term-border/50">
              Welcome to <span class="text-term-green font-semibold">Thio's</span> interactive terminal portfolio (<a href="https://github.com/ath1t" target="_blank" rel="noopener noreferrer" class="text-term-cyan underline">github.com/ath1t</a>).
              Type <button type="button" onclick="runQuickCmd('help')" class="text-term-green underline font-medium">help</button>, <button type="button" onclick="runQuickCmd('github')" class="text-term-cyan underline font-medium">github</button>, or tap a quick command above.
            </div>
          `;
          appendOutput('', welcomeBanner, false);
          await hydrateGitHubData(false);
          appendOutput('neofetch', COMMANDS.neofetch(), true);
          cliInput.focus();
        })();
      })();
    </script>
  </body>
</html>
