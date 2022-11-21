<html>
<body>

<h2>Scale Writer</h2>
<select id="rootSelect">
  <option value="2,7,12,17,22,27,32,37,42">C♯</option>
  <option value="17,22,27,31,37,42,47,52,57">F♯</option>
  <option value="31,37,42,46,52,57,62,66,72">B</option>
  <option value="11,17,22,26,31,37,42,46,52">E</option>
  <option value="26,31,37,41,46,52,57,61,66">A</option>
  <option value="6,11,17,21,26,31,37,41,46">D</option>
  <option value="21,26,31,36,41,46,52,56,61">G</option>
  <option value="1,6,11,16,21,26,31,36,41" selected>C</option>
  <option value="16,21,26,30,36,41,46,51,56">F</option>
  <option value="30,36,41,45,51,56,61,65,71">B♭</option>
  <option value="10,16,21,25,30,36,41,45,51">E♭</option>
  <option value="25,30,36,40,45,51,56,60,65">A♭</option>
  <option value="5,10,16,20,25,30,36,40,45">D♭</option>
  <option value="20,25,30,35,40,45,51,55,60">G♭</option>
  <option value="0,5,10,15,20,25,30,35,40">C♭</option>  
  </select>
  <select id="chordSelect">
    <option value="0,0,0,0,0,0,0,0,0">maj7 | Major</option>
    <option value="0,0,0,0,0,0,1,0,0">7 | Mixolydian</option>
    <option value="0,0,1,0,0,0,1,0,0">-7 | Dorian</option>
    <option value="0,1,1,0,1,1,1,0,1">-7♭5 | Locrian</option>
    <option value="0,0,1,0,1,1,2,1,2">°7 | Diminished</option>
    <option value="0,0,0,-1,0,0,0,0,0">maj+4 | Lydian</option>
    <option value="0,0,0,-1,0,0,1,0,0">7+11 | Lydian Dominant</option>
    <option value="0,1,0,0,0,1,1,0,-1">7♭9 | 3rd Mode of Bebop (Major)</option>
  </select>
<button onclick="scaleFunction()">Add Scale</button>
<button onclick="myBarline()">Add Barline</button>
<button onclick="clearFunction()">Clear</button><br>
<div id="scale"></div>
<script>
function clearFunction() {
document.getElementById("scale").innerHTML = "";
}
function myBarline() {
const node = document.createElement("hr");
document.getElementById("scale").append(node);
}
function scaleFunction() {
let a = rootSelect.options[rootSelect.selectedIndex].text;
let b = chordSelect.options[chordSelect.selectedIndex].text;
const noteArray = ["C♭","C","C♯","D","C","D♭","D","D♯","E","D","E♭","E","E♯","F♯","E♭","F♭","F","F♯","G","F","G♭","G","G♯","A","G","A♭","A","A♯","B","A","B♭","B","B♯","C♯","B♭","C♭","C","C♯","D","C","D♭","D","D♯","E","D","E♭","E","E♯","F♯","E♭","F♭","F","F♯","G","F","G♭","G","G♯","A","G","A♭","A","A♯","B","A","B♭","B","B♯","C♯","B♭","C♭","C","C♯","D"
];
var x = document.getElementById("rootSelect").value;
const keyArray = x.split(",");
var y = document.getElementById("chordSelect").value;
const chordArray = y.split(",");
let scale = "<b>" + a + b + "</b>"+ "<br>";
for (let i = 0; i <= 8; i++) {
    scale += noteArray[keyArray[i]-chordArray[i]] + " ";
}
const div = document.getElementById("scale");
div.insertAdjacentHTML('beforeend', scale + "<br>");
}
</script>

</body>
</html>