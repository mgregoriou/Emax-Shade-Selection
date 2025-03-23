
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
                "ND1": ["MTA1", "LTA1", "HTA1", "MO1", "HO1"],
                "ND2": ["MTA1", "LTA1", "HTA1", "MO1", "HO1"],
                "ND3": ["MTA1", "LTA1", "HTBL4", "MO1", "HO1"],
                "ND4": ["MTBL3", "LTA1", "MO1", "HO1"],
                "ND5": ["LTA1", "HTBL2", "MO1", "HO1"],
                "ND6": ["LTA1", "HTBL2", "MO1", "HO1"],
                "ND7": ["LTA1", "MO1", "HO1"],
                "ND8": ["HO1"],
                "ND9": ["HO1"]
            },
            "A3": {
                "ND1": ["MTA2", "LTA2", "HTA2", "MO2", "HO2"],
                "ND2": ["MTA2", "LTA2", "HTA2", "MO2", "HO2"],
                "ND3": ["MTA2", "LTA2", "HTA2", "MO2", "HO2"],
                "ND4": ["MTA2", "LTA2", "MO2", "HO2"],
                "ND5": ["MTA1", "LTA2", "HTBL3", "MO2", "HO2"],
                "ND6": ["MTA1", LTA2", "HTBL2", "MO2", "HO2"],
                "ND7": ["MTBL2", "LTA2", "MO2", "HO2"],
                "ND8": ["HO2"],
                "ND9": ["HO2"]
            },
"A3.5": {
                "ND1": ["MTA3", "LTA3", "HTA3", "MO2", "HO2"],
                "ND2": ["MTA3", "LTA2", "HTA3", "MO2", "HO2"],
                "ND3": ["MTA2", "LTA3", "HTA3", "MO2", "HO2"],
                "ND4": ["MTA2", "LTA3", "HTB3", "MO2", "HO2"],
                "ND5": ["MTA2", "LTA3", "HTA3", "MO2", "HO2"],
                "ND6": ["MTA2", "LTA3", "HTBL2", "MO2", "HO2"],
                "ND7": ["LTA3", "MO2", "HO2"],
                "ND8": ["LTA3", "HO2"],
                "ND9": ["HO2"]
            },
"A4": {
                "ND1": ["MTA3.5", "LTA3.5", "HTA3.5", "MO4", "HO2"],
                "ND2": ["MTA3.5", "LTA3.5", "HTA3.5", "MO4", "HO2"],
                "ND3": ["MTA3", "LTA3.5", "HTA3.5", "MO4", "HO2"],
                "ND4": ["MTA3", "LTA3.5", "HTB3", "MO4", "HO2"],
                "ND5": ["MTA3", "LTA3.5", "HTA3.5", "MO4", "HO2"],
                "ND6": ["MTA3", "LTA3.5", "HTA3", "MO4", "HO2"],
                "ND7": ["MTA2", "LTA3.5", "MO4", "HO2"],
                "ND8": ["LTA3.5", "HO2"],
                "ND9": ["HO2"]
            },
"B1": {
                "ND1": ["MTB1", "LTB1", "HTB1", "MO1", "HO1"],
                "ND2": ["MTB1", "LTB1", "HTBL4", "MO1", "HO1"],
                "ND3": ["MTBL4", "LTB1", "HTBL3", "MO1", "HO1"],
                "ND4": ["MTBL3", "LTBL3", "MO1", "HO1"],
                "ND5": ["MTBL2", "LTBL3", "MO1", "HO1"],
                "ND6": ["LTBL3", "MO1", "HO1"],
                "ND7": ["LTBL3", "MO1", "HO1"],
                "ND8": ["HO1"],
                "ND9": ["HO1"]
            },
"B2": {
                "ND1": ["MTB1", "LTB1", "HTB1", "MO1", "HO1"],
                "ND2": ["MTB1", "LTB1", "HTBL4", "MO1", "HO1"],
                "ND3": ["MTB1", "LTB1", "HTBL3", "MO1", "HO1"],
                "ND4": ["MTBL4", "LTBL3", "MO1", "HO1"],
                "ND5": ["MTBL3", "LTB1", "HTBL2", "MO1", "HO1"],
                "ND6": ["LTB1", "MO1", "HO1"],
                "ND7": ["LTB1", "MO1", "HO1"],
                "ND8": ["HO1"],
                "ND9": ["HO1"]
            },
"B3": {
                "ND1": ["MTB2", "LTB2", "HTB2", "MO3", "HO1"],
                "ND2": ["MTB2", "LTB2", "HTB2", "MO3", "HO1"],
                "ND3": ["MTB2", "LTB2", "HTB2", "MO3", "HO1"],
                "ND4": ["MTB1", "LTB2", "HTBL2" "MO3", "HO1"],
                "ND5": ["MTBL4", "LTB2", "HTBL3", "MO3", "HO1"],
                "ND6": ["MTBL4", "LTB2", "HTBL2", "MO3", "HO1"],
                "ND7": ["LTB2", "HTBL1", "MO3", "HO1"],
                "ND8": ["HO1"],
                "ND9": ["HO1"]
            },
"B4": {
                "ND1": ["MTA3.5", "LTB3", "HTB3", "MO3", "HO1"],
                "ND2": ["MTA3.5", "LTB3", "HTB3", "MO3", "HO1"],
                "ND3": ["MTA3", "LTB3", "HTB2", "MO3", "HO1"],
                "ND4": ["MTB2", "LTB3", "HTBL3", "MO3", "HO1"],
                "ND5": ["MTBL4", "LTB3", "HTBL3", "MO3", "HO1"],
                "ND6": ["LTB3", "HTBL1", "MO3", "HO1"],
                "ND7": ["LTB2", "HTB2", "MO3", "HO1"],
                "ND8": ["LTB2", "HTB2", "HO1"],
                "ND9": ["HO1"]
            },
"C1": {
                "ND1": ["MTC1", "LTC1", "HTC1", "MO1", "HO1"],
                "ND2": ["MTC1", "LTC1", "HTC1", "MO1", "HO1"],
                "ND3": ["MTC1", "LTC1", "HTBL4", "MO1", "HO1"],
                "ND4": ["MTB1", "LTC1", "HTBL3", "MO1", "HO1"],
                "ND5": ["MTB1", "LTC1", "HTBL3", "MO1", "HO1"],
                "ND6": ["MTB1", "LTC1", "MO1", "HO1"],
                "ND7": ["MTB1", "LTC1", "HTA1", "MO1", "HO1"],
                "ND8": ["LTC1", "HTC1", HO1"],
                "ND9": ["HO1"]
            },
"C2": {
                "ND1": ["MTC1", "LTC1", "HTC1", "MO4", "HO2"],
                "ND2": ["MTC1", "LTC1", "HTC1", "MO4", "HO2"],
                "ND3": ["MTC1", "LTC1", "HTBL4", "MO4", "HO2"],
                "ND4": ["MTC1", "LTC1", "HTB1", "MO4", "HO2"],
                "ND5": ["MTA2", "LTC1", "HTA1", "MO4", "HO2"],
                "ND6": ["MTA2", "LTB2", "HTB1", "MO4", "HO2"],
                "ND7": ["MTA3", "LTB2", "HTA3", "MO4", "HO2"],
                "ND8": ["LTB2", "HTB2", HO2"],
                "ND9": ["HO2"]
            },
"C3": {
                "ND1": ["MTC2", "LTC2", "HTC2", "MO4", "HO2"],
                "ND2": ["MTC2", "LTC2", "HTC2", "MO4", "HO2"],
                "ND3": ["MTC2", "LTC2", "HTC2", "MO4", "HO2"],
                "ND4": ["MTA3", "LTC2", "HTB3", "MO4", "HO2"],
                "ND5": ["MTA3", "LTC2", "HTA3", "MO4", "HO2"],
                "ND6": ["MTA3", "LTC2", "HTB2", "MO4", "HO2"],
                "ND7": ["MTA3", "LTC2", "HTA3.5", "MO4", "HO2"],
                "ND8": ["MTA3", "LTC2", "HTC2", HO2"],
                "ND9": ["HO2"]
            },
"C4": {
                "ND1": ["MTA3.5", "LTC3", "HTC3", "MO4", "HO2"],
                "ND2": ["MTA3.5", "LTC3", "HTC3", "MO4", "HO2"],
                "ND3": ["MTA3", "LTC3", "HTB4", "MO4", "HO2"],
                "ND4": ["MTA3", "LTC3", "HTC2", "MO4", "HO2"],
                "ND5": ["MTA3", "LTC3", "HTB3", "MO4", "HO2"],
                "ND6": ["MTA3", "LTC3", "HTB3", "MO4", "HO2"],
                "ND7": ["MTA3", "LTC3", "HTA4", "MO4", "HO2"],
                "ND8": ["LTC3", "HTC3", HO2"],
                "ND9": ["HO2"]
            },
 "D2": {
                "ND1": ["MTD2", "LTD2", "HTD2", "MO4", "HO2"],
                "ND2": ["MTD2", "LTD2", "HTD2", "MO4", "HO2"],
                "ND3": ["MTD2", "LTD2", "HTB1", "MO4", "HO2"],
                "ND4": ["MTB1", "LTD2", "HTBL3", "MO4", "HO2"],
                "ND5": ["MTB1", "LTD2", "HTBL3", "MO4", "HO2"],
                "ND6": ["MTB1", "LTD2", "HTBL2", "MO4", "HO2"],
                "ND7": ["MTB1", "LTD2", "HTB1", "MO4", "HO2"],
                "ND8": ["MTA1", "LTD2", "HTD2", HO2"],
                "ND9": ["HO2"]
            }
        };
            "D3": {
                "ND1": ["MTD2", "LTD2", "HTD2", "MO4", "HO2"],
                "ND2": ["MTD2", "LTD2", "HTD2", "MO4", "HO2"],
                "ND3": ["MTD2", "LTD2", "HTD2", "MO4", "HO2"],
                "ND4": ["MTB2", "LTB2", "HTB1", "MO4", "HO2"],
                "ND5": ["MTA2", "LTB2", "HTA2", "MO4", "HO2"],
                "ND6": ["MTA2", LTB2", "HTBL2", "MO4", "HO2"],
                "ND7": ["MTA2", "LTB2", "HTBL2", "MO4", "HO2"],
                "ND8": ["LTB2", "HTB2", HO2"],
                "ND9": ["HO2"]
            }
 "D4": {
                "ND1": ["MTD2", "LTD2", "HTD2", "MO4", "HO2"],
                "ND2": ["MTD2", "LTD2", "HTD2", "MO4", "HO2"],
                "ND3": ["MTD2", "LTD2", "HTD2", "MO4", "HO2"],
                "ND4": ["MTB2", "LTB2", "HTB1", "MO4", "HO2"],
                "ND5": ["MTA2", "LTB2", "HTA2", "MO4", "HO2"],
                "ND6": ["MTA2", LTB2", "HTBL2", "MO4", "HO2"],
                "ND7": ["MTA2", "LTB2", "HTBL2", "MO4", "HO2"],
                "ND8": ["LTB2", "HTB2", HO2"],
                "ND9": ["HO2"]
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
