# index.html
# Quran-app
Public
<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<title>نور القرآن</title>

<style>
body{
  font-family: Arial;
  margin:0;
  background:#f4f4f4;
}

header{
  background:#2e7d32;
  color:white;
  text-align:center;
  padding:20px;
  font-size:24px;
}

input{
  width:90%;
  padding:10px;
  margin:10px auto;
  display:block;
  border-radius:8px;
  border:1px solid.   #ccc;
}

.container{
  padding:10px;
  padding-bottom:60px;
}

.surah{
  background:white;
  margin:10px 0;
  padding:15px;
  border-radius:10px;
  cursor:pointer;
}

.ayahs{
  display:none;
  margin-top:10px;
  line-height:1.8;
  color:#333;
}

footer{
  position:fixed;
  bottom:0;
  width:100%;
  background:#2e7d32;
  color:white;
  text-align:center;
  padding:10px;
  font-size:16px;
}
</style>
</head>

<body>

<header>🌙 نور القرآن الكريم</header>

<input type="text" id="search" placeholder="ابحث عن السورة...">

<div id="app" class="container"></div>

<footer>✨ رنيم العنزي</footer>

<script>
let allSurahs = [];

async function loadQuran(){
  let res = await fetch("https://api.alquran.cloud/v1/quran/ar.alafasy");
  let data = await res.json();

  allSurahs = data.data.surahs;
  displaySurahs(allSurahs);
}

function displaySurahs(surahs){
  let app = document.getElementById("app");
  app.innerHTML = "";

  surahs.forEach(surah=>{
    let div = document.createElement("div");
    div.className = "surah";

    let ayahsHTML = surah.ayahs.map(a => 
      `${a.numberInSurah}. ${a.text}<br>`
    ).join("");

    div.innerHTML = `
      <h3>${surah.name}</h3>
      <div class="ayahs">${ayahsHTML}</div>
    `;

    div.onclick = () => {
      let a = div.querySelector(".ayahs");
      a.style.display = a.style.display === "block" ? "none" : "block";
    };

    app.appendChild(div);
  });
}

document.getElementById("search").oninput = function(){
  let value = this.value.trim();
  let filtered = allSurahs.filter(s => 
    s.name.includes(value)
  );
  displaySurahs(filtered);
};

loadQuran();
</ :script>

</body>
</html>.  
