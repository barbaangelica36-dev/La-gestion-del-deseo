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


  <!-- Firebase -->
  

    snapshot.forEach(doc => {
      const div = document.createElement("div");
      div.className = "entry";
      div.textContent = doc.data().contenido;
      container.appendChild(div);
    });

