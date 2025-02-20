<!DOCTYPE html>
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
        // Correct mapping for A1 from the uploaded image
        const materialTypeMapping = {
            "A1": {
                "ND1": ["MTA1", "LTA1", "HTA1", "MO1", "HO1"],
                "ND2": ["MTA1", "LTA1", "HTA1", "MO1", "HO1"],
                "ND3": ["MTBL4", "LTBL4", "HTBL4", "MO1", "HO1"],
                "ND4": ["LTBL3", "MO1", "HO1"],
                "ND5": ["LTBL4", "MO1", "HO1"],
                "ND6": ["LTBL3", "MO1", "HO1"],
                "ND7": ["LTBL2", "MO1", "HO1"],
                "ND8": ["HO1"],  // Only HO1 for ND8
                "ND9": ["HO1"]   // Only HO1 for ND9
            }
        };

        function displayShade() {
            // Get input values and format correctly
            let incisalShade = document.getElementById("incisal").value.trim().toUpperCase();
            let bodyShade = document.getElementById("body").value.trim().toUpperCase();
            let gingivalShade = document.getElementById("gingival").value.trim().toUpperCase();
            let stumpShade = document.getElementById("stump").value.trim().toUpperCase();

            // Remove extra spaces from stump shade input
            stumpShade = stumpShade.replace(/\s+/g, "");

            // Determine the final shade (priority: Incisal > Body > Gingival)
            let finalShade = incisalShade || bodyShade || gingivalShade || "No shade entered";

            // If the final shade is A1, check stump shade mapping
            let categories = [];
            if (finalShade === "A1" && materialTypeMapping["A1"][stumpShade]) {
                categories = materialTypeMapping["A1"][stumpShade];
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