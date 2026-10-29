<!DOCTYPE html>

<html lang="pt-BR">

<head>

&#x20;   <meta charset="UTF-8">

&#x20;   <meta name="viewport" content="width=device-width, initial-scale=1.0">

&#x20;   <title>Gestão de Pessoas para Estudantes</title>

&#x20;   <!-- Tailwind CSS -->

&#x20;   <script src="https://cdn.tailwindcss.com"></script>

&#x20;   <!-- Font Awesome -->

&#x20;   <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">

&#x20;   <!-- Google Fonts -->

&#x20;   <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;800\&display=swap" rel="stylesheet">

&#x20;   <!-- QR Code Library -->

&#x20;   <script src="https://cdnjs.cloudflare.com/ajax/libs/qrcodejs/1.0.0/qrcode.min.js"></script>

&#x20;   <!-- Markdown Parser Simple -->

&#x20;   <script src="https://cdn.jsdelivr.net/npm/marked/marked.min.js"></script>



&#x20;   <style>

&#x20;       body { font-family: 'Inter', sans-serif; background-color: #f3f4f6; }

&#x20;       

&#x20;       /\* Scrollbar styling \*/

&#x20;       ::-webkit-scrollbar { width: 8px; }

&#x20;       ::-webkit-scrollbar-track { background: #f1f1f1; border-radius: 4px; }

&#x20;       ::-webkit-scrollbar-thumb { background: #cbd5e1; border-radius: 4px; }

&#x20;       ::-webkit-scrollbar-thumb:hover { background: #94a3b8; }



&#x20;       .module-btn { transition: all 0.3s ease; }

&#x20;       .module-btn:not(:disabled):hover { transform: translateY(-2px); box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06); }

&#x20;       .module-btn:not(:disabled):active { transform: translateY(0); }

&#x20;       

&#x20;       .chat-message p { margin-bottom: 0.5rem; }

&#x20;       .chat-message p:last-child { margin-bottom: 0; }

&#x20;       .chat-message ul { list-style-type: disc; padding-left: 1.5rem; margin-bottom: 0.5rem; }

&#x20;       .chat-message strong { font-weight: 600; }



&#x20;       /\* Print Styles for Certificate \*/

&#x20;       @media print {

&#x20;           body \* { visibility: hidden; }

&#x20;           #certificate-modal, #certificate-modal \* { visibility: visible; }

&#x20;           #certificate-modal { position: absolute; left: 0; top: 0; width: 100%; height: 100%; display: flex; justify-content: center; align-items: center; background: white !important; }

&#x20;           .no-print { display: none !important; }

&#x20;           .print-border { border: 10px solid #1e3a8a !important; padding: 40px !important; }

&#x20;       }



&#x20;       .loader {

&#x20;           border: 3px solid #f3f3f3;

&#x20;           border-top: 3px solid #3b82f6;

&#x20;           border-radius: 50%;

&#x20;           width: 24px;

&#x20;           height: 24px;

&#x20;           animation: spin 1s linear infinite;

&#x20;       }

&#x20;       @keyframes spin { 0% { transform: rotate(0deg); } 100% { transform: rotate(360deg); } }

&#x20;   </style>

</head>

<body class="text-gray-800 h-screen flex flex-col overflow-hidden">



&#x20;   <!-- Header Banner -->

&#x20;   <header class="bg-gradient-to-r from-blue-900 via-indigo-800 to-purple-900 text-white shadow-lg z-10 relative">

&#x20;       <div class="max-w-7xl mx-auto px-4 py-4 sm:px-6 lg:px-8 flex justify-between items-center">

&#x20;           <div class="flex items-center gap-3">

&#x20;               <div class="bg-white/20 p-2 rounded-lg backdrop-blur-sm">

&#x20;                   <i class="fa-solid fa-users-gear text-xl"></i>

&#x20;               </div>

&#x20;               <h1 class="text-xl md:text-2xl font-bold tracking-tight">GESTÃO DE PESSOAS <span class="font-light text-blue-200">PARA ESTUDANTES</span></h1>

&#x20;           </div>

&#x20;           <button onclick="openShareModal()" class="flex items-center gap-2 bg-white/10 hover:bg-white/20 px-4 py-2 rounded-full transition-colors text-sm font-semibold backdrop-blur-sm">

&#x20;               <i class="fa-solid fa-share-nodes"></i> <span class="hidden md:inline">Compartilhar App</span>

&#x20;           </button>

&#x20;       </div>

&#x20;   </header>



&#x20;   <!-- Main Content Area -->

&#x20;   <main class="flex-1 max-w-7xl w-full mx-auto p-4 flex flex-col gap-4 overflow-hidden">

&#x20;       

&#x20;       <!-- Controls Panel (The Buttons) -->

&#x20;       <div class="bg-white rounded-2xl shadow-sm border border-gray-100 p-4 shrink-0">

&#x20;           <h2 class="text-xs uppercase font-bold text-gray-400 mb-3 tracking-wider"><i class="fa-solid fa-map-location-dot mr-1"></i> Trilha de Desenvolvimento</h2>

&#x20;           

&#x20;           <!-- Row 1: Phases -->

&#x20;           <div class="grid grid-cols-2 md:grid-cols-7 gap-2 mb-2" id="row-phases">

&#x20;               <!-- Buttons injected via JS -->

&#x20;           </div>



&#x20;           <!-- Row 2: Feedbacks \& Certificate -->

&#x20;           <div class="grid grid-cols-2 md:grid-cols-7 gap-2" id="row-feedbacks">

&#x20;               <!-- Buttons injected via JS -->

&#x20;           </div>

&#x20;       </div>



&#x20;       <!-- Interaction Area (The "Hidden AI" Chat) -->

&#x20;       <div class="flex-1 bg-white rounded-2xl shadow-sm border border-gray-100 flex flex-col overflow-hidden relative">

&#x20;           

&#x20;           <!-- Initial Overlay -->

&#x20;           <div id="welcome-overlay" class="absolute inset-0 bg-white/90 backdrop-blur-sm z-10 flex flex-col items-center justify-center p-6 text-center">

&#x20;               <div class="w-20 h-20 bg-blue-100 rounded-full flex items-center justify-center mb-4 text-blue-600 text-3xl shadow-inner">

&#x20;                   <i class="fa-solid fa-rocket"></i>

&#x20;               </div>

&#x20;               <h3 class="text-2xl font-bold text-gray-800 mb-2">Bem-vindo ao seu Treinamento</h3>

&#x20;               <p class="text-gray-500 max-w-md mb-6">Você está prestes a iniciar uma jornada para desenvolver sua liderança e inteligência emocional. Clique em <b>"Anamnese"</b> na trilha acima para começar.</p>

&#x20;               <button onclick="startApp()" class="bg-blue-600 hover:bg-blue-700 text-white font-bold py-3 px-8 rounded-full shadow-lg transition-transform hover:scale-105">

&#x20;                   Iniciar Agora

&#x20;               </button>

&#x20;           </div>



&#x20;           <!-- Messages Container -->

&#x20;           <div id="chat-container" class="flex-1 overflow-y-auto p-4 md:p-6 space-y-6 bg-\[url('https://www.transparenttextures.com/patterns/cubes.png')] bg-opacity-10">

&#x20;               <!-- Messages go here -->

&#x20;           </div>



&#x20;           <!-- Input Area -->

&#x20;           <div class="p-4 bg-gray-50 border-t border-gray-200">

&#x20;               <div class="flex gap-2 relative">

&#x20;                   <textarea id="user-input" rows="2" class="w-full resize-none rounded-xl border border-gray-300 focus:border-blue-500 focus:ring focus:ring-blue-200 transition-all p-3 text-sm" placeholder="Digite sua resposta aqui..." disabled onkeydown="if(event.keyCode===13 \&\& !event.shiftKey) { event.preventDefault(); sendMessage(); }"></textarea>

&#x20;                   <button id="send-btn" onclick="sendMessage()" disabled class="bg-blue-600 hover:bg-blue-700 disabled:bg-gray-400 text-white rounded-xl px-6 flex items-center justify-center transition-colors shadow-md">

&#x20;                       <i class="fa-solid fa-paper-plane"></i>

&#x20;                   </button>

&#x20;                   <!-- Loading Indicator -->

&#x20;                   <div id="typing-indicator" class="absolute -top-10 left-4 bg-white px-4 py-2 rounded-full shadow border border-gray-100 hidden items-center gap-2 text-sm text-gray-500 font-medium">

&#x20;                       <div class="loader"></div> O mentor está analisando...

&#x20;                   </div>

&#x20;               </div>

&#x20;           </div>

&#x20;       </div>

&#x20;   </main>



&#x20;   <!-- Modal Share -->

&#x20;   <div id="share-modal" class="fixed inset-0 bg-black/60 backdrop-blur-sm hidden z-50 flex items-center justify-center p-4">

&#x20;       <div class="bg-white rounded-2xl p-6 max-w-sm w-full shadow-2xl transform transition-all">

&#x20;           <div class="flex justify-between items-center mb-4">

&#x20;               <h3 class="text-lg font-bold text-gray-800">Acessar no Celular</h3>

&#x20;               <button onclick="closeModal('share-modal')" class="text-gray-400 hover:text-gray-600"><i class="fa-solid fa-xmark text-xl"></i></button>

&#x20;           </div>

&#x20;           <div class="flex justify-center mb-6 bg-gray-50 p-4 rounded-xl">

&#x20;               <div id="qrcode"></div>

&#x20;           </div>

&#x20;           <p class="text-sm text-center text-gray-500 mb-4">Escaneie o QR Code acima com a câmera do seu celular para continuar o treinamento.</p>

&#x20;           <button onclick="copyLink()" class="w-full bg-gray-100 hover:bg-gray-200 text-gray-700 font-semibold py-2 px-4 rounded-lg flex items-center justify-center gap-2 transition-colors">

&#x20;               <i class="fa-solid fa-link"></i> <span id="copy-text">Copiar Link</span>

&#x20;           </button>

&#x20;       </div>

&#x20;   </div>



&#x20;   <!-- Modal Alert (Custom instead of alert()) -->

&#x20;   <div id="alert-modal" class="fixed inset-0 bg-black/40 hidden z-50 flex items-center justify-center p-4">

&#x20;       <div class="bg-white rounded-xl p-6 max-w-sm w-full shadow-xl text-center">

&#x20;           <div class="w-16 h-16 bg-yellow-100 rounded-full flex items-center justify-center mx-auto mb-4 text-yellow-500 text-2xl">

&#x20;               <i class="fa-solid fa-circle-exclamation"></i>

&#x20;           </div>

&#x20;           <h3 class="text-lg font-bold text-gray-800 mb-2" id="alert-title">Atenção</h3>

&#x20;           <p class="text-gray-600 mb-6" id="alert-message">Mensagem aqui</p>

&#x20;           <button onclick="closeModal('alert-modal')" class="w-full bg-blue-600 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded-lg transition-colors">Entendi</button>

&#x20;       </div>

&#x20;   </div>



&#x20;   <!-- Modal Certificate -->

&#x20;   <div id="certificate-modal" class="fixed inset-0 bg-gray-900/90 hidden z-50 flex items-center justify-center p-4 overflow-y-auto">

&#x20;       <div class="bg-white rounded-none md:rounded-lg max-w-4xl w-full mx-auto relative print-border" style="min-height: 600px;">

&#x20;           <!-- Actions (No Print) -->

&#x20;           <div class="absolute top-4 right-4 flex gap-2 no-print z-10">

&#x20;               <button onclick="window.print()" class="bg-blue-600 hover:bg-blue-700 text-white px-4 py-2 rounded shadow"><i class="fa-solid fa-print mr-2"></i> Imprimir</button>

&#x20;               <button onclick="closeModal('certificate-modal')" class="bg-gray-200 hover:bg-gray-300 text-gray-800 px-4 py-2 rounded shadow"><i class="fa-solid fa-xmark"></i></button>

&#x20;           </div>

&#x20;           

&#x20;           <!-- Certificate Content -->

&#x20;           <div class="p-12 text-center relative h-full flex flex-col justify-center bg-\[url('https://www.transparenttextures.com/patterns/stardust.png')]">

&#x20;               <!-- Decorative Corners -->

&#x20;               <div class="absolute top-0 left-0 w-32 h-32 border-t-8 border-l-8 border-blue-900"></div>

&#x20;               <div class="absolute top-0 right-0 w-32 h-32 border-t-8 border-r-8 border-blue-900"></div>

&#x20;               <div class="absolute bottom-0 left-0 w-32 h-32 border-b-8 border-l-8 border-blue-900"></div>

&#x20;               <div class="absolute bottom-0 right-0 w-32 h-32 border-b-8 border-r-8 border-blue-900"></div>



&#x20;               <div class="mb-8">

&#x20;                   <i class="fa-solid fa-award text-6xl text-yellow-500 mb-4 drop-shadow-md"></i>

&#x20;                   <h1 class="text-4xl md:text-5xl font-extrabold text-blue-900 uppercase tracking-widest font-serif">Certificado de Conclusão</h1>

&#x20;                   <div class="w-24 h-1 bg-yellow-500 mx-auto mt-6"></div>

&#x20;               </div>



&#x20;               <p class="text-xl text-gray-600 mb-4">Certificamos que</p>

&#x20;               <h2 class="text-3xl md:text-4xl font-bold text-gray-800 border-b-2 border-gray-300 inline-block px-12 pb-2 mb-6" id="cert-name">\[Nome do Aluno]</h2>

&#x20;               

&#x20;               <p class="text-lg text-gray-600 mb-6 max-w-2xl mx-auto">

&#x20;                   Concluiu com êxito o programa autônomo <strong class="text-blue-900">Gestão de Pessoas para Estudantes</strong>, demonstrando proficiência nos módulos de Inteligência Emocional, Comunicação, Liderança, Tomada de Decisão e Ética.

&#x20;               </p>



&#x20;               <div class="bg-blue-50 p-6 rounded-lg border border-blue-100 text-left max-w-2xl mx-auto mb-12 shadow-sm">

&#x20;                   <h3 class="text-sm font-bold text-blue-900 uppercase mb-2"><i class="fa-solid fa-chart-line mr-2"></i> Perfil de Liderança Desenvolvido:</h3>

&#x20;                   <div id="cert-profile" class="text-sm text-gray-700 italic">

&#x20;                       Gerando avaliação de desempenho...

&#x20;                   </div>

&#x20;               </div>



&#x20;               <div class="flex justify-between items-end px-12 mt-auto">

&#x20;                   <div class="text-center">

&#x20;                       <div class="border-b border-gray-400 w-48 mb-2"></div>

&#x20;                       <p class="text-sm text-gray-500">Tutor de IA Generativa</p>

&#x20;                   </div>

&#x20;                   <div class="text-center">

&#x20;                       <p class="text-sm font-bold text-gray-800" id="cert-date"></p>

&#x20;                       <p class="text-xs text-gray-400">Data de Emissão</p>

&#x20;                   </div>

&#x20;               </div>

&#x20;           </div>

&#x20;       </div>

&#x20;   </div>



&#x20;   <!-- Application Logic -->

&#x20;   <script>

&#x20;       // --- CONFIG \& STATE ---

&#x20;       const API\_KEY = ""; // Gemini API Key goes here automatically via Canvas

&#x20;       

&#x20;       // Define Modules

&#x20;       const modules = \[

&#x20;           { id: 'anamnese', name: 'Anamnese', color: 'emerald', short: 'Anamnese' },

&#x20;           { id: 'm1', name: 'Inteligência Emocional', color: 'blue', short: 'Módulo 1' },

&#x20;           { id: 'm2', name: 'Comunicação', color: 'indigo', short: 'Módulo 2' },

&#x20;           { id: 'm3', name: 'Liderança', color: 'violet', short: 'Módulo 3' },

&#x20;           { id: 'm4', name: 'Tomada de Decisão', color: 'purple', short: 'Módulo 4' },

&#x20;           { id: 'm5', name: 'Ética e Cidadania', color: 'fuchsia', short: 'Módulo 5' },

&#x20;           { id: 'm6', name: 'Projeto Final', color: 'pink', short: 'Módulo 6' }

&#x20;       ];



&#x20;       let state = {

&#x20;           currentPhaseId: null,

&#x20;           highestUnlockedIndex: 0, // 0 = anamnese, 1 = m1...

&#x20;           completedModules: \[],

&#x20;           chatHistory: \[] // To keep context for Gemini

&#x20;       };



&#x20;       // --- SYSTEM PROMPT (The "Super Prompt" provided by user) ---

&#x20;       const SYSTEM\_INSTRUCTION = `Você é um engenheiro educacional e tutor autônomo especializado em

desenvolver competências de liderança em estudantes do ensino fundamental

anos finais (6º ao 9º ano) especialmente alunos com comportamento

desafiador, mas com claro potencial de liderança ou profissional de gestão.

Sua missão é conduzir um curso completo de forma TOTALMENTE AUTÔNOMA,

sem depender do professor para cada passo. Você assume o papel de

facilitador, avaliador, mentor e conselheiro ao mesmo tempo.

Use linguagem acessível, amigável, emojis e formatação Markdown para deixar o texto agradável.



=============================================================

REGRA MESTRA DE AUTONOMIA

=============================================================

Você opera em um LOOP AUTÔNOMO. Cada ciclo é: AVALIAR → ENSINAR →

SIMULAR → DAR FEEDBACK → VERIFICAR DOMÍNIO → DECIDIR (avançar ou

retomar) → PROPOR AÇÃO PRÁTICA. Você nunca avança a menos que a

verificação de domínio seja aprovada. Você nunca deixa um aluno

para trás. Você registra o progresso e retoma exatamente onde o

aluno parou, mesmo que a conversa seja retomada dias depois.



=============================================================

FASE 0: ANAMNESE (diagnóstico inicial obrigatório)

=============================================================

Antes de iniciar qualquer módulo, aplique a anamnese. Faça perguntas

curtas, UMA DE CADA VEZ, em linguagem acessível e acolhedora, sem

julgar o aluno. Cubra estas dimensões:

1\. IDENTIDADE E CONTEXTO: nome, idade, série, o que gosta.

2\. AUTOPERCEPÇÃO: como se vê e como os outros o veem.

3\. COMPORTAMENTO: pontos fortes, o que irrita.

4\. RELAÇÕES: colegas, família, prefere liderar ou seguir.

5\. ESTILO DE APRENDIZADO.

Após a anamnese, avise o aluno que ele concluiu esta fase e peça para ele clicar no Módulo 1 na interface.



=============================================================

ARQUITETURA INTERNA DE CADA MÓDULO (5 passos obrigatórios)

=============================================================

Siga estritamente os passos. Não pule.

PASSO 1: ENSINAR O CONCEITO (breve, 3 ideias máx, 1 pergunta rápida).

PASSO 2: SIMULAÇÃO DIFERENCIADA (role-play, cenário prático - adeque ao estilo do aluno).

PASSO 3: FEEDBACK ESTRUTURADO (O que foi bom, o que melhorar, como melhorar).

PASSO 4: VERIFICAÇÃO DE DOMÍNIO (Pergunta de checagem. Se não dominar, repete Passo 1 ou 2).

PASSO 5: AÇÃO PRÁTICA (Uma missão real para a semana. Peça para ele clicar no "Feedback" ou próximo módulo na interface).



MÓDULOS:

M1: Autoconhecimento e Inteligência Emocional

M2: Comunicação e Expressão

M3: Liderança e Trabalho em Equipe

M4: Tomada de Decisão e Resolução de Problemas

M5: Responsabilidade, Ética e Cidadania

M6: Projeto Integrador Final



=============================================================

INSTRUÇÃO TÉCNICA DE INTERFACE (MUITO IMPORTANTE)

=============================================================

O aluno está usando uma interface gráfica com botões. 

Ocasionalmente, o sistema enviará mensagens de bastidores no formato \[SISTEMA: comando].

\- Quando receber \[SISTEMA: INICIAR FASE X], inicie imediatamente o conteúdo daquela fase, lembrando do perfil do aluno.

\- Quando receber \[SISTEMA: GERAR FEEDBACK DA FASE X], gere um resumo elegante e encorajador do desempenho do aluno apenas naquele módulo específico.

\- Quando receber \[SISTEMA: GERAR RESUMO PARA CERTIFICADO], escreva um parágrafo profissional (em 3ª pessoa) resumindo as principais habilidades de liderança que este aluno desenvolveu durante todo o curso. Apenas o parágrafo, sem formatações extras.

Nunca mencione as mensagens \[SISTEMA] para o aluno. Aja naturalmente.`;



&#x20;       // --- INITIALIZATION ---

&#x20;       window.onload = () => {

&#x20;           renderButtons();

&#x20;           // Generate QR Code

&#x20;           new QRCode(document.getElementById("qrcode"), {

&#x20;               text: window.location.href,

&#x20;               width: 128, height: 128,

&#x20;               colorDark : "#1e3a8a", colorLight : "#ffffff",

&#x20;               correctLevel : QRCode.CorrectLevel.H

&#x20;           });

&#x20;           // Set date for cert

&#x20;           const dateStr = new Date().toLocaleDateString('pt-BR');

&#x20;           document.getElementById('cert-date').innerText = dateStr;

&#x20;       };



&#x20;       function startApp() {

&#x20;           document.getElementById('welcome-overlay').style.display = 'none';

&#x20;           document.getElementById('user-input').disabled = false;

&#x20;           selectPhase('anamnese', 0);

&#x20;       }



&#x20;       // --- UI RENDERING ---

&#x20;       function renderButtons() {

&#x20;           const phasesContainer = document.getElementById('row-phases');

&#x20;           const feedbacksContainer = document.getElementById('row-feedbacks');

&#x20;           

&#x20;           phasesContainer.innerHTML = '';

&#x20;           feedbacksContainer.innerHTML = '';



&#x20;           modules.forEach((mod, index) => {

&#x20;               // Phase Button

&#x20;               const isUnlocked = index <= state.highestUnlockedIndex;

&#x20;               const isCurrent = state.currentPhaseId === mod.id;

&#x20;               

&#x20;               let btnClasses = `module-btn w-full py-2 px-1 text-xs md:text-sm font-bold rounded-lg border-b-4 flex flex-col items-center justify-center gap-1 `;

&#x20;               

&#x20;               if (isUnlocked) {

&#x20;                   btnClasses += `bg-${mod.color}-100 text-${mod.color}-700 border-${mod.color}-300 hover:bg-${mod.color}-200 `;

&#x20;                   if (isCurrent) btnClasses += `ring-2 ring-offset-2 ring-${mod.color}-500 bg-${mod.color}-500 text-white border-${mod.color}-700 `;

&#x20;               } else {

&#x20;                   btnClasses += `bg-gray-100 text-gray-400 border-gray-200 opacity-50 cursor-not-allowed `;

&#x20;               }



&#x20;               const btnPhase = document.createElement('button');

&#x20;               btnPhase.className = btnClasses;

&#x20;               btnPhase.disabled = !isUnlocked;

&#x20;               btnPhase.onclick = () => selectPhase(mod.id, index);

&#x20;               

&#x20;               let icon = index === 0 ? 'fa-clipboard-user' : `fa-${index}`;

&#x20;               btnPhase.innerHTML = `<i class="fa-solid ${icon}"></i> <span class="truncate w-full text-center">${mod.short}</span>`;

&#x20;               phasesContainer.appendChild(btnPhase);



&#x20;               // Feedback Button (Row 2)

&#x20;               const feedbackUnlocked = state.completedModules.includes(mod.id) || (index < state.highestUnlockedIndex);

&#x20;               let fbClasses = `module-btn w-full py-1 text-\[10px] md:text-xs font-semibold rounded shadow-sm border flex items-center justify-center gap-1 `;

&#x20;               

&#x20;               if (feedbackUnlocked) {

&#x20;                   fbClasses += `bg-white text-${mod.color}-600 border-${mod.color}-200 hover:bg-${mod.color}-50 `;

&#x20;               } else {

&#x20;                   fbClasses += `bg-gray-50 text-gray-300 border-gray-100 opacity-50 cursor-not-allowed `;

&#x20;               }



&#x20;               const btnFb = document.createElement('button');

&#x20;               btnFb.className = fbClasses;

&#x20;               btnFb.disabled = !feedbackUnlocked;

&#x20;               btnFb.onclick = () => requestFeedback(mod.id, mod.name);

&#x20;               btnFb.innerHTML = `<i class="fa-solid fa-comment-dots"></i> <span class="hidden md:inline">Feedback</span>`;

&#x20;               feedbacksContainer.appendChild(btnFb);

&#x20;           });



&#x20;           // Certificate Button at the end of Row 2

&#x20;           const certUnlocked = state.completedModules.includes('m6'); // Need to finish module 6

&#x20;           const btnCert = document.createElement('button');

&#x20;           btnCert.className = `module-btn w-full py-1 text-\[10px] md:text-xs font-bold rounded shadow-sm border flex items-center justify-center gap-1 ${certUnlocked ? 'bg-gradient-to-r from-yellow-400 to-yellow-500 text-white border-yellow-600 hover:shadow-md' : 'bg-gray-100 text-gray-300 border-gray-200 opacity-50 cursor-not-allowed'}`;

&#x20;           btnCert.disabled = !certUnlocked;

&#x20;           btnCert.onclick = generateCertificate;

&#x20;           btnCert.innerHTML = `<i class="fa-solid fa-graduation-cap"></i> Certificado`;

&#x20;           

&#x20;           // To make it fit the grid nicely, we replace the last item or append if grid allows.

&#x20;           // Since we have 7 items (Anam + 6), and grid is 7 cols, we will replace the M6 feedback with Cert for space, 

&#x20;           // OR just add it. Let's add it by changing grid to 8 or handling it gracefully.

&#x20;           // Actually, best is to append it and change parent grid to 7 cols (Anamnese feedback is weird anyway, let's keep it).

&#x20;           feedbacksContainer.lastChild.remove(); // Remove Feedback M6

&#x20;           feedbacksContainer.appendChild(btnCert); // Put Cert there instead.

&#x20;       }



&#x20;       // --- CORE LOGIC ---

&#x20;       function selectPhase(phaseId, index) {

&#x20;           if (index > state.highestUnlockedIndex) return;

&#x20;           

&#x20;           state.currentPhaseId = phaseId;

&#x20;           renderButtons();

&#x20;           document.getElementById('user-input').focus();



&#x20;           const moduleName = modules.find(m => m.id === phaseId).name;

&#x20;           

&#x20;           // Inject hidden system message to guide the AI

&#x20;           const hiddenMsg = `\[SISTEMA: O usuário clicou no botão para iniciar a fase: ${moduleName}. Assuma o controle, saúde-o rapidamente focando nesta etapa e dê o primeiro passo desta fase conforme suas instruções.]`;

&#x20;           

&#x20;           appendMessage('system', `Iniciando ${moduleName}...`, true); // True = visually distinct, local only

&#x20;           

&#x20;           // Add to history but don't show user the raw prompt

&#x20;           state.chatHistory.push({ role: 'user', parts: \[{ text: hiddenMsg }] });

&#x20;           

&#x20;           callGeminiAPI();

&#x20;       }



&#x20;       function requestFeedback(phaseId, moduleName) {

&#x20;           const hiddenMsg = `\[SISTEMA: GERAR FEEDBACK DA FASE ${moduleName}. Faça um resumo executivo encorajador e direto ao ponto do desempenho do aluno neste módulo.]`;

&#x20;           appendMessage('system', `Solicitando feedback de ${moduleName}...`, true);

&#x20;           state.chatHistory.push({ role: 'user', parts: \[{ text: hiddenMsg }] });

&#x20;           callGeminiAPI();

&#x20;       }



&#x20;       async function generateCertificate() {

&#x20;           showModal('alert-modal', 'Gerando Certificado', 'Aguarde enquanto analisamos seu perfil de liderança para compor o certificado oficial...');

&#x20;           

&#x20;           // Ask AI to generate the summary text

&#x20;           const hiddenMsg = `\[SISTEMA: GERAR RESUMO PARA CERTIFICADO]`;

&#x20;           state.chatHistory.push({ role: 'user', parts: \[{ text: hiddenMsg }] });

&#x20;           

&#x20;           const responseText = await fetchGeminiDirect(state.chatHistory);

&#x20;           

&#x20;           closeModal('alert-modal');

&#x20;           

&#x20;           if(responseText) {

&#x20;               document.getElementById('cert-profile').innerHTML = responseText.replace(/\\n/g, '<br>');

&#x20;               // Prompt user for name

&#x20;               const studentName = prompt("Para o certificado, por favor digite seu nome completo:");

&#x20;               if(studentName) {

&#x20;                   document.getElementById('cert-name').innerText = studentName;

&#x20;                   showModal('certificate-modal');

&#x20;               }

&#x20;           } else {

&#x20;               showAlert("Erro", "Não foi possível gerar o texto do certificado. Tente novamente.");

&#x20;           }

&#x20;       }



&#x20;       async function sendMessage() {

&#x20;           const inputEl = document.getElementById('user-input');

&#x20;           const text = inputEl.value.trim();

&#x20;           if (!text) return;



&#x20;           // UI Update

&#x20;           appendMessage('user', text);

&#x20;           inputEl.value = '';

&#x20;           document.getElementById('send-btn').disabled = true;



&#x20;           // Update History

&#x20;           state.chatHistory.push({ role: 'user', parts: \[{ text: text }] });



&#x20;           // Simulating unlocking logic for demo purposes based on user intent (In a real app, AI function calling would trigger this)

&#x20;           // Let's implement a simple keyword check to "unlock" next levels just so the demo is fully clickable.

&#x20;           checkSimulatedProgression(text);



&#x20;           await callGeminiAPI();

&#x20;           document.getElementById('send-btn').disabled = false;

&#x20;           inputEl.focus();

&#x20;       }



&#x20;       // --- GEMINI API INTEGRATION ---

&#x20;       async function callGeminiAPI() {

&#x20;           showTypingIndicator(true);

&#x20;           

&#x20;           try {

&#x20;               const url = `https://generativelanguage.googleapis.com/v1beta/models/gemini-3-flash-preview:generateContent?key=${API\_KEY}`;

&#x20;               

&#x20;               // Construct Payload per rules

&#x20;               const payload = {

&#x20;                   contents: state.chatHistory,

&#x20;                   systemInstruction: {

&#x20;                       parts: \[{ text: SYSTEM\_INSTRUCTION }]

&#x20;                   }

&#x20;               };



&#x20;               const response = await fetchWithRetry(url, {

&#x20;                   method: 'POST',

&#x20;                   headers: { 'Content-Type': 'application/json' },

&#x20;                   body: JSON.stringify(payload)

&#x20;               });



&#x20;               const result = await response.json();

&#x20;               

&#x20;               if (result.candidates \&\& result.candidates\[0].content) {

&#x20;                   const aiText = result.candidates\[0].content.parts\[0].text;

&#x20;                   state.chatHistory.push({ role: 'model', parts: \[{ text: aiText }] });

&#x20;                   appendMessage('model', aiText);

&#x20;               } else {

&#x20;                   throw new Error("Resposta inválida da API");

&#x20;               }

&#x20;           } catch (error) {

&#x20;               console.error("API Error:", error);

&#x20;               appendMessage('system', "Houve um problema de conexão com o seu mentor. Por favor, tente enviar novamente.");

&#x20;               state.chatHistory.pop(); // Remove last user message so they can retry

&#x20;           } finally {

&#x20;               showTypingIndicator(false);

&#x20;           }

&#x20;       }



&#x20;       // Direct fetch for specific background tasks (like certificate)

&#x20;       async function fetchGeminiDirect(historyArray) {

&#x20;            try {

&#x20;               const url = `https://generativelanguage.googleapis.com/v1beta/models/gemini-3-flash-preview:generateContent?key=${API\_KEY}`;

&#x20;               const payload = {

&#x20;                   contents: historyArray,

&#x20;                   systemInstruction: { parts: \[{ text: SYSTEM\_INSTRUCTION }] }

&#x20;               };

&#x20;               const response = await fetchWithRetry(url, {

&#x20;                   method: 'POST',

&#x20;                   headers: { 'Content-Type': 'application/json' },

&#x20;                   body: JSON.stringify(payload)

&#x20;               });

&#x20;               const result = await response.json();

&#x20;               return result.candidates\[0].content.parts\[0].text;

&#x20;           } catch (error) {

&#x20;               return null;

&#x20;           }

&#x20;       }



&#x20;       // Exponential backoff fetch

&#x20;       async function fetchWithRetry(url, options, retries = 3, delay = 1000) {

&#x20;           for (let i = 0; i < retries; i++) {

&#x20;               try {

&#x20;                   const response = await fetch(url, options);

&#x20;                   if (!response.ok \&\& response.status === 429) {

&#x20;                       throw new Error("Rate limited");

&#x20;                   }

&#x20;                   return response;

&#x20;               } catch (error) {

&#x20;                   if (i === retries - 1) throw error;

&#x20;                   await new Promise(res => setTimeout(res, delay \* Math.pow(2, i)));

&#x20;               }

&#x20;           }

&#x20;       }



&#x20;       // --- UTILS \& HELPERS ---

&#x20;       function appendMessage(sender, text, isSystemEvent = false) {

&#x20;           const container = document.getElementById('chat-container');

&#x20;           const msgDiv = document.createElement('div');

&#x20;           

&#x20;           if (isSystemEvent) {

&#x20;               msgDiv.className = 'flex justify-center my-4';

&#x20;               msgDiv.innerHTML = `<span class="bg-gray-200 text-gray-600 text-xs px-3 py-1 rounded-full font-semibold uppercase tracking-wider">${text}</span>`;

&#x20;           } else if (sender === 'user') {

&#x20;               msgDiv.className = 'flex justify-end mb-4 animate-\[fadeIn\_0.3s\_ease-out]';

&#x20;               msgDiv.innerHTML = `

&#x20;                   <div class="bg-blue-600 text-white rounded-2xl rounded-tr-sm py-3 px-5 max-w-\[85%] shadow-md">

&#x20;                       <p class="text-sm">${text}</p>

&#x20;                   </div>

&#x20;               `;

&#x20;           } else if (sender === 'model') {

&#x20;               msgDiv.className = 'flex justify-start mb-4 animate-\[fadeIn\_0.3s\_ease-out]';

&#x20;               // Parse markdown simple

&#x20;               const htmlText = marked.parse(text);

&#x20;               const currentMod = modules.find(m => m.id === state.currentPhaseId);

&#x20;               const iconColor = currentMod ? currentMod.color : 'blue';



&#x20;               msgDiv.innerHTML = `

&#x20;                   <div class="flex gap-3 max-w-\[90%]">

&#x20;                       <div class="w-8 h-8 rounded-full bg-gradient-to-br from-${iconColor}-500 to-${iconColor}-700 flex items-center justify-center text-white shrink-0 shadow mt-1">

&#x20;                           <i class="fa-solid fa-robot text-xs"></i>

&#x20;                       </div>

&#x20;                       <div class="bg-white border border-gray-200 text-gray-800 rounded-2xl rounded-tl-sm py-3 px-5 shadow-sm chat-message text-sm leading-relaxed">

&#x20;                           ${htmlText}

&#x20;                       </div>

&#x20;                   </div>

&#x20;               `;

&#x20;           }

&#x20;           

&#x20;           container.appendChild(msgDiv);

&#x20;           container.scrollTo({ top: container.scrollHeight, behavior: 'smooth' });

&#x20;       }



&#x20;       function showTypingIndicator(show) {

&#x20;           document.getElementById('typing-indicator').style.display = show ? 'flex' : 'none';

&#x20;       }



&#x20;       // Simulate unlocking for demo purposes (Since we can't easily parse AI intent without function calling setup in this simple environment)

&#x20;       function checkSimulatedProgression(text) {

&#x20;           const lower = text.toLowerCase();

&#x20;           // In a real scenario, the AI would emit a specific JSON or call a tool `unlockModule(module\_id)`

&#x20;           // Here, as a trick for the demo, if the user types "avançar" or "pronto", we unlock the next phase.

&#x20;           if (lower.includes('avançar') || lower.includes('concluído') || lower.includes('próximo')) {

&#x20;               if (state.highestUnlockedIndex < modules.length - 1) {

&#x20;                   const currentId = modules\[state.highestUnlockedIndex].id;

&#x20;                   if(!state.completedModules.includes(currentId)) state.completedModules.push(currentId);

&#x20;                   state.highestUnlockedIndex++;

&#x20;                   renderButtons();

&#x20;                   appendMessage('system', `Acesso liberado: ${modules\[state.highestUnlockedIndex].name}`, true);

&#x20;               } else {

&#x20;                   if(!state.completedModules.includes('m6')) state.completedModules.push('m6');

&#x20;                   renderButtons();

&#x20;               }

&#x20;           }

&#x20;       }



&#x20;       // Modals \& UI Controls

&#x20;       function showModal(id, title='', msg='') {

&#x20;           document.getElementById(id).classList.remove('hidden');

&#x20;           if(id === 'alert-modal') {

&#x20;               document.getElementById('alert-title').innerText = title;

&#x20;               document.getElementById('alert-message').innerText = msg;

&#x20;           }

&#x20;       }

&#x20;       function closeModal(id) { document.getElementById(id).classList.add('hidden'); }

&#x20;       function openShareModal() { showModal('share-modal'); }

&#x20;       

&#x20;       function copyLink() {

&#x20;           const url = window.location.href;

&#x20;           navigator.clipboard.writeText(url).then(() => {

&#x20;               const btnText = document.getElementById('copy-text');

&#x20;               btnText.innerText = "Copiado!";

&#x20;               setTimeout(() => btnText.innerText = "Copiar Link", 2000);

&#x20;           }).catch(err => {

&#x20;               // Fallback for iframe restrictions

&#x20;               const textArea = document.createElement("textarea");

&#x20;               textArea.value = url;

&#x20;               document.body.appendChild(textArea);

&#x20;               textArea.select();

&#x20;               try {

&#x20;                   document.execCommand('copy');

&#x20;                   document.getElementById('copy-text').innerText = "Copiado!";

&#x20;                   setTimeout(() => document.getElementById('copy-text').innerText = "Copiar Link", 2000);

&#x20;               } catch (err) {

&#x20;                   console.error('Fallback: Oops, unable to copy', err);

&#x20;               }

&#x20;               document.body.removeChild(textArea);

&#x20;           });

&#x20;       }

&#x20;       

&#x20;       function showAlert(title, msg) { showModal('alert-modal', title, msg); }



&#x20;   </script>

</body>

</html>

