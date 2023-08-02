<!DOCTYPE html>
<html lang="en">

<head>
    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css" integrity="sha384-ggOyR0iXCbMQv3Xipma34MD+dH/1fQ784/j6cY/iJTQUOhcWr7x9JvoRxT2MZw1T" crossorigin="anonymous">

    <script src="https://code.jquery.com/jquery-3.3.1.slim.min.js" integrity="sha384-q8i/X+965DzO0rT7abK41JStQIAqVgRVzpbzo5smXKp4YfRvH+8abtTE1Pi6jizo" crossorigin="anonymous">
    </script>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.14.7/umd/popper.min.js" integrity="sha384-UO2eT0CpHqdSJQ6hJty5KVphtPhzWj9WO1clHTMGa3JDZwrnQq4sF86dIHNDz0W1" crossorigin="anonymous">
    </script>

    <script src="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/js/bootstrap.min.js" integrity="sha384-JjSmVgyd0p3pXB1rRibZUAYoIIy6OrQ6VrjIEaFf/nJGzIxFDsf4x0xIM+B07jRM" crossorigin="anonymous">
    </script>
</head>

<body>
    <nav class="navbar navbar-expand-lg 
                navbar-light bg-success">
        <a class="navbar-brand" href="#">
            <p style="font-size: 30px;">
                <font color=>THE NOTES TAKER</font>
            </p>

        </a>
    </nav>

    <div class="container my-3">
        <h1><font color="#FF3396 ">Take your Notes here</font></h1>
        <div class="card">
            <div class="card-body">
                <h5 class="card-title">
                    Add a Note

                </h5>
                <div class="form-group">
                    <textarea class="form-control" id="addTxt" rows="3">
                    </textarea>
                </div>
                <button class="btn btn-primary" id="addBtn" style="background-color:#5233FF ">
                    Add Note
                </button>
            </div>
        </div>
        <hr color=" dark pink">
        <h1>Your Notes</h1>
        <hr color="dark pink">

        <div id="notes" class="row container-fluid">
        </div>
    </div>

    <script src="gfg.js"></script>
</body>

</html>
<script>
    showNotes();
    let addBtn = document.getElementById("addBtn");
    addBtn.addEventListener("click", function(e) {
        let addTxt = document.getElementById("addTxt");
        let notes = localStorage.getItem("notes");
    
        if (notes == null) notesObj = [];
        else notesObj = JSON.parse(notes);
    
        notesObj.push(addTxt.value);
        localStorage.setItem("notes", JSON.stringify(notesObj));
        addTxt.value = "";
    
        showNotes();
    });
    function showNotes() {
        let notes = localStorage.getItem("notes");
    
        if (notes == null) notesObj = [];
        else notesObj = JSON.parse(notes);
    
        let html = "";
    
        notesObj.forEach(function(element, index) {
            html += `<div class="noteCard my-2 mx-2 card" 
                style="width: 18rem;">
                    <div class="card-body">
                        <h5 class="card-title">
                            Note ${index + 1}
                        </h5>
                        <p class="card-text"> 
                            ${element}
                        </p>
     
                      <button id="${index}" onclick=
                        "deleteNote(this.id)"
                        class="btn btn-primary">
                        Delete Note
                    </button>
                </div>
            </div>`;
        });
    
        let notesElm = document.getElementById("notes");
    
        if (notesObj.length != 0) notesElm.innerHTML = html;
        else
            notesElm.innerHTML = `Nothing to show! 
            Use "Add a Note" section above to add notes.`;
    }
    
   
    function deleteNote(index) {
        let notes = localStorage.getItem("notes");
    
        if (notes == null) notesObj = [];
        else notesObj = JSON.parse(notes);
    
        notesObj.splice(index, 1);
    
        localStorage.setItem("notes", 
            JSON.stringify(notesObj));
    
        showNotes();
    }
    
</script>
