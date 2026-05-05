<!DOCTYPE html>
<html lang="zh-TW">
<head>
<meta charset="UTF-8">
<title>計分系統（低分獲勝）</title>
<style>
  body { font-family: Arial; padding: 20px; }
  table { border-collapse: collapse; margin-top: 20px; }
  td, th { border: 1px solid #ccc; padding: 8px; text-align: center; }
  input { width: 60px; }
  select { padding: 5px; }
  .winner { background-color: #d4edda; }
</style>
</head>
<body>

<h2>🎯 計分系統（低分獲勝）</h2>

人數：
<select id="playerCount" onchange="initTable()">
  <option value="4">4人</option>
  <option value="5">5人</option>
  <option value="6">6人</option>
  <option value="7">7人</option>
  <option value="8">8人</option>
</select>

<table id="scoreTable"></table>

<script>
const rounds = 5;

function initTable() {
  const count = parseInt(document.getElementById("playerCount").value);
  const table = document.getElementById("scoreTable");
  table.innerHTML = "";

  let header = "<tr><th>玩家</th>";
  for (let r = 1; r <= rounds; r++) {
    header += `<th>第${r}局</th>`;
  }
  header += "<th>總分</th><th>排名</th></tr>";
  table.innerHTML += header;

  for (let i = 0; i < count; i++) {
    let row = `<tr id="row${i}">
      <td>玩家${i+1}</td>`;

    for (let r = 0; r < rounds; r++) {
      row += `<td><input type="number" value="0" onchange="calculate()"></td>`;
    }

    row += `<td class="total">0</td>
            <td class="rank">-</td>
          </tr>`;

    table.innerHTML += row;
  }
}

function calculate() {
  const rows = document.querySelectorAll("#scoreTable tr");
  let scores = [];

  for (let i = 1; i < rows.length; i++) {
    let inputs = rows[i].querySelectorAll("input");
    let total = 0;

    inputs.forEach(input => {
      total += parseInt(input.value) || 0;
    });

    rows[i].querySelector(".total").innerText = total;

    scores.push({
      index: i,
      total: total
    });
  }

  // 低分排序（重點）
  scores.sort((a, b) => a.total - b.total);

  scores.forEach((player, i) => {
    let row = rows[player.index];
    row.querySelector(".rank").innerText = i + 1;
    row.classList.remove("winner");
  });

  // 第一名標綠
  rows[scores[0].index].classList.add("winner");
}

initTable();
</script>

</body>
</html>
