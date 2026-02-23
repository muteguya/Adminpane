<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=yes">
  <title>CIUE · Earn Platform</title>
  <!-- Font Awesome 6 (free) -->
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
      font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif;
    }

    body {
      background: #f5f5f5;
      display: flex;
      justify-content: center;
      align-items: center;
      min-height: 100vh;
      padding: 16px;
    }

    /* phone frame */
    .phone {
      max-width: 390px;
      width: 100%;
      background-color: #ffffff;
      border-radius: 40px;
      box-shadow: 0 25px 60px rgba(0, 20, 30, 0.15);
      overflow: hidden;
      display: flex;
      flex-direction: column;
      height: 700px;
    }

    /* Scrollable content area */
    .scroll-content {
      flex: 1;
      overflow-y: auto;
      padding: 20px 20px 10px 20px;
    }

    /* Bottom Navigation - FIXED */
    .bottom-nav {
      display: flex;
      align-items: center;
      justify-content: space-around;
      background: #ffffff;
      padding: 12px 0 8px 0;
      border-top: 1px solid #f0f0f0;
      width: 100%;
      flex-shrink: 0;
    }

    .nav-item {
      display: flex;
      flex-direction: column;
      align-items: center;
      color: #999999;
      font-size: 0.75rem;
      font-weight: 500;
      gap: 4px;
      cursor: pointer;
    }

    .nav-item i {
      font-size: 1.3rem;
      color: #999999;
    }

    .nav-item.active {
      color: #006a7a;
    }

    .nav-item.active i {
      color: #006a7a;
    }

    /* Auth Pages */
    .auth-container {
      height: 100%;
      display: flex;
      flex-direction: column;
    }

    .auth-content {
      flex: 1;
      overflow-y: auto;
      padding: 20px;
    }

    .logo-area {
      text-align: center;
      margin-bottom: 25px;
    }

    .logo-icon {
      width: 80px;
      height: 80px;
      background: linear-gradient(135deg, #006a7a, #00bcd4);
      border-radius: 30px;
      display: flex;
      align-items: center;
      justify-content: center;
      margin: 0 auto 15px;
      color: white;
      font-size: 2.5rem;
      box-shadow: 0 10px 25px rgba(0,150,170,0.3);
    }

    .logo-area h1 {
      color: #003d4d;
      font-size: 2rem;
      font-weight: 700;
      margin-bottom: 5px;
    }

    .logo-area p {
      color: #597e89;
      font-size: 0.9rem;
    }

    .auth-tabs {
      display: flex;
      background: #ecf7f9;
      border-radius: 60px;
      padding: 5px;
      margin-bottom: 25px;
    }

    .auth-tab {
      flex: 1;
      text-align: center;
      padding: 12px;
      border-radius: 60px;
      font-weight: 600;
      color: #006a7a;
      cursor: pointer;
      transition: all 0.2s;
    }

    .auth-tab.active {
      background: white;
      color: #003d4d;
      box-shadow: 0 4px 10px rgba(0,150,160,0.15);
    }

    .auth-form {
      display: none;
    }

    .auth-form.active {
      display: block;
    }

    .form-group {
      margin-bottom: 20px;
    }

    .form-group label {
      display: block;
      color: #003d4d;
      font-weight: 600;
      margin-bottom: 8px;
      font-size: 0.9rem;
    }

    .input-icon {
      position: relative;
      display: flex;
      align-items: center;
    }

    .input-icon i {
      position: absolute;
      left: 15px;
      color: #00acc1;
      font-size: 1.1rem;
    }

    .input-icon input,
    .input-icon select {
      width: 100%;
      padding: 15px 15px 15px 45px;
      border: 2px solid #e0f0f3;
      border-radius: 30px;
      font-size: 1rem;
      outline: none;
      background: white;
    }

    .auth-btn {
      background: linear-gradient(135deg, #006a7a, #00bcd4);
      color: white;
      border: none;
      width: 100%;
      padding: 18px;
      border-radius: 40px;
      font-size: 1.2rem;
      font-weight: 700;
      margin: 20px 0 15px;
      cursor: pointer;
    }

    .auth-footer {
      text-align: center;
      color: #597e89;
      font-size: 0.9rem;
    }

    .auth-footer a {
      color: #006a7a;
      font-weight: 600;
      text-decoration: none;
    }

    /* Success Message */
    .success-message {
      background: #d4edda;
      color: #155724;
      padding: 15px;
      border-radius: 30px;
      text-align: center;
      margin-bottom: 20px;
      display: none;
    }

    /* Main Dashboard Pages */
    #mainDashboard, #profilePage, #levelPage, #taskPage, #incomePage, #adminPanel {
      display: none;
      flex-direction: column;
      height: 100%;
    }

    /* Welcome Section */
    .welcome-title {
      font-size: 2.2rem;
      font-weight: 700;
      color: #000000;
      margin-bottom: 5px;
    }

    .welcome-subtitle {
      font-size: 0.9rem;
      color: #333333;
      margin-bottom: 15px;
    }

    .divider-line {
      height: 1px;
      background-color: #e0e0e0;
      margin: 15px 0;
    }

    /* Book Card */
    .book-card {
      background: #f9f9f9;
      border-radius: 20px;
      padding: 15px;
      border: 1px solid #eaeaea;
      margin-bottom: 20px;
    }

    .book-title {
      font-weight: 700;
      font-size: 1.1rem;
      color: #000;
      margin-bottom: 10px;
    }

    .read-btn {
      background: #006a7a;
      color: white;
      border: none;
      padding: 12px;
      border-radius: 30px;
      width: 100%;
      font-weight: 600;
      cursor: pointer;
    }

    /* Action Row */
    .action-row {
      display: flex;
      align-items: center;
      justify-content: space-between;
      margin: 20px 0;
    }

    .action-item {
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 5px;
      color: #000000;
      font-weight: 500;
      font-size: 0.9rem;
      cursor: pointer;
    }

    .action-item i {
      font-size: 1.3rem;
      color: #000000;
    }

    /* Upgrade Section */
    .upgrade-section {
      background: #fff9e6;
      border-radius: 20px;
      padding: 20px;
      margin-bottom: 25px;
      border: 2px dashed #ffc107;
    }

    .upgrade-title {
      font-weight: 700;
      color: #b45f06;
      margin-bottom: 15px;
      font-size: 1.1rem;
    }

    .upgrade-list {
      list-style: none;
      margin-bottom: 20px;
    }

    .upgrade-list li {
      margin-bottom: 8px;
      font-size: 0.9rem;
      display: flex;
      align-items: center;
      gap: 8px;
    }

    .upgrade-list li i {
      color: #28a745;
    }

    .upgrade-btn {
      background: #ff9800;
      color: white;
      border: none;
      padding: 14px;
      border-radius: 30px;
      width: 100%;
      font-weight: 600;
      cursor: pointer;
    }

    .company-line {
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding: 15px 0;
      border-bottom: 1px solid #f0f0f0;
    }

    /* Profile Page */
    .profile-header {
      display: flex;
      justify-content: space-between;
      margin-bottom: 20px;
    }

    .employee-name {
      font-size: 1.3rem;
      font-weight: 700;
      margin-bottom: 5px;
    }

    .wallets-container {
      display: flex;
      gap: 10px;
      margin-bottom: 20px;
    }

    .wallet-box {
      flex: 1;
      background: #f9f9f9;
      border-radius: 15px;
      padding: 12px;
      border: 1px solid #eaeaea;
    }

    .wallet-box .label {
      color: #666;
      font-size: 0.7rem;
      margin-bottom: 3px;
    }

    .wallet-box .amount {
      font-size: 1.1rem;
      font-weight: 700;
    }

    /* Level Page */
    .level-header {
      text-align: center;
      margin: 40px 0;
    }

    .level-header h1 {
      color: #ff0000;
      font-size: 2rem;
      font-weight: 800;
      text-transform: uppercase;
    }

    .level-table {
      background: #f9f9f9;
      border-radius: 20px;
      padding: 15px;
      margin-bottom: 20px;
    }

    table {
      width: 100%;
      border-collapse: collapse;
    }

    th {
      background: #006a7a;
      color: white;
      padding: 10px;
    }

    td {
      padding: 8px;
      text-align: center;
      border-bottom: 1px solid #ddd;
    }

    /* Admin Panel */
    .admin-section {
      background: #f5f5f5;
      border-radius: 15px;
      padding: 15px;
      margin-bottom: 20px;
    }

    .pending-item {
      background: white;
      padding: 12px;
      border-radius: 10px;
      margin-bottom: 10px;
      display: flex;
      justify-content: space-between;
      align-items: center;
    }

    .approve-btn {
      background: #28a745;
      color: white;
      border: none;
      padding: 5px 15px;
      border-radius: 20px;
      cursor: pointer;
    }

    .reject-btn {
      background: #dc3545;
      color: white;
      border: none;
      padding: 5px 15px;
      border-radius: 20px;
      cursor: pointer;
    }

    /* Modals */
    .modal-overlay {
      display: none;
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: rgba(0,0,0,0.5);
      justify-content: center;
      align-items: center;
      z-index: 1000;
    }

    .modal-content {
      background: white;
      max-width: 390px;
      width: 90%;
      border-radius: 30px;
      padding: 24px;
    }

    .recipient-card {
      background: #f9f9f9;
      border-radius: 15px;
      padding: 16px;
      text-align: center;
      margin-bottom: 20px;
    }

    .recipient-card .number {
      font-size: 1.3rem;
      font-weight: 700;
    }
  </style>
</head>
<body>
  <div class="phone">
    <!-- AUTHENTICATION SECTION (Shows First) -->
    <div id="authContainer" class="auth-container">
      <div class="auth-content">
        <div class="logo-area">
          <div class="logo-icon">
            <i class="fas fa-hand-holding-heart"></i>
          </div>
          <h1>CIUE</h1>
          <p>Mobile Money • Earn • Task Hall</p>
        </div>

        <div id="messageBox" class="success-message">
          <i class="fas fa-check-circle"></i> <span id="messageText"></span>
        </div>

        <div class="auth-tabs">
          <div class="auth-tab active" onclick="switchAuthTab('login')" id="loginTab">Login</div>
          <div class="auth-tab" onclick="switchAuthTab('register')" id="registerTab">Register</div>
        </div>

        <!-- LOGIN FORM -->
        <div id="loginForm" class="auth-form active">
          <form onsubmit="handleLogin(event)">
            <div class="form-group">
              <label>Phone Number</label>
              <div class="input-icon">
                <i class="fas fa-phone-alt"></i>
                <input type="tel" id="loginPhone" placeholder="Enter your phone number" required>
              </div>
            </div>
            <div class="form-group">
              <label>Password</label>
              <div class="input-icon">
                <i class="fas fa-lock"></i>
                <input type="password" id="loginPassword" placeholder="Enter your password" required>
              </div>
            </div>
            <button type="submit" class="auth-btn">Login</button>
            <div class="auth-footer">
              Don't have an account? <a href="#" onclick="switchAuthTab('register'); return false;">Register now</a>
            </div>
          </form>
        </div>

        <!-- REGISTRATION FORM -->
        <div id="registerForm" class="auth-form">
          <form onsubmit="handleRegister(event)">
            <div class="form-group">
              <label>Full Names</label>
              <div class="input-icon">
                <i class="fas fa-user"></i>
                <input type="text" id="regFullName" placeholder="Enter your full names" required>
              </div>
            </div>
            <div class="form-group">
              <label>Phone Number</label>
              <div class="input-icon">
                <i class="fas fa-phone-alt"></i>
                <input type="tel" id="regPhone" placeholder="Enter your phone number" required>
              </div>
            </div>
            <div class="form-group">
              <label>Country</label>
              <div class="input-icon">
                <i class="fas fa-globe-africa"></i>
                <select id="regCountry" required>
                  <option value="">Select your country</option>
                  <option value="Uganda">Uganda 🇺🇬</option>
                  <option value="Kenya">Kenya 🇰🇪</option>
                  <option value="Tanzania">Tanzania 🇹🇿</option>
                </select>
              </div>
            </div>
            <div class="form-group">
              <label>Password</label>
              <div class="input-icon">
                <i class="fas fa-lock"></i>
                <input type="password" id="regPassword" placeholder="Create a password" required>
              </div>
            </div>
            <button type="submit" class="auth-btn">Register</button>
            <div class="auth-footer">
              Already have an account? <a href="#" onclick="switchAuthTab('login'); return false;">Login here</a>
            </div>
          </form>
        </div>
      </div>
    </div>

    <!-- MAIN DASHBOARD (Home Page) -->
    <div id="mainDashboard">
      <div class="scroll-content">
        <div class="welcome-title">WELCOME</div>
        <div class="welcome-subtitle">NEW OPPORTUNITIES AND CHALLENGES WORK TOGETHER TO CREATE A BETTER FUTURE</div>
        <div class="divider-line"></div>

        <div class="book-card">
          <div class="book-title">Financial literacy</div>
          <button class="read-btn" onclick="alert('Read feature coming soon')">READ</button>
        </div>

        <div class="action-row">
          <div class="action-item" onclick="openDepositModal()">
            <i class="fas fa-wallet"></i>
            <span>Recharge</span>
          </div>
          <div class="action-item" onclick="openWithdrawModal()">
            <i class="fas fa-hand-holding-usd"></i>
            <span>Withdraw</span>
          </div>
          <div class="action-item" onclick="alert('Company profile')">
            <i class="fas fa-building"></i>
            <span>Company</span>
          </div>
        </div>

        <div class="upgrade-section">
          <div class="upgrade-title">⬆️ UPGRADE TO LEVEL 1-9</div>
          <ul class="upgrade-list">
            <li><i class="fas fa-check-circle"></i> Withdraw Monday-Saturday</li>
            <li><i class="fas fa-check-circle"></i> Referral bonuses</li>
            <li><i class="fas fa-check-circle"></i> More books per day</li>
            <li><i class="fas fa-check-circle"></i> Higher rewards</li>
            <li><i class="fas fa-check-circle"></i> 365 days access</li>
          </ul>
          <button class="upgrade-btn" onclick="openDepositModal()">DEPOSIT & UPGRADE NOW</button>
        </div>

        <div class="company-line">
          <span>Company Profile</span>
          <i class="fas fa-chevron-right"></i>
        </div>
      </div>
      <div class="bottom-nav">
        <div class="nav-item active" onclick="showPage('home')"><i class="fas fa-home"></i><span>Home</span></div>
        <div class="nav-item" onclick="showPage('task')"><i class="fas fa-tasks"></i><span>Task</span></div>
        <div class="nav-item" onclick="showPage('level')"><i class="fas fa-chart-simple"></i><span>Level</span></div>
        <div class="nav-item" onclick="showPage('income')"><i class="fas fa-coins"></i><span>Income</span></div>
        <div class="nav-item" onclick="showPage('profile')"><i class="fas fa-user"></i><span>Me</span></div>
      </div>
    </div>

    <!-- PROFILE PAGE -->
    <div id="profilePage">
      <div class="scroll-content">
        <div class="profile-header">
          <span class="time" id="currentTime"></span>
          <span><i class="fas fa-user"></i> <span id="profileDisplayName">User</span></span>
        </div>
        <div class="employee-name" id="profileFullName">Mindy official</div>
        <div class="employee-role" id="profileMemberType">INTERN MEMBER</div>

        <div class="wallets-container">
          <div class="wallet-box main">
            <div class="label">💰 MAIN WALLET</div>
            <div class="amount" id="profileMainWallet">0 <small>UGX</small></div>
          </div>
          <div class="wallet-box commission">
            <div class="label">💼 COMMISSION</div>
            <div class="amount" id="profileCommissionWallet">0 <small>UGX</small></div>
          </div>
        </div>

        <div style="background:#f0f8ff; border-radius:15px; padding:15px; margin-bottom:20px;">
          <div style="display:flex; justify-content:space-between;">
            <span>Days Left: <span id="profileDaysLeft">4</span></span>
            <span>Books Today: <span id="profileBooksToday">0/1</span></span>
          </div>
        </div>

        <button class="logout-btn" onclick="logout()" style="width:100%; padding:12px; border:1px solid #ddd; border-radius:30px; background:none;">Logout</button>
      </div>
      <div class="bottom-nav">
        <div class="nav-item" onclick="showPage('home')"><i class="fas fa-home"></i><span>Home</span></div>
        <div class="nav-item" onclick="showPage('task')"><i class="fas fa-tasks"></i><span>Task</span></div>
        <div class="nav-item" onclick="showPage('level')"><i class="fas fa-chart-simple"></i><span>Level</span></div>
        <div class="nav-item" onclick="showPage('income')"><i class="fas fa-coins"></i><span>Income</span></div>
        <div class="nav-item active" onclick="showPage('profile')"><i class="fas fa-user"></i><span>Me</span></div>
      </div>
    </div>

    <!-- LEVEL PAGE -->
    <div id="levelPage">
      <div class="scroll-content">
        <div class="level-header">
          <h1>LEVELS PRICE AND SALARIES</h1>
        </div>
        
        <div class="level-table">
          <table>
            <tr><th>Level</th><th>Deposit</th><th>Books/Day</th><th>Per Book</th></tr>
            <tr><td>1</td><td>25,000</td><td>2</td><td>1,125</td></tr>
            <tr><td>2</td><td>50,000</td><td>3</td><td>1,500</td></tr>
            <tr><td>3</td><td>100,000</td><td>4</td><td>2,000</td></tr>
            <tr><td>4</td><td>200,000</td><td>5</td><td>2,500</td></tr>
            <tr><td>5</td><td>350,000</td><td>6</td><td>3,000</td></tr>
            <tr><td>6</td><td>500,000</td><td>7</td><td>3,500</td></tr>
            <tr><td>7</td><td>750,000</td><td>8</td><td>4,000</td></tr>
            <tr><td>8</td><td>1,000,000</td><td>9</td><td>4,500</td></tr>
            <tr><td>9</td><td>1,500,000</td><td>10</td><td>5,000</td></tr>
          </table>
        </div>
        <button onclick="openDepositModal()" style="background:#ff9800; color:white; border:none; padding:15px; border-radius:30px; width:100%;">UPGRADE NOW</button>
      </div>
      <div class="bottom-nav">
        <div class="nav-item" onclick="showPage('home')"><i class="fas fa-home"></i><span>Home</span></div>
        <div class="nav-item" onclick="showPage('task')"><i class="fas fa-tasks"></i><span>Task</span></div>
        <div class="nav-item active" onclick="showPage('level')"><i class="fas fa-chart-simple"></i><span>Level</span></div>
        <div class="nav-item" onclick="showPage('income')"><i class="fas fa-coins"></i><span>Income</span></div>
        <div class="nav-item" onclick="showPage('profile')"><i class="fas fa-user"></i><span>Me</span></div>
      </div>
    </div>

    <!-- TASK PAGE -->
    <div id="taskPage">
      <div class="scroll-content">
        <h3 style="margin-bottom:20px;">Book Library</h3>
        <div class="book-card">
          <div class="book-title">Financial literacy</div>
          <button class="read-btn" onclick="alert('Read feature coming soon')">READ</button>
        </div>
        <div class="book-card">
          <div class="book-title">Think and Grow Rich</div>
          <button class="read-btn" onclick="alert('Read feature coming soon')">READ</button>
        </div>
      </div>
      <div class="bottom-nav">
        <div class="nav-item" onclick="showPage('home')"><i class="fas fa-home"></i><span>Home</span></div>
        <div class="nav-item active" onclick="showPage('task')"><i class="fas fa-tasks"></i><span>Task</span></div>
        <div class="nav-item" onclick="showPage('level')"><i class="fas fa-chart-simple"></i><span>Level</span></div>
        <div class="nav-item" onclick="showPage('income')"><i class="fas fa-coins"></i><span>Income</span></div>
        <div class="nav-item" onclick="showPage('profile')"><i class="fas fa-user"></i><span>Me</span></div>
      </div>
    </div>

    <!-- INCOME PAGE -->
    <div id="incomePage">
      <div class="scroll-content">
        <h3 style="margin:20px 0;">Income History</h3>
        <p style="color:#666; text-align:center;">Coming soon...</p>
      </div>
      <div class="bottom-nav">
        <div class="nav-item" onclick="showPage('home')"><i class="fas fa-home"></i><span>Home</span></div>
        <div class="nav-item" onclick="showPage('task')"><i class="fas fa-tasks"></i><span>Task</span></div>
        <div class="nav-item" onclick="showPage('level')"><i class="fas fa-chart-simple"></i><span>Level</span></div>
        <div class="nav-item active" onclick="showPage('income')"><i class="fas fa-coins"></i><span>Income</span></div>
        <div class="nav-item" onclick="showPage('profile')"><i class="fas fa-user"></i><span>Me</span></div>
      </div>
    </div>

    <!-- ADMIN PANEL (Hidden) -->
    <div id="adminPanel">
      <div class="scroll-content">
        <h2 style="margin-bottom:20px;">👑 Admin Panel</h2>
        <div class="admin-section">
          <h4>Pending Deposits</h4>
          <div id="pendingDepositsList">
            <p style="color:#666;">No pending deposits</p>
          </div>
        </div>
        <button onclick="logout()" style="background:#dc3545; color:white; border:none; padding:10px; border-radius:30px; width:100%;">Exit Admin</button>
      </div>
    </div>
  </div>

  <!-- DEPOSIT MODAL -->
  <div class="modal-overlay" id="depositModal">
    <div class="modal-content">
      <div class="modal-header" style="display:flex; justify-content:space-between; margin-bottom:20px;">
        <h2>Deposit</h2>
        <button class="close-btn" onclick="closeDepositModal()" style="font-size:1.8rem; background:none; border:none;">&times;</button>
      </div>
      <div class="recipient-card">
        <div class="number">0756 673 144</div>
        <div class="name">NAMUHANGA VERONIC</div>
      </div>
      <div class="custom-amount">
        <input type="number" id="depositAmount" placeholder="Enter amount" style="width:100%; padding:15px; border:1px solid #ddd; border-radius:15px;">
      </div>
      <button class="deposit-btn" onclick="submitDeposit()" style="background:#000; color:white; width:100%; padding:15px; border:none; border-radius:30px; margin-top:15px;">Send Money</button>
    </div>
  </div>

  <!-- WITHDRAW MODAL -->
  <div class="modal-overlay" id="withdrawModal">
    <div class="modal-content">
      <div class="modal-header" style="display:flex; justify-content:space-between; margin-bottom:20px;">
        <h2>Withdraw</h2>
        <button class="close-btn" onclick="closeWithdrawModal()" style="font-size:1.8rem; background:none; border:none;">&times;</button>
      </div>
      <input type="number" id="withdrawAmount" placeholder="Amount" style="width:100%; padding:15px; border:1px solid #ddd; border-radius:15px; margin-bottom:10px;">
      <input type="tel" id="withdrawPhone" placeholder="Mobile number" style="width:100%; padding:15px; border:1px solid #ddd; border-radius:15px; margin-bottom:10px;">
      <button onclick="submitWithdraw()" style="background:#000; color:white; width:100%; padding:15px; border:none; border-radius:30px;">Withdraw</button>
    </div>
  </div>

  <script>
    let users = JSON.parse(localStorage.getItem('cueUsers')) || {};
    let currentUser = localStorage.getItem('currentUser');
    let pendingDeposits = JSON.parse(localStorage.getItem('pendingDeposits')) || [];

    // Show message
    function showMessage(text, isSuccess = true) {
      const msgBox = document.getElementById('messageBox');
      document.getElementById('messageText').textContent = text;
      msgBox.style.display = 'block';
      msgBox.style.background = isSuccess ? '#d4edda' : '#f8d7da';
      msgBox.style.color = isSuccess ? '#155724' : '#721c24';
      setTimeout(() => msgBox.style.display = 'none', 3000);
    }

    // Switch tabs
    function switchAuthTab(tab) {
      document.getElementById('loginForm').classList.toggle('active', tab === 'login');
      document.getElementById('registerForm').classList.toggle('active', tab === 'register');
      document.getElementById('loginTab').classList.toggle('active', tab === 'login');
      document.getElementById('registerTab').classList.toggle('active', tab === 'register');
    }

    // Handle Login
    function handleLogin(e) {
      e.preventDefault();
      const phone = document.getElementById('loginPhone').value.trim();
      const password = document.getElementById('loginPassword').value;
      
      if (users[phone] && users[phone].password === password) {
        localStorage.setItem('currentUser', phone);
        currentUser = phone;
        showMessage('Login successful!');
        setTimeout(() => {
          loadUserData();
          showPage('home');
        }, 500);
      } else {
        showMessage('Invalid phone or password', false);
      }
    }

    // Handle Register
    function handleRegister(e) {
      e.preventDefault();
      const fullName = document.getElementById('regFullName').value.trim();
      const phone = document.getElementById('regPhone').value.trim();
      const country = document.getElementById('regCountry').value;
      const password = document.getElementById('regPassword').value;

      if (!fullName || !phone || !country || !password) {
        showMessage('Please fill all fields', false);
        return;
      }

      if (users[phone]) {
        showMessage('Phone already registered', false);
        switchAuthTab('login');
        return;
      }

      const now = new Date();
      const expiry = new Date(now);
      expiry.setDate(expiry.getDate() + 4);

      users[phone] = {
        fullName, phone, country, password,
        memberLevel: 0,
        memberExpiry: expiry.toISOString(),
        mainWallet: 0,
        commissionWallet: 0,
        registeredDate: now.toISOString()
      };

      localStorage.setItem('cueUsers', JSON.stringify(users));
      localStorage.setItem('currentUser', phone);
      currentUser = phone;
      showMessage('Registration successful!');
      setTimeout(() => {
        loadUserData();
        showPage('home');
      }, 500);
    }

    // Page navigation
    function showPage(page) {
      document.getElementById('authContainer').style.display = 'none';
      document.getElementById('mainDashboard').style.display = page === 'home' ? 'flex' : 'none';
      document.getElementById('profilePage').style.display = page === 'profile' ? 'flex' : 'none';
      document.getElementById('levelPage').style.display = page === 'level' ? 'flex' : 'none';
      document.getElementById('taskPage').style.display = page === 'task' ? 'flex' : 'none';
      document.getElementById('incomePage').style.display = page === 'income' ? 'flex' : 'none';
      document.getElementById('adminPanel').style.display = 'none';
    }

    // Load user data
    function loadUserData() {
      if (!currentUser) return;
      const user = users[currentUser];
      if (!user) return;

      document.getElementById('profileFullName').textContent = user.fullName || 'User';
      document.getElementById('profileDisplayName').textContent = user.fullName?.split(' ')[0] || 'User';
      document.getElementById('profileMainWallet').innerHTML = `${(user.mainWallet || 0).toLocaleString()} <small>UGX</small>`;
      document.getElementById('profileCommissionWallet').innerHTML = `${(user.commissionWallet || 0).toLocaleString()} <small>UGX</small>`;
      
      const daysLeft = Math.ceil((new Date(user.memberExpiry) - new Date()) / (1000*60*60*24));
      document.getElementById('profileDaysLeft').textContent = daysLeft > 0 ? daysLeft : 0;
      document.getElementById('profileMemberType').textContent = user.memberLevel === 0 ? 'INTERN MEMBER' : `LEVEL ${user.memberLevel} MEMBER`;
      
      updateTime();
    }

    // Admin check
    function checkAdmin() {
      if (window.location.hash === '#admin' && currentUser === '0756673144') {
        document.getElementById('authContainer').style.display = 'none';
        document.getElementById('adminPanel').style.display = 'flex';
        loadAdminData();
      }
    }

    // Load admin data
    function loadAdminData() {
      const list = document.getElementById('pendingDepositsList');
      if (pendingDeposits.length === 0) {
        list.innerHTML = '<p style="color:#666;">No pending deposits</p>';
      } else {
        let html = '';
        pendingDeposits.forEach(deposit => {
          html += `
            <div class="pending-item">
              <div>
                <div>${deposit.phone}</div>
                <div style="font-weight:700;">${deposit.amount.toLocaleString()} UGX</div>
              </div>
              <button class="approve-btn" onclick="approveDeposit(${deposit.id})">Approve</button>
            </div>
          `;
        });
        list.innerHTML = html;
      }
    }

    function approveDeposit(id) {
      const deposit = pendingDeposits.find(d => d.id === id);
      if (deposit && users[deposit.userId]) {
        users[deposit.userId].mainWallet += deposit.amount;
        localStorage.setItem('cueUsers', JSON.stringify(users));
        pendingDeposits = pendingDeposits.filter(d => d.id !== id);
        localStorage.setItem('pendingDeposits', JSON.stringify(pendingDeposits));
        loadAdminData();
        showMessage('Deposit approved!');
      }
    }

    // Deposit functions
    function openDepositModal() {
      document.getElementById('depositModal').style.display = 'flex';
    }

    function closeDepositModal() {
      document.getElementById('depositModal').style.display = 'none';
    }

    function submitDeposit() {
      const amount = parseInt(document.getElementById('depositAmount').value);
      if (!amount || amount < 1000) {
        alert('Please enter valid amount');
        return;
      }

      const deposit = {
        id: Date.now(),
        userId: currentUser,
        phone: users[currentUser]?.phone,
        amount: amount,
        timestamp: new Date().toISOString()
      };

      pendingDeposits.push(deposit);
      localStorage.setItem('pendingDeposits', JSON.stringify(pendingDeposits));
      
      alert('Deposit request sent to admin!');
      closeDepositModal();
    }

    // Withdraw functions
    function openWithdrawModal() {
      document.getElementById('withdrawModal').style.display = 'flex';
    }

    function closeWithdrawModal() {
      document.getElementById('withdrawModal').style.display = 'none';
    }

    function submitWithdraw() {
      const amount = parseInt(document.getElementById('withdrawAmount').value);
      const phone = document.getElementById('withdrawPhone').value;
      const user = users[currentUser];

      if (!amount || amount < 1000) {
        alert('Enter valid amount');
        return;
      }

      if (amount > (user.mainWallet || 0)) {
        alert('Insufficient balance');
        return;
      }

      user.mainWallet -= amount;
      localStorage.setItem('cueUsers', JSON.stringify(users));
      alert(`Withdrawal of ${amount} UGX requested to ${phone}`);
      closeWithdrawModal();
      loadUserData();
    }

    // Time update
    function updateTime() {
      const now = new Date();
      let hours = now.getHours();
      const minutes = now.getMinutes().toString().padStart(2, '0');
      const ampm = hours >= 12 ? 'PM' : 'AM';
      hours = hours % 12 || 12;
      document.getElementById('currentTime').textContent = `${hours}:${minutes} ${ampm}`;
    }

    // Logout
    function logout() {
      localStorage.removeItem('currentUser');
      currentUser = null;
      document.getElementById('authContainer').style.display = 'flex';
      document.getElementById('mainDashboard').style.display = 'none';
      document.getElementById('profilePage').style.display = 'none';
      document.getElementById('levelPage').style.display = 'none';
      document.getElementById('taskPage').style.display = 'none';
      document.getElementById('incomePage').style.display = 'none';
      document.getElementById('adminPanel').style.display = 'none';
      switchAuthTab('login');
    }

    // Initialize
    window.onload = function() {
      // Create demo accounts
      if (Object.keys(users).length === 0) {
        users['0756673144'] = {
          fullName: 'Admin User',
          phone: '0756673144',
          country: 'Uganda',
          password: 'admin123',
          memberLevel: 9,
          memberExpiry: new Date(Date.now() + 365*24*60*60*1000).toISOString(),
          mainWallet: 1000000,
          commissionWallet: 387566.50
        };
        users['0777123456'] = {
          fullName: 'Intern User',
          phone: '0777123456',
          country: 'Uganda',
          password: '123456',
          memberLevel: 0,
          memberExpiry: new Date(Date.now() + 4*24*60*60*1000).toISOString(),
          mainWallet: 0,
          commissionWallet: 1500
        };
        localStorage.setItem('cueUsers', JSON.stringify(users));
      }

      if (currentUser && users[currentUser]) {
        loadUserData();
        showPage('home');
      }

      setInterval(updateTime, 60000);
      updateTime();
      
      // Check for admin hash
      window.addEventListener('hashchange', checkAdmin);
      checkAdmin();
    };
  </script>
</body>
</html>
