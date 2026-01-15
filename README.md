<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>RPG Code Breaker PRO</title>
    <style>
        body { background: #0a0a0c; color: #eee; font-family: 'Segoe UI', sans-serif; margin: 0; padding: 10px; display: flex; flex-direction: column; align-items: center; }
        .header { width: 100%; display: flex; justify-content: space-between; background: #1a1a1f; padding: 10px; border-radius: 10px; border: 1px solid #333; box-sizing: border-box; color: #00ff00; font-weight: bold; }
        .hero-card { width: 100%; max-width: 350px; margin-top: 15px; background: #16161a; border-radius: 15px; border: 2px solid #444; overflow: hidden; }
        .hero-img { width: 100%; height: 200px; object-fit: cover; background: #222; }
        .game-log { width: 100%; max-width: 350px; height: 120px; background: rgba(0,0,0,0.5); margin: 15px 0; padding: 10px; border-radius: 8px; font-size: 15px; overflow-y: auto; border-left: 3px solid #6200ee; box-sizing: border-box; }
        .controls { width: 100%; max-width: 350px; display: grid; grid-template-columns: 1fr 1fr; gap: 10px; }
        button { padding: 15px; border: none; border-radius: 8px; font-size: 14px; font-weight: bold; cursor: pointer; color: white; transition: 0.2s; }
        .btn-act { background: #6200ee; }
        .btn-shop { background: #03dac6; color: #000; }
        .btn-donate { background: #cf6679; grid-column: span 2; margin-top: 5px; animation: pulse 2s infinite; }
        @keyframes pulse { 0% {opacity: 1} 50% {opacity: 0.7} 100% {opacity: 1} }
    </style>
</head>
<body>

<div class="header">
    <span>❤️ <span id="hp">100</span></span>
    <span>💰 <span id="gold">0</span></span>
    <span>⭐ <span id="lvl">1</span></span>
</div>

<div class="hero-card">
    <img id="char-img" class="hero-img" src="https://img.freepik.com/free-photo/view-mysterious-hacker-working-laptop_23-2149155333.jpg" alt="Герой">
    <div style="padding: 10px; text-align: center;">
        <b id="char-name">Начинающий Хакер</b>
    </div>
</div>

<div class="game-log" id="log">Система инициализирована... Готов к взлому?</div>

<div class="controls">
    <button class="btn-act" onclick="action('hack')">ВЗЛОМАТЬ</button>
    <button class="btn-act" onclick="action('explore')">РАЗВЕДКА</button>
    <button class="btn-shop" onclick="action('rest')">ОТДЫХ (-5💰)</button>
    <button class="btn-shop" onclick="action('upgrade')">АПГРЕЙД (-20💰)</button>
    <button class="btn-donate" onclick="donate()">💎 КУПИТЬ VIP И БАЙТЫ (ДОНАТ)</button>
</div>

<script>
    let stats = { hp: 100, gold: 0, lvl: 1, name: "Начинающий Хакер" };

    function updateUI() {
        document.getElementById('hp').innerText = stats.hp;
        document.getElementById('gold').innerText = stats.gold;
        document.getElementById('lvl').innerText = stats.lvl;
        document.getElementById('char-name').innerText = stats.name;
        if(stats.hp <= 0) {
            alert("Критическая ошибка! Система перезагружается...");
            location.reload();
        }
    }

    function logMsg(msg) {
        const log = document.getElementById('log');
        log.innerHTML = msg + "<br>" + log.innerHTML;
    }

    function action(type) {
        if(type === 'hack') {
            if(Math.random() > 0.3) {
                let win = Math.floor(Math.random() * 10) + 5;
                stats.gold += win;
                logMsg("✅ Взлом успешен! +"+win+" байт.");
            } else {
                stats.hp -= 15;
                logMsg("❌ Обнаружен! Защита нанесла -15 урона.");
            }
        } 
        else if(type === 'explore') {
            logMsg("🔍 Ты нашел старую флешку с данными. +2 байта.");
            stats.gold += 2;
        }
        else if(type === 'rest') {
            if(stats.gold >= 5) {
                stats.gold -= 5;
                stats.hp = Math.min(100, stats.hp + 30);
                logMsg("🛠️ Система восстановлена. +30 HP.");
            } else logMsg("⚠️ Недостаточно байт для ремонта!");
        }
        else if(type === 'upgrade') {
            if(stats.gold >= 20) {
                stats.gold -= 20;
                stats.lvl++;
                stats.name = "Продвинутый Взломщик";
                document.getElementById('char-img').src = "https://img.freepik.com/free-photo/hacker-with-laptop-cyber-terrorist-dark-room_155003-11883.jpg";
                logMsg("🆙 Уровень повышен! Ты стал сильнее.");
            } else logMsg("⚠️ Нужно 20 байт для апгрейда!");
        }
        updateUI();
    }

    function donate() {
        // Эта команда будет работать только если бот настроен на прием платежей
        alert("Перенаправляем в магазин бота...");
        window.location.href = "https://t.me/ТВОЙ_БОТ_USERNAME?start=shop"; 
    }

    updateUI();
</script>
</body>
</html>
