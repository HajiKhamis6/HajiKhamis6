<!DOCTYPE html>
<html lang="sw">
<head>
    <meta charset="UTF-8">
    <title>Ramadan Kareem · Fataki ndogo · Fomu moja kwa moja</title>
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">

<style>
/* RESET na msingi */
html, body {
    margin: 0;
    padding: 0;
    height: 100%;
    overflow: hidden;           /* hakuna scroll, fataki full */
    background: #0b2a1f;
    font-family: 'Segoe UI', Tahoma, sans-serif;
}

/* CANVAS ya fataki – juu kabisa, lakini viungo vinaweza kubonyezwa */
#fireworksCanvas {
    position: fixed;
    inset: 0;
    width: 100%;
    height: 100%;
    display: block;
    z-index: 1000;              /* juu ya kila kitu isipokuwa overlay ya mwisho */
    pointer-events: none;       /* kuruhusu kubonyeza vitu vilivyo chini */
}

/* KARATASI KUU – SAIMU IMEWASHA (ndogo na inayovutia) */
.box {
    position: relative;
    z-index: 500;               /* chini ya canvas, juu ya background */
    background: rgba(0, 0, 0, 0.7);
    color: #ffe9a8;
    max-width: 400px;           /* iliyopunguzwa kutoka 520px */
    width: 90%;
    margin: 4vh auto 0;         /* nafasi kidogo juu */
    padding: 25px 20px;         /* padding ndogo, inayofaa */
    border-radius: 30px;
    text-align: center;
    border: 2px solid gold;
    box-shadow: 0 15px 40px black;
    backdrop-filter: blur(3px);
}

/* MAANDIKO YA KITABU – yamebanwa lakini yanasomeka */
.arabic {
    font-size: 1.4rem;          /* ilikuwa 2.2rem, sasa inafaa */
    color: #ffd966;
    margin-bottom: 8px;
    line-height: 1.3;
    word-break: break-word;
}

.box h2 {
    font-size: 1.3rem;
    margin: 8px 0 5px;
}

.box p {
    background: rgba(255, 215, 120, 0.15);
    padding: 12px;
    border-radius: 25px;
    font-size: 0.95rem;
    margin: 10px 0;
}

/* KITUO CHA KUFUNGUA – kimeongezeka sauti lakini si kikubwa */
button {
    margin-top: 10px;
    padding: 14px 25px;
    font-size: 1.3rem;
    border-radius: 40px;
    border: none;
    background: gold;
    color: #1f3a1f;
    font-weight: bold;
    cursor: pointer;
    box-shadow: 0 8px 0 #8a5a00;
    transition: 0.05s linear;
    width: auto;
    min-width: 220px;
}
button:active {
    transform: translateY(6px);
    box-shadow: 0 2px 0 #8a5a00;
}

/* OVERLAY – juu ya fataki (z-index juu zaidi) */
.surprise-overlay {
    position: fixed;
    inset: 0;
    background: rgba(0, 0, 0, 0.6);
    display: flex;
    align-items: center;
    justify-content: center;
    visibility: hidden;
    opacity: 0;
    z-index: 10000;             /* juu ya canvas (1000) */
    transition: 0.25s ease;
    pointer-events: auto;
    backdrop-filter: blur(2px);
}
.surprise-overlay.show {
    visibility: visible;
    opacity: 1;
}

/* KADI NDOGO YA SURPRISE */
.surprise-card {
    background: #1d3b1d;
    border: 4px solid gold;
    border-radius: 40px;
    padding: 25px 20px;
    max-width: 380px;
    width: 85%;
    text-align: center;
    color: #fff3c4;
    box-shadow: 0 0 40px gold;
}

.surprise-card h2 {
    font-size: 1.3rem;
    line-height: 1.4;
    margin: 10px 0;
    word-break: break-word;
}

.surprise-card p {
    font-size: 1.2rem;
    margin: 15px 0;
}

/* KITUO CHA KWENDA FOMU – sasa ni kiungo cha moja kwa moja */
.fomu-link {
    display: inline-block;
    margin-top: 12px;
    padding: 14px 22px;
    font-size: 1.3rem;
    border-radius: 40px;
    border: none;
    background: #e4a010;
    color: #1f3a1f;
    font-weight: bold;
    text-decoration: none;
    box-shadow: 0 6px 0 #7a4f0e;
    transition: 0.05s linear;
    width: auto;
    min-width: 200px;
    cursor: pointer;
}
.fomu-link:active {
    transform: translateY(5px);
    box-shadow: 0 1px 0 #7a4f0e;
}

/* hakuna mabadiliko mengine ya ziada */
</style>
</head>
<body>

<!-- canvas ya fataki iko juu (pointer-events:none) -->
<canvas id="fireworksCanvas"></canvas>

<!-- sanduku kuu – saizi ndogo, imeweka katikati -->
<div class="box">
    <div class="arabic">
        ──────⊹⊱✫⊰⊹──────<br>
        شَهۡرُ رَمَضَانَ ٱلَّذِيٓ أُنزِلَ فِيهِ ٱلۡقُرۡءَانُ هُدٗى لِّلنَّاسِ وَبَيِّنَٰتٖ مِّنَ ٱلۡهُدَىٰ وَٱلۡفُرۡقَانِۚ
    </div>
    <h2><i class="fas fa-envelope-open-text"></i> UMEPOKEA UJUMBE MPYA</h2>
    <p>
        <b>HAJI JECHA KHAMIS akishirikiana na JTL Zanzibar</b><br>
        amekutumia ujumbe maalum wa kukutakia kheri za mwezi mtukufu wa Ramdhan.
    </p>
    <button onclick="openSurprise()">✨ FUNGUA SASA ✨</button>
</div>

<!-- overlay ya kheri + kiungo cha fomu (moja kwa moja) -->
<div id="overlay" class="surprise-overlay">
    <div class="surprise-card">
        <h2>
            🎁 ──────⊹⊱✫⊰⊹──────<br>
            يَٰٓأَيُّهَا ٱلَّذِينَ ءَامَنُواْ كُتِبَ عَلَيۡكُمُ ٱلصِّيَامُ كَمَا كُتِبَ عَلَى ٱلَّذِينَ مِن قَبۡلِكُمۡ لَعَلَّكُمۡ تَتَّقُونَ
        </h2>
        <p>🤍 Heri ya mwezi mtukufu wa Ramadhani 🤍</p>
        <!-- Badala ya button ya kufunga, tumekuwa link ya moja kwa moja ya fomu, lakini bado tunahitaji njia ya kuifunga overlay. Tumebadilisha: sasa kuna fungo ndogo ya "Funga" au tunaweka kiungo cha fomu na kitu kingine. Lakini maagizo yanasema "JAZA FOMU KUPOKEA SWADAQ" ikiwa ni kiungo cha form. Na pia mtumiaji anaweza kutaka kuifunga overlay. Nitaweka link ya fomu kubwa na chini yake "Funga" ndogo ili asije akakwama. -->
        <a href="https://forms.gle/BHq4fi2e4PocRNqk6" target="_blank" class="fomu-link" onclick="event.stopPropagation();">
            📋 JAZA FOMU KUPOKEA SWADAQ
        </a>
        <div style="margin-top: 18px;">
            <button class="close-surprise" onclick="closeSurprise()" style="padding:8px 25px; font-size:1.0rem; background:#b8860b; box-shadow:0 4px 0 #6b4b0e; min-width:auto;">✖ Funga</button>
        </div>
        <p style="font-size:0.85rem; margin-top:12px; background:transparent;">Bonyeza fomu ili kujaza, au funga kuendelea kutazama fataki.</p>
    </div>
</div>

<script>
/* =============== FIREWORKS INAZOENDELEA =============== */
const canvas = document.getElementById("fireworksCanvas");
const ctx = canvas.getContext("2d");
let w, h, fireworks = [], particles = [], running = false;

function resize() {
    w = canvas.width = window.innerWidth;
    h = canvas.height = window.innerHeight;
}
window.addEventListener("resize", resize);
resize();

function random(min, max) { return Math.random() * (max - min) + min; }

class Firework {
    constructor() {
        this.x = random(0, w);
        this.y = h;
        this.targetY = random(h * 0.2, h * 0.55);
        this.color = `hsl(${random(0, 360)}, 100%, 65%)`;
        this.speed = random(9, 14);   // kasi ya kuruka
        this.radius = 4;
    }
    update() {
        this.y -= this.speed;
        if (this.y <= this.targetY) {
            explode(this.x, this.y, this.color);
            return true;
        }
        drawCircle(this.x, this.y, this.radius, this.color);
        return false;
    }
}

class Particle {
    constructor(x, y, color) {
        this.x = x;
        this.y = y;
        this.color = color;
        this.radius = random(3, 6);
        this.speedX = random(-8, 8);
        this.speedY = random(-8, 8);
        this.life = 70;
        this.decay = 0.94;
    }
    update() {
        this.life--;
        this.x += this.speedX;
        this.y += this.speedY;
        this.speedX *= this.decay;
        this.speedY *= this.decay;
        this.radius *= 0.98;
        drawCircle(this.x, this.y, this.radius, this.color);
        return this.life <= 0 || this.radius < 0.3;
    }
}

function explode(x, y, color) {
    let particleCount = 60 + Math.floor(random(20, 40));
    for (let i = 0; i < particleCount; i++) {
        particles.push(new Particle(x, y, color));
    }
    for (let i = 0; i < 15; i++) {
        let extraColor = `hsl(${random(0, 360)}, 90%, 70%)`;
        particles.push(new Particle(x, y, extraColor));
    }
}

function drawCircle(x, y, r, c) {
    ctx.beginPath();
    ctx.arc(x, y, r, 0, Math.PI * 2);
    ctx.fillStyle = c;
    ctx.shadowColor = c;
    ctx.shadowBlur = 12;
    ctx.fill();
    ctx.shadowBlur = 0;
}

function animate() {
    if (!running) return;
    ctx.clearRect(0, 0, w, h);

    // fataki nyingi (0.12 probability)
    if (Math.random() < 0.12) fireworks.push(new Firework());

    fireworks = fireworks.filter(f => !f.update());
    particles = particles.filter(p => !p.update());

    requestAnimationFrame(animate);
}

/* =============== FUNCTIONS ZA OPEN/CLOSE =============== */
function openSurprise() {
    document.getElementById("overlay").classList.add("show");
    running = true;
    animate();
}
function closeSurprise() {
    document.getElementById("overlay").classList.remove("show");
    running = false;
    ctx.clearRect(0, 0, w, h);
    fireworks = [];
    particles = [];
}

// Hakikisha kuwa ikiwa mtumiaji anabonyeza link ya fomu, fataki zinaendelea na overlay haifunguki kwa bahati mbaya.
// Pia, tunataka kuzuia tabia ya kufunga wakati wa kubonyeza link.
document.querySelector('.fomu-link').addEventListener('click', function(e) {
    e.stopPropagation();  // usimpe fursa overlay kuwa closed
    // Fungua link kwa manually kwenye tab mpya (tayari iko target="_blank")
    // Hata hivyo tunataka kuruhusu default, lakini tumekwisha weka target _blank
    // Hii inazuia pia kurudi nyuma.
});

// Vilevile kwa button ya funga hapa chini, tayari inafunga vizuri
</script>

<!-- HAKIKISHA KIUNGO CHA FOMU KINAENDA MOJA KWA MOJA. Pia tumeongeza _blank ili wasiondoke kwenye ukurasa wa fataki. -->
</body>
</html>
