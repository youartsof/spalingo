<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta name="theme-color" content="#dc2626">
  <meta name="description" content="Learn Spanish with vibrant A1 and A2 courses, interactive games, and exercises in a stunning Spanish-Moroccan design.">
  <title>Spanish Learning Hub: A1 & A2</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <script src="https://cdn.jsdelivr.net/npm/react@18.2.0/umd/react.production.min.js"></script>
  <script src="https://cdn.jsdelivr.net/npm/react-dom@18.2.0/umd/react-dom.production.min.js"></script>
  <script src="https://cdn.jsdelivr.net/npm/@babel/standalone@7.22.5/babel.min.js"></script>
  <link href="https://fonts.googleapis.com/css2?family=Cinzel:wght@400;700&family=Lora:wght@400;700&family=Poppins:wght@400;600&display=swap" rel="stylesheet">
  <style>
    body {
      font-family: 'Lora', serif;
      background: linear-gradient(135deg, #fef3e8 0%, #e6f4f1 100%);
      color: #1a3c34;
    }

    .hero-bg {
      background: url('https://images.unsplash.com/photo-1518791841217-8f162f1e1131?ixlib=rb-4.0.3&auto=format&fit=crop&w=1920&q=80') no-repeat center center;
      background-size: cover;
      position: relative;
      overflow: hidden;
    }

    .hero-bg::before {
      content: '';
      position: absolute;
      top: 0;
      left: 0;
      right: 0;
      bottom: 0;
      background: linear-gradient(to bottom, rgba(220, 38, 38, 0.6), rgba(13, 148, 136, 0.4));
      z-index: 1;
    }

    .spanish-moroccan-pattern {
      background: repeating-conic-gradient(#d69e2e 0% 25%, #f59e0b 25% 50%);
      opacity: 0.15;
    }

    .border-spanish-moroccan {
      border: 2px solid #d69e2e;
      border-radius: 20px;
      box-shadow: 0 6px 12px rgba(0, 0, 0, 0.15);
    }

    .button-primary {
      background: linear-gradient(to right, #dc2626, #f59e0b);
      color: white;
      transition: transform 0.2s, box-shadow 0.2s;
    }

    .button-primary:hover {
      transform: translateY(-3px);
      box-shadow: 0 6px 12px rgba(0, 0, 0, 0.2);
    }

    .button-secondary {
      background: linear-gradient(to right, #0d9488, #34d399);
      color: white;
      transition: transform 0.2s, box-shadow 0.2s;
    }

    .button-secondary:hover {
      transform: translateY(-3px);
      box-shadow: 0 6px 12px rgba(0, 0, 0, 0.2);
    }

    .card {
      transition: transform 0.3s, box-shadow 0.3s;
      border-radius: 20px;
    }

    .card:hover {
      transform: translateY(-8px);
      box-shadow: 0 10px 20px rgba(0, 0, 0, 0.2);
    }

    img {
      display: block;
      object-fit: cover;
      border-radius: 10px;
    }

    nav {
      background: rgba(255, 255, 255, 0.9);
      backdrop-filter: blur(10px);
    }

    nav a {
      transition: color 0.3s, border-bottom 0.3s;
    }

    nav a:hover,
    nav a.active {
      color: #dc2626;
      border-bottom: 3px solid #dc2626;
    }

    h1,
    h2,
    h3,
    h4 {
      font-family: 'Cinzel', serif;
    }

    button,
    input {
      font-family: 'Poppins', sans-serif;
    }

    .app-container {
      min-height: 100vh;
      display: flex;
      flex-direction: column;
    }

    main {
      flex: 1;
    }

    @keyframes fadeInUp {
      from {
        opacity: 0;
        transform: translateY(30px);
      }

      to {
        opacity: 1;
        transform: translateY(0);
      }
    }

    .animate-fade-in {
      animation: fadeInUp 0.6s ease-out forwards;
    }

    /* Scroll-triggered animation */
    .scroll-animate {
      opacity: 0;
      transform: translateY(30px);
      transition: opacity 0.6s ease-out, transform 0.6s ease-out;
    }

    .scroll-animate.visible {
      opacity: 1;
      transform: translateY(0);
    }
  </style>
</head>

<body class="app-container">
  <noscript>
    <div class="max-w-5xl mx-auto p-6 text-center">
      <h1 style="color: #1a3c34; font-size: 2rem;">Welcome to Spanish Learning Hub</h1>
      <p>Please enable JavaScript to access interactive A1 and A2 courses, games, and exercises.</p>
    </div>
  </noscript>
  <div id="root" class="max-w-6xl mx-auto p-4 md:p-8"></div>
  <script type="text/babel">
    const { useState, useEffect } = React;

        // Course Data with Unsplash Images
        const courses = {
            A1: [
                {
                    id: 1,
                    title: "Greetings and Introductions",
                    description: "Master greetings and self-introductions in Spanish.",
                    grammar: "Verb 'ser', personal pronouns (yo, tú, él/ella)",
                    vocabulary: ["hola", "adiós", "me llamo", "soy", "gracias"],
                    image: "https://images.unsplash.com/photo-1516321497487-e288fb19713f?ixlib=rb-4.0.3&auto=format&fit=crop&w=120&q=80",
                    progress: 0,
                    exercises: [
                        { id: "1a", type: "fill-in-blank", question: "Yo ___ (ser) estudiante.", options: ["soy", "es"], correct: "soy" },
                        { id: "1b", type: "multiple-choice", question: "Para decir 'gracias', usas:", options: ["hola", "gracias", "adiós"], correct: "gracias" },
                    ],
                },
                {
                    id: 2,
                    title: "Numbers and Time",
                    description: "Learn to count and tell time.",
                    grammar: "Numbers, verb 'ser' for time (es la una, son las dos)",
                    vocabulary: ["uno", "dos", "hora", "media", "cuarto"],
                    image: "https://images.unsplash.com/photo-1501139083538-0139583c0608?ixlib=rb-4.0.3&auto=format&fit=crop&w=120&q=80",
                    progress: 0,
                    exercises: [
                        { id: "2a", type: "fill-in-blank", question: "Son las ___ de la mañana.", options: ["dos", "doce"], correct: "dos" },
                        { id: "2b", type: "multiple-choice", question: "¿Cuánto es 10 + 5?", options: ["diez", "quince", "cinco"], correct: "quince" },
                    ],
                },
                {
                    id: 3,
                    title: "Family and Friends",
                    description: "Talk about family and relationships.",
                    grammar: "Possessive adjectives (mi, tu), verb 'tener'",
                    vocabulary: ["madre", "padre", "hermano", "amigo", "abuelo"],
                    image: "https://images.unsplash.com/photo-1517487881594-2787fef5ebf7?ixlib=rb-4.0.3&auto=format&fit=crop&w=120&q=80",
                    progress: 0,
                    exercises: [
                        { id: "3a", type: "fill-in-blank", question: "Yo ___ (tener) un hermano.", options: ["tengo", "tienes"], correct: "tengo" },
                        { id: "3b", type: "multiple-choice", question: "Mi ___ es alta.", options: ["madre", "padre", "amigo"], correct: "madre" },
                    ],
                },
                {
                    id: 4,
                    title: "Food and Drinks",
                    description: "Order food and describe flavors.",
                    grammar: "Articles (el, la), verb 'querer'",
                    vocabulary: ["pan", "agua", "café", "delicioso", "fruta"],
                    image: "https://images.unsplash.com/photo-1515003197210-e0cd71810b5f?ixlib=rb-4.0.3&auto=format&fit=crop&w=120&q=80",
                    progress: 0,
                    exercises: [
                        { id: "4a", type: "fill-in-blank", question: "Quiero ___ café.", options: ["el", "la"], correct: "el" },
                        { id: "4b", type: "multiple-choice", question: "La fruta es ___.", options: ["delicioso", "agua", "pan"], correct: "delicioso" },
                    ],
                },
                {
                    id: 5,
                    title: "Directions",
                    description: "Ask for and give directions.",
                    grammar: "Prepositions of place (a la izquierda, cerca), verb 'estar'",
                    vocabulary: ["izquierda", "derecha", "cerca", "lejos", "calle"],
                    image: "https://images.unsplash.com/photo-1532453288672-3a823f7d9ac8?ixlib=rb-4.0.3&auto=format&fit=crop&w=120&q=80",
                    progress: 0,
                    exercises: [
                        { id: "5a", type: "fill-in-blank", question: "La tienda está ___ (cerca/lejos).", options: ["cerca", "lejos"], correct: "cerca" },
                        { id: "5b", type: "multiple-choice", question: "Gira a la ___.", options: ["izquierda", "calle", "lejos"], correct: "izquierda" },
                    ],
                },
                {
                    id: 6,
                    title: "Colors",
                    description: "Learn colors and describe objects.",
                    grammar: "Adjectives, agreement (rojo, roja)",
                    vocabulary: ["rojo", "azul", "verde", "amarillo", "blanco"],
                    image: "https://images.unsplash.com/photo-1517086849388-2e7800547c7f?ixlib=rb-4.0.3&auto=format&fit=crop&w=120&q=80",
                    progress: 0,
                    exercises: [
                        { id: "6a", type: "fill-in-blank", question: "El cielo es ___ (color).", options: ["azul", "rojo"], correct: "azul" },
                        { id: "6b", type: "multiple-choice", question: "La bandera es ___ y amarilla.", options: ["rojo", "verde", "blanco"], correct: "rojo" },
                    ],
                },
                {
                    id: 7,
                    title: "Clothing",
                    description: "Talk about clothes and shopping.",
                    grammar: "Verb 'llevar', demonstratives (este, esta)",
                    vocabulary: ["camisa", "pantalones", "zapatos", "vestido", "sombrero"],
                    image: "https://images.unsplash.com/photo-1521335625578-3a0e31d31b9f?ixlib=rb-4.0.3&auto=format&fit=crop&w=120&q=80",
                    progress: 0,
                    exercises: [
                        { id: "7a", type: "fill-in-blank", question: "Yo ___ (llevar) una camisa.", options: ["llevo", "llevas"], correct: "llevo" },
                        { id: "7b", type: "multiple-choice", question: "Este ___ es bonito.", options: ["vestido", "pantalones", "zapatos"], correct: "vestido" },
                    ],
                },
                {
                    id: 8,
                    title: "Weather",
                    description: "Describe the weather and seasons.",
                    grammar: "Verb 'hacer', expressions (hace sol, hace frío)",
                    vocabulary: ["sol", "lluvia", "frío", "calor", "nubes"],
                    image: "https://images.unsplash.com/photo-1503437313881-503a91226402?ixlib=rb-4.0.3&auto=format&fit=crop&w=120&q=80",
                    progress: 0,
                    exercises: [
                        { id: "8a", type: "fill-in-blank", question: "Hoy ___ (hacer) calor.", options: ["hace", "hago"], correct: "hace" },
                        { id: "8b", type: "multiple-choice", question: "Cuando hay nubes, puede haber ___.", options: ["lluvia", "sol", "calor"], correct: "lluvia" },
                    ],
                },
            ],
            A2: [
                {
                    id: 9,
                    title: "Daily Routines",
                    description: "Describe your daily activities.",
                    grammar: "Reflexive verbs (levantarse, ducharse), present tense",
                    vocabulary: ["levantarse", "desayunar", "trabajar", "dormir", "cepillarse"],
                    image: "https://images.unsplash.com/photo-1507525428034-b723cf961d3e?ixlib=rb-4.0.3&auto=format&fit=crop&w=120&q=80",
                    progress: 0,
                    exercises: [
                        { id: "9a", type: "fill-in-blank", question: "Ella ___ (levantarse) a las siete.", options: ["se levanta", "levanta"], correct: "se levanta" },
                        { id: "9b", type: "multiple-choice", question: "Me ___ los dientes.", options: ["cepillo", "desayuno", "duermo"], correct: "cepillo" },
                    ],
                },
                {
                    id: 10,
                    title: "Past Experiences",
                    description: "Talk about past events.",
                    grammar: "Pretérito perfecto (he comido, has ido), irregular verbs",
                    vocabulary: ["he ido", "has comido", "ayer", "semana", "viaje"],
                    image: "https://images.unsplash.com/photo-1506748686214-e9df14d4d9d0?ixlib=rb-4.0.3&auto=format&fit=crop&w=120&q=80",
                    progress: 0,
                    exercises: [
                        { id: "10a", type: "fill-in-blank", question: "Yo ___ (comprar) un libro.", options: ["he comprado", "has comprado"], correct: "he comprado" },
                        { id: "10b", type: "multiple-choice", question: "La ___ pasada fui al cine.", options: ["semana", "ayer", "viaje"], correct: "semana" },
                    ],
                },
                {
                    id: 11,
                    title: "Shopping",
                    description: "Learn to shop and bargain.",
                    grammar: "Direct object pronouns (lo, la)",
                    vocabulary: ["comprar", "tienda", "precio", "descuento", "bolsa"],
                    image: "https://images.unsplash.com/photo-1511556820780-d912e42b4980?ixlib=rb-4.0.3&auto=format&fit=crop&w=120&q=80",
                    progress: 0,
                    exercises: [
                        { id: "11a", type: "fill-in-blank", question: "Yo ___ (comprar) la camisa.", options: ["la compro", "lo compro"], correct: "la compro" },
                        { id: "11b", type: "multiple-choice", question: "Quiero un ___ en el precio.", options: ["descuento", "bolsa", "tienda"], correct: "descuento" },
                    ],
                },
                {
                    id: 12,
                    title: "Travel and Directions",
                    description: "Plan a trip and navigate.",
                    grammar: "Indirect object pronouns (me, te), verb 'ir'",
                    vocabulary: ["viaje", "boleto", "estación", "mapa", "avión"],
                    image: "https://images.unsplash.com/photo-1476514525535-07fb3b4ae5f1?ixlib=rb-4.0.3&auto=format&fit=crop&w=120&q=80",
                    progress: 0,
                    exercises: [
                        { id: "12a", type: "fill-in-blank", question: "___ (ir) a la estación.", options: ["Voy", "Vas"], correct: "Voy" },
                        { id: "12b", type: "multiple-choice", question: "Necesito un ___ para el tren.", options: ["boleto", "mapa", "avión"], correct: "boleto" },
                    ],
                },
                {
                    id: 13,
                    title: "Hobbies and Likes",
                    description: "Express preferences and hobbies.",
                    grammar: "Verb 'gustar', adverbs (mucho, poco)",
                    vocabulary: ["bailar", "leer", "me gusta", "cantar", "deporte"],
                    image: "https://images.unsplash.com/photo-1519125323398-675f0ddb6308?ixlib=rb-4.0.3&auto=format&fit=crop&w=120&q=80",
                    progress: 0,
                    exercises: [
                        { id: "13a", type: "fill-in-blank", question: "A mí ___ (gustar) bailar.", options: ["me gusta", "te gusta"], correct: "me gusta" },
                        { id: "13b", type: "multiple-choice", question: "Juego al ___ los fines de semana.", options: ["deporte", "cantar", "leer"], correct: "deporte" },
                    ],
                },
                {
                    id: 14,
                    title: "Emotions",
                    description: "Express feelings and emotions.",
                    grammar: "Verb 'sentir', adjectives",
                    vocabulary: ["feliz", "triste", "enojado", "cansado", "emocionado"],
                    image: "https://images.unsplash.com/photo-1529333166437-7750a6dd5a70?ixlib=rb-4.0.3&auto=format&fit=crop&w=120&q=80",
                    progress: 0,
                    exercises: [
                        { id: "14a", type: "fill-in-blank", question: "Yo ___ (sentir) feliz.", options: ["me siento", "te sientes"], correct: "me siento" },
                        { id: "14b", type: "multiple-choice", question: "Estoy muy ___ después del trabajo.", options: ["cansado", "feliz", "enojado"], correct: "cansado" },
                    ],
                },
                {
                    id: 15,
                    title: "Technology",
                    description: "Talk about technology and devices.",
                    grammar: "Verb 'usar', nouns",
                    vocabulary: ["computadora", "teléfono", "internet", "correo", "aplicación"],
                    image: "https://images.unsplash.com/photo-1516321318423-f06f85e504b3?ixlib=rb-4.0.3&auto=format&fit=crop&w=120&q=80",
                    progress: 0,
                    exercises: [
                        { id: "15a", type: "fill-in-blank", question: "Yo ___ (usar) la computadora.", options: ["uso", "usas"], correct: "uso" },
                        { id: "15b", type: "multiple-choice", question: "Envío un ___ electrónico.", options: ["correo", "teléfono", "internet"], correct: "correo" },
                    ],
                },
                {
                    id: 16,
                    title: "Dining Out",
                    description: "Order food in a restaurant.",
                    grammar: "Verb 'pedir', formal commands",
                    vocabulary: ["menú", "cuenta", "plato", "mesa", "propina"],
                    image: "https://images.unsplash.com/photo-1517248135467-4c7edcad34c4?ixlib=rb-4.0.3&auto=format&fit=crop&w=120&q=80",
                    progress: 0,
                    exercises: [
                        { id: "16a", type: "fill-in-blank", question: "Yo ___ (pedir) la cuenta.", options: ["pido", "pides"], correct: "pido" },
                        { id: "16b", type: "multiple-choice", question: "Quiero una ___ para dos personas.", options: ["mesa", "plato", "propina"], correct: "mesa" },
                    ],
                },
            ],
        };

        // General Exercises
        const generalExercises = [
            { id: "g1", level: "A1", type: "fill-in-blank", question: "Tú ___ (ser) de España.", options: ["eres", "es"], correct: "eres" },
            { id: "g2", level: "A1", type: "multiple-choice", question: "La casa es ___.", options: ["grande", "pequeño", "lejos"], correct: "grande" },
            { id: "g3", level: "A1", type: "fill-in-blank", question: "Quiero ___ (beber) agua.", options: ["beber", "bebo"], correct: "beber" },
            { id: "g4", level: "A1", type: "multiple-choice", question: "¿Dónde está el ___?", options: ["sol", "luna", "cielo"], correct: "sol" },
            { id: "g5", level: "A2", type: "fill-in-blank", question: "Nosotros ___ (haber) viajado a México.", options: ["hemos", "has"], correct: "hemos" },
            { id: "g6", level: "A2", type: "multiple-choice", question: "Me gusta ___ mucho.", options: ["cantar", "canta", "cantas"], correct: "cantar" },
            { id: "g7", level: "A2", type: "fill-in-blank", question: "Ella ___ (comprar) un boleto.", options: ["lo compra", "la compra"], correct: "lo compra" },
            { id: "g8", level: "A2", type: "multiple-choice", question: "Uso mi ___ para trabajar.", options: ["computadora", "correo", "aplicación"], correct: "computadora" },
        ];

        // Game Data
        const gameWords = [
            { word: "sol", translation: "sun", image: "https://images.unsplash.com/photo-1504384308090-c894fdcc538d?ixlib=rb-4.0.3&auto=format&fit=crop&w=120&q=80" },
            { word: "casa", translation: "house", image: "https://images.unsplash.com/photo-1518780664697-55e3ad937233?ixlib=rb-4.0.3&auto=format&fit=crop&w=120&q=80" },
            { word: "árbol", translation: "tree", image: "https://images.unsplash.com/photo-1446329813274-7c9036bd9a1f?ixlib=rb-4.0.3&auto=format&fit=crop&w=120&q=80" },
            { word: "libro", translation: "book", image: "https://images.unsplash.com/photo-1544947950-fa07a98d237f?ixlib=rb-4.0.3&auto=format&fit=crop&w=120&q=80" },
            { word: "flor", translation: "flower", image: "https://images.unsplash.com/photo-1460039230329-eb070fc6c77c?ixlib=rb-4.0.3&auto=format&fit=crop&w=120&q=80" },
        ];

        // Translation Quiz Game Data
        const quizQuestions = [
            { question: "¿Qué significa 'luna' en inglés?", options: ["moon", "sun", "star"], correct: "moon" },
            { question: "¿Cómo se dice 'water' en español?", options: ["agua", "sol", "casa"], correct: "agua" },
            { question: "¿Qué es 'comer'?", options: ["to eat", "to drink", "to sleep"], correct: "to eat" },
            { question: "¿Cómo se dice 'red' en español?", options: ["rojo", "azul", "verde"], correct: "rojo" },
        ];

        // Lesson Detail Component
        function LessonDetail({ lesson, level, onBack, onComplete }) {
            const [selectedExercise, setSelectedExercise] = useState(null);
            const [userAnswer, setUserAnswer] = useState("");
            const [feedback, setFeedback] = useState("");

            const handleExerciseSubmit = (exercise) => {
                if (!userAnswer) {
                    setFeedback("Por favor, selecciona una respuesta.");
                    return;
                }
                setSelectedExercise(exercise.id);
                if (userAnswer === exercise.correct) {
                    setFeedback("¡Correcto! Bien hecho.");
                } else {
                    setFeedback(`Incorrecto. La respuesta correcta es "${exercise.correct}".`);
                }
            };

            return (
                <div className="p-6 md:p-8 bg-white border-spanish-moroccan rounded-lg animate-fade-in">
                    <button
                        className="mb-4 px-4 py-2 button-primary rounded-lg"
                        onClick={onBack}
                        aria-label="Volver a la página de cursos"
                    >
                        Volver
                    </button>
                    <h2 className="text-3xl md:text-4xl font-bold text-[#dc2626] mb-4">{lesson.title}</h2>
                    <img
                        src={lesson.image}
                        alt={lesson.title}
                        className="w-32 h-32 md:w-40 md:h-40 mx-auto mb-6"
                        onError={(e) => (e.target.src = "https://via.placeholder.com/120?text=Fallback")}
                    />
                    <p className="text-gray-700 mb-6 text-lg">{lesson.description}</p>
                    <h3 className="text-xl font-semibold text-[#0d9488] mb-2">Gramática</h3>
                    <p className="text-gray-700 mb-6">{lesson.grammar}</p>
                    <h3 className="text-xl font-semibold text-[#0d9488] mb-2">Vocabulario</h3>
                    <ul className="list-disc list-inside text-gray-700 mb-6">
                        {lesson.vocabulary.map((word, index) => (
                            <li key={index}>{word}</li>
                        ))}
                    </ul>
                    <h3 className="text-xl font-semibold text-[#0d9488] mb-4">Ejercicios</h3>
                    {lesson.exercises.map((exercise) => (
                        <div key={exercise.id} className="mb-6 bg-gray-50 p-4 rounded-lg">
                            <p className="text-gray-700 mb-2">{exercise.question}</p>
                            {exercise.type === "fill-in-blank" ? (
                                <div className="mt-2">
                                    <input
                                        type="text"
                                        value={userAnswer}
                                        onChange={(e) => setUserAnswer(e.target.value)}
                                        placeholder="Escribe tu respuesta"
                                        className="px-4 py-2 border border-gray-300 rounded-lg w-full focus:ring-2 focus:ring-[#dc2626]"
                                        aria-label={`Respuesta para ${exercise.question}`}
                                    />
                                </div>
                            ) : (
                                <div className="mt-2 space-y-2">
                                    {exercise.options.map((option) => (
                                        <button
                                            key={option}
                                            className={`px-4 py-2 w-full text-left rounded-lg ${
                                                userAnswer === option
                                                    ? "bg-[#0d9488] text-white"
                                                    : "bg-gray-100 text-gray-700 hover:bg-gray-200"
                                            }`}
                                            onClick={() => setUserAnswer(option)}
                                            aria-label={`Opción ${option}`}
                                        >
                                            {option}
                                        </button>
                                    ))}
                                </div>
                            )}
                            <button
                                className="mt-4 px-4 py-2 button-secondary rounded-lg"
                                onClick={() => handleExerciseSubmit(exercise)}
                                aria-label="Enviar respuesta"
                            >
                                Enviar
                            </button>
                            {feedback && selectedExercise === exercise.id && (
                                <p className="mt-2 text-sm text-gray-600">{feedback}</p>
                            )}
                        </div>
                    ))}
                    <button
                        className="mt-6 px-6 py-3 button-primary rounded-lg w-full text-lg"
                        onClick={() => onComplete(level, lesson.id)}
                        aria-label="Completar lección"
                    >
                        Completar Lección
                    </button>
                </div>
            );
        }

        // Main App Component
        function App() {
            const [currentPage, setCurrentPage] = useState("home");
            const [selectedLesson, setSelectedLesson] = useState(null);
            const [selectedLevel, setSelectedLevel] = useState(null);
            const [selectedExercise, setSelectedExercise] = useState(null);
            const [userAnswer, setUserAnswer] = useState("");
            const [feedback, setFeedback] = useState("");
            const [gameScore, setGameScore] = useState(0);
            const [quizScore, setQuizScore] = useState(0);
            const [selectedWord, setSelectedWord] = useState(null);
            const [courseProgress, setCourseProgress] = useState(courses);

            // Scroll animation handler
            useEffect(() => {
                const elements = document.querySelectorAll('.scroll-animate');
                const observer = new IntersectionObserver(
                    (entries) => {
                        entries.forEach((entry) => {
                            if (entry.isIntersecting) {
                                entry.target.classList.add('visible');
                            }
                        });
                    },
                    { threshold: 0.1 }
                );
                elements.forEach((el) => observer.observe(el));
                return () => elements.forEach((el) => observer.unobserve(el));
            }, [currentPage]);

            // Handle navigation
            const navigateTo = (page) => {
                setCurrentPage(page);
                setSelectedLesson(null);
                setSelectedLevel(null);
                setSelectedExercise(null);
                setUserAnswer("");
                setFeedback("");
                window.scrollTo(0, 0);
            };

            // Handle lesson selection
            const handleLessonSelect = (level, lesson) => {
                setSelectedLevel(level);
                setSelectedLesson(lesson);
                setCurrentPage("lesson");
            };

            // Handle lesson completion
            const handleLessonComplete = (level, lessonId) => {
                setCourseProgress((prev) => ({
                    ...prev,
                    [level]: prev[level].map((lesson) =>
                        lesson.id === lessonId ? { ...lesson, progress: 100 } : lesson
                    ),
                }));
                alert(`¡Lección "${courses[level].find(l => l.id === lessonId).title}" completada!`);
                navigateTo("courses");
            };

            // Handle exercise submission
            const handleExerciseSubmit = (exercise) => {
                if (!userAnswer) {
                    setFeedback("Por favor, selecciona una respuesta.");
                    return;
                }
                setSelectedExercise(exercise.id);
                if (userAnswer === exercise.correct) {
                    setFeedback("¡Correcto! Bien hecho.");
                } else {
                    setFeedback(`Incorrecto. La respuesta correcta es "${exercise.correct}".`);
                }
            };

            // Handle game matching
            const handleGameMatch = (word, translation) => {
                if (word.translation === translation) {
                    setGameScore(gameScore + 1);
                    setFeedback("¡Correcto! +1 punto.");
                } else {
                    setFeedback("Incorrecto. Intenta de nuevo.");
                }
                setSelectedWord(null);
            };

            // Handle quiz answer
            const handleQuizAnswer = (question, answer) => {
                if (answer === question.correct) {
                    setQuizScore(quizScore + 1);
                    setFeedback("¡Correcto! +1 punto.");
                } else {
                    setFeedback(`Incorrecto. La respuesta correcta es "${question.correct}".`);
                }
            };

            // Render subpages
            const renderPage = () => {
                if (currentPage === "lesson" && selectedLesson && selectedLevel) {
                    return (
                        <LessonDetail
                            lesson={selectedLesson}
                            level={selectedLevel}
                            onBack={() => navigateTo("courses")}
                            onComplete={handleLessonComplete}
                        />
                    );
                }

                switch (currentPage) {
                    case "home":
                        return (
                            <div>
                                <section className="hero-bg py-24 md:py-32 text-center text-white relative mb-12">
                                    <div className="relative z-10 max-w-4xl mx-auto">
                                        <h1 className="text-5xl md:text-6xl font-bold mb-4">Spanish Learning Hub</h1>
                                        <p className="text-xl md:text-2xl mb-8">
                                            Embark on a vibrant journey to master Spanish with A1 and A2 courses, games, and exercises.
                                        </p>
                                        <button
                                            className="px-6 py-3 button-primary rounded-lg text-lg"
                                            onClick={() => navigateTo("courses")}
                                            aria-label="Empezar a aprender ahora"
                                        >
                                            ¡Empezar Ahora!
                                        </button>
                                    </div>
                                    <div className="h-2 w-64 mx-auto mt-8 spanish-moroccan-pattern"></div>
                                </section>
                                <section className="grid grid-cols-1 md:grid-cols-3 gap-6 scroll-animate">
                                    <div className="p-6 bg-white border-spanish-moroccan text-center card">
                                        <h3 className="text-2xl font-semibold text-[#0d9488] mb-2">Cursos</h3>
                                        <p className="text-gray-700 mb-4">Dive into A1 and A2 lessons to build fluency.</p>
                                        <button
                                            className="px-4 py-2 button-primary rounded-lg"
                                            onClick={() => navigateTo("courses")}
                                            aria-label="Ver cursos"
                                        >
                                            Ver Cursos
                                        </button>
                                    </div>
                                    <div className="p-6 bg-white border-spanish-moroccan text-center card">
                                        <h3 className="text-2xl font-semibold text-[#0d9488] mb-2">Ejercicios</h3>
                                        <p className="text-gray-700 mb-4">Sharpen your skills with interactive exercises.</p>
                                        <button
                                            className="px-4 py-2 button-primary rounded-lg"
                                            onClick={() => navigateTo("exercises")}
                                            aria-label="Practicar ejercicios"
                                        >
                                            Practicar Ahora
                                        </button>
                                    </div>
                                    <div className="p-6 bg-white border-spanish-moroccan text-center card">
                                        <h3 className="text-2xl font-semibold text-[#0d9488] mb-2">Juegos</h3>
                                        <p className="text-gray-700 mb-4">Have fun with games to boost your learning.</p>
                                        <button
                                            className="px-4 py-2 button-primary rounded-lg"
                                            onClick={() => navigateTo("games")}
                                            aria-label="Jugar ahora"
                                        >
                                            Jugar Ahora
                                        </button>
                                    </div>
                                </section>
                            </div>
                        );
                    case "courses":
                        return (
                            <div className="scroll-animate">
                                <h2 className="text-4xl font-bold text-[#dc2626] mb-8 text-center">Cursos</h2>
                                <section className="mb-12">
                                    <h3 className="text-2xl font-semibold text-[#0d9488] mb-4">Nivel A1: Principiante</h3>
                                    {courseProgress.A1.length === 0 ? (
                                        <p className="text-gray-700">No hay lecciones disponibles.</p>
                                    ) : (
                                        <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
                                            {courseProgress.A1.map((lesson) => (
                                                <div
                                                    key={lesson.id}
                                                    className="p-6 bg-white border-spanish-moroccan rounded-lg card cursor-pointer"
                                                    onClick={() => handleLessonSelect("A1", lesson)}
                                                    role="button"
                                                    tabIndex={0}
                                                    onKeyDown={(e) => e.key === 'Enter' && handleLessonSelect("A1", lesson)}
                                                    aria-label={`Abrir lección ${lesson.title}`}
                                                >
                                                    <img
                                                        src={lesson.image}
                                                        alt={lesson.title}
                                                        className="w-28 h-28 mx-auto mb-4"
                                                        onError={(e) => (e.target.src = "https://via.placeholder.com/120?text=Fallback")}
                                                    />
                                                    <h4 className="text-xl font-bold text-[#0d9488] mb-2">{lesson.title}</h4>
                                                    <p className="text-gray-700 mb-2">{lesson.description}</p>
                                                    <p className="text-sm text-gray-600"><strong>Gramática:</strong> {lesson.grammar}</p>
                                                    <p className="text-sm text-gray-600"><strong>Vocabulario:</strong> {lesson.vocabulary.join(", ")}</p>
                                                    <div className="w-full bg-gray-200 rounded-full h-2.5 mt-2">
                                                        <div
                                                            className="bg-[#dc2626] h-2.5 rounded-full"
                                                            style={{ width: `${lesson.progress}%` }}
                                                        ></div>
                                                    </div>
                                                    <p className="text-sm text-gray-500 mt-1">{lesson.progress}% Completado</p>
                                                </div>
                                            ))}
                                        </div>
                                    )}
                                </section>
                                <section>
                                    <h3 className="text-2xl font-semibold text-[#0d9488] mb-4">Nivel A2: Elemental</h3>
                                    {courseProgress.A2.length === 0 ? (
                                        <p className="text-gray-700">No hay lecciones disponibles.</p>
                                    ) : (
                                        <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
                                            {courseProgress.A2.map((lesson) => (
                                                <div
                                                    key={lesson.id}
                                                    className="p-6 bg-white border-spanish-moroccan rounded-lg card cursor-pointer"
                                                    onClick={() => handleLessonSelect("A2", lesson)}
                                                    role="button"
                                                    tabIndex={0}
                                                    onKeyDown={(e) => e.key === 'Enter' && handleLessonSelect("A2", lesson)}
                                                    aria-label={`Abrir lección ${lesson.title}`}
                                                >
                                                    <img
                                                        src={lesson.image}
                                                        alt={lesson.title}
                                                        className="w-28 h-28 mx-auto mb-4"
                                                        onError={(e) => (e.target.src = "https://via.placeholder.com/120?text=Fallback")}
                                                    />
                                                    <h4 className="text-xl font-bold text-[#0d9488] mb-2">{lesson.title}</h4>
                                                    <p className="text-gray-700 mb-2">{lesson.description}</p>
                                                    <p className="text-sm text-gray-600"><strong>Gramática:</strong> {lesson.grammar}</p>
                                                    <p className="text-sm text-gray-600"><strong>Vocabulario:</strong> {lesson.vocabulary.join(", ")}</p>
                                                    <div className="w-full bg-gray-200 rounded-full h-2.5 mt-2">
                                                        <div
                                                            className="bg-[#dc2626] h-2.5 rounded-full"
                                                            style={{ width: `${lesson.progress}%` }}
                                                        ></div>
                                                    </div>
                                                    <p className="text-sm text-gray-500 mt-1">{lesson.progress}% Completado</p>
                                                </div>
                                            ))}
                                        </div>
                                    )}
                                </section>
                            </div>
                        );
                    case "exercises":
                        return (
                            <div className="scroll-animate">
                                <h2 className="text-4xl font-bold text-[#dc2626] mb-8 text-center">Ejercicios</h2>
                                {generalExercises.length === 0 ? (
                                    <p className="text-gray-700">No hay ejercicios disponibles.</p>
                                ) : (
                                    <div className="space-y-6">
                                        {generalExercises.map((exercise) => (
                                            <div
                                                key={exercise.id}
                                                className="p-6 bg-white border-spanish-moroccan rounded-lg card"
                                            >
                                                <h3 className="text-lg font-semibold text-[#0d9488] mb-2">{exercise.question} ({exercise.level})</h3>
                                                {exercise.type === "fill-in-blank" ? (
                                                    <div className="mt-4">
                                                        <input
                                                            type="text"
                                                            value={userAnswer}
                                                            onChange={(e) => setUserAnswer(e.target.value)}
                                                            placeholder="Escribe tu respuesta"
                                                            className="px-4 py-2 border border-gray-300 rounded-lg w-full focus:ring-2 focus:ring-[#dc2626]"
                                                            aria-label={`Respuesta para ${exercise.question}`}
                                                        />
                                                    </div>
                                                ) : (
                                                    <div className="mt-4 space-y-2">
                                                        {exercise.options.map((option) => (
                                                            <button
                                                                key={option}
                                                                className={`px-4 py-2 w-full text-left rounded-lg ${
                                                                    userAnswer === option
                                                                        ? "bg-[#0d9488] text-white"
                                                                        : "bg-gray-100 text-gray-700 hover:bg-gray-200"
                                                                }`}
                                                                onClick={() => setUserAnswer(option)}
                                                                aria-label={`Opción ${option}`}
                                                            >
                                                                {option}
                                                            </button>
                                                        ))}
                                                    </div>
                                                )}
                                                <button
                                                    className="mt-4 px-4 py-2 button-secondary rounded-lg"
                                                    onClick={() => handleExerciseSubmit(exercise)}
                                                    aria-label="Enviar respuesta"
                                                >
                                                    Enviar
                                                </button>
                                                {feedback && selectedExercise === exercise.id && (
                                                    <p className="mt-4 text-sm text-gray-600">{feedback}</p>
                                                )}
                                            </div>
                                        ))}
                                    </div>
                                )}
                            </div>
                        );
                    case "games":
                        return (
                            <div className="scroll-animate">
                                <h2 className="text-4xl font-bold text-[#dc2626] mb-8 text-center">Juegos</h2>
                                <section className="mb-12">
                                    <h3 className="text-2xl font-semibold text-[#0d9488] mb-4">Juego de Emparejar Palabras</h3>
                                    <div className="p-6 bg-white border-spanish-moroccan rounded-lg card">
                                        <p className="text-gray-700 mb-4">Empareja palabras en español con sus traducciones. Puntuación: {gameScore}</p>
                                        <div className="grid grid-cols-2 md:grid-cols-3 gap-4">
                                            {gameWords.map((word) => (
                                                <div key={word.word} className="text-center">
                                                    <img
                                                        src={word.image}
                                                        alt={word.word}
                                                        className="w-24 h-24 mx-auto mb-2"
                                                        onError={(e) => (e.target.src = "https://via.placeholder.com/120?text=Fallback")}
                                                    />
                                                    <button
                                                        className="px-4 py-2 button-primary rounded-lg"
                                                        onClick={() => setSelectedWord(word)}
                                                        aria-label={`Seleccionar palabra ${word.word}`}
                                                    >
                                                        {word.word}
                                                    </button>
                                                </div>
                                            ))}
                                        </div>
                                        {selectedWord && (
                                            <div className="mt-4">
                                                <p className="text-gray-700">Empareja "{selectedWord.word}" con:</p>
                                                {["sun", "house", "tree", "book", "flower"].map((option) => (
                                                    <button
                                                        key={option}
                                                        className="px-4 py-2 button-secondary rounded-lg mr-2 mt-2"
                                                        onClick={() => handleGameMatch(selectedWord, option)}
                                                        aria-label={`Emparejar con ${option}`}
                                                    >
                                                        {option}
                                                    </button>
                                                ))}
                                            </div>
                                        )}
                                        {feedback && !selectedExercise && <p className="mt-4 text-sm text-gray-600">{feedback}</p>}
                                    </div>
                                </section>
                                <section>
                                    <h3 className="text-2xl font-semibold text-[#0d9488] mb-4">Cuestionario de Traducción</h3>
                                    <div className="p-6 bg-white border-spanish-moroccan rounded-lg card">
                                        <p className="text-gray-700 mb-4">Responde las preguntas de traducción. Puntuación: {quizScore}</p>
                                        {quizQuestions.map((question, index) => (
                                            <div key={index} className="mb-6">
                                                <p className="text-gray-700">{question.question}</p>
                                                <div className="mt-2 space-y-2">
                                                    {question.options.map((option) => (
                                                        <button
                                                            key={option}
                                                            className="px-4 py-2 w-full text-left rounded-lg bg-gray-100 text-gray-700 hover:bg-gray-200"
                                                            onClick={() => handleQuizAnswer(question, option)}
                                                            aria-label={`Opción ${option}`}
                                                        >
                                                            {option}
                                                        </button>
                                                    ))}
                                                </div>
                                            </div>
                                        ))}
                                        {feedback && !selectedExercise && <p className="mt-4 text-sm text-gray-600">{feedback}</p>}
                                    </div>
                                </section>
                            </div>
                        );
                    default:
                        return <div className="text-center text-gray-700">Error: Página no encontrada</div>;
                }
            };

            return (
                <div>
                    {/* Navigation */}
                    <nav className="p-4 mb-8 sticky top-0 z-20 shadow-lg" aria-label="Navegación principal">
                        <ul className="flex justify-center space-x-6 text-lg font-semibold">
                            <li>
                                <a
                                    href="#"
                                    onClick={() => navigateTo("home")}
                                    className={`text-[#1a3c34] ${currentPage === "home" ? "active" : ""}`}
                                    aria-current={currentPage === "home" ? "page" : undefined}
                                >
                                    Inicio
                                </a>
                            </li>
                            <li>
                                <a
                                    href="#"
                                    onClick={() => navigateTo("courses")}
                                    className={`text-[#1a3c34] ${currentPage === "courses" ? "active" : ""}`}
                                    aria-current={currentPage === "courses" ? "page" : undefined}
                                >
                                    Cursos
                                </a>
                            </li>
                            <li>
                                <a
                                    href="#"
                                    onClick={() => navigateTo("exercises")}
                                    className={`text-[#1a3c34] ${currentPage === "exercises" ? "active" : ""}`}
                                    aria-current={currentPage === "exercises" ? "page" : undefined}
                                >
                                    Ejercicios
                                </a>
                            </li>
                            <li>
                                <a
                                    href="#"
                                    onClick={() => navigateTo("games")}
                                    className={`text-[#1a3c34] ${currentPage === "games" ? "active" : ""}`}
                                    aria-current={currentPage === "games" ? "page" : undefined}
                                >
                                    Juegos
                                </a>
                            </li>
                        </ul>
                    </nav>

                    {/* Main Content */}
                    <main>{renderPage()}</main>

                    {/* Footer */}
                    <footer className="text-center py-8 mt-12 bg-white border-spanish-moroccan">
                        <p className="text-gray-700">© 2025 Spanish Learning Hub. Learn Spanish with passion and style.</p>
                    </footer>
                </div>
            );
        }

        // Render the app
        try {
            ReactDOM.render(<App />, document.getElementById("root"));
        } catch (e) {
            document.getElementById("root").innerHTML = `
                <div class="text-center p-6">
                    <h1 style="color: #1a3c34;">Error Loading Content</h1>
                    <p>Please refresh the page or try again later.</p>
                </div>
            `;
        }
    </script>
</body>

</html>
