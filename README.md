<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>💘 Quel(le) partenaire tu mérites ?</title>
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@700;900&family=DM+Sans:wght@300;400;500;600&display=swap" rel="stylesheet">
<style>
  :root {
    --pink: #FF3CAC;
    --violet: #784BA0;
    --blue: #2B86C5;
    --gold: #FFD700;
    --dark: #0d0d1a;
    --card: rgba(255,255,255,0.07);
    --border: rgba(255,255,255,0.12);
  }

  * { margin: 0; padding: 0; box-sizing: border-box; }

  body {
    font-family: 'DM Sans', sans-serif;
    background: var(--dark);
    min-height: 100vh;
    overflow-x: hidden;
    color: #fff;
  }

  /* Animated background */
  .bg {
    position: fixed; inset: 0; z-index: 0;
    background: radial-gradient(ellipse at 20% 50%, #FF3CAC33 0%, transparent 50%),
                radial-gradient(ellipse at 80% 20%, #2B86C533 0%, transparent 50%),
                radial-gradient(ellipse at 60% 80%, #784BA033 0%, transparent 50%),
                #0d0d1a;
    animation: bgPulse 8s ease-in-out infinite alternate;
  }
  @keyframes bgPulse {
    0% { filter: hue-rotate(0deg); }
    100% { filter: hue-rotate(30deg); }
  }

  /* Floating particles */
  .particles { position: fixed; inset: 0; z-index: 0; pointer-events: none; }
  .particle {
    position: absolute;
    width: 4px; height: 4px;
    border-radius: 50%;
    background: var(--pink);
    animation: float linear infinite;
    opacity: 0.4;
  }
  @keyframes float {
    0% { transform: translateY(100vh) rotate(0deg); opacity: 0; }
    10% { opacity: 0.4; }
    90% { opacity: 0.4; }
    100% { transform: translateY(-10vh) rotate(720deg); opacity: 0; }
  }

  .container {
    position: relative; z-index: 1;
    max-width: 680px;
    margin: 0 auto;
    padding: 20px 16px 60px;
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
  }

  /* SCREEN management */
  .screen { width: 100%; display: none; animation: fadeUp 0.6s ease; }
  .screen.active { display: flex; flex-direction: column; align-items: center; }
  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(30px); }
    to { opacity: 1; transform: translateY(0); }
  }

  /* ===== WELCOME SCREEN ===== */
  .logo-emoji { font-size: 72px; animation: heartbeat 1.5s ease-in-out infinite; }
  @keyframes heartbeat {
    0%,100% { transform: scale(1); }
    50% { transform: scale(1.15); }
  }

  h1 {
    font-family: 'Playfair Display', serif;
    font-size: clamp(2rem, 7vw, 3.2rem);
    font-weight: 900;
    text-align: center;
    margin: 16px 0 8px;
    background: linear-gradient(135deg, #FF3CAC, #FFD700, #2B86C5);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
    line-height: 1.2;
  }

  .subtitle {
    text-align: center;
    color: rgba(255,255,255,0.6);
    font-size: 1rem;
    margin-bottom: 32px;
    line-height: 1.6;
  }

  /* Gender selector */
  .gender-title {
    font-size: 0.85rem;
    text-transform: uppercase;
    letter-spacing: 2px;
    color: rgba(255,255,255,0.4);
    margin-bottom: 16px;
  }

  .gender-cards {
    display: flex;
    gap: 16px;
    margin-bottom: 32px;
    width: 100%;
    justify-content: center;
  }

  .gender-card {
    flex: 1; max-width: 160px;
    background: var(--card);
    border: 2px solid var(--border);
    border-radius: 20px;
    padding: 24px 16px;
    text-align: center;
    cursor: pointer;
    transition: all 0.3s ease;
  }
  .gender-card:hover { transform: translateY(-4px); border-color: var(--pink); }
  .gender-card.selected {
    border-color: var(--pink);
    background: rgba(255, 60, 172, 0.15);
    box-shadow: 0 0 30px rgba(255, 60, 172, 0.3);
  }
  .gender-card .icon { font-size: 40px; margin-bottom: 8px; }
  .gender-card .label { font-weight: 600; font-size: 0.95rem; }

  /* Buttons */
  .btn-main {
    background: linear-gradient(135deg, #FF3CAC, #784BA0, #2B86C5);
    color: #fff;
    border: none;
    border-radius: 50px;
    padding: 16px 48px;
    font-family: 'DM Sans', sans-serif;
    font-size: 1.1rem;
    font-weight: 600;
    cursor: pointer;
    transition: all 0.3s ease;
    box-shadow: 0 8px 32px rgba(255, 60, 172, 0.4);
    background-size: 200% 200%;
    animation: gradientShift 3s ease infinite;
  }
  @keyframes gradientShift {
    0% { background-position: 0% 50%; }
    50% { background-position: 100% 50%; }
    100% { background-position: 0% 50%; }
  }
  .btn-main:hover { transform: scale(1.05); box-shadow: 0 12px 40px rgba(255, 60, 172, 0.6); }
  .btn-main:disabled { opacity: 0.4; cursor: not-allowed; transform: none; }

  /* ===== QUIZ SCREEN ===== */
  .progress-bar-wrap {
    width: 100%;
    height: 4px;
    background: rgba(255,255,255,0.1);
    border-radius: 10px;
    margin-bottom: 32px;
    overflow: hidden;
  }
  .progress-bar {
    height: 100%;
    background: linear-gradient(90deg, #FF3CAC, #2B86C5);
    border-radius: 10px;
    transition: width 0.5s cubic-bezier(0.4,0,0.2,1);
  }

  .question-counter {
    font-size: 0.8rem;
    text-transform: uppercase;
    letter-spacing: 2px;
    color: rgba(255,255,255,0.4);
    margin-bottom: 12px;
    align-self: flex-start;
  }

  .question-text {
    font-family: 'Playfair Display', serif;
    font-size: clamp(1.3rem, 5vw, 1.9rem);
    font-weight: 700;
    line-height: 1.4;
    margin-bottom: 28px;
    align-self: flex-start;
  }

  .options-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 12px;
    width: 100%;
    margin-bottom: 24px;
  }

  .option-btn {
    background: var(--card);
    border: 2px solid var(--border);
    border-radius: 16px;
    padding: 18px 14px;
    color: #fff;
    font-family: 'DM Sans', sans-serif;
    font-size: 0.95rem;
    font-weight: 500;
    cursor: pointer;
    transition: all 0.25s ease;
    text-align: left;
    line-height: 1.4;
    backdrop-filter: blur(10px);
  }
  .option-btn:hover { background: rgba(255,255,255,0.12); border-color: var(--pink); transform: translateY(-2px); }
  .option-btn.selected {
    border-color: var(--pink);
    background: rgba(255, 60, 172, 0.2);
    box-shadow: 0 0 20px rgba(255, 60, 172, 0.2);
  }
  .option-emoji { display: block; font-size: 22px; margin-bottom: 6px; }

  .btn-next {
    background: linear-gradient(135deg, #FF3CAC, #784BA0);
    color: #fff;
    border: none;
    border-radius: 50px;
    padding: 14px 40px;
    font-family: 'DM Sans', sans-serif;
    font-size: 1rem;
    font-weight: 600;
    cursor: pointer;
    transition: all 0.3s ease;
    align-self: flex-end;
  }
  .btn-next:hover { transform: scale(1.05); }
  .btn-next:disabled { opacity: 0.3; cursor: not-allowed; transform: none; }

  /* ===== LOADING SCREEN ===== */
  .loading-screen {
    text-align: center;
    gap: 20px;
  }
  .loading-orb {
    width: 100px; height: 100px;
    border-radius: 50%;
    background: conic-gradient(#FF3CAC, #784BA0, #2B86C5, #FF3CAC);
    animation: spin 1.5s linear infinite;
    margin: 20px auto;
    box-shadow: 0 0 40px rgba(255, 60, 172, 0.5);
  }
  @keyframes spin { to { transform: rotate(360deg); } }
  .loading-text {
    font-family: 'Playfair Display', serif;
    font-size: 1.5rem;
    color: rgba(255,255,255,0.8);
  }
  .loading-sub { color: rgba(255,255,255,0.4); font-size: 0.9rem; }

  /* ===== RESULT SCREEN ===== */
  .result-screen { text-align: center; gap: 16px; }

  .result-badge {
    display: inline-block;
    background: linear-gradient(135deg, #FF3CAC, #FFD700);
    border-radius: 50px;
    padding: 6px 20px;
    font-size: 0.8rem;
    font-weight: 600;
    text-transform: uppercase;
    letter-spacing: 2px;
    margin-bottom: 8px;
  }

  .result-image-wrap {
    width: 200px; height: 200px;
    border-radius: 50%;
    margin: 0 auto;
    background: linear-gradient(135deg, #FF3CAC44, #2B86C544);
    border: 3px solid rgba(255, 60, 172, 0.5);
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 80px;
    box-shadow: 0 0 60px rgba(255, 60, 172, 0.3);
    animation: glowPulse 2s ease-in-out infinite;
    position: relative;
    overflow: hidden;
  }
  @keyframes glowPulse {
    0%,100% { box-shadow: 0 0 40px rgba(255, 60, 172, 0.3); }
    50% { box-shadow: 0 0 80px rgba(255, 60, 172, 0.6); }
  }
  .result-image-wrap img {
    width: 100%; height: 100%;
    object-fit: cover;
    border-radius: 50%;
  }

  .result-name {
    font-family: 'Playfair Display', serif;
    font-size: clamp(1.8rem, 7vw, 2.8rem);
    font-weight: 900;
    background: linear-gradient(135deg, #FF3CAC, #FFD700);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
  }

  .result-desc {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 20px;
    padding: 20px 24px;
    text-align: left;
    line-height: 1.8;
    color: rgba(255,255,255,0.85);
    font-size: 0.95rem;
    width: 100%;
  }

  .result-traits {
    display: flex;
    flex-wrap: wrap;
    gap: 8px;
    justify-content: center;
    width: 100%;
  }
  .trait-tag {
    background: rgba(255, 60, 172, 0.15);
    border: 1px solid rgba(255, 60, 172, 0.3);
    border-radius: 50px;
    padding: 6px 16px;
    font-size: 0.85rem;
    color: #FF3CAC;
    font-weight: 500;
  }

  .result-compatibility {
    width: 100%;
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 16px;
    padding: 16px 20px;
  }
  .compat-label {
    font-size: 0.75rem;
    text-transform: uppercase;
    letter-spacing: 2px;
    color: rgba(255,255,255,0.4);
    margin-bottom: 8px;
  }
  .compat-bar-wrap {
    height: 8px;
    background: rgba(255,255,255,0.1);
    border-radius: 10px;
    overflow: hidden;
  }
  .compat-bar {
    height: 100%;
    background: linear-gradient(90deg, #FF3CAC, #FFD700);
    border-radius: 10px;
    transition: width 1.5s cubic-bezier(0.4,0,0.2,1);
  }
  .compat-percent {
    font-size: 1.4rem;
    font-weight: 700;
    color: #FFD700;
    margin-top: 6px;
  }

  .btn-retry {
    background: transparent;
    border: 2px solid rgba(255,255,255,0.2);
    color: rgba(255,255,255,0.6);
    border-radius: 50px;
    padding: 12px 32px;
    font-family: 'DM Sans', sans-serif;
    font-size: 0.95rem;
    cursor: pointer;
    transition: all 0.3s;
    margin-top: 8px;
  }
  .btn-retry:hover { border-color: var(--pink); color: #fff; }

  /* Confetti */
  .confetti-piece {
    position: fixed;
    width: 8px; height: 8px;
    border-radius: 2px;
    animation: confettiFall linear forwards;
    z-index: 100;
    pointer-events: none;
  }
  @keyframes confettiFall {
    0% { transform: translateY(-20px) rotate(0deg); opacity: 1; }
    100% { transform: translateY(100vh) rotate(720deg); opacity: 0; }
  }
</style>
</head>
<body>

<div class="bg"></div>
<div class="particles" id="particles"></div>

<div class="container">

  <!-- WELCOME SCREEN -->
  <div class="screen active" id="screen-welcome">
    <div class="logo-emoji">💘</div>
    <h1>Quel(le) partenaire tu mérites vraiment ?</h1>
    <p class="subtitle">Réponds à 10 questions sincères et découvre le profil de ton partenaire idéal — avec son prénom et sa personnalité !</p>
    
    <p class="gender-title">Tu es ?</p>
    <div class="gender-cards">
      <div class="gender-card" id="gc-homme" onclick="selectGender('homme')">
        <div class="icon">👨</div>
        <div class="label">Un homme</div>
      </div>
      <div class="gender-card" id="gc-femme" onclick="selectGender('femme')">
        <div class="icon">👩</div>
        <div class="label">Une femme</div>
      </div>
    </div>

    <button class="btn-main" id="btn-start" onclick="startQuiz()" disabled>
      Découvrir mon partenaire 💫
    </button>
  </div>

  <!-- QUIZ SCREEN -->
  <div class="screen" id="screen-quiz">
    <div class="progress-bar-wrap">
      <div class="progress-bar" id="progress-bar" style="width:0%"></div>
    </div>
    <p class="question-counter" id="q-counter">Question 1 / 10</p>
    <p class="question-text" id="q-text"></p>
    <div class="options-grid" id="options-grid"></div>
    <button class="btn-next" id="btn-next" onclick="nextQuestion()" disabled>Suivant →</button>
  </div>

  <!-- LOADING SCREEN -->
  <div class="screen loading-screen" id="screen-loading">
    <div class="loading-orb"></div>
    <p class="loading-text" id="loading-text">Analyse de ta personnalité...</p>
    <p class="loading-sub">Notre IA cherche ton match parfait ✨</p>
  </div>

  <!-- RESULT SCREEN -->
  <div class="screen result-screen" id="screen-result">
    <div class="result-badge">✨ Ton partenaire idéal</div>
    <div class="result-image-wrap" id="result-avatar"></div>
    <div class="result-name" id="result-name"></div>
    <div class="result-desc" id="result-desc"></div>
    <div class="result-traits" id="result-traits"></div>
    <div class="result-compatibility">
      <div class="compat-label">🔥 Compatibilité avec toi</div>
      <div class="compat-bar-wrap">
        <div class="compat-bar" id="compat-bar" style="width:0%"></div>
      </div>
      <div class="compat-percent" id="compat-percent">0%</div>
    </div>
    <button class="btn-main" onclick="shareResult()">Partager mon résultat 📤</button>
    <button class="btn-retry" onclick="restart()">↺ Refaire le quiz</button>
  </div>

</div>

<script>
// ============ PARTICLES ============
(function() {
  const container = document.getElementById('particles');
  const colors = ['#FF3CAC','#2B86C5','#FFD700','#784BA0'];
  for (let i = 0; i < 30; i++) {
    const p = document.createElement('div');
    p.className = 'particle';
    p.style.left = Math.random() * 100 + 'vw';
    p.style.background = colors[Math.floor(Math.random() * colors.length)];
    p.style.animationDuration = (8 + Math.random() * 12) + 's';
    p.style.animationDelay = (Math.random() * 10) + 's';
    p.style.width = p.style.height = (2 + Math.random() * 4) + 'px';
    container.appendChild(p);
  }
})();

// ============ STATE ============
let userGender = null;
let currentQ = 0;
let answers = [];
let selectedOption = null;

// ============ QUESTIONS ============
const questions = [
  {
    text: "Dans une relation, ce qui compte le plus pour toi c'est...",
    options: [
      { emoji: "💬", text: "La communication profonde", value: "A" },
      { emoji: "🔥", text: "La passion et l'intensité", value: "B" },
      { emoji: "🤝", text: "La stabilité et la confiance", value: "C" },
      { emoji: "🌍", text: "Partager des aventures", value: "D" }
    ]
  },
  {
    text: "Ton week-end idéal ressemble à...",
    options: [
      { emoji: "🏠", text: "Rester à la maison, calme & cozy", value: "A" },
      { emoji: "🎉", text: "Sortir, musique, ambiance", value: "B" },
      { emoji: "🌿", text: "Nature, balade, air frais", value: "C" },
      { emoji: "📚", text: "Apprendre quelque chose de nouveau", value: "D" }
    ]
  },
  {
    text: "En amour, tu es plutôt le genre à...",
    options: [
      { emoji: "💝", text: "Tout donner, cœur à l'envers", value: "A" },
      { emoji: "😎", text: "Garder un peu de mystère", value: "B" },
      { emoji: "🤗", text: "Être protecteur(trice)", value: "C" },
      { emoji: "🎭", text: "Surprendre à tout moment", value: "D" }
    ]
  },
  {
    text: "Quelle qualité tu cherches ABSOLUMENT chez l'autre ?",
    options: [
      { emoji: "🧠", text: "L'intelligence et la sagesse", value: "A" },
      { emoji: "😂", text: "L'humour et la légèreté", value: "B" },
      { emoji: "💪", text: "L'ambition et la détermination", value: "C" },
      { emoji: "🎨", text: "La créativité et l'originalité", value: "D" }
    ]
  },
  {
    text: "Comment tu gères les conflits dans une relation ?",
    options: [
      { emoji: "🗣️", text: "On en parle calmement", value: "A" },
      { emoji: "❄️", text: "J'ai besoin d'un moment seul(e)", value: "B" },
      { emoji: "🤜🤛", text: "On règle ça directement", value: "C" },
      { emoji: "💌", text: "J'écris ce que je ressens", value: "D" }
    ]
  },
  {
    text: "Pour toi, la romance c'est...",
    options: [
      { emoji: "🕯️", text: "Dîner aux chandelles, fleurs, douceur", value: "A" },
      { emoji: "✈️", text: "Voyage surprise, aventure", value: "B" },
      { emoji: "🎮", text: "Soirée jeux, rires, simplicité", value: "C" },
      { emoji: "🌙", text: "Longues discussions sous les étoiles", value: "D" }
    ]
  },
  {
    text: "Ton plus grand défaut dans une relation ?",
    options: [
      { emoji: "😰", text: "Je suis trop jaloux(se)", value: "A" },
      { emoji: "🌀", text: "Je suis trop indépendant(e)", value: "B" },
      { emoji: "💭", text: "Je pense trop, j'analyse tout", value: "C" },
      { emoji: "🎭", text: "Je suis trop impulsif(ve)", value: "D" }
    ]
  },
  {
    text: "Dans 5 ans, tu vois ta vie comment ?",
    options: [
      { emoji: "👨‍👩‍👧", text: "Famille, maison, stabilité", value: "A" },
      { emoji: "🚀", text: "Carrière au sommet, succès", value: "B" },
      { emoji: "🌍", text: "Voyages, liberté, monde entier", value: "C" },
      { emoji: "🎨", text: "Passion, art, créativité", value: "D" }
    ]
  },
  {
    text: "Ce qui te fait craquer instantanément chez quelqu'un ?",
    options: [
      { emoji: "😊", text: "Un beau sourire sincère", value: "A" },
      { emoji: "🧠", text: "Une intelligence qui brille", value: "B" },
      { emoji: "💃", text: "Une confiance naturelle", value: "C" },
      { emoji: "❤️", text: "Une gentillesse authentique", value: "D" }
    ]
  },
  {
    text: "La phrase qui te décrit le mieux en amour ?",
    options: [
      { emoji: "🌹", text: "\"Tout ou rien, je ne fais pas les choses à moitié\"", value: "A" },
      { emoji: "🦋", text: "\"J'aime l'amour libre et sans pression\"", value: "B" },
      { emoji: "🏡", text: "\"Je construis pour durer\"", value: "C" },
      { emoji: "✨", text: "\"Chaque jour est une nouvelle surprise\"", value: "D" }
    ]
  }
];

// ============ PROFILES ============
const profiles = {
  homme: {
    AA: { name: "Yasmine", emoji: "👸", desc: "Yasmine est une femme douce, intelligente et profondément loyale. Elle aime les discussions sincères et sait écouter comme personne. Elle est le genre à te laisser un message le matin pour te souhaiter une belle journée. Avec elle, tu te sens vraiment compris.", traits: ["Douce", "Loyale", "Romantique", "Empathique"], compat: 97 },
    BB: { name: "Aïcha", emoji: "💃", desc: "Aïcha c'est l'énergie pure ! Elle sait mettre de la vie dans chaque pièce où elle entre. Passionnée, drôle, et directe, elle ne s'ennuie jamais et s'assure que toi non plus. Une relation avec elle, c'est une aventure quotidienne.", traits: ["Passionnée", "Directe", "Fun", "Spontanée"], compat: 94 },
    CC: { name: "Fatou", emoji: "🌺", desc: "Fatou est une femme de caractère, ambitieuse et bienveillante à la fois. Elle te pousse à te dépasser tout en étant ton refuge. Mature, stable, elle sait ce qu'elle veut et n'a pas peur de le construire avec toi.", traits: ["Ambitieuse", "Stable", "Protectrice", "Forte"], compat: 95 },
    DD: { name: "Léa", emoji: "🎨", desc: "Léa voit le monde comme une toile blanche. Créative, originale, elle rend chaque instant unique. Elle t'emmènera dans des endroits que tu n'aurais jamais découvert seul. Avec elle, la routine n'existe pas.", traits: ["Créative", "Libre", "Originale", "Artiste"], compat: 92 }
  },
  femme: {
    AA: { name: "Karim", emoji: "🤴", desc: "Karim est un homme doux et attentionné, mais avec un cœur de lion. Il écoute vraiment, se souvient de chaque détail et sait te faire sentir unique. Fidèle et romantique, il ne joue pas avec les sentiments.", traits: ["Attentionné", "Fidèle", "Romantique", "Doux"], compat: 97 },
    BB: { name: "Marcus", emoji: "🕶️", desc: "Marcus dégage une confiance naturelle et une énergie contagieuse. Il sait comment tl
