<style>
@use postcss-preset-env {
  stage: 0;
}
/* config.css */
:root {
  --baseColor: #606468;
}
/* helpers/align.css */
.align {
  display: grid;
  place-items: center;
}
.grid {
  inline-size: 90%;
  margin-inline: auto;
  max-inline-size: 20rem;
}
/* helpers/hidden.css */
.hidden {
  border: 0;
  clip: rect(0 0 0 0);
  height: 1px;
  margin: -1px;
  overflow: hidden;
  padding: 0;
  position: absolute;
  width: 1px;
}
/* helpers/icon.css */
:root {
  --iconFill: var(--baseColor);
}
.icons {
  display: none;
}
.icon {
  block-size: 1em;
  display: inline-block;
  fill: var(--iconFill);
  inline-size: 1em;
  vertical-align: middle;
}
/* layout/base.css */
:root {
  --htmlFontSize: 100%;
  
  --bodyColor: var(--baseColor);
  --bodyFontFamily: "Open Sans";
  --bodyFontFamilyFallback: sans-serif;
  --bodyFontSize: 0.875rem;
  --bodyFontWeight: 400;
  --bodyLineHeight: 1.5;
}
* {
  box-sizing: inherit;
}
html {
  box-sizing: border-box;
  font-size: var(--htmlFontSize);
}
body {
  background: linear-gradient(45deg, #49a09d, #5f2c82);
  color: white;
  font-family: var(--bodyFontFamily), var(--bodyFontFamilyFallback);
  font-size: var(--bodyFontSize);
  font-weight: var(--bodyFontWeight);
  line-height: var(--bodyLineHeight);
  margin: 0;
  min-block-size: 100vh;
}
/* modules/anchor.css */
:root {
  --anchorColor: #eee;
}
a {
  color: var(--anchorColor);
  outline: 0;
  text-decoration: none;
}
a:focus,
a:hover {
  text-decoration: underline;
}
/* modules/form.css */
:root {
  --formGap: 0.875rem;
}
input {
  background-image: none;
  border: 0;
  color: inherit;
  font: inherit;
  margin: 0;
  outline: 0;
  padding: 0;
  transition: background-color 0.3s;
}
input[type="submit"] {
  cursor: pointer;
}
.form {
  display: grid;
  gap: var(--formGap);
}
.form input[type="password"],
.form input[type="text"],
.form input[type="submit"] {
  inline-size: 100%;
}
.form__field {
  display: flex;
}
.form__input {
  flex: 1;
}
/* modules/login.css */
:root {
  --loginBorderRadus: 0.25rem;
  --loginColor: #eee;
  --loginInputBackgroundColor: #3B4148;
  --loginInputHoverBackgroundColor: #434A52;
  --loginLabelBackgroundColor: #363B41;
  --loginSubmitBackgroundColor: #EA4C88;
  --loginSubmitColor: #eee;
  --loginSubmitHoverBackgroundColor: #D44179;
}
/* modules/text.css */
p {
  margin-block: 1.5rem;
}
.text--center {
  text-align: center;
}

</style>

# Profile
<p> Welcome! </p>
<br>
<div id="userInfo">
  <div id="email"></div>
  <div id="name"></div>
  <div id="dob"></div>
  <div id="roles"></div>
</div>
<br>

<p>
<button class="button">Delete </button>
</p>
 
       

<script>
   

Email: <input type="text" id="email">

Name: <input type="text" id="name">

Dob: <input type="date" id="dob">

Password: <input type="text" id="password">
    
    var getUrl = "https://serafina.tk/api/person/email";

    var getOptions = {
      method: 'GET', 
      mode: 'cors', 
      cache: 'default', 
      credentials: 'include', 
      headers: {
        'Content-Type': 'application/json',
      },
    };

    fetch(getUrl, getOptions)
    .then(response => {
        //error message
        if (!response.ok) {
            const errorMsg = 'Login error: ' + response.status;
            console.log(errorMsg);
            return;
        }
 
        response.json().then(data => {
            //if success
            console.log(data); 

            var dob = data.dob;

            document.getElementById("email").placeholder = data.email; 
            document.getElementById("name").placeholder = data.name; 
            document.getElementById("dob").placeholder = dob; 
           

        })
    })


    function update() {
        var getUrl = "https://serafina.tk/api/person/update";

        var getOptions = {
        method: 'GET', 
        mode: 'cors', 
        cache: 'default', 
        credentials: 'include', 
        headers: {
            'Content-Type': 'application/json',
        },
        };

        fetch(getUrl, getOptions)
        .then(response => {
            //error message
            if (!response.ok) {
                const errorMsg = 'Login error: ' + response.status;
                console.log(errorMsg);
                return;
            }
    
            response.json().then(data => {
                console.log(data); 

                var id = data.id; 

                console.log(id);

                var email = document.getElementById("email").value;
                var name = document.getElementById("name").value;
                var dob = document.getElementById("dob").value;

                console.log(email);
                console.log(name);
                console.log(dob);

                var updateUrl = "https://serafina.tk/api/person/update";

       
                var updateBody = {
                    id: id,
                    email: email,
                    name: name,
                    dob: dob
                };

       
                var updateOptions = {
                    method: 'POST',
                    mode: 'cors', // no-cors, *cors, same-origin
                    cache: 'no-cache', // *default, no-cache, reload, force-cache, only-if-cached
                    //credentials: 'include', // include, *same-origin, omit
                    body: JSON.stringify(updateBody),
                    headers: {
                        "content-type": "application/json"
                    },
                };

       

                fetch(updateUrl, updateOptions)
                .then(response => {
                    // trap error response from Web API
                    if (!response.ok) {
                        const errorMsg = 'Login error: ' + response.status;
                        console.log(errorMsg);

                        document.getElementById("updateSuccess").innerHTML = "";


                        var p = document.createElement("p");
                        var msg = document.createTextNode("Info successfully updated!"); 
                        p.appendChild(msg); 
                        document.getElementById("updateSuccess").appendChild(p); 
                    }

                        document.getElementById("updateSuccess").innerHTML = "";

                        var p = document.createElement("p");
                        var msg = document.createTextNode("Info successfully updated!"); 
                        p.appendChild(msg); 
                        document.getElementById("updateSuccess").appendChild(p); 
                })

            }) 
            
        })
    }
        

    function changePassword() {
        document.getElementById("passwordMsg").innerHTML = ""; 
        //get user id from cookie (need id to delete user)
        var getUrl = "https://serafina.tk/api/person/email";

        var getOptions = {
        method: 'GET', 
        mode: 'cors', 
        cache: 'default', 
        credentials: 'include', 
        headers: {
            'Content-Type': 'application/json',
        },
        };

        fetch(getUrl, getOptions)
        .then(response => {
            //error message
            if (!response.ok) {
                const errorMsg = 'Login error: ' + response.status;
                console.log(errorMsg);
                return;
            }
    
            response.json().then(data => {
                //if success
                console.log("User id successfully obtained");
                console.log(data); 

                var id = data.id; 

                console.log(id);

                var password = document.getElementById("password").value;

                console.log(password);

            }) 
            
        })
    }


    function changepassword(id, password) {
        var url = "https://serafina.tk/api/person/update";
       
        var body = {
            id: id,
            password: password
        };


        var option = {
            method: 'POST',
            mode: 'cors', // no-cors, *cors, same-origin
            cache: 'no-cache', // *default, no-cache, reload, force-cache, only-if-cached
            //credentials: 'include', // include, *same-origin, omit
            body: JSON.stringify(body),
            headers: {
                "content-type": "application/json"
            },
        };



        fetch(url, option)
        .then(response => {
            // trap error response from Web API
            if (!response.ok) {
                const errorMsg = 'Login error: ' + response.status;
                console.log(errorMsg);

                var p = document.createElement("p");
                var msg = document.createTextNode("Password successfully changed!"); 
                p.appendChild(msg); 
                document.getElementById("passwordMsg").appendChild(p); 
                return;
            }
            
            var p = document.createElement("p");
            var msg = document.createTextNode("Password successfully changed!"); 
            p.appendChild(msg); 
            document.getElementById("passwordMsg").appendChild(p); 
        })
    }


  function deleteUsr() {
    

    //get user id from cookie (need id to delete user)
    var getUrl = "https://serafina.tk/api/person/delete";

    var getOptions = {
      method: 'GET', 
      mode: 'cors', 
      cache: 'default', 
      credentials: 'include', 
      headers: {
        'Content-Type': 'application/json',
      },
    };

    fetch(getUrl, getOptions)
    .then(response => {
        //error message
        if (!response.ok) {
            const errorMsg = 'Login error: ' + response.status;
            console.log(errorMsg);
            return;
        }

        response.json().then(data => {
          console.log(data);

          //get id from cookie
          var id = data.id;

          console.log("id: " + id);

          //delete user based on id
          var deleteBaseURL = "https://serafina.tk";
          var deleteURL = deleteBaseURL + '/api/person/delete/' + id;

          console.log("delete user url: " + deleteURL);

          var deleteOptions = {
            method: 'GET', 
            mode: 'cors', 
            cache: 'default', 
            credentials: 'include', 
            headers: {
              'Content-Type': 'application/json',
            },
          };
              
          fetch(deleteURL, deleteOptions)
          .then(response => {
              //error
              if (!response.ok) {
                  const errorMsg = 'Error: ' + response.status;
                  console.log(errorMsg);
                  return;
              }

            window.location.href = "/gallery";
            
            })


         
        })
    })
    
       

    }