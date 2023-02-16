<html>
    <head> 
        <script>
        //      function setup() {
        //         document.getElementById('buttonid').addEventListener('click', openDialog);
        //         function openDialog() {
        //             document.getElementById('fileid').click();
        //         }
        //         document.getElementById('fileid').addEventListener('change', submitForm);
        //         function submitForm() {
        //             document.getElementById('formid').submit();
        //         }
        //    }
            function submit(){
                    let data = document.getElementById("file").files[0];
                    let entry = document.getElementById("file").files[0];
                    console.log('submit',entry,data)
                    fetch('https://localhost8192/uploadFile/' + encodeURIComponent(entry.name), {method:'PUT',body:data});
                    alert('your file has been uploaded');
             }
        </script> 
    </head>
    <body onload="submit()">
        <form id='formid' action="javascript:submit()" method="POST" enctype="multipart/form-data"> 
            <input type="file" name="file" id="file">
            <button onclick="submit()" name="submit">Submit</button>
            <!-- <input id='fileid' type='file' name='filename' hidden/>
            <input id='buttonid' type='button' value='Upload Image' /> 
            <input type='submit' value='Submit' />  -->
        </form> 
    </body> 


</html>