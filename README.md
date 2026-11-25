<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Student Portal — Clara Santos</title>
  <style>
    :root {
      --bg: #f4f6fb;
      --surface: #ffffff;
      --surface-alt: #eef2f9;
      --text: #161d2d;
      --muted: #5c687d;
      --primary: #3b5bdb;
      --primary-soft: #e7ecff;
      --accent: #0ca678;
      --accent-soft: #e6fcf5;
      --warn: #e67700;
      --warn-soft: #fff9db;
      --border: #e1e6f0;
      --radius: 14px;
      --shadow: 0 6px 24px rgba(22, 29, 45, 0.05);
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    body {
      font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Inter, sans-serif;
      background: var(--bg);
      color: var(--text);
      line-height: 1.5;
      min-height: 100vh;
    }

    .app {
      display: grid;
      grid-template-columns: 240px 1fr;
      min-height: 100vh;
    }

    /* Sidebar */
    aside {
      background: var(--surface);
      border-right: 1px solid var(--border);
      padding: 24px 16px;
      display: flex;
      flex-direction: column;
      gap: 28px;
    }

    .brand {
      display: flex;
      align-items: center;
      gap: 10px;
      padding: 0 10px;
      font-weight: 700;
      font-size: 1.05rem;
      letter-spacing: -0.01em;
    }

    .brand-badge {
      width: 34px;
      height: 34px;
      border-radius: 10px;
      background: linear-gradient(135deg, var(--primary), #6c5ce7);
      color: #fff;
      display: grid;
      place-items: center;
      font-size: 0.95rem;
    }

    nav {
      display: flex;
      flex-direction: column;
      gap: 6px;
    }

    .nav-btn {
      width: 100%;
      border: none;
      background: transparent;
      color: var(--muted);
      font-size: 0.94rem;
      font-weight: 500;
      padding: 10px 14px;
      border-radius: 10px;
      cursor: pointer;
      display: flex;
      align-items: center;
      gap: 10px;
      text-align: left;
      transition: background 0.15s, color 0.15s;
    }

    .nav-btn:hover {
      background: var(--surface-alt);
      color: var(--text);
    }

    .nav-btn.active {
      background: var(--primary-soft);
      color: var(--primary);
      font-weight: 600;
    }

    .sidebar-footer {
      margin-top: auto;
      padding: 14px;
      border-radius: 12px;
      background: var(--surface-alt);
      font-size: 0.8rem;
      color: var(--muted);
    }

    /* Main Content */
    main {
      padding: 28px 32px;
      max-width: 1200px;
      width: 100%;
      margin: 0 auto;
    }

    header.top-bar {
      display: flex;
      flex-wrap: wrap;
      justify-content: space-between;
      align-items: center;
      gap: 16px;
      margin-bottom: 26px;
    }

    header.top-bar h1 {
      font-size: 1.55rem;
      letter-spacing: -0.02em;
    }

    header.top-bar p {
      color: var(--muted);
      font-size: 0.9rem;
    }

    .student-pill {
      display: flex;
      align-items: center;
      gap: 10px;
      background: var(--surface);
      border: 1px solid var(--border);
      padding: 8px 14px;
      border-radius: 999px;
      font-size: 0.88rem;
      box-shadow: var(--shadow);
    }

    .avatar {
      width: 30px;
      height: 30px;
      border-radius: 50%;
      background: var(--primary);
      color: #fff;
      display: grid;
      place-items: center;
      font-weight: 700;
      font-size: 0.8rem;
    }

    .section {
      display: none;
      animation: fadeIn 0.2s ease;
    }

    .section.active {
      display: block;
    }

    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(4px); }
      to { opacity: 1; transform: translateY(0); }
    }

    /* KPI Grid */
    .kpi-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
      gap: 16px;
      margin-bottom: 24px;
    }

    .card {
      background: var(--surface);
      border: 1px solid var(--border);
      border-radius: var(--radius);
      padding: 20px;
      box-shadow: var(--shadow);
    }

    .kpi-label {
      font-size: 0.82rem;
      color: var(--muted);
      margin-bottom: 6px;
    }

    .kpi-value {
      font-size: 1.65rem;
      font-weight: 700;
      letter-spacing: -0.02em;
    }

    .kpi-meta {
      margin-top: 8px;
      font-size: 0.78rem;
      color: var(--accent);
      font-weight: 500;
    }

    .two-col {
      display: grid;
      grid-template-columns: 1.3fr 1fr;
      gap: 20px;
    }

    .card-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 14px;
    }

    .card-title {
      font-size: 1.02rem;
      font-weight: 650;
    }

    .list-item {
      padding: 12px 0;
      border-bottom: 1px solid var(--border);
      display: flex;
      justify-content: space-between;
      align-items: flex-start;
      gap: 12px;
    }

    .list-item:last-child {
      border-bottom: none;
      padding-bottom: 0;
    }

    .badge {
      font-size: 0.75rem;
      font-weight: 600;
      padding: 4px 10px;
      border-radius: 999px;
      white-space: nowrap;
    }

    .badge-blue { background: var(--primary-soft); color: var(--primary); }
    .badge-green { background: var(--accent-soft); color: var(--accent); }
    .badge-amber { background: var(--warn-soft); color: var(--warn); }

    /* Schedule & Grades Tables */
    .filter-row {
      display: flex;
      flex-wrap: wrap;
      gap: 8px;
      margin-bottom: 16px;
    }

    .chip {
      border: 1px solid var(--border);
      background: var(--surface);
      color: var(--muted);
      padding: 6px 13px;
      border-radius: 999px;
      font-size: 0.84rem;
      cursor: pointer;
      transition: all 0.15s;
    }

    .chip.active {
      background: var(--primary);
      border-color: var(--primary);
      color: #fff;
      font-weight: 500;
    }

    table {
      width: 100%;
      border-collapse: collapse;
      font-size: 0.9rem;
    }

    th, td {
      text-align: left;
      padding: 12px 14px;
      border-bottom: 1px solid var(--border);
    }

    th {
      color: var(--muted);
      font-size: 0.78rem;
      text-transform: uppercase;
      letter-spacing: 0.04em;
      background: var(--surface-alt);
    }

    .progress-bar {
      width: 100%;
      height: 8px;
      background: var(--surface-alt);
      border-radius: 999px;
      overflow: hidden;
      margin-top: 6px;
    }

    .progress-fill {
      height: 100%;
      background: var(--primary);
      border-radius: 999px;
    }

    /* Profile */
    .profile-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
      gap: 16px;
      margin-top: 14px;
    }

    .info-box {
      background: var(--surface-alt);
      padding: 14px 16px;
      border-radius: 10px;
    }

    .info-label {
      font-size: 0.76rem;
      color: var(--muted);
      text-transform: uppercase;
      letter-spacing: 0.04em;
    }

    .info-val {
      font-weight: 600;
      margin-top: 3px;
      font-size: 0.95rem;
    }

    @media (max-width: 860px) {
      .app {
        grid-template-columns: 1fr;
      }
      aside {
        border-right: none;
        border-bottom: 1px solid var(--border);
        padding: 16px;
        gap: 14px;
      }
      nav {
        flex-direction: row;
        overflow-x: auto;
        padding-bottom: 4px;
      }
      .nav-btn {
        width: auto;
        white-space: nowrap;
      }
      .sidebar-footer {
        display: none;
      }
      main {
        padding: 20px 16px;
      }
      .two-col {
        grid-template-columns: 1fr;
      }
      .table-wrap {
        overflow-x: auto;
      }
    }
  </style>
</head>
<body>
  <div class="app">
    <aside>
      <div class="brand">
        <div class="brand-badge">SP</div>
        <span>Northbridge U</span>
      </div>
      <nav id="nav">
        <button class="nav-btn active" data-tab="dashboard">Dashboard</button>
        <button class="nav-btn" data-tab="schedule">Class Schedule</button>
        <button class="nav-btn" data-tab="grades">Grades</button>
        <button class="nav-btn" data-tab="announcements">Announcements</button>
        <button class="nav-btn" data-tab="profile">Student Profile</button>
      </nav>
      <div class="sidebar-footer">
        Academic Term: Fall 2026<br />
        Static Client-Side Demo
      </div>
    </aside>

    <main>
      <header class="top-bar">
        <div>
          <h1 id="page-title">Dashboard</h1>
          <p id="page-subtitle">Welcome back, Clara Santos — BS Information Systems (Year 3)</p>
        </div>
        <div class="student-pill">
          <div class="avatar">CS</div>
          <span>ID: 2024-08419</span>
        </div>
      </header>

      <!-- DASHBOARD -->
      <section id="dashboard" class="section active">
        <div class="kpi-grid">
          <div class="card">
            <div class="kpi-label">Cumulative GPA</div>
            <div class="kpi-value">3.78</div>
            <div class="kpi-meta">+0.06 from Spring term</div>
          </div>
          <div class="card">
            <div class="kpi-label">Enrolled Credits</div>
            <div class="kpi-value">18</div>
            <div class="kpi-meta">5 active courses</div>
          </div>
          <div class="card">
            <div class="kpi-label">Attendance Rate</div>
            <div class="kpi-value">96%</div>
            <div class="kpi-meta">On track for honors</div>
          </div>
          <div class="card">
            <div class="kpi-label">Upcoming Tasks</div>
            <div class="kpi-value">3</div>
            <div class="kpi-meta">Due within 7 days</div>
          </div>
        </div>

        <div class="two-col">
          <div class="card">
            <div class="card-header">
              <h2 class="card-title">Today's Classes</h2>
              <span class="badge badge-blue">Fall 2026</span>
            </div>
            <div id="dash-schedule"></div>
          </div>

          <div class="card">
            <div class="card-header">
              <h2 class="card-title">Recent Announcements</h2>
              <span class="badge badge-amber">Updates</span>
            </div>
            <div id="dash-announcements"></div>
          </div>
        </div>
      </section>

      <!-- SCHEDULE -->
      <section id="schedule" class="section">
        <div class="card">
          <div class="card-header">
            <h2 class="card-title">Weekly Class Schedule</h2>
          </div>
          <div class="filter-row" id="day-filters">
            <button class="chip active" data-day="All">All Days</button>
            <button class="chip" data-day="Mon">Mon</button>
            <button class="chip" data-day="Tue">Tue</button>
            <button class="chip" data-day="Wed">Wed</button>
            <button class="chip" data-day="Thu">Thu</button>
            <button class="chip" data-day="Fri">Fri</button>
          </div>
          <div class="table-wrap">
            <table>
              <thead>
                <tr>
                  <th>Course</th>
                  <th>Days</th>
                  <th>Time</th>
                  <th>Room</th>
                  <th>Instructor</th>
                </tr>
              </thead>
              <tbody id="schedule-body"></tbody>
            </table>
          </div>
        </div>
      </section>

      <!-- GRADES -->
      <section id="grades" class="section">
        <div class="card">
          <div class="card-header">
            <h2 class="card-title">Course Grades & Standing</h2>
            <span class="badge badge-green">Term GPA: 3.82</span>
          </div>
          <div class="table-wrap">
            <table>
              <thead>
                <tr>
                  <th>Course Code</th>
                  <th>Subject</th>
                  <th>Units</th>
                  <th>Score</th>
                  <th>Grade</th>
                </tr>
              </thead>
              <tbody id="grades-body"></tbody>
            </table>
          </div>
        </div>
      </section>

      <!-- ANNOUNCEMENTS -->
      <section id="announcements" class="section">
        <div class="card">
          <div class="card-header">
            <h2 class="card-title">Campus & Course Announcements</h2>
          </div>
          <div id="announcements-list"></div>
        </div>
      </section>

      <!-- PROFILE -->
      <section id="profile" class="section">
        <div class="card">
          <div class="card-header">
            <h2 class="card-title">Student Profile</h2>
            <span class="badge badge-green">Active Enrollment</span>
          </div>
          <p style="color: var(--muted); font-size: 0.92rem;">
            Fictional student record generated for human-computer interaction observation.
          </p>
          <div class="profile-grid">
            <div class="info-box">
              <div class="info-label">Full Name</div>
              <div class="info-val">Clara Mae Santos</div>
            </div>
            <div class="info-box">
              <div class="info-label">Student Number</div>
              <div class="info-val">2024-08419</div>
            </div>
            <div class="info-box">
              <div class="info-label">Program & Year</div>
              <div class="info-val">BS Information Systems — 3rd Year</div>
            </div>
            <div class="info-box">
              <div class="info-label">Academic Advisor</div>
              <div class="info-val">Dr. Mateo Alvarez</div>
            </div>
            <div class="info-box">
              <div class="info-label">University Email</div>
              <div class="info-val">clara.santos@northbridge.edu</div>
            </div>
            <div class="info-box">
              <div class="info-label">Expected Graduation</div>
              <div class="info-val">June 2028</div>
            </div>
          </div>
        </div>
      </section>
    </main>
  </div>

  <script>
    const scheduleData = [
      { code: "HCI 301", name: "Human-Computer Interaction", days: ["Mon", "Wed"], time: "09:00 – 10:30 AM", room: "Tech Hall 204", prof: "Prof. Elena Reyes" },
      { code: "DBM 305", name: "Database Management Systems", days: ["Mon", "Wed"], time: "01:00 – 02:30 PM", room: "Lab B-12", prof: "Dr. Arthur Lim" },
      { code: "WEB 302", name: "Web Systems & Technologies", days: ["Tue", "Thu"], time: "10:00 – 11:30 AM", room: "Lab A-05", prof: "Prof. Hannah Cruz" },
      { code: "SAD 310", name: "Systems Analysis & Design", days: ["Tue", "Thu"], time: "02:00 – 03:30 PM", room: "Room 309", prof: "Prof. David Tan" },
      { code: "ETH 204", name: "Computing Ethics & Society", days: ["Fri"], time: "09:30 – 12:00 PM", room: "Auditorium C", prof: "Dr. Sofia Mendoza" }
    ];

    const gradesData = [
      { code: "HCI 301", name: "Human-Computer Interaction", units: 3, score: 94, grade: "A" },
      { code: "DBM 305", name: "Database Management Systems", units: 4, score: 89, grade: "B+" },
      { code: "WEB 302", name: "Web Systems & Technologies", units: 3, score: 96, grade: "A" },
      { code: "SAD 310", name: "Systems Analysis & Design", units: 3, score: 91, grade: "A-" },
      { code: "ETH 204", name: "Computing Ethics & Society", units: 3, score: 92, grade: "A-" }
    ];

    const announcementsData = [
      { title: "HCI Usability Walkthrough Schedule Posted", date: "Nov 23, 2026", tag: "Course", body: "Group peer-review slots for interface critiques are now open in Tech Hall 204." },
      { title: "Library Extended Hours During Finals Prep", date: "Nov 20, 2026", tag: "Campus", body: "The main learning commons will remain open until 10:00 PM on weekdays starting next week." },
      { title: "Spring 2027 Pre-Advising Reminder", date: "Nov 18, 2026", tag: "Registrar", body: "Confirm your elective plan with your department advisor before December 11." }
    ];

    const tabMeta = {
      dashboard: { title: "Dashboard", subtitle: "Welcome back, Clara Santos — BS Information Systems (Year 3)" },
      schedule: { title: "Class Schedule", subtitle: "Filter your weekly timetable by day" },
      grades: { title: "Grades", subtitle: "Current term performance across enrolled courses" },
      announcements: { title: "Announcements", subtitle: "Latest notices from faculty and administration" },
      profile: { title: "Student Profile", subtitle: "Academic details and enrollment status" }
    };

    // Navigation switching
    const navButtons = document.querySelectorAll(".nav-btn");
    const sections = document.querySelectorAll(".section");
    const pageTitle = document.getElementById("page-title");
    const pageSubtitle = document.getElementById("page-subtitle");

    navButtons.forEach((btn) => {
      btn.addEventListener("click", () => {
        const target = btn.dataset.tab;
        navButtons.forEach((b) => b.classList.remove("active"));
        btn.classList.add("active");

        sections.forEach((sec) => {
          sec.classList.toggle("active", sec.id === target);
        });

        pageTitle.textContent = tabMeta[target].title;
        pageSubtitle.textContent = tabMeta[target].subtitle;
      });
    });

    // Populate Dashboard widgets
    const dashSchedule = document.getElementById("dash-schedule");
    scheduleData.slice(0, 3).forEach((item) => {
      const div = document.createElement("div");
      div.className = "list-item";
      div.innerHTML = `
        <div>
          <strong>${item.code} — ${item.name}</strong>
          <div style="font-size:0.84rem; color:var(--muted);">${item.time} · ${item.room}</div>
        </div>
        <span class="badge badge-blue">${item.days.join("/")}</span>
      `;
      dashSchedule.appendChild(div);
    });

    const dashAnnouncements = document.getElementById("dash-announcements");
    announcementsData.forEach((a) => {
      const div = document.createElement("div");
      div.className = "list-item";
      div.innerHTML = `
        <div>
          <strong>${a.title}</strong>
          <div style="font-size:0.82rem; color:var(--muted);">${a.date}</div>
        </div>
        <span class="badge badge-amber">${a.tag}</span>
      `;
      dashAnnouncements.appendChild(div);
    });

    // Schedule table & day filter
    const scheduleBody = document.getElementById("schedule-body");
    function renderSchedule(day) {
      scheduleBody.innerHTML = "";
      const filtered = day === "All"
        ? scheduleData
        : scheduleData.filter((row) => row.days.includes(day));

      filtered.forEach((row) => {
        const tr = document.createElement("tr");
        tr.innerHTML = `
          <td><strong>${row.code}</strong> — ${row.name}</td>
          <td>${row.days.join(", ")}</td>
          <td>${row.time}</td>
          <td>${row.room}</td>
          <td>${row.prof}</td>
        `;
        scheduleBody.appendChild(tr);
      });
    }
    renderSchedule("All");

    document.querySelectorAll("#day-filters .chip").forEach((chip) => {
      chip.addEventListener("click", () => {
        document.querySelectorAll("#day-filters .chip").forEach((c) => c.classList.remove("active"));
        chip.classList.add("active");
        renderSchedule(chip.dataset.day);
      });
    });

    // Grades table
    const gradesBody = document.getElementById("grades-body");
    gradesData.forEach((g) => {
      const tr = document.createElement("tr");
      tr.innerHTML = `
        <td><strong>${g.code}</strong></td>
        <td>${g.name}</td>
        <td>${g.units}</td>
        <td>
          <div>${g.score}%</div>
          <div class="progress-bar"><div class="progress-fill" style="width:${g.score}%"></div></div>
        </td>
        <td><span class="badge badge-green">${g.grade}</span></td>
      `;
      gradesBody.appendChild(tr);
    });

    // Announcements list
    const annList = document.getElementById("announcements-list");
    announcementsData.forEach((a) => {
      const div = document.createElement("div");
      div.className = "list-item";
      div.innerHTML = `
        <div>
          <strong>${a.title}</strong>
          <p style="font-size:0.88rem; color:var(--muted); margin-top:4px;">${a.body}</p>
          <div style="font-size:0.78rem; color:var(--muted); margin-top:6px;">Posted ${a.date}</div>
        </div>
        <span class="badge badge-blue">${a.tag}</span>
      `;
      annList.appendChild(div);
    });
  </script>
</body>
</html>
