<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>XV Años - Invitación Interactiva</title>
  <link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@400;600;700&family=Great+Vibes&display=swap" rel="stylesheet">
  <style>
    :root {
      --primary: #d4af37; /* Dorado / Oro rosa */
      --dark: #222;
      --bg: #fdfbf7;
      --card-bg: #ffffff;
    }

    * { box-sizing: border-box; margin: 0; padding: 0; }
    
    body {
      font-family: 'Montserrat', sans-serif;
      background-color: var(--bg);
      color: var(--dark);
      display: flex;
      justify-content: center;
      padding: 20px 10px;
    }

    .container {
      max-width: 500px;
      width: 100%;
      background: var(--card-bg);
      border-radius: 20px;
      box-shadow: 0 10px 30px rgba(0,0,0,0.1);
      padding: 30px 20px;
      text-align: center;
      border: 2px solid var(--primary);
    }

    h1.cursive {
      font-family: 'Great Vibes', cursive;
      font-size: 3.2rem;
      color: var(--primary);
      margin-bottom: 5px;
    }

    .subtitle {
      font-size: 0.9rem;
      letter-spacing: 2px;
      text-transform: uppercase;
      margin-bottom: 25px;
      color: #666;
    }

    .box {
      background: #faf8f5;
      border-radius: 12px;
      padding: 20px;
      margin-bottom: 20px;
      text-align: left;
      border-left: 4px solid var(--primary);
    }

    .question-title {
      font-weight: 600;
      margin-bottom: 12px;
      font-size: 0.95rem;
    }

    .option-btn {
      display: block;
      width: 100%;
      padding: 12px;
      margin-bottom: 8px;
      background: #fff;
      border: 1px solid #ddd;
      border-radius: 8px;
      text-align: left;
      cursor: pointer;
      transition: all 0.2s ease;
      font-size: 0.85rem;
    }

    .option-btn:hover, .option-btn.selected {
      border-color: var(--primary);
      background: #fffdf5;
      font-weight: 600;
    }

    .form-group {
      margin-bottom: 15px;
      text-align: left;
    }

    label {
      font-size: 0.85rem;
      font-weight: 600;
      display: block;
      margin-bottom: 5px;
    }

    input, select {
      width: 100%;
      padding: 12px;
      border: 1px solid #ccc;
      border-radius: 8px;
      font-size: 0.9rem;
    }

    .submit-btn {
      background: var(--primary);
      color: #fff;
      border: none;
      width: 100%;
      padding: 15px;
      font-size: 1rem;
      font-weight: 700;
      border-radius: 30px;
      cursor: pointer;
      box-shadow: 0 4px 15px rgba(212, 175, 55, 0.4);
      transition: transform 0.2s;
    }

    .submit-btn:active {
      transform: scale(0.98);
    }

    .hidden { display: none; }

    .success-msg {
      padding: 20px;
      background: #eef9f2;
      border-radius: 12px;
      color: #276738;
    }
  </style>
</head>
<body>

<div class="container">
  <h1 class="cursive">Mis XV Años</h1>
  <p class="subtitle">¡Estás invitado/a a celebrar!</p>

  <!-- SECCIÓN DEL TEST INTERACTIVO -->
  <div id="test-section">
    <div class="box">
      <p class="question-title">📋 1. ¿Cuál es tu plan para la pista de baile?</p>
      <button type="button" class="option-btn" onclick="selectOption(1, 'Bailarín VIP')">A) Bailar de todo hasta que el cuerpo aguante.</button>
      <button type="button" class="option-btn" onclick="selectOption(1, 'Ambiente de mesa')">B) Disfrutar el ambiente, cenar rico y brindar.</button>
    </div>

    <div class="box">
      <p class="question-title">🥳 2. ¿Qué tan listos están para celebrar a la quinceañera?</p>
      <button type="button" class="option-btn" onclick="selectOption(2, '100% Contando días')">A) ¡100% listos y contando los días!</button>
      <button type="button" class="option-btn" onclick="selectOption(2, 'Preparado para el gran día')">B) ¡Listísimos para abrazarla y consentirla!</button>
    </div>
  </div>

  <!-- SECCIÓN DEL FORMULARIO DE CONFIRMACIÓN -->
  <form id="rsvp-form" onsubmit="submitToGoogleForm(event)">
    <div class="form-group">
      <label for="guest-name">👤 Tu Nombre Completo:</label>
      <input type="text" id="guest-name" placeholder="Ej. Familia Pérez / Juan Gómez" required>
    </div>

    <div class="form-group">
      <label for="pass-type">🎟️ Confirmación de Asistencia / Pase:</label>
      <select id="pass-type" required>
        <option value="" disabled selected>Selecciona una opción</option>
        <option value="Individual (Solo yo)">Pase Individual (1 Persona)</option>
        <option value="Pase Doble (Yo + 1 acompañante)">Pase Doble (Máximo 2 Personas en total)</option>
        <option value="Pase Triple (Yo + 2 acompañantes)">Pase Triple (Máximo 3 Personas en total)</option>
      </select>
    </div>

    <button type="submit" class="submit-btn">✨ CONFIRMAR ASISTENCIA</button>
  </form>

  <div id="thank-you" class="success-msg hidden">
    <h2>🎉 ¡Confirmación Recibida!</h2>
    <p>Tus respuestas han sido registradas exitosamente.</p>
    <p>¡Nos dará muchísimo gusto celebrar contigo!</p>
  </div>
</div>

<script>
  let answers = { q1: '', q2: '' };

  function selectOption(qNum, value) {
    answers['q' + qNum] = value;
    // Marcar visualmente
    const buttons = event.target.parentElement.querySelectorAll('.option-btn');
    buttons.forEach(btn => btn.classList.remove('selected'));
    event.target.classList.add('selected');
  }

  function submitToGoogleForm(event) {
    event.preventDefault();

    const name = document.getElementById('guest-name').value;
    const pass = document.getElementById('pass-type').value;
    const testResult = `Pista: ${answers.q1 || 'Sin responder'}, Actitud: ${answers.q2 || 'Sin responder'}`;

    // ⚠️ REEMPLAZA ESTOS VALORES CON LOS DE TU GOOGLE FORM ⚠️
    const FORM_URL = "https://docs.google.com/forms/d/e/TU_ID_DE_FORMULARIO/formResponse";
    const ENTRY_NAME = "entry.123456789";   // ID del campo Nombre
    const ENTRY_PASS = "entry.987654321";   // ID del campo Pase
    const ENTRY_TEST = "entry.555555555";   // ID del campo Test

    // Construcción de datos mediante URLSearchParams
    const formData = new URLSearchParams();
    formData.append(ENTRY_NAME, name);
    formData.append(ENTRY_PASS, pass);
    formData.append(ENTRY_TEST, testResult);

    // Envío silencioso a Google Forms por fetch (mode: no-cors)
    fetch(FORM_URL, {
      method: "POST",
      mode: "no-cors",
      headers: {
        "Content-Type": "application/x-www-form-urlencoded"
      },
      body: formData.toString()
    }).then(() => {
      // Ocultar formulario y mostrar mensaje de agradecimiento
      document.getElementById('test-section').classList.add('hidden');
      document.getElementById('rsvp-form').classList.add('hidden');
      document.getElementById('thank-you').classList.remove('hidden');
    }).catch(error => {
      alert("Hubo un detalle al enviar tu respuesta. Inténtalo de nuevo.");
      console.error(error);
    });
  }
</script>

</body>
</html>
