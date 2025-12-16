<html lang="ko">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>WORDS</title>

  <!-- Google Font : Poppins -->
  <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;500;600&display=swap" rel="stylesheet">

  <!-- SheetJS -->
  <script src="https://cdn.jsdelivr.net/npm/xlsx/dist/xlsx.full.min.js"></script>

  <style>
    body {
      margin: 0;
      background-color: #f5f5f5;
      display: flex;
      justify-content: center;
      font-family: 'Poppins', system-ui, sans-serif;
    }

    .container {
      margin-top: 32px;
      width: 100%;
      max-width: 600px;
      padding: 0 12px;
      text-align: center;
    }

    .title {
      font-size: 28px;
      font-weight: 600;
      letter-spacing: 2px;
      margin-bottom: 24px;
    }

    table {
      width: 100%;
      border-collapse: collapse;
      table-layout: fixed; /* ✅ 열 균등 */
    }

    tr {
      width: 100%;
    }

    td {
      width: 100%;
      display: block;          /* ✅ 칸 느낌 제거 */
      border: none;
      padding: 14px 8px;
      font-size: 17px;
      background: white;       /* 행 단위 배경 */
      margin-bottom: 8px;      /* 행 간격 */
      word-break: break-word;
    }

    /* 모바일에서 살짝 더 크게 */
    @media (max-width: 480px) {
      td {
        font-size: 18px;
      }
    }
  </style>
</head>
<body>
  <div class="container">
    <div class="title">CHINESE</div>
    <div id="table-container"></div>
  </div>

  <script>
    fetch("final.xlsx")
      .then(res => res.arrayBuffer())
      .then(data => {
        const workbook = XLSX.read(data, { type: "array" });
        const sheet = workbook.Sheets[workbook.SheetNames[0]];
        let json = XLSX.utils.sheet_to_json(sheet, { header: 1 });

        // 첫 행 제거
        json.shift();

        renderTable(json);
      });

    function renderTable(data) {
      let html = "<table>";

      data.forEach(row => {
        html += "<tr>";
        row.forEach((cell, colIndex) => {
          // 2번째 열 제거
          if (colIndex === 1) return;
          html += `<td>${cell ?? ""}</td>`;
        });
        html += "</tr>";
      });

      html += "</table>";
      document.getElementById("table-container").innerHTML = html;
    }
  </script>
</body>
</html>
