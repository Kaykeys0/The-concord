import React, { useState, useEffect } from "react";
import axios from "axios";
import {
  BrowserRouter as Router,
  Routes,
  Route,
  Link
} from "react-router-dom";

/* =======================
   Sidebar
======================= */
function Sidebar() {
  return (
    <div className="w-64 h-screen bg-gray-900 text-white fixed">
      <h1 className="text-xl font-bold p-4">Admin Panel</h1>
      <nav className="flex flex-col gap-2 p-4">
        <Link to="/" className="hover:bg-gray-700 p-2 rounded">Dashboard</Link>
        <Link to="/students" className="hover:bg-gray-700 p-2 rounded">Students</Link>
        <Link to="/teachers" className="hover:bg-gray-700 p-2 rounded">Teachers</Link>
        <Link to="/subjects" className="hover:bg-gray-700 p-2 rounded">Subjects</Link>
        <Link to="/results" className="hover:bg-gray-700 p-2 rounded">Results</Link>
      </nav>
    </div>
  );
}

/* =======================
   Navbar
======================= */
function Navbar() {
  return (
    <div className="ml-64 bg-white shadow p-4 flex justify-between">
      <h2 className="font-semibold">School Dashboard</h2>
      <button className="bg-red-500 text-white px-4 py-1 rounded">
        Logout
      </button>
    </div>
  );
}

/* =======================
   Card Component
======================= */
function Card({ title, value }) {
  return (
    <div className="bg-white p-4 shadow rounded">
      <h3>{title}</h3>
      <p className="text-2xl font-bold">{value}</p>
    </div>
  );
}

/* =======================
   Dashboard Page
======================= */
function Dashboard() {
  return (
    <div className="ml-64 p-6 grid grid-cols-3 gap-4">
      <Card title="Students" value="320" />
      <Card title="Teachers" value="25" />
      <Card title="Classes" value="11" />

      <div className="col-span-3 bg-white p-4 shadow rounded">
        <h2 className="font-bold mb-2">Grade Structure</h2>
        <div className="grid grid-cols-3 gap-4">
          <div>
            <h3 className="font-semibold">Pre-Primary</h3>
            <p>PP1, PP2</p>
          </div>
          <div>
            <h3 className="font-semibold">Primary</h3>
            <p>Grade 1 - 6</p>
          </div>
          <div>
            <h3 className="font-semibold">Junior School</h3>
            <p>Grade 7 - 9</p>
          </div>
        </div>
      </div>
    </div>
  );
}

/* =======================
   Students Page
======================= */
function Students() {
  const [students, setStudents] = useState([]);
  const [form, setForm] = useState({ name: "", grade: "", photo: "" });

  const fetchStudents = async () => {
    const res = await axios.get("/api/students");
    setStudents(res.data);
  };

  const addStudent = async () => {
    await axios.post("/api/students", form);
    fetchStudents();
  };

  useEffect(() => { fetchStudents(); }, []);

  return (
    <div className="ml-64 p-6">
      <h2 className="text-xl font-bold mb-4">Students</h2>

      <div className="bg-white p-4 shadow rounded mb-4 flex gap-2">
        <input placeholder="Name" onChange={e=>setForm({...form,name:e.target.value})}/>
        <input placeholder="Grade" onChange={e=>setForm({...form,grade:e.target.value})}/>
        <input placeholder="Photo URL" onChange={e=>setForm({...form,photo:e.target.value})}/>
        <button onClick={addStudent} className="bg-blue-500 text-white px-4 py-1">Add</button>
      </div>

      <table className="w-full bg-white shadow">
        <thead>
          <tr>
            <th>Name</th>
            <th>Grade</th>
          </tr>
        </thead>
        <tbody>
          {students.map(s => (
            <tr key={s._id}>
              <td>{s.name}</td>
              <td>{s.grade}</td>
            </tr>
          ))}
        </tbody>
      </table>
    </div>
  );
}

/* =======================
   Teachers Page
======================= */
function Teachers() {
  return (
    <div className="ml-64 p-6">
      <h2 className="text-xl font-bold">Teachers</h2>
      <p>Connect to backend</p>
    </div>
  );
}

/* =======================
   Subjects Page
======================= */
function Subjects() {
  const [grade, setGrade] = useState("");
  const [subjects, setSubjects] = useState("");

  const save = async () => {
    await axios.post("/api/subjects", {
      grade,
      subjects: subjects.split(",")
    });
    alert("Saved!");
  };

  return (
    <div className="ml-64 p-6">
      <h2 className="text-xl font-bold mb-4">Subjects Setup</h2>

      <div className="flex gap-2">
        <input placeholder="Grade" onChange={e=>setGrade(e.target.value)} />
        <input placeholder="Subjects comma separated" onChange={e=>setSubjects(e.target.value)} />
        <button onClick={save} className="bg-green-500 text-white px-4 py-1">Save</button>
      </div>
    </div>
  );
}

/* =======================
   Results Page
======================= */
function Results() {
  return (
    <div className="ml-64 p-6">
      <h2 className="text-xl font-bold">Results Overview</h2>
      <p>Ranking and analytics coming soon</p>
    </div>
  );
}

/* =======================
   MAIN APP
======================= */
export default function App() {
  return (
    <Router>
      <Sidebar />
      <Navbar />

      <Routes>
        <Route path="/" element={<Dashboard />} />
        <Route path="/students" element={<Students />} />
        <Route path="/teachers" element={<Teachers />} />
        <Route path="/subjects" element={<Subjects />} />
        <Route path="/results" element={<Results />} />
      </Routes>
    </Router>
  );
}
