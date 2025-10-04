<!DOCTYPE html>
<html lang="th">
<head>
  <meta charset="UTF-8">
  <title>โปรแกรมคำนวณกฎของโอห์ม (Ohm's Law)</title>
  <style>
    body { font-family: Tahoma; margin: 40px; background: #f4f6f7; }
    h1 { color: darkblue; }
    .box { background: #fff; padding: 20px; border-radius: 10px; width: 420px; }
    label { display: block; margin-top: 10px; }
    input, select { padding: 5px; margin-top: 5px; width: 100%; }
    button { margin-top: 15px; padding: 10px; width: 48%; }
    .result { margin-top: 20px; font-weight: bold; color: darkgreen; }
    .history { margin-top: 20px; background: #eef; padding: 10px; border-radius: 8px; }
  </style>
</head>
<body>
  <h1>โปรแกรมคำนวณกฎของโอห์ม (V = I × R)</h1>
  <div class="box">
    <label>แรงดันไฟฟ้า V:</label>
    <input type="number" id="voltage" placeholder="ใส่ค่า V ถ้ามี">
    <select id="v_unit">
      <option value="1">โวลต์ (V)</option>
      <option value="0.001">มิลลิโวลต์ (mV)</option>
    </select>

    <label>กระแสไฟฟ้า I:</label>
    <input type="number" id="current" placeholder="ใส่ค่า I ถ้ามี">
    <select id="i_unit">
      <option value="1">แอมป์ (A)</option>
      <option value="0.001">มิลลิแอมป์ (mA)</option>
    </select>

    <label>ความต้านทาน R:</label>
    <input type="number" id="resistance" placeholder="ใส่ค่า R ถ้ามี">
    <select id="r_unit">
      <option value="1">โอห์ม (Ω)</option>
      <option value="1000">กิโลโอห์ม (kΩ)</option>
    </select>

    <div style="display: flex; justify-content: space-between;">
      <button onclick="calculate()">คำนวณ</button>
      <button onclick="resetForm()">ล้างค่า</button>
    </div>

    <div class="result" id="output"></div>
    <div class="history">
      <h3>📜 ประวัติการคำนวณ</h3>
      <ul id="historyList"></ul>
    </div>
  </div>

  <script>
    function calculate() {
      let V = document.getElementById("voltage").value;
      let I = document.getElementById("current").value;
      let R = document.getElementById("resistance").value;

      let v_unit = document.getElementById("v_unit").value;
      let i_unit = document.getElementById("i_unit").value;
      let r_unit = document.getElementById("r_unit").value;

      let result = "";

      if (V == "" && I != "" && R != "") {
        let v = (I * i_unit) * (R * r_unit);
        result = `ใช้สูตร V = I × R → V = ${v.toFixed(3)} V`;
      }
      else if (I == "" && V != "" && R != "") {
        let i = (V * v_unit) / (R * r_unit);
        result = `ใช้สูตร I = V ÷ R → I = ${i.toFixed(3)} A`;
      }
      else if (R == "" && V != "" && I != "") {
        let r = (V * v_unit) / (I * i_unit);
        result = `ใช้สูตร R = V ÷ I → R = ${r.toFixed(3)} Ω`;
      }
      else {
        result = "⚠️ กรุณากรอกค่าอย่างน้อย 2 ค่า";
      }

      document.getElementById("output").innerText = result;
      addHistory(result);
    }

    function resetForm() {
      document.getElementById("voltage").value = "";
      document.getElementById("current").value = "";
      document.getElementById("resistance").value = "";
      document.getElementById("output").innerText = "";
    }

    function addHistory(entry) {
      let list = document.getElementById("historyList");
      let item = document.createElement("li");
      item.textContent = entry;
      list.appendChild(item);
    }
  </script>
</body>
</html>
