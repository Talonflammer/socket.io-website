<!DOCTYPE html>
<html>
<head>
    <title>Multiplayer Trade App</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/socket.io/4.5.4/socket.io.min.js"></script>
</head>
<body>
    <h1>Multiplayer Trade App</h1>
    <input id="username" placeholder="Enter your name">
    <button onclick="join()">Join</button>
    <hr>

    <h2>Trade Items</h2>
    <select id="item">
        <option>Sword</option>
        <option>Shield</option>
        <option>Potion</option>
        <option>Gem</option>
    </select>
    <input id="receiver" placeholder="Receiver Name">
    <button onclick="trade()">Trade</button>

    <h3>Updates:</h3>
    <ul id="updates"></ul>

    <script>
        var socket = io();
        function join() {
            var username = document.getElementById('username').value;
            socket.emit('join', {username: username});
        }

        function trade() {
            var sender = document.getElementById('username').value;
            var receiver = document.getElementById('receiver').value;
            var item = document.getElementById('item').value;
            socket.emit('trade', {sender: sender, receiver: receiver, item: item});
        }

        socket.on('user_joined', function(username){
            var li = document.createElement('li');
            li.innerText = username + " joined the app";
            document.getElementById('updates').appendChild(li);
        });

        socket.on('trade_update', function(message){
            var li = document.createElement('li');
            li.innerText = message;
            document.getElementById('updates').appendChild(li);
        });
    </script>
</body>
</html>


if __name__ == '__main__':
    socketio.run(app, debug=True)


