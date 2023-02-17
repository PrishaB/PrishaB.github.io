{% include navbar.html %}

<html>
    <head> 
        <script>
             function uploadFile()
             {
                alert("Hello Prisha"+ fileInput.files[0].name);
                var formdata = new FormData();
                formdata.append("file", fileInput.files[0], "[PROXY]");
                var requestOptions = {
                method: 'POST',
                body: formdata,
                redirect: 'follow'
                };
                fetch("http://localhost:8192/uploadFile", requestOptions)
                .then(response => response.text())
                .then(result => console.log(result))
                .catch(error => console.log('error', error));
             }
            function submit(){
                    let data = document.getElementById("file").files[0];
                    let entry = document.getElementById("file").files[0];
                    console.log('submit',entry,data)
                    fetch("http://localhost:8192/uploadFile", requestOptions)
                    .then(response => response.text())
                    .then(result => console.log(result))
                    .catch(error => console.log('error', error));
             }
        </script> 
    </head>
    <body>
        <form id='formid'> 
            <input type="file" name="fileInput" id="fileInput">
            <button onclick="uploadFile()" name="submit">Submit</button>
        </form> 
    </body> 


</html>