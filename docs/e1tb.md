<head>
  <style>
    img {
      height: auto;
      width: 100%;
      display: inline-block;
      margin-bottom: 0.5rem;
    }
    select {
      color: white;
      background-color: gray;
      font-family: arial;
      font-size: 2rem;
      border-radius: 0.5rem;
      height: 4.5rem;
      text-align: center;
      margin: 0.1rem;
    }
    #top {
      margin-bottom: 0.5rem;
      font-family: arial;
      font-size: 3rem;
      color: #75ab9a;
    }
    #exercises {
      display:flex;
      align-items: center;
      font-family: arial;
      font-size: 3rem;
    }
    #numberSelect {
      display: flex;
      flex-wrap: wrap;
      align-content: space-between;
    }
    .numberButton {
      font-family:Arial, Helvetica, sans-serif;
      font-size: 2rem;
      border-radius: 0.5rem;
      background-color: #75ab9a;
      color: white;
      padding: 1rem;
      margin: 0.1rem;
      text-decoration: none;
    }
    .numberButton:hover {
      text-decoration:none;
    }
    #transport {
      display: flex;
      align-items:center;
      flex-wrap: wrap;
    }
    #audioControl {
      display: flex;
      flex-wrap: wrap;
      align-items:center;
      margin-right:3rem;
    }
    #nav {
      display: flex;
    }
    .navButton {
      cursor: pointer;
      font-size: 2rem;
      border-radius: 0.5rem;
      background-color: #75ab9a;
      color: white;
      padding: 1rem;
      margin: 0.1rem;
      text-decoration: none;
    }
    .navButton:hover {
      text-decoration:none;
    }
    #pad {
      height: 1440px;
    }
  </style>
</head>
<body onload="selectFunction()" style="background-color:white">
  <div id="top" style="font-family:Arial, Helvetica, sans-serif">ESSENTIAL ELEMENTS FOR BAND:<br>TROMBONE BOOK 1</div>
    <div id="exercises">
    <select id="exerciseSelect" onchange="selectFunction()">
    <option>1-13</option>
    <option>14-26</option>
    <option>27-39</option>
    <option>40-51</option>
    <option>52-58</option>
    <option>59-72</option>
    <option>73-85</option>
    <option>86-99</option>
    <option>100-109</option>
    <option>110-118</option>
    <option>119-131</option>
    <option>132-146</option>
    <option>147-153</option>
    <option>154-164</option>
    <option>165-174</option>
    <option>175-181</option>
    <option>182-184</option>
    <option>185-187</option>
  </select>
    <span class="navButton" onclick="pagePrevious(); selectFunction();">⬅️</span>
    <span class="navButton" onclick="pageNext(); selectFunction();">➡️</span>
    <span class="navButton" id="fs" onclick="fullScreen();">⛶</span>
    </div>
      <br>
  <div id="numberSelect"></div>
  <div id="music"></div>
  <hr style="height:1rem;
  border-radius:0.5rem;
  background-color:#75ab9a;
  border-style:none;">
  <div id="pad"></div>

  <script>
    //FULLSCREEN//
    var elem = document.documentElement;  
    function fullScreen () {
    if (!document.fullscreenElement) {
      if (elem.requestFullscreen) {
      elem.requestFullscreen();
      } else if (elem.webkitRequestFullscreen) { /* Safari */
      elem.webkitRequestFullscreen();
      } else if (elem.msRequestFullscreen) { /* IE11 */
      elem.msRequestFullscreen();
      }
      return;
      }
      if (document.exitFullscreen) {
      document.exitFullscreen();
      } else if (document.webkitExitFullscreen) { /* Safari */
      document.webkitExitFullscreen();
      } else if (document.msExitFullscreen) { /* IE11 */
      document.msExitFullscreen();
      }
      }
    //BUTTONS//
    function pagePrevious() {
      var x = 
      document.getElementById("exerciseSelect").selectedIndex;
      if (x > 0) {
        document.getElementById("exerciseSelect").selectedIndex = x - 1;
      }
      }
    function pageNext() {
      var x = 
      document.getElementById("exerciseSelect").selectedIndex;
      var s = 
      document.getElementById("exerciseSelect").length;
      if (x < s - 1) {
        document.getElementById("exerciseSelect").selectedIndex = x + 1;
      }
      }
    //PLAY//
    function audioPlay(id) {
      var z = document.getElementById(id);
      if (z.paused || z.ended) {
        z.play();
        document.getElementById("transport" + id).innerHTML = "⏸️";
      } else {
        z.pause();
        document.getElementById("transport" + id).innerHTML = "▶️";
      }
      }
    //RESTART//
    function audioRestart(id) {
      var y = document.getElementById(id);   
      y.currentTime=0;
      y.pause();
      document.getElementById("transport" + id).innerHTML = "▶️";
      }
    //PLAYBACKRATE//
    //Needed '' in function call to read as id//
    function audioRate(l,m) {
      var r = document.getElementById(l);
      var v = document.getElementById(m).value;
      r.playbackRate = v;
    }
    //LOOP//
    const aud_dir = "https://e1-assets.s3.us-west-1.amazonaws.com/";
    const aud_name = "E1TB"
    const aud_path = `${aud_dir}${aud_name}`;
    const img_dir = "https://www.essentialelementsinteractive.com/EESONGS/Graphics/"
    const img_name = "B1Tbn";
    const img_path = `${img_dir}${img_name}`;

    function selectFunction() {
     let text1 = "";
     let text2 = "";
     var x = document.getElementById("exerciseSelect").value;
     const myArray = x.split("-");
     var i = myArray[0];
     var num = myArray[1];
     for (; i <= num; i++) 
        {
         if (i < 10) {
         zero = "00";
        } else if (i < 100) {
         zero = "0";
        } else {
         zero = "";
        }
        //LOOP ELEMENTS//
        var img = "<img id=exercise" + i + " src=" + img_path + zero + i + ".jpg>";
        var play = "<span class=navButton id=transport" + i + " onclick=audioPlay(" + i + ")>▶️</span>"
        var aud = "<audio id=" + i + " preload='none'><source src=" +  aud_path + i + ".mp3></audio><span class=navButton onclick=audioRestart(" + i + ")>🔃</span>";
        var rate = "<select id=pbr" + i + " onchange=audioRate(" + i + ",'pbr" + i + "')><option value='0.5' >x0.5</option><option value='0.75'>x0.75</option><option value='1' selected>x1</option></select>";
        var top = "<a class=navButton onclick=audioRestart(" + i + ") href=#top>🔝</a>";
        var exP = "<a class=navButton onclick=audioRestart(" + i + ") href=#line" + (i - 1) + ">⬅️</a>";
        var exN = "<a class=navButton onclick=audioRestart(" + i + ") href=#line" + (i - -1) + ">➡️</a>";
        var line = "<hr id=line" + i + " style=height:1rem;border-radius:0.5rem;background-color:#75ab9a;border-style:none;>"
        text1 += line + "<div id=transport><div id=audioControl>" + play + aud + rate + "</div><div id=nav>" + top + exP + exN + "</div></div>" + img;
        text2 += "<a class=numberButton href=#line" + i + "> " + i + "</a>"
      }
       document.getElementById("music").innerHTML = text1;
       document.getElementById("numberSelect").innerHTML = text2;
     }
  </script>
  </body>