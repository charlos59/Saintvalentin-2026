<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Pour ma magnifique Lamia ❤️</title>
    <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.5.1/dist/confetti.browser.min.js"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Pacifico&family=Poppins:wght@400;700&display=swap');

        body {
            margin: 0;
            height: 100vh;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            background: linear-gradient(135deg, #ffe0f0 0%, #ffc0cb 100%); /* Dégradé doux */
            font-family: 'Poppins', sans-serif;
            overflow: hidden; /* Pour les confettis et les cœurs */
            text-align: center;
            color: #4a4a4a;
            position: relative;
        }

        /* Animation de cœurs flottants en arrière-plan */
        .heart-animation {
            position: absolute;
            width: 100%;
            height: 100%;
            pointer-events: none;
            overflow: hidden;
            z-index: 0;
        }
        .heart {
            position: absolute;
            background-color: rgba(255, 105, 180, 0.7); /* Rose bonbon */
            transform: rotate(-45deg);
            animation: floatHeart 10s infinite ease-in;
            opacity: 0;
            z-index: 0;
        }
        .heart::before, .heart::after {
            content: "";
            position: absolute;
            background-color: rgba(255, 105, 180, 0.7);
            border-radius: 50%;
            width: 100%;
            height: 100%;
        }
        .heart::before { top: -50%; left: 0; }
        .heart::after { top: 0; left: 50%; }

        @keyframes floatHeart {
            0% { transform: translateY(100vh) rotate(-45deg); opacity: 0; }
            25% { opacity: 1; }
            50% { transform: translateY(50vh) rotate(-45deg); }
            75% { opacity: 1; }
            100% { transform: translateY(-20vh) rotate(-45deg); opacity: 0; }
        }

        #main-content {
            z-index: 1; /* Pour que le contenu soit au-dessus des cœurs */
            background-color: rgba(255, 255, 255, 0.9); /* Fond légèrement transparent pour la lisibilité */
            padding: 40px;
            border-radius: 15px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.1);
            max-width: 90%;
            box-sizing: border-box;
        }

        h1 {
            font-family: 'Pacifico', cursive; /* Police manuscrite pour la touche romantique */
            color: #d81b60; /* Rose foncé */
            font-size: clamp(2.5rem, 6vw, 4rem); /* Responsive font size */
            margin-bottom: 30px;
        }

        .buttons-container {
            position: relative;
            width: 100%;
            min-height: 100px; /* Assure un espace pour le bouton "Non" */
            display: flex;
            justify-content: center;
            align-items: center;
            margin-top: 20px;
        }

        button {
            padding: 15px 40px;
            font-size: 1.5rem;
            border: none;
            border-radius: 50px;
            cursor: pointer;
            transition: all 0.3s ease-in-out;
            font-family: 'Poppins', sans-serif;
            font-weight: 700;
            box-shadow: 0 4px 10px rgba(0,0,0,0.1);
        }

        #yesBtn {
            background-color: #66bb6a; /* Vert succès */
            color: white;
            position: relative;
            z-index: 2; /* Pour être toujours cliquable */
            margin: 0 15px;
        }

        #noBtn {
            background-color: #ef5350; /* Rouge non */
            color: white;
            position: absolute; /* Permet de le déplacer */
            z-index: 1; /* Sous le bouton oui si les deux sont proches */
            margin: 0 15px;
            white-space: nowrap; /* Empêche le texte de s'enrouler */
        }

        #final-message {
            display: none;
            color: #d81b60;
            font-family: 'Pacifico', cursive;
            font-size: clamp(2rem, 5vw, 3.5rem);
            font-weight: bold;
            padding: 30px;
            line-height: 1.4;
        }

        /* Responsive adjustments */
        @media (max-width: 600px) {
            #yesBtn, #noBtn {
                padding: 12px 25px;
                font-size: 1.2rem;
            }
        }
    </style>
</head>
<body>
    <div class="heart-animation" id="heartContainer"></div>

    <div id="main-content">
        <h1>Ma chère Lamia,</h1>
        <h1>Veux-tu être ma Valentine cette année ?</h1>
        <div class="buttons-container">
            <button id="yesBtn" onclick="celebrate()">OUI ! 😍</button>
            <button id="noBtn" onmouseover="moveButton()" onclick="moveButton()">NON 😟</button>
        </div>
    </div>
    <div id="final-message">
        Tu as fait le bon choix, ma belle Lamia ! ❤️<br>
        Je t'aime plus que tout et je suis fou de toi ! 🎉<br>
        <br>
        <a href="https://open.spotify.com/track/4rYyL9lq7vPz5d0X7c7rNf?si=YOUR_SONG_ID" target="_blank" style="color: #d81b60; text-decoration: none; font-size: 1.5rem;">Clique ici pour ta playlist Bad Bunny spéciale !</a>
    </div>

    <audio id="confettiSound" src="https://assets.mixkit.co/sfx/preview/mixkit-small-fanfare-celebration-2731.mp3" preload="auto"></audio>

    <script>
        // Fonction pour créer des cœurs flottants
        function createHeart() {
            const heart = document.createElement('div');
            heart.classList.add('heart');
            document.getElementById('heartContainer').appendChild(heart);

            const size = Math.random() * 20 + 10; // Cœurs de 10px à 30px
            heart.style.width = size + 'px';
            heart.style.height = size + 'px';
            heart.style.left = Math.random() * 100 + 'vw';
            heart.style.animationDuration = Math.random() * 5 + 5 + 's'; // Durée de 5 à 10s
            heart.style.animationDelay = Math.random() * 5 + 's'; // Délai pour qu'ils n'apparaissent pas tous en même temps

            setTimeout(() => {
                heart.remove();
            }, parseFloat(heart.style.animationDuration) * 1000); // Supprime le cœur après son animation
        }
        setInterval(createHeart, 300); // Crée un cœur toutes les 300ms

        // Fonction pour déplacer le bouton "Non"
        function moveButton() {
            const btn = document.getElementById('noBtn');
            const container = document.querySelector('.buttons-container'); // Conteneur des boutons
            const containerRect = container.getBoundingClientRect(); // Dimensions du conteneur

            let newX = Math.random() * (containerRect.width - btn.offsetWidth);
            let newY = Math.random() * (containerRect.height - btn.offsetHeight);

            // S'assurer que le bouton ne sorte pas du conteneur et ne chevauche pas trop le bouton "Oui"
            const yesBtn = document.getElementById('yesBtn');
            const yesRect = yesBtn.getBoundingClientRect();

            // S'assurer qu'il ne se superpose pas au bouton OUI
            const minDistanceX = 150; // Distance minimale horizontale
            const minDistanceY = 100; // Distance minimale verticale

            if (Math.abs(newX - (yesRect.left - containerRect.left)) < minDistanceX &&
                Math.abs(newY - (yesRect.top - containerRect.top)) < minDistanceY) {
                // Si trop proche, essaie de le pousser plus loin
                newX = (newX < (yesRect.left - containerRect.left)) ? newX - minDistanceX : newX + minDistanceX;
                newY = (newY < (yesRect.top - containerRect.top)) ? newY - minDistanceY : newY + minDistanceY;
                // Recalculer pour rester dans les limites du conteneur
                newX = Math.max(0, Math.min(newX, containerRect.width - btn.offsetWidth));
                newY = Math.max(0, Math.min(newY, containerRect.height - btn.offsetHeight));
            }


            btn.style.left = newX + 'px';
            btn.style.top = newY + 'px';
            btn.style.transform = 'none'; // Annule la translation initiale
        }


        // Fonction pour la célébration (confettis + message)
        function celebrate() {
            document.getElementById('main-content').style.display = 'none';
            document.getElementById('final-message').style.display = 'block';

            // Joue le son des confettis
            const confettiSound = document.getElementById('confettiSound');
            confettiSound.play();

            // Lance les confettis
            const duration = 10 * 1000;
            const end = Date.now() + duration;

            (function frame() {
                confetti({
                    particleCount: 5,
                    angle: 60,
                    spread: 80,
                    origin: { x: 0 },
                    colors: ['#ffc0cb', '#ff69b4', '#d81b60', '#f48fb1']
                });
                confetti({
                    particleCount: 5,
                    angle: 120,
                    spread: 80,
                    origin: { x: 1 },
                    colors: ['#ffc0cb', '#ff69b4', '#d81b60', '#f48fb1']
                });

                if (Date.now() < end) {
                    requestAnimationFrame(frame);
                }
            }());
        }

        // Positionne le bouton "Non" initialement de manière aléatoire au chargement
        window.onload = () => {
            const noBtn = document.getElementById('noBtn');
            const container = document.querySelector('.buttons-container');
            const yesBtn = document.getElementById('yesBtn');

            // Réinitialise la position pour le calcul initial
            noBtn.style.position = 'absolute';
            noBtn.style.left = '';
            noBtn.style.top = '';
            noBtn.style.transform = '';

            const containerRect = container.getBoundingClientRect();
            const btnRect = noBtn.getBoundingClientRect();
            const yesRect = yesBtn.getBoundingClientRect();

            let newX, newY;
            let attempts = 0;
            const maxAttempts = 50;

            do {
                newX = Math.random() * (containerRect.width - btnRect.width);
                newY = Math.random() * (containerRect.height - btnRect.height);

                // Vérifier la distance avec le bouton "Oui"
                const distanceX = Math.abs(newX - (yesRect.left - containerRect.left));
                const distanceY = Math.abs(newY - (yesRect.top - containerRect.top));

                attempts++;
                if (attempts > maxAttempts) break; // Éviter une boucle infinie si impossible de trouver une bonne place
            } while (distanceX < 150 && distanceY < 100); // 150px et 100px comme distances minimales

            noBtn.style.left = newX + 'px';
            noBtn.style.top = newY + 'px';
            noBtn.style.transform = 'none'; // Supprime le transform initial s'il y en avait
        };


    </script>
</body>
</html>

