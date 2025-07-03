# Examen-adm
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Examen de Derecho Administrativo</title>
    <style>
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            line-height: 1.6;
            color: #333;
            max-width: 800px;
            margin: 0 auto;
            padding: 20px;
            background-color: #f5f5f5;
        }
        h1 {
            color: #2c3e50;
            text-align: center;
            margin-bottom: 30px;
            border-bottom: 2px solid #3498db;
            padding-bottom: 10px;
        }
        .quiz-container {
            background-color: white;
            padding: 25px;
            border-radius: 8px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
            margin-bottom: 30px;
        }
        .question {
            margin-bottom: 25px;
            padding-bottom: 15px;
            border-bottom: 1px solid #eee;
        }
        .question-text {
            font-weight: bold;
            margin-bottom: 15px;
            font-size: 18px;
        }
        .options {
            margin-left: 20px;
        }
        .option {
            margin-bottom: 10px;
        }
        .true-false {
            display: flex;
            gap: 20px;
        }
        .true-false button {
            padding: 8px 20px;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            font-weight: bold;
            transition: all 0.3s;
        }
        .true-false button:hover {
            opacity: 0.9;
        }
        .btn-true {
            background-color: #2ecc71;
            color: white;
        }
        .btn-false {
            background-color: #e74c3c;
            color: white;
        }
        .btn-submit {
            display: block;
            width: 100%;
            padding: 12px;
            background-color: #3498db;
            color: white;
            border: none;
            border-radius: 4px;
            font-size: 16px;
            cursor: pointer;
            margin-top: 20px;
            transition: background-color 0.3s;
        }
        .btn-submit:hover {
            background-color: #2980b9;
        }
        .result {
            text-align: center;
            font-size: 20px;
            font-weight: bold;
            margin-top: 20px;
            padding: 15px;
            border-radius: 4px;
            display: none;
        }
        .correct {
            background-color: #d4edda;
            color: #155724;
        }
        .incorrect {
            background-color: #f8d7da;
            color: #721c24;
        }
        .score {
            font-size: 24px;
            margin-top: 20px;
            text-align: center;
        }
        .explanation {
            margin-top: 10px;
            padding: 10px;
            background-color: #f8f9fa;
            border-left: 4px solid #3498db;
            display: none;
            font-size: 14px;
        }
        .progress {
            margin-bottom: 20px;
            text-align: right;
            font-style: italic;
            color: #7f8c8d;
        }
        @media (max-width: 600px) {
            body {
                padding: 10px;
            }
            .quiz-container {
                padding: 15px;
            }
            .question-text {
                font-size: 16px;
            }
        }
    </style>
</head>
<body>
    <h1>Examen de Derecho Administrativo</h1>
    
    <div class="quiz-container">
        <div class="progress">Pregunta <span id="current-question">1</span> de 60</div>
        
        <div id="quiz"></div>
        
        <button id="submit" class="btn-submit">Verificar respuesta</button>
        
        <div id="result" class="result"></div>
        <div id="explanation" class="explanation"></div>
        
        <div id="score" class="score"></div>
    </div>

    <script>
        // Banco de preguntas (60 preguntas)
        const questions = [
            // Preguntas de verdadero/falso
            {
                type: 'true-false',
                question: "El COA se divide en 5 libros según su estructura.",
                answer: true,
                explanation: "Correcto. El COA se divide efectivamente en 5 libros: Preliminar, I, II, III y IV."
            },
            {
                type: 'true-false',
                question: "El principio de legalidad en el derecho sancionador permite a la administración crear nuevas sanciones no previstas en la ley cuando lo considere necesario.",
                answer: false,
                explanation: "Incorrecto. El principio de legalidad establece que no se puede sancionar sin una norma previa que lo establezca."
            },
            {
                type: 'true-false',
                question: "El 'ius variandi' permite a la administración modificar unilateralmente contratos administrativos sin límites.",
                answer: false,
                explanation: "Incorrecto. El 'ius variandi' tiene límites como respetar la esencia del contrato y el equilibrio económico."
            },
            {
                type: 'true-false',
                question: "El artículo 42 COA regula 9 aspectos del ámbito material u objetivo del derecho administrativo.",
                answer: true,
                explanation: "Correcto. El art. 42 COA enumera 9 materias que regula el código."
            },
            {
                type: 'true-false',
                question: "La prescripción para infracciones administrativas muy graves es de 3 años según el COA.",
                answer: false,
                explanation: "Incorrecto. Para infracciones muy graves el plazo es de 5 años (art. 245 COA)."
            },
            {
                type: 'true-false',
                question: "Los ministerios en Ecuador tienen personalidad jurídica propia según el COA.",
                answer: false,
                explanation: "Incorrecto. El art. 46 COA establece que los ministerios son órganos sin personalidad jurídica."
            },
            {
                type: 'true-false',
                question: "El principio 'non bis in idem' permite sancionar a un funcionario por la misma conducta tanto administrativa como penalmente.",
                answer: true,
                explanation: "Correcto. Aunque protege contra doble sanción, el ámbito administrativo y penal son independientes."
            },
            {
                type: 'true-false',
                question: "El recurso extraordinario de revisión puede interponerse por error de hecho evidente dentro del plazo de 1 año.",
                answer: true,
                explanation: "Correcto. Es una de las causales del art. 232 COA."
            },
            {
                type: 'true-false',
                question: "La desconcentración implica la creación de nuevas entidades con personalidad jurídica.",
                answer: false,
                explanation: "Incorrecto. La desconcentración distribuye funciones sin crear nuevas entidades (art. 7 COA)."
            },
            {
                type: 'true-false',
                question: "El COA establece que para procedimientos coactivos se aplicarán únicamente sus normas, sin excepciones.",
                answer: false,
                explanation: "Incorrecto. Hay excepciones como en materia tributaria (Disposición General Tercera COA)."
            },
            {
                type: 'true-false',
                question: "El principio de imprevisión permite ajustar contratos cuando circunstancias imprevistas alteran su equilibrio financiero.",
                answer: true,
                explanation: "Correcto. Es una excepción al principio pacta sunt servanda."
            },
            {
                type: 'true-false',
                question: "Los órganos colegiados pueden resolver recursos de impugnación según el COA.",
                answer: false,
                explanation: "Incorrecto. El art. 55 COA establece que normalmente no tienen esta competencia."
            },
            {
                type: 'true-false',
                question: "El plazo para interponer recurso de apelación es de 15 días según el COA.",
                answer: false,
                explanation: "Incorrecto. El plazo general es de 10 días (art. 217 COA)."
            },
            {
                type: 'true-false',
                question: "El 'hecho del príncipe' se refiere a modificaciones directas al contrato por la administración.",
                answer: false,
                explanation: "Incorrecto. Se refiere a medidas generales que afectan indirectamente el contrato."
            },
            {
                type: 'true-false',
                question: "El COA permite la aplicación supletoria del derecho privado a los contratos administrativos.",
                answer: true,
                explanation: "Correcto. Cuando no haya regulación específica en derecho público."
            },
            {
                type: 'true-false',
                question: "La delegación de competencias implica pérdida definitiva de la titularidad por parte del órgano delegante.",
                answer: false,
                explanation: "Incorrecto. En la delegación el órgano delegante conserva la titularidad."
            },
            {
                type: 'true-false',
                question: "El principio de especialidad permite a los órganos ejercer competencias no expresamente previstas pero necesarias para sus funciones.",
                answer: true,
                explanation: "Correcto. Así lo establece el art. 67 COA."
            },
            {
                type: 'true-false',
                question: "Los conflictos entre GADs se resuelven por el Tribunal Contencioso Administrativo.",
                answer: false,
                explanation: "Incorrecto. Los resuelve el Consejo Nacional de Competencias (art. 85 COA)."
            },
            {
                type: 'true-false',
                question: "El COA establece que las empresas públicas tienen personalidad jurídica de derecho privado.",
                answer: false,
                explanation: "Incorrecto. Tienen personalidad jurídica de derecho público (art. 46 COA)."
            },
            {
                type: 'true-false',
                question: "La regla 'non reformatio in pejus' permite empeorar la situación del recurrente si el acto original era ilegal.",
                answer: false,
                explanation: "Incorrecto. Esta regla prohíbe empeorar la situación del recurrente (art. 223 COA)."
            },
            // Preguntas de opción múltiple
            {
                type: 'multiple-choice',
                question: "¿Cuál de estos NO es un principio que limita el poder punitivo según el COA?",
                options: [
                    "Legalidad",
                    "Proporcionalidad",
                    "Discrecionalidad",
                    "Debido proceso"
                ],
                answer: 2,
                explanation: "La discrecionalidad no es un principio limitador, sino todo lo contrario. Los principios que limitan el poder punitivo son legalidad, proporcionalidad y debido proceso."
            },
            {
                type: 'multiple-choice',
                question: "Según el COA, ¿qué elemento NO forma parte del ámbito material u objetivo?",
                options: [
                    "La relación jurídico-administrativa",
                    "La actividad jurídica de las administraciones públicas",
                    "Los procedimientos administrativos especiales",
                    "La organización de los partidos políticos"
                ],
                answer: 3,
                explanation: "La organización de partidos políticos no está incluida en el art. 42 COA que define el ámbito material."
            },
            {
                type: 'multiple-choice',
                question: "¿Qué tipo de órgano administrativo está facultado para resolver recursos de impugnación según el COA?",
                options: [
                    "Órganos colegiados",
                    "Órganos consultivos",
                    "Órganos activos",
                    "Órganos de control"
                ],
                answer: 2,
                explanation: "Los órganos activos (de decisión) son los competentes para resolver recursos, no así los colegiados o consultivos (art. 55 COA)."
            },
            {
                type: 'multiple-choice',
                question: "¿Cuál de estas NO es una característica de los órganos colegiados según el COA?",
                options: [
                    "Sin personalidad jurídica",
                    "Pueden resolver recursos de impugnación",
                    "Sus miembros son responsables si votan a favor",
                    "Se rigen por su normativa y el COA"
                ],
                answer: 1,
                explanation: "Los órganos colegiados normalmente NO pueden resolver recursos de impugnación (art. 55 COA)."
            },
            {
                type: 'multiple-choice',
                question: "¿Qué artículo del COA regula el principio de mutabilidad o 'ius variandi'?",
                options: [
                    "Art. 42",
                    "Art. 68",
                    "No está regulado expresamente en el COA",
                    "Art. 150"
                ],
                answer: 2,
                explanation: "El 'ius variandi' es un principio doctrinario que no está regulado expresamente en el COA, aunque se deriva de la potestad administrativa."
            },
            {
                type: 'multiple-choice',
                question: "¿Qué plazo tiene la administración para resolver un recurso de apelación según el COA?",
                options: [
                    "15 días",
                    "1 mes",
                    "3 meses",
                    "10 días"
                ],
                answer: 1,
                explanation: "El art. 217 COA establece un plazo de 1 mes para resolver el recurso de apelación."
            },
            {
                type: 'multiple-choice',
                question: "¿Qué institución resuelve conflictos de competencia entre gobiernos autónomos descentralizados?",
                options: [
                    "Tribunal Contencioso Administrativo",
                    "Consejo Nacional de Competencias",
                    "Corte Constitucional",
                    "Procuraduría General del Estado"
                ],
                answer: 1,
                explanation: "El art. 85 COA y 119.n COOTAD asignan esta competencia al Consejo Nacional de Competencias."
            },
            {
                type: 'multiple-choice',
                question: "¿Qué principio permite a los órganos ejercer competencias no expresamente previstas pero necesarias para sus funciones?",
                options: [
                    "Principio de legalidad",
                    "Principio de especialidad",
                    "Principio de eficiencia",
                    "Principio de jerarquía"
                ],
                answer: 1,
                explanation: "El art. 67 COA establece el principio de especialidad que permite esto."
            },
            {
                type: 'multiple-choice',
                question: "¿Qué tipo de sanción administrativa NO está prevista en el COA?",
                options: [
                    "Amonestación",
                    "Multa",
                    "Arresto",
                    "Pena de prisión"
                ],
                answer: 3,
                explanation: "La pena de prisión es una sanción penal, no administrativa."
            },
            {
                type: 'multiple-choice',
                question: "¿Qué elemento NO es parte del procedimiento sancionador según el COA?",
                options: [
                    "Iniciación de oficio",
                    "Derecho de defensa",
                    "Presunción de culpabilidad",
                    "Plazos de prescripción"
                ],
                answer: 2,
                explanation: "El COA establece presunción de inocencia, no de culpabilidad (art. 76 CRE aplicable)."
            },
            {
                type: 'multiple-choice',
                question: "¿Qué plazo tiene para prescribir una infracción administrativa leve según el COA?",
                options: [
                    "6 meses",
                    "1 año",
                    "3 años",
                    "5 años"
                ],
                answer: 1,
                explanation: "El art. 245 COA establece 1 año para infracciones leves."
            },
            {
                type: 'multiple-choice',
                question: "¿Qué recurso administrativo puede interponerse por error de hecho evidente?",
                options: [
                    "Recurso de apelación",
                    "Recurso de reposición",
                    "Recurso extraordinario de revisión",
                    "Recurso de queja"
                ],
                answer: 2,
                explanation: "El recurso extraordinario de revisión por causal 1 (art. 232 COA)."
            },
            {
                type: 'multiple-choice',
                question: "¿Qué principio contractual permite a la administración modificar unilateralmente el contrato?",
                options: [
                    "Pacta sunt servanda",
                    "Ius variandi",
                    "Rebus sic stantibus",
                    "Iustum pretium"
                ],
                answer: 1,
                explanation: "El 'ius variandi' o principio de mutabilidad concede esta potestad exorbitante."
            },
            {
                type: 'multiple-choice',
                question: "¿Qué artículo del COA regula la delegación de competencias?",
                options: [
                    "Art. 7",
                    "Art. 68",
                    "Art. 78",
                    "Art. 84"
                ],
                answer: 1,
                explanation: "El art. 68 COA regula las formas de transferencia de competencias, incluyendo la delegación."
            },
            {
                type: 'multiple-choice',
                question: "¿Qué diferencia a la descentralización de la desconcentración?",
                options: [
                    "La descentralización crea nuevas entidades con personalidad jurídica",
                    "La desconcentración transfiere competencias definitivamente",
                    "La descentralización no requiere ley para implementarse",
                    "La desconcentración es exclusiva de los GADs"
                ],
                answer: 0,
                explanation: "La descentralización crea nuevas entidades con personalidad jurídica (art. 8 COA), mientras la desconcentración no (art. 7 COA)."
            },
            {
                type: 'multiple-choice',
                question: "¿Qué elemento NO es característico de los contratos administrativos?",
                options: [
                    "Cláusulas exorbitantes",
                    "Equilibrio económico",
                    "Aplicación exclusiva del derecho público",
                    "Posibilidad de modificación unilateral"
                ],
                answer: 2,
                explanation: "Los contratos administrativos admiten aplicación supletoria del derecho privado cuando no hay regulación específica."
            },
            {
                type: 'multiple-choice',
                question: "¿Qué pla
