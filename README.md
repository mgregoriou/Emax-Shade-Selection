
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
            width: 500px; /* Increased logo size */
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
    <label>Stump Shade: <input type="text" id="stump"></label><br> <!-- New Stump Shade Input -->
    <button onclick="displayShade()">Submit</button>

    <!-- Output Section -->
    <p>Selected Shade: <span id="output"></span></p>
    <p>Shade Categories: <span id="categories"></span></p>

    <script>
        // RX Shade to Puck Shade conversion mapping
        const shadeConversion = {
            "A1": "A1", "A2": "A1", "A3": "A2", "A3.5": "A3", "A4": "A3.5",
            "B1": "B1", "B2": "B1", "B3": "B2", "B4": "B3",
            "C1": "C1", "C2": "C1", "C3": "C2", "C4": "C3",
            "D2": "B2", "D3": "A3", "D4": "A3",
            "OM1": "OM1", "OM2": "OM2", "OM3": "OM3",
            "3D": "OM3"
        };

        // Mapping for Shade Categories (MT, LT, HT, MO, HO) based on Stump Shade Influence
        const categoryMapping = {
            "A1": { "light": ["MTA1", "LTA1", "HTA1", "MO1", "HO1"], "dark": ["MO1", "HO2"] },
            "A2": { "light": ["MTA2", "LTA2", "HTA2", "MO2", "HO1"], "dark": ["MO2", "HO2"] },
            "A3": { "light": ["MTA3", "LTA3", "HTA3", "MO2", "HO2"], "dark": ["MO3", "HO2"] },
            "A3.5": { "light": ["MTA3.5", "LTA3.5", "HTA3.5", "MO4", "HO2"], "dark": ["MO4", "HO3"] },
            "A4": { "light": ["MTA4", "LTA4", "HTA4", "MO4", "HO2"], "dark": ["MO4", "HO3"] },
            "B1": { "light": ["MTB1", "LTB1", "HTB1", "MO1", "HO1"], "dark": ["MO1", "HO2"] },
            "B2": { "light": ["MTB2", "LTB2", "HTB2", "MO3", "HO1"], "dark": ["MO3", "HO2"] },
            "B3": { "light": ["MTB3", "LTB3", "HTB3", "MO3", "HO1"], "dark": ["MO3", "HO2"] },
            "B4": { "light": ["MTB4", "LTB4", "HTB4", "MO3", "HO1"], "dark": ["MO3", "HO2"] },
            "OM1": { "light": ["MTBL1", "LTBL1", "HTBL1", "MO0", "HO0"], "dark": ["MO1", "HO1"] },
            "OM2": { "light": ["MTBL2", "LTBL2", "HTBL2", "MO0", "HO0"], "dark": ["MO1", "HO1"] },
            "OM3": { "light": ["MTBL3", "LTBL3", "HTBL3", "MO0", "HO0"], "dark": ["MO1", "HO2"] }
        };

        function displayShade() {
            // Get input values
            let incisalShade = document.getElementById("incisal").value.trim().toUpperCase();
            let bodyShade = document.getElementById("body").value.trim().toUpperCase();
            let gingivalShade = document.getElementById("gingival").value.trim().toUpperCase();
            let stumpShade = document.getElementById("stump").value.trim().toLowerCase(); // Stump shade input (light or dark)

            console.log("Input Incisal Shade:", incisalShade);
            console.log("Input Body Shade:", bodyShade);
            console.log("Input Gingival Shade:", gingivalShade);
            console.log("Input Stump Shade:", stumpShade);

            // Convert RX shades to Puck shades
            let convertedIncisal = shadeConversion[incisalShade] || "";
            let convertedBody = shadeConversion[bodyShade] || "";
            let convertedGingival = shadeConversion[gingivalShade] || "";

            console.log("Converted Incisal Shade:", convertedIncisal);
            console.log("Converted Body Shade:", convertedBody);
            console.log("Converted Gingival Shade:", convertedGingival);

            // Determine the final shade
            let finalShade = convertedIncisal || convertedBody || convertedGingival || "No shade entered";

            // Determine shade categories based on stump shade
            let categories = categoryMapping[finalShade] 
                ? (stumpShade === "dark" ? categoryMapping[finalShade]["dark"] : categoryMapping[finalShade]["light"]) 
                : ["No matching categories"];

            console.log("Final Selected Shade:", finalShade);
            console.log("Matching Categories:", categories);

            // Display the selected shade and categories
            document.getElementById("output").innerText = finalShade;
            document.getElementById("categories").innerText = categories.join(", ");
        }
    </script>

</body>
</html>
