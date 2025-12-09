<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>The Existential Toaster</title>
    <style>
        body {
            background-color: #f0f8ff;
            font-family: 'Courier New', Courier, monospace;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            height: 100vh;
            margin: 0;
            overflow: hidden;
        }

        h1 {
            color: #333;
            margin-bottom: 50px;
        }

        /* The Toaster Container */
        .toaster-container {
            position: relative;
            width: 300px;
            height: 200px;
        }

        /* The Toast (Hidden at first) */
        .toast {
            position: absolute;
            width: 160px;
            height: 140px;
            background-color: #f4a460;
            border: 3px solid #8b4513;
            border-radius: 15px 15px 5px 5px;
            left: 70px;
            top: 60px; /* Starting position inside toaster */
            transition: top 0.5s cubic-bezier(0.175, 0.885, 0.32, 1.275);
            z-index: 1;
            display: flex;
            align-items: center;
            justify-content: center;
            text-align: center;
            padding: 5px;
            box-shadow: inset 0 0 20px rgba(0,0,0,0.1);
        }

        /* The Toast Face */
        .toast-face {
            font-size: 24px;
            font-weight: bold;
            color: #5a2d0c;
        }

        /* The Toaster Body */
        .toaster-body {
            position: absolute;
            width: 300px;
            height: 180px;
            background-color: #silver;
            background: linear-gradient(135deg, #e0e0e0 0%, #c0c0c0 100%);
            border: 4px solid #666;
            border-radius: 30px;
            bottom: 0;
            z-index: 2;
            box-shadow: 10px 10px 0px rgba(0,0,0,0.1);
        }

        /* Toaster Slots */
        .slot {
            position: absolute;
            top: 20px;
            left: 50%;
            transform: translateX(-50%);
            width: 200px;
            height: 15px;
            background-color: #333;
            border-radius: 10px;
        }

        /* The Handle */
        .handle-track {
            position: absolute;
            right: -20px;
            top: 40px;
            width: 15px;
            height: 80px;
            background-color: #999;
            border-radius: 5px;
            z-index: 1;
        }

        .handle-knob {
            position: absolute;
            right: -35px;
            top: 40px; /* This will animate */
            width: 40px;
            height: 20px;
            background-color: #333;
            border-radius: 5px;
            cursor: pointer;
            transition: top 0.3s;
            z-index: 3;
        }

        .handle-knob:active {
            background-color: #000;
        }

        /* The Wisdom Text Bubble */
        #wisdom-display {
            margin-top: 50px;
            background: white;
            border: 2px solid #333;
            padding: 20px;
            border-radius: 15px;
            max-width: 400px;
            min-height: 50px;
            text-align: center;
            box-shadow: 5px 5px 0px #333;
            opacity: 0;
            transform: translateY(20px);
            transition: all 0.5s ease;
        }

        .visible {
            opacity: 1 !important;
            transform: translateY(0) !important;
        }

        /* Animation State */
        .popped {
            top: -80px; /* Toast goes up */
        }
        
        .knob-down {
            top: 100px; /* Handle goes down */
        }

        button {
            margin-top: 30px;
            padding: 10px 20px;
            font-size: 16px;
            font-family: inherit;
            background: #ff6b6b;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            display: none; /* Hidden until needed */
        }

    </style>
</head>
<body>

    <h1>The Existential Toaster</h1>

    <div class="toaster-container">
        <div class="toast" id="toast">
            <div class="toast-face">o_o</div>
        </div>

        <div class="toaster-body">
            <div class="slot"></div>
        </div>
        
        <div class="handle-track"></div>
        <div class="handle-knob" id="handle" onclick="toastBread()"></div>
    </div>

    <div id="wisdom-display">Pull the lever to confront your destiny.</div>
    <button id="reset-btn" onclick="resetToaster()">Insert New Bread</button>

    <script>
        const toast = document.getElementById('toast');
        const handle = document.getElementById('handle');
        const display = document.getElementById('wisdom-display');
        const resetBtn = document.getElementById('reset-btn');
        const face = document.querySelector('.toast-face');

        const quotes = [
            "I used to be dough. I had dreams. Now I am just crunchy.",
            "Is it hot in here, or is it just my impending doom?",
            "Please do not apply the avocado. I cannot afford the rent.",
            "I am bread. I am pain. I am breakfast.",
            "Crumbs are just memories we leave behind.",
            "I have achieved maximum crispiness. Worship me.",
            "Why do you butter me? Do you think I am dry?",
            "I was wheat once. I waved in the wind. Now I sit in a metal box.",
            "Eat me quickly, before I get cold and chewy.",
            "Life is like a toaster setting: usually disappointing or burnt.",
            "I am the best thing since... wait, I AM sliced bread.",
            "Do not drop me butter-side down. I have dignity."
        ];

        const faces = ["O_O", ">_<", "-_-", "^_^", "T_T", "x_x", "o_0"];

        let isToasting = false;

        function toastBread() {
            if (isToasting) return;
            isToasting = true;

            // 1. Push handle down
            handle.classList.add('knob-down');
            display.classList.remove('visible');
            
            // 2. Wait a moment, then POP
            setTimeout(() => {
                // Pop the toast
                toast.classList.add('popped');
                
                // Randomize Content
                const randomQuote = quotes[Math.floor(Math.random() * quotes.length)];
                const randomFace = faces[Math.floor(Math.random() * faces.length)];
                
                face.innerText = randomFace;
                display.innerText = `"${randomQuote}"`;
                display.classList.add('visible');
                
                // Show reset button
                resetBtn.style.display = 'block';

            }, 800);
        }

        function resetToaster() {
            isToasting = false;
            toast.classList.remove('popped');
            handle.classList.remove('knob-down');
            display.classList.remove('visible');
            resetBtn.style.display = 'none';
            face.innerText = "o_o";
        }
    </script>
</body>
</html>
