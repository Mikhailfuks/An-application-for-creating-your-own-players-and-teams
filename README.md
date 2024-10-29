<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Player and Team Manager</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <div class="container">
        <h1>Player and Team Manager</h1>

        <div class="form-section">
            <h2>Add Player</h2>
            <input type="text" id="playerName" placeholder="Player Name">
            <input type="text" id="playerPosition" placeholder="Player Position">
            <button id="addPlayer">Add Player</button>
        </div>

        <div class="form-section">
            <h2>Create Team</h2>
            <input type="text" id="teamName" placeholder="Team Name">
            <button id="createTeam">Create Team</button>
        </div>

        <div class="form-section">
            <h2>Assign Player to Team</h2>
            <input type="text" id="assignPlayerName" placeholder="Player Name">
            <input type="text" id="assignTeamName" placeholder="Team Name">
            <button id="assignPlayer">Assign Player</button>
        </div>

        <h2>Players</h2>
        <ul id="playerList"></ul>

        <h2>Teams</h2>
        <ul id="teamList"></ul>
    </div>

    <script src="app.js"></script>
</body>
</html>


/* styles.css */
body {
    font-family: Arial, sans-serif;
    background-color: #f4f4f4;
    margin: 0;
    padding: 20px;
}

.container {
    max-width: 600px;
    margin: 0 auto;
    background: white;
    padding: 20px;
    border-radius: 8px;
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
}

h1, h2 {
    color: #333;
}

.form-section {
    margin-bottom: 20px;
}

input {
    width: calc(100% - 22px);
    padding: 10px;
    margin-bottom: 10px;
    border: 1px solid #ccc;
    border-radius: 4px;
}

button {
    width: 100%;
    padding: 10px;
    background-color: #007bff;
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
}

button:hover {
    background-color: #0056b3;
}

ul {
    list-style-type: none;
    padding: 0;
}

li {
    padding: 10px;
    background: #f8f8f8;
    margin-bottom: 5px;
    border-radius: 4px;
}

// app.js
document.addEventListener('DOMContentLoaded', () => {
    const addPlayerButton = document.getElementById('addPlayer');
    const createTeamButton = document.getElementById('createTeam');
    const assignPlayerButton = document.getElementById('assignPlayer');
    const playerList = document.getElementById('playerList');
    const teamList = document.getElementById('teamList');

    let players = [];
    let teams = {};

    // Добавление игрока
    addPlayerButton.addEventListener('click', () => {



        const playerName = document.getElementById('playerName').value;
        const playerPosition = document.getElementById('playerPosition').value;

        if (playerName && playerPosition) {
            const player = { name: playerName, position: playerPosition };
            players.push(player);
            updatePlayerList();
            document.getElementById('playerName').value = '';
            document.getElementById('playerPosition').value = '';
        } else {
            alert('Please fill in both fields.');
        }
    });

    // Создание команды
    createTeamButton.addEventListener('click', () => {
        const teamName = document.getElementById('teamName').value;

        if (teamName) {
            teams[teamName] = [];
            updateTeamList();
            document.getElementById('teamName').value = '';
        } else {
            alert('Please enter a team name.');
        }
    });

    // Назначение игрока команде
    assignPlayerButton.addEventListener('click', () => {
        const assignPlayerName = document.getElementById('assignPlayerName').value;
        const assignTeamName = document.getElementById('assignTeamName').value;

        const playerExists = players.some(player => player.name === assignPlayerName);
        const teamExists = teams.hasOwnProperty(assignTeamName);

        if (playerExists && teamExists) {
            teams[assignTeamName].push(assignPlayerName);
            updateTeamList();
            document.getElementById('assignPlayerName').value = '';
            document.getElementById('assignTeamName').value = '';
        } else {
            alert('Player or Team does not exist.');
        }
    });

    // Обновление списка игроков
    function updatePlayerList() {
        playerList.innerHTML = '';
        players.forEach(player => {
            const li = document.createElement('li');
            li.textContent = `${player.name} (${player.position})`;
            playerList.appendChild(li);
        });
    }

    // Обновление списка команд
    function updateTeamList() {
        teamList.innerHTML = '';
        for (const team in teams) {
            const li = document.createElement('li');
            li.textContent = `${team}: ${teams[team].join(', ')}`;
            teamList.appendChild(li);
        }
    }
});
