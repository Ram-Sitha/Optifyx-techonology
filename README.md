# Optifyx-techonology
Welcome to Optifyx Technology! We are a dynamic and innovative company dedicated to empowering the next generation of tech enthusiasts and budding professionals. At Optifyx Technology, we believe that hands-on experience is the key to unlocking one's full potential and building a successful career in the everevolving tech

"TO-DO-LIST LEVEL-2 TASK-1"

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>To-Do List</title>
    <style>
        body {
            font-family:Arial, sans-serif;
            display:flex;
            justify-content:center;
            align-items:center;
            height:100vh;
            background-color:blue;
        }
        .container {
            background:white;
            padding:20px;
            border-radius:10px;
            box-shadow:0 0 10px rgba(0, 0, 0, 0.1);
            width:300px;
        }
        ul {
            list-style:none;
            padding:0;
        }
        li {
            display:flex;
            justify-content:space-between;
            padding:8px;
            border-bottom:1px solid #ddd;
        }
        button {
            margin-left:5px;
            cursor:pointer;
        }
    </style>
</head>
<body>
    <div class="container">
        <h2>To-Do List</h2>
        <input type="text" id="taskInput" placeholder="Add a task">
        <button onclick="addTask()">Add</button>
        <ul id="taskList"></ul>
    </div>

    <script>
        document.addEventListener("DOMContentLoaded", loadTasks);

        function addTask() {
            let taskInput=document.getElementById("taskInput");
            let taskText=taskInput.value.trim();
            if (taskText==="") return;

            let tasks=JSON.parse(localStorage.getItem("tasks")) || [];
            tasks.push(taskText);
            localStorage.setItem("tasks", JSON.stringify(tasks));
            taskInput.value="";
            loadTasks();
        }

        function loadTasks() {
            let taskList=document.getElementById("taskList");
            taskList.innerHTML="";
            let tasks=JSON.parse(localStorage.getItem("tasks")) || [];
            tasks.forEach((task,index) => {
                let li=document.createElement("li");
                li.textContent=task;
                let deleteBtn=document.createElement("button");
                deleteBtn.textContent="❌";
                deleteBtn.onclick=() => deleteTask(index);
                li.appendChild(deleteBtn);
                taskList.appendChild(li);
            });
        }

        function deleteTask(index) {
            let tasks=JSON.parse(localStorage.getItem("tasks")) || [];
            tasks.splice(index, 1);
            localStorage.setItem("tasks", JSON.stringify(tasks));
            loadTasks();
        }
    </script>
</body>
</html>



"WEATHER APPLICATION" TASK-2


<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Weather App</title>
    <style>
        body {
            font-family:Arial, sans-serif;
            display:flex;
            justify-content:center;
            align-items:center;
            height:100vh;
            background-color:skyblue;
        }
        .container {
            background:whitesmoke;
            padding:20px;
            border-radius:10px;
            box-shadow:0 0 10px rgba(0, 0, 0, 0.1);
            text-align:center;
            width:300px;
        }
        input {
            padding:8px;
            width:80%;
            margin-bottom:10px;
        }
        button {
            padding:8px;
            cursor:pointer;
        }
        .weather-info {
            margin-top:10px;
        }
    </style>
</head>
<body>
    <div class="container">
        <h2>Weather App</h2>
        <input type="text" id="cityInput" placeholder="Enter city name">
        <button onclick="getWeather()">Get Weather</button>
        <div class="weather-info" id="weatherInfo"></div>
    </div>

    <script>
        async function getWeather() {
            const apiKey='your_api_key_here'; // Replace with your API key
            const city=document.getElementById("cityInput").value.trim();
            if (!city) return;

            const url=`https://api.openweathermap.org/data/2.5/weather?q=${city}&appid=${apiKey}&units=metric`;
            
            try {
                const response=await fetch(url);
                const data=await response.json();
                if (data.cod===200) {
                    document.getElementById("weatherInfo").innerHTML = `
                        <h3>${data.name},${data.sys.country}</h3>
                        <p>Temperature:${data.main.temp}°C</p>
                        <p>Weather:${data.weather[0].description}</p>
                        <p>Humidity:${data.main.humidity}%</p>
                    `;
                } else {
                    document.getElementById("weatherInfo").innerHTML=`<p>City not found</p>`;
                }
            } catch (error) {
                document.getElementById("weatherInfo").innerHTML=`<p>Error fetching weather data</p>`;
            }
        }
    </script>
</body>
</html>



"IMAGE_GALLERY" TASK-3


<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Image Gallery with Filtering</title>
    <style>
        body {
            font-family:Arial,sans-serif;
            text-align:center;
        }
        .filter-buttons {
            margin-bottom:20px;
        }
        button {
            margin:5px;
            padding:10px;
            cursor:pointer;
        }
        .gallery {
            display:flex;
            flex-wrap:wrap;
            justify-content:center;
        }
        .gallery img {
            width:200px;
            height:150px;
            margin:10px;
            display:block;
        }
        .hide {
            display:none;
        }
    </style>
</head>
<body>
    <h2>Image Gallery with Filtering</h2>
    <div class="filter-buttons">
        <button onclick="filterImages('all')">All</button>
        <button onclick="filterImages('nature')">Nature</button>
        <button onclick="filterImages('animals')">Animals</button>
        <button onclick="filterImages('city')">City</button>
    </div>
    <div class="gallery">
        <img src="holding-earth-green-tree-hands-world-environment-day-concept-saving-growing-young-tree-element-image-furnished-74844293.webp" class="image nature">
        <img src="adults-baby-hand-tree-environment-earth-day-hands-trees-growing-seedlings-bokeh-green-background-female-holding-tr-130090566.webp" class="image nature">
        <img src="pexels-photo-792381.jpeg" class="image animals">
        <img src="fawn-deer-283005.avif" class="image animals">
        <img src="images.jpg" class="image city">
        <img src="images (1).jpg" class="image city">
    </div>
    <script>
        function filterImages(category) {
            let images=document.querySelectorAll('.image');
            images.forEach(img => {
                if (category==='all'||img.classList.contains(category)) {
                    img.classList.remove('hide');
                } else {
                    img.classList.add('hide');
                }
            });
        }
    </script>
</body>
</html>


