<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Gene Therapy Tracker</title>
    <script>
        async function loadStockData() {
            const sheetURL = "https://docs.google.com/spreadsheets/d/YOUR_SHEET_ID/gviz/tq?tqx=out:json";
            const response = await fetch(sheetURL);
            const text = await response.text();
            const json = JSON.parse(text.substr(47).slice(0, -2)); 
            let table = "<table border='1'><tr><th>Company</th><th>Symbol</th><th>Price</th></tr>";
            json.table.rows.forEach(row => {
                table += `<tr><td>${row.c[0].v}</td><td>${row.c[1].v}</td><td>${row.c[2].v}</td></tr>`;
            });
            table += "</table>";
            document.getElementById("stockData").innerHTML = table;
        }
        window.onload = loadStockData;
    </script>
</head>
<body>
    <h1>Gene Therapy Stock Tracker</h1>
    <div id="stockData">Loading...</div>
</body>
</html>
