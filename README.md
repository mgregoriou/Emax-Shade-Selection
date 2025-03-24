<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>Emax Press Shade Selector</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      text-align: center;
      padding: 20px;
    }
    img {
      width: 300px;
      margin-bottom: 10px;
    }
    h1 {
      font-size: 22px;
    }
    label {
      display: block;
      margin: 8px 0;
    }
    input {
      padding: 5px;
      text-transform: uppercase;
    }
    button {
      padding: 10px 16px;
      background-color: #007bff;
      color: white;
      border: none;
      margin-top: 10px;
      cursor: pointer;
    }
    button:hover {
      background-color: #0056b3;
    }
    .output {
      margin-top: 20px;
      font-weight: bold;
    }
  </style>
</head>
<body>

  <!-- Logo -->
  <img src="logo.png" alt="Company Logo" onerror="this.style.display='none'">
  <h1>Emax Press Shade Selector</h1>

  <!-- Shade Input Form -->
  <label>Incisal Shade:
    <input type="text" id="incisal">
  </label>
  <label>Body Shade:
    <input type="text" id="body">
  </label>
  <label>Gingival Shade:
    <input type="text" id="gingival">
  </label>
  <label>Stump Shade (ND1–ND9):
    <input type="text" id="stump">
  </label>

  <button onclick="getMaterials()">Get Material Options</button>

  <!-- Output -->
  <div class="output">
    <p>Selected Base Shade: <span id="baseShade">-</span></p>
    <p>Suggested Materials: <span id="materials">-</span></p>
  </div>

  <!-- Mapping + Script -->
  <script>
    // Paste your full materialTypeMapping here (shortened here for demo)
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
      // ... rest of your full map continues here ...
    };

    function getMaterials() {
      const incisal = document.getElementById('incisal').value.trim().toUpperCase();
      const body = document.getElementById('body').value.trim().toUpperCase();
      const gingival = document.getElementById('gingival').value.trim().toUpperCase();
      const stump = document.getElementById('stump').value.trim().toUpperCase();

      // Priority: Incisal > Body > Gingival
      const baseShade = incisal || body || gingival;

      let result = [];
      if (materialTypeMapping[baseShade] && materialTypeMapping[baseShade][stump]) {
        result = materialTypeMapping[baseShade][stump];
      }

      document.getElementById('baseShade').textContent = baseShade || "Not Found";
      document.getElementById('materials').textContent = result.length ? result.join(", ") : "No match found";
    }
  </script>

</body>
</html>
