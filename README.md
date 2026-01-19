# La-gestion-del-deseo

<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Página en pausa</title>
  <link rel="stylesheet" href="styles.css">
</head>
<body>

  <main>
    <h1>Capítulo I</h1>

    <p class="story">
      La casa estaba en silencio.  
      La luz del teléfono era suficiente.  
      Se detuvo justo antes de decirlo.
    </p>

    <div class="pause">
      <h2>Capítulo en actualización</h2>
      <p>La espera está activa.</p>
    </div>

    <section class="write">
      <h3>Escribe la actualización que esperas</h3>
      <textarea id="userText" placeholder="Aquí continúa la historia..."></textarea>
      <button onclick="saveText()">Guardar</button>
      <p id="status"></p>
    </section>

    <section class="archive">
      <h3>Actualizaciones escritas</h3>
      <div id="entries"></div>
    </section>
  </main>

  <!-- Firebase -->
  <script src="https://www.gstatic.com/firebasejs/9.23.0/firebase-app-compat.js"></script>
  <script src="https://www.gstatic.com/firebasejs/9.23.0/firebase-firestore-compat.js"></script>
  <script src="app.js"></script>

</body>
</html>
body {
  font-family: sans-serif;
  background: #f5f5f5;
  color: #111;
  margin: 0;
  padding: 40px;
}

main {
  max-width: 600px;
  margin: auto;
}

.story {
  font-size: 1.1em;
  margin-bottom: 40px;
}

.pause {
  border-top: 1px solid #ccc;
  padding-top: 20px;
  margin-bottom: 30px;
}

textarea {
  width: 100%;
  height: 120px;
  padding: 10px;
  margin-top: 10px;
}

button {
  margin-top: 10px;
}

.archive {
  margin-top: 50px;
  border-top: 1px solid #ccc;
  padding-top: 20px;
}

.entry {
  background: #fff;
  padding: 10px;
  margin-bottom: 10px;
}
// REEMPLAZA con tu configuración de Firebase
const firebaseConfig = {
  apiKey: "TU_API_KEY",
  authDomain: "TU_DOMINIO",
  projectId: "TU_PROJECT_ID",
};

firebase.initializeApp(firebaseConfig);
const db = firebase.firestore();

 {
  const text = document.getElementById("userText").value;
  if (text.trim() === "") return;

  db.collection("actualizaciones").add({
    contenido: text,
    fecha: new Date()
  });

  document.getElementById("userText").value = "";
  document.getElementById("status").innerText = "Texto guardado.";
}

db.collection("actualizaciones")
  .orderBy("fecha", "desc")
  .onSnapshot(snapshot => {
    const container = document.getElementById("entries");
    container.innerHTML = "";

    snapshot.forEach(doc => {
      const div = document.createElement("div");
      div.className = "entry";
      div.textContent = doc.data().contenido;
      container.appendChild(div);
    });

