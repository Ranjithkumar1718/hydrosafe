import React, { useState } from "react";

export default function App() {
  const [step, setStep] = useState(1);
  const [gender, setGender] = useState("");
  const [age, setAge] = useState("");
  const [symptoms, setSymptoms] = useState([]);
  const [village, setVillage] = useState("");
  const [landmark, setLandmark] = useState("");
  const [submitted, setSubmitted] = useState(false);

  const villages = {
    "Village A": ["Temple", "School", "Well"],
    "Village B": ["Bus Stop", "Market", "Panchayat Office"],
    "Village C": ["Church", "Lake", "Clinic"],
  };

  const symptomOptions = ["Fever", "Diarrhea", "Vomiting", "Stomach Pain"];

  const genderOptions = [
    { label: "Male", img: "https://i.ibb.co/ZYW3VTp/male.png" },
    { label: "Female", img: "https://i.ibb.co/ypkgK0X/female.png" },
    { label: "Other", img: "https://i.ibb.co/x2G8qH6/other.png" },
  ];

  const handleSymptomChange = (symptom) => {
    setSymptoms((prev) =>
      prev.includes(symptom)
        ? prev.filter((s) => s !== symptom)
        : [...prev, symptom]
    );
  };

  const handleSubmit = () => {
    setSubmitted(true);
  };

  const buttonStyle = {
    display: "block",
    width: "100%",
    margin: "0.3rem 0",
    padding: "0.5rem",
    borderRadius: "8px",
    border: "1px solid #ccc",
    background: "#f8f8f8",
    cursor: "pointer",
  };

  return (
    <div
      style={{
        display: "flex",
        justifyContent: "center",
        alignItems: "center",
        minHeight: "100vh",
        background: "#E0F2FE",
        padding: "1rem",
      }}
    >
      <div
        style={{
          background: "white",
          borderRadius: "1rem",
          boxShadow: "0 4px 10px rgba(0,0,0,0.1)",
          width: "100%",
          maxWidth: "400px",
          padding: "1.5rem",
        }}
      >
        <h1 style={{ textAlign: "center", color: "#1D4ED8" }}>
          HydroSafe - MVP
        </h1>

        {!submitted ? (
          <>
            {step === 1 && (
              <>
                <p><b>Select Gender:</b></p>
                {genderOptions.map((g) => (
                  <button
                    key={g.label}
                    style={{
                      ...buttonStyle,
                      display: "flex",
                      alignItems: "center",
                      justifyContent: "center",
                      border:
                        gender === g.label
                          ? "2px solid #1D4ED8"
                          : buttonStyle.border,
                    }}
                    onClick={() => setGender(g.label)}
                  >
                    <img
                      src={g.img}
                      alt={g.label}
                      style={{ width: "40px", marginRight: "10px" }}
                    />
                    {g.label}
                  </button>
                ))}
                <button
                  style={{
                    ...buttonStyle,
                    background: "#1D4ED8",
                    color: "white",
                  }}
                  disabled={!gender}
                  onClick={() => setStep(2)}
                >
                  Next
                </button>
              </>
            )}

            {step === 2 && (
              <>
                <p><b>Select Age Group:</b></p>
                {["0-5 years", "6-12 years", "13-18 years", "Adult", "Senior"].map(
                  (a) => (
                    <button
                      key={a}
                      style={{
                        ...buttonStyle,
                        border:
                          age === a
                            ? "2px solid #1D4ED8"
                            : buttonStyle.border,
                      }}
                      onClick={() => setAge(a)}
                    >
                      {a}
                    </button>
                  )
                )}
                <button
                  style={{
                    ...buttonStyle,
                    background: "#1D4ED8",
                    color: "white",
                  }}
                  disabled={!age}
                  onClick={() => setStep(3)}
                >
                  Next
                </button>
              </>
            )}

            {step === 3 && (
              <>
                <p><b>Select Symptoms:</b></p>
                {symptomOptions.map((s) => (
                  <label key={s} style={{ display: "block", margin: "0.5rem 0" }}>
                    <input
                      type="checkbox"
                      checked={symptoms.includes(s)}
                      onChange={() => handleSymptomChange(s)}
                    />{" "}
                    {s}
                  </label>
                ))}
                <button
                  style={{
                    ...buttonStyle,
                    background: "#1D4ED8",
                    color: "white",
                  }}
                  disabled={symptoms.length === 0}
                  onClick={() => setStep(4)}
                >
                  Next
                </button>
              </>
            )}

            {step === 4 && (
              <>
                <p><b>Select Village:</b></p>
                {Object.keys(villages).map((v) => (
                  <button
                    key={v}
                    style={{
                      ...buttonStyle,
                      border:
                        village === v
                          ? "2px solid #1D4ED8"
                          : buttonStyle.border,
                    }}
                    onClick={() => {
                      setVillage(v);
                      setLandmark("");
                    }}
                  >
                    {v}
                  </button>
                ))}

                {village && (
                  <>
                    <p><b>Select Landmark:</b></p>
                    {villages[village].map((lm) => (
                      <button
                        key={lm}
                        style={{
                          ...buttonStyle,
                          border:
                            landmark === lm
                              ? "2px solid #1D4ED8"
                              : buttonStyle.border,
                        }}
                        onClick={() => setLandmark(lm)}
                      >
                        {lm}
                      </button>
                    ))}
                  </>
                )}

                <button
                  style={{
                    ...buttonStyle,
                    background: "#1D4ED8",
                    color: "white",
                  }}
                  disabled={!landmark}
                  onClick={() => setStep(5)}
                >
                  Next
                </button>
              </>
            )}

            {step === 5 && (
              <>
                <p><b>Review Your Report:</b></p>
                <ul>
                  <li><b>Gender:</b> {gender}</li>
                  <li><b>Age Group:</b> {age}</li>
                  <li><b>Symptoms:</b> {symptoms.join(", ")}</li>
                  <li><b>Village:</b> {village}</li>
                  <li><b>Landmark:</b> {landmark}</li>
                </ul>
                <button
                  style={{
                    ...buttonStyle,
                    background: "#16A34A",
                    color: "white",
                  }}
                  onClick={handleSubmit}
                >
                  Confirm & Submit
                </button>
              </>
            )}
          </>
        ) : (
          <div style={{ textAlign: "center" }}>
            <h2 style={{ color: "green" }}>✅ Report Submitted!</h2>
            <p>Your health officer will be notified.</p>
          </div>
        )}
      </div>
    </div>
  );
}
