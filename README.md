<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>F.6 English Grammar Academy</title>
  <style>
    :root {
      --primary: #2563eb;
      --primary-dark: #1d4ed8;
      --secondary: #0ea5e9;
      --success: #16a34a;
      --danger: #dc2626;
      --bg: #f8fafc;
      --card-bg: #ffffff;
      --text: #1e293b;
      --text-muted: #64748b;
      --border: #cbd5e1;
      --shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1);
    }
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      font-family: 'Segoe UI', system-ui, -apple-system, sans-serif;
    }
    body {
      background-color: var(--bg);
      color: var(--text);
      line-height: 1.5;
      min-height: 100vh;
      display: flex;
      flex-direction: column;
    }
    header {
      background: linear-gradient(135deg, #1e3a8a, #3b82f6);
      color: white;
      padding: 1rem 1.5rem;
      display: flex;
      justify-content: space-between;
      align-items: center;
      box-shadow: var(--shadow);
    }
    header h1 {
      font-size: 1.3rem;
      font-weight: 700;
    }
    .header-actions {
      display: flex;
      gap: 0.5rem;
      align-items: center;
    }
    button {
      cursor: pointer;
      border: none;
      border-radius: 8px;
      padding: 0.55rem 1.1rem;
      font-weight: 600;
      font-size: 0.9rem;
      transition: all 0.2s ease;
    }
    .btn-primary { background-color: var(--primary); color: white; }
    .btn-primary:hover { background-color: var(--primary-dark); }
    .btn-secondary { background-color: #e2e8f0; color: var(--text); }
    .btn-secondary:hover { background-color: #cbd5e1; }
    .btn-danger { background-color: var(--danger); color: white; }
    .btn-teacher { background-color: #475569; color: #f8fafc; font-size: 0.8rem; }
    main {
      flex: 1;
      max-width: 950px;
      width: 100%;
      margin: 1.5rem auto;
      padding: 0 1rem;
    }
    .view-panel { display: none; }
    .view-panel.active { display: block !important; }
    .card {
      background: var(--card-bg);
      border-radius: 12px;
      border: 1px solid var(--border);
      padding: 1.5rem;
      box-shadow: var(--shadow);
      margin-bottom: 1.5rem;
    }
    /* Avatar Grid Selection */
    .avatar-selection-grid {
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      gap: 0.75rem;
      margin: 0.75rem 0 1rem 0;
    }
    @media (max-width: 600px) {
      .avatar-selection-grid { grid-template-columns: repeat(2, 1fr); }
    }
    .avatar-card {
      background: #f8fafc;
      border: 2px solid #cbd5e1;
      border-radius: 10px;
      padding: 0.8rem 0.5rem;
      text-align: center;
      cursor: pointer;
      position: relative;
    }
    .avatar-card:hover {
      border-color: var(--secondary);
      background: #f0f9ff;
    }
    .avatar-card.active {
      border-color: var(--primary);
      background: #eff6ff;
      box-shadow: 0 0 0 3px rgba(37, 99, 235, 0.2);
    }
    .avatar-card.active::after {
      content: "✔";
      position: absolute;
      top: 5px;
      right: 5px;
      background: var(--primary);
      color: white;
      border-radius: 50%;
      width: 18px;
      height: 18px;
      font-size: 0.7rem;
      display: flex;
      align-items: center;
      justify-content: center;
      font-weight: 700;
    }
    .avatar-card-icon { font-size: 2.3rem; display: block; margin-bottom: 0.2rem; }
    .avatar-card-name { font-size: 0.85rem; font-weight: 700; }

    /* Dashboard Avatar Showcase & Wearables */
    .avatar-showcase {
      display: flex;
      align-items: center;
      gap: 1.5rem;
      background: linear-gradient(135deg, #eff6ff, #dbeafe);
      border: 2px dashed #93c5fd;
      border-radius: 16px;
      padding: 1.25rem 1.5rem;
      margin-bottom: 1.5rem;
    }
    .avatar-frame {
      width: 90px;
      height: 90px;
      border-radius: 50%;
      background: white;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 3.2rem;
      box-shadow: 0 4px 10px rgba(0,0,0,0.12);
      position: relative;
      flex-shrink: 0;
      user-select: none;
    }
    .wearable-item {
      position: absolute;
      pointer-events: none;
      line-height: 1;
      filter: drop-shadow(0 2px 4px rgba(0, 0, 0, 0.25));
      transition: all 0.3s cubic-bezier(0.34, 1.56, 0.64, 1);
    }
    .wearable-head {
      top: -16px;
      font-size: 2rem;
      left: 50%;
      transform: translateX(-50%);
      z-index: 5;
    }
    .wearable-eyes {
      top: 26px;
      left: 50%;
      transform: translateX(-50%);
      font-size: 1.5rem;
      z-index: 6;
    }
    .wearable-neck {
      bottom: -6px;
      left: 50%;
      transform: translateX(-50%);
      font-size: 1.8rem;
      z-index: 7;
    }
    .wearable-badge {
      top: 4px;
      left: -6px;
      font-size: 1.4rem;
      z-index: 8;
    }
    .avatar-gear-badge {
      position: absolute;
      bottom: -3px;
      right: -3px;
      background: #f59e0b;
      color: white;
      border-radius: 50%;
      width: 24px;
      height: 24px;
      font-size: 0.75rem;
      display: flex;
      align-items: center;
      justify-content: center;
      font-weight: 700;
      z-index: 9;
    }
    .accessory-chip {
      background: white;
      border: 1px solid #cbd5e1;
      border-radius: 20px;
      padding: 0.25rem 0.75rem;
      font-size: 0.8rem;
      font-weight: 600;
      display: inline-flex;
      align-items: center;
      gap: 0.35rem;
      margin-right: 0.4rem;
      margin-top: 0.4rem;
      box-shadow: 0 1px 2px rgba(0,0,0,0.05);
    }

    /* Topics Grid */
    .grid-2 {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
      gap: 1.25rem;
    }
    .topic-card {
      background: white;
      border-radius: 10px;
      border: 1px solid var(--border);
      padding: 1.25rem;
      box-shadow: var(--shadow);
    }
    .topic-card h3 {
      font-size: 1.1rem;
      margin-bottom: 0.5rem;
      color: var(--primary-dark);
    }
    .stage-buttons {
      display: flex;
      gap: 0.4rem;
      flex-wrap: wrap;
      margin-top: 0.5rem;
    }
    .btn-stage {
      flex: 1;
      min-width: 42px;
      padding: 0.5rem 0.2rem;
      font-size: 0.8rem;
      text-align: center;
      border-radius: 6px;
      background-color: #f1f5f9;
      color: var(--text-muted);
      border: 1px solid #cbd5e1;
    }
    .btn-stage.unlocked {
      background-color: #dbeafe;
      color: var(--primary-dark);
      border-color: #93c5fd;
      cursor: pointer;
      font-weight: 600;
    }
    .btn-stage.cleared {
      background-color: #dcfce7;
      color: #15803d;
      border-color: #86efac;
      cursor: pointer;
      font-weight: 700;
    }

    /* Quiz Area */
    .quiz-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 1.25rem;
      border-bottom: 2px solid var(--border);
      padding-bottom: 0.75rem;
    }
    .q-box {
      font-size: 1.25rem;
      font-weight: 600;
      margin-bottom: 1.5rem;
      color: #0f172a;
      min-height: 40px;
    }
    .options-grid {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 0.8rem;
      margin-bottom: 1.5rem;
    }
    @media (max-width: 600px) {
      .options-grid { grid-template-columns: 1fr; }
    }
    .opt-btn {
      padding: 0.9rem;
      text-align: left;
      font-size: 1.05rem;
      border-radius: 8px;
      background: #f8fafc;
      border: 2px solid #cbd5e1;
      color: var(--text);
    }
    .opt-btn:hover:not(:disabled) {
      border-color: var(--primary);
      background-color: #eff6ff;
    }
    .opt-btn.selected 
