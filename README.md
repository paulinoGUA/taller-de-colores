# taller-de-colores
taller de colores 
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Taller de Mezcla de Pigmentos</title>
    <!-- Carga de Tailwind CSS para un estilizado rápido y responsivo -->
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        /* Define la fuente Inter si no está ya en el sistema */
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&display=swap');
        body {
            font-family: 'Inter', sans-serif;
            background-color: #f0fdf4; /* Un verde muy claro para el fondo */
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            padding: 1rem;
            box-sizing: border-box;
        }
        .container {
            background-color: #ffffff;
            border-radius: 1.5rem; /* Bordes más redondeados */
            box-shadow: 0 10px 20px rgba(0, 0, 0, 0.1);
            max-width: 900px;
            width: 100%;
            padding: 2.5rem; /* Más padding */
            display: flex;
            flex-direction: column;
            gap: 2rem;
        }
        .color-palette {
            display: flex;
            flex-wrap: wrap;
            gap: 0.75rem; /* Espaciado entre colores */
            justify-content: center;
        }
        .color-swatch {
            width: 50px;
            height: 50px;
            border-radius: 50%; /* Círculos perfectos */
            border: 2px solid #cbd5e1; /* Borde sutil */
            cursor: pointer;
            transition: transform 0.2s ease-in-out, box-shadow 0.2s ease-in-out;
        }
        .color-swatch:hover {
            transform: scale(1.1);
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2);
        }
        .color-picker {
            display: flex;
            flex-direction: column;
            gap: 1rem;
        }
        .mixed-color-display {
            width: 150px;
            height: 150px;
            border-radius: 1.5rem;
            border: 3px solid #6ee7b7; /* Borde verde claro */
            background-color: #e2e8f0; /* Color inicial gris claro */
            margin: 0 auto;
            transition: background-color 0.5s ease-in-out;
        }
        .result-text {
            font-size: 1.125rem; /* Texto más grande */
            font-weight: 600;
            color: #16a34a; /* Verde oscuro */
            text-align: center;
        }
        button {
            padding: 0.75rem 1.5rem;
            border-radius: 0.75rem;
            font-weight: 600;
            cursor: pointer;
            transition: background-color 0.3s ease, transform 0.2s ease;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
        }
        button:hover {
            transform: translateY(-2px);
        }
        .button-primary {
            background-color: #059669; /* Verde más fuerte */
            color: white;
            border: none;
        }
        .button-primary:hover {
            background-color: #047857;
        }
        .feedback-message {
            margin-top: 1rem;
            padding: 1rem;
            border-radius: 0.75rem;
            font-weight: 500;
            text-align: center;
            opacity: 0; /* Oculto por defecto */
            transition: opacity 0.5s ease;
        }
        .feedback-message.show {
            opacity: 1; /* Mostrar mensaje */
        }
        .feedback-success {
            background-color: #d1fae5; /* Verde claro */
            color: #065f46; /* Verde oscuro */
        }
        .feedback-error {
            background-color: #fee2e2; /* Rojo claro */
            color: #991b1b; /* Rojo oscuro */
        }

        /* Estilos responsivos para dispositivos móviles */
        @media (max-width: 768px) {
            .container {
                padding: 1.5rem;
                gap: 1.5rem;
            }
            .color-swatch {
                width: 45px;
                height: 45px;
            }
            .mixed-color-display {
                width: 120px;
                height: 120px;
            }
            h1 {
                font-size: 1.75rem;
            }
            p {
                font-size: 0.9rem;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <h1 class="text-3xl font-bold text-center text-gray-800 mb-4">🎨 Taller de Mezcla de Pigmentos: ¡Descubre el Color! 🖌️</h1>
        <p class="text-lg text-center text-gray-600">
            <strong>Instrucciones:</strong> Selecciona dos colores primarios de la paleta. Después de mezclar, te desafiaremos a nombrar el color resultante.
            ¡Explora y experimenta con la combinación de pigmentos!
        </p>

        <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
            <!-- Sección de selección de colores -->
            <div class="color-picker p-6 bg-gray-50 rounded-xl shadow-inner">
                <h2 class="text-xl font-semibold text-gray-700 mb-4 text-center">Selecciona tus Pigmentos</h2>
                <div class="color-palette">
                    <!-- Colores primarios -->
                    <div class="color-swatch" style="background-color: #FF0000;" data-color="red" data-name="Rojo" onclick="selectColor(this)"></div>
                    <div class="color-swatch" style="background-color: #0000FF;" data-color="blue" data-name="Azul" onclick="selectColor(this)"></div>
                    <div class="color-swatch" style="background-color: #FFFF00;" data-color="yellow" data-name="Amarillo" onclick="selectColor(this)"></div>
                </div>
                <div class="flex justify-center mt-4 gap-4">
                    <div id="selectedColor1" class="w-20 h-20 border-2 border-dashed border-gray-400 rounded-lg flex items-center justify-center text-gray-500 font-medium">1er Color</div>
                    <div id="selectedColor2" class="w-20 h-20 border-2 border-dashed border-gray-400 rounded-lg flex items-center justify-center text-gray-500 font-medium">2do Color</div>
                </div>
                <button class="button-primary mt-6" onclick="mixColors()">¡Mezclar Colores!</button>
            </div>

            <!-- Sección de resultado y desafío -->
            <div class="p-6 bg-gray-50 rounded-xl shadow-inner flex flex-col items-center justify-center gap-4">
                <h2 class="text-xl font-semibold text-gray-700 text-center">Color Resultante</h2>
                <div id="mixedColorDisplay" class="mixed-color-display"></div>
                <p id="resultText" class="result-text mt-2">Mezcla los colores para ver el resultado.</p>

                <div class="w-full flex flex-col items-center mt-4">
                    <label for="colorGuess" class="text-gray-700 text-lg mb-2">¿Cómo se llama este color?</label>
                    <input type="text" id="colorGuess" class="w-full max-w-xs p-3 border border-gray-300 rounded-lg shadow-sm focus:outline-none focus:ring-2 focus:ring-green-400" placeholder="Escribe tu respuesta aquí...">
                    <button class="button-primary mt-4" onclick="checkGuess()">Verificar Respuesta</button>
                    <div id="feedbackMessage" class="feedback-message"></div>
                </div>
            </div>
        </div>
    </div>

    <script type="module">
        // Importar las funciones de Firebase
        import { initializeApp } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-app.js";
        import { getAuth, signInAnonymously, signInWithCustomToken, onAuthStateChanged } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-auth.js";
        import { getFirestore, doc, setDoc, getDoc, collection, addDoc } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-firestore.js";

        // Inicializar variables globales para Firebase
        let app;
        let db;
        let auth;
        let userId;

        // Configuración de Firebase (se inyecta en el entorno de Canvas)
        const firebaseConfig = JSON.parse(typeof __firebase_config !== 'undefined' ? __firebase_config : '{}');
        const appId = typeof __app_id !== 'undefined' ? __app_id : 'default-app-id';

        // Función para inicializar Firebase y autenticar al usuario
        async function initializeFirebase() {
            try {
                if (!app) { // Inicializar la app solo una vez
                    app = initializeApp(firebaseConfig);
                    db = getFirestore(app);
                    auth = getAuth(app);

                    // Autenticar al usuario
                    if (typeof __initial_auth_token !== 'undefined') {
                        await signInWithCustomToken(auth, __initial_auth_token);
                    } else {
                        await signInAnonymously(auth);
                    }

                    // Obtener el userId después de la autenticación
                    userId = auth.currentUser?.uid || crypto.randomUUID();
                    console.log("Firebase inicializado. User ID:", userId);
                }
            } catch (error) {
                console.error("Error al inicializar Firebase o autenticar:", error);
            }
        }

        // Llamar a la función de inicialización de Firebase al cargar la ventana
        window.onload = initializeFirebase;

        let selectedColors = [];
        const colorNames = {
            "red": "Rojo",
            "blue": "Azul",
            "yellow": "Amarillo",
            "orange": "Naranja",
            "green": "Verde",
            "purple": "Violeta"
        };
        const colorHex = {
            "red": "#FF0000",
            "blue": "#0000FF",
            "yellow": "#FFFF00",
            "orange": "#FFA500", // Rojo + Amarillo
            "green": "#008000", // Azul + Amarillo
            "purple": "#800080" // Rojo + Azul
        };

        const mixRules = {
            "red_yellow": { name: "Naranja", hex: "#FFA500" },
            "yellow_red": { name: "Naranja", hex: "#FFA500" },
            "blue_yellow": { name: "Verde", hex: "#008000" },
            "yellow_blue": { name: "Verde", hex: "#008000" },
            "red_blue": { name: "Violeta", hex: "#800080" },
            "blue_red": { name: "Violeta", hex: "#800080" }
        };

        let currentMixedColorName = ''; // Para almacenar el nombre del color mezclado actual

        // Función para seleccionar colores
        function selectColor(element) {
            const color = element.dataset.color;
            const colorName = element.dataset.name;

            if (selectedColors.length < 2) {
                selectedColors.push({ color: color, name: colorName });
                updateSelectedColorDisplay();
            } else {
                // Si ya hay dos colores, reemplazar el primero
                selectedColors.shift();
                selectedColors.push({ color: color, name: colorName });
                updateSelectedColorDisplay();
            }
        }

        // Actualiza la visualización de los colores seleccionados
        function updateSelectedColorDisplay() {
            const selectedColor1Div = document.getElementById('selectedColor1');
            const selectedColor2Div = document.getElementById('selectedColor2');

            selectedColor1Div.innerHTML = selectedColors[0] ? `<div class="w-full h-full rounded-lg" style="background-color: ${colorHex[selectedColors[0].color]};"></div>` : '1er Color';
            selectedColor2Div.innerHTML = selectedColors[1] ? `<div class="w-full h-full rounded-lg" style="background-color: ${colorHex[selectedColors[1].color]};"></div>` : '2do Color';
        }

        // Función para mezclar colores
        async function mixColors() {
            const mixedColorDisplay = document.getElementById('mixedColorDisplay');
            const resultText = document.getElementById('resultText');
            const feedbackMessage = document.getElementById('feedbackMessage');
            feedbackMessage.classList.remove('show', 'feedback-success', 'feedback-error'); // Limpiar mensajes anteriores
            document.getElementById('colorGuess').value = ''; // Limpiar campo de adivinanza

            if (selectedColors.length === 2) {
                const mixKey = `${selectedColors[0].color}_${selectedColors[1].color}`;
                const mixedResult = mixRules[mixKey];

                if (mixedResult) {
                    mixedColorDisplay.style.backgroundColor = mixedResult.hex;
                    resultText.textContent = `¡Has mezclado ${selectedColors[0].name} y ${selectedColors[1].name}!`;
                    currentMixedColorName = mixedResult.name; // Almacenar el nombre correcto del color mezclado
                    console.log(`Color mezclado: ${currentMixedColorName}`);

                    // Guardar la mezcla en Firestore
                    if (db && userId) {
                        try {
                            const mixesCollectionRef = collection(db, `artifacts/${appId}/users/${userId}/colorMixes`);
                            await addDoc(mixesCollectionRef, {
                                color1: selectedColors[0].name,
                                color2: selectedColors[1].name,
                                mixedColor: mixedResult.name,
                                timestamp: new Date()
                            });
                            console.log("Mezcla guardada en Firestore.");
                        } catch (e) {
                            console.error("Error al guardar la mezcla en Firestore:", e);
                        }
                    } else {
                        console.warn("Firebase no está listo o userId no disponible para guardar la mezcla.");
                    }
                } else {
                    mixedColorDisplay.style.backgroundColor = '#e2e8f0'; // Volver al color por defecto si la mezcla no está definida
                    resultText.textContent = "Mezcla de colores no definida. Intenta con colores primarios.";
                    currentMixedColorName = '';
                }
            } else {
                resultText.textContent = "Por favor, selecciona dos colores para mezclar.";
                mixedColorDisplay.style.backgroundColor = '#e2e8f0';
                currentMixedColorName = '';
            }
        }

        // Función para verificar la adivinanza del usuario
        function checkGuess() {
            const userGuess = document.getElementById('colorGuess').value.trim();
            const feedbackMessage = document.getElementById('feedbackMessage');
            feedbackMessage.classList.remove('feedback-success', 'feedback-error'); // Limpiar clases anteriores

            if (!currentMixedColorName) {
                feedbackMessage.textContent = "Primero, mezcla dos colores.";
                feedbackMessage.classList.add('feedback-error', 'show');
                return;
            }

            if (userGuess.toLowerCase() === currentMixedColorName.toLowerCase()) {
                feedbackMessage.textContent = `¡Correcto! Es ${currentMixedColorName}. ¡Excelente! 🎉`;
                feedbackMessage.classList.add('feedback-success', 'show');
            } else {
                feedbackMessage.textContent = `Incorrecto. El color es ${currentMixedColorName}. ¡Sigue practicando! 🤔`;
                feedbackMessage.classList.add('feedback-error', 'show');
            }
        }

    </script>
</body>
</html>
