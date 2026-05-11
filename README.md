# wedding-of-zain-and-Imon
index.html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Nikah Invitation | Zain & Umme</title>
    <link href="https://fonts.googleapis.com/css2?family=Cinzel+Decorative:wght@700&family=Great+Vibes&family=Montserrat:wght@300;400;600&display=swap" rel="stylesheet">
    <style>
        :root {
            --royal-green: #004225;
            --gold: #D4AF37;
            --ivory: #FFFFF0;
            --deep-gold: #996515;
        }

        * { margin: 0; padding: 0; box-sizing: border-box; }

        body {
            background-color: #002b18;
            height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            overflow: hidden;
            font-family: 'Montserrat', sans-serif;
        }

        .bg-pattern {
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            background-image: url("data:image/svg+xml,%3Csvg width='80' height='80' viewBox='0 0 80 80' xmlns='http://www.w3.org/2000/svg'%3E%3Cpath d='M40 0l40 40-40 40L0 40z' fill='%23d4af37' fill-opacity='0.03'/%3E%3C/svg%3E");
            z-index: -1;
        }

        .envelope-wrapper {
            position: relative;
            cursor: pointer;
            perspective: 1500px;
        }

        .envelope {
            position: relative;
            width: 320px;
            height: 220px;
            background: var(--royal-green);
            border: 2px solid var(--gold);
            box-shadow: 0 20px 50px rgba(0,0,0,0.6);
            z-index: 1;
        }

        .flap {
            position: absolute;
            top: 0; left: 0;
            width: 100%; height: 100%;
            background: var(--royal-green);
            border: 1px solid var(--gold);
            clip-path: polygon(0 0, 50% 60%, 100% 0);
            z-index: 5;
            transition: transform 0.8s ease;
            transform-origin: top;
        }

        .envelope-wrapper.open .flap {
            transform: rotateX(180deg);
            z-index: 0;
        }

        .card {
            position: absolute;
            top: 5px; left: 5px;
            width: 310px;
            height: 210px;
            background: var(--ivory);
            z-index: 2;
            transition: all 1s cubic-bezier(0.4, 0, 0.2, 1);
            border: 5px double var(--gold);
            padding: 25px 15px;
            overflow-y: auto;
            scrollbar-width: none;
            display: flex;
            flex-direction: column;
            align-items: center;
            opacity: 0;
        }

        .envelope-wrapper.open .card {
            transform: translateY(-280px);
            height: 75vh;
            max-height: 700px;
            opacity: 1;
            z-index: 10;
            box-shadow: 0 10px 30px rgba(0,0,0,0.3);
        }

        .content {
            display: none;
            text-align: center;
            color: var(--royal-green);
            width: 100%;
        }

        .envelope-wrapper.open .content {
            display: block;
            animation: fadeIn 1.2s forwards;
            animation-delay: 0.7s;
        }

        .bismillah { font-size: 1.2rem; color: var(--deep-gold); margin-bottom: 5px; font-weight: bold; }
        .insha-allah { font-family: 'Cinzel Decorative', serif; font-size: 0.8rem; color: var(--deep-gold); margin-bottom: 15px; letter-spacing: 2px; }
        
        h1 { font-family: 'Great Vibes', cursive; color: var(--deep-gold); font-size: 2.2rem; margin: 8px 0; }
        h2 { font-family: 'Cinzel Decorative', serif; font-size: 0.65rem; color: var(--royal-green); margin: 10px 0 5px 0; letter-spacing: 1px; }
        
        .family-section {
            font-size: 0.7rem;
            line-height: 1.4;
            color: #333;
            margin: 10px 0;
            padding: 10px;
            background: rgba(212, 175, 55, 0.04);
            border: 1px solid rgba(212, 175, 55, 0.2);
        }
        
        .name-title { font-weight: 600; color: var(--royal-green); text-transform: uppercase; font-size: 0.75rem; display: block; }

        .nikah-box {
            background: var(--royal-green);
            color: var(--gold);
            padding: 15px 10px;
            margin: 15px 0;
            border: 1px solid var(--gold);
            width: 90%;
        }

        .nikah-box p { font-size: 0.8rem; line-height: 1.5; margin: 2px 0; }
        .nikah-title { font-family: 'Cinzel Decorative', serif; font-size: 0.9rem; margin-bottom: 8px; display: block; border-bottom: 1px solid var(--gold); padding-bottom: 5px; }

        .venue-section {
            margin: 10px 0;
            padding: 15px;
            border: 1px dashed var(--gold);
            background: rgba(212, 175, 55, 0.02);
            width: 90%;
        }

        .venue-section strong { color: var(--deep-gold); font-family: 'Cinzel Decorative', serif; font-size: 0.9rem; display: block; margin-bottom: 4px; }
        .valima-text { color: var(--royal-green); font-weight: 700; font-size: 0.85rem; margin-top: 10px; border-top: 1px solid rgba(212, 175, 55, 0.3); padding-top: 8px; }

        .btn-container { display: flex; gap: 10px; justify-content: center; margin: 20px 0; }
        .btn {
            padding: 10px 15px;
            border: 1px solid var(--gold);
            background: var(--royal-green);
            color: var(--gold);
            text-decoration: none;
            font-size: 0.65rem;
            font-weight: 600;
        }

        @keyframes blink { 0%, 100% { opacity: 1; } 50% { opacity: 0.3; } }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }

        .particle { position: absolute; background: var(--gold); border-radius: 50%; pointer-events: none; }
        .tap-text { position: absolute; bottom: -50px; width: 100%; text-align: center; color: var(--gold); font-family: 'Cinzel Decorative', serif; font-size: 0.8rem; letter-spacing: 2px; animation: blink 2s infinite; }

        @media (max-width: 400px) {
            .envelope { width: 280px; height: 190px; }
            .card { width: 270px; }
            .envelope-wrapper.open .card { transform: translateY(-260px); }
        }
    </style>
</head>
<body>

    <div class="bg-pattern"></div>

    <div class="envelope-wrapper" id="invitation">
        <div class="flap"></div>
        <div class="envelope"></div>
        
        <div class="card" id="card">
            <div class="content">
                <p class="bismillah">بِسْمِ اللهِ الرَّحْمٰنِ الرَّحِيْمِ</p>
                <p class="insha-allah">Insha Allah</p>
                
                <p style="font-size: 0.6rem; letter-spacing: 1px; font-weight: 600;">WITH THE BLESSINGS OF ALMIGHTY ALLAH</p>

                <div class="family-section">
                    <span class="name-title">Alhaj Noor Ahmed Shariff</span>
                    <small>Manager of Nazneen Silk Khadi</small><br>
                    <strong>P/O:</strong> Late Fakhruddin Shariff Sab @ Chote sab, Upperpet<br>
                    <strong>M/O:</strong> Late Umar Shariff Sab, Shidlaghatta
                </div>

                <h2>REQUEST THE HONOR OF YOUR COMPANY AT THE NIKAH OF THEIR SON</h2>
                <h1>Zain Shariff <span style="font-size: 0.9rem; font-family: 'Montserrat';">BCA</span></h1>
                
                <p style="font-family: 'Great Vibes'; font-size: 1.6rem; color: var(--gold); margin: 5px 0;">With</p>

                <h1>Umme Imon <span style="font-size: 0.9rem; font-family: 'Montserrat';">MCA</span></h1>
                <h2>DAUGHTER OF</h2>

                <div class="family-section">
                    <span class="name-title">Late Fayaz Ulla Khan</span>
                    <small>Jewellery Merchant</small><br>
                    <strong>P/O:</strong> Ameer Khan, Silk Merchant, Chinsander<br>
                    <strong>M/O:</strong> Al Haj Mutwalli Ibrahim Sab, Mango Merchant, Taylur
                </div>

                <div class="nikah-box">
                    <span class="nikah-title">NIKAH CEREMONY</span>
                    <p><strong>Sunday, 7th June 2026</strong></p>
                    <p>After Namaz-e-Zohar</p>
                    <p style="margin-top: 8px;"><strong>Masjid-e-Sharifiya Umar Farooq</strong></p>
                    <p>Upperpet</p>
                </div>

                <div class="venue-section">
                    <strong>Venue: Firdose Palace</strong>
                    <p style="font-size: 0.8rem;">
                        Upperpet, Sidlaghatta Road,<br>
                        Chintamani Taluk.
                    </p>
                    <p class="valima-text">Valima Dinner: 8:00 p.m. onwards</p>
                </div>

                <div class="btn-container">
                    <a href="https://www.google.com/maps/search/Firdose+Palace+Chintamani" target="_blank" class="btn">VIEW ON MAP</a>
                    <a href="https://wa.me/919740376070" class="btn">RSVP WHATSAPP</a>
                </div>

                <p style="margin-bottom: 30px; font-size: 0.7rem; font-style: italic; color: var(--deep-gold);">
                    — Awaiting your presence and prayers —
                </p>
            </div>
        </div>

        <div class="tap-text">TAP TO OPEN</div>
    </div>

    <script>
        const envelope = document.getElementById('invitation');

        envelope.addEventListener('click', () => {
            envelope.classList.toggle('open');
        });

        function createSparkle() {
            const p = document.createElement('div');
            p.classList.add('particle');
            const size = Math.random() * 3 + 1 + 'px';
            p.style.width = size; p.style.height = size;
            p.style.left = Math.random() * 100 + 'vw';
            p.style.top = '-10px';
            document.body.appendChild(p);

            const duration = Math.random() * 3 + 4;
            p.animate([
                { transform: 'translateY(0)', opacity: 0.8 },
                { transform: 'translateY(110vh)', opacity: 0 }
            ], { duration: duration * 1000 });

            setTimeout(() => p.remove(), duration * 1000);
        }
        setInterval(createSparkle, 600);
    </script>
</body>
</html>
