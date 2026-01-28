<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Voice Planner Pro</title>
    <link href="https://fonts.googleapis.com/css2?family=Outfit:wght@300;500;700&display=swap" rel="stylesheet">
    <style>
        :root {
            --bg: #f0f2f5;
            --card-bg: #ffffff;
            --primary: #6c5ce7;
            --accent: #ff85a2;
            --text: #2d3436;
        }

        * { box-sizing: border-box; -webkit-tap-highlight-color: transparent; }

        body {
            font-family: 'Outfit', sans-serif;
            background-color: var(--bg);
            margin: 0;
            padding: 20px;
            color: var(--text);
            display: flex;
            flex-direction: column;
            align-items: center;
        }

        header {
            width: 100%;
            max-width: 500px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 25px;
        }

        h1 { font-size: 1.5rem; margin: 0; color: var(--primary); }

        /* The App Grid */
        .app-grid {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 15px;
            width: 100%;
            max-width: 500px;
        }

        .day-card {
            background: var(--card-bg);
            padding: 20px;
            border-radius: 24px;
            box-shadow: 0 10px 20px rgba(0,0,0,0.05);
            display: flex;
            flex-direction: column;
            align-items: center;
            transition: transform 0.2s;
            border: 2px solid transparent;
        }

        .day-card:active { transform: scale(0.95); }
        .day-card.has-tasks { border-color: var(--accent); }

        .day-name { font-weight: 700; font-size: 1.1rem; margin-bottom: 5px; }
        .task-count { font-size: 0.8rem; color: #a2a2a2; }

        /* Full Screen Modal for Editing */
        .modal {
            display: none;
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            background: var(--bg);
            z-index: 100;
            padding: 20px;
            overflow-y: auto;
        }

        .modal-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
        }

        .task-row {
            background: white;
            padding: 10px;
            border-radius: 15px;
            display: grid;
            grid-template-columns: 1fr 100px 40px;
            gap: 10px;
            margin-bottom: 10px;
            box-shadow: 0 4px 6px rgba(0,0,0,0.02);
        }

        input { border: none; background: #f8f9fa; padding: 12px; border-radius: 10px; font-size: 16px; }
        
        .btn {
            border: none;
            padding: 15px;
            border-radius: 15px;
            font-weight: 700;
            width: 100%;
            cursor: pointer;
            margin-top: 10px;
        }

        .btn-primary { background: var(--primary); color: white; }
        .btn-ghost { background: #e0e0e0; color: #666; }
        
        .close-btn { font-size: 2rem; border: none; background: none; color: var(--primary); }

        /* Status Badge */
        .status-bar {
            width: 100%;
            max-width: 500px;
            background: #fff;
            padding: 15px;
            border-radius: 15px;
            margin-bottom: 20px;
            font-size: 0.9rem;
            display: flex;
            align-items: center;
            gap: 10px;
        }
        .dot { height: 10px; width: 10px; background: #2ecc71; border-radius: 50%; display: inline-block; }
    </style>
</head>
<body>

<header>
    <h1>✨ VoicePlanner</h1>
    <button class="close-btn" onclick="location.reload()">🔄</button>
</header>

<div class="status-bar">
    <span class="dot"></span> Voice System Active
</div>

<div class="app-grid" id="appGrid">
    </div>

<div id="editorModal" class="modal">
    <div class="modal-header">
        <h2 id="modalDayTitle" style="margin:0;">Monday</h2>
        <button class="close-btn" onclick="closeModal()">✕</button>
    </div>
    
    <div id="taskList"></div>
    
    <button class="btn btn-ghost" onclick="addNewRow()">＋ Add New Task</button>
    <button class="btn btn-primary" style="margin-top:40px;" onclick="saveAndClose()">Save & Set Alarms</button>
    <button class="btn" style="color: #ff7675; background:none;" onclick="clearDay()">Clear All for this Day</button>
</div>

<script>
    const days = ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday', 'Sunday'];
    let currentEditingDay = "";
    let synth = window.speechSynthesis;

    // Build the Main Dashboard
    function renderDashboard() {
        const grid = document.getElementById('appGrid');
        grid.innerHTML = '';
        
        days.forEach(day => {
            const data = JSON.parse(localStorage.getItem(day)) || [];
            const card = document.createElement('div');
            card.className = `day-card ${data.length > 0 ? 'has-tasks' : ''}`;
            card.onclick = () => openModal(day);
            card.innerHTML = `
                <div class="day-name">${day.substring(0,3)}</div>
                <div class="task-count">${data.length} Tasks</div>
            `;
            grid.appendChild(card);
        });
    }

    function openModal(day) {
        currentEditingDay = day;
        document.getElementById('modalDayTitle').innerText = day;
        document.getElementById('editorModal').style.display = 'block';
        
        const list = document.getElementById('taskList');
        list.innerHTML = '';
        const saved = JSON.parse(localStorage.getItem(day)) || [];
        
        if(saved.length === 0) {
            addNewRow();
        } else {
            saved.forEach(t => addNewRow(t.text, t.time));
        }
    }

    function addNewRow(txt = "", tm = "") {
        const div = document.createElement('div');
        div.className = 'task-row';
        div.innerHTML = `
            <input type="text" class="t-txt" placeholder="Task..." value="${txt}">
            <input type="time" class="t-tm" value="${tm}">
            <button style="border:none; background:none; color:red;" onclick="this.parentElement.remove()">✕</button>
        `;
        document.getElementById('taskList').appendChild(div);
    }

    function saveAndClose() {
        const tasks = [];
        document.querySelectorAll('.task-row').forEach(row => {
            const text = row.querySelector('.t-txt').value;
            const time = row.querySelector('.t-tm').value;
            if(text && time) tasks.push({ text, time });
        });
        localStorage.setItem(currentEditingDay, JSON.stringify(tasks));
        closeModal();
        renderDashboard();
        speak("Schedule Updated");
    }

    function closeModal() {
        document.getElementById('editorModal').style.display = 'none';
    }

    function clearDay() {
        if(confirm("Clear everything?")) {
            localStorage.removeItem(currentEditingDay);
            saveAndClose();
        }
    }

    function speak(text) {
        const msg = new SpeechSynthesisUtterance(text);
        msg.rate = 0.9;
        synth.speak(msg);
    }

    function speak(phrase) {
        if (synth.speaking) synth.cancel(); 
        const msg = new SpeechSynthesisUtterance(phrase);
        msg.pitch = 1.1;
        msg.rate = 0.95;
        synth.speak(msg);
    }

    // Initialize
    renderDashboard();

    // Reminders Logic (Runs in background)
    setInterval(() => {
        const today = days[new Date().getDay() === 0 ? 6 : new Date().getDay() - 1];
        const now = new Date().toTimeString().substring(0, 5);
        const tasks = JSON.parse(localStorage.getItem(today)) || [];
        
        tasks.forEach(t => {
            if(t.time === now && !t.alerted) {
                speak(`Reminder: ${t.text}`);
                t.alerted = true; // Simple logic to prevent double speaking
            }
        });
    }, 30000);

</script>
</body>
</html>
