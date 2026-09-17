<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Classroom Hub - EduPortal</title>
    <style>
        :root {
            --primary: #4361ee;
            --primary-hover: #3a0ca3;
            --secondary: #4cc9f0;
            --bg: #f8f9fa;
            --card-bg: #ffffff;
            --text: #212529;
            --gray: #6c757d;
            --border: #dee2e6;
            --danger: #ef476f;
            --success: #06d6a0;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background-color: var(--bg);
            color: var(--text);
            min-height: 100vh;
            display: flex;
            flex-direction: column;
        }

        header {
            background-color: var(--card-bg);
            border-bottom: 1px solid var(--border);
            padding: 1rem 2rem;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .logo {
            font-size: 1.5rem;
            font-weight: bold;
            color: var(--primary);
        }

        .container {
            max-width: 1000px;
            margin: 2rem auto;
            padding: 0 1rem;
            width: 100%;
            flex: 1;
        }

        .card {
            background: var(--card-bg);
            border: 1px solid var(--border);
            border-radius: 8px;
            padding: 2rem;
            box-shadow: 0 4px 6px rgba(0,0,0,0.02);
            margin-bottom: 1.5rem;
        }

        h1, h2, h3 {
            margin-bottom: 1rem;
        }

        .form-group {
            margin-bottom: 1rem;
        }

        label {
            display: block;
            margin-bottom: 0.5rem;
            font-weight: 600;
            color: var(--gray);
            font-size: 0.9rem;
        }

        input, select, textarea {
            width: 100%;
            padding: 0.75rem;
            border: 1px solid var(--border);
            border-radius: 4px;
            font-size: 1rem;
            outline: none;
            transition: border-color 0.2s;
        }

        input:focus, select:focus, textarea:focus {
            border-color: var(--primary);
        }

        button {
            background-color: var(--primary);
            color: white;
            border: none;
            padding: 0.75rem 1.5rem;
            border-radius: 4px;
            font-size: 1rem;
            font-weight: 600;
            cursor: pointer;
            transition: background-color 0.2s;
        }

        button:hover {
            background-color: var(--primary-hover);
        }

        button.secondary {
            background-color: var(--gray);
        }
        button.secondary:hover {
            background-color: #5a6268;
        }

        button.danger {
            background-color: var(--danger);
        }
        button.danger:hover {
            background-color: #d90429;
        }

        .auth-container {
            max-width: 400px;
            margin: 4rem auto;
        }

        .tabs {
            display: flex;
            margin-bottom: 1.5rem;
            border-bottom: 1px solid var(--border);
        }

        .tab {
            padding: 0.75rem 1.5rem;
            cursor: pointer;
            font-weight: 600;
            color: var(--gray);
            border-bottom: 2px solid transparent;
        }

        .tab.active {
            color: var(--primary);
            border-bottom-color: var(--primary);
        }

        .class-code-badge {
            background: #e9ecef;
            padding: 0.25rem 0.5rem;
            border-radius: 4px;
            font-family: monospace;
            font-weight: bold;
            letter-spacing: 1px;
            color: var(--primary);
        }

        .flex-row {
            display: flex;
            gap: 1rem;
            align-items: center;
        }

        .grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
            gap: 1.5rem;
        }

        .class-card {
            border: 1px solid var(--border);
            border-radius: 8px;
            padding: 1.5rem;
            background: white;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
        }

        .class-card h3 {
            color: var(--primary);
        }

        .hidden {
            display: none !important;
        }

        .nav-right {
            display: flex;
            gap: 1rem;
            align-items: center;
        }
        
        .assignment-item {
            padding: 1rem;
            border: 1px solid var(--border);
            border-radius: 6px;
            margin-bottom: 0.75rem;
            background: #fafafa;
        }
    </style>
</head>
<body>

    <header>
        <div class="logo">EduPortal Hub</div>
        <div id="nav-user-info" class="nav-right hidden">
            <span id="welcome-msg" style="font-weight: 600;"></span>
            <button class="secondary" onclick="logout()">Log Out</button>
        </div>
    </header>

    <div class="container">
        
        <!-- AUTH SECTION -->
        <div id="auth-section" class="auth-container card">
            <div class="tabs">
                <div class="tab active" onclick="switchAuthTab('login')">Login</div>
                <div class="tab" onclick="switchAuthTab('register')">Register</div>
            </div>

            <!-- Login Form -->
            <div id="login-form">
                <h2>Welcome Back</h2>
                <div class="form-group">
                    <label>Username</label>
                    <input type="text" id="login-username" placeholder="Enter username">
                </div>
                <div class="form-group">
                    <label>Password</label>
                    <input type="password" id="login-password" placeholder="Enter password">
                </div>
                <button onclick="login()" style="width: 100%;">Log In</button>
            </div>

            <!-- Register Form -->
            <div id="register-form" class="hidden">
                <h2>Create Account</h2>
                <div class="form-group">
                    <label>Username</label>
                    <input type="text" id="reg-username" placeholder="Choose a username">
                </div>
                <div class="form-group">
                    <label>Password</label>
                    <input type="password" id="reg-password" placeholder="Choose a password">
                </div>
                <div class="form-group">
                    <label>I am a:</label>
                    <select id="reg-role">
                        <option value="teacher">Teacher</option>
                        <option value="student">Student</option>
                    </select>
                </div>
                <button onclick="register()" style="width: 100%;">Sign Up</button>
            </div>
        </div>

        <!-- TEACHER DASHBOARD -->
        <div id="teacher-dashboard" class="hidden">
            <div class="card flex-row" style="justify-content: space-between;">
                <div>
                    <h2>Teacher Dashboard</h2>
                    <p style="color: var(--gray);">Create classes, manage students, and distribute assignments.</p>
                </div>
                <button onclick="openCreateClassModal()">+ Create New Class</button>
            </div>

            <h2>My Classes</h2>
            <div id="teacher-classes-grid" class="grid">
                <!-- Populated via JS -->
            </div>
        </div>

        <!-- TEACHER CLASS DETAIL VIEW -->
        <div id="teacher-class-detail" class="hidden">
            <button class="secondary" onclick="backToTeacherDashboard()" style="margin-bottom: 1rem;">← Back to Classes</button>
            <div class="card">
                <h1 id="t-class-title"></h1>
                <p><strong>Description:</strong> <span id="t-class-desc"></span></p>
                <p style="margin-top: 0.5rem;"><strong>Class Code:</strong> <span id="t-class-code" class="class-code-badge"></span></p>
            </div>

            <div class="grid" style="grid-template-columns: 1fr 1fr;">
                <div class="card">
                    <h2>Assignments</h2>
                    <div class="form-group">
                        <label>Assignment Title</label>
                        <input type="text" id="new-assign-title" placeholder="e.g., Chapter 1 Homework">
                    </div>
                    <div class="form-group">
                        <label>Instructions</label>
                        <textarea id="new-assign-desc" rows="3" placeholder="Describe instructions..."></textarea>
                    </div>
                    <button onclick="createAssignment()">Post Assignment</button>
                    
                    <div id="teacher-assignments-list" style="margin-top: 1.5rem;">
                        <!-- Populated via JS -->
                    </div>
                </div>

                <div class="card">
                    <h2>Enrolled Students</h2>
                    <ul id="teacher-student-list" style="list-style-type: none; padding: 0;">
                        <!-- Populated via JS -->
                    </ul>
                </div>
            </div>
        </div>

        <!-- STUDENT DASHBOARD -->
        <div id="student-dashboard" class="hidden">
            <div class="card flex-row" style="justify-content: space-between;">
                <div>
                    <h2>Student Dashboard</h2>
                    <p style="color: var(--gray);">Join your teacher's class code to view assignments.</p>
                </div>
                <div class="flex-row">
                    <input type="text" id="join-code-input" placeholder="Enter Class Code (e.g. AB12CD)" style="text-transform: uppercase;">
                    <button onclick="joinClass()">Join Class</button>
                </div>
            </div>

            <h2>Enrolled Classes</h2>
            <div id="student-classes-grid" class="grid">
                <!-- Populated via JS -->
            </div>
        </div>

        <!-- STUDENT CLASS DETAIL VIEW -->
        <div id="student-class-detail" class="hidden">
            <button class="secondary" onclick="backToStudentDashboard()" style="margin-bottom: 1rem;">← Back to My Classes</button>
            <div class="card">
                <h1 id="s-class-title"></h1>
                <p><strong>Teacher:</strong> <span id="s-class-teacher"></span></p>
                <p><strong>Description:</strong> <span id="s-class-desc"></span></p>
            </div>

            <div class="card">
                <h2>Assignments & Work</h2>
                <div id="student-assignments-list">
                    <!-- Populated via JS -->
                </div>
            </div>
        </div>

    </div>

    <!-- MODAL FOR CREATING CLASS -->
    <div id="create-class-modal" class="hidden" style="position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.5); display: flex; align-items: center; justify-content: center;">
        <div class="card" style="width: 400px; margin: 0;">
            <h2>Create New Class</h2>
            <div class="form-group">
                <label>Class Name</label>
                <input type="text" id="class-name-input" placeholder="e.g. Algebra Period 3">
            </div>
            <div class="form-group">
                <label>Description / Subject</label>
                <input type="text" id="class-desc-input" placeholder="e.g. Introduction to linear functions">
            </div>
            <div class="flex-row" style="justify-content: flex-end;">
                <button class="secondary" onclick="closeCreateClassModal()">Cancel</button>
                <button onclick="saveNewClass()">Create</button>
            </div>
        </div>
    </div>

    <script>
        // LocalStorage database initialization
        let db = JSON.parse(localStorage.getItem('edu_db')) || {
            users: [],
            classes: [], // { id, name, description, code, teacher, students: [], assignments: [] }
            submissions: [] // { classId, assignmentId, studentUsername, text, submittedAt }
        };

        function saveDB() {
            localStorage.setItem('edu_db', JSON.stringify(db));
        }

        let currentUser = JSON.parse(localStorage.getItem('edu_current_user')) || null;
        let activeClassId = null;

        // On Load initialization
        window.onload = function() {
            if (currentUser) {
                showDashboard();
            }
        };

        // Auth Tab Switching
        function switchAuthTab(tab) {
            document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
            if (tab === 'login') {
                document.querySelectorAll('.tab')[0].classList.add('active');
                document.getElementById('login-form').classList.remove('hidden');
                document.getElementById('register-form').classList.add('hidden');
            } else {
                document.querySelectorAll('.tab')[1].classList.add('active');
                document.getElementById('register-form').classList.remove('hidden');
                document.getElementById('login-form').classList.add('hidden');
            }
        }

        // Register Account
        function register() {
            const username = document.getElementById('reg-username').value.trim();
            const password = document.getElementById('reg-password').value;
            const role = document.getElementById('reg-role').value;

            if (!username || !password) {
                alert('Please fill out all fields.');
                return;
            }

            if (db.users.find(u => u.username === username)) {
                alert('Username already exists.');
                return;
            }

            db.users.push({ username, password, role });
            saveDB();
            alert('Account created successfully! Please log in.');
            switchAuthTab('login');
        }

        // Login Account
        function login() {
            const username = document.getElementById('login-username').value.trim();
            const password = document.getElementById('login-password').value;

            const user = db.users.find(u => u.username === username && u.password === password);
            if (!user) {
                alert('Invalid username or password.');
                return;
            }

            currentUser = user;
            localStorage.setItem('edu_current_user', JSON.stringify(currentUser));
            showDashboard();
        }

        // Logout
        function logout() {
            currentUser = null;
            activeClassId = null;
            localStorage.removeItem('edu_current_user');
            
            // Reset UI states
            document.getElementById('auth-section').classList.remove('hidden');
            document.getElementById('teacher-dashboard').classList.add('hidden');
            document.getElementById('student-dashboard').classList.add('hidden');
            document.getElementById('teacher-class-detail').classList.add('hidden');
            document.getElementById('student-class-detail').classList.add('hidden');
            document.getElementById('nav-user-info').classList.add('hidden');
            
            // Clear inputs
            document.getElementById('login-username').value = '';
            document.getElementById('login-password').value = '';
        }

        // Show relevant dashboard based on role
        function showDashboard() {
            document.getElementById('auth-section').classList.add('hidden');
            document.getElementById('nav-user-info').classList.remove('hidden');
            document.getElementById('welcome-msg').innerText = `Hello, ${currentUser.username} (${currentUser.role})`;

            if (currentUser.role === 'teacher') {
                document.getElementById('teacher-dashboard').classList.remove('hidden');
                loadTeacherClasses();
            } else {
                document.getElementById('student-dashboard').classList.remove('hidden');
                loadStudentClasses();
            }
        }

        // --- TEACHER FUNCTIONS ---
        function openCreateClassModal() {
            document.getElementById('create-class-modal').classList.remove('hidden');
        }

        function closeCreateClassModal() {
            document.getElementById('create-class-modal').classList.add('hidden');
            document.getElementById('class-name-input').value = '';
            document.getElementById('class-desc-input').value = '';
        }

        function generateCode() {
            const chars = 'ABCDEFGHJKLMNPQRSTUVWXYZ23456789';
            let code = '';
            for (let i = 0; i < 6; i++) {
                code += chars.charAt(Math.floor(Math.random() * chars.length));
            }
            return code;
        }

        function saveNewClass() {
            const name = document.getElementById('class-name-input').value.trim();
            const description = document.getElementById('class-desc-input').value.trim();

            if (!name) {
                alert('Please provide a class name.');
                return;
            }

            const newClass = {
                id: 'class_' + Date.now(),
                name,
                description,
                code: generateCode(),
                teacher: currentUser.username,
                students: [],
                assignments: []
            };

            db.classes.push(newClass);
            saveDB();
            closeCreateClassModal();
            loadTeacherClasses();
        }

        function loadTeacherClasses() {
            const grid = document.getElementById('teacher-classes-grid');
            grid.innerHTML = '';

            const myClasses = db.classes.filter(c => c.teacher === currentUser.username);

            if (myClasses.length === 0) {
                grid.innerHTML = '<p style="color: var(--gray);">No classes created yet. Click "Create New Class" to start!</p>';
                return;
            }

            myClasses.forEach(c => {
                grid.innerHTML += `
                    <div class="class-card">
                        <div>
                            <h3>${c.name}</h3>
                            <p style="color: var(--gray); font-size: 0.9rem; margin-top: 0.25rem;">${c.description || 'No description'}</p>
                            <p style="margin-top: 1rem;">Code: <span class="class-code-badge">${c.code}</span></p>
                            <p style="margin-top: 0.5rem; font-size: 0.85rem; color: var(--gray);">${c.students.length} students enrolled</p>
                        </div>
                        <button style="margin-top: 1.5rem;" onclick="openTeacherClass('${c.id}')">Manage Class</button>
                    </div>
                `;
            });
        }

        function openTeacherClass(classId) {
            activeClassId = classId;
            const c = db.classes.find(item => item.id === classId);

            document.getElementById('teacher-dashboard').classList.add('hidden');
            document.getElementById('teacher-class-detail').classList.remove('hidden');

            document.getElementById('t-class-title').innerText = c.name;
            document.getElementById('t-class-desc').innerText = c.description || 'None';
            document.getElementById('t-class-code').innerText = c.code;

            renderTeacherAssignments();
            renderTeacherStudents();
        }

        function backToTeacherDashboard() {
            activeClassId = null;
            document.getElementById('teacher-class-detail').classList.add('hidden');
            document.getElementById('teacher-dashboard').classList.remove('hidden');
            loadTeacherClasses();
        }

        function createAssignment() {
            const title = document.getElementById('new-assign-title').value.trim();
            const description = document.getElementById('new-assign-desc').value.trim();

            if (!title) {
                alert('Assignment needs a title.');
                return;
            }

            const c = db.classes.find(item => item.id === activeClassId);
            c.assignments.push({
                id: 'assign_' + Date.now(),
                title,
                description,
                date: new Date().toLocaleDateString()
            });

            saveDB();
            document.getElementById('new-assign-title').value = '';
            document.getElementById('new-assign-desc').value = '';
            renderTeacherAssignments();
        }

        function renderTeacherAssignments() {
            const c = db.classes.find(item => item.id === activeClassId);
            const list = document.getElementById('teacher-assignments-list');
            list.innerHTML = '<h3>Posted Assignments</h3>';

            if (c.assignments.length === 0) {
                list.innerHTML += '<p style="color: var(--gray);">No assignments posted yet.</p>';
                return;
            }

            c.assignments.forEach(a => {
                // Find student submissions for this assignment
                const subs = db.submissions.filter(s => s.classId === c.id && s.assignmentId === a.id);

                list.innerHTML += `
                    <div class="assignment-item">
                        <h4>${a.title}</h4>
                        <p style="font-size: 0.9rem; color: var(--gray);">${a.description}</p>
                        <div style="margin-top: 0.5rem; font-size: 0.85rem;">
                            <strong>Submissions (${subs.length}):</strong>
                            <ul style="margin-left: 1.2rem; margin-top: 0.25rem;">
                                ${subs.length === 0 ? '<li>None yet</li>' : subs.map(s => `<li><b>${s.studentUsername}:</b> ${s.text} <span style="color:var(--gray)">(${s.submittedAt})</span></li>`).join('')}
                            </ul>
                        </div>
                    </div>
                `;
            });
        }

        function renderTeacherStudents() {
            const c = db.classes.find(item => item.id === activeClassId);
            const list = document.getElementById('teacher-student-list');
            list.innerHTML = '';

            if (c.students.length === 0) {
                list.innerHTML = '<li style="color: var(--gray);">No students have joined yet. Share your class code with them!</li>';
                return;
            }

            c.students.forEach(student => {
                list.innerHTML += `<li style="padding: 0.5rem 0; border-bottom: 1px solid var(--border); display: flex; justify-content: space-between;"><span>👤 ${student}</span></li>`;
            });
        }

        // --- STUDENT FUNCTIONS ---
        function joinClass() {
            const code = document.getElementById('join-code-input').value.trim().toUpperCase();
            if (!code) {
                alert('Please type a class code.');
                return;
            }

            const targetClass = db.classes.find(c => c.code === code);
            if (!targetClass) {
                alert('Class not found with that code.');
                return;
            }

            if (targetClass.students.includes(currentUser.username)) {
                alert('You are already enrolled in this class.');
                return;
            }

            targetClass.students.push(currentUser.username);
            saveDB();
            document.getElementById('join-code-input').value = '';
            loadStudentClasses();
            alert(`Successfully joined ${targetClass.name}!`);
        }

        function loadStudentClasses() {
            const grid = document.getElementById('student-classes-grid');
            grid.innerHTML = '';

            const myClasses = db.classes.filter(c => c.students.includes(currentUser.username));

            if (myClasses.length === 0) {
                grid.innerHTML = '<p style="color: var(--gray);">You are not enrolled in any classes. Enter a code above to join one!</p>';
                return;
            }

            myClasses.forEach(c => {
                grid.innerHTML += `
                    <div class="class-card">
                        <div>
                            <h3>${c.name}</h3>
                            <p style="color: var(--gray); font-size: 0.9rem; margin-top: 0.25rem;">Teacher: ${c.teacher}</p>
                            <p style="color: var(--gray); font-size: 0.85rem; margin-top: 0.5rem;">${c.description || ''}</p>
                        </div>
                        <button style="margin-top: 1.5rem;" onclick="openStudentClass('${c.id}')">View Class</button>
                    </div>
                `;
            });
        }

        function openStudentClass(classId) {
            activeClassId = classId;
            const c = db.classes.find(item => item.id === classId);

            document.getElementById('student-dashboard').classList.add('hidden');
            document.getElementById('student-class-detail').classList.remove('hidden');

            document.getElementById('s-class-title').innerText = c.name;
            document.getElementById('s-class-teacher').innerText = c.teacher;
            document.getElementById('s-class-desc').innerText = c.description || 'None';

            renderStudentAssignments();
        }

        function backToStudentDashboard() {
            activeClassId = null;
            document.getElementById('student-class-detail').classList.add('hidden');
            document.getElementById('student-dashboard').classList.remove('hidden');
            loadStudentClasses();
        }

        function renderStudentAssignments() {
            const c = db.classes.find(item => item.id === activeClassId);
            const container = document.getElementById('student-assignments-list');
            container.innerHTML = '';

            if (c.assignments.length === 0) {
                container.innerHTML = '<p style="color: var(--gray);">No assignments posted by your teacher yet.</p>';
                return;
            }

            c.assignments.forEach(a => {
                // Check if student already submitted
                const existingSub = db.submissions.find(s => s.classId === c.id && s.assignmentId === a.id && s.studentUsername === currentUser.username);

                container.innerHTML += `
                    <div class="assignment-item">
                        <h4>${a.title} <span style="font-size: 0.8rem; font-weight: normal; color: var(--gray);">Posted: ${a.date}</span></h4>
                        <p style="margin: 0.5rem 0; font-size: 0.95rem;">${a.description}</p>
                        <div style="margin-top: 1rem; border-top: 1px dashed var(--border); padding-top: 0.75rem;">
                            ${existingSub ? 
                                `<p style="color: var::success; font-size: 0.9rem;">✅ <strong>Submitted:</strong> ${existingSub.text} <span style="color:var(--gray)">(${existingSub.submittedAt})</span></p>` :
                                `<div class="flex-row">
                                    <input type="text" id="sub-input_${a.id}" placeholder="Type your answer or paste link..." style="flex: 1;">
                                    <button onclick="submitAssignment('${a.id}')">Turn In</button>
                                 </div>`
                            }
                        </div>
                    </div>
                `;
            });
        }

        function submitAssignment(assignmentId) {
            const inputVal = document.getElementById(`sub-input_${assignmentId}`).value.trim();
            if (!inputVal) {
                alert('Please write your work before submitting.');
                return;
            }

            db.submissions.push({
                classId: activeClassId,
                assignmentId: assignmentId,
                studentUsername: currentUser.username,
                text: inputVal,
                submittedAt: new Date().toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' })
            });

            saveDB();
            renderStudentAssignments();
        }
    </script>
</body>
</html>
