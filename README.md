
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
        // Full mapping for all shades (A1-D4, OM1-OM3) with ND1-ND9 stump shades
        const materialTypeMapping = {
            "A1": {
                "ND1": ["MTA1", "LTA1", "HTA1", "MO1", "HO1"],
                "ND2": ["MTA1", "LTA1", "HTA1", "MO1", "HO1"],
                "ND3": ["MTBL4", "LTBL4", "HTBL4", "MO1", "HO1"],
                "ND4": ["LTBL3", "MO1", "HO1"],
                "ND5": ["LTBL4", "MO1", "HO1"],
                "ND6": ["LTBL3", "MO1", "HO1"],
                "ND7": ["LTBL2", "MO1", "HO1"],
                "ND8": ["HO1"],
                "ND9": ["HO1"]
            },
            "A2": {
                "ND1": ["MTA2", "LTA2", "HTA2", "MO2", "HO2"],
                "ND2": ["MTA2", "LTA2", "HTA2", "MO2", "HO2"],
                "ND3": ["MTBL4", "LTBL4", "HTBL4", "MO2", "HO2"],
                "ND4": ["LTBL3", "MO2", "HO2"],
                "ND5": ["LTBL4", "MO2", "HO2"],
                "ND6": ["LTBL3", "MO2", "HO2"],
                "ND7": ["LTBL2", "MO2", "HO2"],
                "ND8": ["HO2"],
                "ND9": ["HO2"]
            },
            "A3": {
                "ND1": ["MTA3", "LTA3", "HTA3", "MO3", "HO2"],
                "ND2": ["MTA3", "LTA3", "HTA3", "MO3", "HO2"],
                "ND3": ["MTBL4", "LTBL4", "HTBL4", "MO3", "HO2"],
                "ND4": ["LTBL3", "MO3", "HO2"],
                "ND5": ["LTBL4", "MO3", "HO2"],
                "ND6": ["LTBL3", "MO3", "HO2"],
                "ND7": ["LTBL2", "MO3", "HO2"],
                "ND8": ["HO2"],
                "ND9": ["HO2"]
            },
            "D3": {
                "ND1": ["MTD3", "LTD3", "HTD3", "MO3", "HO3"],
                "ND2": ["MTD3", "LTD3", "HTD3", "MO3", "HO3"],
                "ND3": ["MTBL4", "LTBL4", "HTBL4", "MO3", "HO3"],
                "ND4": ["LTBL3", "MO3", "HO3"],
                "ND5": ["LTBL4", "MO3", "HO3"],
                "ND6": ["LTBL3", "MO3", "HO3"],
                "ND7": ["LTBL2", "MO3", "HO3"],
                "ND8": ["HO3"],
                "ND9": ["HO3"]
            }
        };

        function displayShade() {
            // Get user input and format correctly
            let incisalShade = document.getElementById("incisal").value.trim().toUpperCase();
            let bodyShade = document.getElementById("body").value.trim().toUpperCase();
            let gingivalShade = document.getElementById("gingival").value.trim().toUpperCase();
            let stumpShade = document.getElementById("stump").value.trim().toUpperCase();

            // Remove extra spaces from stump shade input
            stumpShade = stumpShade.replace(/\s+/g, "");

            // Determine the final shade (priority: Incisal > Body > Gingival)
            let finalShade = incisalShade || bodyShade || gingivalShade || "No shade entered";

            // If the shade exists in the mapping, check the stump shade mapping
            let categories = [];
            if (materialTypeMapping[finalShade] && materialTypeMapping[finalShade][stumpShade]) {
                categories = materialTypeMapping[finalShade][stumpShade];
            } else {
                categories = ["No matching categories"];
            }

            // Display the selected shade and material types
            document.getElementById("output").innerText = finalShade;
            document.getElementById("categories").innerText = categories.join(", ");
        }
    </script>

</body>
</html>