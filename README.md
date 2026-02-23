<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>CIUE · Admin Panel</title>
  <!-- Font Awesome -->
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
      font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
    }

    body {
      background: #f0f2f5;
      padding: 20px;
    }

    .container {
      max-width: 1200px;
      margin: 0 auto;
    }

    /* Admin Login */
    .login-container {
      max-width: 400px;
      margin: 100px auto;
      background: white;
      border-radius: 20px;
      padding: 30px;
      box-shadow: 0 10px 30px rgba(0,0,0,0.1);
    }

    .login-container h2 {
      color: #006a7a;
      margin-bottom: 30px;
      text-align: center;
    }

    .login-container input {
      width: 100%;
      padding: 15px;
      margin-bottom: 15px;
      border: 2px solid #e0e0e0;
      border-radius: 10px;
      font-size: 1rem;
    }

    .login-container button {
      width: 100%;
      padding: 15px;
      background: #006a7a;
      color: white;
      border: none;
      border-radius: 10px;
      font-size: 1.1rem;
      font-weight: 600;
      cursor: pointer;
    }

    /* Main Admin Dashboard */
    .admin-header {
      background: white;
      border-radius: 15px;
      padding: 20px;
      margin-bottom: 30px;
      display: flex;
      justify-content: space-between;
      align-items: center;
      box-shadow: 0 5px 15px rgba(0,0,0,0.05);
    }

    .admin-header h1 {
      color: #006a7a;
      font-size: 1.8rem;
    }

    .logout-btn {
      background: #dc3545;
      color: white;
      border: none;
      padding: 10px 20px;
      border-radius: 10px;
      cursor: pointer;
    }

    /* Stats Cards */
    .stats-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
      gap: 20px;
      margin-bottom: 30px;
    }

    .stat-card {
      background: white;
      border-radius: 15px;
      padding: 20px;
      box-shadow: 0 5px 15px rgba(0,0,0,0.05);
    }

    .stat-card h3 {
      color: #666;
      font-size: 0.9rem;
      margin-bottom: 10px;
    }

    .stat-card .number {
      font-size: 2rem;
      font-weight: 700;
      color: #006a7a;
    }

    /* Section Cards */
    .section-card {
      background: white;
      border-radius: 15px;
      padding: 20px;
      margin-bottom: 30px;
      box-shadow: 0 5px 15px rgba(0,0,0,0.05);
    }

    .section-title {
      font-size: 1.3rem;
      color: #333;
      margin-bottom: 20px;
      padding-bottom: 10px;
      border-bottom: 2px solid #f0f0f0;
    }

    /* Tables */
    .table-responsive {
      overflow-x: auto;
    }

    table {
      width: 100%;
      border-collapse: collapse;
    }

    th {
      background: #f8f9fa;
      padding: 12px;
      text-align: left;
      font-weight: 600;
      color: #555;
    }

    td {
      padding: 12px;
      border-bottom: 1px solid #f0f0f0;
    }

    .badge {
      padding: 5px 10px;
      border-radius: 20px;
      font-size: 0.8rem;
      font-weight: 600;
    }

    .badge.pending {
      background: #fff3cd;
      color: #856404;
    }

    .badge.approved {
      background: #d4edda;
      color: #155724;
    }

    /* Buttons */
    .btn {
      padding: 8px 15px;
      border: none;
      border-radius: 8px;
      cursor: pointer;
      font-size: 0.9rem;
      margin: 0 5px;
    }

    .btn-approve {
      background: #28a745;
      color: white;
    }

    .btn-reject {
      background: #dc3545;
      color: white;
    }

    .btn-edit {
      background: #ffc107;
      color: #333;
    }

    .btn-reset {
      background: #17a2b8;
      color: white;
    }

    .btn-save {
      background: #006a7a;
      color: white;
    }

    .btn-refresh {
      background: #6c757d;
      color: white;
      padding: 10px 20px;
      border: none;
      border-radius: 10px;
      cursor: pointer;
      margin-bottom: 20px;
    }

    /* Modal */
    .modal {
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
      max-width: 500px;
      width: 90%;
      border-radius: 20px;
      padding: 30px;
    }

    .modal-content h3 {
      margin-bottom: 20px;
      color: #333;
    }

    .modal-content input,
    .modal-content select {
      width: 100%;
      padding: 12px;
      margin-bottom: 15px;
      border: 2px solid #e0e0e0;
      border-radius: 8px;
    }

    .modal-buttons {
      display: flex;
      gap: 10px;
      justify-content: flex-end;
    }

    /* Search Bar */
    .search-bar {
      margin-bottom: 20px;
      display: flex;
      gap: 10px;
    }

    .search-bar input {
      flex: 1;
      padding: 12px;
      border: 2px solid #e0e0e0;
      border-radius: 10px;
      font-size: 1rem;
    }

    .search-bar button {
      padding: 12px 25px;
      background: #006a7a;
      color: white;
      border: none;
      border-radius: 10px;
      cursor: pointer;
    }

    /* Empty State */
    .empty-state {
      text-align: center;
      padding: 40px;
      color: #999;
      font-size: 1rem;
    }

    .empty-state i {
      font-size: 3rem;
      margin-bottom: 15px;
      color: #ddd;
    }

    /* Responsive */
    @media (max-width: 768px) {
      .admin-header {
        flex-direction: column;
        gap: 15px;
        text-align: center;
      }
      
      .stats-grid {
        grid-template-columns: 1fr;
      }
    }
  </style>
</head>
<body>
  <div class="container">
    <!-- LOGIN SECTION -->
    <div id="loginSection" class="login-container">
      <h2><i class="fas fa-crown"></i> Admin Login</h2>
      <input type="text" id="adminUsername" placeholder="Username" value="admin">
      <input type="password" id="adminPassword" placeholder="Password">
      <button onclick="adminLogin()">Login to Dashboard</button>
    </div>

    <!-- ADMIN DASHBOARD (Hidden initially) -->
    <div id="adminDashboard" style="display: none;">
      <!-- Header -->
      <div class="admin-header">
        <h1><i class="fas fa-crown" style="margin-right:10px;"></i> CIUE Admin Panel</h1>
        <div>
          <button class="btn-refresh" onclick="refreshDashboard()"><i class="fas fa-sync-alt"></i> Refresh Data</button>
          <button class="logout-btn" onclick="logout()"><i class="fas fa-sign-out-alt"></i> Logout</button>
        </div>
      </div>

      <!-- Stats Cards -->
      <div class="stats-grid" id="statsContainer">
        <!-- Stats loaded via JS -->
      </div>

      <!-- PENDING DEPOSITS SECTION -->
      <div class="section-card">
        <h2 class="section-title"><i class="fas fa-clock" style="margin-right:10px; color:#ffc107;"></i> Pending Deposits</h2>
        <div class="table-responsive">
          <table id="pendingDepositsTable">
            <thead>
              <tr>
                <th>Date</th>
                <th>User</th>
                <th>Phone</th>
                <th>Amount</th>
                <th>Level</th>
                <th>Action</th>
              </tr>
            </thead>
            <tbody id="pendingDepositsBody">
              <!-- Data loaded via JS -->
            </tbody>
          </table>
        </div>
      </div>

      <!-- PENDING WITHDRAWALS SECTION -->
      <div class="section-card">
        <h2 class="section-title"><i class="fas fa-hand-holding-usd" style="margin-right:10px; color:#17a2b8;"></i> Pending Withdrawals</h2>
        <div class="table-responsive">
          <table id="pendingWithdrawalsTable">
            <thead>
              <tr>
                <th>Date</th>
                <th>User</th>
                <th>Phone</th>
                <th>Amount</th>
                <th>Wallet</th>
                <th>Mobile Money</th>
                <th>Action</th>
              </tr>
            </thead>
            <tbody id="pendingWithdrawalsBody">
              <!-- Data loaded via JS -->
            </tbody>
          </table>
        </div>
      </div>

      <!-- ALL MEMBERS SECTION -->
      <div class="section-card">
        <h2 class="section-title"><i class="fas fa-users" style="margin-right:10px;"></i> All Members</h2>
        
        <!-- Search Bar -->
        <div class="search-bar">
          <input type="text" id="searchMember" placeholder="Search by name or phone...">
          <button onclick="searchMembers()"><i class="fas fa-search"></i> Search</button>
        </div>

        <div class="table-responsive">
          <table id="membersTable">
            <thead>
              <tr>
                <th>Name</th>
                <th>Phone</th>
                <th>Country</th>
                <th>Level</th>
                <th>Main Wallet</th>
                <th>Commission</th>
                <th>Expiry</th>
                <th>Actions</th>
              </tr>
            </thead>
            <tbody id="membersBody">
              <!-- Data loaded via JS -->
            </tbody>
          </table>
        </div>
      </div>
    </div>

    <!-- EDIT MEMBER MODAL -->
    <div id="editModal" class="modal">
      <div class="modal-content">
        <h3><i class="fas fa-edit"></i> Edit Member</h3>
        <input type="hidden" id="editPhone">
        
        <label>Full Name</label>
        <input type="text" id="editFullName" placeholder="Full Name">
        
        <label>Phone Number</label>
        <input type="tel" id="editNewPhone" placeholder="New Phone Number">
        
        <label>Country</label>
        <select id="editCountry">
          <option value="Uganda">Uganda</option>
          <option value="Kenya">Kenya</option>
          <option value="Tanzania">Tanzania</option>
          <option value="Burundi">Burundi</option>
          <option value="South Sudan">South Sudan</option>
        </select>
        
        <label>Member Level</label>
        <select id="editLevel">
          <option value="0">Intern</option>
          <option value="1">Level 1</option>
          <option value="2">Level 2</option>
          <option value="3">Level 3</option>
          <option value="4">Level 4</option>
          <option value="5">Level 5</option>
          <option value="6">Level 6</option>
          <option value="7">Level 7</option>
          <option value="8">Level 8</option>
          <option value="9">Level 9</option>
        </select>
        
        <label>Main Wallet Balance</label>
        <input type="number" id="editMainWallet" placeholder="Main Wallet">
        
        <label>Commission Wallet</label>
        <input type="number" id="editCommissionWallet" placeholder="Commission Wallet">

        <div class="modal-buttons">
          <button class="btn btn-save" onclick="saveMemberChanges()">Save Changes</button>
          <button class="btn" style="background:#6c757d; color:white;" onclick="closeEditModal()">Cancel</button>
        </div>
      </div>
    </div>

    <!-- RESET PASSWORD MODAL -->
    <div id="resetModal" class="modal">
      <div class="modal-content">
        <h3><i class="fas fa-key"></i> Reset Password</h3>
        <input type="hidden" id="resetPhone">
        
        <label>New Password</label>
        <input type="text" id="newPassword" value="123456">
        
        <p style="color:#666; font-size:0.9rem; margin-bottom:20px;">Default password: 123456</p>

        <div class="modal-buttons">
          <button class="btn btn-reset" onclick="resetPassword()">Reset Password</button>
          <button class="btn" style="background:#6c757d; color:white;" onclick="closeResetModal()">Cancel</button>
        </div>
      </div>
    </div>
  </div>

  <script>
    // ========== DATA ==========
    let users = JSON.parse(localStorage.getItem('cueUsers')) || {};
    let pendingDeposits = JSON.parse(localStorage.getItem('pendingDeposits')) || [];
    let pendingWithdrawals = JSON.parse(localStorage.getItem('pendingWithdrawals')) || [];
    let isAdminLoggedIn = sessionStorage.getItem('adminLoggedIn') === 'true';

    // Admin credentials (change these)
    const ADMIN_USER = 'admin';
    const ADMIN_PASS = 'admin123';

    // ========== LOGIN ==========
    function adminLogin() {
      const username = document.getElementById('adminUsername').value;
      const password = document.getElementById('adminPassword').value;

      if (username === ADMIN_USER && password === ADMIN_PASS) {
        sessionStorage.setItem('adminLoggedIn', 'true');
        isAdminLoggedIn = true;
        showDashboard();
      } else {
        alert('Invalid credentials!');
      }
    }

    function logout() {
      sessionStorage.removeItem('adminLoggedIn');
      isAdminLoggedIn = false;
      document.getElementById('loginSection').style.display = 'block';
      document.getElementById('adminDashboard').style.display = 'none';
    }

    // ========== DASHBOARD ==========
    function showDashboard() {
      document.getElementById('loginSection').style.display = 'none';
      document.getElementById('adminDashboard').style.display = 'block';
      refreshDashboard();
    }

    // Load Stats
    function loadStats() {
      const totalUsers = Object.keys(users).length;
      const pendingDepositsCount = pendingDeposits.length;
      const pendingWithdrawalsCount = pendingWithdrawals.length;
      
      // Calculate total deposits approved
      const totalDeposits = Object.values(users).reduce((sum, user) => sum + (user.mainWallet || 0), 0);
      
      const statsHtml = `
        <div class="stat-card">
          <h3>Total Users</h3>
          <div class="number">${totalUsers}</div>
        </div>
        <div class="stat-card">
          <h3>Pending Deposits</h3>
          <div class="number">${pendingDepositsCount}</div>
        </div>
        <div class="stat-card">
          <h3>Pending Withdrawals</h3>
          <div class="number">${pendingWithdrawalsCount}</div>
        </div>
        <div class="stat-card">
          <h3>Total Balance</h3>
          <div class="number">${totalDeposits.toLocaleString()} UGX</div>
        </div>
      `;
      
      document.getElementById('statsContainer').innerHTML = statsHtml;
    }

    // ========== PENDING DEPOSITS ==========
    function loadPendingDeposits() {
      const tbody = document.getElementById('pendingDepositsBody');
      
      if (pendingDeposits.length === 0) {
        tbody.innerHTML = `
          <tr>
            <td colspan="6" style="text-align:center; padding:40px;">
              <div class="empty-state">
                <i class="fas fa-inbox"></i>
                <p>No pending deposits</p>
              </div>
            </td>
          </tr>`;
        return;
      }

      let html = '';
      pendingDeposits.forEach(deposit => {
        const user = users[deposit.userId] || {};
        html += `
          <tr>
            <td>${new Date(deposit.timestamp).toLocaleString()}</td>
            <td>${user.fullName || 'Unknown'}</td>
            <td>${deposit.phone || user.phone || 'N/A'}</td>
            <td><strong>${deposit.amount.toLocaleString()} UGX</strong></td>
            <td>Level ${deposit.level || '?'}</td>
            <td>
              <button class="btn btn-approve" onclick="approveDeposit(${deposit.id})">
                <i class="fas fa-check"></i> Approve
              </button>
              <button class="btn btn-reject" onclick="rejectDeposit(${deposit.id})">
                <i class="fas fa-times"></i> Reject
              </button>
            </td>
          </tr>
        `;
      });
      
      tbody.innerHTML = html;
    }

    function approveDeposit(id) {
      if (!confirm('Approve this deposit?')) return;
      
      const deposit = pendingDeposits.find(d => d.id === id);
      if (!deposit) return;

      const user = users[deposit.userId];
      if (user) {
        // Add to main wallet
        user.mainWallet = (user.mainWallet || 0) + deposit.amount;
        
        // Upgrade level if selected
        if (deposit.level && deposit.level > (user.memberLevel || 0)) {
          user.memberLevel = deposit.level;
          // Set expiry to 365 days from now
          const expiry = new Date();
          expiry.setDate(expiry.getDate() + 365);
          user.memberExpiry = expiry.toISOString();
        }

        // Add transaction record
        if (!user.transactions) user.transactions = [];
        user.transactions.unshift({
          type: 'deposit',
          amount: deposit.amount,
          date: new Date().toLocaleString(),
          status: 'approved'
        });

        localStorage.setItem('cueUsers', JSON.stringify(users));
      }

      // Remove from pending - permanently!
      pendingDeposits = pendingDeposits.filter(d => d.id !== id);
      localStorage.setItem('pendingDeposits', JSON.stringify(pendingDeposits));

      alert(`✅ Deposit of ${deposit.amount.toLocaleString()} UGX approved!`);
      refreshDashboard();
    }

    function rejectDeposit(id) {
      if (!confirm('Reject this deposit?')) return;
      
      // Remove from pending - permanently!
      pendingDeposits = pendingDeposits.filter(d => d.id !== id);
      localStorage.setItem('pendingDeposits', JSON.stringify(pendingDeposits));

      alert(`❌ Deposit rejected`);
      refreshDashboard();
    }

    // ========== PENDING WITHDRAWALS ==========
    function loadPendingWithdrawals() {
      const tbody = document.getElementById('pendingWithdrawalsBody');
      
      if (pendingWithdrawals.length === 0) {
        tbody.innerHTML = `
          <tr>
            <td colspan="7" style="text-align:center; padding:40px;">
              <div class="empty-state">
                <i class="fas fa-inbox"></i>
                <p>No pending withdrawals</p>
              </div>
            </td>
          </tr>`;
        return;
      }

      let html = '';
      pendingWithdrawals.forEach(withdrawal => {
        const user = users[withdrawal.userId] || {};
        html += `
          <tr>
            <td>${new Date(withdrawal.timestamp).toLocaleString()}</td>
            <td>${user.fullName || 'Unknown'}</td>
            <td>${withdrawal.phone || user.phone || 'N/A'}</td>
            <td><strong>${withdrawal.amount.toLocaleString()} UGX</strong></td>
            <td>${withdrawal.wallet || 'main'}</td>
            <td>${withdrawal.mobileNumber || 'N/A'}</td>
            <td>
              <button class="btn btn-approve" onclick="approveWithdrawal(${withdrawal.id})">
                <i class="fas fa-check"></i> Approve
              </button>
              <button class="btn btn-reject" onclick="rejectWithdrawal(${withdrawal.id})">
                <i class="fas fa-times"></i> Reject
              </button>
            </td>
          </tr>
        `;
      });
      
      tbody.innerHTML = html;
    }

    function approveWithdrawal(id) {
      if (!confirm('Approve this withdrawal?')) return;
      
      const withdrawal = pendingWithdrawals.find(w => w.id === id);
      if (!withdrawal) return;

      // Remove from pending - permanently!
      pendingWithdrawals = pendingWithdrawals.filter(w => w.id !== id);
      localStorage.setItem('pendingWithdrawals', JSON.stringify(pendingWithdrawals));

      alert(`✅ Withdrawal approved!`);
      refreshDashboard();
    }

    function rejectWithdrawal(id) {
      if (!confirm('Reject this withdrawal? Funds will be returned to user.')) return;
      
      const withdrawal = pendingWithdrawals.find(w => w.id === id);
      if (!withdrawal) return;

      // Refund the money back to user
      const user = users[withdrawal.userId];
      if (user) {
        if (withdrawal.wallet === 'main') {
          user.mainWallet = (user.mainWallet || 0) + withdrawal.amount;
        } else {
          user.commissionWallet = (user.commissionWallet || 0) + withdrawal.amount;
        }
        localStorage.setItem('cueUsers', JSON.stringify(users));
      }

      // Remove from pending - permanently!
      pendingWithdrawals = pendingWithdrawals.filter(w => w.id !== id);
      localStorage.setItem('pendingWithdrawals', JSON.stringify(pendingWithdrawals));

      alert(`❌ Withdrawal rejected and funds returned`);
      refreshDashboard();
    }

    // ========== MEMBERS MANAGEMENT ==========
    function loadAllMembers(searchTerm = '') {
      const tbody = document.getElementById('membersBody');
      const membersArray = Object.values(users);
      
      if (membersArray.length === 0) {
        tbody.innerHTML = `
          <tr>
            <td colspan="8" style="text-align:center; padding:40px;">
              <div class="empty-state">
                <i class="fas fa-users-slash"></i>
                <p>No members found</p>
              </div>
            </td>
          </tr>`;
        return;
      }

      // Filter by search term
      const filtered = membersArray.filter(user => 
        user.fullName?.toLowerCase().includes(searchTerm.toLowerCase()) ||
        user.phone?.includes(searchTerm)
      );

      if (filtered.length === 0) {
        tbody.innerHTML = `
          <tr>
            <td colspan="8" style="text-align:center; padding:40px;">
              <div class="empty-state">
                <i class="fas fa-search"></i>
                <p>No matching members found</p>
              </div>
            </td>
          </tr>`;
        return;
      }

      let html = '';
      filtered.forEach(user => {
        const daysLeft = user.memberExpiry ? 
          Math.ceil((new Date(user.memberExpiry) - new Date()) / (1000*60*60*24)) : 0;
        
        html += `
          <tr>
            <td><strong>${user.fullName || 'N/A'}</strong></td>
            <td>${user.phone || 'N/A'}</td>
            <td>${user.country || 'N/A'}</td>
            <td>${user.memberLevel === 0 ? 'Intern' : `Level ${user.memberLevel}`}</td>
            <td>${(user.mainWallet || 0).toLocaleString()} UGX</td>
            <td>${(user.commissionWallet || 0).toLocaleString()} UGX</td>
            <td>${daysLeft > 0 ? daysLeft + ' days' : 'Expired'}</td>
            <td>
              <button class="btn btn-edit" onclick="openEditModal('${user.phone}')">
                <i class="fas fa-edit"></i>
              </button>
              <button class="btn btn-reset" onclick="openResetModal('${user.phone}')">
                <i class="fas fa-key"></i>
              </button>
            </td>
          </tr>
        `;
      });
      
      tbody.innerHTML = html;
    }

    function searchMembers() {
      const searchTerm = document.getElementById('searchMember').value;
      loadAllMembers(searchTerm);
    }

    // ========== EDIT MEMBER ==========
    function openEditModal(phone) {
      const user = users[phone];
      if (!user) return;

      document.getElementById('editPhone').value = phone;
      document.getElementById('editFullName').value = user.fullName || '';
      document.getElementById('editNewPhone').value = phone;
      document.getElementById('editCountry').value = user.country || 'Uganda';
      document.getElementById('editLevel').value = user.memberLevel || 0;
      document.getElementById('editMainWallet').value = user.mainWallet || 0;
      document.getElementById('editCommissionWallet').value = user.commissionWallet || 0;

      document.getElementById('editModal').style.display = 'flex';
    }

    function closeEditModal() {
      document.getElementById('editModal').style.display = 'none';
    }

    function saveMemberChanges() {
      const oldPhone = document.getElementById('editPhone').value;
      const newPhone = document.getElementById('editNewPhone').value;
      const user = users[oldPhone];
      
      if (!user) return;

      // Update user data
      user.fullName = document.getElementById('editFullName').value;
      user.country = document.getElementById('editCountry').value;
      user.memberLevel = parseInt(document.getElementById('editLevel').value);
      user.mainWallet = parseFloat(document.getElementById('editMainWallet').value) || 0;
      user.commissionWallet = parseFloat(document.getElementById('editCommissionWallet').value) || 0;

      // Handle phone number change
      if (oldPhone !== newPhone) {
        users[newPhone] = user;
        delete users[oldPhone];
        
        // Update currentUser if needed
        if (localStorage.getItem('currentUser') === oldPhone) {
          localStorage.setItem('currentUser', newPhone);
        }
      }

      localStorage.setItem('cueUsers', JSON.stringify(users));
      
      alert('✅ Member information updated successfully!');
      closeEditModal();
      refreshDashboard();
    }

    // ========== RESET PASSWORD ==========
    function openResetModal(phone) {
      document.getElementById('resetPhone').value = phone;
      document.getElementById('newPassword').value = '123456';
      document.getElementById('resetModal').style.display = 'flex';
    }

    function closeResetModal() {
      document.getElementById('resetModal').style.display = 'none';
    }

    function resetPassword() {
      const phone = document.getElementById('resetPhone').value;
      const newPass = document.getElementById('newPassword').value;
      
      if (users[phone]) {
        users[phone].password = newPass;
        localStorage.setItem('cueUsers', JSON.stringify(users));
        alert(`✅ Password reset to "${newPass}" for ${users[phone].fullName}`);
        closeResetModal();
      }
    }

    // ========== REFRESH ==========
    function refreshDashboard() {
      // Reload all data from localStorage
      users = JSON.parse(localStorage.getItem('cueUsers')) || {};
      pendingDeposits = JSON.parse(localStorage.getItem('pendingDeposits')) || [];
      pendingWithdrawals = JSON.parse(localStorage.getItem('pendingWithdrawals')) || [];
      
      loadStats();
      loadPendingDeposits();
      loadPendingWithdrawals();
      loadAllMembers();
    }

    // ========== INIT ==========
    window.onload = function() {
      // Check if already logged in
      if (isAdminLoggedIn) {
        showDashboard();
      }
    };

    // Close modals when clicking outside
    window.onclick = function(event) {
      const editModal = document.getElementById('editModal');
      const resetModal = document.getElementById('resetModal');
      
      if (event.target === editModal) closeEditModal();
      if (event.target === resetModal) closeResetModal();
    };
  </script>
</body>
</html>
