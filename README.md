<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Will you be my Valentine? 💌</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            background: linear-gradient(135deg, #ffe6f2 0%, #ffc2d1 100%);
            min-height: 100vh;
            font-family: 'Segoe UI', 'Arial', sans-serif;
            overflow-x: hidden;
            position: relative;
        }

        .floating-heart {
            position: absolute;
            color: #ff69b4;
            opacity: 0.5;
            animation: float 8s linear infinite;
        }

        @keyframes float {
            0% {
                transform: translateY(100vh) rotate(0deg);
                opacity: 0;
            }
            10% { opacity: 0.5; }
            90% { opacity: 0.5; }
            100% {
                transform: translateY(-20vh) rotate(360deg);
                opacity: 0;
            }
        }

        .container {
            text-align: center;
            padding: 50px 20px;
            position: relative;
            z-index: 10;
            margin-top: 60px;
        }

        .card {
            background: white;
            max-width: 500px;
            margin: 0 auto;
            padding: 40px 30px;
            border-radius: 20px;
            box-shadow: 0 10px 30px rgba(255, 105, 180, 0.2);
            position: relative;
            min-height: 550px; /* Extra space for GIF */
        }

        .card::before, .card::after {
            content: "❤️";
            position: absolute;
            font-size: 24px;
        }

        .card::before { top: 20px; left: 20px; }
        .card::after { top: 20px; right: 20px; }

        h1 {
            color: #d63384;
            font-size: 2.2rem;
            margin-bottom: 30px;
            text-shadow: 2px 2px 4px rgba(255, 105, 180, 0.3);
        }

        .subtitle {
            color: #6c757d;
            font-size: 1.1rem;
            margin-bottom: 40px;
            line-height: 1.5;
        }

        button {
            margin: 10px;
            padding: 15px 35px;
            font-size: 18px;
            cursor: pointer;
            border: none;
            border-radius: 30px;
            transition: all 0.2s ease !important;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
        }

        #yesBtn {
            background-color: #ff69b4;
            color: white;
            position: relative;
            display: inline-block;
        }

        #yesBtn:hover {
            background-color: #d63384;
            transform: scale(1.05);
            box-shadow: 0 8px 20px rgba(255, 105, 180, 0.3);
        }

        #noBtn {
            background-color: #6495ED;
            color: white;
            position: absolute;
            left: 50%;
            top: 280px;
            transform: translateX(-50%);
            width: 150px;
        }

        #noBtn:hover {
            background-color: #4169e1;
        }

        .moving-btn {
            cursor: default;
            background-color: #b0c4de !important;
        }

        /* Ensure GIF displays properly */
        #happyBoyGif {
            display: none;
            margin: 30px auto 0;
            max-width: 300px;
            width: 100%;
            height: auto;
            border-radius: 15px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
            border: none; /* Remove any hidden borders */
        }

        /* Fallback message if GIF fails */
        .gif-fallback {
            display: none;
            color: #d63384;
            font-weight: bold;
            margin: 20px 0;
        }

        .footer {
            margin-top: 30px;
            color: #6c757d;
            font-style: italic;
            position: absolute;
            bottom: 20px;
            left: 50%;
            transform: translateX(-50%);
        }

        @media (max-width: 480px) {
            h1 { font-size: 1.8rem; }
            #yesBtn {
                display: block;
                width: 80%;
                margin: 15px auto;
            }
            #noBtn {
                width: 80%;
                top: 320px;
            }
            .card { padding: 30px 20px; min-height: 600px; }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="card">
            <h1>Will you be my Valentine? 💌</h1>
            <p class="subtitle">Every moment with you feels like magic... I want to make this Valentine's Day unforgettable with YOU.</p>
            
            <button id="yesBtn">Yes, I do! ❤️</button>
            <button id="noBtn">No</button>
            
            <!-- Primary GIF with backup -->
            <img 
                id="happyBoyGif" 
                src="https://media.giphy.com/media/3ohhwE9cP7p2jp8hqA/giphy.gif" 
                alt="Happy boy jumping in celebration"
                onerror="showFallback()" <!-- Show fallback if primary fails -->
            >
            <div class="gif-fallback" id="gifFallback">🎉 YES! So happy we're spending Valentine's together! 🎉</div>
            
            <div class="footer">Made with all my love ❤️</div>
        </div>
    </div>

    <script>
        function createFloatingHearts() {
            const heartCount = 15;
            for (let i = 0; i < heartCount; i++) {
                const heart = document.createElement('div');
                heart.className = 'floating-heart';
                heart.textContent = '❤️';
                heart.style.fontSize = `${Math.random() * 20 + 10}px`;
                heart.style.left = `${Math.random() * 100}vw`;
                heart.style.animationDelay = `${Math.random() * 8}s`;
                heart.style.animationDuration = `${Math.random() * 10 + 5}s`;
                document.body.appendChild(heart);
            }
        }

        let clickCount = 0;
        const messages = [
            "Are you sure? 🥺",
            "why don't we try? 💖",
            "just once please?",
            "I just want to talk to you for the last time 😭",
            "please accept my offer" 
        ];

        const yesBtn = document.getElementById('yesBtn');
        const noBtn = document.getElementById('noBtn');
        const happyBoyGif = document.getElementById('happyBoyGif');
        const gifFallback = document.getElementById('gifFallback');
        const card = document.querySelector('.card');
        
        const moveDistance = 60;
        const directions = [
            { x: -moveDistance, y: 0 },
            { x: moveDistance, y: 0 },
            { x: 0, y: -moveDistance },
            { x: 0, y: moveDistance }
        ];

        let currentX = 50;
        let currentY = 280;

        // Show GIF or fallback when Yes is clicked
        function showCelebration() {
            happyBoyGif.style.display = 'block';
            // Check if GIF loaded successfully
            if (happyBoyGif.complete && happyBoyGif.naturalHeight === 0) {
                showFallback();
            }
        }

        // Show fallback message if GIF fails
        function showFallback() {
            happyBoyGif.style.display = 'none';
            gifFallback.style.display = 'block';
        }

        // Yes button action
        yesBtn.addEventListener('click', function() {
            alert("Yay! Wala nang bawian ah ❤️");
            showCelebration(); // Trigger GIF/fallback
            yesBtn.disabled = true;
            noBtn.disabled = true;
            noBtn.style.cursor = 'not-allowed';
        });

        // No button click handler
        noBtn.addEventListener('click', function() {
            if (clickCount < messages.length) {
                alert(messages[clickCount]);
                clickCount++;
                setTimeout(() => noBtn.focus(), 10);
                
                if (clickCount >= messages.length) {
                    noBtn.classList.add('moving-btn');
                }
            }
        });

        // No button movement
        noBtn.addEventListener('mouseenter', function() {
            if (clickCount >= messages.length) {
                const cardRect = card.getBoundingClientRect();
                const btnRect = noBtn.getBoundingClientRect();

                const randomDir = directions[Math.floor(Math.random() * directions.length)];

                let newX = currentX + randomDir.x;
                let newY = currentY + randomDir.y;

                const minX = 10;
                const maxX = 90;
                const minY = 100;
                const maxY = cardRect.height - btnRect.height - 40;

                if (newX < minX) newX = maxX - moveDistance;
                if (newX > maxX) newX = minX + moveDistance;
                if (newY < minY) newY = maxY - moveDistance;
                if (newY > maxY) newY = minY + moveDistance;

                currentX = newX;
                currentY = newY;
                noBtn.style.left = `${newX}%`;
                noBtn.style.top = `${newY}px`;
                noBtn.style.transform = 'translateX(-50%)';
            }
        });

        createFloatingHearts();
    </script>
</body>
</html>
