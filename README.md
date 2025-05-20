<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>ChatBot Ingeniería Civil Industrial</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f2f2f2;
      padding: 20px;
    }
    #chatbox {
      background: #fff;
      border: 1px solid #ccc;
      border-radius: 10px;
      padding: 15px;
      max-width: 600px;
      height: 400px;
      overflow-y: auto;
      white-space: pre-line;
    }
    input, button {
      padding: 10px;
      margin-top: 10px;
      width: 300px;
      font-size: 16px;
    }
    .qr img {
      margin-top: 10px;
      width: 120px;
      height: 120px;
    }
  </style>
</head>
<body>

<h2>Bienvenido al ChatBot de Ingeniería Civil Industrial 👷‍♂️</h2>
<div id="chatbox">¿En qué te puedo ayudar?
1. Información general de la carrera  
2. Preguntas Frecuentes (FAQ)  
3. Otros  
4. Salir
</div>

<input type="text" id="userInput" placeholder="Escribe el número de opción aquí...">
<button onclick="procesarEntrada()">Enviar</button>

<script>
let estado = 'menu';

const urlAdaptacion = "https://scanned.page/p/681e2c35aadee";
const urlBuses = "https://uta.cl/buses";

const menuPrincipal = "¿En qué te puedo ayudar?\n1. Información general de la carrera\n2. Preguntas Frecuentes (FAQ)\n3. Otros\n4. Salir";
const submenuInfoGeneral = "📌 Submenú - Información General:\n1. Perfil de egreso\n2. Objetivos de la carrera\n3. Áreas de formación\n0. Volver";
const submenuFAQ = "❓ Submenú - Preguntas Frecuentes:\n1. Licencias Médicas\n2. Trabajo al egresar\n3. Traslado\n4. Postulaciones\n5. Inscripciones\n6. Becas\n7. Biblioteca\n0. Volver";
const submenuPostulaciones = "📝 Submenú - Postulaciones:\n1. Ayudante\n2. Tutor Par\n3. CEC\n0. Volver";
const submenuInscripciones = "📆 Submenú - Inscripciones:\n1. ¿Asignaturas?\n2. ¿Matrículas?\n3. ¿Modificar inscripción?\n0. Volver";
const submenuBecas = "🎓 Submenú - Becas:\n1. Honor\n2. CFT\n3. Estudiantil\n4. Alimentación\n5. Fotocopias\n6. Residencia\n7. BAES\n8. Títulos\n9. Internado\n10. Práctica\n11. Viaje\n0. Volver";
const submenuBiblioteca = "📚 Submenú - Biblioteca:\n1. Libros\n2. Box\n3. Impreteca\n4. Tablets\n5. Audiovisuales\n6. Inclusiva\n0. Volver";
const submenuTraslado = "🔄 Submenú - Traslado:\n1. Carrera\n2. Sede\n3. Institución\n0. Volver al menú principal";
const submenuOtros = "🔧 Submenú - Otros:\n1. Buses de acercamiento\n2. Denuncias y Acoso\n3. Servicio Médico Estudiantil\n4. Adaptación Regular Académica\n5. Reincorporación a la carrera\n0. Volver al menú principal";

function actualizarChat(texto) {
  const chatbox = document.getElementById('chatbox');
  chatbox.innerHTML += `<p>${texto}</p>`;
  chatbox.scrollTop = chatbox.scrollHeight;
}

function mostrarQR(url) {
  const chatbox = document.getElementById('chatbox');
  const qrURL = `https://api.qrserver.com/v1/create-qr-code/?size=120x120&data=${encodeURIComponent(url)}`;
  chatbox.innerHTML += `<div class="qr"><img src="${qrURL}" alt="QR"></div>`;
  chatbox.scrollTop = chatbox.scrollHeight;
}

document.getElementById("userInput").addEventListener("keypress", function (e) {
  if (e.key === "Enter") procesarEntrada();
});

function procesarEntrada() {
  const entrada = document.getElementById('userInput').value.trim();
  document.getElementById('userInput').value = '';

  switch (estado) {
    case 'menu':
      if (entrada === '1') { estado = 'info_general'; actualizarChat(submenuInfoGeneral); }
      else if (entrada === '2') { estado = 'faq'; actualizarChat(submenuFAQ); }
      else if (entrada === '3') { estado = 'otros'; actualizarChat(submenuOtros); }
      else if (entrada === '4') { estado = 'finalizado'; actualizarChat("🚪 Gracias por usar el chatbot. ¡Hasta luego!"); }
      else actualizarChat("❌ Opción inválida.");
      break;

    case 'otros':
      if (entrada === '1') {
        actualizarChat("🚌 Buses gratuitos de acercamiento.");
        mostrarQR(urlBuses);
        actualizarChat(submenuOtros);
      } else if (entrada === '2') {
        actualizarChat("🚨 Denuncias en plataforma institucional.");
        actualizarChat(submenuOtros);
      } else if (entrada === '3') {
        actualizarChat("🏥 Atención médica gratuita.");
        actualizarChat(submenuOtros);
      } else if (entrada === '4') {
        actualizarChat("📘 Adaptación académica para condiciones especiales. Escanea el siguiente código QR:");
        mostrarQR(urlAdaptacion);
        actualizarChat(submenuOtros);
      } else if (entrada === '5') {
        actualizarChat("↩️ Reincorporación mediante solicitud formal.");
        actualizarChat(submenuOtros);
      } else if (entrada === '0') {
        estado = 'menu';
        actualizarChat(menuPrincipal);
      } else {
        actualizarChat("❌ Opción inválida.");
        actualizarChat(submenuOtros);
      }
      break;

    case 'info_general':
      const info = {
        '1': "👨‍🎓 Perfil: lidera procesos organizacionales.",
        '2': "🎯 Objetivo: formar profesionales íntegros.",
        '3': "📚 Áreas: Ciencias Básicas, Ingeniería, Gestión."
      };
      if (entrada === '0') { estado = 'menu'; actualizarChat(menuPrincipal); return; }
      actualizarChat(info[entrada] || "❌ Opción inválida.");
      actualizarChat(submenuInfoGeneral);
      break;

    case 'faq':
      if (entrada === '1') actualizarChat("📄 Licencias en Secretaría de Carrera dentro de 3 días.");
      else if (entrada === '2') actualizarChat("🏢 Puedes trabajar en sector público, privado, industria.");
      else if (entrada === '3') { estado = 'traslado'; actualizarChat(submenuTraslado); return; }
      else if (entrada === '4') { estado = 'postulaciones'; actualizarChat(submenuPostulaciones); return; }
      else if (entrada === '5') { estado = 'inscripciones'; actualizarChat(submenuInscripciones); return; }
      else if (entrada === '6') { estado = 'becas'; actualizarChat(submenuBecas); return; }
      else if (entrada === '7') { estado = 'biblioteca'; actualizarChat(submenuBiblioteca); return; }
      else if (entrada === '0') { estado = 'menu'; actualizarChat(menuPrincipal); return; }
      else actualizarChat("❌ Opción inválida.");
      actualizarChat(submenuFAQ);
      break;

    case 'postulaciones':
      const post = {
        '1': "🧑‍🏫 Ayudantías desde segundo año.",
        '2': "🤝 Tutor Par: apoyo entre estudiantes.",
        '3': "👥 CEC organiza actividades y representa a estudiantes."
      };
      if (entrada === '0') { estado = 'faq'; actualizarChat(submenuFAQ); return; }
      actualizarChat(post[entrada] || "❌ Opción inválida.");
      actualizarChat(submenuPostulaciones);
      break;

    case 'inscripciones':
      const ins = {
        '1': "📘 Asignaturas vía Portal Académico.",
        '2': "🧾 Matrículas online o presencial según calendario.",
        '3': "✏️ Puedes modificar inscripción durante ajustes."
      };
      if (entrada === '0') { estado = 'faq'; actualizarChat(submenuFAQ); return; }
      actualizarChat(ins[entrada] || "❌ Opción inválida.");
      actualizarChat(submenuInscripciones);
      break;

    case 'becas':
      const becas = {
        '1': '🏆 Beca de Honor.',
        '2': '🏫 CFT: Apoyo técnico.',
        '3': '🎓 Estudiantil.',
        '4': '🍴 Alimentación.',
        '5': '🖨️ Fotocopias.',
        '6': '🏠 Residencia.',
        '7': '💳 BAES.',
        '8': '📜 Títulos.',
        '9': '🏥 Internado.',
        '10': '📚 Práctica.',
        '11': '🚌 Viaje.'
      };
      if (entrada === '0') { estado = 'faq'; actualizarChat(submenuFAQ); return; }
      actualizarChat(becas[entrada] || "❌ Opción inválida.");
      actualizarChat(submenuBecas);
      break;

    case 'biblioteca':
      const bib = {
        '1': '📚 Libros físicos y digitales.',
        '2': '📖 Reserva box estudio.',
        '3': '🖨️ Impreteca.',
        '4': '📱 Tablets/iPads.',
        '5': '🎥 Audiovisuales.',
        '6': '🧏 Sala inclusiva.'
      };
      if (entrada === '0') { estado = 'faq'; actualizarChat(submenuFAQ); return; }
      actualizarChat(bib[entrada] || "❌ Opción inválida.");
      actualizarChat(submenuBiblioteca);
      break;

    case 'traslado':
      const tras = {
        '1': '🔄 Cambio de carrera con requisitos.',
        '2': '🏙️ Cambio de sede sujeto a vacantes.',
        '3': '🏛️ Cambio de institución con postulación especial.'
      };
      if (entrada === '0') { estado = 'faq'; actualizarChat(submenuFAQ); return; }
      actualizarChat(tras[entrada] || "❌ Opción inválida.");
      actualizarChat(submenuTraslado);
      break;

    case 'finalizado':
      actualizarChat("🚫 Chat finalizado. Recarga para comenzar de nuevo.");
      break;

    default:
      actualizarChat("⚠️ Estado desconocido.");
      break;
  }
}
</script>

</body>
</html>
