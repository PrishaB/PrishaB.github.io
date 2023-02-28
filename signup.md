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
  color: var(--bodyColor);
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
  --loginSubmitBackgroundColor: #041836;
  --loginSubmitColor: #eee;
  --loginSubmitHoverBackgroundColor: #D44179;
}
.login {
  color: var(--loginColor);
}
.login label,
.login input[type="text"],
.login input[type="password"],
.login input[type="submit"] {
  border-radius: var(--loginBorderRadus);
  padding: 1rem;
}
.login label {
  background-color: var(--loginLabelBackgroundColor);
  border-bottom-right-radius: 0;
  border-top-right-radius: 0;
  padding-inline: 1.25rem;
}
.login input[type="password"],
.login input[type="text"] {
  background-color: var(--loginInputBackgroundColor);
  border-bottom-left-radius: 0;
  border-top-left-radius: 0;
}
.login input[type="password"]:focus,
.login input[type="password"]:hover,
.login input[type="text"]:focus,
.login input[type="text"]:hover {
  background-color: var(--loginInputHoverBackgroundColor);
}
.login input[type="submit"] {
  background-color: var(--loginSubmitBackgroundColor);
  color: var(--loginSubmitColor);
  font-weight: 700;
  text-transform: uppercase;
}
.login input[type="submit"]:focus,
.login input[type="submit"]:hover {
  background-color: var(--loginSubmitHoverBackgroundColor);
}
/* modules/text.css */
p {
  margin-block: 1.5rem;
}
.text--center {
  text-align: center;
}

</style>


<body class="align">
  <div class="grid">
    <form href="https://httpbin.org/post" method="POST" class="form login" action="javascript:signup()">
      <div class="form__field">
        <label for="login__username"><svg class="icon"> <use xlink:href="#icon-user"></use></svg>
          <span class="hidden">Name</span></label>
        <input autocomplete="Name" id="name" type="text" name="name" class="form__input" placeholder="name" required>
      </div>
       <div class="form__field">
        <label for="login__dob"><svg class="icon"> <use xlink:href="#icon-user"></use></svg>
          <span class="hidden">Date of Birth</span></label>
        <input autocomplete="dob" id="dob" type="text" name="dob" class="form__input" placeholder="MM-DD-YYYY" required>
      </div>
      <div class="form__field">
        <label for="login__email"><svg class="icon"> <use xlink:href="#icon-user"></use></svg>
          <span class="hidden">Email</span></label>
        <input autocomplete="email" id="email" type="text" name="email" class="form__input" placeholder="Email" required>
      </div>
      <div class="form__field">
        <label for="login__password"><svg class="icon"> <use xlink:href="#icon-lock"></use></svg><span class="hidden">Password</span></label>
        <input id="password" type="password" name="password" class="form__input" placeholder="Password" required>
      </div>
      <div class="form__field">
         <label for="login__password"><svg class="icon"> <use xlink:href="#icon-lock"></use></svg><span class="hidden">Confirm password</span></label>
        <input id="password2" type="password" name="password" class="form__input" placeholder="Confirm Password" required>
      </div>
      <div class="form__field">
        <input type="submit" value="Sign Up">
      </div>
      <input type="hidden" name="${_csrf.parameterName}" value="${_csrf.token}"/>
    </form>
  </div>

<script>
    function signup() {
      if(password ==password2){
var url = "https://serafina.tk"
    // Comment out next line for local testing
     url = "http://localhost:8192"
        // Authenticate endpoint
        const signup = url + '/api/person/post';

        const body = {
            email: document.getElementById("email").value,
            password: document.getElementById("password").value,
            name: document.getElementById("name").value,
            Dob: document.getElementById("dob").value
        };

       

        const requestOptions = {
            method: 'POST',
            mode: 'cors', 
            cache: 'no-cache', 
            credentials: 'include',
            body: JSON.stringify(body),
            headers: {
                "content-type": "application/json",
               'Authorization': 'Bearer my-token',
            },
        };

        
            fetch(signup, requestOptions)
            .then(response => {
                // trap error response from Web API
                if (!response.ok) {
                    const error = 'Error: ' + response.status;
                    console.log(error);
               
                }
                window.location.href = "/gallery";
                
            })
      }else{
         window.location.href = "/error";
      }
        

    }

