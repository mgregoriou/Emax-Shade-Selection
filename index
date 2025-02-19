
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

    <!-- Corrected Company Logo Reference -->
    <img src="OPI.jpg" alt="Company Logo" onerror="this.onerror=null; this.src='default-logo.png';">

    <!-- Main Title and Subtitle -->
    <h1>Emax Press Shade Conversion</h1>
    <h3>Please input all shades provided on the prescription.</h3>

    <!-- Shade Input Form -->
    <label>Incisal Shade (RX): <input type="text" id="incisal"></label><br>
    <label>Body/Mid Shade: <input type="text" id="body"></label><br>
    <label>Gingival Shade: <input type="text" id="gingival"></label><br>
    <label>Stump Shade: <input type="text" id="stump"></label><br> <!-- Stump Shade Input -->
    <button onclick="displayShade()">Submit</button>

    <!-- Output Section -->
    <p>Selected Shade: <span id="output"></span></p>
    <p>Shade Categories: <span id="categories"></span></p>

    <script>
        // Full RX Shade to Puck Shade conversion mapping (Bioform, 3D Master, Chromascope, Vita Classic, Bleach)
        const shadeConversion = {
            // Vita Classic & 3D Master
            "A1": "A1", "A2": "A1", "A3": "A2", "A3.5": "A3", "A4": "A3.5",
            "B1": "B1", "B2": "B1", "B3": "B2", "B4": "B3",
            "C1": "C1", "C2": "C1", "C3": "C2", "C4": "C3",
            "D2": "B2", "D3": "A3", "D4": "A3",
            "OM1": "OM1", "OM2": "OM2", "OM3": "OM3",
            // 3D Master Conversions
            "1M1": "B1", "1M2": "A1", "2L1.5": "A1", "2L2.5": "A2", "2M1": "A1",
            "3M1": "C1", "3M2": "D3", "3M3": "A3.5",
            // Chromascope Conversions
            "110": "A1", "120": "A1/A2", "130": "A2", "140": "A2",
            "210": "A3", "220": "A3", "230": "A3.5",
            // Bioform Conversions
            "B51": "A1", "B52": "B2", "B53": "A2", "B54": "A3",
            "B69": "D4", "B77": "C2", "B81": "C3"
        };

        // Stump Shade to Puck Shade conversion
        const stumpShadeConversion = {
            "ND1": "A1", "ND2": "A1", "ND3": "A2", "ND4": "A3",
            "ND5": "A3.5", "ND6": "B1", "ND7": "B2", "ND8": "B3", "ND9": "C1"
        };

        // Shade Categories (MT, LT, HT, MO, HO) based on Stump Shade Influence
        const categoryMapping = {
            "A1": ["MTA1", "LTA1", "HTA1", "MO1", "HO1"],
            "A2": ["MTA2", "LTA2", "HTA2", "MO2", "HO1"],
            "A3": ["MTA3", "LTA3", "HTA3", "MO2", "HO2"],
            "A3.5": ["MTA3.5", "LTA3.5", "HTA3.5", "MO4", "HO2"],
            "B1": ["MTB1", "LTB1", "HTB1", "MO1", "HO1"],
            "B2": ["MTB2", "LTB2", "HTB2", "MO3", "HO1"],
            "D4": ["MTD4", "LTD4", "HTD4", "MO4", "HO3"],
            "OM1": ["MTBL1", "LTBL1", "HTBL1", "MO0", "HO0"]
        };

        function displayShade() {
            // Get input values
            let incisalShade = document.getElementById("incisal").value.trim().toUpperCase();
            let bodyShade = document.getElementById("body").value.trim().toUpperCase();
            let gingivalShade = document.getElementById("gingival").value.trim().toUpperCase();
            let stumpShade = document.getElementById("stump").value.trim().toUpperCase();

            // Convert RX shades to Puck shades
            let convertedIncisal = shadeConversion[incisalShade] || "";
            let convertedBody = shadeConversion[bodyShade] || "";
            let convertedGingival = shadeConversion[gingivalShade] || "";
            let convertedStump = stumpShadeConversion[stumpShade] || "";

            // Determine the final shade (priority: Incisal > Body > Gingival > Stump)
            let finalShade = convertedIncisal || convertedBody || convertedGingival || convertedStump || "No shade entered";

            // Find shade categories
            let categories = categoryMapping[finalShade] || ["No matching categories"];

            // Display the selected shade and categories
            document.getElementById("output").innerText = finalShade;
            document.getElementById("categories").innerText = categories.join(", ");
        }
    </script>

</body>
</html>
