## Calculator FRQ 

### You can use this feature to do some basic calculations :)

<button onclick="calculator()">Enter Equation</button>

<p> Answer: <p id="answer"> </p>

<script>
  
  function calculator() {
    let expression = prompt("Enter equation");
    const urlStart = "https://serafina.tk/api/calculator/";
    const url = urlStart + expression;

    console.log(url),{"method": "GET"}; 

    fetch(url,{"method": "GET"})
      .then(res => res.json())
      .then(data => {
        console.log(data);
        
        document.getElementById("answer").innerHTML = data.result; 
      
      })
      
}
</script>

<style> 
button {
background-color: pink;
  border: none;
  color: white;
  padding: 15px 32px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  margin: 4px 2px;
  cursor: pointer;
  border-radius: 12px;
}

p {
  font-size: 20px;
  color: white;
}
</style>