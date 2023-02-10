## Storing Info About a Person FRQ


<script>
  
  function person() {
    
    result = document.getElementById("personInformation");
    fetch('https://serafina.tk/api/person/')
    .then(response => response.json())
    .then(data => {
        
        console.log(data);
        
        result.innerHTML = "Information from the API: " + data.post;
      
      })
      
}
</script>

<style> 
button {
	width: 120px;
	height: 40px;
	font-size: 15px;
	background-color: #43B4E5;
	color: #fff;
	border: none;
	cursor: pointer;
}

p {
  font-size: 20px;
  color: white;
  
}
</style>

<button onclick="person()">Information About People</button>
<p id="personInformation"></p>