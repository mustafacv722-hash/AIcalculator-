Aicalculator 
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Al-Harithiya Calculator</title>
<script src="https://cdnjs.cloudflare.com/ajax/libs/decimal.js/10.4.3/decimal.min.js"></script>
<style>
body {
  margin:0;
  padding:0;
  font-family: Arial;
  background: linear-gradient(135deg,#0f0c29,#302b63,#24243e);
  color:white;
  display:flex;
  justify-content:center;
  align-items:center;
  min-height:100vh;
  text-align:center;
}

/* صفحة الترحيب */
#welcome {
  display:flex;
  flex-direction:column;
  justify-content:center;
  align-items:center;
}
#welcome h1 { font-size:24px; margin-bottom:20px; }
#welcome .desc { font-size:14px; margin:5px 0; }
#welcome button {
  background: rgba(255,255,255,0.1);
  border:2px solid #888;
  padding:20px 40px;
  font-size:18px;
  border-radius:20px;
  color:white;
  cursor:pointer;
  transition:0.3s;
  max-width:500px;
}
#welcome button:hover { transform: scale(1.05); }

/* صفحة الحاسبة */
#calculator {
  display:none;
  padding:20px;
  width:100%;
  max-width:600px;
  text-align:center;
  overflow:auto;
  max-height:100vh;
}
input {
  padding:12px;
  width:90%;
  font-size:18px;
  border-radius:10px;
  border:2px solid #888;
  text-align:center;
  background: rgba(0,0,0,0.3);
  color:#fff;
  backdrop-filter: blur(5px);
  margin-bottom:20px;
}

/* مربع الأزرار الرمزية */
#buttons-box {
  background: rgba(0,0,0,0.3);
  padding:15px;
  border-radius:15px;
  display:inline-block;
  margin-bottom:20px;
  border:2px solid #888;
}

/* الناتج والشرح */
#result-box {
  margin:10px auto;
  max-width:90%;
  text-align:center;
  border:2px solid #888;
  border-radius:12px;
  padding:10px;
  background: rgba(0,0,0,0.3);
}
#result, #explain {
  background: rgba(0,0,0,0.3);
  padding:10px;
  border-radius:12px;
  font-size:16px;
  min-height:40px;
  margin-bottom:5px;
  overflow-wrap:break-word;
  border:2px solid #888;
}

/* مربع القائمة الفيزيائية */
#physics-box {
  background: rgba(0,0,0,0.3);
  padding:15px;
  border-radius:15px;
  display:inline-block;
  margin-bottom:20px;
  max-width:90%;
  border:2px solid #888;
}

/* الأزرار */
.button-container, #physics-list {
  display:flex;
  justify-content:center;
  flex-wrap:wrap;
  gap:10px;
}
button.calc {
  padding:12px 18px;
  margin:5px;
  border:2px solid #888;
  cursor:pointer;
  border-radius:10px;
  color:white;
  background: rgba(0,0,0,0.3);
  backdrop-filter: blur(5px);
  transition:0.2s;
  font-size:18px;
}
button.calc:hover { transform: scale(1.05);}
#physics-list { max-height:0; overflow:hidden; transition:max-height 0.4s ease; margin-top:10px;}
#physics-list.open { max-height:1000px; }

/* المربع العائم للقوانين */
#overlay {
  display:none;
  position:fixed;
  top:0; left:0;
  width:100%;
  height:100%;
  background: rgba(0,0,0,0.7);
  justify-content:center;
  align-items:center;
  z-index:999;
}
#overlay .popup {
  background: rgba(0,0,0,0.3);
  border:2px solid #888;
  padding:20px;
  border-radius:15px;
  display:flex;
  flex-direction:column;
  gap:10px;
  width:300px;
}
#overlay .popup input {
  padding:10px;
  border-radius:10px;
  border:2px solid #888;
  background: rgba(0,0,0,0.2);
  color:white;
  text-align:center;
}
#overlay .popup button {
  padding:10px;
  border-radius:10px;
  border:2px solid #888;
  background: rgba(0,0,0,0.3);
  color:white;
  cursor:pointer;
}
</style>
</head>
<body>

<!-- صفحة الترحيب -->
<div id="welcome">
  <h1>Hi! Welcome to Al-Harithiya AI Calculator</h1>
  <button onclick="startCalculator()">Start</button>
  <div class="desc">This is a smart calculator powered by AI, containing the most famous physics and math formulas.</div>
  <div class="desc">Designed by: Mustafa Ahmed Shaheed, Ali Saif, and Amir Ghaith Shawqi with assistance from Mustafa Ahmed Khurshid</div>
</div>

<!-- صفحة الحاسبة -->
<div id="calculator">
<input id="input" placeholder="Type operation or use buttons">

<!-- مربع الأزرار الرمزية -->
<div id="buttons-box" class="button-container">
  <button class="calc" onclick="addWord('+')">+</button>
  <button class="calc" onclick="addWord('-')">-</button>
  <button class="calc" onclick="addWord('*')">×</button>
  <button class="calc" onclick="addWord('/')">÷</button>
  <button class="calc" onclick="addWord('**')">^</button>
  <button class="calc" onclick="addWord('/100')">%</button>
  <button class="calc" onclick="clearInput()">C</button>
</div>

<!-- مربع القائمة الفيزيائية -->
<div id="physics-box">
  <button class="calc" onclick="togglePhysics()">Physics Formulas ⬇️</button>
  <div id="physics-list">
    <button class="calc" onclick="showPopup('Force')">Force</button>
    <button class="calc" onclick="showPopup('Pressure')">Pressure</button>
    <button class="calc" onclick="showPopup('Energy')">Energy</button>
    <button class="calc" onclick="showPopup('Kinetic')">Kinetic Energy</button>
    <button class="calc" onclick="showPopup('Gravity')">Gravity</button>
    <button class="calc" onclick="showPopup('Ohm')">Ohm</button>
    <button class="calc" onclick="showPopup('Work')">Work</button>
    <button class="calc" onclick="showPopup('Power')">Power</button>
    <button class="calc" onclick="showPopup('Density')">Density</button>
    <button class="calc" onclick="showPopup('Momentum')">Momentum</button>
    <button class="calc" onclick="showPopup('Acceleration')">Acceleration</button>
    <button class="calc" onclick="showPopup('Velocity')">Velocity</button>
    <button class="calc" onclick="showPopup('Frequency')">Frequency</button>
  </div>
</div>

<!-- زر الحساب -->
<button class="calc" onclick="calculate()">Confirm</button>

<!-- الناتج والشرح -->
<div id="result-box">
  <div id="result">Result</div>
  <div id="explain">Explanation</div>
</div>

<!-- مربع القوانين العائم -->
<div id="overlay">
  <div class="popup">
    <div id="popup-title"></div>
    <input id="val1" placeholder="">
    <input id="val2" placeholder="">
    <button onclick="applyFormula()">Apply</button>
  </div>
</div>

<script>
function togglePhysics(){ document.getElementById("physics-list").classList.toggle("open"); }
function addWord(w){ document.getElementById("input").value += " "+w+" "; }
function clearInput(){ 
  document.getElementById("input").value=""; 
  document.getElementById("result").innerText="Result"; 
  document.getElementById("explain").innerText="Explanation"; 
}
function startCalculator(){
  document.getElementById("welcome").style.display="none";
  document.getElementById("calculator").style.display="block";
}

/* المربع العائم */
let currentFormula = '';
function showPopup(formula){
  currentFormula = formula;
  document.getElementById("popup-title").innerText = formula;
  document.getElementById("val1").value = '';
  document.getElementById("val2").value = '';
  
  switch(formula){
    case 'Force':
      document.getElementById("val1").placeholder = "Mass (m)";
      document.getElementById("val2").placeholder = "Acceleration (a)";
      break;
    case 'Pressure':
      document.getElementById("val1").placeholder = "Force (F)";
      document.getElementById("val2").placeholder = "Area (A)";
      break;
    case 'Energy':
      document.getElementById("val1").placeholder = "Mass (m)";
      document.getElementById("val2").placeholder = "Speed of light (c)";
      break;
    case 'Kinetic':
      document.getElementById("val1").placeholder = "Mass (m)";
      document.getElementById("val2").placeholder = "Velocity (v)";
      break;
    case 'Gravity':
      document.getElementById("val1").placeholder = "Mass1 (m1)";
      document.getElementById("val2").placeholder = "Mass2 (m2)";
      break;
    case 'Ohm':
      document.getElementById("val1").placeholder = "Current (I)";
      document.getElementById("val2").placeholder = "Resistance (R)";
      break;
    case 'Work':
      document.getElementById("val1").placeholder = "Force (F)";
      document.getElementById("val2").placeholder = "Distance (d)";
      break;
    case 'Power':
      document.getElementById("val1").placeholder = "Work (W)";
      document.getElementById("val2").placeholder = "Time (t)";
      break;
    case 'Density':
      document.getElementById("val1").placeholder = "Mass (m)";
      document.getElementById("val2").placeholder = "Volume (V)";
      break;
    case 'Momentum':
      document.getElementById("val1").placeholder = "Mass (m)";
      document.getElementById("val2").placeholder = "Velocity (v)";
      break;
    case 'Acceleration':
      document.getElementById("val1").placeholder = "Change in Velocity (Δv)";
      document.getElementById("val2").placeholder = "Time (t)";
      break;
    case 'Velocity':
      document.getElementById("val1").placeholder = "Distance (d)";
      document.getElementById("val2").placeholder = "Time (t)";
      break;
    case 'Frequency':
      document.getElementById("val1").placeholder = "1";
      document.getElementById("val2").placeholder = "Period (T)";
      break;
  }
  document.getElementById("overlay").style.display='flex';
}

function applyFormula(){
  let val1 = document.getElementById("val1").value;
  let val2 = document.getElementById("val2").value;
  let inputStr = '';
  switch(currentFormula){
    case 'Force': inputStr = val1+'*'+val2; break;             // F = m * a
    case 'Pressure': inputStr = val1+'/'+val2; break;          // P = F / A
    case 'Energy': inputStr = val1+'*'+val2+'**2'; break;     // E = m * c^2
    case 'Kinetic': inputStr = '0.5*'+val1+'*'+val2+'**2'; break; // KE = 0.5 * m * v^2
    case 'Gravity': inputStr = val1+'*'+val2+'/r**2'; break;  // F = G * m1 * m2 / r^2
    case 'Ohm': inputStr = val1+'/'+val2; break;              // V = I / R
    case 'Work': inputStr = val1+'*'+val2; break;             // W = F * d
    case 'Power': inputStr = val1+'/'+val2; break;            // P = W / t
    case 'Density': inputStr = val1+'/'+val2; break;          // ρ = m / V
    case 'Momentum': inputStr = val1+'*'+val2; break;         // p = m * v
    case 'Acceleration': inputStr = val1+'/'+val2; break;     // a = Δv / t
    case 'Velocity': inputStr = val1+'/'+val2; break;         // v = d / t
    case 'Frequency': inputStr = val1+'/'+val2; break;        // f = 1 / T
  }
  document.getElementById("input").value = inputStr;
  document.getElementById("overlay").style.display='none';
}

/* الحساب */
function interpretInput(inputVal){
  return inputVal.toLowerCase()
    .replace(/plus/g,'+')
    .replace(/minus/g,'-')
    .replace(/multiply/g,'*')
    .replace(/divide/g,'/')
    .replace(/percent/g,'/100')
    .replace(/power/g,'**');
}
function calculate(){
  try{
    let p=interpretInput(document.getElementById("input").value);
    let resultVal = new Decimal(eval(p));
    document.getElementById("result").innerText = resultVal.toString();
    document.getElementById("explain").innerText = document.getElementById("input").value + " = " + resultVal.toString();
  }catch{
    document.getElementById("result").innerText = "Error";
    document.getElementById("explain").innerText = "Check your input";
  }
}
</script>
</body>
</html>
