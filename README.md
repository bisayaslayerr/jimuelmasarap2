<!DOCTYPE html>
<html>
<head>
    <title>Advanced Random Color Generator</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            margin-top: 80px;
            transition: background 0.6s ease;
        }
        h1 {
            margin-bottom: 10px;
        }
        #colorBox {
            font-size: 22px;
            margin: 20px;
            font-weight: bold;
        }
        button {
            padding: 10px 20px;
            margin: 8px;
            font-size: 16px;
            cursor: pointer;
            border: none;
            border-radius: 8px;
        }
        .primary {
            background-color: black;
            color: white;
        }
        .secondary {
            background-color: #444;
            color: white;
        }
    </style>
</head>
<body>

    <h1>🎨 Advanced Random Color Generator</h1>
    <div id="colorBox">
        HEX: #FFFFFF<br>
        RGB: rgb(255, 255, 255)
    </div>

    <button class="primary" onclick="generateColor()">Generate Color</button>
    <button class="secondary" onclick="toggleGradient()">Toggle Gradient</button>
    <button class="secondary" onclick="copyColor()">Copy HEX</button>

    <script>
        let gradientMode = false;
        let currentHex = "#FFFFFF";

        function randomColor() {
            return "#" + Math.floor(Math.random()*16777215).toString(16).padStart(6, '0');
        }

        function hexToRgb(hex) {
            let r = parseInt(hex.substring(1,3), 16);
            let g = parseInt(hex.substring(3,5), 16);
            let b = parseInt(hex.substring(5,7), 16);
            return `rgb(${r}, ${g}, ${b})`;
        }

        function getBrightness(hex) {
            let r = parseInt(hex.substring(1,3), 16);
            let g = parseInt(hex.substring(3,5), 16);
            let b = parseInt(hex.substring(5,7), 16);
            return (r * 299 + g * 587 + b * 114) / 1000;
        }

        function generateColor() {
            let color1 = randomColor();
            currentHex = color1;

            if (gradientMode) {
                let color2 = randomColor();
                document.body.style.background = 
                    `linear-gradient(45deg, ${color1}, ${color2})`;
            } else {
                document.body.style.background = color1;
            }

            let rgb = hexToRgb(color1);
            document.getElementById("colorBox").innerHTML = 
                `HEX: ${color1}<br>RGB: ${rgb}`;

            // Auto text contrast
            let brightness = getBrightness(color1);
            document.body.style.color = brightness > 128 ? "black" : "white";
        }

        function toggleGradient() {
            gradientMode = !gradientMode;
            generateColor();
        }

        function copyColor() {
            navigator.clipboard.writeText(currentHex);
            alert("Copied: " + currentHex);
        }
    </script>

</body>
</html>
