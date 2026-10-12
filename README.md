
<html lang="pt-BR" class="dark">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>S.A.M.S. - Habitações em Ambientes de Gravidade Extrema</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    colors: {
                        space: {
                            950: '#020617',
                            900: '#030712',
                            800: '#0b0f19',
                            700: '#111827',
                        },
                        sams: {
                            cyan: '#00f3ff',
                            emerald: '#10b981',
                            amber: '#f59e0b',
                            violet: '#8b5cf6',
                            rose: '#f43f5e'
                        }
                    },
                    fontFamily: {
                        mono: ['JetBrains Mono', 'Courier New', monospace],
                        orbitron: ['Orbitron', 'sans-serif']
                    }
                }
            }
        }
    </script>
    <!-- Google Fonts -->
    <link href="https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@400;700&family=Orbitron:wght@500;700;900&display=swap" rel="stylesheet">
    <!-- FontAwesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        body {
            font-family: 'JetBrains Mono', monospace;
            background-color: #020617;
            color: #f8fafc;
            overflow-x: hidden;
        }
        h1, h2, h3, .font-orbitron {
            font-family: 'Orbitron', sans-serif;
        }
        .glow-cyan {
            box-shadow: 0 0 25px rgba(0, 243, 255, 0.35);
        }
        .glow-rose {
            box-shadow: 0 0 25px rgba(244, 63, 94, 0.45);
        }
        .glow-emerald {
            box-shadow: 0 0 25px rgba(16, 185, 129, 0.35);
        }
        .text-glow-cyan {
            text-shadow: 0 0 12px rgba(0, 243, 255, 0.8);
        }
        .scanline {
            background: linear-gradient(
                to bottom,
                rgba(255,255,255,0),
                rgba(255,255,255,0) 50%,
                rgba(0, 243, 255, 0.02) 50%,
                rgba(0, 243, 255, 0.02)
            );
            background-size: 100% 4px;
        }
        /* Custom scrollbar */
        ::-webkit-scrollbar {
            width: 6px;
        }
        ::-webkit-scrollbar-track {
            background: #030712;
        }
        ::-webkit-scrollbar-thumb {
            background: #111827;
            border-radius: 3px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #00f3ff;
        }
    </style>
</head>
<body class="min-h-screen flex flex-col bg-space-950 scanline">

    <header class="border-b border-sams-cyan/30 bg-space-900/90 backdrop-blur-md sticky top-0 z-50 px-4 py-3">
        <div class="max-w-7xl mx-auto flex flex-col md:flex-row items-center justify-between gap-4">
            
            <div class="flex items-center space-x-3">
                <div id="logo-icon-container" class="w-10 h-10 rounded-xl bg-space-800 border border-sams-cyan flex items-center justify-center glow-cyan transition-all">
                    <i class="fa-solid fa-shield-halved text-sams-cyan text-xl"></i>
                </div>
                <div>
                    <h1 class="text-xl font-black tracking-wider text-sams-cyan text-glow-cyan">S.A.M.S. - GRAVITY DAMPING</h1>
                    <p class="text-[10px] text-slate-400 uppercase tracking-widest">Habitações em Ambientes de Gravidade Extrema</p>
                </div>
            </div>

            <!-- View Modes & Tabs -->
            <div class="flex flex-wrap items-center gap-1.5 bg-space-950/80 p-1.5 rounded-xl border border-space-800">
                <button onclick="switchView('surface')" id="tab-surface" class="px-3.5 py-1.5 rounded-lg text-xs font-bold transition-all bg-sams-cyan/25 text-sams-cyan border border-sams-cyan/60 glow-cyan flex items-center gap-2">
                    <i class="fa-solid fa-mountain"></i> Superfície Super-Terra
                </button>
                <button onclick="switchView('internal')" id="tab-internal" class="px-3.5 py-1.5 rounded-lg text-xs font-bold transition-all text-slate-400 hover:text-sams-cyan hover:bg-space-800 border border-transparent flex items-center gap-2">
                    <i class="fa-solid fa-house-chimney"></i> Interior do Domo (1.0G)
                </button>
                <button onclick="switchView('molecular')" id="tab-molecular" class="px-3.5 py-1.5 rounded-lg text-xs font-bold transition-all text-slate-400 hover:text-sams-cyan hover:bg-space-800 border border-transparent flex items-center gap-2">
                    <i class="fa-solid fa-atom"></i> Malha Piezoelétrica
                </button>
            </div>

            <!-- Action Buttons -->
            <div class="flex items-center space-x-3">
                <button onclick="toggleAudio()" id="btn-audio" class="w-9 h-9 rounded-xl bg-space-800 border border-space-700 hover:border-sams-cyan text-slate-300 flex items-center justify-center text-xs transition-all" title="Alternar Som Ambiente">
                    <i class="fa-solid fa-volume-xmark" id="audio-icon"></i>
                </button>
                <button onclick="openModal()" class="px-3 py-1.5 rounded-xl bg-space-800 border border-sams-cyan/40 hover:border-sams-cyan text-sams-cyan text-xs font-bold flex items-center gap-2 transition-all glow-cyan">
                    <i class="fa-solid fa-book-open"></i> Visão Geral do Aplicativo
                </button>
            </div>
        </div>
    </header>

    <main class="flex-1 max-w-7xl w-full mx-auto p-4 grid grid-cols-1 lg:grid-cols-4 gap-4">
        
        <!-- Canvas Area (3 Cols) -->
        <div class="lg:col-span-3 flex flex-col gap-4">
            
            <div id="canvas-wrapper" class="relative w-full aspect-[16/10] bg-space-900 rounded-2xl border border-sams-cyan/30 overflow-hidden glow-cyan flex items-center justify-center transition-all">
                
                <!-- Main Canvas Element -->
                <canvas id="simCanvas" class="w-full h-full block cursor-crosshair"></canvas>

                <!-- Floating HUD Overlays -->
                <div class="absolute top-4 left-4 bg-space-950/85 backdrop-blur-md p-3 rounded-xl border border-sams-cyan/30 text-xs space-y-1 pointer-events-none">
                    <div id="hud-title" class="text-sams-cyan font-bold uppercase tracking-wider flex items-center gap-2">
                        <i class="fa-solid fa-satellite-dish animate-pulse"></i> <span>BOLHA KINETIC DAMPING: ATIVA</span>
                    </div>
                    <div class="text-slate-400">FPS: <span id="hud-fps" class="text-white">60</span> | GRAVIDADE EXTERNA: <span id="hud-ext-g" class="text-amber-400">8.5G</span></div>
                    <div class="text-slate-400">GRAVIDADE INTERNA: <span id="hud-int-g" class="text-emerald-400">1.00G (Estável)</span></div>
                </div>

                <!-- SAMS Failure Warning Overlay -->
                <div id="sams-alert" class="absolute top-4 right-4 bg-rose-950/90 backdrop-blur-md px-4 py-2 rounded-xl border border-rose-500 text-xs font-bold text-rose-300 hidden animate-pulse flex items-center gap-2">
                    <i class="fa-solid fa-triangle-exclamation"></i> ALERTA: SAMS DESLIGADO - COLAPSO ESTRUTURAL IMINENTE
                </div>

                <!-- Simulation Playback Controls Bar -->
                <div class="absolute bottom-4 left-1/2 -translate-x-1/2 bg-space-950/90 backdrop-blur-md px-6 py-3 rounded-2xl border border-sams-cyan/40 flex items-center gap-4 shadow-2xl">
                    <button onclick="togglePlayPause()" id="btn-play" class="w-10 h-10 rounded-xl bg-sams-cyan hover:bg-emerald-400 text-space-950 font-bold flex items-center justify-center transition-all glow-cyan">
                        <i class="fa-solid fa-pause" id="icon-play"></i>
                    </button>
                    <div class="h-6 w-[1px] bg-space-800"></div>
                    <div class="flex items-center gap-2">
                        <span class="text-xs text-slate-400 uppercase">Velocidade:</span>
                        <button onclick="setSpeed(1)" id="spd-1" class="px-2.5 py-1 rounded-lg text-xs font-bold bg-sams-cyan/25 text-sams-cyan border border-sams-cyan">1x</button>
                        <button onclick="setSpeed(3)" id="spd-3" class="px-2.5 py-1 rounded-lg text-xs font-bold bg-space-800 text-slate-400 border border-space-700">3x</button>
                        <button onclick="setSpeed(5)" id="spd-5" class="px-2.5 py-1 rounded-lg text-xs font-bold bg-space-800 text-slate-400 border border-space-700">5x</button>
                    </div>
                    <div class="h-6 w-[1px] bg-space-800"></div>
                    <button onclick="triggerSeismicPurge()" class="px-3 py-1.5 rounded-xl bg-violet-950/80 hover:bg-violet-900 text-xs text-violet-300 border border-violet-500/50 flex items-center gap-2 transition-all font-bold">
                        <i class="fa-solid fa-wave-square"></i> Purga Sísmica
                    </button>
                </div>
            </div>

            <!-- Description Box -->
            <div class="bg-space-900/90 backdrop-blur-md p-4 rounded-2xl border border-space-800 text-sm">
                <h3 class="font-bold text-sams-cyan mb-1 flex items-center gap-2"><i class="fa-solid fa-circle-info"></i> Mecanismo de Amortecimento Cinético</h3>
                <p id="view-desc" class="text-slate-300 text-xs leading-relaxed">
                    O SAMS (Smart Adaptive Material Systems) utiliza ressonadores piezoelétricos de alta frequência combinados com fluido magnetorreológico para neutralizar ondas de compressão gravitacional, mantendo o interior do domo em confortáveis 1.0G mesmo sob gravidade extrema de Super-Terras.
                </p>
            </div>

        </div>

        <div class="lg:col-span-1 flex flex-col gap-4">
            
            <!-- Telemetry Panel -->
            <div class="bg-space-900/90 backdrop-blur-md p-4 rounded-2xl border border-sams-cyan/30 flex flex-col gap-4">
                <div class="flex items-center justify-between border-b border-space-800 pb-3">
                    <h2 class="font-orbitron font-bold text-sm text-sams-cyan flex items-center gap-2">
                        <i class="fa-solid fa-gauge-high"></i> Telemetria SAMS
                    </h2>
                    <span id="system-status-badge" class="text-[10px] bg-emerald-500/20 text-emerald-400 px-2 py-0.5 rounded border border-emerald-500/40">ESTÁVEL</span>
                </div>

                <!-- Metrics -->
                <div class="space-y-3 text-xs">
                    <div>
                        <div class="flex justify-between mb-1">
                            <span class="text-slate-400">Integridade Estrutural</span>
                            <span id="val-integrity" class="text-emerald-400 font-bold">100.0%</span>
                        </div>
                        <div class="w-full bg-space-950 rounded-full h-2 overflow-hidden border border-space-800">
                            <div id="bar-integrity" class="bg-emerald-400 h-full transition-all duration-300" style="width: 100%;"></div>
                        </div>
                    </div>

                    <div>
                        <div class="flex justify-between mb-1">
                            <span class="text-slate-400">Eficiência de Amortecimento</span>
                            <span id="val-efficiency" class="text-sams-cyan font-bold">99.8%</span>
                        </div>
                        <div class="w-full bg-space-950 rounded-full h-2 overflow-hidden border border-space-800">
                            <div id="bar-efficiency" class="bg-sams-cyan h-full transition-all duration-300" style="width: 99.8%;"></div>
                        </div>
                    </div>

                    <div>
                        <div class="flex justify-between mb-1">
                            <span class="text-slate-400">Carga Energética SAMS</span>
                            <span id="val-power" class="text-amber-400 font-bold">420 GW</span>
                        </div>
                        <div class="w-full bg-space-950 rounded-full h-2 overflow-hidden border border-space-800">
                            <div id="bar-power" class="bg-amber-400 h-full transition-all duration-300" style="width: 70%;"></div>
                        </div>
                    </div>
                </div>

                <!-- Controls -->
                <div class="space-y-3 pt-2 border-t border-space-800">
                    <h3 class="font-bold text-xs text-sams-cyan uppercase">Controles do Sistema</h3>
                    
                    <div class="flex items-center justify-between bg-space-950 p-2.5 rounded-xl border border-space-800">
                        <span class="text-xs text-slate-300">Sistema SAMS Damping</span>
                        <button onclick="toggleSamsSystem()" id="btn-sams" class="px-3 py-1 rounded-lg text-xs font-bold bg-emerald-500/20 text-emerald-400 border border-emerald-500/50 glow-emerald transition-all">
                            ATIVADO
                        </button>
                    </div>

                    <div class="space-y-1">
                        <div class="flex justify-between text-xs">
                            <span class="text-slate-400">Gravidade do Planeta</span>
                            <span id="label-gravity" class="text-amber-400 font-bold">8.5G</span>
                        </div>
                        <input type="range" id="gravitySlider" min="2.0" max="12.0" step="0.5" value="8.5" 
                            class="w-full accent-amber-400 bg-space-950 rounded-lg appearance-none cursor-pointer h-2 border border-space-800"
                            oninput="updateGravity(this.value)">
                    </div>

                    <div class="space-y-1">
                        <div class="flex justify-between text-xs">
                            <span class="text-slate-400">Frequência Piezoelétrica</span>
                            <span id="label-freq" class="text-sams-cyan font-bold">42.5 kHz</span>
                        </div>
                        <input type="range" id="freqSlider" min="10" max="100" step="1" value="42.5" 
                            class="w-full accent-sams-cyan bg-space-950 rounded-lg appearance-none cursor-pointer h-2 border border-space-800"
                            oninput="updateFreq(this.value)">
                    </div>

                    <div class="space-y-1">
                        <div class="flex justify-between text-xs">
                            <span class="text-slate-400">Viscosidade Fluido MR</span>
                            <span id="label-viscosity" class="text-violet-400 font-bold">Ótima (75 Pa·s)</span>
                        </div>
                        <input type="range" id="viscositySlider" min="10" max="150" step="5" value="75" 
                            class="w-full accent-violet-400 bg-space-950 rounded-lg appearance-none cursor-pointer h-2 border border-space-800"
                            oninput="updateViscosity(this.value)">
                    </div>
                </div>

            </div>

            <!-- Terminal Log -->
            <div class="bg-space-900/90 backdrop-blur-md p-4 rounded-2xl border border-space-800 flex flex-col flex-1 min-h-[180px]">
                <div class="flex items-center justify-between border-b border-space-800 pb-2 mb-2">
                    <h3 class="font-orbitron font-bold text-xs text-sams-cyan flex items-center gap-2">
                        <i class="fa-solid fa-terminal"></i> Log de Diagnóstico SAMS
                    </h3>
                    <button onclick="clearLogs()" class="text-[10px] text-slate-400 hover:text-sams-cyan underline">Limpar</button>
                </div>
                <div id="log-container" class="flex-1 overflow-y-auto space-y-1.5 font-mono text-[11px] text-slate-300 max-h-[160px]">
                    <div class="text-sams-cyan">[08:22:00] SAMS Damping Bubble inicializado com sucesso.</div>
                    <div class="text-emerald-400">[08:22:01] Ressonadores piezoelétricos sincronizados a 42.5 kHz.</div>
                    <div class="text-slate-400">[08:22:02] Gravidade externa estabilizada em 8.5G (Interior 1.0G).</div>
                </div>
            </div>

        </div>

    </main>

    <div id="infoModal" class="fixed inset-0 bg-space-950/80 backdrop-blur-sm z-50 flex items-center justify-center p-4 hidden">
        <div class="bg-space-900 border border-sams-cyan/50 rounded-2xl max-w-2xl w-full p-6 space-y-4 glow-cyan relative max-h-[90vh] overflow-y-auto">
            <div class="flex items-center justify-between border-b border-space-800 pb-3">
                <h3 class="font-orbitron font-bold text-lg text-sams-cyan flex items-center gap-2">
                    <i class="fa-solid fa-shield-halved text-sams-cyan"></i> Visão Geral do Aplicativo & Fundamentos
                </h3>
                <button onclick="closeModal()" class="text-slate-400 hover:text-white text-lg"><i class="fa-solid fa-xmark"></i></button>
            </div>
            
            <div class="space-y-3 text-xs text-slate-300 leading-relaxed">
                <p>
                    <strong class="text-sams-cyan">Problema Resolvido:</strong> A impossibilidade humana de colonizar planetas massivos (Super-Terras) ou construir bases sob pressão gravitacional esmagadora é resolvida anulando o estresse mecânico externo.
                </p>
                <p>
                    <strong class="text-emerald-400">Resonadores Piezoelétricos:</strong> Integrados à estrutura molecular das paredes modulares, geram contra-ondas sônicas e mecânicas exatas em frequências milimétricas para anular a compressão gravitacional.
                </p>
                <p>
                    <strong class="text-violet-400">Fluido Magnetorreológico:</strong> Canais estruturais preenchidos com nanopartículas metálicas em suspensão alteram instantaneamente sua viscosidade sob campos magnéticos programados, criando uma "bolha de amortecimento cinético" flexível e indestrutível.
                </p>
                <div class="bg-space-950 p-3 rounded-xl border border-space-800 space-y-1">
                    <div class="font-bold text-sams-cyan">Recursos do Simulador:</div>
                    <ul class="list-disc pl-4 space-y-1 text-slate-400">
                        <li><strong>Superfície de Super-Terra:</strong> Visualização de ondas gravitacionais e atmosfera densa.</li>
                        <li><strong>Domo SAMS:</strong> Monitoramento da integridade estrutural e da bolha de força cianeto-violeta.</li>
                        <li><strong>Controle de Gravidade:</strong> Ajuste dinâmico de 2.0G até 12.0G para testar limites de colapso.</li>
                    </ul>
                </div>
            </div>

            <div class="pt-3 border-t border-space-800 flex justify-end">
                <button onclick="closeModal()" class="px-4 py-2 rounded-xl bg-sams-cyan text-space-950 font-bold text-xs hover:bg-emerald-400 transition-all glow-cyan">
                    Entendido, Iniciar Simulação
                </button>
            </div>
        </div>
    </div>

    <script>
        const canvas = document.getElementById('simCanvas');
        const ctx = canvas.getContext('2d');

        let currentView = 'surface'; // 'surface', 'internal', 'molecular'
        let isRunning = true;
        let timeScale = 1;
        let simulationTime = 0;
        
        let planetGravity = 8.5;
        let samsActive = true;
        let piezoFreq = 42.5;
        let mrViscosity = 75;
        
        let structuralIntegrity = 100.0;
        let dampingEfficiency = 99.8;
        let powerConsumption = 420;

        let canvasShakeTimer = 0;

        function resizeCanvas() {
            const rect = canvas.getBoundingClientRect();
            canvas.width = rect.width * window.devicePixelRatio;
            canvas.height = rect.height * window.devicePixelRatio;
            ctx.scale(window.devicePixelRatio, window.devicePixelRatio);
        }
        window.addEventListener('resize', resizeCanvas);
        resizeCanvas();

        // --- AUDIO SYSTEM ---
        let audioCtx = null;
        let audioMuted = true;
        let ambientOsc = null;
        let ambientGain = null;

        function toggleAudio() {
            audioMuted = !audioMuted;
            const icon = document.getElementById('audio-icon');
            if (!audioMuted) {
                icon.className = "fa-solid fa-volume-high text-sams-cyan";
                initWebAudio();
                addLog("Áudio ambiente SAMS ativado.");
            } else {
                icon.className = "fa-solid fa-volume-xmark";
                if (audioCtx && audioCtx.state === 'running') {
                    audioCtx.suspend();
                }
                addLog("Áudio desativado.");
            }
        }

        function initWebAudio() {
            if (!audioCtx) {
                audioCtx = new (window.AudioContext || window.webkitAudioContext)();
            }
            if (audioCtx.state === 'suspended') {
                audioCtx.resume();
            }
            if (!ambientOsc) {
                ambientOsc = audioCtx.createOscillator();
                ambientGain = audioCtx.createGain();
                
                ambientOsc.type = 'sine';
                ambientOsc.frequency.setValueAtTime(55, audioCtx.currentTime);
                ambientGain.gain.setValueAtTime(0.02, audioCtx.currentTime);

                ambientOsc.connect(ambientGain);
                ambientGain.connect(audioCtx.destination);
                ambientOsc.start();
            }
        }

        // --- VIEW SWITCHING ---
        function switchView(view) {
            currentView = view;
            ['surface', 'internal', 'molecular'].forEach(v => {
                const btn = document.getElementById(`tab-${v}`);
                if (v === view) {
                    btn.className = "px-3.5 py-1.5 rounded-lg text-xs font-bold transition-all bg-sams-cyan/25 text-sams-cyan border border-sams-cyan/60 glow-cyan flex items-center gap-2";
                } else {
                    btn.className = "px-3.5 py-1.5 rounded-lg text-xs font-bold transition-all text-slate-400 hover:text-sams-cyan hover:bg-space-800 border border-transparent flex items-center gap-2";
                }
            });

            const titles = {
                surface: "BOLHA KINETIC DAMPING: ATIVA (SUPER-TERRA)",
                internal: "VISTA INTERIOR DO DOMO: ESTÁVEL (1.0G)",
                molecular: "MALHA PIEOELÉTRICA E FLUIDO MAGNETORREOLÓGICO"
            };
            const descs = {
                surface: "O SAMS neutraliza ondas de compressão gravitacional externa em tempo real, mantendo a estrutura do domo intacta sob gravidade esmagadora.",
                internal: "Cidadãos e infraestrutura operam em gravidade artificial perfeita de 1.0G, protegidos das forças titânicas do planeta massivo.",
                molecular: "Nanopartículas metálicas e cristais piezoelétricos oscilam em contra-frequência para dissipar toda a energia cinética gravitacional."
            };
            document.getElementById('hud-title').querySelector('span').innerText = titles[view];
            document.getElementById('view-desc').innerText = descs[view];
            addLog(`Alternado para a visualização: ${view.toUpperCase()}`);
        }

        // --- CONTROLS ---
        function togglePlayPause() {
            isRunning = !isRunning;
            const icon = document.getElementById('icon-play');
            const btn = document.getElementById('btn-play');
            if (isRunning) {
                icon.className = "fa-solid fa-pause";
                btn.classList.add('bg-sams-cyan', 'glow-cyan');
                btn.classList.remove('bg-space-800');
                addLog("Simulação retomada.");
            } else {
                icon.className = "fa-solid fa-play";
                btn.classList.remove('bg-sams-cyan', 'glow-cyan');
                btn.classList.add('bg-space-800');
                addLog("Simulação pausada.");
            }
        }

        function setSpeed(spd) {
            timeScale = spd;
            [1, 3, 5].forEach(s => {
                const b = document.getElementById(`spd-${s}`);
                if (s === spd) {
                    b.className = "px-2.5 py-1 rounded-lg text-xs font-bold bg-sams-cyan/25 text-sams-cyan border border-sams-cyan";
                } else {
                    b.className = "px-2.5 py-1 rounded-lg text-xs font-bold bg-space-800 text-slate-400 border border-space-700";
                }
            });
            addLog(`Velocidade ajustada para ${spd}x.`);
        }

        function toggleSamsSystem() {
            samsActive = !samsActive;
            const btn = document.getElementById('btn-sams');
            const alertElem = document.getElementById('sams-alert');
            const badge = document.getElementById('system-status-badge');
            const wrapper = document.getElementById('canvas-wrapper');
            const logoIcon = document.getElementById('logo-icon-container');

            if (samsActive) {
                btn.innerText = "ATIVADO";
                btn.className = "px-3 py-1 rounded-lg text-xs font-bold bg-emerald-500/20 text-emerald-400 border border-emerald-500/50 glow-emerald transition-all";
                alertElem.classList.add('hidden');
                badge.innerText = "ESTÁVEL";
                badge.className = "text-[10px] bg-emerald-500/20 text-emerald-400 px-2 py-0.5 rounded border border-emerald-500/40";
                wrapper.classList.remove('border-rose-500', 'glow-rose');
                wrapper.classList.add('border-sams-cyan/30', 'glow-cyan');
                logoIcon.classList.remove('border-rose-500');
                logoIcon.classList.add('border-sams-cyan');
                addLog("Sistema SAMS Damping reativado. Estabilizando estrutura.");
            } else {
                btn.innerText = "DESLIGADO";
                btn.className = "px-3 py-1 rounded-lg text-xs font-bold bg-rose-500/20 text-rose-400 border border-rose-500/50 glow-rose transition-all";
                alertElem.classList.remove('hidden');
                badge.innerText = "COLAPSO";
                badge.className = "text-[10px] bg-rose-500/20 text-rose-400 px-2 py-0.5 rounded border border-rose-500/40";
                wrapper.classList.remove('border-sams-cyan/30', 'glow-cyan');
                wrapper.classList.add('border-rose-500', 'glow-rose');
                logoIcon.classList.remove('border-sams-cyan');
                logoIcon.classList.add('border-rose-500');
                addLog("ALERTA CRÍTICO: SAMS DESLIGADO! Gravidade extrema esmagando estrutura!");
            }
        }

        function updateGravity(val) {
            planetGravity = parseFloat(val);
            document.getElementById('label-gravity').innerText = planetGravity.toFixed(1) + "G";
            document.getElementById('hud-ext-g').innerText = planetGravity.toFixed(1) + "G";
            powerConsumption = Math.round(420 * (planetGravity / 8.5));
            document.getElementById('val-power').innerText = powerConsumption + " GW";
            document.getElementById('bar-power').style.width = Math.min(100, (powerConsumption / 800) * 100) + "%";
            addLog(`Gravidade do planeta ajustada para ${planetGravity.toFixed(1)}G.`);
        }

        function updateFreq(val) {
            piezoFreq = parseFloat(val);
            document.getElementById('label-freq').innerText = piezoFreq.toFixed(1) + " kHz";
            addLog(`Frequência piezoelétrica ajustada para ${piezoFreq.toFixed(1)} kHz.`);
        }

        function updateViscosity(val) {
            mrViscosity = parseInt(val);
            let desc = "Ótima";
            if (mrViscosity < 40) desc = "Baixa";
            else if (mrViscosity > 110) desc = "Alta";
            document.getElementById('label-viscosity').innerText = `${desc} (${mrViscosity} Pa·s)`;
            addLog(`Viscosidade do fluido MR ajustada para ${mrViscosity} Pa·s.`);
        }

        function triggerSeismicPurge() {
            canvasShakeTimer = 30;
            addLog("Purga sísmica acionada! Dissipando energia acumulada nas fundações.");
        }

        function openModal() {
            document.getElementById('infoModal').classList.remove('hidden');
        }
        function closeModal() {
            document.getElementById('infoModal').classList.add('hidden');
        }

        function clearLogs() {
            document.getElementById('log-container').innerHTML = `<div class="text-slate-400">[Console limpo pelo operador]</div>`;
        }

        function addLog(text) {
            const container = document.getElementById('log-container');
            const now = new Date().toTimeString().split(' ')[0];
            const div = document.createElement('div');
            div.className = "text-slate-300";
            div.innerHTML = `<span class="text-sams-cyan">[${now}]</span> ${text}`;
            container.appendChild(div);
            container.scrollTop = container.scrollHeight;
        }

        // --- DRAWING FUNCTIONS ---

        function drawStarfield(w, h) {
            ctx.fillStyle = '#020617';
            ctx.fillRect(0, 0, w, h);

            ctx.fillStyle = '#ffffff';
            for (let i = 0; i < 60; i++) {
                let x = (Math.sin(i * 77) * 10000) % w;
                let y = (Math.cos(i * 99) * 10000) % h;
                if (x < 0) x += w;
                if (y < 0) y += h;
                let alpha = 0.2 + (Math.sin(simulationTime * 0.05 + i) * 0.2);
                ctx.globalAlpha = Math.max(0.1, alpha);
                ctx.fillRect(x, y, 1.5, 1.5);
            }
            ctx.globalAlpha = 1.0;
        }

        // 1. Surface View (Super-Earth landscape, incoming gravity waves, SAMS dome & shield)
        function drawSurfaceView(w, h) {
            drawStarfield(w, h);
            const cx = w / 2;
            const cy = h / 2 + 50;

            // Massive Super-Earth Crimson Horizon
            const horizonGrad = ctx.createLinearGradient(0, cy - 80, 0, h);
            horizonGrad.addColorStop(0, '#7f1d1d');
            horizonGrad.addColorStop(0.3, '#450a0a');
            horizonGrad.addColorStop(1, '#020617');
            ctx.fillStyle = horizonGrad;
            ctx.fillRect(0, cy - 80, w, h - cy + 80);

            // Ground Surface Line
            ctx.strokeStyle = '#f87171';
            ctx.lineWidth = 3;
            ctx.beginPath();
            ctx.moveTo(0, cy);
            ctx.lineTo(w, cy);
            ctx.stroke();

            // Incoming Gravitational Compression Waves (Red/Orange downward undulating waves)
            if (isRunning) {
                ctx.strokeStyle = 'rgba(248, 113, 113, 0.4)';
                ctx.lineWidth = 2;
                for (let i = 0; i < 5; i++) {
                    let waveY = cy - 180 + ((simulationTime * 2 + i * 40) % 200);
                    ctx.beginPath();
                    for (let x = 0; x < w; x += 20) {
                        let wy = waveY + Math.sin(x * 0.02 + simulationTime * 0.05) * 10;
                        if (x === 0) ctx.moveTo(x, wy);
                        else ctx.lineTo(x, wy);
                    }
                    ctx.stroke();
                }
            }

            // Dome Habitat Position
            let domeX = cx;
            let domeY = cy;
            let domeRadius = 75;

            // SAMS Kinetic Damping Bubble (Force-field)
            if (samsActive) {
                dampingEfficiency = 99.8;
                if (structuralIntegrity < 100) structuralIntegrity = Math.min(100, structuralIntegrity + 0.5);

                const shieldGrad = ctx.createRadialGradient(domeX, domeY - 30, domeRadius * 0.5, domeX, domeY - 30, domeRadius * 1.4);
                shieldGrad.addColorStop(0, 'rgba(0, 243, 255, 0.35)');
                shieldGrad.addColorStop(0.7, 'rgba(139, 92, 246, 0.2)');
                shieldGrad.addColorStop(1, 'transparent');
                ctx.fillStyle = shieldGrad;
                ctx.beginPath();
                ctx.arc(domeX, domeY, domeRadius * 1.4, Math.PI, 0, false);
                ctx.fill();

                ctx.strokeStyle = '#00f3ff';
                ctx.lineWidth = 2;
                ctx.beginPath();
                ctx.arc(domeX, domeY, domeRadius * 1.4, Math.PI, 0, false);
                ctx.stroke();

                // Counter-resonance wave rings
                ctx.strokeStyle = 'rgba(16, 185, 129, 0.6)';
                ctx.lineWidth = 1.5;
                let ringRadius = domeRadius + ((simulationTime * 3) % 40);
                ctx.beginPath();
                ctx.arc(domeX, domeY, ringRadius, Math.PI, 0, false);
                ctx.stroke();
            } else {
                dampingEfficiency = 0.0;
                structuralIntegrity = Math.max(0, structuralIntegrity - 0.8);
                if (structuralIntegrity <= 0) structuralIntegrity = 0;
            }

            // Draw Dome Structure
            ctx.fillStyle = '#1e293b';
            ctx.strokeStyle = samsActive ? '#10b981' : '#f43f5e';
            ctx.lineWidth = 3;
            ctx.beginPath();
            ctx.arc(domeX, domeY, domeRadius, Math.PI, 0, false);
            ctx.closePath();
            ctx.fill();
            ctx.stroke();

            // Dome grid lines
            ctx.strokeStyle = samsActive ? 'rgba(0, 243, 255, 0.4)' : 'rgba(244, 63, 94, 0.6)';
            ctx.lineWidth = 1;
            ctx.beginPath();
            ctx.moveTo(domeX - domeRadius, domeY);
            ctx.lineTo(domeX + domeRadius, domeY);
            ctx.moveTo(domeX, domeY - domeRadius);
            ctx.lineTo(domeX, domeY);
            ctx.stroke();

            // Update UI telemetry bars
            document.getElementById('val-integrity').innerText = structuralIntegrity.toFixed(1) + "%";
            document.getElementById('bar-integrity').style.width = structuralIntegrity + "%";
            document.getElementById('val-efficiency').innerText = dampingEfficiency.toFixed(1) + "%";
            document.getElementById('bar-efficiency').style.width = dampingEfficiency + "%";
            document.getElementById('hud-int-g').innerText = samsActive ? "1.00G (Estável)" : (planetGravity.toFixed(1) + "G (FATAL!)");
        }

        // 2. Internal View (Safe citizens & stable internal 1.0G gravity)
        function drawInternalView(w, h) {
            drawStarfield(w, h);
            const cx = w / 2;
            const cy = h / 2;

            // Internal Habitat Room Frame
            ctx.fillStyle = '#0f172a';
            ctx.strokeStyle = '#00f3ff';
            ctx.lineWidth = 4;
            ctx.strokeRect(cx - 180, cy - 120, 360, 240);
            ctx.fillRect(cx - 180, cy - 120, 360, 240);

            // Floor line
            ctx.strokeStyle = '#10b981';
            ctx.lineWidth = 4;
            ctx.beginPath();
            ctx.moveTo(cx - 180, cy + 120);
            ctx.lineTo(cx + 180, cy + 120);
            ctx.stroke();

            // Draw Habitat interior details (Control consoles & citizens)
            ctx.fillStyle = '#38bdf8';
            ctx.fillRect(cx - 140, cy + 60, 80, 60); // Console 1
            ctx.fillRect(cx + 60, cy + 60, 80, 60);  // Console 2

            // Citizen figures standing comfortably
            ctx.fillStyle = '#f8fafc';
            // Citizen 1
            ctx.beginPath();
            ctx.arc(cx - 100, cy + 10, 8, 0, Math.PI * 2); // Head
            ctx.fill();
            ctx.fillRect(cx - 104, cy + 18, 8, 30);       // Body

            // Citizen 2
            ctx.beginPath();
            ctx.arc(cx + 100, cy + 10, 8, 0, Math.PI * 2); // Head
            ctx.fill();
            ctx.fillRect(cx + 96, cy + 18, 8, 30);       // Body

            // Internal Gravity HUD Badge inside canvas
            ctx.fillStyle = 'rgba(16, 185, 129, 0.2)';
            ctx.strokeStyle = '#10b981';
            ctx.lineWidth = 1;
            ctx.fillRect(cx - 110, cy - 100, 220, 30);
            ctx.strokeRect(cx - 110, cy - 100, 220, 30);

            ctx.fillStyle = '#10b981';
            ctx.font = '12px Orbitron';
            ctx.fillText("GRAVIDADE INTERNA: 1.00G", cx - 95, cy - 81);
        }

        // 3. Molecular / Piezo View (Zoom into walls with MR fluid & piezo crystals)
        function drawMolecularView(w, h) {
            drawStarfield(w, h);
            const cx = w / 2;
            const cy = h / 2;

            // Draw structural wall matrix channel
            ctx.fillStyle = '#1e293b';
            ctx.strokeStyle = '#8b5cf6';
            ctx.lineWidth = 3;
            ctx.strokeRect(cx - 200, cy - 100, 400, 200);
            ctx.fillRect(cx - 200, cy - 100, 400, 200);

            // Piezoelectric crystals grid
            for (let x = cx - 170; x < cx + 180; x += 50) {
                for (let y = cy - 70; y < cy + 80; y += 50) {
                    let pulse = Math.sin(simulationTime * 0.1 + x) * 6;
                    ctx.fillStyle = '#00f3ff';
                    ctx.beginPath();
                    ctx.arc(x, y, 8 + pulse * 0.3, 0, Math.PI * 2);
                    ctx.fill();
                }
            }

            // Magnetorheological fluid channels
            ctx.strokeStyle = '#10b981';
            ctx.lineWidth = 4;
            ctx.beginPath();
            ctx.moveTo(cx - 170, cy);
            ctx.lineTo(cx + 170, cy);
            ctx.stroke();

            // Overlay label
            ctx.fillStyle = '#00f3ff';
            ctx.font = '12px Orbitron';
            ctx.fillText(`MALHA PIEZOELÉTRICA (${piezoFreq.toFixed(1)} kHz)`, cx - 170, cy - 125);
            ctx.fillStyle = '#10b981';
            ctx.font = '11px JetBrains Mono';
            ctx.fillText(`FLUIDO MR VISCOSIDADE: ${mrViscosity} Pa·s`, cx - 170, cy + 135);
        }

        // Main Animation Loop
        function simulationLoop() {
            const w = canvas.clientWidth;
            const h = canvas.clientHeight;

            if (canvas.width !== w * window.devicePixelRatio || canvas.height !== h * window.devicePixelRatio) {
                canvas.width = w * window.devicePixelRatio;
                canvas.height = h * window.devicePixelRatio;
                ctx.scale(window.devicePixelRatio, window.devicePixelRatio);
            }

            ctx.clearRect(0, 0, w, h);

            if (isRunning) {
                simulationTime += 1 * timeScale;
            }

            ctx.save();
            if (canvasShakeTimer > 0) {
                canvasShakeTimer--;
                let offsetX = (Math.random() - 0.5) * 8;
                let offsetY = (Math.random() - 0.5) * 8;
                ctx.translate(offsetX, offsetY);
            }

            if (currentView === 'surface') {
                drawSurfaceView(w, h);
            } else if (currentView === 'internal') {
                drawInternalView(w, h);
            } else if (currentView === 'molecular') {
                drawMolecularView(w, h);
            }
            ctx.restore();

            requestAnimationFrame(simulationLoop);
        }

        window.onload = function() {
            addLog("Sistema SAMS inicializado. Malha de amortecimento cinético pronta.");
            requestAnimationFrame(simulationLoop);
        };
    </script>
</body>
</html>
