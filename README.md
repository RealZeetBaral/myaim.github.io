<!DOCTYPE html>
<html lang="bn" class="dark">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>জীৎ বড়াল-এর মিশন কন্ট্রোল</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Hind+Siliguri:wght@400;500;600;700&family=Inter:wght@400;500;700;800&display=swap" rel="stylesheet">
    <script src="https://kit.fontawesome.com/a076d05399.js" crossorigin="anonymous"></script> <!-- Placeholder for icons, will use SVG -->
    <style>
        :root {
            --bg-dark: #0F172A;
            --card-dark: #1E293B;
            --border-dark: #334155;
            --text-main-dark: #F1F5F9;
            --text-secondary-dark: #94A3B8;
            --accent-color: #38BDF8;

            --bg-light: #F1F5F9;
            --card-light: #FFFFFF;
            --border-light: #CBD5E1;
            --text-main-light: #1E293B;
            --text-secondary-light: #475569;
        }

        /* Applying theme colors */
        body {
            font-family: 'Hind Siliguri', 'Inter', sans-serif;
            transition: background-color 0.5s ease, color 0.5s ease;
        }

        html.dark body {
            background-color: var(--bg-dark);
            color: var(--text-main-dark);
        }

        html.light body {
            background-color: var(--bg-light);
            color: var(--text-main-light);
        }
        
        .card {
            transition: transform 0.3s ease, box-shadow 0.3s ease, background-color 0.5s ease, border-color 0.5s ease;
            border-radius: 1.25rem; /* More rounded corners */
            padding: 1.75rem;
            border: 1px solid;
            box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -2px rgba(0, 0, 0, 0.1);
        }

        html.dark .card {
            background-color: var(--card-dark);
            border-color: var(--border-dark);
        }
        html.light .card {
            background-color: var(--card-light);
            border-color: var(--border-light);
        }

        .card:hover {
            transform: translateY(-8px);
            box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.1), 0 8px 10px -6px rgba(0, 0, 0, 0.1);
        }

        /* Background Animation */
        body::before {
            content: '';
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -1;
            background: radial-gradient(circle, rgba(56, 189, 248, 0.1) 0%, rgba(56, 189, 248, 0) 60%);
            animation: pulse 10s infinite ease-in-out;
        }
        html.light body::before {
            background: radial-gradient(circle, rgba(56, 189, 248, 0.05) 0%, rgba(56, 189, 248, 0) 50%);
        }

        @keyframes pulse {
            0% { transform: scale(0.8); opacity: 0.5; }
            50% { transform: scale(1.2); opacity: 1; }
            100% { transform: scale(0.8); opacity: 0.5; }
        }

        @keyframes fadeIn { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }
        .fade-in { animation: fadeIn 0.8s ease-out forwards; }

        /* Countdown Style */
        .countdown-item {
            position: relative;
            width: 100px;
            height: 100px;
            display: flex;
            align-items: center;
            justify-content: center;
        }
        .countdown-svg {
            position: absolute;
            top: 0; left: 0;
            transform: rotate(-90deg);
        }
        .countdown-svg-circle {
            stroke-dasharray: 251.2; /* 2 * PI * 40 */
            transition: stroke-dashoffset 1s linear;
        }
        .countdown-content { text-align: center; }
        .countdown-number { font-size: 2rem; font-weight: 800; }
        html.dark .countdown-number { color: var(--text-main-dark); }
        html.light .countdown-number { color: var(--text-main-light); }
        .countdown-label { font-size: 0.8rem; text-transform: uppercase; letter-spacing: 1px; }
        html.dark .countdown-label { color: var(--text-secondary-dark); }
        html.light .countdown-label { color: var(--text-secondary-light); }
        
        /* Goal Item Style */
        .goal-item {
            display: flex;
            align-items: center;
            padding: 0.75rem 1rem;
            border-radius: 0.75rem;
            transition: all 0.3s ease;
        }
        html.dark .goal-item { background-color: #334155; }
        html.light .goal-item { background-color: #E2E8F0; }
        .goal-item.completed span {
            text-decoration: line-through;
            opacity: 0.5;
        }
        .goal-item:hover {
            transform: translateX(5px);
        }
        html.dark .goal-item:hover { background-color: #475569; }
        html.light .goal-item:hover { background-color: #CBD5E1; }
        
        .delete-goal-btn {
            opacity: 0;
            transition: opacity 0.3s ease;
        }
        .goal-item:hover .delete-goal-btn {
            opacity: 1;
        }
    </style>
</head>
<body class="antialiased">
    <div id="app" class="container mx-auto p-4 md:p-8 max-w-7xl">
        <!-- Header -->
        <header class="flex justify-between items-center mb-10 fade-in" style="animation-delay: 100ms;">
            <div class="text-left">
                <h1 class="text-4xl md:text-5xl font-extrabold">মিশন কন্ট্রোল</h1>
                <p class="text-lg mt-2">"কঠোর পরিশ্রমই সৌভাগ্যের চাবিকাঠি।"</p>
                <html.dark><p class="text-lg text-gray-400 mt-2">"কঠোর পরিশ্রমই সৌভাগ্যের চাবিকাঠি।"</p></html.dark>
                <html.light><p class="text-lg text-gray-500 mt-2">"কঠোর পরিশ্রমই সৌভাগ্যের চাবিকাঠি।"</p></html.light>
            </div>
            <button id="theme-toggle" class="p-3 rounded-full focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-sky-500">
                <!-- Sun/Moon Icon will be injected here -->
            </button>
        </header>

        <main class="grid grid-cols-1 lg:grid-cols-3 gap-8">
            <!-- Left Column: Countdown & Goals -->
            <div class="lg:col-span-2 space-y-8">
                <!-- Countdown -->
                <div class="card fade-in" style="animation-delay: 200ms;">
                    <h2 class="text-2xl font-bold mb-4">লক্ষ্যের পথে কাউন্টডাউন</h2>
                    <div class="p-4 rounded-lg">
                        <h3 class="text-xl font-semibold text-center mb-6">HSC পরীক্ষা ২০২৭</h3>
                        <div id="countdown" class="flex flex-wrap justify-center items-center gap-4">
                            <!-- Countdown items injected by JS -->
                        </div>
                    </div>
                </div>

                <!-- Goals -->
                <div class="card fade-in" style="animation-delay: 300ms;">
                    <div class="flex justify-between items-center mb-4">
                        <h2 class="text-2xl font-bold">আমার প্রধান লক্ষ্যসমূহ</h2>
                        <div id="goal-loader" class="animate-spin rounded-full h-5 w-5 border-b-2 border-sky-400"></div>
                    </div>
                    <ul id="goal-list" class="space-y-3 mb-4">
                        <!-- Goals injected by JS -->
                    </ul>
                    <div class="mt-4 flex gap-2">
                        <input type="text" id="new-goal-input" placeholder="নতুন লক্ষ্য যোগ করুন..." class="w-full p-3 rounded-lg focus:outline-none focus:ring-2 focus:ring-sky-500 border text-base">
                        <html.dark><input class="bg-gray-700 border-gray-600 text-white placeholder-gray-400"></html.dark>
                        <html.light><input class="bg-gray-100 border-gray-300 text-black placeholder-gray-500"></html.light>
                        <button id="add-goal-btn" class="bg-sky-500 hover:bg-sky-600 text-white font-bold py-2 px-5 rounded-lg transition-colors duration-300">যোগ</button>
                    </div>
                </div>
            </div>

            <!-- Right Column: Tools & Notes -->
            <div class="space-y-8">
                <!-- Clock & Date -->
                <div class="card fade-in" style="animation-delay: 400ms;">
                     <div class="p-4 rounded-lg text-center">
                        <html.dark><p class="text-gray-400 text-sm">বরিশাল, বাংলাদেশ</p></html.dark>
                        <html.light><p class="text-gray-500 text-sm">বরিশাল, বাংলাদেশ</p></html.light>
                        <div id="clock" class="text-5xl font-bold tracking-wider my-2"></div>
                        <div id="date" class="text-lg"></div>
                     </div>
                </div>

                <!-- Personal Notes -->
                <div class="card h-full flex flex-col fade-in" style="animation-delay: 500ms;">
                    <div class="flex justify-between items-center mb-4">
                         <h2 class="text-2xl font-bold">ব্যক্তিগত নোট</h2>
                         <div id="saveStatus" class="text-sm transition-opacity duration-500 opacity-0 flex items-center gap-2">
                            <!-- Status Icon & Text injected by JS -->
                         </div>
                    </div>
                    <textarea id="notes" class="flex-grow w-full p-3 rounded-lg focus:outline-none focus:ring-2 focus:ring-sky-500 text-base" placeholder="আপনার চিন্তা, ধারণা বা আজকের কাজগুলো এখানে লিখুন..."></textarea>
                    <html.dark><textarea class="bg-gray-800 border-gray-600 text-gray-200"></textarea></html.dark>
                    <html.light><textarea class="bg-gray-100 border-gray-300 text-gray-900"></textarea></html.light>
                </div>
            </div>
        </main>
    </div>

    <script type="module">
        // Firebase Imports
        import { initializeApp } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-app.js";
        import { getAuth, signInAnonymously, signInWithCustomToken, onAuthStateChanged } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-auth.js";
        import { getFirestore, doc, setDoc, getDoc, onSnapshot, collection, addDoc, deleteDoc, updateDoc, query, getDocs } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-firestore.js";

        // --- Global Config & State ---
        const config = {
            appId: typeof __app_id !== 'undefined' ? __app_id : 'default-app-id',
            firebase: typeof __firebase_config !== 'undefined' ? JSON.parse(__firebase_config) : {},
            authToken: typeof __initial_auth_token !== 'undefined' ? __initial_auth_token : null,
            hscExamDate: new Date('April 1, 2027 09:00:00')
        };
        
        let state = {
            db: null,
            auth: null,
            userId: null,
            docRefs: {},
            noteSaveTimeout: null,
            theme: localStorage.getItem('theme') || 'dark',
            goals: []
        };

        // --- UI Elements ---
        const ui = {
            themeToggle: document.getElementById('theme-toggle'),
            countdown: document.getElementById('countdown'),
            clock: document.getElementById('clock'),
            date: document.getElementById('date'),
            notes: document.getElementById('notes'),
            saveStatus: document.getElementById('saveStatus'),
            goalList: document.getElementById('goal-list'),
            newGoalInput: document.getElementById('new-goal-input'),
            addGoalBtn: document.getElementById('add-goal-btn'),
            goalLoader: document.getElementById('goal-loader')
        };
        
        const icons = {
            sun: `<svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 3v1m0 16v1m9-9h-1M4 12H3m15.364 6.364l-.707-.707M6.343 6.343l-.707-.707m12.728 0l-.707.707M6.343 17.657l-.707.707M16 12a4 4 0 11-8 0 4 4 0 018 0z"></path></svg>`,
            moon: `<svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M20.354 15.354A9 9 0 018.646 3.646 9.003 9.003 0 0012 21a9.003 9.003 0 008.354-5.646z"></path></svg>`,
            saving: `<svg class="animate-spin h-5 w-5 text-sky-400" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24"><circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" stroke-width="4"></circle><path class="opacity-75" fill="currentColor" d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z"></path></svg>`,
            saved: `<svg class="h-5 w-5 text-green-400" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7"></path></svg>`,
            trash: `<svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-red-400" viewBox="0 0 20 20" fill="currentColor"><path fill-rule="evenodd" d="M9 2a1 1 0 00-.894.553L7.382 4H4a1 1 0 000 2v10a2 2 0 002 2h8a2 2 0 002-2V6a1 1 0 100-2h-3.382l-.724-1.447A1 1 0 0011 2H9zM7 8a1 1 0 012 0v6a1 1 0 11-2 0V8zm5-1a1 1 0 00-1 1v6a1 1 0 102 0V8a1 1 0 00-1-1z" clip-rule="evenodd" /></svg>`
        };
        
        // --- Core Functions ---

        function setupTheme() {
            if (state.theme === 'light') {
                document.documentElement.classList.remove('dark');
                document.documentElement.classList.add('light');
                ui.themeToggle.innerHTML = icons.moon;
            } else {
                document.documentElement.classList.remove('light');
                document.documentElement.classList.add('dark');
                ui.themeToggle.innerHTML = icons.sun;
            }
        }
        
        function toggleTheme() {
            state.theme = (state.theme === 'dark') ? 'light' : 'dark';
            localStorage.setItem('theme', state.theme);
            setupTheme();
            if (state.docRefs.settings) {
                setDoc(state.docRefs.settings, { theme: state.theme }, { merge: true });
            }
        }

        function createCountdownUnit(label, value, max) {
            const dashOffset = 251.2 * (1 - (value / max));
            return `
                <div class="countdown-item">
                    <svg class="countdown-svg w-full h-full" viewBox="0 0 100 100">
                        <circle class="stroke-current opacity-20" cx="50" cy="50" r="40" fill="transparent" stroke-width="8"></circle>
                        <circle class="countdown-svg-circle text-sky-400 stroke-current" cx="50" cy="50" r="40" fill="transparent" stroke-width="8" stroke-linecap="round" style="stroke-dashoffset: ${dashOffset};"></circle>
                    </svg>
                    <div class="countdown-content">
                        <span class="countdown-number">${value}</span>
                        <span class="countdown-label">${label}</span>
                    </div>
                </div>`;
        }
        
        function updateCountdown() {
            const now = new Date().getTime();
            const distance = config.hscExamDate.getTime() - now;

            if (distance < 0) {
                ui.countdown.innerHTML = `<div class="text-2xl font-bold text-green-400">পরীক্ষা সম্পন্ন! ভবিষ্যতের জন্য শুভকামনা!</div>`;
                return;
            }

            const days = Math.floor(distance / (1000 * 60 * 60 * 24));
            const hours = Math.floor((distance % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
            const minutes = Math.floor((distance % (1000 * 60 * 60)) / (1000 * 60));
            const seconds = Math.floor((distance % (1000 * 60)) / 1000);

            ui.countdown.innerHTML = 
                createCountdownUnit('দিন', days, 365) +
                createCountdownUnit('ঘন্টা', hours, 24) +
                createCountdownUnit('মিনিট', minutes, 60) +
                createCountdownUnit('সেকেন্ড', seconds, 60);
        }

        function updateClockAndDate() {
            const now = new Date();
            const timeOpts = { hour: '2-digit', minute: '2-digit', second: '2-digit', hour12: true };
            const dateOpts = { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' };
            
            ui.clock.textContent = now.toLocaleTimeString('bn-BD', timeOpts);
            ui.date.textContent = now.toLocaleDateString('bn-BD', dateOpts);
        }
        
        function showSaveStatus(type, message) {
            const icon = type === 'saving' ? icons.saving : icons.saved;
            ui.saveStatus.innerHTML = `${icon} <span class="text-sm">${message}</span>`;
            ui.saveStatus.style.opacity = '1';
            
            if (type === 'saved') {
                setTimeout(() => ui.saveStatus.style.opacity = '0', 2000);
            }
        }
        
        async function saveNote() {
            if (!state.docRefs.notes) return;
            showSaveStatus('saving', 'সংরক্ষণ করা হচ্ছে...');
            try {
                await setDoc(state.docRefs.notes, { content: ui.notes.value }, { merge: true });
                showSaveStatus('saved', 'সংরক্ষিত');
            } catch (error) {
                console.error("Error saving note: ", error);
            }
        }

        function renderGoals() {
            ui.goalList.innerHTML = '';
            if (state.goals.length === 0) {
                ui.goalList.innerHTML = `<p class="text-center p-4">কোনো লক্ষ্য এখনো যোগ করা হয়নি।</p>`;
                return;
            }
            state.goals.forEach(goal => {
                const li = document.createElement('li');
                li.className = `goal-item ${goal.completed ? 'completed' : ''}`;
                li.dataset.id = goal.id;
                li.innerHTML = `
                    <input type="checkbox" ${goal.completed ? 'checked' : ''} class="form-checkbox h-5 w-5 rounded text-sky-500 bg-transparent border-2 border-gray-400 focus:ring-sky-500 cursor-pointer mr-4">
                    <span class="flex-grow">${goal.text}</span>
                    <button class="delete-goal-btn ml-auto p-1 rounded-full hover:bg-red-500/20">${icons.trash}</button>
                `;
                ui.goalList.appendChild(li);

                li.querySelector('input[type="checkbox"]').addEventListener('change', (e) => toggleGoalCompletion(goal.id, e.target.checked));
                li.querySelector('.delete-goal-btn').addEventListener('click', () => deleteGoal(goal.id));
            });
        }

        // --- Firebase Functions ---
        
        async function addGoal() {
            const text = ui.newGoalInput.value.trim();
            if (text === '' || !state.docRefs.goals) return;
            
            ui.addGoalBtn.disabled = true;
            try {
                const newGoal = { text, completed: false, createdAt: new Date() };
                const docRef = await addDoc(state.docRefs.goals, newGoal);
                state.goals.push({ id: docRef.id, ...newGoal });
                renderGoals();
                ui.newGoalInput.value = '';
            } catch(e) { console.error("Error adding goal: ", e); }
            finally { ui.addGoalBtn.disabled = false; }
        }

        async function toggleGoalCompletion(id, completed) {
            const goalIndex = state.goals.findIndex(g => g.id === id);
            if (goalIndex === -1) return;
            
            state.goals[goalIndex].completed = completed;
            renderGoals();

            const goalDocRef = doc(state.db, `artifacts/${config.appId}/users/${state.userId}/goals/${id}`);
            await updateDoc(goalDocRef, { completed });
        }
        
        async function deleteGoal(id) {
            state.goals = state.goals.filter(g => g.id !== id);
            renderGoals();
            const goalDocRef = doc(state.db, `artifacts/${config.appId}/users/${state.userId}/goals/${id}`);
            await deleteDoc(goalDocRef);
        }

        async function initializeFirebase() {
            if (Object.keys(config.firebase).length === 0) {
                console.warn("Firebase config not available.");
                return;
            }
            try {
                const app = initializeApp(config.firebase);
                state.db = getFirestore(app);
                state.auth = getAuth(app);
                
                onAuthStateChanged(state.auth, async (user) => {
                    if (user) {
                        state.userId = user.uid;
                        
                        // Setup Doc References
                        state.docRefs.notes = doc(state.db, `artifacts/${config.appId}/users/${state.userId}/personal_notes/dashboard_note`);
                        state.docRefs.settings = doc(state.db, `artifacts/${config.appId}/users/${state.userId}/settings/dashboard_settings`);
                        state.docRefs.goals = collection(state.db, `artifacts/${config.appId}/users/${state.userId}/goals`);

                        // Notes listener
                        onSnapshot(state.docRefs.notes, (doc) => {
                            if (doc.exists() && ui.notes.value !== doc.data().content) {
                                ui.notes.value = doc.data().content;
                            }
                        });
                        
                        // Settings listener (for theme)
                        const settingsDoc = await getDoc(state.docRefs.settings);
                        if (settingsDoc.exists() && settingsDoc.data().theme) {
                            state.theme = settingsDoc.data().theme;
                            localStorage.setItem('theme', state.theme);
                            setupTheme();
                        }

                        // Goals listener
                        const q = query(state.docRefs.goals);
                        const initialSnapshot = await getDocs(q);
                        if (initialSnapshot.empty) {
                             const initialGoals = [
                                { text: 'HSC পরীক্ষায় প্রতিটি বিষয়ে ৯৫+ নম্বর অর্জন।', completed: false },
                                { text: 'সেরা প্রতিষ্ঠানে ভর্তি: ঢামেক, বুয়েট, ঢাবি।', completed: false },
                                { text: 'বিশ্বসেরা বিশ্ববিদ্যালয়ে সম্পূর্ণ অর্থায়নে স্কলারশিপ।', completed: false },
                            ];
                            for (const goal of initialGoals) {
                                await addDoc(state.docRefs.goals, { ...goal, createdAt: new Date() });
                            }
                        }

                        onSnapshot(q, (querySnapshot) => {
                            state.goals = [];
                            querySnapshot.forEach((doc) => {
                                state.goals.push({ id: doc.id, ...doc.data() });
                            });
                             state.goals.sort((a, b) => a.createdAt.toDate() - b.createdAt.toDate());
                            ui.goalLoader.style.display = 'none';
                            renderGoals();
                        });

                    }
                });

                if (config.authToken) {
                    await signInWithCustomToken(state.auth, config.authToken);
                } else {
                    await signInAnonymously(state.auth);
                }
            } catch (error) {
                console.error("Firebase Initialization Error:", error);
            }
        }
        
        // --- Event Listeners ---
        function setupEventListeners() {
            ui.themeToggle.addEventListener('click', toggleTheme);
            ui.notes.addEventListener('input', () => {
                clearTimeout(state.noteSaveTimeout);
                state.noteSaveTimeout = setTimeout(saveNote, 1000);
            });
            ui.addGoalBtn.addEventListener('click', addGoal);
            ui.newGoalInput.addEventListener('keypress', (e) => {
                if(e.key === 'Enter') addGoal();
            });
        }
        
        // --- App Initialization ---
        function init() {
            setupTheme();
            setupEventListeners();
            updateCountdown();
            updateClockAndDate();
            setInterval(updateCountdown, 1000);
            setInterval(updateClockAndDate, 1000);
            initializeFirebase();
        }

        init();
    </script>
</body>
</html>
