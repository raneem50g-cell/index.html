# index.html
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

.container{
  padding:10px;
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
}
footer{
  text-align:center;
  padding:10px;
  background:#2e7d32;
  color:white;
}
</style>
</head>

<body>

<header>🌙 نور القرآن الكريم</header>

<div id="app" class="container"></div>

<footer>✨ رنيم العنزي</footer>

<script>
async function loadQuran(){
  let res = await fetch("https://api.alquran.cloud/v1/quran/ar.alafasy");
  let data = await res.json();

  let surahs = data.data.surahs;
  let app = document.getElementById("app");

  surahs.forEach(surah=>{
    let div = document.createElement("div");
    div.className = "surah";

    let ayahsHTML = surah.ayahs.map(a =>
      a.numberInSurah + ". " + a.text + "<br>"
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

loadQuran();
</script>

</body>
</html>
