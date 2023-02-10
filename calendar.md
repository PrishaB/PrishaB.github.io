## Calendar FRQ

<script>

function getYear(){
    let inputYear = document.getElementById("inputYear").value;
    return inputYear;
}

function getMonth(){
    let inputMonth = document.getElementById("inputMonth").value;
    return inputMonth;
}

function getDay(){
    let inputDay = document.getElementById("inputDay").value;
    return inputDay;
}

function getYear2(){
    let inputYear2 = document.getElementById("inputYear2").value;
    return inputYear2;
}

function isLeapYear(yearparam) {
    
    result = document.getElementById("isLeapYearResult");

    // Fetch data from API
    fetch('https://serafina.tk/api/calendar/isLeapYear/' + yearparam)
    .then(response => response.json())
    .then(data => {

        console.log(data);

        result.innerHTML = "Is " + yearparam + " a leap year: " + data.isLeapYear;

    })
}

function firstDayOfYear(yearparam) {

    result = document.getElementById("theFirstDayOfYear");
    fetch('https://serafina.tk/api/calendar/firstDayOfYear/' + yearparam)
    .then(response => response.json())
    .then(data => {
        
        console.log(data);

        result.innerHTML = "The first day of the year: " + yearparam + "was this day of the week: " + data.firstDayOfYear;
    })
}

function dayOfYear(monthparam, dayparam, yearparam) {
    
    result = document.getElementById("dayOfYear");

    // Fetch data from API
    fetch('https://serafina.tk/api/calendar/dayOfYear/' + monthparam+ dayparam+yearparam)
    .then(response => response.json())
    .then(data => {

        console.log(data);

        result.innerHTML = "What day of the year is the date " + monthparam+ dayparam+ yearparam  + data.dayOfYear;

    })
}

function numberOfLeapYears(yearparam, year2param) {
    
    result = document.getElementById("numberOfLeapYears");

    // Fetch data from API
    fetch('https://serafina.tk/api/calendar/numberOfLeapYears/' + yearparam+year2param)
    .then(response => response.json())
    .then(data => {

        console.log(data);

        result.innerHTML = "How many leap years are between " + yearparam + "and" +year2param + data.numberOfLeapYears;

    })
}


function dayOfWeek(monthparam,dayparam, yearparam) {
    
    result = document.getElementById("dayOfWeek");

    // Fetch data from API
    fetch('https://serafina.tk/api/calendar/dayOfWeek/' +monthparam+ dayparam+yearparam)
    .then(response => response.json())
    .then(data => {

        console.log(data);

        result.innerHTML = "What day of the week is the date " + monthparam+ dayparam+ yearparam  +data.dayOfWeek;

    })
}
</script>

### Is this year a leap year?
<input id="inputYear" placeholder="Input a Year">
<button onclick="isLeapYear(getYear())">Submit</button>
<p id="isLeapYearResult"></p>

### The day of week of the first day of Year 
<input id="inputYear" placeholder="Input a Year">
<button onclick="firstDayOfYear(getYear())">Submit</button>
<p id="theFirstDayOfYear"></p>

### Day of Year
<input id="input month" placeholder="Input a month">
<input id="input day" placeholder="Input a day">
<input id="inputYear" placeholder="Input a Year">
<button onclick="dayOfYear(getMonth(),getDay(), getYear())">Submit</button>
<p id="dayOfYear"></p>

### Number of leap years between years
<input id="inputYear" placeholder="Input a Year">
<input id="inputYear2" placeholder="Input a second Year">
<button onclick="numberOfLeapYears(getYear(),getYear2())">Submit</button>
<p id="numberOfLeapYears"></p>

### Day of week
<input id="input month" placeholder="Input a month">
<input id="input day" placeholder="Input a day">
<input id="inputYear" placeholder="Input a Year">
<button onclick="dayOfWeek(getMonth(),getDay(), getYear())">Submit</button>
<p id="dayOfWeek"></p>

<style> 


p {
  font-size: 20px;
  color: white;
}
</style>