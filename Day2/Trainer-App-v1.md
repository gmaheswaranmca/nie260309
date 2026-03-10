**simple MERN demo project**:

* **React + Vite frontend**
* **Bootstrap via CDN**
* **Navbar routing**
* **Add Trainer page**
* **List Trainers page**
* **Express backend (single file ES6)**
* **MongoDB Atlas connection**
* **.env for config**
* **3 demo trainer records**

Ports:

* Frontend → **3000**
* Backend → **5000**

---

# 1. Project Folder Structure

```
mern-trainer-app
│
├── backend
│   │
│   ├── server.js
│   ├── package.json
│   └── .env
│
└── frontend
    │
    ├── index.html
    ├── vite.config.js
    ├── package.json
    │
    └── src
        │
        ├── main.jsx
        ├── App.jsx
        │
        ├── components
        │     └── Navbar.jsx
        │
        └── pages
              ├── AddTrainer.jsx
              └── ListTrainer.jsx
```

---

# 2. Backend Setup (Express + MongoDB Atlas)

## backend/package.json

```json
{
  "name": "trainer-backend",
  "type": "module",
  "dependencies": {
    "cors": "^2.8.5",
    "dotenv": "^16.3.1",
    "express": "^4.18.2",
    "mongoose": "^8.0.0"
  }
}
```

Install:

```bash
cd backend
npm install
```

---

# 3. Environment File

## backend/.env

```
PORT=5000
MONGO_URL=mongodb+srv://username:password@cluster.mongodb.net/trainerdb
```

---

# 4. Express Server (Single File ES6)

## backend/server.js

```javascript
import express from "express"
import mongoose from "mongoose"
import cors from "cors"
import dotenv from "dotenv"

dotenv.config()

const app = express()

app.use(cors())
app.use(express.json())

const PORT = process.env.PORT
const DB = process.env.MONGO_URL

mongoose.connect(DB)
.then(()=>console.log("MongoDB Connected"))
.catch(err=>console.log(err))

const TrainerSchema = new mongoose.Schema({
    name:String,
    skills:String
})

const Trainer = mongoose.model("Trainer",TrainerSchema)


// Insert demo trainers (only if empty)
async function seedData(){

    const count = await Trainer.countDocuments()

    if(count===0){

        await Trainer.insertMany([
            {name:"Mahesh",skills:"React"},
            {name:"Arun",skills:"Node"},
            {name:"Divya",skills:"MongoDB"}
        ])

        console.log("Demo trainers inserted")
    }
}

seedData()


// get trainers
app.get("/trainers", async(req,res)=>{

    const data = await Trainer.find()

    res.json(data)
})


// add trainer
app.post("/trainer", async(req,res)=>{

    const trainer = new Trainer(req.body)

    await trainer.save()

    res.json({message:"Trainer Added"})
})

app.listen(PORT,()=>{
    console.log("Server running on",PORT)
})
```

Run:

```bash
node server.js
```

Server runs at

```
http://localhost:5000
```

---

# 5. Frontend Setup (React + Vite)

Create project

```bash
npm create vite@latest frontend
cd frontend
npm install
npm install react-router-dom axios
```

---

# 6. Force Vite to run on port 3000

## vite.config.js

```javascript
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'

export default defineConfig({
  plugins: [react()],
  server:{
    port:3000
  }
})
```

---

# 7. Bootstrap CDN

## index.html

```html
<!DOCTYPE html>
<html>
<head>
<title>Trainer App</title>

<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet">

</head>

<body>

<div id="root"></div>

<script type="module" src="/src/main.jsx"></script>

</body>
</html>
```

---

# 8. React Entry

## src/main.jsx

```javascript
import React from "react"
import ReactDOM from "react-dom/client"
import App from "./App"

ReactDOM.createRoot(document.getElementById("root")).render(
<App/>
)
```

---

# 9. App Routing

## src/App.jsx

```javascript
import {BrowserRouter,Routes,Route} from "react-router-dom"

import Navbar from "./components/Navbar"
import AddTrainer from "./pages/AddTrainer"
import ListTrainer from "./pages/ListTrainer"

function App(){

return(

<BrowserRouter>

<Navbar/>

<div className="container mt-3">

<Routes>

<Route path="/" element={<ListTrainer/>}/>

<Route path="/add" element={<AddTrainer/>}/>

</Routes>

</div>

</BrowserRouter>

)

}

export default App
```

---

# 10. Navbar

## components/Navbar.jsx

```javascript
import {Link} from "react-router-dom"

function Navbar(){

return(

<nav className="navbar navbar-dark bg-dark navbar-expand">

<div className="container">

<Link className="navbar-brand" to="/">TrainerApp</Link>

<div className="navbar-nav">

<Link className="nav-link" to="/">List Trainers</Link>

<Link className="nav-link" to="/add">Add Trainer</Link>

</div>

</div>

</nav>

)

}

export default Navbar
```

---

# 11. Add Trainer Page

## pages/AddTrainer.jsx

```javascript
import {useState} from "react"
import axios from "axios"

function AddTrainer(){

const [name,setName] = useState("")
const [skills,setSkills] = useState("")

const saveTrainer = async()=>{

await axios.post("http://localhost:5000/trainer",{
name,
skills
})

alert("Trainer Added")

setName("")
setSkills("")
}

return(

<div>

<h3>Add Trainer</h3>

<input
className="form-control mb-2"
placeholder="Trainer Name"
value={name}
onChange={(e)=>setName(e.target.value)}
/>

<input
className="form-control mb-2"
placeholder="Skills"
value={skills}
onChange={(e)=>setSkills(e.target.value)}
/>

<button
className="btn btn-primary"
onClick={saveTrainer}
>
Save
</button>

</div>

)

}

export default AddTrainer
```

---

# 12. List Trainers Page

## pages/ListTrainer.jsx

```javascript
import {useEffect,useState} from "react"
import axios from "axios"

function ListTrainer(){

const [trainers,setTrainers] = useState([])

useEffect(()=>{

axios.get("http://localhost:5000/trainers")
.then(res=>setTrainers(res.data))

},[])

return(

<div>

<h3>Trainer List</h3>

<table className="table table-bordered">

<thead>

<tr>
<th>Name</th>
<th>Skills</th>
</tr>

</thead>

<tbody>

{trainers.map(t=>(
<tr key={t._id}>
<td>{t.name}</td>
<td>{t.skills}</td>
</tr>
))}

</tbody>

</table>

</div>

)

}

export default ListTrainer
```

---

# 13. Run the Application

### Start Backend

```bash
cd backend
node server.js
```

Runs on

```
http://localhost:5000
```

---

### Start Frontend

```bash
cd frontend
npm run dev
```

Runs on

```
http://localhost:3000
```

---

# Final Output

Navbar:

```
TrainerApp | List Trainers | Add Trainer
```

Pages:

**List Trainers**

| Name   | Skills  |
| ------ | ------- |
| Mahesh | React   |
| Arun   | Node    |
| Divya  | MongoDB |

**Add Trainer**

```
Name  : ______
Skills: ______
[Save]
```
