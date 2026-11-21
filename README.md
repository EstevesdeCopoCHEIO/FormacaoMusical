# FormacaoMusical
Laboratorio de formação musical
<!DOCTYPE html>
<html lang="pt-PT">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Laboratório de Timbres — Formação Auditiva e Orquestração</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Google Fonts: Inter & Fraunces -->
    <link href="https://fonts.googleapis.com/css2?family=Fraunces:opsz,wght@9..144,600;9..144,700&family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
    <!-- FontAwesome para Ícones -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Soundfont-Player para amostras reais de instrumentos -->
    <script src="https://cdn.jsdelivr.net/npm/soundfont-player@0.12.0/dist/soundfont-player.min.js"></script>
    
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    fontFamily: {
                        sans: ['Inter', 'sans-serif'],
                        serif: ['Fraunces', 'serif'],
                    }
                }
            }
        }
    </script>
    <style>
        body {
            background-color: #FAF8F5;
            background-image: radial-gradient(#E5E2DC 0.8px, transparent 0.8px);
            background-size: 24px 24px;
        }
        ::-webkit-scrollbar { width: 6px; height: 6px; }
        ::-webkit-scrollbar-track { background: #F5F5F4; }
        ::-webkit-scrollbar-thumb { background: #D6D3D1; border-radius: 3px; }
        ::-webkit-scrollbar-thumb:hover { background: #A8A29E; }
    </style>
</head>
<body class="text-slate-900 antialiased min-h-screen flex flex-col">

    <!-- Cabeçalho da Sala de Conservatório -->
    <header class="bg-slate-950 text-white border-b border-amber-500/30 sticky top-0 z-30 shadow-md">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-3.5 flex flex-col lg:flex-row justify-between items-center gap-4">
            <div class="flex items-center gap-3.5 w-full lg:w-auto justify-between lg:justify-start">
                <div class="flex items-center gap-3">
                    <div class="w-11 h-11 rounded-xl bg-amber-500/15 text-amber-400 flex items-center justify-center shadow-inner border border-amber-400/30">
                        <i class="fa-solid fa-ear-listen text-xl"></i>
                    </div>
                    <div>
                        <div class="flex items-center gap-2">
                            <h1 class="font-serif text-xl sm:text-2xl font-bold text-stone-50 tracking-tight">Laboratório de Timbres</h1>
                            <span class="hidden sm:inline-flex items-center px-2 py-0.5 rounded-md text-[10px] font-bold uppercase tracking-wider bg-amber-500/20 text-amber-300 border border-amber-400/30">
                                Sala Acústica HD
                            </span>
                        </div>
                        <p class="text-xs text-slate-400 font-medium">Formação Auditiva e Orquestração &bull; 20 Instrumentos</p>
                    </div>
                </div>

                <!-- Indicador de Estado Sonoro (Respeita Sigilo Estrito no Modo Desafio) -->
                <div id="audio-status-badge" class="flex items-center gap-2 px-3.5 py-1.5 rounded-full bg-slate-900 border border-slate-700 text-xs font-medium text-slate-200 transition-all">
                    <span id="status-dot" class="w-2.5 h-2.5 rounded-full bg-emerald-400"></span>
                    <span id="status-text">Orquestra pronta</span>
                </div>
            </div>

            <!-- Navegação Principal (3 Separadores) -->
            <nav class="flex bg-slate-900 p-1 rounded-xl w-full lg:w-auto border border-slate-800">
                <button id="tab-explore" onclick="switchTab('explore')" class="flex-1 lg:flex-none px-4 py-2 rounded-lg text-xs sm:text-sm font-semibold transition-all bg-amber-500 text-slate-950 shadow-sm flex items-center justify-center gap-2">
                    <i class="fa-solid fa-compass"></i>
                    <span>Explorar Orquestra</span>
                </button>
                <button id="tab-compare" onclick="switchTab('compare')" class="flex-1 lg:flex-none px-4 py-2 rounded-lg text-xs sm:text-sm font-semibold text-slate-300 hover:text-white transition-all flex items-center justify-center gap-2">
                    <i class="fa-solid fa-code-compare text-amber-400"></i>
                    <span>Comparação A/B</span>
                </button>
                <button id="tab-quiz" onclick="switchTab('quiz')" class="flex-1 lg:flex-none px-4 py-2 rounded-lg text-xs sm:text-sm font-semibold text-slate-300 hover:text-white transition-all flex items-center justify-center gap-2">
                    <i class="fa-solid fa-graduation-cap text-emerald-400"></i>
                    <span>Desafio Auditivo (10)</span>
                </button>
            </nav>
        </div>
    </header>

    <!-- Conteúdo Principal -->
    <main class="flex-grow max-w-7xl w-full mx-auto px-4 sm:px-6 lg:px-8 py-6 sm:py-8">

        <!-- Nota Pedagógica do Professor -->
        <div class="mb-6 bg-white border-l-4 border-amber-500 border-y border-r border-stone-200 rounded-r-2xl rounded-l-md p-4 shadow-sm flex items-start gap-3.5 text-sm">
            <div class="mt-0.5 w-8 h-8 rounded-lg bg-amber-50 text-amber-700 flex items-center justify-center shrink-0 border border-amber-200">
                <i class="fa-solid fa-chalkboard-user"></i>
            </div>
            <div>
                <p class="font-bold text-slate-900">Nota do Professor de Educação Musical:</p>
                <p id="teacher-banner-text" class="text-slate-600 mt-0.5 leading-relaxed">
                    Para distinguir qualquer instrumento, escuta com atenção três momentos: o <strong>ataque inicial</strong> (o roçar do arco, o sopro na palheta ou o impacto percutido), o <strong>corpo harmónico</strong> e a <strong>ressonância</strong>. Experimenta a <em>Nota Longa Sustentada</em> para isolar estas características!
                </p>
            </div>
        </div>

        <!-- ========================================================== -->
        <!-- SEPARADOR 1: EXPLORAR ORQUESTRA (20 INSTRUMENTOS + FICHA)  -->
        <!-- ========================================================== -->
        <section id="view-explore" class="space-y-6">
            <!-- Controlos de Filtro e Frase Musical -->
            <div class="bg-white p-4 rounded-2xl border border-stone-200 shadow-sm flex flex-col xl:flex-row xl:items-center justify-between gap-4">
                <div class="flex flex-wrap gap-1.5" id="explore-family-filters">
                    <button onclick="setExploreFamily('all')" data-fam="all" class="exp-fam-btn px-3.5 py-2 rounded-xl text-xs sm:text-sm font-semibold bg-slate-900 text-white shadow-sm transition-all">
                        Todas (20)
                    </button>
                    <button onclick="setExploreFamily('strings')" data-fam="strings" class="exp-fam-btn px-3.5 py-2 rounded-xl text-xs sm:text-sm font-medium bg-stone-50 text-slate-700 border border-stone-200 hover:bg-amber-50 transition-all">
                        Cordas (6)
                    </button>
                    <button onclick="setExploreFamily('woodwinds')" data-fam="woodwinds" class="exp-fam-btn px-3.5 py-2 rounded-xl text-xs sm:text-sm font-medium bg-stone-50 text-slate-700 border border-stone-200 hover:bg-emerald-50 transition-all">
                        Madeiras (5)
                    </button>
                    <button onclick="setExploreFamily('brass')" data-fam="brass" class="exp-fam-btn px-3.5 py-2 rounded-xl text-xs sm:text-sm font-medium bg-stone-50 text-slate-700 border border-stone-200 hover:bg-orange-50 transition-all">
                        Metais (4)
                    </button>
                    <button onclick="setExploreFamily('keys')" data-fam="keys" class="exp-fam-btn px-3.5 py-2 rounded-xl text-xs sm:text-sm font-medium bg-stone-50 text-slate-700 border border-stone-200 hover:bg-blue-50 transition-all">
                        Teclas (3)
                    </button>
                    <button onclick="setExploreFamily('percussion')" data-fam="percussion" class="exp-fam-btn px-3.5 py-2 rounded-xl text-xs sm:text-sm font-medium bg-stone-50 text-slate-700 border border-stone-200 hover:bg-purple-50 transition-all">
                        Percussão (2)
                    </button>
                </div>

                <div class="flex items-center gap-2.5 bg-stone-50 px-3.5 py-2 rounded-xl border border-stone-200 text-xs sm:text-sm shrink-0">
                    <span class="text-slate-500 font-semibold"><i class="fa-solid fa-music mr-1 text-amber-600"></i>Frase Musical:</span>
                    <select id="explore-phrase-select" class="bg-transparent font-bold text-slate-900 focus:outline-none cursor-pointer">
                        <option value="arpeggio">Arpejo Clássico (Dó-Mi-Sol-Dó5)</option>
                        <option value="melody">Motivo Lírico Expressivo</option>
                        <option value="scale">Escala Ascendente (Dó Maior)</option>
                        <option value="fanfare">Chamada Rítmica (Fanfarra)</option>
                        <option value="long_note">Nota Longa Sustentada (2.4s)</option>
                    </select>
                </div>
            </div>

            <!-- Layout Principal: Grelha de Instrumentos (Esquerda) + Ficha Acústica (Direita) -->
            <div class="grid grid-cols-1 lg:grid-cols-12 gap-6 items-start">
                <!-- Grelha de Cartões Clicáveis -->
                <div id="explore-grid" class="lg:col-span-8 grid grid-cols-1 sm:grid-cols-2 xl:grid-cols-3 gap-3.5">
                    <!-- Injetado via JavaScript -->
                </div>

                <!-- Painel Lateral: Ficha Acústica do Professor -->
                <aside class="lg:col-span-4 bg-white rounded-3xl border border-stone-200 shadow-md overflow-hidden sticky top-24">
                    <div class="bg-slate-900 text-white p-5 border-b border-amber-500/30">
                        <div class="flex items-center justify-between">
                            <span class="text-[11px] font-bold uppercase tracking-widest text-amber-400">Ficha Acústica do Professor</span>
                            <span id="sheet-family-badge" class="px-2.5 py-0.5 rounded-full text-[11px] font-semibold bg-white/10 text-stone-200">Cordas</span>
                        </div>
                        <div class="flex items-center gap-3 mt-3">
                            <div id="sheet-icon" class="w-12 h-12 rounded-2xl bg-amber-500/20 border border-amber-400/30 text-amber-300 flex items-center justify-center text-2xl shrink-0">
                                🎻
                            </div>
                            <div>
                                <h2 id="sheet-name" class="font-serif text-2xl font-bold text-white">Violino</h2>
                                <p id="sheet-register" class="text-xs text-slate-300 mt-0.5">Tessitura: Agudo (Soprano)</p>
                            </div>
                        </div>
                    </div>

                    <div class="p-5 space-y-4 text-sm">
                        <div>
                            <h3 class="text-[11px] font-bold uppercase tracking-wider text-slate-400 mb-1">Mecanismo de Produção Sonora</h3>
                            <p id="sheet-production" class="text-slate-700 leading-relaxed"></p>
                        </div>

                        <div class="pt-3 border-t border-stone-100">
                            <h3 class="text-[11px] font-bold uppercase tracking-wider text-slate-400 mb-1">Assinatura Harmónica e Timbre</h3>
                            <p id="sheet-timbre" class="text-slate-700 leading-relaxed"></p>
                        </div>

                        <div class="bg-amber-50/80 border border-amber-200/80 rounded-2xl p-3.5">
                            <h3 class="text-[11px] font-bold uppercase tracking-wider text-amber-800 mb-1 flex items-center gap-1.5">
                                <i class="fa-solid fa-ear-listen"></i>
                                <span>Dica Auditiva de Identificação</span>
                            </h3>
                            <p id="sheet-tip" class="text-amber-950 text-xs sm:text-sm leading-relaxed font-medium"></p>
                        </div>

                        <button id="btn-sheet-replay" onclick="replayActiveExploreInstrument()" class="w-full py-3.5 px-4 rounded-xl bg-slate-900 hover:bg-slate-800 active:scale-[0.99] text-white font-bold text-sm shadow transition-all flex items-center justify-center gap-2">
                            <i class="fa-solid fa-volume-high text-amber-400"></i>
                            <span>Ouvir Novamente</span>
                        </button>
                    </div>
                </aside>
            </div>
        </section>

        <!-- ========================================================== -->
        <!-- SEPARADOR 2: COMPARAÇÃO A/B                                -->
        <!-- ========================================================== -->
        <section id="view-compare" class="hidden max-w-5xl mx-auto space-y-6">
            <div class="bg-white rounded-3xl border border-stone-200 shadow-sm p-6 sm:p-8">
                <div class="flex flex-col lg:flex-row lg:items-center justify-between gap-4 pb-6 border-b border-stone-200">
                    <div>
                        <span class="text-xs font-bold uppercase tracking-wider text-amber-700">Treino de Discriminação Fina</span>
                        <h2 class="font-serif text-2xl font-bold text-slate-900 mt-1">Comparação Direta A / B</h2>
                        <p class="text-sm text-slate-600 mt-1">Compara lado a lado instrumentos que frequentemente se confundem na audição.</p>
                    </div>

                    <!-- Atalhos Rápidos para Pares Clássicos -->
                    <div class="flex flex-col gap-1.5">
                        <span class="text-[11px] font-bold uppercase tracking-wider text-slate-400">Pares Clássicos Sugeridos:</span>
                        <div class="flex flex-wrap gap-1.5">
                            <button onclick="setComparePair('violin', 'viola')" class="px-2.5 py-1.5 rounded-lg bg-amber-50 hover:bg-amber-100 text-amber-950 border border-amber-200 text-xs font-semibold transition-all">
                                Violino vs. Viola d'Arco
                            </button>
                            <button onclick="setComparePair('oboe', 'clarinet')" class="px-2.5 py-1.5 rounded-lg bg-emerald-50 hover:bg-emerald-100 text-emerald-950 border border-emerald-200 text-xs font-semibold transition-all">
                                Oboé vs. Clarinete
                            </button>
                            <button onclick="setComparePair('french_horn', 'trombone')" class="px-2.5 py-1.5 rounded-lg bg-orange-50 hover:bg-orange-100 text-orange-950 border border-orange-200 text-xs font-semibold transition-all">
                                Trompa vs. Trombone
                            </button>
                            <button onclick="setComparePair('piano', 'harpsichord')" class="px-2.5 py-1.5 rounded-lg bg-blue-50 hover:bg-blue-100 text-blue-950 border border-blue-200 text-xs font-semibold transition-all">
                                Piano vs. Cravo
                            </button>
                            <button onclick="setComparePair('cello', 'bassoon')" class="px-2.5 py-1.5 rounded-lg bg-purple-50 hover:bg-purple-100 text-purple-950 border border-purple-200 text-xs font-semibold transition-all">
                                Violoncelo vs. Fagote
                            </button>
                            <button onclick="setComparePair('marimba', 'xylophone')" class="px-2.5 py-1.5 rounded-lg bg-stone-100 hover:bg-stone-200 text-slate-900 border border-stone-300 text-xs font-semibold transition-all">
                                Marimba vs. Xilofone
                            </button>
                        </div>
                    </div>
                </div>

                <!-- Controlos Centrais de Frase e Alternância A -> B -->
                <div class="my-6 flex flex-wrap items-center justify-between gap-4 bg-stone-50 p-4 rounded-2xl border border-stone-200">
                    <div class="flex items-center gap-2.5">
                        <span class="text-xs font-bold uppercase tracking-wider text-slate-500">Frase Musical:</span>
                        <select id="compare-phrase-select" class="bg-white border border-stone-300 rounded-xl px-3.5 py-2 text-sm font-bold text-slate-900 focus:outline-none focus:ring-2 focus:ring-amber-500">
                            <option value="melody">Motivo Lírico Expressivo</option>
                            <option value="arpeggio">Arpejo Clássico (Dó-Mi-Sol-Dó5)</option>
                            <option value="scale">Escala Ascendente (Dó Maior)</option>
                            <option value="fanfare">Chamada Rítmica (Fanfarra)</option>
                            <option value="long_note">Nota Longa Sustentada (2.4s)</option>
                        </select>
                    </div>

                    <button id="btn-alternate-ab" onclick="playAlternateAB()" class="px-5 py-2.5 rounded-xl bg-slate-900 hover:bg-slate-800 text-white font-bold text-xs sm:text-sm shadow-sm transition-all flex items-center gap-2">
                        <i class="fa-solid fa-right-left text-amber-400"></i>
                        <span>Alternar A &rarr; B Automaticamente</span>
                    </button>
                </div>

                <!-- Painéis Lado a Lado A e B -->
                <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                    <!-- Painel A -->
                    <div id="compare-box-a" class="rounded-2xl border-2 border-slate-300 bg-white p-5 flex flex-col justify-between transition-all">
                        <div>
                            <div class="flex items-center justify-between gap-2 mb-4">
                                <span class="px-3 py-1 rounded-lg bg-slate-900 text-amber-400 font-bold text-xs uppercase tracking-wider">Instrumento A</span>
                                <select id="select-compare-a" onchange="renderComparePanels()" class="bg-stone-50 border border-stone-300 rounded-xl px-3 py-1.5 text-sm font-bold text-slate-900 focus:outline-none focus:ring-2 focus:ring-amber-500 max-w-[210px]">
                                    <!-- Preenchido via JS -->
                                </select>
                            </div>
                            <div id="compare-info-a" class="space-y-3 text-sm text-slate-700"></div>
                        </div>
                        <button onclick="playCompareSingle('a')" class="mt-6 w-full py-3.5 px-4 rounded-xl bg-slate-900 hover:bg-slate-800 text-white font-bold text-sm shadow transition-all flex items-center justify-center gap-2">
                            <i class="fa-solid fa-play text-amber-400"></i>
                            <span>Tocar A</span>
                        </button>
                    </div>

                    <!-- Painel B -->
                    <div id="compare-box-b" class="rounded-2xl border-2 border-amber-300 bg-amber-50/15 p-5 flex flex-col justify-between transition-all">
                        <div>
                            <div class="flex items-center justify-between gap-2 mb-4">
                                <span class="px-3 py-1 rounded-lg bg-amber-600 text-white font-bold text-xs uppercase tracking-wider">Instrumento B</span>
                                <select id="select-compare-b" onchange="renderComparePanels()" class="bg-white border border-stone-300 rounded-xl px-3 py-1.5 text-sm font-bold text-slate-900 focus:outline-none focus:ring-2 focus:ring-amber-500 max-w-[210px]">
                                    <!-- Preenchido via JS -->
                                </select>
                            </div>
                            <div id="compare-info-b" class="space-y-3 text-sm text-slate-700"></div>
                        </div>
                        <button onclick="playCompareSingle('b')" class="mt-6 w-full py-3.5 px-4 rounded-xl bg-amber-600 hover:bg-amber-700 text-white font-bold text-sm shadow transition-all flex items-center justify-center gap-2">
                            <i class="fa-solid fa-play"></i>
                            <span>Tocar B</span>
                        </button>
                    </div>
                </div>

                <!-- Resumo Comparativo Pedagógico -->
                <div id="compare-summary-box" class="mt-6 bg-stone-50 border border-stone-200 rounded-2xl p-4 sm:p-5 text-sm">
                    <!-- Preenchido dinamicamente -->
                </div>
            </div>
        </section>

        <!-- ========================================================== -->
        <!-- SEPARADOR 3: DESAFIO AUDITIVO (PROVA DE 10 PERGUNTAS)      -->
        <!-- ========================================================== -->
        <section id="view-quiz" class="hidden max-w-5xl mx-auto">
            
            <!-- Cabeçalho de Progresso (10 Perguntas) e Dificuldade -->
            <div class="bg-white rounded-2xl border border-stone-200 p-4 sm:p-5 mb-6 shadow-sm space-y-4">
                <div class="flex flex-col md:flex-row md:items-center justify-between gap-4">
                    <div class="flex items-center gap-5 sm:gap-6">
                        <div>
                            <span class="text-[11px] font-bold uppercase tracking-wider text-slate-400 block">Progresso da Prova</span>
                            <span id="quiz-q-current" class="text-2xl font-bold text-slate-900">1</span>
                            <span class="text-sm text-slate-400 font-semibold">/ 10</span>
                        </div>
                        <div class="h-8 w-px bg-stone-200"></div>
                        <div>
                            <span class="text-[11px] font-bold uppercase tracking-wider text-slate-400 block">Pontuação</span>
                            <span id="quiz-score-val" class="text-2xl font-bold text-emerald-600">0</span>
                            <span class="text-sm text-slate-400 font-semibold">/ 10</span>
                        </div>
                        <div class="h-8 w-px bg-stone-200"></div>
                        <div>
                            <span class="text-[11px] font-bold uppercase tracking-wider text-slate-400 block">Sequência</span>
                            <div class="flex items-center gap-1.5">
                                <i class="fa-solid fa-fire text-amber-500"></i>
                                <span id="quiz-streak-val" class="text-2xl font-bold text-slate-900">0</span>
                            </div>
                        </div>
                    </div>

                    <!-- Seletor de Dificuldade -->
                    <div class="flex flex-col">
                        <label for="quiz-difficulty" class="text-[10px] font-bold uppercase tracking-wider text-slate-400 mb-0.5">Nível de Dificuldade</label>
                        <select id="quiz-difficulty" onchange="resetQuizSession()" class="bg-stone-50 border border-stone-300 text-slate-900 text-xs sm:text-sm font-bold rounded-xl px-3.5 py-2 focus:outline-none focus:ring-2 focus:ring-amber-500">
                            <option value="easy">Iniciante (4 opções • Famílias distintas)</option>
                            <option value="medium" selected>Intermédio (4 opções • Próximas)</option>
                            <option value="conservatory">Conservatório (6 opções • Mesma família)</option>
                            <option value="hard">Hard (Todos os 20 Instrumentos)</option>
                        </select>
                    </div>
                </div>

                <!-- Barra de Progresso -->
                <div class="w-full bg-stone-100 h-2.5 rounded-full overflow-hidden border border-stone-200/70">
                    <div id="quiz-progress-fill" class="bg-amber-500 h-full transition-all duration-500" style="width: 10%;"></div>
                </div>
            </div>

            <!-- Cartão Ativo da Pergunta -->
            <div id="quiz-question-card" class="bg-white rounded-3xl border border-stone-200 shadow-md overflow-hidden">
                <!-- Palco Acústico Escuro com Osciloscópio -->
                <div class="bg-gradient-to-br from-slate-950 via-slate-900 to-slate-800 text-white p-6 sm:p-8 text-center relative border-b border-amber-500/30">
                    <canvas id="oscilloscope-canvas" class="w-full h-24 mb-5 rounded-2xl bg-black/40 border border-white/10"></canvas>

                    <div class="inline-flex items-center gap-2 px-3 py-1 rounded-full bg-amber-500/15 border border-amber-400/30 text-amber-300 text-xs font-semibold mb-2">
                        <i class="fa-solid fa-user-secret"></i>
                        <span id="quiz-difficulty-label">Nível Intermédio</span>
                    </div>

                    <h2 class="font-serif text-xl sm:text-2xl font-bold mb-1.5">Pergunta <span id="quiz-title-num">1</span> de 10: Qual é o instrumento misterioso?</h2>
                    <p class="text-slate-300 text-xs sm:text-sm mb-6">Podes repetir o som ou experimentar noutra frase musical antes de responder.</p>

                    <div class="flex flex-wrap items-center justify-center gap-3">
                        <button id="btn-quiz-mystery-play" onclick="playQuizMysterySound()" class="px-6 py-3.5 rounded-2xl bg-amber-500 hover:bg-amber-400 active:scale-95 text-slate-950 font-bold shadow-lg shadow-amber-500/25 transition-all flex items-center gap-2.5 text-sm sm:text-base">
                            <i class="fa-solid fa-play"></i>
                            <span>Ouvir Som Misterioso</span>
                        </button>

                        <div class="flex items-center gap-2 bg-white/10 border border-white/20 rounded-2xl px-3.5 py-2.5 text-xs sm:text-sm">
                            <span class="text-amber-300 font-semibold"><i class="fa-solid fa-music mr-1"></i>Frase:</span>
                            <select id="quiz-phrase-select" onchange="playQuizMysterySound()" class="bg-transparent font-bold text-white focus:outline-none cursor-pointer">
                                <option value="arpeggio" class="text-slate-900">Arpejo Clássico</option>
                                <option value="melody" class="text-slate-900">Motivo Lírico</option>
                                <option value="scale" class="text-slate-900">Escala Ascendente</option>
                                <option value="fanfare" class="text-slate-900">Chamada Rítmica</option>
                                <option value="long_note" class="text-slate-900">Nota Longa Sustentada</option>
                            </select>
                        </div>
                    </div>
                </div>

                <!-- Grelha de Opções de Resposta -->
                <div class="p-6 sm:p-8">
                    <div id="quiz-options-container">
                        <!-- Injetado via JavaScript -->
                    </div>

                    <!-- Feedback Pedagógico Pós-Resposta -->
                    <div id="quiz-feedback-panel" class="hidden mt-6 rounded-2xl p-5 border transition-all">
                        <div class="flex items-start gap-3.5">
                            <div id="quiz-fb-icon" class="w-10 h-10 rounded-full flex items-center justify-center shrink-0 text-lg"></div>
                            <div class="flex-grow">
                                <h3 id="quiz-fb-title" class="font-bold text-base sm:text-lg"></h3>
                                <p id="quiz-fb-body" class="text-sm mt-1.5 leading-relaxed"></p>

                                <div class="mt-4 pt-3.5 border-t border-black/10 flex flex-wrap items-center justify-between gap-3">
                                    <div class="flex flex-wrap gap-2">
                                        <button id="btn-quiz-hear-correct" class="text-xs font-bold uppercase tracking-wider px-3.5 py-2 rounded-xl bg-white hover:bg-stone-50 text-slate-900 border border-black/15 shadow-sm transition-all flex items-center gap-1.5">
                                            <i class="fa-solid fa-volume-high text-emerald-600"></i>
                                            <span>Ouvir o Correto</span>
                                        </button>
                                        <button id="btn-quiz-hear-choice" class="hidden text-xs font-bold uppercase tracking-wider px-3.5 py-2 rounded-xl bg-white hover:bg-stone-50 text-slate-900 border border-black/15 shadow-sm transition-all flex items-center gap-1.5">
                                            <i class="fa-solid fa-volume-high text-rose-600"></i>
                                            <span>Ouvir a Tua Escolha</span>
                                        </button>
                                    </div>

                                    <button id="btn-quiz-next" onclick="nextQuizStep()" class="px-5 py-2.5 rounded-xl bg-slate-900 hover:bg-slate-800 text-white font-semibold text-sm shadow transition-all flex items-center gap-2 ml-auto">
                                        <span>Próxima Pergunta</span>
                                        <i class="fa-solid fa-arrow-right"></i>
                                    </button>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Ecrã Final: Relatório Final de Avaliação Auditiva (Após 10.ª pergunta) -->
            <div id="quiz-report-card" class="hidden bg-white rounded-3xl border border-stone-200 shadow-lg overflow-hidden">
                <div class="bg-slate-950 text-white p-8 text-center border-b border-amber-500/30">
                    <div class="w-16 h-16 rounded-2xl bg-amber-500/20 border border-amber-400/40 text-amber-400 flex items-center justify-center mx-auto mb-4 text-3xl">
                        <i class="fa-solid fa-award"></i>
                    </div>
                    <span class="text-xs font-bold uppercase tracking-widest text-amber-400">Conservatório de Música &bull; Avaliação Concluída</span>
                    <h2 class="font-serif text-2xl sm:text-3xl font-bold mt-1">Relatório Final de Avaliação Auditiva</h2>

                    <div class="mt-6 inline-flex items-baseline gap-2 bg-white/10 px-6 py-3 rounded-2xl border border-white/15">
                        <span id="report-score" class="text-4xl sm:text-5xl font-bold text-amber-400">0</span>
                        <span class="text-lg text-slate-300 font-semibold">/ 10</span>
                        <span id="report-percent" class="ml-2 px-3 py-0.5 rounded-full text-xs font-bold bg-amber-500 text-slate-950">0%</span>
                    </div>

                    <p id="report-verdict-title" class="font-bold text-lg text-white mt-4"></p>
                    <p id="report-verdict-comment" class="text-sm text-slate-300 max-w-2xl mx-auto mt-1.5 leading-relaxed"></p>
                </div>

                <div class="p-6 sm:p-8">
                    <h3 class="text-xs font-bold uppercase tracking-wider text-slate-500 mb-3">Detalhe das 10 Questões Avaliadas:</h3>
                    <div id="report-questions-list" class="grid grid-cols-1 sm:grid-cols-2 gap-2.5 mb-8">
                        <!-- Injetado via JavaScript -->
                    </div>

                    <div class="flex flex-wrap items-center justify-center gap-3">
                        <button onclick="resetQuizSession()" class="px-7 py-3.5 rounded-2xl bg-amber-500 hover:bg-amber-400 text-slate-950 font-bold text-sm sm:text-base shadow-lg shadow-amber-500/25 transition-all flex items-center gap-2.5">
                            <i class="fa-solid fa-rotate-right"></i>
                            <span>Iniciar Nova Prova (10 Perguntas)</span>
                        </button>
                        <button onclick="switchTab('compare')" class="px-5 py-3.5 rounded-2xl bg-stone-100 hover:bg-stone-200 text-slate-800 font-semibold text-sm transition-all flex items-center gap-2">
                            <i class="fa-solid fa-code-compare text-amber-700"></i>
                            <span>Treinar Pares na Comparação A/B</span>
                        </button>
                    </div>
                </div>
            </div>
        </section>

    </main>

    <!-- Rodapé -->
    <footer class="bg-white border-t border-stone-200 mt-12 py-6">
        <div class="max-w-7xl mx-auto px-4 text-center text-xs text-slate-500">
            <p>Laboratório de Timbres &bull; Motor Acústico Híbrido (Amostras Orquestrais Reais <strong>MusyngKite</strong> + Reverberação de Sala de Concertos) &bull; Português de Portugal.</p>
        </div>
    </footer>

    <!-- ========================================================== -->
    <!-- SCRIPT COMPLETO: CATÁLOGO, ÁUDIO REAL, FALLBACK E LÓGICA   -->
    <!-- ========================================================== -->
    <script>
        // ----------------------------------------------------------
        // 1. CATÁLOGO COMPLETO DOS 20 INSTRUMENTOS (5 FAMÍLIAS)
        // ----------------------------------------------------------
        const INSTRUMENTS = [
            // FAMÍLIA: CORDAS (strings) - 6 Instrumentos
            {
                id: 'violin',
                sf: 'violin',
                name: 'Violino',
                family: 'strings',
                familyName: 'Cordas',
                icon: '🎻',
                octaveShift: 0,
                confusedWith: ['viola', 'flute', 'oboe'],
                register: 'Agudo (Soprano)',
                production: 'Fricção de um arco de crina de cavalo sobre 4 cordas afinadas em quintas (Sol3-Ré4-Lá4-Mi5).',
                timbre: 'Luminoso, brilhante, ágil e muito expressivo, com harmónicos agudos ricos e vibrato intenso.',
                tip: 'Procura o som agudo e cantante com o ligeiro atrito inicial da crina do arco na corda.'
            },
            {
                id: 'viola',
                sf: 'viola',
                name: "Viola d'Arco",
                family: 'strings',
                familyName: 'Cordas',
                icon: '🎻',
                octaveShift: -5,
                confusedWith: ['violin', 'cello', 'clarinet'],
                register: 'Médio (Contralto)',
                production: 'Caixa de ressonância maior que a do violino, afinada uma quinta justa abaixo (Dó3-Sol3-Ré4-Lá4).',
                timbre: 'Mais escuro, aveludado, introspetivo e ligeiramente anasalado que o violino, sem a corda Mi aguda.',
                tip: 'Tem o carácter do arco das cordas, mas com uma voz mais quente, madura e menos estridente que o violino.'
            },
            {
                id: 'cello',
                sf: 'cello',
                name: 'Violoncelo',
                family: 'strings',
                familyName: 'Cordas',
                icon: '🎻',
                octaveShift: -12,
                confusedWith: ['viola', 'contrabass', 'bassoon'],
                register: 'Grave / Tenor',
                production: 'Apoiado no solo por um espigão e tocado entre os joelhos, afinado uma oitava abaixo da viola d\'arco.',
                timbre: 'Profundo, encorpado, caloroso e nobre — considerado o timbre instrumental mais próximo da voz humana.',
                tip: 'Ressonância grave muito rica e aveludada, com ataque de arco bem definido e sustentação cheia.'
            },
            {
                id: 'contrabass',
                sf: 'contrabass',
                name: 'Contrabaixo',
                family: 'strings',
                familyName: 'Cordas',
                icon: '🎻',
                octaveShift: -24,
                confusedWith: ['cello', 'tuba', 'bassoon'],
                register: 'Muito Grave (Baixo)',
                production: 'O maior e mais grave instrumento das cordas friccionadas (cerca de 1,80m), afinado por quartas.',
                timbre: 'Escuro, cavernoso, pesado e profundo, sustentando a base harmónica da orquestra.',
                tip: 'Sente a vibração densa e muito grave da corda espessa sob o movimento lento do arco.'
            },
            {
                id: 'harp',
                sf: 'orchestral_harp',
                name: 'Harpa de Concerto',
                family: 'strings',
                familyName: 'Cordas',
                icon: '🪕',
                octaveShift: 0,
                confusedWith: ['guitar', 'piano', 'harpsichord'],
                register: 'Extenso (Grave a Agudo)',
                production: '47 cordas verticais dedilhadas com a polpa dos dedos de ambas as mãos, com 7 pedais de afinação.',
                timbre: 'Cristalino, etéreo, puro e altamente ressonante, com uma cauda sonora luminosa.',
                tip: 'Ataque suave e arredondado (sem palheta nem martelo) seguido de uma ressonância longa e pura.'
            },
            {
                id: 'guitar',
                sf: 'acoustic_guitar_nylon',
                name: 'Guitarra Clássica',
                family: 'strings',
                familyName: 'Cordas',
                icon: '🎸',
                octaveShift: -12,
                confusedWith: ['harp', 'harpsichord', 'piano'],
                register: 'Médio',
                production: '6 cordas de nylon dedilhadas sobre uma caixa acústica de madeira com abertura circular.',
                timbre: 'Íntimo, cálido, doce e amadeirado, com ataque imediato e decaimento natural mais curto que a harpa.',
                tip: 'Nota o toque direto nos dedos sobre a corda de nylon e o calor íntimo da caixa de madeira.'
            },

            // FAMÍLIA: MADEIRAS (woodwinds) - 5 Instrumentos
            {
                id: 'flute',
                sf: 'flute',
                name: 'Flauta Transversal',
                family: 'woodwinds',
                familyName: 'Madeiras',
                icon: '🪈',
                octaveShift: 12,
                confusedWith: ['violin', 'clarinet', 'oboe'],
                register: 'Agudo',
                production: 'Tubo cilíndrico sem palheta; o som resulta do sopro direcionado contra o rebordo (bisel) do bocal.',
                timbre: 'Puro, cristalino, ágil, luminoso e arejado, com poucos harmónicos superiores.',
                tip: 'Timbre muito limpo e transparente no registo agudo, com um sopro de ar subtil no início da nota.'
            },
            {
                id: 'oboe',
                sf: 'oboe',
                name: 'Oboé',
                family: 'woodwinds',
                familyName: 'Madeiras',
                icon: '🎷',
                octaveShift: 0,
                confusedWith: ['clarinet', 'alto_sax', 'violin'],
                register: 'Agudo / Médio-Agudo',
                production: 'Tubo cónico estreito de madeira de granadilha com palheta dupla de cana.',
                timbre: 'Penetrante, anasalado, expressivo e pastoril. É o instrumento que dá o "Lá" de afinação à orquestra.',
                tip: 'A cor distintamente anasalada e focada da palheta dupla é a sua impressão digital.'
            },
            {
                id: 'clarinet',
                sf: 'clarinet',
                name: 'Clarinete em Sib',
                family: 'woodwinds',
                familyName: 'Madeiras',
                icon: '🎶',
                octaveShift: 0,
                confusedWith: ['oboe', 'flute', 'alto_sax'],
                register: 'Médio / Agudo',
                production: 'Tubo cilíndrico com boquilha e uma palheta simples de cana presa por uma abraçadeira.',
                timbre: 'Aveludado, redondo, escuro e ligeiramente "oco" no registo médio (chalumeau), brilhante no agudo.',
                tip: 'Muito mais doce, redondo e aveludado que o oboé, sem qualquer timbre nasal.'
            },
            {
                id: 'bassoon',
                sf: 'bassoon',
                name: 'Fagote',
                family: 'woodwinds',
                familyName: 'Madeiras',
                icon: '🎵',
                octaveShift: -12,
                confusedWith: ['cello', 'trombone', 'french_horn'],
                register: 'Grave / Tenor',
                production: 'Longo tubo cónico de madeira dobrado em "U" com tudel metálico curvo e palheta dupla.',
                timbre: 'Amadeirado, grave, expressivo e nobre em legato, ou seco e humorístico em staccato.',
                tip: 'Une a profundidade do registo grave à textura amadeirada e anasalada da palheta dupla.'
            },
            {
                id: 'alto_sax',
                sf: 'alto_sax',
                name: 'Saxofone Alto',
                family: 'woodwinds',
                familyName: 'Madeiras',
                icon: '🎷',
                octaveShift: 0,
                confusedWith: ['clarinet', 'french_horn', 'oboe'],
                register: 'Médio',
                production: 'Corpo cónico em latão, mas pertence às Madeiras por utilizar boquilha com palheta simples.',
                timbre: 'Quente, encorpado, vocal, flexível e com brilho metálico na projeção sonora.',
                tip: 'Tem a maleabilidade da palheta do clarinete mas com maior potência, calor e brilho.'
            },

            // FAMÍLIA: METAIS (brass) - 4 Instrumentos
            {
                id: 'trumpet',
                sf: 'trumpet',
                name: 'Trompete',
                family: 'brass',
                familyName: 'Metais',
                icon: '🎺',
                octaveShift: 0,
                confusedWith: ['french_horn', 'trombone', 'alto_sax'],
                register: 'Agudo',
                production: 'Vibração dos lábios num bocal em taça, tubo cilíndrico com 3 pistões e campânula.',
                timbre: 'Brilhante, heroico, incisivo, claro e intensamente metálico.',
                tip: 'Ataque direto e brilho metálico agudo muito focado e penetrante.'
            },
            {
                id: 'french_horn',
                sf: 'french_horn',
                name: 'Trompa',
                family: 'brass',
                familyName: 'Metais',
                icon: '📯',
                octaveShift: -5,
                confusedWith: ['trombone', 'bassoon', 'alto_sax'],
                register: 'Médio / Grave',
                production: 'Longo tubo cónico enrolado em espiral com bocal em funil e campânula voltada para trás.',
                timbre: 'Nobre, quente, aveludado, solene e envolvente — faz a ponte entre madeiras e metais.',
                tip: 'É o som mais redondo, suave e "distante" dos metais, muito menos estridente que o trompete.'
            },
            {
                id: 'trombone',
                sf: 'trombone',
                name: 'Trombone de Vara',
                family: 'brass',
                familyName: 'Metais',
                icon: '🎺',
                octaveShift: -12,
                confusedWith: ['french_horn', 'tuba', 'bassoon'],
                register: 'Grave / Tenor',
                production: 'Tubo cilíndrico com vara deslizante telescópica que altera continuamente o comprimento do tubo.',
                timbre: 'Imponente, cheio, poderoso e solene, com forte presença metálica no registo grave.',
                tip: 'Mais direto e metálico que a trompa, numa tessitura grave encorpada.'
            },
            {
                id: 'tuba',
                sf: 'tuba',
                name: 'Tuba',
                family: 'brass',
                familyName: 'Metais',
                icon: '📯',
                octaveShift: -24,
                confusedWith: ['trombone', 'contrabass', 'bassoon'],
                register: 'Muito Grave (Baixo)',
                production: 'O maior e mais grave instrumento dos metais, com tubo cónico largo e campânula voltada para cima.',
                timbre: 'Profundo, maciço, redondo e aveludado no registo grave.',
                tip: 'Som de sopro muito grave e largo, com ataque mais pesado e redondo que o trombone.'
            },

            // FAMÍLIA: TECLAS E PERCUSSÃO MELÓDICA (keys) - 3 Instrumentos
            {
                id: 'piano',
                sf: 'acoustic_grand_piano',
                name: 'Piano de Cauda',
                family: 'keys',
                familyName: 'Teclas',
                icon: '🎹',
                octaveShift: 0,
                confusedWith: ['harpsichord', 'harp', 'marimba'],
                register: 'Completo (88 teclas)',
                production: 'Teclas acionam martelos revestidos a feltro que percutem cordas de aço sobre uma tábua harmónica.',
                timbre: 'Equilibrado, percussivo no ataque inicial e rico em sustentação harmónica.',
                tip: 'Sente o impacto macio do martelo de feltro seguido de uma ressonância cheia e limpa.'
            },
            {
                id: 'harpsichord',
                sf: 'harpsichord',
                name: 'Cravo',
                family: 'keys',
                familyName: 'Teclas',
                icon: '🎼',
                octaveShift: 0,
                confusedWith: ['piano', 'harp', 'guitar'],
                register: 'Médio / Agudo',
                production: 'Instrumento barroco onde cada tecla aciona um plectro que belisca a corda (sem martelos).',
                timbre: 'Brilhante, metálico, estaladiço, recortado e com decaimento rápido.',
                tip: 'O ruído característico de "beliscão" metálico e estaladiço distingue-o imediatamente do piano.'
            },
            {
                id: 'marimba',
                sf: 'marimba',
                name: 'Marimba',
                family: 'keys',
                familyName: 'Teclas',
                icon: '🪵',
                octaveShift: 0,
                confusedWith: ['xylophone', 'piano', 'harp'],
                register: 'Médio / Grave',
                production: 'Lâminas largas de madeira (pau-rosa) percutidas com baquetas macias sobre tubos ressoadores.',
                timbre: 'Quente, redondo, amadeirado, doce e ressonante.',
                tip: 'Percussão de madeira muito mais suave, grave e redonda que o xilofone.'
            },

            // FAMÍLIA: PERCUSSÃO ORQUESTRAL (percussion) - 2 Instrumentos
            {
                id: 'timpani',
                sf: 'timpani',
                name: 'Tímpanos',
                family: 'percussion',
                familyName: 'Percussão',
                icon: '🥁',
                octaveShift: -12,
                confusedWith: ['contrabass', 'tuba', 'marimba'],
                register: 'Grave',
                production: 'Membrana esticada sobre uma caldeira de cobre, percutida com baquetas de feltro e afinada por pedal.',
                timbre: 'Dramático, profundo, retumbante e ressonante, com altura musical definida.',
                tip: 'Impacto grave de pele/membrana seguido de uma longa ressonância cavernosa de cobre.'
            },
            {
                id: 'xylophone',
                sf: 'xylophone',
                name: 'Xilofone',
                family: 'percussion',
                familyName: 'Percussão',
                icon: '🦴',
                octaveShift: 12,
                confusedWith: ['marimba', 'harpsichord', 'piano'],
                register: 'Agudo',
                production: 'Lâminas estreitas de madeira dura percutidas com baquetas rígidas de ebonite ou madeira.',
                timbre: 'Seco, estaladiço, brilhante, agudo e muito curto (pouca sustentação).',
                tip: 'Batida seca e penetrante no agudo, com notas muito curtas e articuladas.'
            }
        ];

        // ----------------------------------------------------------
        // 2. AS 5 FRASES MUSICAIS PEDAGÓGICAS
        // ----------------------------------------------------------
        const MUSICAL_PHRASES = {
            arpeggio: [
                { note: 60, dur: 0.36 }, // Dó4
                { note: 64, dur: 0.36 }, // Mi4
                { note: 67, dur: 0.36 }, // Sol4
                { note: 72, dur: 0.55 }, // Dó5
                { note: 67, dur: 0.36 }, // Sol4
                { note: 64, dur: 0.36 }, // Mi4
                { note: 60, dur: 0.75 }  // Dó4
            ],
            melody: [
                { note: 67, dur: 0.42 }, // Sol4
                { note: 69, dur: 0.42 }, // Lá4
                { note: 71, dur: 0.42 }, // Si4
                { note: 74, dur: 0.65 }, // Ré5
                { note: 72, dur: 0.42 }, // Dó5
                { note: 71, dur: 0.42 }, // Si4
                { note: 69, dur: 0.42 }, // Lá4
                { note: 67, dur: 0.85 }  // Sol4
            ],
            scale: [
                { note: 60, dur: 0.28 }, // Dó4
                { note: 62, dur: 0.28 }, // Ré4
                { note: 64, dur: 0.28 }, // Mi4
                { note: 65, dur: 0.28 }, // Fá4
                { note: 67, dur: 0.28 }, // Sol4
                { note: 69, dur: 0.28 }, // Lá4
                { note: 71, dur: 0.28 }, // Si4
                { note: 72, dur: 0.75 }  // Dó5
            ],
            fanfare: [
                { note: 60, dur: 0.45 }, // Dó4
                { note: 67, dur: 0.25 }, // Sol4
                { note: 72, dur: 0.45 }, // Dó5
                { note: 76, dur: 0.32 }, // Mi5
                { note: 72, dur: 0.85 }  // Dó5
            ],
            long_note: [
                { note: 60, dur: 2.40 }  // Nota Longa Sustentada (2.4s)
            ]
        };

        // ----------------------------------------------------------
        // 3. MOTOR DE ÁUDIO REALISTA + REVERB + FALLBACK ACÚSTICO
        // ----------------------------------------------------------
        let audioCtx = null;
        let analyser = null;
        let masterBus = null;
        let reverbConvolver = null;
        const sfCache = {};
        let stopCallbacks = [];
        let playbackTimer = null;

        // Gera resposta impulsiva matemática de Sala de Concertos
        function buildConcertHallImpulse(ctx) {
            const sampleRate = ctx.sampleRate;
            const length = Math.floor(sampleRate * 1.65); // 1.65s de cauda acústica
            const impulse = ctx.createBuffer(2, length, sampleRate);
            for (let ch = 0; ch < 2; ch++) {
                const data = impulse.getChannelData(ch);
                for (let i = 0; i < length; i++) {
                    const env = Math.pow(1 - i / length, 2.5);
                    data[i] = (Math.random() * 2 - 1) * env * 0.42;
                }
            }
            return impulse;
        }

        function ensureAudioContext() {
            if (!audioCtx) {
                const AudioContextClass = window.AudioContext || window.webkitAudioContext;
                audioCtx = new AudioContextClass();

                analyser = audioCtx.createAnalyser();
                analyser.fftSize = 256;

                masterBus = audioCtx.createGain();
                masterBus.gain.value = 0.9;

                reverbConvolver = audioCtx.createConvolver();
                reverbConvolver.buffer = buildConcertHallImpulse(audioCtx);

                const dryGain = audioCtx.createGain();
                dryGain.gain.value = 0.86;

                const wetGain = audioCtx.createGain();
                wetGain.gain.value = 0.25;

                masterBus.connect(dryGain);
                masterBus.connect(reverbConvolver);
                reverbConvolver.connect(wetGain);

                dryGain.connect(analyser);
                wetGain.connect(analyser);
                analyser.connect(audioCtx.destination);
            }
            if (audioCtx.state === 'suspended') {
                audioCtx.resume();
            }
        }

        function updateStatusIndicator(mode, text) {
            const dot = document.getElementById('status-dot');
            const label = document.getElementById('status-text');
            if (!dot || !label) return;
            label.textContent = text;
            if (mode === 'loading') {
                dot.className = 'w-2.5 h-2.5 rounded-full bg-amber-400 animate-ping';
            } else if (mode === 'playing') {
                dot.className = 'w-2.5 h-2.5 rounded-full bg-sky-400 animate-pulse';
            } else {
                dot.className = 'w-2.5 h-2.5 rounded-full bg-emerald-400';
            }
        }

        function stopCurrentPlayback() {
            if (playbackTimer) {
                clearTimeout(playbackTimer);
                playbackTimer = null;
            }
            stopCallbacks.forEach(fn => {
                try { fn(); } catch (e) {}
            });
            stopCallbacks = [];
        }

        // Síntese Acústica de Reserva (Fallback Instantâneo com ADSR e Filtros)
        function playFallbackAcousticNote(inst, midiNote, startTime, duration) {
            const freq = 440 * Math.pow(2, (midiNote - 69) / 12);
            const osc = audioCtx.createOscillator();
            const filter = audioCtx.createBiquadFilter();
            const gain = audioCtx.createGain();

            let attack = 0.03;
            let decay = 0.15;
            let sustain = 0.65;
            let release = 0.18;
            let wave = 'triangle';
            let cutoff = 2400;

            if (inst.family === 'strings') {
                wave = (inst.id === 'harp' || inst.id === 'guitar') ? 'triangle' : 'sawtooth';
                attack = (inst.id === 'harp' || inst.id === 'guitar') ? 0.01 : 0.11;
                sustain = (inst.id === 'harp' || inst.id === 'guitar') ? 0.12 : 0.78;
                cutoff = 2000;
            } else if (inst.family === 'woodwinds') {
                wave = inst.id === 'flute' ? 'sine' : (inst.id === 'clarinet' ? 'square' : 'sawtooth');
                attack = 0.06;
                cutoff = inst.id === 'oboe' ? 3200 : 1800;
            } else if (inst.family === 'brass') {
                wave = 'sawtooth';
                attack = 0.05;
                cutoff = 2800;
            } else if (inst.family === 'keys' || inst.family === 'percussion') {
                wave = inst.id === 'harpsichord' ? 'sawtooth' : 'triangle';
                attack = 0.008;
                sustain = 0.15;
                cutoff = inst.id === 'timpani' ? 420 : 2600;
            }

            osc.type = wave;
            osc.frequency.setValueAtTime(freq, startTime);

            filter.type = 'lowpass';
            filter.frequency.setValueAtTime(cutoff, startTime);

            gain.gain.setValueAtTime(0.0001, startTime);
            gain.gain.linearRampToValueAtTime(0.32, startTime + attack);
            gain.gain.exponentialRampToValueAtTime(Math.max(0.001, 0.32 * sustain), startTime + attack + decay);
            gain.gain.setValueAtTime(Math.max(0.001, 0.32 * sustain), startTime + duration);
            gain.gain.exponentialRampToValueAtTime(0.0001, startTime + duration + release);

            osc.connect(filter);
            filter.connect(gain);
            gain.connect(masterBus);

            osc.start(startTime);
            osc.stop(startTime + duration + release + 0.05);

            stopCallbacks.push(() => {
                try { osc.stop(); } catch (e) {}
            });
        }

        // Carrega SoundFont MusyngKite com timeout de segurança e cache
        async function loadSoundfontWithTimeout(inst, secretMode = false) {
            ensureAudioContext();
            if (sfCache[inst.id]) {
                return sfCache[inst.id];
            }

            updateStatusIndicator('loading', secretMode ? 'A preparar som misterioso...' : `A carregar ${inst.name}...`);

            const loadPromise = Soundfont.instrument(audioCtx, inst.sf, {
                soundfont: 'MusyngKite',
                destination: masterBus,
                nameToUrl: (name, sf, format) => {
                    return `https://gleitz.github.io/midi-js-soundfonts/${sf}/${name}-${format || 'mp3'}.js`;
                }
            });

            // Timeout de 4.5s para evitar espera infinita em redes lentas
            const timeoutPromise = new Promise((_, reject) =>
                setTimeout(() => reject(new Error('Timeout SoundFont')), 4500)
            );

            try {
                const player = await Promise.race([loadPromise, timeoutPromise]);
                sfCache[inst.id] = player;
                return player;
            } catch (err) {
                console.warn(`Fallback acústico ativado para ${inst.name}:`, err.message);
                return null;
            }
        }

        // Função Principal de Reprodução de Frase Musical
        async function playInstrument(instrumentId, phraseKey = 'arpeggio', secretMode = false, onFinished = null) {
            stopCurrentPlayback();
            const inst = INSTRUMENTS.find(i => i.id === instrumentId);
            if (!inst) return;

            const player = await loadSoundfontWithTimeout(inst, secretMode);
            const phrase = MUSICAL_PHRASES[phraseKey] || MUSICAL_PHRASES.arpeggio;

            // REGRA CRÍTICA DE SIGILO: Em secretMode nunca mostra o nome do instrumento
            updateStatusIndicator('playing', secretMode ? 'Som Misterioso em reprodução' : `A tocar: ${inst.name}`);

            let now = audioCtx.currentTime + 0.05;
            let elapsed = 0;

            phrase.forEach(step => {
                const midiNote = step.note + inst.octaveShift;
                if (player) {
                    const node = player.play(midiNote, now, {
                        duration: step.dur * 1.15,
                        gain: 1.35
                    });
                    if (node && node.stop) {
                        stopCallbacks.push(() => node.stop());
                    }
                } else {
                    playFallbackAcousticNote(inst, midiNote, now, step.dur);
                }
                const stepSpacing = step.dur * 0.94;
                now += stepSpacing;
                elapsed += stepSpacing;
            });

            playbackTimer = setTimeout(() => {
                updateStatusIndicator('ready', 'Orquestra pronta');
                if (onFinished) onFinished();
            }, (elapsed + 0.35) * 1000);
        }

        // ----------------------------------------------------------
        // 4. OSCILOSCÓPIO EM TEMPO REAL (CANVAS)
        // ----------------------------------------------------------
        function startOscilloscopeLoop() {
            const canvas = document.getElementById('oscilloscope-canvas');
            if (!canvas) return;
            const ctx = canvas.getContext('2d');

            function renderFrame() {
                requestAnimationFrame(renderFrame);
                const rect = canvas.getBoundingClientRect();
                if (rect.width === 0 || rect.height === 0) return;

                if (canvas.width !== Math.floor(rect.width) || canvas.height !== Math.floor(rect.height)) {
                    canvas.width = Math.floor(rect.width);
                    canvas.height = Math.floor(rect.height);
                }

                const w = canvas.width;
                const h = canvas.height;
                ctx.clearRect(0, 0, w, h);

                // Linha central de referência
                ctx.strokeStyle = 'rgba(245, 158, 11, 0.16)';
                ctx.lineWidth = 1;
                ctx.beginPath();
                ctx.moveTo(0, h / 2);
                ctx.lineTo(w, h / 2);
                ctx.stroke();

                ctx.lineWidth = 2.5;
                ctx.strokeStyle = '#F59E0B';
                ctx.beginPath();

                if (!analyser) {
                    ctx.moveTo(0, h / 2);
                    ctx.lineTo(w, h / 2);
                    ctx.stroke();
                    return;
                }

                const bufferLen = analyser.frequencyBinCount;
                const dataArray = new Uint8Array(bufferLen);
                analyser.getByteTimeDomainData(dataArray);

                const sliceWidth = w / bufferLen;
                let x = 0;

                for (let i = 0; i < bufferLen; i++) {
                    const v = dataArray[i] / 128.0;
                    const y = (v * h) / 2;
                    if (i === 0) ctx.moveTo(x, y);
                    else ctx.lineTo(x, y);
                    x += sliceWidth;
                }
                ctx.lineTo(w, h / 2);
                ctx.stroke();
            }

            renderFrame();
        }

        // ----------------------------------------------------------
        // 5. NAVEGAÇÃO ENTRE SEPARADORES
        // ----------------------------------------------------------
        let currentTab = 'explore';

        function switchTab(tabName) {
            stopCurrentPlayback();
            updateStatusIndicator('ready', 'Orquestra pronta');
            currentTab = tabName;

            const tabs = ['explore', 'compare', 'quiz'];
            tabs.forEach(t => {
                const btn = document.getElementById(`tab-${t}`);
                const view = document.getElementById(`view-${t}`);
                if (t === tabName) {
                    btn.className = 'flex-1 lg:flex-none px-4 py-2 rounded-lg text-xs sm:text-sm font-semibold transition-all bg-amber-500 text-slate-950 shadow-sm flex items-center justify-center gap-2';
                    view.classList.remove('hidden');
                } else {
                    btn.className = 'flex-1 lg:flex-none px-4 py-2 rounded-lg text-xs sm:text-sm font-semibold text-slate-300 hover:text-white transition-all flex items-center justify-center gap-2';
                    view.classList.add('hidden');
                }
            });

            if (tabName === 'quiz' && !quizState.target) {
                resetQuizSession();
            }
        }

        // ----------------------------------------------------------
        // 6. SEPARADOR 1: EXPLORAR ORQUESTRA
        // ----------------------------------------------------------
        let exploreFamily = 'all';
        let activeExploreId = 'violin';

        function setExploreFamily(family) {
            exploreFamily = family;
            document.querySelectorAll('.exp-fam-btn').forEach(btn => {
                if (btn.dataset.fam === family) {
                    btn.className = 'exp-fam-btn px-3.5 py-2 rounded-xl text-xs sm:text-sm font-semibold bg-slate-900 text-white shadow-sm transition-all';
                } else {
                    btn.className = 'exp-fam-btn px-3.5 py-2 rounded-xl text-xs sm:text-sm font-medium bg-stone-50 text-slate-700 border border-stone-200 hover:bg-amber-50 transition-all';
                }
            });
            renderExploreGrid();
        }

        function renderExploreGrid() {
            const grid = document.getElementById('explore-grid');
            grid.innerHTML = '';

            const filtered = exploreFamily === 'all'
                ? INSTRUMENTS
                : INSTRUMENTS.filter(i => i.family === exploreFamily);

            const badgeColors = {
                strings: 'bg-amber-100 text-amber-900 border-amber-200',
                woodwinds: 'bg-emerald-100 text-emerald-900 border-emerald-200',
                brass: 'bg-orange-100 text-orange-900 border-orange-200',
                keys: 'bg-blue-100 text-blue-900 border-blue-200',
                percussion: 'bg-purple-100 text-purple-900 border-purple-200'
            };

            filtered.forEach(inst => {
                const isSelected = inst.id === activeExploreId;
                const card = document.createElement('button');
                card.type = 'button';
                card.onclick = () => selectAndPlayExploreInstrument(inst.id);
                card.className = `text-left p-4 rounded-2xl border-2 transition-all flex flex-col justify-between bg-white hover:shadow-md ${
                    isSelected
                        ? 'border-amber-500 ring-2 ring-amber-500/20 bg-amber-50/25'
                        : 'border-stone-200 hover:border-amber-300'
                }`;

                card.innerHTML = `
                    <div>
                        <div class="flex items-center justify-between gap-2 mb-2.5">
                            <span class="text-2xl">${inst.icon}</span>
                            <span class="px-2.5 py-0.5 rounded-full text-[11px] font-bold border ${badgeColors[inst.family]}">
                                ${inst.familyName}
                            </span>
                        </div>
                        <h3 class="font-serif text-lg font-bold text-slate-900 leading-snug">${inst.name}</h3>
                        <p class="text-xs text-slate-500 mt-0.5">${inst.register}</p>
                    </div>
                    <div class="mt-4 pt-2.5 border-t border-stone-100 flex items-center justify-between text-xs font-bold ${isSelected ? 'text-amber-700' : 'text-slate-600'}">
                        <span>${isSelected ? 'Selecionado' : 'Clique para ouvir'}</span>
                        <i class="fa-solid ${isSelected ? 'fa-volume-high text-amber-600' : 'fa-play text-slate-400'}"></i>
                    </div>
                `;
                grid.appendChild(card);
            });
        }

        function updateProfessorSheet(instId) {
            const inst = INSTRUMENTS.find(i => i.id === instId);
            if (!inst) return;
            activeExploreId = inst.id;

            document.getElementById('sheet-family-badge').textContent = inst.familyName;
            document.getElementById('sheet-icon').textContent = inst.icon;
            document.getElementById('sheet-name').textContent = inst.name;
            document.getElementById('sheet-register').textContent = `Tessitura: ${inst.register}`;
            document.getElementById('sheet-production').textContent = inst.production;
            document.getElementById('sheet-timbre').textContent = inst.timbre;
            document.getElementById('sheet-tip').textContent = inst.tip;
        }

        function selectAndPlayExploreInstrument(instId) {
            updateProfessorSheet(instId);
            renderExploreGrid();
            const phraseKey = document.getElementById('explore-phrase-select').value;
            playInstrument(instId, phraseKey, false);
        }

        function replayActiveExploreInstrument() {
            const phraseKey = document.getElementById('explore-phrase-select').value;
            playInstrument(activeExploreId, phraseKey, false);
        }

        // ----------------------------------------------------------
        // 7. SEPARADOR 2: COMPARAÇÃO A/B
        // ----------------------------------------------------------
        function initCompareSelectors() {
            const selA = document.getElementById('select-compare-a');
            const selB = document.getElementById('select-compare-b');
            const optionsHtml = INSTRUMENTS.map(i => `<option value="${i.id}">${i.name} (${i.familyName})</option>`).join('');
            selA.innerHTML = optionsHtml;
            selB.innerHTML = optionsHtml;
            selA.value = 'violin';
            selB.value = 'viola';
            renderComparePanels();
        }

        function setComparePair(idA, idB) {
            document.getElementById('select-compare-a').value = idA;
            document.getElementById('select-compare-b').value = idB;
            renderComparePanels();
        }

        function renderComparePanels() {
            const idA = document.getElementById('select-compare-a').value;
            const idB = document.getElementById('select-compare-b').value;
            const instA = INSTRUMENTS.find(i => i.id === idA);
            const instB = INSTRUMENTS.find(i => i.id === idB);

            const renderInfo = (inst) => `
                <div class="flex items-center gap-2.5 pb-2 border-b border-stone-100">
                    <span class="text-2xl">${inst.icon}</span>
                    <div>
                        <p class="font-bold text-slate-900">${inst.familyName}</p>
                        <p class="text-xs text-slate-500">Tessitura: ${inst.register}</p>
                    </div>
                </div>
                <p><strong class="text-slate-900">Produção:</strong> ${inst.production}</p>
                <p><strong class="text-slate-900">Timbre:</strong> ${inst.timbre}</p>
                <p class="text-xs bg-stone-50 p-2.5 rounded-xl border border-stone-200 text-slate-700">
                    <strong>Dica:</strong> ${inst.tip}
                </p>
            `;

            document.getElementById('compare-info-a').innerHTML = renderInfo(instA);
            document.getElementById('compare-info-b').innerHTML = renderInfo(instB);

            document.getElementById('compare-summary-box').innerHTML = `
                <div class="flex items-start gap-3">
                    <i class="fa-solid fa-scale-balanced text-amber-600 text-lg mt-0.5"></i>
                    <div>
                        <h4 class="font-bold text-slate-900">Síntese Comparativa: ${instA.name} vs. ${instB.name}</h4>
                        <p class="text-slate-600 mt-1 leading-relaxed">
                            O <strong>${instA.name}</strong> (${instA.register}) destaca-se pelo carácter ${instA.timbre.toLowerCase()} 
                            Em contraste, o <strong>${instB.name}</strong> (${instB.register}) apresenta um timbre ${instB.timbre.toLowerCase()}
                        </p>
                    </div>
                </div>
            `;
        }

        function playCompareSingle(side) {
            const id = document.getElementById(side === 'a' ? 'select-compare-a' : 'select-compare-b').value;
            const phrase = document.getElementById('compare-phrase-select').value;
            playInstrument(id, phrase, false);
        }

        function playAlternateAB() {
            const idA = document.getElementById('select-compare-a').value;
            const idB = document.getElementById('select-compare-b').value;
            const phrase = document.getElementById('compare-phrase-select').value;
            const boxA = document.getElementById('compare-box-a');
            const boxB = document.getElementById('compare-box-b');

            boxA.classList.add('ring-4', 'ring-slate-900/20');
            boxB.classList.remove('ring-4', 'ring-amber-500/30');

            playInstrument(idA, phrase, false, () => {
                boxA.classList.remove('ring-4', 'ring-slate-900/20');
                boxB.classList.add('ring-4', 'ring-amber-500/30');
                playInstrument(idB, phrase, false, () => {
                    boxB.classList.remove('ring-4', 'ring-amber-500/30');
                });
            });
        }

        // ----------------------------------------------------------
        // 8. SEPARADOR 3: DESAFIO AUDITIVO (10 PERGUNTAS + MODO HARD)
        // ----------------------------------------------------------
        const TOTAL_QUESTIONS = 10;

        let quizState = {
            questionIndex: 1,
            score: 0,
            streak: 0,
            usedInstrumentIds: [],
            history: [],
            target: null,
            options: [],
            answered: false
        };

        function resetQuizSession() {
            stopCurrentPlayback();
            updateStatusIndicator('ready', 'Orquestra pronta');

            quizState = {
                questionIndex: 1,
                score: 0,
                streak: 0,
                usedInstrumentIds: [],
                history: [],
                target: null,
                options: [],
                answered: false
            };

            document.getElementById('quiz-report-card').classList.add('hidden');
            document.getElementById('quiz-question-card').classList.remove('hidden');
            prepareNextQuestion();
        }

        function updateQuizProgressUI() {
            document.getElementById('quiz-q-current').textContent = quizState.questionIndex;
            document.getElementById('quiz-title-num').textContent = quizState.questionIndex;
            document.getElementById('quiz-score-val').textContent = quizState.score;
            document.getElementById('quiz-streak-val').textContent = quizState.streak;
            const percentage = (quizState.questionIndex / TOTAL_QUESTIONS) * 100;
            document.getElementById('quiz-progress-fill').style.width = `${percentage}%`;
        }

        function prepareNextQuestion() {
            const diff = document.getElementById('quiz-difficulty').value;

            // Escolhe instrumento alvo sem repetir na mesma prova de 10 perguntas
            let candidates = INSTRUMENTS.filter(i => !quizState.usedInstrumentIds.includes(i.id));
            if (candidates.length === 0) candidates = [...INSTRUMENTS];

            const target = candidates[Math.floor(Math.random() * candidates.length)];
            quizState.usedInstrumentIds.push(target.id);

            let options = [];

            if (diff === 'hard') {
                // MODO HARD: Todos os 20 instrumentos disponíveis
                options = [...INSTRUMENTS];
            } else if (diff === 'easy') {
                // Iniciante: 4 opções de famílias distintas
                const usedFamilies = new Set([target.family]);
                const shuffled = [...INSTRUMENTS].sort(() => Math.random() - 0.5);
                const distractors = [];
                for (const item of shuffled) {
                    if (!usedFamilies.has(item.family)) {
                        distractors.push(item);
                        usedFamilies.add(item.family);
                    }
                    if (distractors.length === 3) break;
                }
                options = [target, ...distractors].sort(() => Math.random() - 0.5);
            } else if (diff === 'conservatory') {
                // Conservatório: 6 opções da mesma família ou pares muito próximos
                const confusedObjs = (target.confusedWith || [])
                    .map(id => INSTRUMENTS.find(i => i.id === id))
                    .filter(Boolean);
                const sameFamily = INSTRUMENTS.filter(i => i.id !== target.id && i.family === target.family && !confusedObjs.includes(i));
                const rest = INSTRUMENTS.filter(i => i.id !== target.id && !confusedObjs.includes(i) && !sameFamily.includes(i));

                confusedObjs.sort(() => Math.random() - 0.5);
                sameFamily.sort(() => Math.random() - 0.5);
                rest.sort(() => Math.random() - 0.5);

                const distractors = [...sameFamily, ...confusedObjs, ...rest].slice(0, 5);
                options = [target, ...distractors].sort(() => Math.random() - 0.5);
            } else {
                // Intermédio: 4 opções próximas
                const confusedObjs = (target.confusedWith || [])
                    .map(id => INSTRUMENTS.find(i => i.id === id))
                    .filter(Boolean)
                    .sort(() => Math.random() - 0.5);
                const sameFamily = INSTRUMENTS.filter(i => i.id !== target.id && i.family === target.family && !confusedObjs.includes(i))
                    .sort(() => Math.random() - 0.5);
                const rest = INSTRUMENTS.filter(i => i.id !== target.id && !confusedObjs.includes(i) && !sameFamily.includes(i))
                    .sort(() => Math.random() - 0.5);

                const distractors = [...confusedObjs, ...sameFamily, ...rest].slice(0, 3);
                options = [target, ...distractors].sort(() => Math.random() - 0.5);
            }

            quizState.target = target;
            quizState.options = options;
            quizState.answered = false;

            const diffLabels = {
                easy: 'Nível Iniciante (4 Opções • Famílias Distintas)',
                medium: 'Nível Intermédio (4 Opções • Timbres Próximos)',
                conservatory: 'Nível Conservatório (6 Opções • Alta Precisão)',
                hard: 'Modo Hard (Orquestra Completa • 20 Instrumentos)'
            };
            document.getElementById('quiz-difficulty-label').textContent = diffLabels[diff];
            document.getElementById('quiz-feedback-panel').classList.add('hidden');

            updateQuizProgressUI();
            renderQuizOptions();

            setTimeout(() => playQuizMysterySound(), 200);
        }

        function playQuizMysterySound() {
            if (!quizState.target) return;
            const phrase = document.getElementById('quiz-phrase-select').value;
            const btn = document.getElementById('btn-quiz-mystery-play');
            btn.innerHTML = '<i class="fa-solid fa-volume-high animate-bounce"></i><span>A reproduzir...</span>';

            // Mantém sigilo absoluto enquanto !quizState.answered
            const secretMode = !quizState.answered;

            playInstrument(quizState.target.id, phrase, secretMode, () => {
                btn.innerHTML = '<i class="fa-solid fa-play"></i><span>Ouvir Som Misterioso</span>';
            });
        }

        function renderQuizOptions() {
            const container = document.getElementById('quiz-options-container');
            const diff = document.getElementById('quiz-difficulty').value;
            container.innerHTML = '';

            if (diff === 'hard') {
                // Grelha compacta organizada para os 20 instrumentos
                container.className = 'grid grid-cols-1 sm:grid-cols-2 md:grid-cols-4 gap-2.5';
                quizState.options.forEach(opt => {
                    const btn = document.createElement('button');
                    btn.type = 'button';
                    btn.id = `q-opt-${opt.id}`;
                    btn.onclick = () => submitQuizAnswer(opt.id);
                    btn.className = 'p-3 rounded-xl border border-stone-200 hover:border-amber-500 hover:bg-amber-50/60 text-left transition-all flex items-center justify-between gap-2 bg-white group';
                    btn.innerHTML = `
                        <div class="flex items-center gap-2 min-w-0">
                            <span class="text-lg shrink-0">${opt.icon}</span>
                            <div class="min-w-0">
                                <span class="font-bold text-slate-900 block text-xs sm:text-sm truncate">${opt.name}</span>
                                <span class="text-[11px] text-slate-500 block truncate">${opt.familyName}</span>
                            </div>
                        </div>
                        <i class="fa-solid fa-chevron-right text-stone-300 group-hover:text-amber-500 text-xs shrink-0"></i>
                    `;
                    container.appendChild(btn);
                });
            } else {
                container.className = 'grid grid-cols-1 sm:grid-cols-2 gap-3.5';
                quizState.options.forEach(opt => {
                    const btn = document.createElement('button');
                    btn.type = 'button';
                    btn.id = `q-opt-${opt.id}`;
                    btn.onclick = () => submitQuizAnswer(opt.id);
                    btn.className = 'p-4 rounded-2xl border-2 border-stone-200 hover:border-amber-500 hover:bg-amber-50/40 text-left transition-all flex items-center justify-between bg-white group';
                    btn.innerHTML = `
                        <div class="flex items-center gap-3">
                            <div class="w-10 h-10 rounded-xl bg-stone-100 group-hover:bg-amber-100 flex items-center justify-center text-xl shrink-0">
                                ${opt.icon}
                            </div>
                            <div>
                                <span class="font-bold text-slate-900 block text-sm sm:text-base">${opt.name}</span>
                                <span class="text-xs text-slate-500">${opt.familyName} &bull; ${opt.register}</span>
                            </div>
                        </div>
                        <i class="fa-solid fa-chevron-right text-stone-300 group-hover:text-amber-500 transition-colors"></i>
                    `;
                    container.appendChild(btn);
                });
            }
        }

        function submitQuizAnswer(selectedId) {
            if (quizState.answered) return;
            quizState.answered = true;

            const diff = document.getElementById('quiz-difficulty').value;
            const isHard = diff === 'hard';
            const target = quizState.target;
            const selected = INSTRUMENTS.find(i => i.id === selectedId);
            const isCorrect = selectedId === target.id;

            if (isCorrect) {
                quizState.score++;
                quizState.streak++;
            } else {
                quizState.streak = 0;
            }

            quizState.history.push({
                num: quizState.questionIndex,
                targetName: target.name,
                selectedName: selected.name,
                isCorrect
            });

            updateQuizProgressUI();

            // Destaca a opção correta e a escolhida
            quizState.options.forEach(opt => {
                const btn = document.getElementById(`q-opt-${opt.id}`);
                btn.disabled = true;
                btn.classList.remove('hover:border-amber-500', 'hover:bg-amber-50/40', 'hover:bg-amber-50/60');

                const baseStyle = isHard ? 'p-3 rounded-xl border-2' : 'p-4 rounded-2xl border-2';

                if (opt.id === target.id) {
                    btn.className = `${baseStyle} border-emerald-500 bg-emerald-50 text-left flex items-center justify-between gap-2`;
                    btn.querySelector('.fa-chevron-right').className = 'fa-solid fa-circle-check text-emerald-600 text-lg shrink-0';
                } else if (opt.id === selectedId && !isCorrect) {
                    btn.className = `${baseStyle} border-rose-400 bg-rose-50 text-left flex items-center justify-between gap-2`;
                    btn.querySelector('.fa-chevron-right').className = 'fa-solid fa-circle-xmark text-rose-600 text-lg shrink-0';
                } else {
                    btn.classList.add('opacity-40');
                }
            });

            // Revela feedback pedagógico
            const fbPanel = document.getElementById('quiz-feedback-panel');
            const fbIcon = document.getElementById('quiz-fb-icon');
            const fbTitle = document.getElementById('quiz-fb-title');
            const fbBody = document.getElementById('quiz-fb-body');
            const btnHearCorrect = document.getElementById('btn-quiz-hear-correct');
            const btnHearChoice = document.getElementById('btn-quiz-hear-choice');
            const btnNext = document.getElementById('btn-quiz-next');

            fbPanel.classList.remove('hidden', 'bg-emerald-50', 'border-emerald-200', 'text-emerald-950', 'bg-rose-50', 'border-rose-200', 'text-rose-950');

            const currentPhrase = document.getElementById('quiz-phrase-select').value;

            if (isCorrect) {
                fbPanel.classList.add('bg-emerald-50', 'border-emerald-200', 'text-emerald-950');
                fbIcon.className = 'w-10 h-10 rounded-full bg-emerald-600 text-white flex items-center justify-center shrink-0 text-lg';
                fbIcon.innerHTML = '<i class="fa-solid fa-check"></i>';
                fbTitle.textContent = `Correto! Era mesmo o ${target.name}.`;
                fbBody.innerHTML = `<strong>Análise do Professor:</strong> ${target.timbre} <em>${target.tip}</em>`;
                btnHearChoice.classList.add('hidden');
            } else {
                fbPanel.classList.add('bg-rose-50', 'border-rose-200', 'text-rose-950');
                fbIcon.className = 'w-10 h-10 rounded-full bg-rose-600 text-white flex items-center justify-center shrink-0 text-lg';
                fbIcon.innerHTML = '<i class="fa-solid fa-xmark"></i>';
                fbTitle.textContent = `Escolheste ${selected.name}, mas o som era de ${target.name}.`;
                fbBody.innerHTML = `
                    <strong>Diferença Tímbrica:</strong> O <strong>${selected.name}</strong> (${selected.familyName}) tem um timbre ${selected.timbre.toLowerCase()} 
                    Já o <strong>${target.name}</strong> (${target.familyName}) distingue-se porque: <em>${target.tip}</em>
                `;
                btnHearChoice.classList.remove('hidden');
                btnHearChoice.innerHTML = `<i class="fa-solid fa-volume-high text-rose-600"></i><span>Ouvir ${selected.name}</span>`;
                btnHearChoice.onclick = () => playInstrument(selected.id, currentPhrase, false);
            }

            btnHearCorrect.innerHTML = `<i class="fa-solid fa-volume-high text-emerald-600"></i><span>Ouvir ${target.name}</span>`;
            btnHearCorrect.onclick = () => playInstrument(target.id, currentPhrase, false);

            if (quizState.questionIndex >= TOTAL_QUESTIONS) {
                btnNext.innerHTML = `<span>Ver Relatório Final (10/10)</span><i class="fa-solid fa-flag-checkered"></i>`;
            } else {
                btnNext.innerHTML = `<span>Próxima Pergunta (${quizState.questionIndex + 1}/10)</span><i class="fa-solid fa-arrow-right"></i>`;
            }
        }

        function nextQuizStep() {
            if (quizState.questionIndex >= TOTAL_QUESTIONS) {
                renderQuizFinalReport();
            } else {
                quizState.questionIndex++;
                prepareNextQuestion();
            }
        }

        function renderQuizFinalReport() {
            stopCurrentPlayback();
            updateStatusIndicator('ready', 'Orquestra pronta');

            document.getElementById('quiz-question-card').classList.add('hidden');
            document.getElementById('quiz-report-card').classList.remove('hidden');

            const score = quizState.score;
            const pct = Math.round((score / TOTAL_QUESTIONS) * 100);

            document.getElementById('report-score').textContent = score;
            document.getElementById('report-percent').textContent = `${pct}%`;

            let title = '';
            let comment = '';

            if (score === 10) {
                title = 'Excelência Absoluta — Ouvido de Maestro!';
                comment = 'Acertaste todas as 10 questões. A tua capacidade de identificar o ataque, a tessitura e o espectro harmónico de cada família orquestral é extraordinária.';
            } else if (score >= 8) {
                title = 'Muito Bom — Excelente Perceção Tímbrica!';
                comment = 'Demonstras grande domínio na identificação auditiva. Recomendo utilizar a Comparação A/B para aperfeiçoar os pequenos detalhes que ainda geraram dúvida.';
            } else if (score >= 5) {
                title = 'Suficiente — Em Evolução Positiva';
                comment = 'Já identificas com segurança várias famílias, mas alguns timbres próximos ainda se confundem. Experimenta ouvir a "Nota Longa Sustentada" para estudar o ataque inicial de cada instrumento.';
            } else {
                title = 'Fase Inicial — Continua o Treino Auditivo';
                comment = 'Sugestão pedagógica: regressa ao separador "Explorar Orquestra", filtra uma família de cada vez e compara os pares sugeridos na "Comparação A/B" antes de repetir a prova.';
            }

            document.getElementById('report-verdict-title').textContent = title;
            document.getElementById('report-verdict-comment').textContent = comment;

            const listEl = document.getElementById('report-questions-list');
            listEl.innerHTML = quizState.history.map(item => `
                <div class="flex items-center justify-between p-3 rounded-xl border ${
                    item.isCorrect
                        ? 'bg-emerald-50/70 border-emerald-200 text-emerald-950'
                        : 'bg-rose-50/70 border-rose-200 text-rose-950'
                } text-xs sm:text-sm">
                    <div class="flex items-center gap-2.5 min-w-0">
                        <span class="w-6 h-6 rounded-full ${item.isCorrect ? 'bg-emerald-600 text-white' : 'bg-rose-600 text-white'} flex items-center justify-center text-xs font-bold shrink-0">
                            ${item.num}
                        </span>
                        <div class="truncate">
                            <span class="font-bold block truncate">${item.targetName}</span>
                            ${
                                item.isCorrect
                                    ? '<span class="text-[11px] text-emerald-700 block">Resposta certa</span>'
                                    : `<span class="text-[11px] text-rose-700 block truncate">A tua resposta: ${item.selectedName}</span>`
                            }
                        </div>
                    </div>
                    <i class="fa-solid ${item.isCorrect ? 'fa-check text-emerald-600' : 'fa-xmark text-rose-600'} shrink-0 ml-2"></i>
                </div>
            `).join('');
        }

        // ----------------------------------------------------------
        // 9. INICIALIZAÇÃO GLOBAL
        // ----------------------------------------------------------
        window.addEventListener('DOMContentLoaded', () => {
            updateProfessorSheet('violin');
            renderExploreGrid();
            initCompareSelectors();
            startOscilloscopeLoop();
        });
    </script>
</body>
</html>
