
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
        // Stump Shade Mapping (Ensuring all ND1-ND9 are included)
        const stumpShadeMapping = {
            "ND1": "A1", "ND2": "A2", "ND3": "A3", "ND4": "A3.5", "ND5": "B1",
            "ND6": "B2", "ND7": "B3", "ND8": "C1", "ND9": "C2"
        };

        // Full Material Type Mapping (Ensuring ALL stump shades map properly)
        const materialTypeMapping = {};
        const finalShades = ["A1", "A2", "A3", "A3.5", "A4", "B1", "B2", "B3", "B4", "C1", "C2", "C3", "C4", "D2", "D3", "D4", "OM1", "OM2", "OM3"];
        const stumpShades = ["ND1", "ND2", "ND3", "ND4", "ND5", "ND6", "ND7", "ND8", "ND9"];
        const materialTypes = ["MT", "LT", "HT", "MO", "HO"];

        // Generate full mapping dynamically
        finalShades.forEach(shade => {
            materialTypeMapping[shade] = {};
            stumpShades.forEach(stump => {
                materialTypeMapping[shade][stump] = materialTypes.map(type => `${type}${shade}`);
            });
        });

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