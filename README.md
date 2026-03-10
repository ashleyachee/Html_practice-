# Html_practice-
Html practice - HR simulation
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>HR Command Center</title>
  <style>
    :root {
      --bg: #f4f7fb;
      --panel: #ffffff;
      --panel-alt: #eef4ff;
      --text: #162033;
      --muted: #4f5d75;
      --border: #cbd5e1;
      --accent: #1d4ed8;
      --accent-dark: #153ea8;
      --success-bg: #eaf8ef;
      --success-text: #14532d;
      --error-bg: #fff1f2;
      --error-text: #9f1239;
      --shadow: 0 12px 28px rgba(15, 23, 42, 0.08);
      --radius: 18px;
      --focus: 0 0 0 4px rgba(29, 78, 216, 0.2);
    }

    * {
      box-sizing: border-box;
    }

    html, body {
      margin: 0;
      padding: 0;
      background: var(--bg);
      color: var(--text);
      font-family: Arial, Helvetica, sans-serif;
      line-height: 1.5;
    }

    button, input, select, textarea {
      font: inherit;
    }

    #hr-command-center {
      width: 100%;
      max-width: 1100px;
      margin: 0 auto;
      padding: 20px;
    }

    .sr-only {
      position: absolute;
      width: 1px;
      height: 1px;
      padding: 0;
      margin: -1px;
      overflow: hidden;
      clip: rect(0, 0, 0, 0);
      white-space: nowrap;
      border: 0;
    }

    .hero {
      background: linear-gradient(135deg, #ffffff 0%, #eef4ff 100%);
      border: 1px solid var(--border);
      border-radius: 24px;
      box-shadow: var(--shadow);
      padding: 24px;
      margin-bottom: 20px;
    }

    .hero-top {
      display: flex;
      justify-content: space-between;
      gap: 16px;
      align-items: flex-start;
      flex-wrap: wrap;
    }

    .eyebrow {
      margin: 0 0 8px;
      font-size: 0.9rem;
      font-weight: 700;
      letter-spacing: 0.04em;
      text-transform: uppercase;
      color: var(--accent);
    }

    .hero h1 {
      margin: 0 0 10px;
      font-size: clamp(1.8rem, 4vw, 2.5rem);
      line-height: 1.15;
    }

    .hero p {
      margin: 0;
      max-width: 65ch;
      color: var(--muted);
      font-size: 1rem;
    }

    .status-chip {
      display: inline-flex;
      align-items: center;
      gap: 8px;
      background: #fff;
      border: 1px solid var(--border);
      border-radius: 999px;
      padding: 10px 14px;
      font-weight: 700;
      color: var(--text);
      white-space: nowrap;
    }

    .layout {
      display: grid;
      grid-template-columns: minmax(280px, 1fr) minmax(320px, 1.2fr);
      gap: 20px;
      align-items: start;
    }

    .panel {
      background: var(--panel);
      border: 1px solid var(--border);
      border-radius: var(--radius);
      box-shadow: var(--shadow);
      padding: 18px;
    }

    .panel h2 {
      margin: 0 0 8px;
      font-size: 1.25rem;
    }

    .panel-intro {
      margin: 0 0 16px;
      color: var(--muted);
      font-size: 0.98rem;
    }

    .dashboard-grid {
      display: grid;
      grid-template-columns: repeat(2, minmax(0, 1fr));
      gap: 12px;
    }

    .dashboard-card {
      position: relative;
      border: 1px solid var(--border);
      border-radius: 16px;
      padding: 14px;
      background: var(--panel-alt);
      min-height: 110px;
      display: flex;
      flex-direction: column;
      justify-content: space-between;
    }

    .dashboard-card h3 {
      margin: 0 0 6px;
      font-size: 1rem;
    }

    .dashboard-card p {
      margin: 0;
      font-size: 0.95rem;
      color: var(--muted);
    }

    .card-icon {
      font-size: 1.4rem;
      display: inline-block;
      margin-bottom: 8px;
    }

    .alert-badge {
      position: absolute;
      top: 10px;
      right: 10px;
      min-width: 28px;
      height: 28px;
      padding: 0 8px;
      border-radius: 999px;
      background: #dc2626;
      color: #fff;
      font-size: 0.9rem;
      font-weight: 700;
      display: inline-flex;
      align-items: center;
      justify-content: center;
      border: 2px solid #fff;
      animation: pulse 1.7s infinite;
    }

    .scenario-stage {
      min-height: 100%;
    }

    .scenario-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      gap: 12px;
      flex-wrap: wrap;
      margin-bottom: 14px;
    }

    .progress {
      font-weight: 700;
      color: var(--accent);
      background: #edf4ff;
      border-radius: 999px;
      padding: 8px 12px;
    }

    .alert-button {
      width: 100%;
      text-align: left;
      border: 1px solid var(--border);
      border-radius: 16px;
      background: linear-gradient(180deg, #ffffff 0%, #f8fbff 100%);
      padding: 18px;
      cursor: pointer;
      transition: transform 0.2s ease, border-color 0.2s ease, box-shadow 0.2s ease;
      margin-bottom: 16px;
    }

    .alert-button:hover,
    .alert-button:focus-visible {
      transform: translateY(-2px);
      border-color: var(--accent);
      box-shadow: var(--focus);
      outline: none;
    }

    .alert-label {
      display: inline-flex;
      align-items: center;
      gap: 8px;
      font-weight: 700;
      color: #b91c1c;
      margin-bottom: 8px;
    }

    .alert-button h3 {
      margin: 0 0 8px;
      font-size: 1.2rem;
      color: var(--text);
    }

    .alert-button p {
      margin: 0;
      color: var(--muted);
    }

    .choice-grid {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 10px;
      margin-top: 14px;
    }

    .role-button,
    .next-button,
    .restart-button {
      border: 1px solid var(--border);
      border-radius: 14px;
      padding: 14px;
      background: #fff;
      color: var(--text);
      cursor: pointer;
      text-align: left;
      transition: border-color 0.2s ease, transform 0.2s ease, background 0.2s ease, box-shadow 0.2s ease;
    }

    .role-button:hover,
    .role-button:focus-visible,
    .next-button:hover,
    .next-button:focus-visible,
    .restart-button:hover,
    .restart-button:focus-visible {
      border-color: var(--accent);
      box-shadow: var(--focus);
      outline: none;
      transform: translateY(-1px);
    }

    .role-button strong {
      display: block;
      margin-bottom: 4px;
      font-size: 1rem;
    }

    .role-button span {
      display: block;
      color: var(--muted);
      font-size: 0.92rem;
    }

    .role-button[disabled] {
      cursor: default;
      opacity: 0.95;
    }

    .role-button.correct-choice {
      background: var(--success-bg);
      border-color: #65a30d;
    }

    .role-button.wrong-choice {
      background: var(--error-bg);
      border-color: #fb7185;
    }

    .feedback-box {
      margin-top: 16px;
      border-radius: 16px;
      padding: 14px 16px;
      border: 1px solid transparent;
    }

    .feedback-box.correct {
      background: var(--success-bg);
      color: var(--success-text);
      border-color: #86efac;
    }

    .feedback-box.incorrect {
      background: var(--error-bg);
      color: var(--error-text);
      border-color: #fda4af;
    }

    .feedback-box p {
      margin: 0;
    }

    .feedback-box p + p {
      margin-top: 8px;
    }

    .button-row {
      display: flex;
      gap: 10px;
      margin-top: 16px;
      flex-wrap: wrap;
    }

    .next-button,
    .restart-button {
      text-align: center;
      font-weight: 700;
      min-width: 160px;
    }

    .top-reset-button {
      min-width: 150px;
      background: #ffffff;
    }

    .next-button {
      background: var(--accent);
      color: #fff;
      border-color: var(--accent);
    }

    .next-button:hover,
    .next-button:focus-visible {
      background: var(--accent-dark);
      border-color: var(--accent-dark);
    }

    .summary-grid {
      display: grid;
      grid-template-columns: repeat(2, minmax(0, 1fr));
      gap: 12px;
      margin-top: 16px;
    }

    .summary-card {
      border: 1px solid var(--border);
      border-radius: 16px;
      padding: 14px;
      background: #fff;
    }

    .summary-card h3 {
      margin: 0 0 6px;
      font-size: 1rem;
    }

    .summary-card p {
      margin: 0;
      color: var(--muted);
    }

    .score-box {
      background: linear-gradient(135deg, #eff6ff, #ffffff);
      border: 1px solid var(--border);
      border-radius: 18px;
      padding: 18px;
      margin: 10px 0 8px;
    }

    .score-box strong {
      display: block;
      font-size: 1.6rem;
      margin-bottom: 4px;
      color: var(--accent);
    }

    .footer-note {
      margin-top: 14px;
      color: var(--muted);
    }

    [hidden] {
      display: none !important;
    }

    :focus-visible {
      outline: none;
      box-shadow: var(--focus);
    }

    @keyframes pulse {
      0% { transform: scale(1); }
      50% { transform: scale(1.08); }
      100% { transform: scale(1); }
    }

    @media (max-width: 860px) {
      .layout {
        grid-template-columns: 1fr;
      }
    }

    @media (max-width: 640px) {
      #hr-command-center {
        padding: 14px;
      }

      .hero,
      .panel {
        padding: 16px;
      }

      .dashboard-grid,
      .choice-grid,
      .summary-grid {
        grid-template-columns: 1fr;
      }

      .status-chip,
      .progress {
        width: 100%;
        justify-content: center;
      }
    }

    @media (prefers-reduced-motion: reduce) {
      *, *::before, *::after {
        animation: none !important;
        transition: none !important;
        scroll-behavior: auto !important;
      }
    }
  </style>
</head>
<body>
  <div id="hr-command-center">
    <section class="hero" aria-labelledby="activity-title">
      <div class="hero-top">
        <div>
          <p class="eyebrow">Interactive HR Learning Activity</p>
          <h1 id="activity-title">HR Command Center</h1>
          <p>
            Welcome to the HR dashboard for BrightPath Co. Watch for alerts, open each situation,
            and decide which HR role should respond first.
          </p>
        </div>
        <div style="display:flex; gap:10px; flex-wrap:wrap; align-items:center;">
        <div class="status-chip" aria-label="System status">
          <span aria-hidden="true">🟢</span>
          <span>Dashboard Online</span>
        </div>
        <button type="button" class="restart-button top-reset-button" id="top-reset-button">Reset Activity</button>
      </div>
      </div>
    </section>

    <main class="layout">
      <section class="panel" aria-labelledby="dashboard-title">
        <h2 id="dashboard-title">Company Dashboard</h2>
        <p class="panel-intro">
          These panels show the areas HR watches every day. A red alert means a new situation needs attention.
        </p>

        <div class="dashboard-grid" aria-label="Dashboard areas">
          <article class="dashboard-card">
            <div>
              <span class="card-icon" aria-hidden="true">🧑‍💼</span>
              <h3>Hiring</h3>
              <p>Planning jobs, pay, and future staffing.</p>
            </div>
            <span class="alert-badge" id="badge-hiring" aria-label="Hiring alerts">0</span>
          </article>

          <article class="dashboard-card">
            <div>
              <span class="card-icon" aria-hidden="true">💬</span>
              <h3>Employee Feedback</h3>
              <p>Listening to concerns and support needs.</p>
            </div>
            <span class="alert-badge" id="badge-feedback" aria-label="Employee feedback alerts">0</span>
          </article>

          <article class="dashboard-card">
            <div>
              <span class="card-icon" aria-hidden="true">📘</span>
              <h3>Training</h3>
              <p>Helping people learn and grow at work.</p>
            </div>
            <span class="alert-badge" id="badge-training" aria-label="Training alerts">0</span>
          </article>

          <article class="dashboard-card">
            <div>
              <span class="card-icon" aria-hidden="true">📋</span>
              <h3>Policies</h3>
              <p>Keeping rules and processes clear and fair.</p>
            </div>
            <span class="alert-badge" id="badge-policies" aria-label="Policy alerts">0</span>
          </article>

          <article class="dashboard-card">
            <div>
              <span class="card-icon" aria-hidden="true">📈</span>
              <h3>Team Performance</h3>
              <p>Helping teams succeed and stay on track.</p>
            </div>
            <span class="alert-badge" id="badge-performance" aria-label="Performance alerts">0</span>
          </article>

          <article class="dashboard-card">
            <div>
              <span class="card-icon" aria-hidden="true">⚖️</span>
              <h3>Workplace Fairness</h3>
              <p>Making sure people are treated with care and respect.</p>
            </div>
            <span class="alert-badge" id="badge-fairness" aria-label="Fairness alerts">0</span>
          </article>
        </div>
      </section>

      <section class="panel scenario-stage" aria-labelledby="response-title">
        <div id="game-screen">
          <div class="scenario-header">
            <h2 id="response-title">Respond to Alerts</h2>
            <div class="progress" id="progress-text">Alert 1 of 6</div>
          </div>

          <button type="button" class="alert-button" id="alert-card" aria-describedby="alert-description">
            <span class="alert-label"><span aria-hidden="true">🚨</span> New Alert</span>
            <h3 id="alert-title"></h3>
            <p id="alert-description"></p>
          </button>

          <div id="choices" class="choice-grid" aria-label="Choose the HR role that should respond first"></div>

          <div id="feedback" class="feedback-box" hidden>
            <p id="feedback-message"></p>
            <p id="feedback-support"></p>
          </div>

          <div class="button-row">
            <button type="button" class="next-button" id="next-button" hidden>Next Alert</button>
            <button type="button" class="restart-button" id="restart-button" hidden>Start Again</button>
          </div>
        </div>

        <div id="final-screen" hidden tabindex="-1">
          <h2>Command Center Summary</h2>
          <p class="panel-intro">
            You finished all the alerts. Here is your score and a quick review of the four HR roles.
          </p>

          <div class="score-box">
            <strong id="final-score">0 out of 6</strong>
            <span id="final-message">Nice work!</span>
          </div>

          <div class="summary-grid" aria-label="Summary of HR roles">
            <article class="summary-card">
              <h3>🧭 Strategic Partner</h3>
              <p>Helps the organization plan ahead and make sure the right people are in the right jobs.</p>
            </article>

            <article class="summary-card">
              <h3>🤝 Employee Champion</h3>
              <p>Helps employees feel supported, treated fairly, and ready to do their best work.</p>
            </article>

            <article class="summary-card">
              <h3>🔄 Change Agent</h3>
              <p>Helps people learn new skills and adjust when the workplace changes.</p>
            </article>

            <article class="summary-card">
              <h3>🗂️ Administrative Expert</h3>
              <p>Makes sure HR rules, forms, and processes are clear, fair, and followed correctly.</p>
            </article>
          </div>

          <p class="footer-note">
            All four roles matter. In real workplaces, HR often works together across these roles to solve problems.
          </p>

          <div class="button-row">
            <button type="button" class="restart-button" id="restart-button-final">Try the Alerts Again</button>
          </div>
        </div>

        <div class="sr-only" aria-live="polite" id="live-region"></div>
      </section>
    </main>
  </div>

  <script>
    /*
      HR Command Center
      -----------------
      Edit the scenarios below to change the activity content.
      Each object includes a title, short description, correct role,
      and brief feedback for correct and incorrect answers.
    */
    const scenarios = [
      {
        panel: "hiring",
        title: "Big Hiring Plan",
        description: "The company expects to grow next year and may need many new employees. HR needs to think ahead about hiring needs.",
        correctRole: "Strategic Partner",
        supportRole: "Administrative Expert",
        feedbackCorrect: "Strategic Partner is the best choice because this alert is about planning for future hiring.",
        feedbackIncorrect: "This role helps in other ways, but this alert is mainly about planning ahead for the organization."
      },
      {
        panel: "feedback",
        title: "Employees Feel Stressed",
        description: "Several employees say they feel overwhelmed and unsupported. They want someone to listen and help improve their work experience.",
        correctRole: "Employee Champion",
        supportRole: "Change Agent",
        feedbackCorrect: "Employee Champion is the best choice because this role focuses on support, fairness, and employee well-being.",
        feedbackIncorrect: "This role matters too, but this alert starts with listening to employees and helping them feel supported."
      },
      {
        panel: "training",
        title: "New Software Rollout",
        description: "The company is using a new software system next month. Employees need help learning how to use it.",
        correctRole: "Change Agent",
        supportRole: "Employee Champion",
        feedbackCorrect: "Change Agent is the best choice because this role helps people learn and adjust when work changes.",
        feedbackIncorrect: "This role can still help, but the main need here is helping people adapt to a new way of working."
      },
      {
        panel: "policies",
        title: "Hiring Rules Are Being Missed",
        description: "Some managers are skipping parts of the hiring process. HR needs to make sure the process is followed the same way every time.",
        correctRole: "Administrative Expert",
        supportRole: "Strategic Partner",
        feedbackCorrect: "Administrative Expert is the best choice because this role keeps HR processes clear, fair, and consistent.",
        feedbackIncorrect: "This role helps in other situations, but this alert is mostly about following rules and using the process correctly."
      },
      {
        panel: "fairness",
        title: "Pay May Not Be Competitive",
        description: "Employees say pay may be lower than what other companies offer. HR needs to review whether pay still helps the company attract and keep people.",
        correctRole: "Strategic Partner",
        supportRole: "Employee Champion",
        feedbackCorrect: "Strategic Partner is the best choice because pay planning connects to long-term staffing and business goals.",
        feedbackIncorrect: "This role may help later, but the first step is reviewing pay as part of the organization's future planning."
      },
      {
        panel: "performance",
        title: "Team Expectations Are Unclear",
        description: "One team is missing goals because workers are confused about what success looks like. HR needs to help improve support and performance expectations.",
        correctRole: "Employee Champion",
        supportRole: "Administrative Expert",
        feedbackCorrect: "Employee Champion is the best choice because the team needs support so people can do their best work.",
        feedbackIncorrect: "Another HR role may support this, but this alert starts with helping employees succeed and feel guided."
      }
    ];

    const roleDetails = {
      "Strategic Partner": "Plans ahead for future workforce needs.",
      "Employee Champion": "Supports employees and fairness at work.",
      "Change Agent": "Helps people adapt and learn during change.",
      "Administrative Expert": "Keeps HR rules and processes clear and consistent."
    };

    const state = {
      currentIndex: 0,
      score: 0,
      answered: false
    };

    function initHRCommandCenter() {
      cacheElements();
      bindEvents();
      resetActivity();
    }

    let elements = {};

    function cacheElements() {
      elements.progressText = document.getElementById("progress-text");
      elements.alertCard = document.getElementById("alert-card");
      elements.alertTitle = document.getElementById("alert-title");
      elements.alertDescription = document.getElementById("alert-description");
      elements.choices = document.getElementById("choices");
      elements.feedback = document.getElementById("feedback");
      elements.feedbackMessage = document.getElementById("feedback-message");
      elements.feedbackSupport = document.getElementById("feedback-support");
      elements.nextButton = document.getElementById("next-button");
      elements.restartButton = document.getElementById("restart-button");
      elements.restartButtonFinal = document.getElementById("restart-button-final");
      elements.topResetButton = document.getElementById("top-reset-button");
      elements.gameScreen = document.getElementById("game-screen");
      elements.finalScreen = document.getElementById("final-screen");
      elements.finalScore = document.getElementById("final-score");
      elements.finalMessage = document.getElementById("final-message");
      elements.liveRegion = document.getElementById("live-region");

      elements.badges = {
        hiring: document.getElementById("badge-hiring"),
        feedback: document.getElementById("badge-feedback"),
        training: document.getElementById("badge-training"),
        policies: document.getElementById("badge-policies"),
        performance: document.getElementById("badge-performance"),
        fairness: document.getElementById("badge-fairness")
      };
    }

    function bindEvents() {
      elements.nextButton.addEventListener("click", goToNextScenario);
      elements.restartButton.addEventListener("click", resetActivity);
      elements.restartButtonFinal.addEventListener("click", resetActivity);
      elements.topResetButton.addEventListener("click", resetActivity);
      elements.alertCard.addEventListener("click", function () {
        const firstChoice = elements.choices.querySelector("button:not([disabled])") || elements.choices.querySelector("button");
        if (firstChoice) {
          firstChoice.focus();
        }
      });
    }

    function resetActivity() {
      state.currentIndex = 0;
      state.score = 0;
      state.answered = false;

      elements.gameScreen.hidden = false;
      elements.finalScreen.hidden = true;
      elements.restartButton.hidden = true;
      elements.nextButton.hidden = true;
      elements.feedback.hidden = true;

      updateBadges();
      renderScenario();
      announce("HR Command Center restarted. Alert 1 is ready.");
    }

    function updateBadges() {
      const remainingCounts = {
        hiring: 0,
        feedback: 0,
        training: 0,
        policies: 0,
        performance: 0,
        fairness: 0
      };

      for (let i = state.currentIndex; i < scenarios.length; i += 1) {
        remainingCounts[scenarios[i].panel] += 1;
      }

      Object.keys(elements.badges).forEach(function (key) {
        const badge = elements.badges[key];
        badge.textContent = remainingCounts[key];
        badge.setAttribute("aria-label", key + " alerts: " + remainingCounts[key]);
        badge.hidden = remainingCounts[key] === 0;
      });
    }

    function renderScenario() {
      const scenario = scenarios[state.currentIndex];
      state.answered = false;

      elements.progressText.textContent = "Alert " + (state.currentIndex + 1) + " of " + scenarios.length;
      elements.alertTitle.textContent = scenario.title;
      elements.alertDescription.textContent = scenario.description;
      elements.feedback.hidden = true;
      elements.nextButton.hidden = true;
      elements.restartButton.hidden = true;
      elements.choices.innerHTML = "";

      Object.keys(roleDetails).forEach(function (roleName) {
        const button = document.createElement("button");
        button.type = "button";
        button.className = "role-button";
        button.setAttribute("data-role", roleName);
        button.innerHTML = "<strong>" + roleName + "</strong><span>" + roleDetails[roleName] + "</span>";
        button.addEventListener("click", function () {
          handleChoice(roleName, button);
        });
        elements.choices.appendChild(button);
      });
    }

    function handleChoice(selectedRole, selectedButton) {
      if (state.answered) {
        return;
      }

      state.answered = true;
      const scenario = scenarios[state.currentIndex];
      const isCorrect = selectedRole === scenario.correctRole;
      const allButtons = elements.choices.querySelectorAll("button");

      allButtons.forEach(function (button) {
        button.disabled = true;
        const role = button.getAttribute("data-role");

        if (role === scenario.correctRole) {
          button.classList.add("correct-choice");
        }

        if (button === selectedButton && !isCorrect) {
          button.classList.add("wrong-choice");
        }
      });

      if (isCorrect) {
        state.score += 1;
      }

      elements.feedback.className = "feedback-box " + (isCorrect ? "correct" : "incorrect");
      elements.feedbackMessage.textContent = isCorrect ? scenario.feedbackCorrect : scenario.feedbackIncorrect;
      elements.feedbackSupport.textContent = "Support role: " + scenario.supportRole + " may also help with this situation.";
      elements.feedback.hidden = false;

      if (state.currentIndex === scenarios.length - 1) {
        elements.restartButton.hidden = true;
        elements.nextButton.textContent = "See Summary";
      } else {
        elements.nextButton.textContent = "Next Alert";
      }

      elements.nextButton.hidden = false;
      announce((isCorrect ? "Correct. " : "Not quite. ") + elements.feedbackMessage.textContent + " " + elements.feedbackSupport.textContent);
      elements.nextButton.focus();
    }

    function goToNextScenario() {
      state.currentIndex += 1;
      updateBadges();

      if (state.currentIndex >= scenarios.length) {
        showFinalScreen();
        return;
      }

      renderScenario();
      announce("Now viewing alert " + (state.currentIndex + 1) + " of " + scenarios.length + ".");
    }

    function showFinalScreen() {
      elements.gameScreen.hidden = true;
      elements.finalScreen.hidden = false;
      elements.finalScore.textContent = state.score + " out of " + scenarios.length;
      elements.finalMessage.textContent = getFinalMessage();
      elements.finalScreen.focus();
      announce("Activity complete. You scored " + state.score + " out of " + scenarios.length + ".");
    }

    function getFinalMessage() {
      if (state.score === scenarios.length) {
        return "Excellent work. You matched every alert to the right HR role.";
      }
      if (state.score >= 4) {
        return "Nice job. You are building a strong understanding of the different HR roles.";
      }
      return "Good start. Review the role summaries below to strengthen your understanding of HR work.";
    }

    function announce(message) {
      elements.liveRegion.textContent = "";
      window.setTimeout(function () {
        elements.liveRegion.textContent = message;
      }, 30);
    }

    document.addEventListener("DOMContentLoaded", initHRCommandCenter);
  </script>
</body>
</html>
