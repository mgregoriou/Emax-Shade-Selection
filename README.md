
<html>
<head>
    <title>Emax Press Shade Conversion</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            margin: 20px;
        }
        img {
            width: 500px;
            margin-bottom: 10px;
        }
        h1 {
            font-size: 24px;
        }
        h3 {
            font-size: 16px;
            color: gray;
        }
        input {
            margin: 5px;
            padding: 5px;
        }
        button {
            padding: 8px 12px;
            background-color: #007bff;
            color: white;
            border: none;
            cursor: pointer;
        }
        button:hover {
            background-color: #0056b3;
        }
        p {
            font-weight: bold;
            margin-top: 15px;
        }
    </style>
</head>
<body>

    <!-- Company Logo -->
    <img src="OPI.jpg" alt="Company Logo" onerror="this.onerror=null; this.src='default-logo.png';">

    <!-- Main Title and Subtitle -->
    <h1>Emax Press Shade Conversion</h1>
    <h3>Please input all shades provided on the prescription.</h3>

    <!-- Shade Input Form -->
    <label>Incisal Shade (RX): <input type="text" id="incisal"></label><br>
    <label>Body/Mid Shade: <input type="text" id="body"></label><br>
    <label>Gingival Shade: <input type="text" id="gingival"></label><br>
    <label>Stump Shade (ND1-ND9, ST1-ST9): <input type="text" id="stump"></label><br> <!-- Stump Shade Input -->
    <button onclick="displayShade()">Submit</button>

    <!-- Output Section -->
    <p>Selected Shade: <span id="output"></span></p>
    <p>Shade Categories: <span id="categories"></span></p>

    <script>
        // Mapping of Stump Shades to corresponding Puck Shades
        const stumpShadeMapping = {
            "ND1": "A1", "ND2": "A1", "ND3": "A2", "ND4": "A3", "ND5": "A3.5",
            "ND6": "B1", "ND7": "B2", "ND8": "B3", "ND9": "C1",
            "ST1": "A1", "ST2": "A2", "ST3": "A3", "ST4": "A3.5", "ST5": "B1",
            "ST6": "B2", "ST7": "B3", "ST8": "C1", "ST9": "C2"
        };

        // Mapping of Material Types (MT, LT, HT, MO, HO) based on Stump Shade & Final Shade
        const materialTypeMapping = {
            "A1": { "ND1": ["MTA1", "LTA1", "HTA1", "MO1", "HO1"], "ND2": ["MTA1", "LTA1", "HTA1", "MO1", "HO1"] },
            "A2": { "ND2": ["MTA2", "LTA2", "HTA2", "MO2", "HO1"], "ND3": ["MTA2", "LTA2", "HTA2", "MO2", "HO2"] },
            "A3": { "ND3": ["MTA3", "LTA3", "HTA3", "MO3", "HO2"], "ND4": ["MTA3", "LTA3", "HTA3", "MO3", "HO3"] },
            "A3.5": { "ND4": ["MTA3.5", "LTA3.5", "HTA3.5", "MO4", "HO3"], "ND5": ["MTA3.5", "LTA3.5", "HTA3.5", "MO4", "HO4"] },
            "B1": { "ND6": ["MTB1", "LTB1", "HTB1", "MO1", "HO1"], "ND1": ["MTB1", "LTB1", "HTB1", "MO1", "HO1"] },
            "B2": { "ND7": ["MTB2", "LTB2", "HTB2", "MO3", "HO2"], "ND2": ["MTB2", "LTB2", "HTB2", "MO3", "HO2"] },
            "B3": { "ND8": ["MTB3", "LTB3", "HTB3", "MO3", "HO1"], "ND3": ["MTB3", "LTB3", "HTB3", "MO3", "HO1"] },
            "C1": { "ND9": ["MTC1", "LTC1", "HTC1", "MO1", "HO1"], "ND4": ["MTC1", "LTC1", "HTC1", "MO1", "HO1"] }
        };

        function displayShade() {
            // Get input values
            let incisalShade = document.getElementById("incisal").value.trim().toUpperCase();
            let bodyShade = document.getElementById("body").value.trim().toUpperCase();
            let gingivalShade = document.getElementById("gingival").value.trim().toUpperCase();
            let stumpShade = document.getElementById("stump").value.trim().toUpperCase();

            // Remove extra spaces from stump shade input
            stumpShade = stumpShade.replace(/\s+/g, "");

            // Convert Stump Shade to Puck Shade
            let convertedStump = stumpShadeMapping[stumpShade] || "";

            // Determine the final shade (priority: Incisal > Body > Gingival > Stump)
            let finalShade = incisalShade || bodyShade || gingivalShade || convertedStump || "No shade entered";

            // Find matching Material Types based on Final Shade & Stump Shade
            let categories = materialTypeMapping[finalShade] && materialTypeMapping[finalShade][stumpShade] 
                ? materialTypeMapping[finalShade][stumpShade] 
                : ["No matching categories"];

            // Display the selected shade and material types
            document.getElementById("output").innerText = finalShade;
            document.getElementById("categories").innerText = categories.join(", ");
        }
    </script>

</body>
</html>
