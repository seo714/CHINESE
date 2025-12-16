<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8" />
  <title>Chinese Words</title>

  <!-- SheetJS (xlsx 읽기용) -->
  <script src="https://cdn.jsdelivr.net/npm/xlsx/dist/xlsx.full.min.js"></script>

  <style>
    body {
      margin: 0;
      font-family: Arial, sans-serif;
      background-color: #f5f5f5;
    }

    .container {
      width: 100%;
      text-align: center;
      margin-top: 40px;
    }

    h1 {
      font-size: 48px;
      margin: 0;
    }

    h2 {
      font-size: 24px;
      margin-top: 10px;
      color: #555;
    }

    table {
      margin: 40px auto;
      border-collapse: collapse;
      background: white;
    }

    th, td {
      border: 1px solid #ccc;
      padding: 8px 14px;
      text-align: center;
    }

    th {
      background-color: #eee;
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>CHINESE</h1>
    <h2>WORDS</h2>

    <div id="table-container"></div>
  </div>

  <script>
    fetch("final.xlsx")
      .then(res => res.arrayBuffer())
      .then(data => {
        const workbook = XLSX.read(data, { type: "array" });
        const sheet = workbook.Sheets[workbook.SheetNames[0]];
        const json = XLSX.utils.sheet_to_json(sheet, { header: 1 });
        renderTable(json);
      });

    function renderTable(data) {
      let html = "<table>";

      data.forEach((row, rowIndex) => {
        html += "<tr>";

        row.forEach((cell, colIndex) => {
          // ❌ 2번째 열(colIndex === 1) 제외
          if (colIndex === 1) return;

          if (rowIndex === 0) {
            html += `<th>${cell ?? ""}</th>`;
          } else {
            html += `<td>${cell ?? ""}</td>`;
          }
        });

        html += "</tr>";
      });

      html += "</table>";
      document.getElementById("table-container").innerHTML = html;
    }
  </script>
</body>
</html>
