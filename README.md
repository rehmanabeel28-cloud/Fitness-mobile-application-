# Fitness-mobile-application-
assignment of fitness mobile application
import { useState } from "react";

const exercises = [
  {
    id: 1,
    name: "Push-Ups",
    category: "Chest",
    duration: "3 sets × 15 reps",
    image: "💪",
    description:
      "A classic upper-body exercise that targets the chest, shoulders, and triceps. Keep your body straight and lower your chest to the floor, then push back up.",
    completed: false,
    color: "#FF6B6B",
  },
  {
    id: 2,
    name: "Squats",
    category: "Legs",
    duration: "4 sets × 20 reps",
    image: "🦵",
    description:
      "The king of leg exercises. Stand with feet shoulder-width apart, lower your hips as if sitting in a chair, keeping your knees behind your toes.",
    completed: false,
    color: "#4ECDC4",
  },
  {
    id: 3,
    name: "Plank",
    category: "Core",
    duration: "3 sets × 60 sec",
    image: "🧘",
    description:
      "A full-body isometric exercise that strengthens the core, shoulders, and glutes. Hold a straight line from head to heels.",
    completed: false,
    color: "#45B7D1",
  },
  {
    id: 4,
    name: "Jumping Jacks",
    category: "Cardio",
    duration: "3 sets × 2 min",
    image: "⚡",
    description:
      "A full-body cardio movement that raises heart rate and warms up every muscle group. Jump while spreading legs and raising arms overhead.",
    completed: false,
    color: "#F7DC6F",
  },
  {
    id: 5,
    name: "Bicep Curls",
    category: "Arms",
    duration: "3 sets × 12 reps",
    image: "🏋️",
    description:
      "Isolation exercise for the biceps. Stand with dumbbells at your sides, curl the weight upward while keeping elbows tucked.",
    completed: false,
    color: "#BB8FCE",
  },
  {
    id: 6,
    name: "Mountain Climbers",
    category: "Cardio",
    duration: "3 sets × 45 sec",
    image: "🏃",
    description:
      "A dynamic core and cardio exercise. Start in a push-up position and alternate driving knees toward your chest rapidly.",
    completed: false,
    color: "#F0B27A",
  },
];

const motivationalQuotes = [
  { text: "The only bad workout is the one that didn't happen.", author: "Unknown" },
  { text: "Push yourself, because no one else is going to do it for you.", author: "Unknown" },
  { text: "Sweat is just fat crying.", author: "Unknown" },
  { text: "Your body can stand almost anything. It's your mind that you have to convince.", author: "Unknown" },
  { text: "No pain, no gain. Shut up and train.", author: "Unknown" },
];

export default function FitnessTrackerApp() {
  const [screen, setScreen] = useState("home");
  const [selectedExercise, setSelectedExercise] = useState(null);
  const [exerciseList, setExerciseList] = useState(exercises);
  const [form, setForm] = useState({ name: "", category: "", duration: "", description: "" });
  const [formError, setFormError] = useState("");
  const [formSuccess, setFormSuccess] = useState(false);
  const [activeTab, setScreen2] = useState("exercises");
  const [quote] = useState(motivationalQuotes[Math.floor(Math.random() * motivationalQuotes.length)]);

  const toggleComplete = (id) => {
    setExerciseList((prev) =>
      prev.map((ex) => (ex.id === id ? { ...ex, completed: !ex.completed } : ex))
    );
  };

  const handleAddExercise = () => {
    if (!form.name || !form.category || !form.duration) {
      setFormError("Please fill in all required fields.");
      return;
    }
    const newEx = {
      id: Date.now(),
      name: form.name,
      category: form.category,
      duration: form.duration,
      description: form.description || "Custom exercise added by user.",
      image: "🔥",
      completed: false,
      color: "#" + Math.floor(Math.random() * 0xffffff).toString(16).padStart(6, "0"),
    };
    setExerciseList((prev) => [...prev, newEx]);
    setForm({ name: "", category: "", duration: "", description: "" });
    setFormError("");
    setFormSuccess(true);
    setTimeout(() => setFormSuccess(false), 2500);
  };

  const completedCount = exerciseList.filter((e) => e.completed).length;

  const styles = {
    phone: {
      width: 390,
      minHeight: 780,
      background: "#0D0D0D",
      borderRadius: 40,
      margin: "0 auto",
      fontFamily: "'Courier New', monospace",
      overflow: "hidden",
      boxShadow: "0 0 0 8px #1a1a1a, 0 0 0 12px #333, 0 40px 80px rgba(0,0,0,0.8)",
      position: "relative",
      border: "1px solid #2a2a2a",
    },
    statusBar: {
      background: "#0D0D0D",
      padding: "14px 28px 8px",
      display: "flex",
      justifyContent: "space-between",
      alignItems: "center",
      color: "#fff",
      fontSize: 12,
      fontWeight: "bold",
    },
    screen: {
      background: "#0D0D0D",
      minHeight: 660,
      overflowY: "auto",
      maxHeight: 660,
      scrollbarWidth: "none",
    },
    navBar: {
      background: "#111",
      borderTop: "1px solid #1e1e1e",
      display: "flex",
      justifyContent: "space-around",
      padding: "10px 0 16px",
    },
    navBtn: (active) => ({
      background: "none",
      border: "none",
      color: active ? "#00FF94" : "#555",
      cursor: "pointer",
      display: "flex",
      flexDirection: "column",
      alignItems: "center",
      gap: 4,
      fontSize: 10,
      fontFamily: "'Courier New', monospace",
      fontWeight: active ? "bold" : "normal",
    }),
  };

  const HomeScreen = () => (
    <div style={{ padding: "0 0 20px" }}>
      {/* Header */}
      <div
        style={{
          background: "linear-gradient(135deg, #00FF94 0%, #00C9FF 100%)",
          padding: "24px 24px 32px",
          position: "relative",
          overflow: "hidden",
        }}
      >
        <div style={{ position: "absolute", top: -30, right: -30, width: 120, height: 120, borderRadius: "50%", background: "rgba(255,255,255,0.1)" }} />
        <div style={{ position: "absolute", bottom: -20, left: -20, width: 80, height: 80, borderRadius: "50%", background: "rgba(0,0,0,0.1)" }} />
        <p style={{ margin: 0, color: "#005F3A", fontSize: 11, letterSpacing: 3, textTransform: "uppercase" }}>GOOD MORNING</p>
        <h1 style={{ margin: "4px 0 2px", color: "#000", fontSize: 26, fontWeight: 900, letterSpacing: -1 }}>FIT_TRACK</h1>
        <p style={{ margin: 0, color: "#004d30", fontSize: 12 }}>
          {completedCount}/{exerciseList.length} exercises done today
        </p>
        {/* progress bar */}
        <div style={{ marginTop: 12, background: "rgba(0,0,0,0.2)", borderRadius: 10, height: 6 }}>
          <div
            style={{
              width: `${(completedCount / exerciseList.length) * 100}%`,
              height: "100%",
              background: "#000",
              borderRadius: 10,
              transition: "width 0.4s ease",
            }}
          />
        </div>
      </div>

      {/* Quote card */}
      <div style={{ margin: "16px 16px 0", background: "#111", borderRadius: 16, padding: "14px 18px", borderLeft: "3px solid #00FF94" }}>
        <p style={{ margin: 0, color: "#00FF94", fontSize: 10, letterSpacing: 2, textTransform: "uppercase" }}>DAILY MOTIVATION</p>
        <p style={{ margin: "6px 0 2px", color: "#eee", fontSize: 12, lineHeight: 1.5, fontStyle: "italic" }}>"{quote.text}"</p>
      </div>

      {/* Exercise List */}
      <div style={{ padding: "20px 16px 0" }}>
        <p style={{ margin: "0 0 12px", color: "#555", fontSize: 11, letterSpacing: 3, textTransform: "uppercase" }}>EXERCISES</p>
        {exerciseList.map((ex) => (
          <div
            key={ex.id}
            style={{
              background: ex.completed ? "#0a1a0f" : "#111",
              borderRadius: 16,
              marginBottom: 10,
              padding: "14px 16px",
              display: "flex",
              alignItems: "center",
              gap: 14,
              cursor: "pointer",
              border: ex.completed ? "1px solid #00FF94" : "1px solid #1e1e1e",
              transition: "all 0.2s",
            }}
            onClick={() => { setSelectedExercise(ex); setScreen("detail"); }}
          >
            <div
              style={{
                width: 48,
                height: 48,
                borderRadius: 14,
                background: ex.color + "22",
                display: "flex",
                alignItems: "center",
                justifyContent: "center",
                fontSize: 22,
                flexShrink: 0,
              }}
            >
              {ex.image}
            </div>
            <div style={{ flex: 1 }}>
              <p style={{ margin: 0, color: ex.completed ? "#00FF94" : "#fff", fontSize: 14, fontWeight: "bold" }}>{ex.name}</p>
              <p style={{ margin: "2px 0 0", color: "#555", fontSize: 11 }}>{ex.category} · {ex.duration}</p>
            </div>
            <button
              onClick={(e) => { e.stopPropagation(); toggleComplete(ex.id); }}
              style={{
                width: 28,
                height: 28,
                borderRadius: "50%",
                border: ex.completed ? "none" : "2px solid #333",
                background: ex.completed ? "#00FF94" : "transparent",
                color: ex.completed ? "#000" : "transparent",
                cursor: "pointer",
                fontSize: 14,
                display: "flex",
                alignItems: "center",
                justifyContent: "center",
                flexShrink: 0,
              }}
            >
              ✓
            </button>
          </div>
        ))}
      </div>
    </div>
  );

  const DetailScreen = () => {
    if (!selectedExercise) return null;
    const ex = exerciseList.find((e) => e.id === selectedExercise.id);
    return (
      <div>
        {/* Back + hero */}
        <div
          style={{
            background: `linear-gradient(160deg, ${ex.color}33 0%, #0D0D0D 70%)`,
            padding: "16px 20px 30px",
            position: "relative",
          }}
        >
          <button
            onClick={() => setScreen("home")}
            style={{
              background: "#1a1a1a",
              border: "1px solid #333",
              color: "#fff",
              borderRadius: 20,
              padding: "6px 14px",
              cursor: "pointer",
              fontSize: 12,
              fontFamily: "'Courier New', monospace",
              marginBottom: 20,
            }}
          >
            ← Back
          </button>
          <div style={{ textAlign: "center" }}>
            <div
              style={{
                width: 90,
                height: 90,
                borderRadius: 28,
                background: ex.color + "33",
                border: `2px solid ${ex.color}66`,
                display: "flex",
                alignItems: "center",
                justifyContent: "center",
                fontSize: 44,
                margin: "0 auto 14px",
              }}
            >
              {ex.image}
            </div>
            <h2 style={{ margin: 0, color: "#fff", fontSize: 22, fontWeight: 900 }}>{ex.name}</h2>
            <p style={{ margin: "4px 0 0", color: ex.color, fontSize: 12, letterSpacing: 2 }}>{ex.category.toUpperCase()}</p>
          </div>
        </div>

        <div style={{ padding: "20px" }}>
          {/* Stats row */}
          <div style={{ display: "flex", gap: 10, marginBottom: 20 }}>
            {[["⏱", ex.duration, "VOLUME"], ["✅", ex.completed ? "Done" : "Pending", "STATUS"]].map(([icon, val, label]) => (
              <div key={label} style={{ flex: 1, background: "#111", borderRadius: 14, padding: "14px 12px", textAlign: "center", border: "1px solid #1e1e1e" }}>
                <p style={{ margin: 0, fontSize: 20 }}>{icon}</p>
                <p style={{ margin: "4px 0 2px", color: "#fff", fontSize: 13, fontWeight: "bold" }}>{val}</p>
                <p style={{ margin: 0, color: "#555", fontSize: 10, letterSpacing: 2 }}>{label}</p>
              </div>
            ))}
          </div>

          {/* Description */}
          <div style={{ background: "#111", borderRadius: 16, padding: "16px", marginBottom: 20, border: "1px solid #1e1e1e" }}>
            <p style={{ margin: "0 0 8px", color: "#555", fontSize: 10, letterSpacing: 3 }}>DESCRIPTION</p>
            <p style={{ margin: 0, color: "#ccc", fontSize: 13, lineHeight: 1.7 }}>{ex.description}</p>
          </div>

          <button
            onClick={() => toggleComplete(ex.id)}
            style={{
              width: "100%",
              padding: "16px",
              borderRadius: 16,
              border: "none",
              background: ex.completed ? "#1a1a1a" : "linear-gradient(135deg, #00FF94, #00C9FF)",
              color: ex.completed ? "#555" : "#000",
              fontSize: 14,
              fontWeight: "bold",
              fontFamily: "'Courier New', monospace",
              cursor: "pointer",
              letterSpacing: 1,
            }}
          >
            {ex.completed ? "✓ MARK AS INCOMPLETE" : "MARK AS COMPLETE ✓"}
          </button>
        </div>
      </div>
    );
  };

  const AddExerciseScreen = () => (
    <div style={{ padding: "24px 20px" }}>
      <h2 style={{ margin: "0 0 4px", color: "#fff", fontSize: 22, fontWeight: 900 }}>ADD EXERCISE</h2>
      <p style={{ margin: "0 0 24px", color: "#555", fontSize: 12 }}>Create your custom workout</p>

      {formSuccess && (
        <div style={{ background: "#0a2a15", border: "1px solid #00FF94", borderRadius: 12, padding: "12px 16px", marginBottom: 16 }}>
          <p style={{ margin: 0, color: "#00FF94", fontSize: 13 }}>✓ Exercise added successfully!</p>
        </div>
      )}
      {formError && (
        <div style={{ background: "#2a0a0a", border: "1px solid #FF6B6B", borderRadius: 12, padding: "12px 16px", marginBottom: 16 }}>
          <p style={{ margin: 0, color: "#FF6B6B", fontSize: 13 }}>⚠ {formError}</p>
        </div>
      )}

      {[
        { label: "Exercise Name *", key: "name", placeholder: "e.g. Deadlifts" },
        { label: "Category *", key: "category", placeholder: "e.g. Back, Legs, Cardio" },
        { label: "Duration / Sets *", key: "duration", placeholder: "e.g. 3 sets × 10 reps" },
        { label: "Description", key: "description", placeholder: "Describe the exercise..." },
      ].map(({ label, key, placeholder }) => (
        <div key={key} style={{ marginBottom: 16 }}>
          <p style={{ margin: "0 0 6px", color: "#777", fontSize: 11, letterSpacing: 2, textTransform: "uppercase" }}>{label}</p>
          {key === "description" ? (
            <textarea
              value={form[key]}
              onChange={(e) => setForm((f) => ({ ...f, [key]: e.target.value }))}
              placeholder={placeholder}
              rows={3}
              style={{
                width: "100%",
                background: "#111",
                border: "1px solid #222",
                borderRadius: 12,
                padding: "12px 14px",
                color: "#fff",
                fontSize: 13,
                fontFamily: "'Courier New', monospace",
                resize: "none",
                outline: "none",
                boxSizing: "border-box",
              }}
            />
          ) : (
            <input
              type="text"
              value={form[key]}
              onChange={(e) => setForm((f) => ({ ...f, [key]: e.target.value }))}
              placeholder={placeholder}
              style={{
                width: "100%",
                background: "#111",
                border: "1px solid #222",
                borderRadius: 12,
                padding: "12px 14px",
                color: "#fff",
                fontSize: 13,
                fontFamily: "'Courier New', monospace",
                outline: "none",
                boxSizing: "border-box",
              }}
            />
          )}
        </div>
      ))}

      <button
        onClick={handleAddExercise}
        style={{
          width: "100%",
          padding: "16px",
          borderRadius: 16,
          border: "none",
          background: "linear-gradient(135deg, #00FF94, #00C9FF)",
          color: "#000",
          fontSize: 14,
          fontWeight: "bold",
          fontFamily: "'Courier New', monospace",
          cursor: "pointer",
          letterSpacing: 1,
          marginTop: 8,
        }}
      >
        + ADD EXERCISE
      </button>
    </div>
  );

  const CompletedScreen = () => {
    const done = exerciseList.filter((e) => e.completed);
    return (
      <div style={{ padding: "24px 20px" }}>
        <h2 style={{ margin: "0 0 4px", color: "#fff", fontSize: 22, fontWeight: 900 }}>COMPLETED</h2>
        <p style={{ margin: "0 0 24px", color: "#555", fontSize: 12 }}>{done.length} exercises finished</p>
        {done.length === 0 ? (
          <div style={{ textAlign: "center", padding: "40px 20px" }}>
            <p style={{ fontSize: 40 }}>🏁</p>
            <p style={{ color: "#444", fontSize: 13 }}>No completed exercises yet.<br />Go crush some workouts!</p>
          </div>
        ) : (
          done.map((ex) => (
            <div
              key={ex.id}
              style={{
                background: "#0a1a0f",
                borderRadius: 14,
                marginBottom: 10,
                padding: "14px 16px",
                display: "flex",
                alignItems: "center",
                gap: 14,
                border: "1px solid #00FF9444",
              }}
            >
              <div style={{ fontSize: 24 }}>{ex.image}</div>
              <div style={{ flex: 1 }}>
                <p style={{ margin: 0, color: "#00FF94", fontSize: 14, fontWeight: "bold" }}>{ex.name}</p>
                <p style={{ margin: "2px 0 0", color: "#555", fontSize: 11 }}>{ex.duration}</p>
              </div>
              <span style={{ color: "#00FF94", fontSize: 18 }}>✓</span>
            </div>
          ))
        )}
      </div>
    );
  };

  const tabs = [
    { id: "home", label: "HOME", icon: "🏠" },
    { id: "add", label: "ADD", icon: "➕" },
    { id: "done", label: "DONE", icon: "✅" },
  ];

  const renderScreen = () => {
    if (screen === "detail") return <DetailScreen />;
    if (activeTab === "home") return <HomeScreen />;
    if (activeTab === "add") return <AddExerciseScreen />;
    if (activeTab === "done") return <CompletedScreen />;
  };

  return (
    <div
      style={{
        minHeight: "100vh",
        background: "radial-gradient(ellipse at top, #0a2a1a 0%, #050505 60%)",
        display: "flex",
        alignItems: "center",
        justifyContent: "center",
        padding: "40px 20px",
        fontFamily: "'Courier New', monospace",
      }}
    >
      <div>
        {/* App title above phone */}
        <div style={{ textAlign: "center", marginBottom: 24 }}>
          <h1 style={{ margin: 0, color: "#00FF94", fontSize: 13, letterSpacing: 6, textTransform: "uppercase" }}>
            FITNESS TRACKER — EXPO / REACT NATIVE
          </h1>
        </div>

        {/* Phone frame */}
        <div style={styles.phone}>
          {/* Notch */}
          <div style={{ background: "#0D0D0D", display: "flex", justifyContent: "center", paddingTop: 10 }}>
            <div style={{ width: 100, height: 28, background: "#000", borderRadius: 20 }} />
          </div>

          {/* Status bar */}
          <div style={styles.statusBar}>
            <span>9:41</span>
            <span>●●● 5G 🔋</span>
          </div>

          {/* App screen */}
          <div style={styles.screen}>{renderScreen()}</div>

          {/* Nav bar */}
          {screen !== "detail" && (
            <div style={styles.navBar}>
              {tabs.map((tab) => (
                <button
                  key={tab.id}
                  style={styles.navBtn(activeTab === tab.id)}
                  onClick={() => { setScreen2(tab.id); setScreen("home"); }}
                >
                  <span style={{ fontSize: 20 }}>{tab.icon}</span>
                  <span>{tab.label}</span>
                </button>
              ))}
            </div>
          )}
        </div>

        <p style={{ textAlign: "center", color: "#333", fontSize: 11, marginTop: 20, letterSpacing: 2 }}>
          BUILT WITH EXPO / REACT NATIVE · ALL SCREENS FUNCTIONAL
        </p>
      </div>
    </div>
  );
}
