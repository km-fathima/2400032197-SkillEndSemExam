# 2400032197-SkillEndSemExam
<!DOCTYPE html>
<html>
<head>
    <title>Student Notes App</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 30px;
        }
        #noteInput {
            width: 300px;
            height: 80px;
            padding: 10px;
        }
        button {
            padding: 8px 12px;
            margin-top: 10px;
        }
        .note {
            background: #f4f4f4;
            margin: 10px 0;
            padding: 10px;
            border-radius: 5px;
        }
        .actions button {
            margin-right: 10px;
        }
    </style>
</head>

<body>

<h2>Student Notes App (CRUD)</h2>

<textarea id="noteInput" placeholder="Enter your note..."></textarea><br>
<button onclick="addNote()">Add Note</button>

<h3>Saved Notes:</h3>
<div id="notesList"></div>

<script>
    // Load notes from localStorage
    function loadNotes() {
        let notes = JSON.parse(localStorage.getItem("notes")) || [];
        let notesList = document.getElementById("notesList");
        notesList.innerHTML = "";

        notes.forEach((note, index) => {
            let div = document.createElement("div");
            div.className = "note";
            div.innerHTML = `
                <p>${note}</p>
                <div class="actions">
                    <button onclick="editNote(${index})">Edit</button>
                    <button onclick="deleteNote(${index})">Delete</button>
                </div>
            `;
            notesList.appendChild(div);
        });
    }

    // Add a new note
    function addNote() {
        let noteText = document.getElementById("noteInput").value;
        if (noteText.trim() === "") return alert("Enter a note!");

        let notes = JSON.parse(localStorage.getItem("notes")) || [];
        notes.push(noteText);
        localStorage.setItem("notes", JSON.stringify(notes));

        document.getElementById("noteInput").value = "";
        loadNotes();
    }

    // Edit existing note
    function editNote(index) {
        let notes = JSON.parse(localStorage.getItem("notes"));
        let updatedText = prompt("Update your note:", notes[index]);

        if (updatedText !== null) {
            notes[index] = updatedText;
            localStorage.setItem("notes", JSON.stringify(notes));
            loadNotes();
        }
    }

    // Delete note
    function deleteNote(index) {
        let notes = JSON.parse(localStorage.getItem("notes"));
        notes.splice(index, 1);
        localStorage.setItem("notes", JSON.stringify(notes));
        loadNotes();
    }

    loadNotes(); // Load notes on startup
</script>

</body>
</html>
