<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>FLAMES Game</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f4;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
        }
        .container {
            text-align: center;
            background: white;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
        }
        input {
            padding: 10px;
            margin: 10px;
            width: 200px;
            border: 1px solid #ccc;
            border-radius: 4px;
        }
        button {
            padding: 10px 15px;
            background-color: #28a745;
            color: white;
            border: none;
            border-radius: 4px;
            cursor: pointer;
        }
        button:hover {
            background-color: #218838;
        }
        #result {
            margin-top: 20px;
            font-size: 1.5em;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>FLAMES Game</h1>
        <input type="text" id="yourName" placeholder="Enter your name" required>
        <input type="text" id="friendName" placeholder="Enter friend's name" required>
        <button id="calculateButton">Calculate Relationship</button>
        <div id="result"></div>
    </div>
    <script>
        document.getElementById("calculateButton").addEventListener("click", function() {
            const yourName = document.getElementById("yourName").value.toLowerCase();
            const friendName = document.getElementById("friendName").value.toLowerCase();
            const flames = ["F", "L", "A", "M", "E", "S"];

            // Convert names to arrays
            let listYourName = yourName.split('');
            let listFriendName = friendName.split('');

            // Remove common letters
            listYourName.forEach(letter => {
                const index = listFriendName.indexOf(letter);
                if (index !== -1) {
                    listFriendName.splice(index, 1);
                    listYourName.splice(listYourName.indexOf(letter), 1);
                }
            });

            // Count remaining letters
            const count = listYourName.length + listFriendName.length;

            // FLAMES logic
            let index = 0;
            while (flames.length > 1) {
                index = (index + count - 1) % flames.length;
                flames.splice(index, 1);
            }

            // Determine relationship
            const relationshipMap = {
                "F": "Friends",
                "L": "Lovers",
                "A": "Admirers",
                "M": "Marriage",
                "E": "Enemies",
                "S": "Secret Lovers"
            };

            const result = relationshipMap[flames[0]];
            document.getElementById("result").innerText = `The relationship is: ${result}`;
        });
    </script>
</body>
</html>