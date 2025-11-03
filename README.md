<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>FRIENDLY GOLF TOUR</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Noto+Sans+KR:wght@400;700;900&family=Inter:wght@400;700;900&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Inter', 'Noto Sans KR', sans-serif;
            background-color: #121212;
            color: #E0E0E0;
        }
        .nav-link {
            transition: all 0.3s ease;
            cursor: pointer;
        }
        .nav-link:hover, .nav-link.active {
            color: #10B981; /* Emerald-500 */
            border-bottom: 2px solid #10B981;
        }
        .section {
            display: none;
            animation: fadeIn 0.5s ease;
        }
        .section.active {
            display: block;
        }
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }
        .team-card, .player-card, .admin-card {
            background-color: #1E1E1E;
            border: 1px solid #333;
            transition: transform 0.3s ease, box-shadow 0.3s ease;
        }
        .team-card:hover, .player-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 15px -3px rgba(16, 185, 129, 0.1), 0 4px 6px -2px rgba(16, 185, 129, 0.05);
        }
        .btn-primary {
            background-color: #10B981;
            color: #FFFFFF;
            font-weight: bold;
            transition: background-color 0.3s ease;
        }
        .btn-primary:hover {
            background-color: #059669;
        }
        .btn-secondary {
            background-color: #374151;
            color: #FFFFFF;
            font-weight: bold;
            transition: background-color 0.3s ease;
        }
        .btn-secondary:hover {
            background-color: #4B5563;
        }
        .modal {
            transition: opacity 0.3s ease;
        }
        .table-header {
            background-color: #333;
            color: #E0E0E0;
        }
        .table-row-dark {
            background-color: #1E1E1E;
        }
        .table-row-light {
             background-color: #242424;
        }
        /* Admin Form Styles */
        .form-input, .form-select {
            background-color: #333;
            border: 1px solid #555;
            color: #E0E0E0;
            border-radius: 0.375rem; /* rounded-md */
            padding: 0.5rem 0.75rem;
            width: 100%;
        }
        .form-input:focus, .form-select:focus {
            outline: none;
            border-color: #10B981;
            box-shadow: 0 0 0 2px rgba(16, 185, 129, 0.5);
        }
        .form-label {
            display: block;
            margin-bottom: 0.5rem;
            font-weight: 600;
        }
        /* Hole score input style */
        .hole-score-input {
            padding: 0.5rem;
            text-align: center;
        }
        /* Scorecard table style */
        .scorecard-table th, .scorecard-table td {
            border: 1px solid #444;
            padding: 0.5rem 0.25rem;
            text-align: center;
            min-width: 30px;
        }
        /* Admin Tab Style */
        .admin-tab {
            transition: color 0.2s, border-color 0.2s;
            border-bottom: 2px solid transparent;
        }
        .admin-tab.active {
            color: #10B981;
            border-bottom-color: #10B981;
        }
    </style>
</head>
<body class="antialiased">

    <!-- Header & Navigation -->
    <header class="bg-black/80 backdrop-blur-sm sticky top-0 z-50">
        <nav class="container mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex items-center justify-between h-16">
                <div class="flex-shrink-0">
                    <h1 class="text-2xl font-black text-white tracking-tighter">FRIENDLY GOLF TOUR</h1>
                </div>
                <div class="hidden md:block">
                    <div class="ml-10 flex items-baseline space-x-4">
                        <a class="nav-link active px-3 py-2 text-sm font-bold" data-target="home">HOME</a>
                        <a class="nav-link px-3 py-2 text-sm font-bold" data-target="teams">TEAMS</a>
                        <a class="nav-link px-3 py-2 text-sm font-bold" data-target="players">PLAYERS</a>
                        <a class="nav-link px-3 py-2 text-sm font-bold" data-target="standings">STANDINGS</a>
                        <a class="nav-link px-3 py-2 text-sm font-bold" data-target="rules">RULES</a>
                        <a class="nav-link px-3 py-2 text-sm font-bold text-red-400 hover:text-red-300" data-target="admin">ADMIN</a>
                    </div>
                </div>
                <div class="md:hidden">
                    <button id="mobile-menu-button" class="text-white hover:text-emerald-400 focus:outline-none">
                        <svg class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16m-7 6h7" />
                        </svg>
                    </button>
                </div>
            </div>
        </nav>
        <!-- Mobile Menu -->
        <div id="mobile-menu" class="md:hidden hidden">
            <a class="nav-link block px-3 py-2 text-base font-medium" data-target="home">HOME</a>
            <a class="nav-link block px-3 py-2 text-base font-medium" data-target="teams">TEAMS</a>
            <a class="nav-link block px-3 py-2 text-base font-medium" data-target="players">PLAYERS</a>
            <a class="nav-link block px-3 py-2 text-base font-medium" data-target="standings">STANDINGS</a>
            <a class="nav-link block px-3 py-2 text-base font-medium" data-target="rules">RULES</a>
            <a class="nav-link block px-3 py-2 text-base font-medium text-red-400" data-target="admin">ADMIN</a>
        </div>
    </header>

    <main class="container mx-auto px-4 sm:px-6 lg:px-8 py-8">

        <!-- Home Section -->
        <section id="home" class="section active">
             <!-- Home Banner Container: This will be filled by renderHome() -->
             <div id="home-banner-container" class="relative text-center rounded-lg overflow-hidden min-h-[250px] bg-[#1E1E1E]">
                <!-- Content injected by JS -->
             </div>
            
            <div class="mt-12">
                <h3 class="text-3xl font-bold text-center mb-8">LEAGUE TEAMS</h3>
                <div class="grid md:grid-cols-3 gap-8" id="home-teams">
                    <!-- Team cards will be injected here by JS -->
                </div>
            </div>

            <div class="mt-16">
                 <h3 class="text-3xl font-bold text-center mb-8">RECENT MATCH</h3>
                 <div class="max-w-3xl mx-auto bg-[#1E1E1E] border border-gray-700 rounded-lg p-8" id="recent-match-container">
                    <!-- Recent Match will be injected here by JS -->
                 </div>
            </div>
        </section>

        <!-- Teams Section -->
        <section id="teams" class="section">
            <h2 class="text-4xl font-extrabold text-center mb-12">TEAMS</h2>
            <div class="space-y-16" id="team-details">
                <!-- Team details will be injected here by JS -->
            </div>
        </section>

        <!-- Players Section -->
        <section id="players" class="section">
            <h2 class="text-4xl font-extrabold text-center mb-12">PLAYERS</h2>
            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6" id="player-profiles">
                <!-- Player profiles will be injected by JS -->
            </div>
        </section>

        <!-- Standings Section -->
        <section id="standings" class="section">
             <h2 class="text-4xl font-extrabold text-center mb-12">STANDINGS & RESULTS</h2>
             <div id="team-standings-container"></div>
             <div id="player-scores-container" class="mt-12"></div>
        </section>

        <!-- Rules Section -->
        <section id="rules" class="section">
            <div class="max-w-4xl mx-auto">
                <h2 class="text-4xl font-extrabold text-center mb-12">LEAGUE RULES</h2>
                <div class="bg-[#1E1E1E] border border-gray-700 rounded-lg p-8 space-y-6 text-gray-300">
                    <div>
                        <h3 class="text-2xl font-bold text-emerald-400 mb-2">기본 룰: 오장 (Oh-Jang)</h3>
                        <p>모든 매치는 '오장' 룰을 기본으로 합니다. 이는 5,000원빵을 의미하며, 각 홀마다 승부를 가려 정산하는 방식입니다.</p>
                    </div>
                     <div>
                        <h3 class="text-2xl font-bold text-emerald-400 mb-2">타이트한 대회 룰</h3>
                        <p>본 리그는 친목 도모를 목적으로 하지만, 공정한 승부를 위해 매우 엄격한 골프 룰을 적용합니다. 이로 인해 평소보다 타수가 더 많이 나올 수 있습니다.</p>
                    </div>
                    <div>
                        <h3 class="text-2xl font-bold text-emerald-400 mb-2">주요 특징</h3>
                        <ul class="list-disc list-inside space-y-2 pl-4">
                            <li><strong>컨시드 (Gimmies)</strong>: 퍼터 그립 끝(흑갈치) 안쪽 거리는 컨시드(OK)로 인정합니다.</li>
                            <li><strong>엄격한 룰 적용</strong>: OB, 해저드 등 모든 상황에 대해 정식 룰에 따른 벌타를 부과합니다.</li>
                            <li><strong>스코어카드 상호 확인</strong>: 라운드 종료 후 각 플레이어는 스코어카드를 상호 확인하고 서명합니다.</li>
                        </ul>
                    </div>
                </div>
            </div>
        </section>

        <!-- Admin Section -->
        <section id="admin" class="section">
            <h2 class="text-4xl font-extrabold text-center mb-12">ADMIN PANEL</h2>

            <!-- Admin Login -->
            <div id="admin-login" class="max-w-md mx-auto admin-card rounded-lg p-8">
                <h3 class="text-2xl font-bold text-center mb-6">관리자 로그인</h3>
                <div class="space-y-4">
                    <div>
                        <label for="password" class="form-label">비밀번호</label>
                        <input type="password" id="password" class="form-input" placeholder="Enter password">
                    </div>
                    <button id="login-button" class="btn-primary w-full py-2 rounded-md">로그인</button>
                    <p id="login-error" class="text-red-400 text-sm text-center hidden">비밀번호가 틀렸습니다.</p>
                </div>
            </div>

            <!-- Admin Panel (Initially hidden by 'hidden' class) -->
            <div id="admin-panel" class="hidden">
                <p class="text-center text-emerald-400 mb-6">관리자님, 환영합니다.</p>
                
                <!-- Admin Tabs -->
                <div class="flex flex-wrap justify-center border-b border-gray-700 mb-6">
                    <button class="admin-tab active py-2 px-4 font-bold" data-target="admin-score">스코어카드 입력</button>
                    <button class="admin-tab py-2 px-4 font-bold text-gray-500" data-target="admin-match">팀 매치 입력</button>
                    <button class="admin-tab py-2 px-4 font-bold text-gray-500" data-target="admin-player">선수 정보 수정</button>
                    <button class="admin-tab py-2 px-4 font-bold text-gray-500" data-target="admin-settings">사이트 설정</button>
                </div>

                <!-- Admin Tab Content: Add Score -->
                <div id="admin-score" class="admin-tab-content active">
                    <div class="admin-card rounded-lg p-6 max-w-3xl mx-auto">
                        <h3 class="text-xl font-bold mb-4">18홀 스코어카드 추가</h3>
                        <form id="add-score-form" class="space-y-4">
                            <div class="grid md:grid-cols-3 gap-4">
                                <div class="md:col-span-1">
                                    <label for="score-player" class="form-label">선수 선택</label>
                                    <select id="score-player" class="form-select"></select>
                                </div>
                                <div class="md:col-span-1">
                                    <label for="score-course" class="form-label">골프장</label>
                                    <input type="text" id="score-course" class="form-input" placeholder="예: Namseoul CC" required>
                                </div>
                                 <div class="md:col-span-1">
                                    <label for="score-date" class="form-label">날짜</label>
                                    <input type="date" id="score-date" class="form-input" required>
                                </div>
                            </div>
                            
                            <!-- 18 Hole Inputs -->
                            <div>
                                <h4 class="text-lg font-semibold mt-4 mb-2">Hole Scores</h4>
                                <div class="p-4 bg-gray-900/50 rounded-lg">
                                    <h5 class="text-sm font-bold text-gray-400">FRONT 9</h5>
                                    <div class="grid grid-cols-9 gap-2 mt-2">
                                        <input type="number" class="form-input hole-score-input hole-score" placeholder="H1" min="1" max="15" required>
                                        <input type="number" class="form-input hole-score-input hole-score" placeholder="H2" min="1" max="15" required>
                                        <input type="number" class="form-input hole-score-input hole-score" placeholder="H3" min="1" max="15" required>
                                        <input type="number" class="form-input hole-score-input hole-score" placeholder="H4" min="1" max="15" required>
                                        <input type="number" class="form-input hole-score-input hole-score" placeholder="H5" min="1" max="15" required>
                                        <input type="number" class="form-input hole-score-input hole-score" placeholder="H6" min="1" max="15" required>
                                        <input type="number" class="form-input hole-score-input hole-score" placeholder="H7" min="1" max="15" required>
                                        <input type="number" class="form-input hole-score-input hole-score" placeholder="H8" min="1" max="15" required>
                                        <input type="number" class="form-input hole-score-input hole-score" placeholder="H9" min="1" max="15" required>
                                    </div>
                                    <h5 class="text-sm font-bold text-gray-400 mt-4">BACK 9</h5>
                                    <div class="grid grid-cols-9 gap-2 mt-2">
                                        <input type="number" class="form-input hole-score-input hole-score" placeholder="H10" min="1" max="15" required>
                                        <input type="number" class="form-input hole-score-input hole-score" placeholder="H11" min="1" max="15" required>
                                        <input type="number" class="form-input hole-score-input hole-score" placeholder="H12" min="1" max="15" required>
                                        <input type="number" class="form-input hole-score-input hole-score" placeholder="H13" min="1" max="15" required>
                                        <input type="number" class="form-input hole-score-input hole-score" placeholder="H14" min="1" max="15" required>
                                        <input type="number" class="form-input hole-score-input hole-score" placeholder="H15" min="1" max="15" required>
                                        <input type="number" class="form-input hole-score-input hole-score" placeholder="H16" min="1" max="15" required>
                                        <input type="number" class="form-input hole-score-input hole-score" placeholder="H17" min="1" max="15" required>
                                        <input type="number" class="form-input hole-score-input hole-score" placeholder="H18" min="1" max="15" required>
                                    </div>
                                </div>
                            </div>
                            
                            <div class="flex justify-between items-center pt-4">
                                <h3 class="text-2xl font-bold">Total: <span id="score-total" class="text-emerald-400">0</span></h3>
                                <button type="submit" class="btn-primary py-2 px-6 rounded-md">스코어카드 저장</button>
                            </div>
                        </form>
                    </div>
                </div>

                <!-- Admin Tab Content: Add Match -->
                <div id="admin-match" class="admin-tab-content hidden">
                    <div class="admin-card rounded-lg p-6 max-w-lg mx-auto">
                        <h3 class="text-xl font-bold mb-4">팀 매치 결과 추가</h3>
                        <form id="add-match-form" class="space-y-4">
                            <div class="grid grid-cols-2 gap-4">
                                <div>
                                    <label for="match-team1" class="form-label">Team 1</label>
                                    <select id="match-team1" class="form-select"></select>
                                </div>
                                <div>
                                    <label for="match-score1" class="form-label">Score 1</label>
                                    <input type="number" id="match-score1" class="form-input" value="0" min="0">
                                </div>
                            </div>
                            <div class="grid grid-cols-2 gap-4">
                                <div>
                                    <label for="match-team2" class="form-label">Team 2</label>
                                    <select id="match-team2" class="form-select"></select>
                                </div>
                                <div>
                                    <label for="match-score2" class="form-label">Score 2</label>
                                    <input type="number" id="match-score2" class="form-input" value="0" min="0">
                                </div>
                            </div>
                            <button type="submit" class="btn-primary w-full py-2 rounded-md">매치 결과 저장</button>
                        </form>
                    </div>
                </div>

                <!-- Admin Tab Content: Edit Player -->
                <div id="admin-player" class="admin-tab-content hidden">
                    <div class="admin-card rounded-lg p-6 max-w-lg mx-auto">
                        <h3 class="text-xl font-bold mb-4">선수 정보 수정</h3>
                        <form id="edit-player-form" class="space-y-4">
                             <div>
                                <label for="edit-player-select" class="form-label">선수 선택</label>
                                <select id="edit-player-select" class="form-select"></select>
                            </div>
                            <div>
                                <label for="edit-player-image" class="form-label">프로필 사진 URL</label>
                                <input type="text" id="edit-player-image" class="form-input" placeholder="https://...">
                            </div>
                            <div>
                                <label for="edit-player-video" class="form-label">스윙 영상 URL</label>
                                <input type="text" id="edit-player-video" class="form-input" placeholder="https://...">
                            </div>
                            <div>
                                <label for="edit-player-feature" class="form-label">특징</label>
                                <input type="text" id="edit-player-feature" class="form-input" placeholder="예: Power Hitter">
                            </div>
                            <button type="submit" class="btn-primary w-full py-2 rounded-md">선수 정보 수정</button>
                        </form>
                    </div>
                </div>
                
                <!-- Admin Tab Content: Site Settings -->
                <div id="admin-settings" class="admin-tab-content hidden">
                    <!-- Home Background -->
                    <div class="admin-card rounded-lg p-6 max-w-lg mx-auto mb-6">
                        <h3 class="text-xl font-bold mb-4">메인 홈 배경 설정</h3>
                        <form id="edit-home-bg-form" class="space-y-4">
                            <div>
                                <label for="setting-bg-type" class="form-label">배경 타입</label>
                                <select id="setting-bg-type" class="form-select">
                                    <option value="image">이미지</option>
                                    <option value="video">동영상</option>
                                </select>
                            </div>
                            <div>
                                <label for="setting-bg-url" class="form-label">미디어 URL (이미지 또는 동영상)</label>
                                <input type="text" id="setting-bg-url" class="form-input" placeholder="https://...">
                            </div>
                            <button type="submit" class="btn-primary w-full py-2 rounded-md">홈 배경 저장</button>
                        </form>
                    </div>
                    
                    <!-- Team Logos -->
                    <div class="admin-card rounded-lg p-6 max-w-lg mx-auto">
                        <h3 class="text-xl font-bold mb-4">팀 로고 수정</h3>
                        <form id="edit-team-logo-form" class="space-y-4">
                            <div>
                                <label for="setting-team-select" class="form-label">팀 선택</label>
                                <select id="setting-team-select" class="form-select"></select>
                            </div>
                            <div>
                                <label for="setting-team-logo-url" class="form-label">새 로고 URL</label>
                                <input type="text" id="setting-team-logo-url" class="form-input" placeholder="https://...">
                            </div>
                            <div>
                                <label class="form-label">현재 로고 미리보기</label>
                                <img id="setting-team-logo-preview" src="" alt="Logo Preview" class="w-24 h-24 object-contain bg-gray-700 rounded-md">
                            </div>
                            <button type="submit" class="btn-primary w-full py-2 rounded-md">팀 로고 저장</button>
                        </form>
                    </div>
                </div>

                 <div class="mt-8 text-center">
                    <button id="reset-data-button" class="btn-secondary py-2 px-4 rounded-md text-sm text-red-400">데이터 초기화 (주의)</button>
                    <p class="text-xs text-gray-500 mt-2">모든 스코어와 매치 기록, 사이트 설정을 초기화합니다.</p>
                </div>
            </div>
        </section>
    </main>
    
    <!-- Swing Video Modal -->
    <div id="video-modal" class="modal fixed inset-0 bg-black bg-opacity-80 flex items-center justify-center z-50 hidden">
        <div class="bg-[#1E1E1E] rounded-lg w-11/12 max-w-4xl p-4 relative">
            <button class="close-modal-btn absolute top-4 right-4 text-white text-2xl">&times;</button>
            <h3 id="modal-player-name" class="text-2xl font-bold mb-4"></h3>
            <div class="aspect-w-16 aspect-h-9">
                <video id="swing-video" controls class="w-full rounded" src=""></video>
            </div>
        </div>
    </div>
    
    <!-- Scorecard Modal -->
    <div id="scorecard-modal" class="modal fixed inset-0 bg-black bg-opacity-80 flex items-center justify-center z-50 hidden">
        <div class="bg-[#1E1E1E] rounded-lg w-11/12 max-w-4xl p-4 relative border border-gray-700">
            <button class="close-modal-btn absolute top-4 right-4 text-white text-2xl">&times;</button>
            <h3 id="scorecard-player-name" class="text-2xl font-bold mb-4"></h3>
            <div id="scorecard-content" class="max-h-[70vh] overflow-y-auto pr-2">
                <!-- Scorecards will be injected here -->
            </div>
        </div>
    </div>

    <!-- Global Message -->
    <div id="global-message" class="hidden fixed bottom-5 right-5 bg-emerald-500 text-white py-3 px-6 rounded-lg shadow-lg z-50">
        저장되었습니다!
    </div>

<script>
    // --- ADMIN PASSWORD ---
    const ADMIN_PASSWORD = 'fgtadmin'; // 관리자 비밀번호

    // --- DATABASE KEYS ---
    const DB_KEYS = {
        teams: 'fgt_teams',
        players: 'fgt_players',
        standings: 'fgt_standings',
        settings: 'fgt_site_settings' // New key for site settings
    };

    // --- DEFAULT (INITIAL) DATA ---
    const DEFAULT_TEAMS = [
        {
            id: 'amsagolf',
            name: 'AMSAGOLF',
            logo: 'https://i.imgur.com/Kq25T0p.png',
            description: '서울 강동 지역을 중심으로 편성된 팀. 평균 비거리 230미터 이상을 자랑하는 파워 히터들의 집합체입니다.',
            region: '서울 강동',
            feature: '평균 비거리 230m+',
            players: ['용성민', '박신형', '이준우', '우동준']
        },
        {
            id: 'gwangnam',
            name: 'GWANGNAM',
            logo: 'https://i.imgur.com/xO4bV9S.png',
            description: '광교, 강남 지역의 친목 골프팀. 팀의 주축을 이루는 장타자들이 경기를 압도합니다.',
            region: '광교, 강남',
            feature: '장타 군단',
            players: ['이형준', '박종률', '최광일', '김종경']
        },
        {
            id: 'ssg',
            name: 'SSG',
            logo: 'https://i.imgur.com/e5kPq3A.png',
            description: '강북, 강서 지역의 친목팀. 싱글 플레이어 진흥수를 중심으로 단단한 숏게임을 보유하고 있는 강팀입니다.',
            region: '강북, 강서',
            feature: '견고한 숏게임',
            players: ['진흥수', '채태식', '권우성', '한태준']
        }
    ];

    const DEFAULT_PLAYER_IMAGE = 'https://placehold.co/80x80/718096/E0E0E0?text=No+Img';
    const DEFAULT_PLAYER_VIDEO = 'https://assets.mixkit.co/videos/preview/mixkit-golf-player-hitting-the-ball-3039-large.mp4';

    const DEFAULT_PLAYERS = [
        { name: '용성민', team: 'AMSAGOLF', role: 'Captain', feature: 'Power Hitter', scores: [], swingVideo: DEFAULT_PLAYER_VIDEO, imageUrl: DEFAULT_PLAYER_IMAGE },
        { name: '박신형', team: 'AMSAGOLF', role: 'Player', feature: 'Consistent Driver', scores: [], swingVideo: DEFAULT_PLAYER_VIDEO, imageUrl: DEFAULT_PLAYER_IMAGE },
        { name: '이준우', team: 'AMSAGOLF', role: 'Player', feature: 'Putting Master', scores: [], swingVideo: DEFAULT_PLAYER_VIDEO, imageUrl: DEFAULT_PLAYER_IMAGE },
        { name: '우동준', team: 'AMSAGOLF', role: 'Player', feature: 'Aggressive Play', scores: [], swingVideo: DEFAULT_PLAYER_VIDEO, imageUrl: DEFAULT_PLAYER_IMAGE },
        { name: '이형준', team: 'GWANGNAM', role: 'Captain', feature: 'Long Hitter', scores: [], swingVideo: DEFAULT_PLAYER_VIDEO, imageUrl: DEFAULT_PLAYER_IMAGE },
        { name: '박종률', team: 'GWANGNAM', role: 'Player', feature: 'Strategic Player', scores: [], swingVideo: DEFAULT_PLAYER_VIDEO, imageUrl: DEFAULT_PLAYER_IMAGE },
        { name: '최광일', team: 'GWANGNAM', role: 'Player', feature: 'Long Hitter', scores: [], swingVideo: DEFAULT_PLAYER_VIDEO, imageUrl: DEFAULT_PLAYER_IMAGE },
        { name: '김종경', team: 'GWANGNAM', role: 'Player', feature: 'Long Hitter', scores: [], swingVideo: DEFAULT_PLAYER_VIDEO, imageUrl: DEFAULT_PLAYER_IMAGE },
        { name: '진흥수', team: 'SSG', role: 'Captain', feature: 'Single Player', scores: [], swingVideo: DEFAULT_PLAYER_VIDEO, imageUrl: DEFAULT_PLAYER_IMAGE },
        { name: '채태식', team: 'SSG', role: 'Player', feature: 'Short Game Specialist', scores: [], swingVideo: DEFAULT_PLAYER_VIDEO, imageUrl: DEFAULT_PLAYER_IMAGE },
        { name: '권우성', team: 'SSG', role: 'Player', feature: 'Iron Master', scores: [], swingVideo: DEFAULT_PLAYER_VIDEO, imageUrl: DEFAULT_PLAYER_IMAGE },
        { name: '한태준', team: 'SSG', role: 'Player', feature: 'Clutch Player', scores: [], swingVideo: DEFAULT_PLAYER_VIDEO, imageUrl: DEFAULT_PLAYER_IMAGE },
    ];

    const DEFAULT_STANDINGS = [
        { t1: 'amsagolf', s1: 2, t2: 'ssg', s2: 0, date: new Date().toISOString().split('T')[0] }
    ];

    // New Default Settings
    const DEFAULT_SETTINGS = {
        backgroundType: 'image',
        backgroundUrl: 'https://placehold.co/1200x400/1E1E1E/10B981?text=Friendly+Golf+Tour'
    };

    // --- APP CLASS ---
    class GolfLeagueApp {
        constructor() {
            this.teams = [];
            this.players = [];
            this.standings = [];
            this.settings = {}; // New settings object
            this.isAdminLoggedIn = false;
        }

        init() {
            this.loadData();
            this.setupNavigation();
            this.setupModals();
            this.setupAdmin();
            this.renderAll();
            this.showSection('home');
        }

        // --- Data Management ---
        loadData() {
            const teams = localStorage.getItem(DB_KEYS.teams);
            const players = localStorage.getItem(DB_KEYS.players);
            const standings = localStorage.getItem(DB_KEYS.standings);
            const settings = localStorage.getItem(DB_KEYS.settings); // Load settings

            this.teams = teams ? JSON.parse(teams) : DEFAULT_TEAMS;
            this.players = players ? JSON.parse(players) : DEFAULT_PLAYERS;
            this.standings = standings ? JSON.parse(standings) : DEFAULT_STANDINGS;
            this.settings = settings ? JSON.parse(settings) : DEFAULT_SETTINGS; // Init settings
            
            // Data structure migration check
            this.players.forEach(p => {
                if (!p.imageUrl) p.imageUrl = DEFAULT_PLAYER_IMAGE;
                if (!p.swingVideo) p.swingVideo = DEFAULT_PLAYER_VIDEO;
                if (p.scores.length > 0 && typeof p.scores[0] === 'number') {
                    p.scores = p.scores.map((score, index) => ({
                        id: `R${index + 1}`,
                        date: 'N/A',
                        course: 'Unknown',
                        holeScores: Array(18).fill('?'),
                        total: score
                    }));
                }
            });
            
            // Ensure all teams from DEFAULT_TEAMS exist, preserving logos from localStorage
            DEFAULT_TEAMS.forEach(defaultTeam => {
                const existingTeam = this.teams.find(t => t.id === defaultTeam.id);
                if (existingTeam) {
                    // Ensure all properties exist, but keep saved logo
                    existingTeam.name = defaultTeam.name;
                    existingTeam.description = defaultTeam.description;
                    existingTeam.region = defaultTeam.region;
                    existingTeam.feature = defaultTeam.feature;
                    existingTeam.players = defaultTeam.players;
                    // existingTeam.logo is preserved
                } else {
                    // Add new team
                    this.teams.push(defaultTeam);
                }
            });


            this.saveData(); // Save defaults or migrated data
        }

        saveData() {
            localStorage.setItem(DB_KEYS.teams, JSON.stringify(this.teams));
            localStorage.setItem(DB_KEYS.players, JSON.stringify(this.players));
            localStorage.setItem(DB_KEYS.standings, JSON.stringify(this.standings));
            localStorage.setItem(DB_KEYS.settings, JSON.stringify(this.settings)); // Save settings
        }

        resetData() {
            if (confirm('모든 스코어와 매치 기록, 사이트 설정을 초기화합니다. 정말 실행하시겠습니까?')) {
                localStorage.removeItem(DB_KEYS.teams);
                localStorage.removeItem(DB_KEYS.players);
                localStorage.removeItem(DB_KEYS.standings);
                localStorage.removeItem(DB_KEYS.settings); // Reset settings
                this.loadData();
                this.renderAll();
                this.showGlobalMessage('데이터가 초기화되었습니다.', 'secondary');
            }
        }

        // --- Navigation ---
        setupNavigation() {
            const navLinks = document.querySelectorAll('.nav-link');
            const mobileMenuButton = document.getElementById('mobile-menu-button');
            const mobileMenu = document.getElementById('mobile-menu');

            navLinks.forEach(link => link.addEventListener('click', (e) => {
                e.preventDefault();
                const targetId = link.dataset.target;
                this.showSection(targetId);
                mobileMenu.classList.add('hidden');
            }));

            mobileMenuButton.addEventListener('click', () => mobileMenu.classList.toggle('hidden'));
        }

        showSection(targetId) {
            document.querySelectorAll('.section').forEach(section => section.classList.remove('active'));
            document.getElementById(targetId)?.classList.add('active');

            document.querySelectorAll('.nav-link').forEach(link => {
                link.classList.remove('active');
                if (link.dataset.target === targetId) link.classList.add('active');
            });
            window.scrollTo(0, 0);
        }

        // --- Modal ---
        setupModals() {
            const videoModal = document.getElementById('video-modal');
            const scorecardModal = document.getElementById('scorecard-modal');
            const videoPlayer = document.getElementById('swing-video');

            document.body.addEventListener('click', (e) => {
                const button = e.target.closest('button');
                if (!button) return;

                if (button.classList.contains('open-video-btn')) {
                    const playerName = button.dataset.playerName;
                    const videoSrc = button.dataset.videoSrc;
                    document.getElementById('modal-player-name').textContent = `${playerName}'s Swing`;
                    videoPlayer.src = videoSrc;
                    videoModal.classList.remove('hidden');
                }
                
                if (button.classList.contains('open-score-btn')) {
                    const playerName = button.dataset.playerName;
                    const player = this.players.find(p => p.name === playerName);
                    if (player) {
                        this.renderScorecardModal(player);
                        scorecardModal.classList.remove('hidden');
                    }
                }

                if (button.classList.contains('close-modal-btn')) {
                    videoModal.classList.add('hidden');
                    scorecardModal.classList.add('hidden');
                    videoPlayer.pause();
                    videoPlayer.src = '';
                }
            });

            [videoModal, scorecardModal].forEach(modal => {
                modal.addEventListener('click', (e) => {
                    if (e.target === modal) {
                        modal.classList.add('hidden');
                        videoPlayer.pause();
                        videoPlayer.src = '';
                    }
                });
            });
        }
        
        renderScorecardModal(player) {
            const contentEl = document.getElementById('scorecard-content');
            document.getElementById('scorecard-player-name').textContent = `${player.name}'s Scorecards`;
            
            if (player.scores.length === 0) {
                contentEl.innerHTML = `<p class="text-gray-400 text-center">아직 등록된 스코어카드가 없습니다.</p>`;
                return;
            }
            
            let html = '';
            [...player.scores].reverse().forEach(round => {
                const outScores = round.holeScores.slice(0, 9);
                const inScores = round.holeScores.slice(9, 18);
                const outTotal = outScores.reduce((a, b) => (a + (Number(b) || 0)), 0);
                const inTotal = inScores.reduce((a, b) => (a + (Number(b) || 0)), 0);
                
                html += `
                    <div class="bg-gray-800/50 rounded-lg p-4 mb-4 border border-gray-700">
                        <div class="flex justify-between items-center mb-3">
                            <div>
                                <h4 class="text-xl font-bold">${round.course}</h4>
                                <p class="text-sm text-gray-400">${round.date}</p>
                            </div>
                            <h3 class="text-3xl font-bold text-emerald-400">Total: ${round.total}</h3>
                        </div>
                        <div class="overflow-x-auto">
                            <table class="w-full text-center scorecard-table border-collapse">
                                <thead class="text-xs text-gray-400">
                                    <tr>
                                        <th>Hole</th>
                                        ${Array.from({length: 9}, (_, i) => `<th>${i+1}</th>`).join('')}
                                        <th class="text-white bg-gray-600">OUT</th>
                                        ${Array.from({length: 9}, (_, i) => `<th>${i+10}</th>`).join('')}
                                        <th class="text-white bg-gray-600">IN</th>
                                    </tr>
                                </thead>
                                <tbody class="font-bold">
                                    <tr>
                                        <td class="text-sm text-gray-400 font-normal">Score</td>
                                        ${outScores.map(s => `<td>${s}</td>`).join('')}
                                        <td class="text-emerald-400 bg-gray-700">${outTotal}</td>
                                        ${inScores.map(s => `<td>${s}</td>`).join('')}
                                        <td class="text-emerald-400 bg-gray-700">${inTotal}</td>
                                    </tr>
                                </tbody>
                            </table>
                        </div>
                    </div>
                `;
            });
            contentEl.innerHTML = html;
        }

        // --- Admin ---
        setupAdmin() {
            // Login
            document.getElementById('login-button').addEventListener('click', () => {
                if (document.getElementById('password').value === ADMIN_PASSWORD) {
                    this.isAdminLoggedIn = true;
                    document.getElementById('admin-login').classList.add('hidden');
                    document.getElementById('admin-panel').classList.remove('hidden');
                    this.populateAdminForms();
                    document.getElementById('score-date').value = new Date().toISOString().split('T')[0];
                } else {
                    document.getElementById('login-error').classList.remove('hidden');
                }
            });
            
            // Admin Tabs
            document.querySelectorAll('.admin-tab').forEach(tab => {
                tab.addEventListener('click', (e) => {
                    document.querySelectorAll('.admin-tab').forEach(t => {
                        t.classList.add('text-gray-500');
                        t.classList.remove('active');
                    });
                    e.target.classList.remove('text-gray-500');
                    e.target.classList.add('active');
                    document.querySelectorAll('.admin-tab-content').forEach(c => c.classList.add('hidden'));
                    document.getElementById(e.target.dataset.target).classList.remove('hidden');
                });
            });
            
            // Auto-sum score form
            document.getElementById('add-score-form').addEventListener('input', (e) => {
                if (e.target.classList.contains('hole-score')) {
                    let total = 0;
                    document.querySelectorAll('.hole-score').forEach(input => {
                        total += Number(input.value) || 0;
                    });
                    document.getElementById('score-total').textContent = total;
                }
            });
            
            // Form Handlers
            document.getElementById('add-score-form').addEventListener('submit', (e) => this.handleAddScore(e));
            document.getElementById('add-match-form').addEventListener('submit', (e) => this.handleAddMatch(e));
            document.getElementById('edit-player-form').addEventListener('submit', (e) => this.handleEditPlayer(e));
            document.getElementById('edit-home-bg-form').addEventListener('submit', (e) => this.handleEditHomeBg(e));
            document.getElementById('edit-team-logo-form').addEventListener('submit', (e) => this.handleEditTeamLogo(e));
            
            document.getElementById('edit-player-select').addEventListener('change', (e) => this.populateEditPlayerForm(e));
            document.getElementById('setting-team-select').addEventListener('change', (e) => this.populateEditTeamLogoForm(e));
            
            document.getElementById('reset-data-button').addEventListener('click', () => this.resetData());
        }

        populateAdminForms() {
            // Player selects
            const scorePlayerSelect = document.getElementById('score-player');
            const editPlayerSelect = document.getElementById('edit-player-select');
            const playerOptions = this.players.map(p => `<option value="${p.name}">${p.name} (${p.team})</option>`).join('');
            scorePlayerSelect.innerHTML = playerOptions;
            editPlayerSelect.innerHTML = `<option value="">-- 선수 선택 --</option>` + playerOptions;

            // Team selects
            const team1Select = document.getElementById('match-team1');
            const team2Select = document.getElementById('match-team2');
            const settingTeamSelect = document.getElementById('setting-team-select');
            const teamOptions = this.teams.map(t => `<option value="${t.id}">${t.name}</option>`).join('');
            team1Select.innerHTML = teamOptions;
            team2Select.innerHTML = teamOptions;
            team2Select.value = this.teams[1]?.id || '';
            settingTeamSelect.innerHTML = `<option value="">-- 팀 선택 --</option>` + teamOptions;

            // Site Settings forms
            document.getElementById('setting-bg-type').value = this.settings.backgroundType;
            document.getElementById('setting-bg-url').value = this.settings.backgroundUrl;
            
            this.populateEditTeamLogoForm({ target: { value: '' }});
        }

        populateEditPlayerForm(e) {
            const playerName = e.target.value;
            const player = this.players.find(p => p.name === playerName);
            if (player) {
                document.getElementById('edit-player-image').value = player.imageUrl || '';
                document.getElementById('edit-player-video').value = player.swingVideo || '';
                document.getElementById('edit-player-feature').value = player.feature || '';
            } else {
                 document.getElementById('edit-player-form').reset();
            }
        }
        
        populateEditTeamLogoForm(e) {
            const teamId = e.target.value;
            const team = this.teams.find(t => t.id === teamId);
            if (team) {
                document.getElementById('setting-team-logo-url').value = team.logo || '';
                document.getElementById('setting-team-logo-preview').src = team.logo || '';
            } else {
                document.getElementById('setting-team-logo-url').value = '';
                document.getElementById('setting-team-logo-preview').src = '';
            }
        }
        
        handleAddScore(e) {
            e.preventDefault();
            const form = e.target;
            const playerName = document.getElementById('score-player').value;
            const course = document.getElementById('score-course').value;
            const date = document.getElementById('score-date').value;
            
            const holeScores = [];
            const scoreInputs = document.querySelectorAll('.hole-score');
            for (const input of scoreInputs) {
                if (input.value === '' || isNaN(parseInt(input.value))) {
                    alert('18홀 스코어를 모두 정확히 입력하세요.');
                    return;
                }
                holeScores.push(parseInt(input.value));
            }
            
            const total = holeScores.reduce((a, b) => a + b, 0);

            const player = this.players.find(p => p.name === playerName);
            if (player) {
                const newRound = {
                    id: `R${player.scores.length + 1}`,
                    date,
                    course,
                    holeScores,
                    total
                };
                player.scores.push(newRound);
                this.saveData();
                this.renderStandings();
                this.showGlobalMessage('스코어카드가 저장되었습니다.');
                form.reset();
                document.getElementById('score-total').textContent = '0';
                document.getElementById('score-date').value = new Date().toISOString().split('T')[0];
            }
        }

        handleAddMatch(e) {
            e.preventDefault();
            const t1 = document.getElementById('match-team1').value;
            const s1 = parseInt(document.getElementById('match-score1').value);
            const t2 = document.getElementById('match-team2').value;
            const s2 = parseInt(document.getElementById('match-score2').value);

            if (t1 === t2) {
                alert('같은 팀 간의 경기는 추가할 수 없습니다.');
                return;
            }
            
            this.standings.push({ t1, s1, t2, s2, date: new Date().toISOString().split('T')[0] });
            this.saveData();
            this.renderStandings();
            this.renderHome();
            this.showGlobalMessage('매치 결과가 저장되었습니다.');
            e.target.reset();
        }
        
        handleEditPlayer(e) {
            e.preventDefault();
            const playerName = document.getElementById('edit-player-select').value;
            if (!playerName) { alert('선수를 선택하세요.'); return; }
            
            const imageUrl = document.getElementById('edit-player-image').value;
            const videoUrl = document.getElementById('edit-player-video').value;
            const feature = document.getElementById('edit-player-feature').value;
            
            const player = this.players.find(p => p.name === playerName);
            if(player) {
                player.imageUrl = imageUrl || DEFAULT_PLAYER_IMAGE;
                player.swingVideo = videoUrl || DEFAULT_PLAYER_VIDEO;
                player.feature = feature;
                this.saveData();
                this.renderPlayers();
                this.renderTeams();
                this.showGlobalMessage('선수 정보가 수정되었습니다.');
                e.target.reset();
            }
        }

        handleEditHomeBg(e) {
            e.preventDefault();
            this.settings.backgroundType = document.getElementById('setting-bg-type').value;
            this.settings.backgroundUrl = document.getElementById('setting-bg-url').value;
            this.saveData();
            this.renderHome();
            this.showGlobalMessage('홈 배경이 저장되었습니다.');
        }
        
        handleEditTeamLogo(e) {
            e.preventDefault();
            const teamId = document.getElementById('setting-team-select').value;
            if (!teamId) { alert('팀을 선택하세요.'); return; }
            
            const newLogoUrl = document.getElementById('setting-team-logo-url').value;
            const team = this.teams.find(t => t.id === teamId);
            
            if (team) {
                team.logo = newLogoUrl;
                this.saveData();
                this.renderAll(); // Re-render everything as logos are everywhere
                this.showGlobalMessage('팀 로고가 수정되었습니다.');
                // Update preview
                document.getElementById('setting-team-logo-preview').src = newLogoUrl;
            }
        }

        // --- Rendering ---
        renderAll() {
            this.renderHome();
            this.renderTeams();
            this.renderPlayers();
            this.renderStandings();
        }

        renderHome() {
            // --- 1. Render Home Banner (Image or Video) ---
            const container = document.getElementById('home-banner-container');
            container.innerHTML = ''; // Clear previous content
            
            const textOverlay = `
                <div class="relative z-10 py-24 px-6 flex flex-col items-center justify-center h-full">
                    <h2 class="text-5xl font-extrabold text-white drop-shadow-lg">THREE TEAMS, ONE GOAL</h2>
                    <p class="mt-4 text-xl text-gray-200 drop-shadow-md">친목을 넘어 진정한 승부를 가린다.</p>
                </div>`;
            
            if (this.settings.backgroundType === 'video' && this.settings.backgroundUrl) {
                container.innerHTML = `
                    <video classD="absolute top-0 left-0 w-full h-full object-cover z-0" src="${this.settings.backgroundUrl}" autoplay loop muted playsinline></video>
                    <div class="absolute top-0 left-0 w-full h-full bg-black/30 z-0"></div>
                    ${textOverlay}
                `;
            } else {
                // Default to image
                container.style.backgroundImage = `url('${this.settings.backgroundUrl || DEFAULT_SETTINGS.backgroundUrl}')`;
                container.style.backgroundSize = 'cover';
                container.style.backgroundPosition = 'center';
                container.innerHTML = `
                    <div class="absolute top-0 left-0 w-full h-full bg-black/30 z-0"></div>
                    ${textOverlay}
                `;
            }

            // --- 2. Render Home Teams ---
            const homeTeamsContainer = document.getElementById('home-teams');
            homeTeamsContainer.innerHTML = '';
            this.teams.forEach(team => {
                homeTeamsContainer.innerHTML += `
                    <div class="team-card rounded-lg p-6 text-center">
                        <img src="${team.logo}" alt="${team.name} Logo" class="w-24 h-24 mx-auto mb-4 object-contain">
                        <h4 class="text-2xl font-bold">${team.name}</h4>
                        <p class="text-gray-400 mt-2">${team.region}</p>
                        <p class="mt-4 text-emerald-400 font-semibold">${team.feature}</p>
                    </div>`;
            });

            // --- 3. Render Recent Match ---
            const recentMatchContainer = document.getElementById('recent-match-container');
            const lastMatch = this.standings.length > 0 ? this.standings[this.standings.length - 1] : null;
            if (lastMatch) {
                const team1 = this.teams.find(t => t.id === lastMatch.t1);
                const team2 = this.teams.find(t => t.id === lastMatch.t2);
                if (!team1 || !team2) { 
                     recentMatchContainer.innerHTML = `<p class="text-center text-gray-400">매치 데이터를 불러오는 데 오류가 발생했습니다.</p>`;
                     return;
                }
                const winner = lastMatch.s1 > lastMatch.s2 ? team1 : (lastMatch.s2 > lastMatch.s1 ? team2 : null);
                
                recentMatchContainer.innerHTML = `
                    <div class="flex flex-col sm:flex-row justify-around items-center text-center gap-4">
                        <div class="flex flex-col items-center">
                            <img src="${team1.logo}" class="h-20 mb-2 object-contain ${winner && winner.id === team2.id ? 'opacity-50' : ''}" alt="${team1.name} Logo">
                            <span class="text-2xl font-black ${winner && winner.id === team1.id ? 'text-emerald-400' : (winner ? 'text-gray-500' : 'text-white')}">${team1.name}</span>
                        </div>
                        <div class="text-center my-4 sm:my-0">
                            <span class="text-6xl font-bold text-white">${lastMatch.s1} : ${lastMatch.s2}</span>
                            <p class="text-gray-400 mt-2">${lastMatch.date || 'Recent Match'}</p>
                        </div>
                         <div class="flex flex-col items-center">
                            <img src="${team2.logo}" class="h-20 mb-2 object-contain ${winner && winner.id === team1.id ? 'opacity-50' : ''}" alt="${team2.name} Logo">
                            <span class="text-2xl font-black ${winner && winner.id === team2.id ? 'text-emerald-400' : (winner ? 'text-gray-500' : 'text-white')}">${team2.name}</span>
                        </div>
                    </div>`;
            } else {
                 recentMatchContainer.innerHTML = `<p class="text-center text-gray-400">아직 등록된 매치 결과가 없습니다.</p>`;
            }
        }

        renderTeams() {
            const teamDetailsContainer = document.getElementById('team-details');
            teamDetailsContainer.innerHTML = '';
            this.teams.forEach(team => {
                const playersHtml = team.players.map(playerName => {
                    const player = this.players.find(p => p.name === playerName);
                    if (!player) return '';
                    return `
                        <div class="flex items-center space-x-4 p-3 bg-gray-800 rounded-md">
                            <img src="${player.imageUrl}" alt="${player.name}" class="w-10 h-10 rounded-full object-cover flex-shrink-0">
                            <div>
                                <p class="font-bold text-white">${playerName} ${player.role === 'Captain' ? '<span class="text-xs text-emerald-400">(C)</span>' : ''}</p>
                                <p class="text-sm text-gray-400">${player.feature}</p>
                            </div>
                        </div>`;
                }).join('');

                teamDetailsContainer.innerHTML += `
                    <div class="team-card rounded-lg p-8 grid md:grid-cols-3 gap-8 items-center">
                        <div class="md:col-span-1 text-center">
                            <img src="${team.logo}" alt="${team.name} Logo" class="w-32 h-32 mx-auto mb-4 object-contain">
                            <h3 class="text-4xl font-black">${team.name}</h3>
                            <p class="text-gray-400 mt-2">${team.feature}</p>
                        </div>
                        <div class="md:col-span-2">
                            <p class="text-lg text-gray-300 mb-6">${team.description}</p>
                            <h4 class="text-xl font-bold mb-4">Player Roster</h4>
                            <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">${playersHtml}</div>
                        </div>
                    </div>`;
            });
        }

        renderPlayers() {
            const playerProfilesContainer = document.getElementById('player-profiles');
            playerProfilesContainer.innerHTML = '';
            this.players.forEach(player => {
                playerProfilesContainer.innerHTML += `
                    <div class="player-card rounded-lg p-5 text-center flex flex-col justify-between">
                        <div>
                            <img src="${player.imageUrl}" alt="${player.name}" class="w-20 h-20 rounded-full object-cover mx-auto border-4 border-gray-600 mb-4">
                            <h5 class="text-xl font-bold">${player.name}</h5>
                            <p class="text-emerald-400">${player.team}</p>
                            <p class="text-sm text-gray-400 mt-2 min-h-[20px]">${player.feature || ''}</p>
                        </div>
                        <div class="grid grid-cols-2 gap-2 mt-4">
                            <button class="btn-primary w-full py-2 rounded-md open-video-btn" data-player-name="${player.name}" data-video-src="${player.swingVideo || ''}">
                                Swing
                            </button>
                            <button class="btn-secondary w-full py-2 rounded-md open-score-btn" data-player-name="${player.name}">
                                Scorecards
                            </button>
                        </div>
                    </div>`;
            });
        }

        renderStandings() {
            // --- 1. Team Standings ---
            const teamStats = {};
            this.teams.forEach(t => {
                teamStats[t.id] = { ...t, w: 0, l: 0, d: 0, pts: 0 };
            });

            this.standings.forEach(match => {
                const { t1, s1, t2, s2 } = match;
                if (!teamStats[t1] || !teamStats[t2]) return;

                if (s1 > s2) {
                    teamStats[t1].w++;
                    teamStats[t2].l++;
                    teamStats[t1].pts += 2;
                } else if (s2 > s1) {
                    teamStats[t2].w++;
                    teamStats[t1].l++;
                    teamStats[t2].pts += 2;
                } else {
                    teamStats[t1].d++;
                    teamStats[t2].d++;
                    teamStats[t1].pts += 1;
                    teamStats[t2].pts += 1;
                }
            });

            const sortedTeams = Object.values(teamStats).sort((a, b) => b.pts - a.pts || (b.w - b.l) - (a.w - a.l));
            
            let teamStandingsHtml = `
                <div class="bg-[#1E1E1E] border border-gray-700 rounded-lg overflow-hidden">
                    <div class="p-6"><h3 class="text-2xl font-bold">Team Standings</h3></div>
                    <div class="overflow-x-auto">
                        <table class="w-full text-left">
                            <thead class="table-header">
                                <tr>
                                    <th class="p-4">POS</th>
                                    <th class="p-4">TEAM</th>
                                    <th class="p-4 text-center">W</th>
                                    <th class="p-4 text-center">L</th>
                                    <th class="p-4 text-center">D</th>
                                    <th class="p-4 text-center">PTS</th>
                                </tr>
                            </thead>
                            <tbody>`;
            
            sortedTeams.forEach((team, index) => {
                const rowClass = index % 2 === 0 ? 'table-row-light' : 'table-row-dark';
                teamStandingsHtml += `
                    <tr class="${rowClass} border-t border-gray-700">
                        <td class="p-4 font-bold">${index + 1}</td>
                        <td class="p-4 font-bold text-emerald-400 flex items-center gap-4">
                            <img src="${team.logo}" class="h-8 w-8 object-contain" alt="${team.name} logo">
                            <span>${team.name}</span>
                        </td>
                        <td class="p-4 text-center">${team.w}</td>
                        <td class="p-4 text-center">${team.l}</td>
                        <td class="p-4 text-center">${team.d}</td>
                        <td class="p-4 text-center">${team.pts}</td>
                    </tr>`;
            });
            teamStandingsHtml += `</tbody></table></div></div>`;
            document.getElementById('team-standings-container').innerHTML = teamStandingsHtml;

            // --- 2. Individual Scoreboard (based on round totals) ---
            let maxRounds = 0;
            this.players.forEach(p => {
                if (p.scores.length > maxRounds) maxRounds = p.scores.length;
            });

            const sortedPlayers = [...this.players].sort((a, b) => {
                const avgA = a.scores.length ? a.scores.reduce((sum, round) => sum + round.total, 0) / a.scores.length : Infinity;
                const avgB = b.scores.length ? b.scores.reduce((sum, round) => sum + round.total, 0) / b.scores.length : Infinity;
                return avgA - avgB;
            });

            let individualScoresHtml = `
                <div class="bg-[#1E1E1E] border border-gray-700 rounded-lg overflow-hidden">
                    <div class="p-6"><h3 class="text-2xl font-bold">Individual Scoreboard</h3></div>
                    <div class="overflow-x-auto">
                        <table class="w-full text-left min-w-[600px]">
                            <thead class="table-header text-sm">
                                <tr>
                                    <th class="p-3">POS</th>
                                    <th class="p-3">Player</th>
                                    <th class="p-3">Team</th>`;
            if (maxRounds === 0) {
                individualScoresHtml += `<th class="p-3 text-center">R1</th>`;
                maxRounds = 1; // Show at least 1 round column
            }
            for (let i = 1; i <= maxRounds; i++) {
                individualScoresHtml += `<th class="p-3 text-center">R${i}</th>`;
            }
            individualScoresHtml += `<th class="p-3 text-center font-bold">AVG</th></tr></thead><tbody>`;

            sortedPlayers.forEach((player, index) => {
                const rowClass = index % 2 === 0 ? 'table-row-light' : 'table-row-dark';
                let totalScoreSum = 0;
                let scoreCount = 0;
                
                let scoresHtml = '';
                for (let i = 0; i < maxRounds; i++) {
                    const round = player.scores[i];
                    if (round) {
                        totalScoreSum += round.total;
                        scoreCount++;
                        scoresHtml += `<td class="p-3 text-center">${round.total}</td>`;
                    } else {
                        scoresHtml += `<td class="p-3 text-center text-gray-500">-</td>`;
                    }
                }
                
                const avgScore = scoreCount > 0 ? (totalScoreSum / scoreCount).toFixed(2) : '-';

                individualScoresHtml += `
                    <tr class="${rowClass} border-t border-gray-700">
                        <td class="p-3 font-bold">${index + 1}</td>
                        <td class="p-3 font-bold">${player.name}</td>
                        <td class="p-3 text-gray-400">${player.team}</td>
                        ${scoresHtml}
                        <td class="p-3 text-center font-bold text-emerald-400">${avgScore}</td>
                    </tr>`;
            });
            individualScoresHtml += `</tbody></table></div></div>`;
            document.getElementById('player-scores-container').innerHTML = individualScoresHtml;
        }
        
        showGlobalMessage(message, type = 'success') {
            const msgBox = document.getElementById('global-message');
            msgBox.textContent = message;
            if (type === 'success') {
                msgBox.classList.remove('bg-red-500', 'bg-gray-500');
                msgBox.classList.add('bg-emerald-500');
            } else {
                msgBox.classList.remove('bg-emerald-500');
                msgBox.classList.add('bg-red-500');
            }
            msgBox.classList.remove('hidden');
            setTimeout(() => {
                msgBox.classList.add('hidden');
            }, 2000);
        }
    }

    // --- Run App ---
    document.addEventListener('DOMContentLoaded', () => {
        const app = new GolfLeagueApp();
        app.init();
    });
</script>

</body>
</html>
