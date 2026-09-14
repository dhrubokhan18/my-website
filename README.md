<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>A Special Surprise</title>
    <style>
        body {
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            background-color: #ffe6e6; 
            font-family: 'Times New Roman', Times, serif; /* সব জায়গায় Times New Roman */
            text-align: center;
            overflow: hidden;
            position: relative;
        }

        .container {
            background: white;
            padding: 40px;
            border-radius: 15px;
            box-shadow: 0 10px 20px rgba(0,0,0,0.1);
            width: 350px;
            height: 250px;
            position: relative;
            z-index: 10;
        }

        input[type="date"] {
            padding: 10px;
            font-size: 16px;
            font-family: 'Times New Roman', Times, serif;
            border: 2px solid #ff9999;
            border-radius: 5px;
            margin-top: 20px;
            cursor: pointer;
        }

        button {
            padding: 10px 25px;
            font-size: 18px;
            font-family: 'Times New Roman', Times, serif;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-weight: bold;
        }

        .btn-submit {
            background-color: #ff4d4d;
            color: white;
            margin-top: 20px;
            transition: 0.2s;
        }

        .btn-yes {
            background-color: #4CAF50; 
            color: white;
            position: absolute;
            top: 150px;
            left: 70px;
            z-index: 20; 
        }

        .btn-no {
            background-color: #f44336; 
            color: white;
            position: absolute;
            top: 150px;
            left: 200px;
            transition: top 0.1s, left 0.1s; 
            z-index: 15;
        }

        #step2, #step3 {
            display: none;
        }

        h2 {
            color: #333;
            margin-bottom: 20px;
        }

      
        .love-text {
            font-size: 70px;
            font-weight: bold;
            color: #ff0000;
            text-shadow: 0px 0px 15px #ff9999, 0px 0px 30px #ff4d4d; /* সুন্দর গ্লো ইফেক্ট */
            animation: heartbeat 1.2s infinite alternate;
            z-index: 20;
            position: relative;
        }

        @keyframes heartbeat {
            0% { transform: scale(1); text-shadow: 0px 0px 15px #ff9999; }
            100% { transform: scale(1.15); text-shadow: 0px 0px 40px #ff0000; }
        }

        .floating-heart {
            position: absolute;
            bottom: -50px;
            color: red;
            animation: floatUp linear infinite;
            z-index: 5;
            opacity: 0.8;
        }

        @keyframes floatUp {
            0% { transform: translateY(0) rotate(0deg); opacity: 1; }
            100% { transform: translateY(-100vh) rotate(360deg); opacity: 0; }
        }
    </style>
</head>
<body>

   
    <audio id="clickSound" src="click.mp3"></audio>
    <audio id="bgMusic" src="music.mp3" loop></audio>

   
    <div id="step1" class="container">
        <h2>Enter Date of Birth</h2>
        <input type="date" id="dobInput">
        <br>
        <button class="btn-submit" onclick="checkDOB()">Enter</button>
        <p id="errorMsg" style="color:red; display:none; font-weight:bold; margin-top:15px;">Wrong Date! Try Again.</p>
    </div>

   
    <div id="step2" class="container">
        <h2> do you want to see something?</h2>
        <button class="btn-yes" onclick="showLove()">Yes</button>
        <button class="btn-no" id="noBtn" onmouseover="moveButton()" ontouchstart="moveButton()">No</button>
    </div>

    
    <div id="step3">
        <div class="love-text">I LOVE YOU ,DELULU❤️</div>
    </div>

    <script>
      
        document.body.addEventListener('click', function() {
            var clickAudio = document.getElementById('clickSound');
            clickAudio.currentTime = 0; 
            clickAudio.play().catch(e => {}); 
        });

        function checkDOB() {
            var dob = document.getElementById('dobInput').value;
            if (dob === '2005-07-13') {
                document.getElementById('step1').style.display = 'none'; 
                document.getElementById('step2').style.display = 'block'; 
                
                var music = document.getElementById('bgMusic');
                music.volume = 0.5; 
                music.play().catch(e => {}); 
            } else {
                document.getElementById('errorMsg').style.display = 'block'; 
            }
        }

        function moveButton() {
            var btn = document.getElementById('noBtn');
            var container = document.getElementById('step2');
            
            var maxTop = container.offsetHeight - btn.offsetHeight - 20;
            var maxLeft = container.offsetWidth - btn.offsetWidth - 20;
            
            var newTop = Math.max(20, Math.random() * maxTop);
            var newLeft = Math.max(20, Math.random() * maxLeft);
            
            btn.style.top = newTop + 'px';
            btn.style.left = newLeft + 'px';
        }

        function showLove() {
            document.getElementById('step2').style.display = 'none';
            document.getElementById('step3').style.display = 'block';
            createHearts();
        }

        function createHearts() {
            for (let i = 0; i < 40; i++) {
                setTimeout(() => {
                    let heart = document.createElement('div');
                    heart.innerHTML = '❤️';
                    heart.classList.add('floating-heart');
                    heart.style.left = Math.random() * 100 + 'vw';
                    heart.style.fontSize = (Math.random() * 20 + 20) + 'px'; 
                    heart.style.animationDuration = (Math.random() * 3 + 2) + 's'; 
                    document.body.appendChild(heart);
                    
                    setTimeout(() => { heart.remove(); }, 5000);
                }, i * 150); 
            }
        }
    </script>
</body>
</html>
