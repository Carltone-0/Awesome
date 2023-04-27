# Awesome
 A simple web application that allows users to create, view, and delete notes.
<!DOCTYPE html>
<html>
<head>
    <title>Awesome App</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <h1>Awesome App</h1>
    <form>
        <label for="note-title">Title:</label>
        <input type="text" id="note-title" name="note-title">
        <br>
        <label for="note-message">Message:</label>
        <textarea id="note-message" name="note-message"></textarea>
        <br>
        <button type="button" onclick="createNote()">Create Note</button>
    </form>
    <ul id="note-list"></ul>
    <script src="script.js"></script>
</body>
</html>


body {
    font-family: Arial, sans-serif;
}

form {
    border: 1px solid #ccc;
    padding: 10px;
    margin-bottom: 20px;
}

form label {
    display: block;
    margin-bottom: 5px;
}

form input, form textarea {
    width: 100%;
    padding: 5px;
    margin-bottom: 10px;
    border: 1px solid #ccc;
}

form button {
    padding: 5px 10px;
    background-color: #4CAF50;
    color: #fff;
    border: none;
    cursor: pointer;
}

ul {
    list-style-type: none;
    margin: 0;
    padding: 0;
}

li {
    border: 1px solid #ccc;
    padding: 10px;
    margin-bottom: 10px;
}

li h2 {
    margin-top: 0;
}

li p {
    margin: 0;
}

let notes = [];

function createNote() {
    const title = document.getElementById('note-title').value;
    const message = document.getElementById('note-message').value;
    notes.push({ title, message });
    updateNoteList();
    clearNoteForm();
}

function updateNoteList() {
    const noteList = document.getElementById('note-list');
    noteList.innerHTML = '';
    for (let i = 0; i < notes.length; i++) {
        const note = notes[i];
        const li = document.createElement('li');
        const h2 = document.createElement('h2');
        const p = document.createElement('p');
        const deleteButton = document.createElement('button');
        deleteButton.innerText = 'Delete';
        deleteButton.onclick = function() {
            notes.splice(i, 1);
            updateNoteList();
        }
        h2.innerText = note.title;
        p.innerText = note.message.substring(0, 20) + '...';
        li.appendChild(h2);
        li.appendChild(p);
        li.appendChild(deleteButton);
        noteList.appendChild(li);
    }
}

function clearNoteForm() {
    document.getElementById('note-title').value = '';
    document.getElementById('note-message').value = '';
}



