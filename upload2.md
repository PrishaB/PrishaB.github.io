{% include navbar.html %}

<html>
    <head> 
        <script>
             function uploadFile02()
             {
                alert("Hello Prisha"+ fileInput.files[0].name);
                console.log("testing");
                var formdata = new FormData();
                formdata.append("file", fileInput.files[0], "[PROXY]");
                var requestOptions = {
                method: 'POST',
                body: formdata,
                redirect: 'follow'
                };
                console.log("before calling the URL");
                fetch("http://localhost:8192/uploadFile", requestOptions)
                .then(response => response.text())
                .then(result => console.log(result))
                .catch(error => console.log('error', error));
                alert("Completed");
             }
             function uploadFile()
             {
                alert("Hello Prisha"+ fileInput.files[0].name);
                var innerhtml = document.getElementById("img-test").innerHTML;
                console.log("testing");
                var formdata = new FormData();
                formdata.append("filename", fileInput.files[0]);
                var requestOptions = {
                method: 'POST',
                body: formdata,
                redirect: 'follow'
                };
                console.log("before calling the URL");
                fetch("http://localhost:8192/mvc/uploader", requestOptions)
                .then(response => response.text())
                .then(result => console.log(result))
                .catch(error => console.log('error', error));
                alert("Completed");
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
        <br>
        <iframe id="img-test" src="http://localhost:8192/mvc/upload" width="100%" height="100%"> </iframe>
    </body> 


</html>