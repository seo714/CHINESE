<html lang="ko">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Chinese Phrases</title>
<style>
    body {
        display: flex;
        justify-content: center;
        align-items: center;
        min-height: 100vh;
        font-family: Arial, sans-serif;
        margin: 0;
        background-color: #f5f5f5;
    }
    .container {
        width: 90%;
        max-width: 600px;
        background-color: white;
        padding: 20px;
        box-shadow: 0 4px 10px rgba(0,0,0,0.1);
        border-radius: 12px;
        overflow-x: auto;
    }
    table {
        width: 100%;
        border-collapse: collapse;
    }
    table, th, td {
        border: 1px solid #ddd;
    }
    th, td {
        padding: 8px;
        text-align: center;
    }
    th {
        background-color: #f2f2f2;
    }
    @media (max-width: 600px) {
        th, td {
            font-size: 14px;
            padding: 6px;
        }
    }
</style>
</head>
<body>
<div class="container">
    <table id="phraseTable">
        <thead></thead>
        <tbody></tbody>
    </table>
</div>

<script>
fetch('chinese_phrases.xlsx')
.then(response => response.text())
.then(data => {
    const lines = data.split('\n').filter(line => line.trim() !== '');
    const table = document.getElementById('phraseTable');
    const thead = table.querySelector('thead');
    const tbody = table.querySelector('tbody');

    // 헤더
    const headers = lines[0].split(',');
    const trHead = document.createElement('tr');
    headers.forEach(h => {
        const th = document.createElement('th');
        th.textContent = h;
        trHead.appendChild(th);
    });
    thead.appendChild(trHead);

    // 데이터
    for(let i=1; i<lines.length; i++){
        const tr = document.createElement('tr');
        const cells = lines[i].split(',');
        cells.forEach(c => {
            const td = document.createElement('td');
            td.textContent = c;
            tr.appendChild(td);
        });
        tbody.appendChild(tr);
    }
});
</script>
</body>
</html>
