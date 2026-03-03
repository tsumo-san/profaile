<!DOCTYPE html>
<html lang="ja">
<head>
<meta charset="UTF-8">
<title>超簡単ターン制RPG</title>
<style>
body{
    background:black;
    color:white;
    font-family:sans-serif;
    text-align:center;
    padding-top:50px;
}
button{
    padding:10px 20px;
    margin:10px;
    font-size:16px;
    cursor:pointer;
}
.box{
    border:2px solid white;
    padding:20px;
    width:300px;
    margin:20px auto;
}
</style>
</head>
<body>

<h1>⚔ ターン制RPG ⚔</h1>

<div class="box">
    <p>🧑 プレイヤー HP: <span id="playerHP">100</span></p>
    <p>👾 モンスター HP: <span id="enemyHP">100</span></p>
</div>

<button onclick="attack()">攻撃</button>
<button onclick="heal()">回復</button>

<p id="log"></p>

<script>
let playerHP = 100;
let enemyHP = 100;

function update() {
    document.getElementById("playerHP").textContent = playerHP;
    document.getElementById("enemyHP").textContent = enemyHP;
}

function enemyTurn(){
    if(enemyHP <= 0) return;

    let damage = Math.floor(Math.random()*15)+5;
    playerHP -= damage;
    document.getElementById("log").textContent = 
        "モンスターの攻撃！ " + damage + " ダメージ！";

    if(playerHP <= 0){
        alert("ゲームオーバー...");
        location.reload();
    }
    update();
}

function attack(){
    let damage = Math.floor(Math.random()*20)+10;
    enemyHP -= damage;
    document.getElementById("log").textContent = 
        "あなたの攻撃！ " + damage + " ダメージ！";

    if(enemyHP <= 0){
        alert("勝利！！！");
        location.reload();
    }
    update();
    setTimeout(enemyTurn,1000);
}

function heal(){
    let healAmount = Math.floor(Math.random()*15)+10;
    playerHP += healAmount;
    if(playerHP > 100) playerHP = 100;

    document.getElementById("log").textContent = 
        "回復した！ +" + healAmount;

    update();
    setTimeout(enemyTurn,1000);
}
</script>

</body>
</html>
