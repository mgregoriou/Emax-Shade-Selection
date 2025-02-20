
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
    <label>Stump Shade (ND1-ND9, ST1-ST9): <input type="text" id="stump"></label><br>
    <button onclick="displayShade()">Submit</button>

    <!-- Output Section -->
    <p>Selected Shade: <span id="output"></span></p>
    <p>Shade Categories: <span id="categories"></span></p>

    <script>
        // Stump Shade Mapping (from Emax Press PDF)
        const stumpShadeMapping = {
            "ND1": "A1", "ND2": "A2", "ND3": "A3", "ND4": "A3.5", "ND5": "B1",
            "ND6": "B2", "ND7": "B3", "ND8": "C1", "ND9": "C2",
            "ST1": "A1", "ST2": "A2", "ST3": "A3", "ST4": "A3.5", "ST5": "B1",
            "ST6": "B2", "ST7": "B3", "ST8": "C1", "ST9": "C2"
        };

        // Material Types Mapping (MT, LT, HT, MO, HO) from the Emax Press PDF
        const materialTypeMapping = {
            "A1": { "ND1": ["MTA1", "LTA1", "HTA1", "MO1", "HO1"], "ND2": ["MTA1", "LTA1", "HTA1", "MO1", "HO1"] },
            "A2": { "ND2": ["MTA2", "LTA2", "HTA2", "MO2", "HO1"], "ND3": ["MTA2", "LTA2", "HTA2", "MO2", "HO2"] },
            "A3": { "ND3": ["MTA3", "LTA3", "HTA3", "MO3", "HO2"], "ND4": ["MTA3", "LTA3", "HTA3", "MO3", "HO3"] },
            "A3.5": { "ND4": ["MTA3.5", "LTA3.5", "HTA3.5", "MO4", "HO3"], "ND5": ["MTA3.5", "LTA3.5", "HTA3.5", "MO4", "HO4"] },
            "B1": { "ND5": ["MTB1", "LTB1", "HTB1", "MO1", "HO1"] },
            "B2": { "ND6": ["MTB2", "LTB2", "HTB2", "MO3", "HO2"], "ND9": ["MTB2", "LTB2", "HTB2", "MO3", "HO2"] },
            "B3": { "ND7": ["MTB3", "LTB3", "HTB3", "MO3", "HO1"] },
            "C1": { "ND8": ["MTC1", "LTC1", "HTC1", "MO1", "HO1"], "ND4": ["MTC1", "LTC1", "HTC1", "MO1", "HO1"] },
            "C2": { "ND9": ["MTC2", "LTC2", "HTC2", "MO2", "HO2"] },
            "D2": { "ND3": ["MTD2", "LTD2", "HTD2", "MO2", "HO2"] },
            "D3": { "ND5": ["MTD3", "LTD3", "HTD3", "MO3", "HO3"] },
            "D4": { "ND7": ["MTD4", "LTD4", "HTD4", "MO4", "HO4"] }
        };

        function displayShade() {
            // Get input values and format them correctly
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