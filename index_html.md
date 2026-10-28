<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Brasileirão Stats & Palpites 2026</title>
  
  <!-- Tailwind CSS CDN -->
  <script src="https://cdn.tailwindcss.com"></script>
  
  <!-- React & React DOM CDNs -->
  <script crossorigin src="https://unpkg.com/react@18/umd/react.production.min.js"></script>
  <script crossorigin src="https://unpkg.com/react-dom@18/umd/react-dom.production.min.js"></script>
  
  <!-- Babel Standalone for JSX transformation in-browser -->
  <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>

  <!-- Lucide Icons CDN -->
  <script src="https://unpkg.com/lucide@latest"></script>

  <style>
    body {
      background-color: #0D1117;
      color: #f3f4f6;
      font-family: ui-sans-serif, system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
    }
    /* Custom scrollbar */
    ::-webkit-scrollbar {
      width: 6px;
      height: 6px;
    }
    ::-webkit-scrollbar-track {
      background: #0D1117;
    }
    ::-webkit-scrollbar-thumb {
      background: #21262D;
      border-radius: 4px;
    }
    ::-webkit-scrollbar-thumb:hover {
      background: #30363D;
    }
  </style>
</head>
<body class="bg-[#0D1117] text-gray-100 antialiased selection:bg-[#00E676] selection:text-black">

  <div id="root"></div>

  <!-- React Application Code -->
  <script type="text/babel">
    const { useState, useEffect } = React;

    // Helper SVG Component for Lucide Icons
    const Icon = ({ name, className = "w-4 h-4" }) => {
      useEffect(() => {
        if (window.lucide) {
          window.lucide.createIcons();
        }
      }, [name]);
      return <i data-lucide={name} class={className}></i>;
    };

    // --- OFFICIAL TEAM CRESTS (GOOGLE SPORTS CDN) ---
    const CRESTS = {
      Flamengo: 'https://ssl.gstatic.com/onebox/media/sports/logos/optimized/orE554NToSkH6nuwofe7Yg_500x500.png',
      Palmeiras: 'https://ssl.gstatic.com/onebox/media/sports/logos/optimized/7spurne-xDt2p6C0imYYNA_500x500.png',
      Cruzeiro: 'https://ssl.gstatic.com/onebox/media/sports/logos/optimized/Tcv9X__nIh-6wFNJPMwIXQ_500x500.png',
      'Athletico-PR': 'https://ssl.gstatic.com/onebox/media/sports/logos/optimized/9LkdBR4L5plovKM8eIy7nQ_500x500.png',
      Fluminense: 'https://ssl.gstatic.com/onebox/media/sports/logos/optimized/fCMxMMDF2AZPU7LzYKSlig_500x500.png',
      'Atlético-MG': 'https://ssl.gstatic.com/onebox/media/sports/logos/optimized/q9fhEsgpuyRq58OgmSndcQ_500x500.png',
      Bahia: 'https://ssl.gstatic.com/onebox/media/sports/logos/optimized/nIdbR6qIUDyZUBO9vojSPw_500x500.png',
      Santos: 'https://ssl.gstatic.com/onebox/media/sports/logos/optimized/VHdNOT6wWOw_vJ38GMjMzg_500x500.png',
      'São Paulo': 'https://ssl.gstatic.com/onebox/media/sports/logos/optimized/4w2Z97Hf9CSOqICK3a8AxQ_500x500.png',
      'Red Bull Bragantino': 'https://ssl.gstatic.com/onebox/media/sports/logos/optimized/lMyw2zn1Z4cdkaxKJWnsQw_500x500.png',
      Botafogo: 'https://ssl.gstatic.com/onebox/media/sports/logos/optimized/KLDWYp-H8CAOT9H_JgizRg_500x500.png',
      Coritiba: 'https://ssl.gstatic.com/onebox/media/sports/logos/optimized/LaFlBADLmsjHfGTehCYtuA_500x500.png',
      'Vasco da Gama': 'https://ssl.gstatic.com/onebox/media/sports/logos/optimized/hHwT8LwRmYCAGxQ-STLxYA_500x500.png',
      Vitória: 'https://ssl.gstatic.com/onebox/media/sports/logos/optimized/LHSM6VchpkI4NIptoSTHOg_500x500.png',
      Mirassol: 'https://ssl.gstatic.com/onebox/media/sports/logos/optimized/5J3JY7fcdiDYU5rbPW7AKA_500x500.png',
      Internacional: 'https://ssl.gstatic.com/onebox/media/sports/logos/optimized/OWVFKuHrQuf4q2Wk0hEmSA_500x500.png',
      Grêmio: 'https://ssl.gstatic.com/onebox/media/sports/logos/optimized/Ku-73v_TW9kpex-IEGb0ZA_500x500.png',
      Corinthians: 'https://ssl.gstatic.com/onebox/media/sports/logos/optimized/tCMSqgXVHROpdCpQhzTo1g_500x500.png',
      Remo: 'https://ssl.gstatic.com/onebox/media/sports/logos/optimized/bENrK5iSMF6sXrEkDNNxng_500x500.png',
      Chapecoense: 'https://ssl.gstatic.com/onebox/media/sports/logos/optimized/K7JQUKTRsuXfO9YrD5dq5g_500x500.png'
    };

    const TEAMS_LIST = Object.keys(CRESTS);

    // --- REAL MATCHES FOR TODAY (28/10/2026 - RODADA 33) ---
    const INITIAL_MATCHES = [
      {
        id: 'm1',
        round: 33,
        homeTeam: 'Santos',
        awayTeam: 'Palmeiras',
        homeLogo: CRESTS['Santos'],
        awayLogo: CRESTS['Palmeiras'],
        date: 'Hoje (28/10), 19:30',
        stadium: 'Vila Belmiro, Santos',
        aiPrediction: { home: 1, away: 2, probHome: 28, probDraw: 30, probAway: 42, reasoning: 'Palmeiras briga ponto a ponto pelo título com o Flamengo. Santos tenta estabilidade na Série A.' }
      },
      {
        id: 'm2',
        round: 33,
        homeTeam: 'Fluminense',
        awayTeam: 'Internacional',
        homeLogo: CRESTS['Fluminense'],
        awayLogo: CRESTS['Internacional'],
        date: 'Hoje (28/10), 19:30',
        stadium: 'Maracanã, Rio de Janeiro',
        aiPrediction: { home: 2, away: 1, probHome: 48, probDraw: 28, probAway: 24, reasoning: 'Fluminense busca consolidar vaga no G6. Internacional tenta fugir da aproximação da Z4.' }
      },
      {
        id: 'm3',
        round: 33,
        homeTeam: 'Red Bull Bragantino',
        awayTeam: 'Chapecoense',
        homeLogo: CRESTS['Red Bull Bragantino'],
        awayLogo: CRESTS['Chapecoense'],
        date: 'Hoje (28/10), 19:30',
        stadium: 'Cícero Marques, Bragança Paulista',
        aiPrediction: { home: 3, away: 0, probHome: 68, probDraw: 20, probAway: 12, reasoning: 'Massa Bruta é forte mandante contra a lanterna Chapecoense em crise defensiva.' }
      },
      {
        id: 'm4',
        round: 33,
        homeTeam: 'Remo',
        awayTeam: 'Botafogo',
        homeLogo: CRESTS['Remo'],
        awayLogo: CRESTS['Botafogo'],
        date: 'Hoje (28/10), 21:30',
        stadium: 'Baenão / Mangueirão, Belém',
        aiPrediction: { home: 1, away: 1, probHome: 35, probDraw: 35, probAway: 30, reasoning: 'Remo em situação crítica na 19ª posição atua sob forte pressão da torcida no Pará.' }
      },
      {
        id: 'm5',
        round: 33,
        homeTeam: 'Bahia',
        awayTeam: 'São Paulo',
        homeLogo: CRESTS['Bahia'],
        awayLogo: CRESTS['São Paulo'],
        date: 'Hoje (28/10), 21:30',
        stadium: 'Arena Fonte Nova, Salvador',
        aiPrediction: { home: 2, away: 1, probHome: 45, probDraw: 30, probAway: 25, reasoning: 'Bahia com bom retrospecto na Fonte Nova mirando vaga direta na Libertadores.' }
      }
    ];

    // --- REAL STANDINGS TABLE (OCTOBER 28, 2026 - 32 MATCHES) ---
    const INITIAL_STANDINGS = [
      { pos: 1, name: 'Flamengo', pts: 70, j: 32, v: 21, e: 7, d: 4, sg: 37, form: ['V', 'V', 'E', 'V', 'V'], logo: CRESTS['Flamengo'] },
      { pos: 2, name: 'Palmeiras', pts: 69, j: 32, v: 20, e: 9, d: 3, sg: 34, form: ['V', 'V', 'V', 'E', 'V'], logo: CRESTS['Palmeiras'] },
      { pos: 3, name: 'Cruzeiro', pts: 54, j: 32, v: 16, e: 6, d: 10, sg: 5, form: ['D', 'V', 'E', 'V', 'V'], logo: CRESTS['Cruzeiro'] },
      { pos: 4, name: 'Athletico-PR', pts: 54, j: 32, v: 15, e: 9, d: 8, sg: 12, form: ['V', 'E', 'V', 'D', 'E'], logo: CRESTS['Athletico-PR'] },
      { pos: 5, name: 'Fluminense', pts: 51, j: 32, v: 14, e: 9, d: 9, sg: 9, form: ['E', 'V', 'V', 'D', 'V'], logo: CRESTS['Fluminense'] },
      { pos: 6, name: 'Atlético-MG', pts: 50, j: 32, v: 14, e: 8, d: 10, sg: 6, form: ['V', 'D', 'E', 'V', 'D'], logo: CRESTS['Atlético-MG'] },
      { pos: 7, name: 'Bahia', pts: 50, j: 32, v: 13, e: 11, d: 8, sg: 5, form: ['E', 'V', 'D', 'V', 'E'], logo: CRESTS['Bahia'] },
      { pos: 8, name: 'Santos', pts: 46, j: 32, v: 12, e: 10, d: 10, sg: 2, form: ['V', 'E', 'D', 'E', 'V'], logo: CRESTS['Santos'] },
      { pos: 9, name: 'São Paulo', pts: 43, j: 32, v: 12, e: 7, d: 13, sg: 1, form: ['D', 'V', 'D', 'V', 'D'], logo: CRESTS['São Paulo'] },
      { pos: 10, name: 'Red Bull Bragantino', pts: 41, j: 32, v: 11, e: 8, d: 13, sg: 1, form: ['E', 'D', 'V', 'D', 'E'], logo: CRESTS['Red Bull Bragantino'] },
      { pos: 11, name: 'Botafogo', pts: 39, j: 32, v: 10, e: 9, d: 13, sg: -7, form: ['D', 'E', 'D', 'D', 'V'], logo: CRESTS['Botafogo'] },
      { pos: 12, name: 'Coritiba', pts: 39, j: 32, v: 10, e: 9, d: 13, sg: -12, form: ['V', 'D', 'E', 'V', 'D'], logo: CRESTS['Coritiba'] },
      { pos: 13, name: 'Vasco da Gama', pts: 38, j: 31, v: 10, e: 8, d: 13, sg: -6, form: ['E', 'V', 'D', 'E', 'D'], logo: CRESTS['Vasco da Gama'] },
      { pos: 14, name: 'Vitória', pts: 38, j: 32, v: 10, e: 8, d: 14, sg: -11, form: ['V', 'D', 'V', 'D', 'V'], logo: CRESTS['Vitória'] },
      { pos: 15, name: 'Mirassol', pts: 37, j: 32, v: 9, e: 10, d: 13, sg: -8, form: ['E', 'E', 'D', 'V', 'D'], logo: CRESTS['Mirassol'] },
      { pos: 16, name: 'Internacional', pts: 35, j: 32, v: 8, e: 11, d: 13, sg: -4, form: ['D', 'E', 'D', 'E', 'V'], logo: CRESTS['Internacional'] },
      { pos: 17, name: 'Grêmio', pts: 34, j: 32, v: 8, e: 10, d: 14, sg: -9, form: ['D', 'D', 'V', 'E', 'D'], logo: CRESTS['Grêmio'] },
      { pos: 18, name: 'Corinthians', pts: 33, j: 32, v: 8, e: 9, d: 15, sg: -8, form: ['D', 'V', 'D', 'D', 'E'], logo: CRESTS['Corinthians'] },
      { pos: 19, name: 'Remo', pts: 26, j: 32, v: 5, e: 11, d: 16, sg: -16, form: ['E', 'D', 'E', 'D', 'D'], logo: CRESTS['Remo'] },
      { pos: 20, name: 'Chapecoense', pts: 21, j: 31, v: 4, e: 9, d: 18, sg: -31, form: ['D', 'D', 'D', 'E', 'D'], logo: CRESTS['Chapecoense'] }
    ];

    const TOP_SCORERS = [
      { rank: 1, name: 'Pedro', team: 'Flamengo', goals: 18, logo: CRESTS['Flamengo'] },
      { rank: 2, name: 'Estêvão', team: 'Palmeiras', goals: 15, logo: CRESTS['Palmeiras'] },
      { rank: 3, name: 'Kaio Jorge', team: 'Cruzeiro', goals: 13, logo: CRESTS['Cruzeiro'] },
      { rank: 4, name: 'Hulk', team: 'Atlético-MG', goals: 12, logo: CRESTS['Atlético-MG'] },
      { rank: 5, name: 'Luciano', team: 'São Paulo', goals: 11, logo: CRESTS['São Paulo'] }
    ];

    function App() {
      // Authentication State
      const [isAuthenticated, setIsAuthenticated] = useState(false);
      const [authTab, setAuthTab] = useState('LOGIN');

      // Login/Signup Inputs
      const [inputName, setInputName] = useState('');
      const [inputEmail, setInputEmail] = useState('');
      const [inputPassword, setInputPassword] = useState('');
      const [selectedFavoriteTeam, setSelectedFavoriteTeam] = useState('Flamengo');

      // Profile State
      const [currentUser, setCurrentUser] = useState(null);

      // App State
      const [activeTab, setActiveTab] = useState('PALPITES');
      const [userPoints, setUserPoints] = useState(0);
      const [userPredictions, setUserPredictions] = useState({});
      const [savedStatus, setSavedStatus] = useState({});
      const [leaderboardUsers, setLeaderboardUsers] = useState([]);

      // Chat Messages
      const [chatMessages, setChatMessages] = useState([
        { id: 'c1', user: 'Sistema', team: 'Flamengo', text: 'Bem-vindo ao Chat Oficial do Brasileirão 2026! Crie sua conta para palpitar e entrar no Ranking.', time: '18:00', avatar: '🤖' }
      ]);
      const [newMessage, setNewMessage] = useState('');

      useEffect(() => {
        if (window.lucide) {
          window.lucide.createIcons();
        }
      });

      const handleAuthSubmit = (e) => {
        e.preventDefault();
        if (!inputEmail || !inputPassword) return;

        const userName = inputName.trim() || inputEmail.split('@')[0];
        const userObj = {
          name: userName,
          email: inputEmail,
          favoriteTeam: selectedFavoriteTeam,
          avatar: '⚽',
          joinedDate: '28/10/2026'
        };

        setCurrentUser(userObj);
        setIsAuthenticated(true);
        setUserPoints(0);
        setUserPredictions({});

        setLeaderboardUsers(prev => {
          const exists = prev.some(u => u.email === userObj.email);
          if (exists) return prev;
          return [
            ...prev,
            {
              name: userObj.name,
              email: userObj.email,
              team: userObj.favoriteTeam,
              pts: 0,
              exactCount: 0,
              accuracy: 0,
              avatar: userObj.avatar
            }
          ];
        });

        setChatMessages(prev => [
          ...prev,
          {
            id: Date.now().toString(),
            user: userName,
            team: selectedFavoriteTeam,
            text: `Olá galera! Acabei de entrar no app. Pra cima, ${selectedFavoriteTeam}! 🚀`,
            time: new Date().toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' }),
            avatar: '⚽'
          }
        ]);
      };

      const handleLogout = () => {
        setIsAuthenticated(false);
        setCurrentUser(null);
      };

      const handleScoreChange = (matchId, team, delta) => {
        setUserPredictions(prev => {
          const current = prev[matchId] || { home: 0, away: 0 };
          const newVal = Math.max(0, (current[team] || 0) + delta);
          return {
            ...prev,
            [matchId]: {
              ...current,
              [team]: newVal
            }
          };
        });
        setSavedStatus(prev => ({ ...prev, [matchId]: false }));
      };

      const handleSavePrediction = (matchId) => {
        setSavedStatus(prev => ({ ...prev, [matchId]: true }));
        setTimeout(() => {
          setSavedStatus(prev => ({ ...prev, [matchId]: false }));
        }, 2500);
      };

      const handleSendMessage = (e) => {
        e.preventDefault();
        if (!newMessage.trim() || !currentUser) return;
        const msg = {
          id: Date.now().toString(),
          user: currentUser.name,
          team: currentUser.favoriteTeam,
          text: newMessage,
          time: new Date().toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' }),
          avatar: currentUser.avatar
        };
        setChatMessages([...chatMessages, msg]);
        setNewMessage('');
      };

      // LOGIN SCREEN
      if (!isAuthenticated) {
        return (
          <div className="min-h-screen bg-[#0D1117] text-gray-100 flex items-center justify-center p-4">
            <div className="w-full max-w-md bg-[#161B22] rounded-3xl border border-gray-800 p-6 md:p-8 shadow-2xl space-y-6 relative overflow-hidden">
              <div className="text-center space-y-2">
                <div className="w-16 h-16 mx-auto rounded-2xl bg-gradient-to-tr from-[#00E676] to-[#FFD600] p-0.5 shadow-lg shadow-[#00E676]/20">
                  <div className="w-full h-full bg-[#0D1117] rounded-[14px] flex items-center justify-center">
                    <Icon name="trophy" className="w-8 h-8 text-[#00E676]" />
                  </div>
                </div>
                <h1 className="font-extrabold text-xl tracking-tight text-white">
                  Brasileirão <span className="text-[#00E676]">Stats</span> & <span className="text-[#FFD600]">Palpites</span>
                </h1>
                <p className="text-xs text-gray-400">Edição Série A 2026 • Entre para dar seus palpites</p>
              </div>

              <div className="grid grid-cols-2 p-1 bg-[#0D1117] rounded-xl border border-gray-800 text-xs font-bold">
                <button
                  type="button"
                  onClick={() => setAuthTab('LOGIN')}
                  className={`py-2.5 rounded-lg transition-all ${authTab === 'LOGIN' ? 'bg-[#21262D] text-[#00E676]' : 'text-gray-400'}`}
                >
                  Entrar
                </button>
                <button
                  type="button"
                  onClick={() => setAuthTab('REGISTER')}
                  className={`py-2.5 rounded-lg transition-all ${authTab === 'REGISTER' ? 'bg-[#21262D] text-[#00E676]' : 'text-gray-400'}`}
                >
                  Criar Conta
                </button>
              </div>

              <form onSubmit={handleAuthSubmit} className="space-y-4">
                {authTab === 'REGISTER' && (
                  <div>
                    <label className="block text-xs font-bold text-gray-300 mb-1">Nome Completo</label>
                    <input
                      type="text"
                      required
                      placeholder="Ex: Lucas Silva"
                      value={inputName}
                      onChange={(e) => setInputName(e.target.value)}
                      className="w-full bg-[#0D1117] border border-gray-800 rounded-xl px-3 py-2.5 text-xs text-white focus:outline-none focus:border-[#00E676]"
                    />
                  </div>
                )}

                <div>
                  <label className="block text-xs font-bold text-gray-300 mb-1">E-mail</label>
                  <input
                    type="email"
                    required
                    placeholder="seuemail@exemplo.com"
                    value={inputEmail}
                    onChange={(e) => setInputEmail(e.target.value)}
                    className="w-full bg-[#0D1117] border border-gray-800 rounded-xl px-3 py-2.5 text-xs text-white focus:outline-none focus:border-[#00E676]"
                  />
                </div>

                <div>
                  <label className="block text-xs font-bold text-gray-300 mb-1">Senha</label>
                  <input
                    type="password"
                    required
                    minLength={6}
                    placeholder="••••••••"
                    value={inputPassword}
                    onChange={(e) => setInputPassword(e.target.value)}
                    className="w-full bg-[#0D1117] border border-gray-800 rounded-xl px-3 py-2.5 text-xs text-white focus:outline-none focus:border-[#00E676]"
                  />
                </div>

                <div>
                  <label className="block text-xs font-bold text-gray-300 mb-1">Time do Coração</label>
                  <div className="bg-[#0D1117] border border-gray-800 rounded-xl p-2.5 max-h-36 overflow-y-auto grid grid-cols-2 gap-2">
                    {TEAMS_LIST.map((team) => (
                      <button
                        key={team}
                        type="button"
                        onClick={() => setSelectedFavoriteTeam(team)}
                        className={`flex items-center gap-2 p-2 rounded-lg border text-left transition-all text-xs font-bold ${
                          selectedFavoriteTeam === team ? 'bg-[#00E676]/10 border-[#00E676] text-[#00E676]' : 'bg-[#161B22] border-gray-800 text-gray-300'
                        }`}
                      >
                        <img src={CRESTS[team]} alt={team} className="w-5 h-5 object-contain" />
                        <span className="truncate">{team}</span>
                      </button>
                    ))}
                  </div>
                </div>

                <button
                  type="submit"
                  className="w-full py-3 bg-[#00E676] hover:bg-[#00C853] text-black font-extrabold text-xs rounded-xl shadow-lg shadow-[#00E676]/20 transition-all flex items-center justify-center gap-2 mt-2"
                >
                  {authTab === 'LOGIN' ? 'Entrar na Plataforma' : 'Criar Minha Conta'}
                </button>
              </form>
            </div>
          </div>
        );
      }

      // MAIN APP AFTER LOGIN
      return (
        <div className="min-h-screen bg-[#0D1117] text-gray-100 flex flex-col">
          {/* HEADER */}
          <header className="sticky top-0 z-50 bg-[#161B22]/95 backdrop-blur-md border-b border-gray-800 px-4 py-3">
            <div className="max-w-7xl mx-auto flex items-center justify-between gap-3">
              <div className="flex items-center gap-3">
                <div className="w-10 h-10 rounded-xl bg-gradient-to-tr from-[#00E676] to-[#FFD600] p-0.5 flex items-center justify-center">
                  <div className="w-full h-full bg-[#0D1117] rounded-[10px] flex items-center justify-center">
                    <Icon name="trophy" className="w-5 h-5 text-[#00E676]" />
                  </div>
                </div>
                <div>
                  <h1 className="font-extrabold text-base leading-tight">
                    BRASILEIRÃO <span className="text-[#00E676]">STATS</span> & <span className="text-[#FFD600]">PALPITES</span>
                  </h1>
                  <p className="text-[10px] text-gray-400">Edição 2026 • Rodada 33 (28/10/2026)</p>
                </div>
              </div>

              <div className="flex items-center gap-3 bg-[#0D1117] p-1.5 rounded-2xl border border-gray-800">
                <div className="flex items-center gap-2 pl-2">
                  <div className="w-7 h-7 rounded-lg bg-[#21262D] border border-gray-700 flex items-center justify-center text-xs">
                    {currentUser.avatar}
                  </div>
                  <div className="text-left leading-tight hidden sm:block">
                    <div className="font-bold text-xs text-gray-200 flex items-center gap-1">
                      <span>{currentUser.name}</span>
                      <img src={CRESTS[currentUser.favoriteTeam]} className="w-3.5 h-3.5 object-contain" />
                    </div>
                    <div className="text-[10px] text-[#00E676] font-bold">{userPoints} Pts</div>
                  </div>
                </div>

                <button
                  onClick={handleLogout}
                  className="p-1.5 text-gray-400 hover:text-red-400 rounded-xl transition-all"
                  title="Sair"
                >
                  <Icon name="log-out" className="w-4 h-4" />
                </button>
              </div>
            </div>
          </header>

          {/* MAIN CONTENT */}
          <main className="flex-1 max-w-7xl w-full mx-auto p-3 md:p-6 pb-12">
            {/* TABS */}
            <div className="grid grid-cols-4 gap-2 bg-[#161B22] p-1.5 rounded-2xl border border-gray-800 mb-6">
              <button
                onClick={() => setActiveTab('PALPITES')}
                className={`py-2.5 px-3 rounded-xl font-bold text-xs transition-all flex items-center justify-center gap-2 ${
                  activeTab === 'PALPITES' ? 'bg-[#21262D] text-[#00E676] border border-[#00E676]/30' : 'text-gray-400'
                }`}
              >
                <Icon name="flame" className="w-4 h-4 text-[#FFD600]" />
                <span className="hidden sm:inline">Palpites</span>
              </button>

              <button
                onClick={() => setActiveTab('TABELA')}
                className={`py-2.5 px-3 rounded-xl font-bold text-xs transition-all flex items-center justify-center gap-2 ${
                  activeTab === 'TABELA' ? 'bg-[#21262D] text-[#00E676] border border-[#00E676]/30' : 'text-gray-400'
                }`}
              >
                <Icon name="bar-chart-3" className="w-4 h-4 text-[#00E676]" />
                <span className="hidden sm:inline">Tabela 2026</span>
              </button>

              <button
                onClick={() => setActiveTab('IA')}
                className={`py-2.5 px-3 rounded-xl font-bold text-xs transition-all flex items-center justify-center gap-2 ${
                  activeTab === 'IA' ? 'bg-[#21262D] text-[#00E676] border border-[#00E676]/30' : 'text-gray-400'
                }`}
              >
                <Icon name="bot" className="w-4 h-4 text-cyan-400" />
                <span className="hidden sm:inline">IA Gemini</span>
              </button>

              <button
                onClick={() => setActiveTab('PERFIL')}
                className={`py-2.5 px-3 rounded-xl font-bold text-xs transition-all flex items-center justify-center gap-2 ${
                  activeTab === 'PERFIL' ? 'bg-[#21262D] text-[#00E676] border border-[#00E676]/30' : 'text-gray-400'
                }`}
              >
                <Icon name="user" className="w-4 h-4 text-purple-400" />
                <span className="hidden sm:inline">Perfil</span>
              </button>
            </div>

            {/* TAB 1: PALPITES */}
            {activeTab === 'PALPITES' && (
              <div className="grid grid-cols-1 lg:grid-cols-3 gap-6">
                <div className="lg:col-span-2 space-y-4">
                  {INITIAL_MATCHES.map((match) => {
                    const pred = userPredictions[match.id] || { home: 0, away: 0 };
                    const isSaved = savedStatus[match.id];

                    return (
                      <div key={match.id} className="bg-[#161B22] rounded-2xl border border-gray-800 p-4 space-y-3">
                        <div className="flex items-center justify-between text-xs text-gray-400">
                          <span className="text-[#FFD600] font-bold">{match.date}</span>
                          <span>{match.stadium}</span>
                        </div>

                        <div className="flex items-center justify-between gap-2 bg-[#0D1117] p-3 rounded-xl border border-gray-800">
                          <div className="flex items-center gap-2 flex-1 justify-end">
                            <span className="font-bold text-xs sm:text-sm text-right">{match.homeTeam}</span>
                            <img src={match.homeLogo} className="w-7 h-7 object-contain" />
                          </div>

                          <div className="flex items-center gap-2">
                            <div className="flex flex-col items-center gap-1">
                              <button onClick={() => handleScoreChange(match.id, 'home', 1)} className="text-xs bg-[#21262D] w-6 h-5 rounded font-bold">+</button>
                              <span className="w-7 h-7 rounded bg-[#21262D] font-extrabold flex items-center justify-center text-[#00E676]">{pred.home}</span>
                              <button onClick={() => handleScoreChange(match.id, 'home', -1)} className="text-xs bg-[#21262D] w-6 h-5 rounded font-bold">-</button>
                            </div>
                            <span className="text-xs font-bold text-gray-500">X</span>
                            <div className="flex flex-col items-center gap-1">
                              <button onClick={() => handleScoreChange(match.id, 'away', 1)} className="text-xs bg-[#21262D] w-6 h-5 rounded font-bold">+</button>
                              <span className="w-7 h-7 rounded bg-[#21262D] font-extrabold flex items-center justify-center text-[#00E676]">{pred.away}</span>
                              <button onClick={() => handleScoreChange(match.id, 'away', -1)} className="text-xs bg-[#21262D] w-6 h-5 rounded font-bold">-</button>
                            </div>
                          </div>

                          <div className="flex items-center gap-2 flex-1">
                            <img src={match.awayLogo} className="w-7 h-7 object-contain" />
                            <span className="font-bold text-xs sm:text-sm">{match.awayTeam}</span>
                          </div>
                        </div>

                        <button
                          onClick={() => handleSavePrediction(match.id)}
                          className={`w-full py-2 rounded-xl font-bold text-xs transition-all ${
                            isSaved ? 'bg-emerald-600 text-white' : 'bg-[#00E676] text-black hover:bg-[#00C853]'
                          }`}
                        >
                          {isSaved ? 'Palpite Salvo!' : 'Salvar Palpite'}
                        </button>
                      </div>
                    );
                  })}
                </div>

                {/* SIDEBAR: CHAT & RANKING */}
                <div className="space-y-6">
                  {/* CHAT */}
                  <div className="bg-[#161B22] rounded-2xl border border-gray-800 p-4 h-[350px] flex flex-col">
                    <h3 className="font-bold text-xs mb-3 text-gray-300">Resenha dos Torcedores</h3>
                    <div className="flex-1 overflow-y-auto space-y-2 pr-1 text-xs">
                      {chatMessages.map((msg) => (
                        <div key={msg.id} className="bg-[#0D1117] p-2 rounded-xl border border-gray-800">
                          <div className="flex justify-between text-[10px] text-gray-400 mb-1">
                            <span className="font-bold text-gray-200 flex items-center gap-1">
                              {msg.user}
                              {msg.team && <img src={CRESTS[msg.team]} className="w-3 h-3 inline" />}
                            </span>
                            <span>{msg.time}</span>
                          </div>
                          <p className="text-gray-300">{msg.text}</p>
                        </div>
                      ))}
                    </div>

                    <form onSubmit={handleSendMessage} className="flex gap-2 pt-2">
                      <input
                        type="text"
                        placeholder="Comentar..."
                        value={newMessage}
                        onChange={(e) => setNewMessage(e.target.value)}
                        className="flex-1 bg-[#0D1117] border border-gray-700 rounded-xl px-3 py-1.5 text-xs focus:outline-none focus:border-[#00E676]"
                      />
                      <button type="submit" className="bg-[#00E676] text-black px-3 rounded-xl font-bold text-xs">
                        Enviar
                      </button>
                    </form>
                  </div>

                  {/* RANKING */}
                  <div className="bg-[#161B22] rounded-2xl border border-gray-800 p-4">
                    <h3 className="font-bold text-xs mb-3 text-[#FFD600]">Ranking dos Palpitantes</h3>
                    <div className="space-y-2 text-xs">
                      {leaderboardUsers.map((user, idx) => (
                        <div key={user.email} className="flex items-center justify-between bg-[#0D1117] p-2 rounded-xl border border-gray-800">
                          <div className="flex items-center gap-2">
                            <span className="font-bold text-[#FFD600]">#{idx + 1}</span>
                            <span>{user.name}</span>
                            <img src={CRESTS[user.team]} className="w-3.5 h-3.5 object-contain" />
                          </div>
                          <span className="font-extrabold text-[#00E676]">{user.pts} pts</span>
                        </div>
                      ))}
                    </div>
                  </div>
                </div>
              </div>
            )}

            {/* TAB 2: TABELA */}
            {activeTab === 'TABELA' && (
              <div className="bg-[#161B22] rounded-2xl border border-gray-800 p-4 overflow-x-auto space-y-4">
                <h3 className="font-bold text-sm text-gray-100">Tabela Série A (28/10/2026)</h3>
                <table className="w-full text-left text-xs">
                  <thead>
                    <tr className="border-b border-gray-800 text-gray-400 font-bold uppercase text-[10px]">
                      <th className="py-2 px-2 text-center">Pos</th>
                      <th className="py-2 px-2">Clube</th>
                      <th className="py-2 px-2 text-center">Pts</th>
                      <th className="py-2 px-2 text-center">J</th>
                      <th className="py-2 px-2 text-center">V</th>
                      <th className="py-2 px-2 text-center">SG</th>
                    </tr>
                  </thead>
                  <tbody className="divide-y divide-gray-800/60 font-medium">
                    {INITIAL_STANDINGS.map((team) => (
                      <tr key={team.name} className="hover:bg-[#21262D]">
                        <td className="py-2 px-2 text-center font-bold">{team.pos}º</td>
                        <td className="py-2 px-2 font-bold flex items-center gap-2">
                          <img src={team.logo} className="w-5 h-5 object-contain" />
                          <span>{team.name}</span>
                        </td>
                        <td className="py-2 px-2 text-center font-bold text-[#00E676]">{team.pts}</td>
                        <td className="py-2 px-2 text-center text-gray-400">{team.j}</td>
                        <td className="py-2 px-2 text-center">{team.v}</td>
                        <td className="py-2 px-2 text-center">{team.sg > 0 ? `+${team.sg}` : team.sg}</td>
                      </tr>
                    ))}
                  </tbody>
                </table>
              </div>
            )}

            {/* TAB 3: IA */}
            {activeTab === 'IA' && (
              <div className="grid grid-cols-1 md:grid-cols-2 gap-4">
                {INITIAL_MATCHES.map((match) => (
                  <div key={match.id} className="bg-[#161B22] rounded-2xl border border-gray-800 p-4 space-y-3">
                    <div className="flex items-center justify-between text-xs font-bold border-b border-gray-800 pb-2">
                      <div className="flex items-center gap-2">
                        <img src={match.homeLogo} className="w-5 h-5 object-contain" />
                        <span>{match.homeTeam}</span>
                      </div>
                      <span className="text-[#00E676] bg-[#0D1117] px-2 py-1 rounded">
                        IA: {match.aiPrediction.home} x {match.aiPrediction.away}
                      </span>
                      <div className="flex items-center gap-2">
                        <span>{match.awayTeam}</span>
                        <img src={match.awayLogo} className="w-5 h-5 object-contain" />
                      </div>
                    </div>
                    <p className="text-xs text-gray-300 bg-[#0D1117] p-3 rounded-xl border border-gray-800">
                      {match.aiPrediction.reasoning}
                    </p>
                  </div>
                ))}
              </div>
            )}

            {/* TAB 4: PERFIL */}
            {activeTab === 'PERFIL' && (
              <div className="max-w-md mx-auto bg-[#161B22] rounded-3xl border border-gray-800 p-6 space-y-4 text-center">
                <div className="w-20 h-20 mx-auto rounded-full bg-[#0D1117] border border-gray-800 flex items-center justify-center text-3xl">
                  {currentUser.avatar}
                </div>
                <div>
                  <h2 className="font-bold text-lg text-gray-100">{currentUser.name}</h2>
                  <p className="text-xs text-gray-400">{currentUser.email}</p>
                </div>
                <div className="flex justify-center items-center gap-2 bg-[#0D1117] p-2 rounded-xl border border-gray-800 text-xs">
                  <span className="text-gray-400">Time:</span>
                  <img src={CRESTS[currentUser.favoriteTeam]} className="w-4 h-4 object-contain" />
                  <span className="font-bold">{currentUser.favoriteTeam}</span>
                </div>
                <button
                  onClick={handleLogout}
                  className="w-full py-2.5 bg-red-500/10 text-red-400 border border-red-500/30 rounded-xl font-bold text-xs"
                >
                  Sair da Conta
                </button>
              </div>
            )}
          </main>
        </div>
      );
    }

    ReactDOM.createRoot(document.getElementById('root')).render(<App />);
  </script>
</body>
</html>