# healthcare
it is about healthcare for disabled people as well as for people facing from disease
fhir/mock_data.json — Fake FHIR Patient Data
{
  "resourceType": "Patient",
  "id": "12345",
  "name": [{
    "use": "official",
    "family": "Keller",
    "given": ["Helen"]
  }],
  "gender": "female",
  "birthDate": "1880-06-27"
}
frontend/App.jsx — React App with Symptom Input
import { useState } from "react";
import axios from "axios";

function App() {
  const [symptoms, setSymptoms] = useState("");
  const [result, setResult] = useState("");

  const handleSubmit = async () => {
    const res = await axios.post("http://localhost:8000/predict", {
      symptoms: symptoms.toLowerCase().split(","),
    });
    setResult(res.data.prediction);
  };

  return (
    <div className="p-4 max-w-md mx-auto">
      <h1 className="text-2xl font-bold mb-4">HealChain MVP</h1>
      <textarea
        className="w-full border p-2 mb-2"
        rows="3"
        placeholder="Enter symptoms (e.g. fatigue, fever)"
        value={symptoms}
        onChange={(e) => setSymptoms(e.target.value)}
      />
      <button
        onClick={handleSubmit}
        className="bg-blue-500 text-white px-4 py-2 rounded"
      >
        Predict
      </button>
      {result && <p className="mt-4 text-lg">Prediction: {result}</p>}
    </div>
  );
}

export default App;
