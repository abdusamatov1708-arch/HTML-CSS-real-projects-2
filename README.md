# HTML-CSS-real-projects-2
HTMK
<!DOCTYPE html>
<html lang="uz">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Admin Dashboard</title>
    <!-- FontAwesome iconlari uchun -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        /* Umumiy sozlamalar */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        :root {
            --bg-color: #f8fafc;
            --sidebar-bg: #1e293b;
            --sidebar-color: #94a3b8;
            --sidebar-hover: #334155;
            --sidebar-active: #3b82f6;
            --text-main: #1e293b;
            --text-light: #64748b;
            --white: #ffffff;
            --border-color: #e2e8f0;
            --primary: #3b82f6;
            --success: #10b981;
            --warning: #f59e0b;
            --danger: #ef4444;
        }

        body {
            background-color: var(--bg-color);
            color: var(--text-main);
        }

        /* 5. CSS Grid bilan 2 ustunli layout */
        .admin-layout {
            display: grid;
            grid-template-columns: 260px 1fr;
            min-height: 100vh;
        }

        /* 1. Sticky Sidebar */
        .sidebar {
            position: sticky;
            top: 0;
            height: 100vh;
            background-color: var(--sidebar-bg);
            color: var(--sidebar-color);
            display: flex;
            flex-direction: column;
            justify-content: space-between;
            padding: 20px;
            transition: all 0.3s ease;
            z-index: 100;
        }

        .sidebar-logo {
            font-size: 1.25rem;
            font-weight: bold;
            color: var(--white);
            display: flex;
            align-items: center;
            gap: 10px;
            padding-bottom: 20px;
            border-bottom: 1px solid #334155;
        }

        .sidebar-logo i {
            color: var(--primary);
        }

        .sidebar-nav {
            list-style: none;
            margin-top: 20px;
            display: flex;
            flex-direction: column;
            gap: 8px;
            flex-grow: 1;
        }

        .sidebar-nav a {
            display: flex;
            align-items: center;
            gap: 12px;
            padding: 12px 15px;
            color: var(--sidebar-color);
            text-decoration: none;
            border-radius: 8px;
            transition: 0.2s;
        }

        .sidebar-nav a:hover, .sidebar-nav a.active {
            background-color: var(--sidebar-hover);
            color: var(--white);
        }

        .sidebar-nav a.active {
            background-color: var(--sidebar-active);
        }

        .sidebar-profile {
            display: flex;
            align-items: center;
            gap: 12px;
            padding-top: 15px;
            border-top: 1px solid #334155;
        }

        .sidebar-profile img {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            object-fit: cover;
        }

        .profile-info h4 {
            font-size: 0.9rem;
            color: var(--white);
        }

        .profile-info p {
            font-size: 0.75rem;
            color: var(--sidebar-color);
        }

        /* Asosiy kontent qismi */
        .main-content {
            display: flex;
            flex-direction: column;
        }

        /* 2. Top Header */
        .top-header {
            background-color: var(--white);
            padding: 15px 30px;
            display: flex;
            align-items: center;
            justify-content: space-between;
            border-bottom: 1px solid var(--border-color);
            position: sticky;
            top: 0;
            z-index: 99;
        }

        .header-title h2 {
            font-size: 1.4rem;
            color: var(--text-main);
        }

        .header-search {
            position: relative;
            width: 300px;
        }

        .header-search input {
            width: 100%;
            padding: 10px 15px 10px 40px;
            border: 1px solid var(--border-color);
            border-radius: 8px;
            outline: none;
            font-size: 0.9rem;
            background-color: var(--bg-color);
        }

        .header-search i {
            position: absolute;
            left: 15px;
            top: 50%;
            transform: translateY(-50%);
            color: var(--text-light);
        }

        .header-actions {
            display: flex;
            align-items: center;
            gap: 20px;
        }

        .notification-icon {
            position: relative;
            font-size: 1.2rem;
            color: var(--text-light);
            cursor: pointer;
        }

        .notification-icon .badge {
            position: absolute;
            top: -5px;
            right: -5px;
            background-color: var(--danger);
            color: var(--white);
            font-size: 0.65rem;
            padding: 2px 5px;
            border-radius: 50%;
        }

        /* Dashboard tanasi */
        .dashboard-body {
            padding: 30px;
            display: flex;
            flex-direction: column;
            gap: 30px;
        }

        /* 3. Stats Kartalar */
        .stats-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
            gap: 20px;
        }

        .stat-card {
            background-color: var(--white);
            padding: 20px;
            border-radius: 12px;
            border: 1px solid var(--border-color);
            display: flex;
            align-items: center;
            gap: 20px;
        }

        .stat-icon {
            width: 55px;
            height: 55px;
            border-radius: 10px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.5rem;
        }

        .stat-icon.users { background-color: #dbeafe; color: #3b82f6; }
        .stat-icon.revenue { background-color: #d1fae5; color: #10b981; }
        .stat-icon.orders { background-color: #fef3c7; color: #f59e0b; }
        .stat-icon.growth { background-color: #fee2e2; color: #ef4444; }

        .stat-info p {
            font-size: 0.85rem;
            color: var(--text-light);
            margin-bottom: 5px;
        }

        .stat-info h3 {
            font-size: 1.5rem;
            font-weight: 700;
            margin-bottom: 5px;
        }

        .stat-info span {
            font-size: 0.75rem;
            font-weight: 600;
        }

        .trend.positive { color: var(--success); }
        .trend.negative { color: var(--danger); }

        /* 4. Data Table */
        .table-container {
            background-color: var(--white);
            border-radius: 12px;
            border: 1px solid var(--border-color);
            padding: 20px;
            overflow-x: auto;
        }

        .table-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
        }

        .table-header h3 {
            font-size: 1.1rem;
        }

        .btn-add {
            background-color: var(--primary);
            color: var(--white);
            border: none;
            padding: 8px 16px;
            border-radius: 6px;
            cursor: pointer;
            font-size: 0.9rem;
            transition: 0.2s;
        }

        .btn-add:hover {
            background-color: #2563eb;
        }

        table {
            width: 100%;
            border-collapse: collapse;
            text-align: left;
        }

        th, td {
            padding: 12px 15px;
            border-bottom: 1px solid var(--border-color);
            font-size: 0.9rem;
        }

        th {
            color: var(--text-light);
            font-weight: 600;
            background-color: #f8fafc;
        }

        tbody tr:hover {
            background-color: #f1f5f9;
        }

        /* Status Badge */
        .status {
            padding: 5px 10px;
            border-radius: 20px;
            font-size: 0.75rem;
            font-weight: 600;
            display: inline-block;
        }

        .status.active { background-color: #d1fae5; color: #065f46; }
        .status.pending { background-color: #fef3c7; color: #92400e; }
        .status.cancelled { background-color: #fee2e2; color: #991b1b; }

        /* 6. Responsive — Mobil qurilmalar uchun */
        @media (max-width: 768px) {
            .admin-layout {
                grid-template-columns: 1fr;
            }
            .sidebar {
                display: none; /* Kichik ekranlarda sidebar yashiriladi */
            }
            .header-search {
                width: 180px;
            }
            .dashboard-body {
                padding: 15px;
            }
        }
    </style>
</head>
<body>

    <div class="admin-layout">
        <!-- 1. Sticky Sidebar -->
        <aside class="sidebar">
            <div class="sidebar-logo">
                <i class="fas fa-cube"></i>
                <span>AdminPanel</span>
            </div>
            <ul class="sidebar-nav">
                <li><a href="#" class="active"><i class="fas fa-home"></i> Asosiy</a></li>
                <li><a href="#"><i class="fas fa-users"></i> Foydalanuvchilar</a></li>
                <li><a href="#"><i class="fas fa-box"></i> Buyurtmalar</a></li>
                <li><a href="#"><i class="fas fa-chart-line"></i> Statistika</a></li>
                <li><a href="#"><i class="fas fa-cog"></i> Sozlamalar</a></li>
            </ul>
            <div class="sidebar-profile">
                <img src="https://images.unsplash.com/photo-1534528741775-53994a69daeb?w=100" alt="Foydalanuvchi">
                <div class="profile-info">
                    <h4>Madina</h4>
                    <p>Boshqaruvchi</p>
                </div>
            </div>
        </aside>

        <!-- Asosiy qism -->
        <main class="main-content">
            <!-- 2. Top Header -->
            <header class="top-header">
                <div class="header-title">
                    <h2>Boshqaruv Paneli</h2>
                </div>
                <div class="header-search">
                    <i class="fas fa-search"></i>
                    <input type="text" placeholder="Qidirish...">
                </div>
                <div class="header-actions">
                    <div class="notification-icon">
                        <i class="fas fa-bell"></i>
                        <span class="badge">3</span>
                    </div>
                </div>
            </header>

            <!-- Dashboard Kontenti -->
            <div class="dashboard-body">
                <!-- 3. Stats Kartalar (4 ta ko'rsatkich) -->
                <div class="stats-grid">
                    <div class="stat-card">
                        <div class="stat-icon users">
                            <i class="fas fa-users"></i>
                        </div>
                        <div class="stat-info">
                            <p>Foydalanuvchilar</p>
                            <h3>12,450</h3>
                            <span class="trend positive">+12% oxirgi oy</span>
                        </div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-icon revenue">
                            <i class="fas fa-wallet"></i>
                        </div>
                        <div class="stat-info">
                            <p>Daromad</p>
                            <h3>$34,200</h3>
                            <span class="trend positive">+8.4% o'sish</span>
                        </div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-icon orders">
                            <i class="fas fa-shopping-bag"></i>
                        </div>
                        <div class="stat-info">
                            <p>Buyurtmalar</p>
                            <h3>1,280</h3>
                            <span class="trend negative">-2.1% pasayish</span>
                        </div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-icon growth">
                            <i class="fas fa-chart-pie"></i>
                        </div>
                        <div class="stat-info">
                            <p>Umumiy o'sish</p>
                            <h3>24.8%</h3>
                            <span class="trend positive">+4.3% barqaror</span>
                        </div>
                    </div>
                </div>

                <!-- 4. Data Table (Jadval va Status Badge) -->
                <div class="table-container">
                    <div class="table-header">
                        <h3>Oxirgi buyurtmalar ro'yxati</h3>
                        <button class="btn-add"><i class="fas fa-plus"></i> Yangi qo'shish</button>
                    </div>
                    <table>
                        <thead>
                            <tr>
                                <th>ID</th>
                                <th>Mijoz</th>
                                <th>Mahsulot</th>
                                <th>Sana</th>
                                <th>Status</th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr>
                                (#1023) <td>#1023</td>
                                <td>Alisher Navoiy</td>
                               <td>Smartfon X12 Pro</td>
                                <td>20.08.2026</td>
                                <td><span class="status active">Tugallangan</span></td>
                            </tr>
                            <tr>
                                <td>#1024</td>
                                <td>Zulayho Rahimova</td>
                                <td>Noutbuk Air 14</td>
                                <td>19.08.2026</td>
                                <td><span class="status pending">Kutilmoqda</span></td>
                            </tr>
                            <tr>
                                <td>#1025</td>
                                <td>Jasurbek Umarov</td>
                                <td>Bluetooth Naushnik</td>
                                <td>18.08.2026</td>
                                <td><span class="status cancelled">Bekor qilingan</span></td>
                            </tr>
                            <tr>
                                <td>#1026</td>
                                <td>Nigora Saidova</td>
                                <td>Smart Soat S2</td>
                                <td>17.08.2026</td>
                                <td><span class="status active">Tugallangan</span></td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </div>
        </main>
    </div>

</body>
</html>
