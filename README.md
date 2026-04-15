<!DOCTYPE html>
<html lang="zh-TW">
<head>
  <meta charset="UTF-8">
  <title>團險報名系統</title>
</head>
<body>

<h2>團體保險報名表</h2>

<form id="insuranceForm">
  <label>公司名稱：</label><br>
  <input type="text" name="company" required><br><br>

  <label>統一編號：</label><br>
  <input type="text" name="taxId" required><br><br>

  <label>投保人數：</label><br>
  <input type="number" name="people" required><br><br>

  <label>職業編號：</label><br>
  <input type="text" name="jobCode"><br><br>

  <label>原投保壽險公司：</label><br>
  <input type="text" name="insuranceCompany"><br><br>

  <button type="submit">送出</button>
</form>

<script>
document.getElementById("insuranceForm").addEventListener("submit", function(e) {
  e.preventDefault();

  const formData = new FormData(this);
  const data = Object.fromEntries(formData);

  console.log(data);

  alert("資料已送出！");
});
</script>

</body>
</html>
