# Proyecto sugerencias de cursadas - scripts para cargar datos iniciales
Lo divido en varias partes para que no se haga taaaan largo.

```
db.GeneralAcademicData.insertOne({ 
    careerPairs: [
        { shortCareer: { id: 21 }, longCareer: { id: 38 } },
        { shortCareer: { id: 7 }, longCareer: { id: 13 } },
        { shortCareer: { id: 5 }, longCareer: { id: 31 } },
        { shortCareer: { id: 6 }, longCareer: { id: 34 } },
        { shortCareer: { id: 8 }, longCareer: { id: 39 } },
    ],
    fakeSubjectIds: [441, 508, 509, 510, 792, 793, 794, 577, 576],
    specialSubjects: [
        { id: 4, name: "Nuevos Entornos" },
        { id: 41, name: "Programación" }
    ],
    englishLevelIds: [31, 44]
})
```

```
db.SuggestionTextTemplate.insertMany([
    {
        textId: 'suggestionMail',
        _rawData: [
            {
                key: "intro",
                text: [
                    "Estimado/a ${nombreDelAlumno},", "",
                    "En función de tu recorrido académico en la carrera ${nombreDeLaCarrera}, te enviamos las siguientes sugerencias de inscripción para el próximo período."
                ],
                conditions: [
                    {
                        codigo_condicion: 'SIEMPRE'
                    },
                ]
            },
            {
                key: 'materiasCorrelativas',
                text: [
                    "Por un lado, considerando las materias que regularizaste hasta ahora, <i>te sugerimos</i> que consideres para " +
                    "tu inscripción algunas de las siguientes materias, en función de las correlatividades de tu plan de estudios:",
                    "",
                    "${materiasCorrelativas}",
                    "<b><u>Aclaración</u></b>: ",
                    "Si entre las sugerencias ves una materia que ya regularizaste o tenés en curso, no te preocupes, se debe a una cuestión administrativa interna.",
                    "",
                ],
                conditions: [
                    {
                        codigo_condicion: 'SIEMPRE'
                    },
                ]
            },
            {
                key: 'recomendacionCantidadMaterias',
                text: [
                    "Por otro lado, hemos notado que en tus últimos dos cuatrimestres " +
                    "${cantidadMateriasInscriptoTotal} y ${cantidadMateriasRegularizadasTotal}. " +
                    "Por lo tanto, para el próximo cuatrimestre <i>te sugerimos</i> que ${cantidadMateriasRecomendacion}${anualesQueSeRestan}.",
                    "Es importante que consideres el tiempo que deberás dedicarle a cada materia, " +
                    "tanto de cursada como por fuera de las clases, y el tiempo del que podrás disponer para el estudio." +
                    "La planificación del cuatrimestre es un acto fundamental para el sostenimiento de la cursada en la universidad."
                ],
                conditions: [
                    {
                        codigo_condicion: 'SIEMPRE'
                    },
                ]
            },
            {
                key: 'materiasComunes',
                text: [
                    "Recordá que también podés cursar las siguientes materias comunes en cualquier momento de la carrera y que, " +
                    "por su carga horaria semanal, pueden ser un buen complemento para materias con mayor carga teórica:",
                    "",
                    "${materiasComunesPendientes}"
                ],
                conditions: [
                    {
                        codigo_condicion: 'MATERIAS_COMUNES'
                    },
                ]
            },
            {
                key: 'informatica1MateriasBasicas',
                text:
                    "Te sugerimos que no dejes para último momento la cursada de ${informaticaMateriasBasicas}; esto es importante " +
                    "para incorporar otros conocimientos y fundamental para poder seguir avanzando en tu trayecto.",
                conditions: [
                    {
                        codigo_condicion: 'EN_CARRERA',
                        config_condicion: { id_carreras: [21, 38], condicion_en_carrera: "incluye"}
                    },
                    {
                        codigo_condicion: 'MATERIAS_NO_PENDIENTES',
                        config_condicion: { id_materias: [578], cant: 1 }
                    },
                    {
                        codigo_condicion: 'MATERIAS_PENDIENTES',
                        config_condicion: { id_materias: [545, 546], cant: 1 }
                    }
                ]
            },
            {
                key: 'informatica2Ingles',
                text:
                    "Te sugerimos que por tu grado de avance en la carrera consideres hacer Inglés 1 dada " +
                    "la importancia del idioma al momento de encarar materias avanzadas.",
                conditions: [
                    {
                        codigo_condicion: 'EN_CARRERA',
                        config_condicion: { id_carreras: [21, 38], condicion_en_carrera: "incluye" }
                    },
                    {
                        codigo_condicion: 'CANT_APROBADAS',
                        config_condicion: { cant: 7 }
                    },
                    {
                        codigo_condicion: 'MATERIAS_PENDIENTES',
                        config_condicion: { id_materias: [31], cant: 1 }
                    }
                ]
            },
            {
                key: 'educFisica1Natacion',
                text:
                    "Te sugerimos que no dejes para los últimos años la cursada de ${materiasNatacionFaltantes}. " +
                    "Tené en cuenta esto, sobre todo, si no tenés experiencia en natación.",
                conditions: [
                    {
                        codigo_condicion: 'EN_CARRERA',
                        config_condicion: { id_carreras: [1], condicion_en_carrera: "incluye" }
                    },
                    {
                        codigo_condicion: 'MATERIAS_PENDIENTES',
                        config_condicion: { id_materias: [20, 26], cant: 1 }
                    }
                ]
            },
            {
                key: 'metalurgia1MateriasTroncalesAnio1',
                text:
                    "Te sugerimos que no dejes para último momento la cursada de ${metalurgiaMateriasTroncalesAnio1Pendientes} del primer año; " +
                    "esto es fundamental para poder seguir avanzando en tu trayectoria académica.",
                conditions: [
                    {
                        codigo_condicion: 'EN_CARRERA',
                        config_condicion: { id_carreras: [5, 31], condicion_en_carrera: "incluye" }
                    },
                    {
                        codigo_condicion: 'MATERIAS_PENDIENTES',
                        config_condicion: { id_materias: [160, 149], cant: 1 }
                    }
                ]
            },
            {
                key: 'finalesPendientes',
                text: [
                    "Asimismo, es importante que en la planificación de tu cursada consideres también " +
                    "la preparación de los exámenes finales de las siguientes materias que ya tenés regularizadas:",
                    "",
                    "${materiasConFinalPendiente}",
                ],
                conditions: [
                    {
                        codigo_condicion: 'FINALES_PENDIENTES'
                    },
                ]
            },
            {
                key: 'finalesFechasLimite',
                text:
                    "(1) Si no te presentás a rendir el final en los próximos llamados, se vencerá tu regularidad y deberás recursar la materia. " +
                    "Para conocer las fechas de llamados a exámenes finales, podés consultar el Calendario Académico: " +
                    "http://www.unahur.edu.ar/es/calendario-academico.",
                conditions: [
                    {
                        codigo_condicion: 'LIMITE_FINALES_PENDIENTES'
                    },
                ]
            },
            {
                key: 'avisoImportante',
                text:
                    "<b>IMPORTANTE</b>: esta información podría no tener en cuenta los datos de la cursada inmediata anterior. " +
                    "No te preocupes si eso sucede, la información está siendo procesada.",
                conditions: [
                    {
                        codigo_condicion: 'SIEMPRE'
                    },
                ]
            },
            {
                key: 'orientacion',
                text:
                    "Si necesitás asesoramiento en la planificación de tu carrera o acompañamiento para retomar tu cursada, " +
                    "podés acercarte a la Dirección de Orientación al Estudiante o también al Instituto que te corresponde.",
                conditions: [
                    {
                        codigo_condicion: 'ORIENTACION'
                    },
                ]
            },
            {
                key: 'final',
                text: [
                    "Frente a cualquier duda, podés comunicarte con la dirección del Instituto al que pertenece tu carrera. " +
                    "En la UNAHUR estamos para acompañarte.",
                    "",
                    "Para referencia UNAHUR - DNI: ${dni}"
                ],
                conditions: [
                    {
                        codigo_condicion: 'SIEMPRE'
                    },
                ]
            },
        ]
    },
    {
        textId: 'genericTexts',
        _rawData: [
            { key: "nombreMateriaUnahur", text: 'Materias UNAHUR' },
            { key: "cantidadHorasMateriaUnahur", text: '2' }
        ]
    }
])
```


```
db.SuggestionTextConditions.insertMany([
    {
        "name": "EN_CARRERA"
    },
    {
        "name": "CANT_APROBADAS"
    },
    {
        "name": "MATERIAS_NO_PENDIENTES"
    },
    {
        "name": "SIEMPRE"
    },
    {
        "name": "MATERIAS_COMUNES"
    },
    {
        "name": "MATERIAS_PENDIENTES"
    },
    {
        "name": "FINALES_PENDIENTES"
    },
    {
        "name": "LIMITE_FINALES_PENDIENTES"
    },
    {
        "name": "ORIENTACION"
    },
    {
        "name": "NUNCA"
    }
])
```

```
db.CareerData.insertMany([
    { 
        careerId: 1, 
        unahurSubjects: [{year:1},{year:4}], englishLevels: [{year:3},{year:4}], 
        suggestionThresholdRegularizedSubjects: 4 
    },
    { 
        careerId: 5, 
        unahurSubjects: [{year: 1}], englishLevels: [{year:2}, {year:3}], 
        suggestionThresholdRegularizedSubjects: 3
    },
    { 
        careerId: 6, 
        unahurSubjects: [{year:1}, {year:2}, {year:3}], englishLevels: [{year:2}], 
        suggestionThresholdRegularizedSubjects: 5 
    },
    { 
        careerId: 7, 
        unahurSubjects: [{year:3, campo: 'CFC1'}], 
        englishLevels: [{year:1, campo: 'CFC1'}], 
        suggestionThresholdRegularizedSubjects: 3 
    },
    { 
        careerId: 13, 
        unahurSubjects: [{ year: 3, campo: 'CFC1' }, { year: 4, campo: 'CFC2'}],
        englishLevels: [{ year: 1, campo: 'CFC1' }, { year: 5, campo: 'CFC2'}], 
        suggestionThresholdRegularizedSubjects: 3
    },
    { 
        careerId: 16, 
        unahurSubjects: [{year:1}, {year:4}], englishLevels: [{year:2}, {year:3}], 
        suggestionThresholdRegularizedSubjects: 3 
    },
    { 
        careerId: 21, 
        unahurSubjects: [{year:3, campo: 'Gral'}], 
        englishLevels: [{ year: 1, campo: 'Gral' }, { year: 2, campo: 'Gral'}], 
        suggestionThresholdRegularizedSubjects: 3 
    },
    { 
        careerId: 31, 
        unahurSubjects: [{year:1}], englishLevels: [{year:2}, {year:3}], 
        suggestionThresholdRegularizedSubjects: 3 
    },
    { 
        careerId: 34, 
        unahurSubjects: [{year:1}, {year:2}, {year:3}], englishLevels: [{year:2}, {year:4}], 
        suggestionThresholdRegularizedSubjects: 5 
    },
    { 
        careerId: 38, 
        unahurSubjects: [{ year: 3, campo: 'Gral' }, { year: 4, campo: 'Gral'}], 
        englishLevels: [{ year: 1, campo: 'Gral' }, { year: 3, campo: 'Gral'}], 
        suggestionThresholdRegularizedSubjects: 3, 
        specialCareerName: "Tecnicatura / Licenciatura en informática"
    }
])
```

```
db.GeneralAcademicData.insertOne({ 
    careerPairs: [
        { shortCareer: { id: 21 }, longCareer: { id: 38 } },
        { shortCareer: { id: 7 }, longCareer: { id: 13 } },
        { shortCareer: { id: 5 }, longCareer: { id: 31 } },
        { shortCareer: { id: 6 }, longCareer: { id: 34 } },
        { shortCareer: { id: 8 }, longCareer: { id: 39 } },
    ],
    fakeSubjectIds: [441, 508, 509, 510, 792, 793, 794, 577, 576],
    specialSubjects: [
        { id: 4, name: "Nuevos Entornos" },
        { id: 41, name: "Programación" }
    ],
    englishLevelIds: [31, 44]
})
```

```
db.RegistrationSuggestionCondition.insertMany([
    { 
        codigo: "N-1", 
        descripcion: "Para cursar cualquier materia del año N hay que tener regularizadas todas las del N-1"
    },
    {
        codigo: "N-2",
        descripcion: "Para cursar cualquier materia del año N hay que tener regularizadas todas las del N-2"
    },
    {
        codigo: "N-1R-2A",
        descripcion: "Para cursar cualquier materia del año N hay que tener, o bien regularizadas todas las del N-1, o bien aprobadas todas las del N-2"
    },
    {
        codigo: "CANT-MATERIAS",
        descripcion: "Hay que tener una cantidad de materias regularizadas, puede restringirse por campos",
        parametros: [
            { nombre: "cantidad", tipo: "Number", descripcion: "cuántas materias debe tener regularizadas el estudiante"},
            { nombre: "campos", tipo: "[String]", descripcion: "se piden materias de estos campos" },
            { nombre: "campos_excepto", tipo: "[String]", descripcion: "se piden materias que no sean de estos campos" },
        ]
    },
    {
        codigo: "ANIOS-COMPLETOS",
        descripcion: "Hay que tener regularizadas todas las materias hasta un año, salvo una determinada cantidad",
        parametros: [
            { nombre: "anio", tipo: "Number", descripcion: "hasta qué año debe tener completo el estudiante" },
            { nombre: "salvo_cantidad", tipo: "Number", descripcion: "hasta cuántas materias pueden faltar" }
        ]
    },
    {
        codigo: "CAMPOS-COMPLETOS",
        descripcion: "Hay que tener regularizadas todas las materias de uno o varios campos, salvo una determinada cantidad",
        parametros: [
            { nombre: "campos", tipo: "[String]", descripcion: "qué campos debe tener completo el estudiante" },
            { nombre: "salvo_cantidad", tipo: "Number", descripcion: "hasta cuántas materias pueden faltar" }
        ]
    },
    {
        codigo: "CANT-MATERIAS-ANIO",
        descripcion: "Hay que tener regularizadas una cantidad de materias de un año, cualesquiera o de ciertos campos",
        parametros: [
            { nombre: "anio", tipo: "Number", descripcion: "de qué año hay que tener una cantidad de materias regularizadas" },
            { nombre: "campos", tipo: "[String]", descripcion: "se piden materias de estos campos" },
            { nombre: "cantidad", tipo: "Number", descripcion: "cuántas materias debe tener regularizadas el estudiante del año indicado" }
        ]
    },
    {
        codigo: "MATERIAS-ESPECIFICAS",
        descripcion: "Hay que tener regularizadas ciertas materias",
        parametros: [
            { nombre: "materias", tipo: "[Number]", descripcion: "id de las materias que hay que tener regularizadas" },
            { nombre: "salvo_cantidad", tipo: "Number", descripcion: "hasta cuántas materias pueden faltar" }
        ]
    }
])
```

```
db.RegistrationSuggestionConditionUse.insertMany([
    {
        id_carrera: 6, 
        anio: 2,
        codigo_condicion: 'CANT-MATERIAS-ANIO',
        config_condicion: { anio: 1, cantidad: 3, campos: ['CFE1', 'CFE2'] }   
    },
    {
        id_carrera: 6,
        anio: 2,
        codigo_condicion: 'CANT-MATERIAS-ANIO',
        config_condicion: { anio: 1, cantidad: 2, campos: ['CFB1', 'CFB2'] }
    },
    {
        id_carrera: 34,
        anio: 2,
        codigo_condicion: 'CANT-MATERIAS-ANIO',
        config_condicion: { anio: 1, cantidad: 3, campos: ['CFE1', 'CFE2'] }
    },
    {
        id_carrera: 34,
        anio: 2,
        codigo_condicion: 'CANT-MATERIAS-ANIO',
        config_condicion: { anio: 1, cantidad: 2, campos: ['CFB1', 'CFB2'] }
    },
    {
        id_carrera: 6,
        anio: 3,
        codigo_condicion: 'ANIOS-COMPLETOS',
        config_condicion: { anio: 1 }
    },
    {
        id_carrera: 6,
        anio: 3,
        codigo_condicion: 'CANT-MATERIAS-ANIO',
        config_condicion: { anio: 2, cantidad: 3, campos: ['CFE1', 'CFE2'] }
    },
    {
        id_carrera: 34,
        anio: 3,
        codigo_condicion: 'ANIOS-COMPLETOS',
        config_condicion: { anio: 1 }
    },
    {
        id_carrera: 34,
        anio: 3,
        codigo_condicion: 'CANT-MATERIAS-ANIO',
        config_condicion: { anio: 2, cantidad: 3, campos: ['CFE1', 'CFE2'] }
    },
    {
        id_carrera: 34,
        anio: 4,
        codigo_condicion: 'CAMPOS-COMPLETOS',
        config_condicion: { campos: ['CFE1', 'CFB1'] }
    },
    {
        id_carrera: 34,
        anio: 5,
        codigo_condicion: 'CANT-MATERIAS-ANIO',
        config_condicion: { anio: 4, cantidad: 2, campos: ['CFE1', 'CFE2'] }
    },
    {
        id_carrera: 34,
        anio: 5,
        codigo_condicion: 'CANT-MATERIAS-ANIO',
        config_condicion: { anio: 4, cantidad: 2, campos: ['CFB1', 'CFB2'] }
    },
    {
        id_carrera: 6,
        id_materia: 227,
        codigo_condicion: 'ANIOS-COMPLETOS',
        config_condicion: { anio: 3 }
    },
    {
        id_carrera: 34,
        id_materia: 227,
        codigo_condicion: 'ANIOS-COMPLETOS',
        config_condicion: { anio: 3 }
    },
    {
        id_carrera: 7, 
        codigo_condicion: 'N-2'
    },
    {
        id_carrera: 7,
        id_materia: 210,
        codigo_condicion: 'CANT-MATERIAS',
        config_condicion: { cantidad: 12, campos_excepto: ['CFC1', 'CFC2'] }
    },
    {
        id_carrera: 7,
        id_materia: 263,
        codigo_condicion: 'CANT-MATERIAS',
        config_condicion: { cantidad: 12, campos_excepto: ['CFC1', 'CFC2'] }
    }
])
```


```
db.RegistrationSuggestionConditionUse.insertMany([
    {
        id_carrera: 13,
        codigo_condicion: 'N-2'
    },
    {
        id_carrera: 13,
        id_materia: 210,
        codigo_condicion: 'CANT-MATERIAS',
        config_condicion: { cantidad: 12, campos_excepto: ['CFC1', 'CFC2'] }
    },
    {
        id_carrera: 13,
        id_materia: 263,
        codigo_condicion: 'CANT-MATERIAS',
        config_condicion: { cantidad: 12, campos_excepto: ['CFC1', 'CFC2'] }
    },
    {
        id_carrera: 13,
        id_materia: 399,
        codigo_condicion: 'CANT-MATERIAS',
        config_condicion: { cantidad: 22 }
    },
    {
        id_carrera: 13,
        id_materia: 398,
        codigo_condicion: 'CANT-MATERIAS',
        config_condicion: { cantidad: 22 }
    },
    {
        id_carrera: 13,
        id_materia: 407,
        codigo_condicion: 'CANT-MATERIAS',
        config_condicion: { cantidad: 34 }
    },
    {
        id_carrera: 13,
        anio: 4,
        codigo_condicion: 'ANIOS-COMPLETOS',
        config_condicion: { anio: 3, salvo_cantidad: 3 }
    },
    {
        id_carrera: 13,
        anio: 5,
        codigo_condicion: 'ANIOS-COMPLETOS',
        config_condicion: { anio: 3, salvo_cantidad: 3 }
    },
    {
        id_carrera: 1,
        codigo_condicion: 'N-2'
    },
    {
        id_carrera: 16,
        codigo_condicion: 'N-1R-2A'
    },
    {
        id_carrera: 21,
        anio: 3,
        codigo_condicion: 'MATERIAS-ESPECIFICAS',
        config_condicion: { materias: [545, 580, 546, 547, 549, 550] }
    },
    {
        id_carrera: 21,
        id_materia: 559,
        codigo_condicion: 'MATERIAS-ESPECIFICAS',
        config_condicion: { materias: [551] }
    },
    {
        id_carrera: 21,
        id_materia: 579,
        codigo_condicion: 'MATERIAS-ESPECIFICAS',
        config_condicion: { materias: [554] }
    },
    {
        id_carrera: 38,
        anio: 3,
        codigo_condicion: 'MATERIAS-ESPECIFICAS',
        config_condicion: { materias: [545, 580, 546, 547, 549, 550] }
    },
    {
        id_carrera: 38,
        id_materia: 559,
        codigo_condicion: 'MATERIAS-ESPECIFICAS',
        config_condicion: { materias: [551] }
    },
    {
        id_carrera: 38,
        id_materia: 579,
        codigo_condicion: 'MATERIAS-ESPECIFICAS',
        config_condicion: { materias: [554] }
    },
    {
        id_carrera: 39,
        codigo_condicion: 'N-2'
    },
    {
        id_carrera: 11,
        codigo_condicion: 'N-2'
    },
    {
        id_carrera: 2,
        codigo_condicion: 'N-2'
    },
    {
        id_carrera: 53,
        codigo_condicion: 'N-2'
    },
    {
        id_carrera: 12,
        codigo_condicion: 'N-2'
    }
])
```


```
db.SubjectData.insertMany([
  { id_materia: 149, id_carrera: 5, anio: 1 },
  { id_materia: 152, id_carrera: 5, anio: 1 },
  { id_materia: 151, id_carrera: 5, anio: 1 },
  { id_materia: 443, id_carrera: 5, anio: 1 },
  { id_materia: 153, id_carrera: 5, anio: 1 },
  { id_materia: 160, id_carrera: 5, anio: 1 },
  { id_materia: 444, id_carrera: 5, anio: 1 },
  { id_materia: 149, id_carrera: 31, anio: 1 },
  { id_materia: 152, id_carrera: 31, anio: 1 },
  { id_materia: 151, id_carrera: 31, anio: 1 },
  { id_materia: 150, id_carrera: 31, anio: 1 },
  { id_materia: 153, id_carrera: 31, anio: 1 },
  { id_materia: 160, id_carrera: 31, anio: 1 },
  { id_materia: 444, id_carrera: 31, anio: 1 },
  { id_materia: 41, id_carrera: 31, anio: 1 },
])
```

```
db.SubjectData.insertMany([
  { id_materia: 123, id_carrera: 6, anio: 1, campo: "CFB1" },
  { id_materia: 124, id_carrera: 6, anio: 1, campo: "CFB1" },
  { id_materia: 129, id_carrera: 6, anio: 1, campo: "CFE1" },
  { id_materia: 125, id_carrera: 6, anio: 1, campo: "CFB1" },
  { id_materia: 222, id_carrera: 6, anio: 1, campo: "CFB1" },
  { id_materia: 141, id_carrera: 6, anio: 1, campo: "CFE1" },
  { id_materia: 131, id_carrera: 6, anio: 1, campo: "CFE1" },
  { id_materia: 4, id_carrera: 6, anio: 1 },
  { id_materia: 126, id_carrera: 6, anio: 2, campo: "CFB1" },
  { id_materia: 133, id_carrera: 6, anio: 2, campo: "CFE1" },
  { id_materia: 139, id_carrera: 6, anio: 2, campo: "CFE1" },
  { id_materia: 225, id_carrera: 6, anio: 2, campo: "CFE1" },
  { id_materia: 130, id_carrera: 6, anio: 2, campo: "CFB1" },
  { id_materia: 223, id_carrera: 6, anio: 2, campo: "CFB1" },
  { id_materia: 132, id_carrera: 6, anio: 2, campo: "CFE1" },
  { id_materia: 31, id_carrera: 6, anio: 2 },
  { id_materia: 221, id_carrera: 6, anio: 3, campo: "CFB1" },
  { id_materia: 135, id_carrera: 6, anio: 3, campo: "CFE1" },
  { id_materia: 140, id_carrera: 6, anio: 3, campo: "CFB1" },
  { id_materia: 134, id_carrera: 6, anio: 3, campo: "CFE1" },
  { id_materia: 137, id_carrera: 6, anio: 3, campo: "CFB1" },
  { id_materia: 142, id_carrera: 6, anio: 3, campo: "CFE1" },
  { id_materia: 226, id_carrera: 6, anio: 3, campo: "CFE1" },
  { id_materia: 224, id_carrera: 6, anio: 3, campo: "CFB1" },
  { id_materia: 128, id_carrera: 6, anio: 3, campo: "CFE1" },
  { id_materia: 227, id_carrera: 6, anio: 3 },
  { id_materia: 123, id_carrera: 34, anio: 1, campo: "CFB1" },
  { id_materia: 124, id_carrera: 34, anio: 1, campo: "CFB1" },
  { id_materia: 129, id_carrera: 34, anio: 1, campo: "CFE1" },
  { id_materia: 125, id_carrera: 34, anio: 1, campo: "CFB1" },
  { id_materia: 222, id_carrera: 34, anio: 1, campo: "CFB1" },
  { id_materia: 141, id_carrera: 34, anio: 1, campo: "CFE1" },
  { id_materia: 131, id_carrera: 34, anio: 1, campo: "CFE1" },
  { id_materia: 4, id_carrera: 34, anio: 1 },
  { id_materia: 126, id_carrera: 34, anio: 2, campo: "CFB1" },
  { id_materia: 133, id_carrera: 34, anio: 2, campo: "CFE1" },
  { id_materia: 139, id_carrera: 34, anio: 2, campo: "CFE1" },
  { id_materia: 225, id_carrera: 34, anio: 2, campo: "CFE1" },
  { id_materia: 130, id_carrera: 34, anio: 2, campo: "CFB1" },
  { id_materia: 223, id_carrera: 34, anio: 2, campo: "CFB1" },
  { id_materia: 132, id_carrera: 34, anio: 2, campo: "CFE1" },
  { id_materia: 31, id_carrera: 34, anio: 2 },
  { id_materia: 221, id_carrera: 34, anio: 3, campo: "CFB1" },
  { id_materia: 135, id_carrera: 34, anio: 3, campo: "CFE1" },
  { id_materia: 140, id_carrera: 34, anio: 3, campo: "CFB1" },
  { id_materia: 134, id_carrera: 34, anio: 3, campo: "CFE1" },
  { id_materia: 137, id_carrera: 34, anio: 3, campo: "CFB1" },
  { id_materia: 142, id_carrera: 34, anio: 3, campo: "CFE1" },
  { id_materia: 226, id_carrera: 34, anio: 3, campo: "CFE1" },
  { id_materia: 224, id_carrera: 34, anio: 3, campo: "CFB1" },
  { id_materia: 128, id_carrera: 34, anio: 3, campo: "CFE1" },
  { id_materia: 227, id_carrera: 34, anio: 3 },
  { id_materia: 687, id_carrera: 34, anio: 4 },
  { id_materia: 474, id_carrera: 34, anio: 4, campo: "CFB2" },
  { id_materia: 696, id_carrera: 34, anio: 4 },
  { id_materia: 693, id_carrera: 34, anio: 4, campo: "CFE2" },
  { id_materia: 689, id_carrera: 34, anio: 4, campo: "CFE2" },
  { id_materia: 685, id_carrera: 34, anio: 4, campo: "CFB2" },
  { id_materia: 44, id_carrera: 34, anio: 4 },
  { id_materia: 691, id_carrera: 34, anio: 5, campo: "CFE2" },
  { id_materia: 692, id_carrera: 34, anio: 5, campo: "CFE2" },
  { id_materia: 690, id_carrera: 34, anio: 5, campo: "CFE2" },
  { id_materia: 684, id_carrera: 34, anio: 5 },
  { id_materia: 695, id_carrera: 34, anio: 5 }
])
```

```
db.SubjectData.insertMany([
  { id_materia: 149, id_carrera: 13, anio: 1, campo: "CFB1" },
  { id_materia: 203, id_carrera: 13, anio: 1, campo: "CIC1" },
  { id_materia: 4, id_carrera: 13, anio: 1, campo: "CFC1" },
  { id_materia: 195, id_carrera: 13, anio: 1, campo: "CFB1" },
  { id_materia: 196, id_carrera: 13, anio: 1, campo: "CFB1" },
  { id_materia: 348, id_carrera: 13, anio: 1, campo: "CFB1" },
  { id_materia: 31, id_carrera: 13, anio: 1, campo: "CFC1" },
  { id_materia: 416, id_carrera: 13, anio: 1, campo: "CIC1" },
  { id_materia: 198, id_carrera: 13, anio: 2, campo: "CFB1" },
  { id_materia: 154, id_carrera: 13, anio: 2, campo: "CFB1" },
  { id_materia: 199, id_carrera: 13, anio: 2, campo: "CFB1" },
  { id_materia: 415, id_carrera: 13, anio: 2, campo: "CFE1" },
  { id_materia: 200, id_carrera: 13, anio: 2, campo: "CFB1" },
  { id_materia: 417, id_carrera: 13, anio: 2, campo: "CIC1" },
  { id_materia: 208, id_carrera: 13, anio: 2, campo: "CIC1" },
  { id_materia: 197, id_carrera: 13, anio: 2, campo: "CFE1" },
  { id_materia: 205, id_carrera: 13, anio: 3, campo: "CFE1" },
  { id_materia: 211, id_carrera: 13, anio: 3, campo: "CIC1" },
  { id_materia: 201, id_carrera: 13, anio: 3, campo: "CFB1" },
  { id_materia: 204, id_carrera: 13, anio: 3, campo: "CFE1" },
  { id_materia: 357, id_carrera: 13, anio: 3, campo: "CFB1" },
  { id_materia: 418, id_carrera: 13, anio: 3, campo: "CIC1" },
  { id_materia: 210, id_carrera: 13, anio: 3, campo: "CFB1" },
  { id_materia: 263, id_carrera: 13, anio: 3, campo: "CFE1" },
  { id_materia: 41, id_carrera: 13, anio: 4, campo: "CFC2" },
  { id_materia: 396, id_carrera: 13, anio: 4, campo: "CFE2" },
  { id_materia: 397, id_carrera: 13, anio: 4, campo: "CFE2" },
  { id_materia: 398, id_carrera: 13, anio: 4, campo: "CFE2" },
  { id_materia: 399, id_carrera: 13, anio: 4, campo: "CIC2" },
  { id_materia: 400, id_carrera: 13, anio: 4, campo: "CFE2" },
  { id_materia: 401, id_carrera: 13, anio: 4, campo: "CFE2" },
  { id_materia: 402, id_carrera: 13, anio: 4, campo: "CFE2" },
  { id_materia: 403, id_carrera: 13, anio: 4, campo: "CFE2" },
  { id_materia: 680, id_carrera: 13, anio: 5, campo: "CFE2" },
  { id_materia: 405, id_carrera: 13, anio: 5, campo: "CFE2" },
  { id_materia: 406, id_carrera: 13, anio: 5, campo: "CFE2" },
  { id_materia: 407, id_carrera: 13, anio: 5, campo: "CIC2" },
  { id_materia: 209, id_carrera: 13, anio: 5, campo: "CIC2" },
  { id_materia: 44, id_carrera: 13, anio: 5, campo: "CFC2" },
  { id_materia: 408, id_carrera: 13, anio: 5, campo: "CFE2" },
  { id_materia: 409, id_carrera: 13, anio: 5, campo: "CIC2" },
  { id_materia: 410, id_carrera: 13, anio: 5, campo: "CFE2" },
  { id_materia: 367, id_carrera: 13, anio: 5, campo: "CIC2" },
  { id_materia: 149, id_carrera: 7, anio: 1, campo: "CFB1" },
  { id_materia: 203, id_carrera: 7, anio: 1, campo: "CIC1" },
  { id_materia: 4, id_carrera: 7, anio: 1, campo: "CFC1" },
  { id_materia: 195, id_carrera: 7, anio: 1, campo: "CFB1" },
  { id_materia: 196, id_carrera: 7, anio: 1, campo: "CFB1" },
  { id_materia: 348, id_carrera: 7, anio: 1, campo: "CFB1" },
  { id_materia: 31, id_carrera: 7, anio: 1, campo: "CFC1" },
  { id_materia: 416, id_carrera: 7, anio: 1, campo: "CIC1" },
  { id_materia: 198, id_carrera: 7, anio: 2, campo: "CFB1" },
  { id_materia: 154, id_carrera: 7, anio: 2, campo: "CFB1" },
  { id_materia: 199, id_carrera: 7, anio: 2, campo: "CFB1" },
  { id_materia: 415, id_carrera: 7, anio: 2, campo: "CFE1" },
  { id_materia: 200, id_carrera: 7, anio: 2, campo: "CFB1" },
  { id_materia: 417, id_carrera: 7, anio: 2, campo: "CIC1" },
  { id_materia: 208, id_carrera: 7, anio: 2, campo: "CIC1" },
  { id_materia: 197, id_carrera: 7, anio: 2, campo: "CFE1" },
  { id_materia: 205, id_carrera: 7, anio: 3, campo: "CFE1" },
  { id_materia: 211, id_carrera: 7, anio: 3, campo: "CIC1" },
  { id_materia: 201, id_carrera: 7, anio: 3, campo: "CFB1" },
  { id_materia: 204, id_carrera: 7, anio: 3, campo: "CFE1" },
  { id_materia: 357, id_carrera: 7, anio: 3, campo: "CFB1" },
  { id_materia: 418, id_carrera: 7, anio: 3, campo: "CIC1" },
  { id_materia: 210, id_carrera: 7, anio: 3, campo: "CFB1" },
  { id_materia: 263, id_carrera: 7, anio: 3, campo: "CFE1" }
])
```

```
db.SubjectData.insertMany([
  { id_materia: 1, id_carrera: 1, anio: 1 },
  { id_materia: 2, id_carrera: 1, anio: 1 },
  { id_materia: 6, id_carrera: 1, anio: 1 },
  { id_materia: 4, id_carrera: 1, anio: 1 },
  { id_materia: 22, id_carrera: 1, anio: 1 },
  { id_materia: 8, id_carrera: 1, anio: 1 },
  { id_materia: 9, id_carrera: 1, anio: 1 },
  { id_materia: 10, id_carrera: 1, anio: 1 },
  { id_materia: 12, id_carrera: 1, anio: 1 },
  { id_materia: 52, id_carrera: 1, anio: 1 },
  { id_materia: 13, id_carrera: 1, anio: 2 },
  { id_materia: 14, id_carrera: 1, anio: 2 },
  { id_materia: 15, id_carrera: 1, anio: 2 },
  { id_materia: 16, id_carrera: 1, anio: 2 },
  { id_materia: 18, id_carrera: 1, anio: 2 },
  { id_materia: 7, id_carrera: 1, anio: 2 },
  { id_materia: 19, id_carrera: 1, anio: 2 },
  { id_materia: 20, id_carrera: 1, anio: 2 },
  { id_materia: 21, id_carrera: 1, anio: 2 },
  { id_materia: 25, id_carrera: 1, anio: 2 },
  { id_materia: 23, id_carrera: 1, anio: 2 },
  { id_materia: 24, id_carrera: 1, anio: 3 },
  { id_materia: 17, id_carrera: 1, anio: 3 },
  { id_materia: 26, id_carrera: 1, anio: 3 },
  { id_materia: 27, id_carrera: 1, anio: 3 },
  { id_materia: 28, id_carrera: 1, anio: 3 },
  { id_materia: 29, id_carrera: 1, anio: 3 },
  { id_materia: 30, id_carrera: 1, anio: 3 },
  { id_materia: 31, id_carrera: 1, anio: 3 },
  { id_materia: 32, id_carrera: 1, anio: 3 },
  { id_materia: 34, id_carrera: 1, anio: 3 },
  { id_materia: 33, id_carrera: 1, anio: 3 },
  { id_materia: 35, id_carrera: 1, anio: 3 },
  { id_materia: 50, id_carrera: 1, anio: 3 },
  { id_materia: 37, id_carrera: 1, anio: 4 },
  { id_materia: 38, id_carrera: 1, anio: 4 },
  { id_materia: 39, id_carrera: 1, anio: 4 },
  { id_materia: 40, id_carrera: 1, anio: 4 },
  { id_materia: 41, id_carrera: 1, anio: 4 },
  { id_materia: 219, id_carrera: 1, anio: 4 },
  { id_materia: 47, id_carrera: 1, anio: 4 },
  { id_materia: 44, id_carrera: 1, anio: 4 },
  { id_materia: 46, id_carrera: 1, anio: 4 },
  { id_materia: 48, id_carrera: 1, anio: 4 },
  { id_materia: 49, id_carrera: 1, anio: 4 },
  { id_materia: 51, id_carrera: 1, anio: 4 }
])
```

```
db.SubjectData.insertMany([
  { id_materia: 123, id_carrera: 16, anio: 1 },
  { id_materia: 4, id_carrera: 16, anio: 1 },
  { id_materia: 124, id_carrera: 16, anio: 1 },
  { id_materia: 478, id_carrera: 16, anio: 1 },
  { id_materia: 476, id_carrera: 16, anio: 1 },
  { id_materia: 222, id_carrera: 16, anio: 1 },
  { id_materia: 479, id_carrera: 16, anio: 1 },
  { id_materia: 475, id_carrera: 16, anio: 2 },
  { id_materia: 223, id_carrera: 16, anio: 2 },
  { id_materia: 130, id_carrera: 16, anio: 2 },
  { id_materia: 482, id_carrera: 16, anio: 2 },
  { id_materia: 140, id_carrera: 16, anio: 2 },
  { id_materia: 472, id_carrera: 16, anio: 2 },
  { id_materia: 480, id_carrera: 16, anio: 2 },
  { id_materia: 477, id_carrera: 16, anio: 2 },
  { id_materia: 125, id_carrera: 16, anio: 2 },
  { id_materia: 485, id_carrera: 16, anio: 2 },
  { id_materia: 31, id_carrera: 16, anio: 2 },
  { id_materia: 483, id_carrera: 16, anio: 2 },
  { id_materia: 488, id_carrera: 16, anio: 3 },
  { id_materia: 492, id_carrera: 16, anio: 3 },
  { id_materia: 486, id_carrera: 16, anio: 3 },
  { id_materia: 481, id_carrera: 16, anio: 3 },
  { id_materia: 136, id_carrera: 16, anio: 3 },
  { id_materia: 41, id_carrera: 16, anio: 3 },
  { id_materia: 474, id_carrera: 16, anio: 3 },
  { id_materia: 44, id_carrera: 16, anio: 3 },
  { id_materia: 126, id_carrera: 16, anio: 3 },
  { id_materia: 221, id_carrera: 16, anio: 3 },
  { id_materia: 487, id_carrera: 16, anio: 4 },
  { id_materia: 489, id_carrera: 16, anio: 4 },
  { id_materia: 494, id_carrera: 16, anio: 4 },
  { id_materia: 507, id_carrera: 16, anio: 4 },
  { id_materia: 493, id_carrera: 16, anio: 4 },
  { id_materia: 484, id_carrera: 16, anio: 4 },
  { id_materia: 497, id_carrera: 16, anio: 4 },
  { id_materia: 498, id_carrera: 16, anio: 4 },
  { id_materia: 499, id_carrera: 16, anio: 4 },
  { id_materia: 490, id_carrera: 16, anio: 5 },
  { id_materia: 501, id_carrera: 16, anio: 5 },
  { id_materia: 502, id_carrera: 16, anio: 5 },
  { id_materia: 473, id_carrera: 16, anio: 5 },
  { id_materia: 224, id_carrera: 16, anio: 5 },
  { id_materia: 500, id_carrera: 16, anio: 5 },
  { id_materia: 495, id_carrera: 16, anio: 5 },
  { id_materia: 491, id_carrera: 16, anio: 5 },
  { id_materia: 135, id_carrera: 16, anio: 5 }
])
```

```
db.SubjectData.insertMany([
  { id_materia: 545, id_carrera: 38, anio: 1, campo: "CB" },
  { id_materia: 580, id_carrera: 38, anio: 1, campo: "AYL" },
  { id_materia: 546, id_carrera: 38, anio: 1, campo: "ASOYR" },
  { id_materia: 4, id_carrera: 38, anio: 1, campo: 'Gral' },
  { id_materia: 547, id_carrera: 38, anio: 1, campo: "TC" },
  { id_materia: 549, id_carrera: 38, anio: 1, campo: "AYL" },
  { id_materia: 550, id_carrera: 38, anio: 1, campo: "ISBDYSI" },
  { id_materia: 31, id_carrera: 38, anio: 1, campo: 'Gral' },
  { id_materia: 551, id_carrera: 38, anio: 2, campo: "CB" },
  { id_materia: 578, id_carrera: 38, anio: 2, campo: "AYL" },
  { id_materia: 553, id_carrera: 38, anio: 2, campo: "ASOYR" },
  { id_materia: 554, id_carrera: 38, anio: 2, campo: "ASOYR" },
  { id_materia: 555, id_carrera: 38, anio: 2, campo: "ISBDYSI" },
  { id_materia: 724, id_carrera: 38, anio: 2 },
  { id_materia: 557, id_carrera: 38, anio: 2, campo: "ISBDYSI" },
  { id_materia: 559, id_carrera: 38, anio: 2, campo: "AYL" },
  { id_materia: 560, id_carrera: 38, anio: 2, campo: "ASOYR" },
  { id_materia: 558, id_carrera: 38, anio: 3, campo: "ISBDYSI" },
  { id_materia: 579, id_carrera: 38, anio: 3, campo: "AYL" },
  { id_materia: 44, id_carrera: 38, anio: 3, campo: 'Gral' },
  { id_materia: 561, id_carrera: 38, anio: 3, campo: "ISBDYSI" },
  { id_materia: 725, id_carrera: 38, anio: 4 },
  { id_materia: 726, id_carrera: 38, anio: 4 },
  { id_materia: 727, id_carrera: 38, anio: 3 },
  { id_materia: 728, id_carrera: 38, anio: 4 },
  { id_materia: 729, id_carrera: 38, anio: 3 },
  { id_materia: 562, id_carrera: 38, anio: 4 },
  { id_materia: 545, id_carrera: 21, anio: 1, campo: "CB" },
  { id_materia: 580, id_carrera: 21, anio: 1, campo: "AYL" },
  { id_materia: 546, id_carrera: 21, anio: 1, campo: "ASOYR" },
  { id_materia: 4, id_carrera: 21, anio: 1, campo: 'Gral' },
  { id_materia: 547, id_carrera: 21, anio: 1, campo: "TC" },
  { id_materia: 549, id_carrera: 21, anio: 1, campo: "AYL" },
  { id_materia: 550, id_carrera: 21, anio: 1, campo: "ISBDYSI" },
  { id_materia: 31, id_carrera: 21, anio: 1, campo: 'Gral' },
  { id_materia: 551, id_carrera: 21, anio: 2, campo: "CB" },
  { id_materia: 578, id_carrera: 21, anio: 2, campo: "AYL" },
  { id_materia: 553, id_carrera: 21, anio: 2, campo: "ASOYR" },
  { id_materia: 554, id_carrera: 21, anio: 2, campo: "ASOYR" },
  { id_materia: 555, id_carrera: 21, anio: 2, campo: "ISBDYSI" },
  { id_materia: 579, id_carrera: 21, anio: 2, campo: "AYL" },
  { id_materia: 557, id_carrera: 21, anio: 2, campo: "ISBDYSI" },
  { id_materia: 558, id_carrera: 21, anio: 2, campo: "ISBDYSI" },
  { id_materia: 44, id_carrera: 21, anio: 2, campo: 'Gral' },  
  { id_materia: 559, id_carrera: 21, anio: 3, campo: "AYL" },
  { id_materia: 560, id_carrera: 21, anio: 3, campo: "ASOYR" },
  { id_materia: 561, id_carrera: 21, anio: 3, campo: "ISBDYSI" },
  { id_materia: 562, id_carrera: 21, anio: 3 },
  { id_materia: 563, id_carrera: 21, anio: 3, campo: "COMP" },
  { id_materia: 564, id_carrera: 21, anio: 3, campo: "COMP" },
  { id_materia: 565, id_carrera: 21, anio: 3, campo: "COMP" },
  { id_materia: 566, id_carrera: 21, anio: 3, campo: "COMP" },
  { id_materia: 567, id_carrera: 21, anio: 3, campo: "COMP" },
  { id_materia: 568, id_carrera: 21, anio: 3, campo: "COMP" },
  { id_materia: 569, id_carrera: 21, anio: 3, campo: "COMP" },
  { id_materia: 571, id_carrera: 21, anio: 3, campo: "COMP" },
  { id_materia: 572, id_carrera: 21, anio: 3, campo: "COMP" },
  { id_materia: 573, id_carrera: 21, anio: 3, campo: "COMP" },
  { id_materia: 574, id_carrera: 21, anio: 3, campo: "COMP" },
  { id_materia: 575, id_carrera: 21, anio: 3, campo: "COMP" },
  { id_materia: 724, id_carrera: 21, anio: 3, campo: "COMP" },
  { id_materia: 725, id_carrera: 21, anio: 3, campo: "COMP" },
  { id_materia: 726, id_carrera: 21, anio: 3, campo: "COMP" },
  { id_materia: 727, id_carrera: 21, anio: 3, campo: "COMP" },
  { id_materia: 729, id_carrera: 21, anio: 3, campo: "COMP" },
  { id_materia: 745, id_carrera: 21, anio: 3, campo: "COMP" },
  { id_materia: 746, id_carrera: 21, anio: 3, campo: "COMP" }
])
```

```
db.SubjectData.insertMany([
  { id_carrera: 39, id_materia: 4, anio: 1, campo: "CFB" },
  { id_carrera: 39, id_materia: 31, anio: 1, campo: "CFC" },
  { id_carrera: 39, id_materia: 228, anio: 1, campo: "CFC" },
  { id_carrera: 39, id_materia: 230, anio: 1, campo: "CFC" },
  { id_carrera: 39, id_materia: 232, anio: 1, campo: "CFB" },
  { id_carrera: 39, id_materia: 233, anio: 1, campo: "CFB" },
  { id_carrera: 39, id_materia: 244, anio: 1, campo: "CFE" },
  { id_carrera: 39, id_materia: 795, anio: 1, campo: "CFB" },
  { id_carrera: 39, id_materia: 807, anio: 1, campo: "CFB" },
  { id_carrera: 39, id_materia: 44, anio: 2, campo: "CFC" },
  { id_carrera: 39, id_materia: 234, anio: 2, campo: "CFB" },
  { id_carrera: 39, id_materia: 235, anio: 2, campo: "CFE" },
  { id_carrera: 39, id_materia: 236, anio: 2, campo: "CFE" },
  { id_carrera: 39, id_materia: 237, anio: 2, campo: "CFB" },
  { id_carrera: 39, id_materia: 238, anio: 2, campo: "CFE" },
  { id_carrera: 39, id_materia: 239, anio: 2, campo: "CFE" },
  { id_carrera: 39, id_materia: 240, anio: 2, campo: "CFE" },
  { id_carrera: 39, id_materia: 247, anio: 2, campo: "CFE" },
  { id_carrera: 39, id_materia: 241, anio: 3, campo: "CFE" },
  { id_carrera: 39, id_materia: 242, anio: 3, campo: "CIC" },
  { id_carrera: 39, id_materia: 243, anio: 3, campo: "CFB" },
  { id_carrera: 39, id_materia: 245, anio: 3, campo: "CIC" },
  { id_carrera: 39, id_materia: 246, anio: 3, campo: "CFE" },
  { id_carrera: 39, id_materia: 248, anio: 3, campo: "CIC" },
  { id_carrera: 39, id_materia: 249, anio: 3, campo: "CIC" },
  { id_carrera: 39, id_materia: 255, anio: 3, campo: "CFE" },
  { id_carrera: 39, id_materia: 766, anio: 4, campo: "CIC" },
  { id_carrera: 39, id_materia: 767, anio: 4, campo: "CIC" },
  { id_carrera: 39, id_materia: 768, anio: 4, campo: "CFB" },
  { id_carrera: 39, id_materia: 769, anio: 4, campo: "CFE" },
  { id_carrera: 39, id_materia: 770, anio: 4, campo: "CIC" },
  { id_carrera: 39, id_materia: 771, anio: 4, campo: "CIC" },
  { id_carrera: 39, id_materia: 772, anio: 4, campo: "CFB" },
  { id_carrera: 39, id_materia: 773, anio: 4, campo: "CFB" },
  { id_carrera: 39, id_materia: 774, anio: 5, campo: "CIC" },
  { id_carrera: 39, id_materia: 775, anio: 5, campo: "CFE" },
  { id_carrera: 39, id_materia: 776, anio: 5, campo: "CFE" },
  { id_carrera: 39, id_materia: 777, anio: 5, campo: "CFE" },
  { id_carrera: 39, id_materia: 778, anio: 5, campo: "CIC" },
  { id_carrera: 39, id_materia: 779, anio: 5, campo: "CFE" },
  { id_carrera: 39, id_materia: 780, anio: 5, campo: "CFB" }
])
```

```
db.SubjectData.insertMany([
  { id_carrera: 53, id_materia: 4, anio: 1, campo: "CFC" },
  { id_carrera: 53, id_materia: 917, anio: 1, campo: "CFE" },
  { id_carrera: 53, id_materia: 918, anio: 1, campo: "CFE" },
  { id_carrera: 53, id_materia: 919, anio: 1, campo: "CFE" },
  { id_carrera: 53, id_materia: 920, anio: 1, campo: "CFE" },
  { id_carrera: 53, id_materia: 921, anio: 1, campo: "CFE" },
  { id_carrera: 53, id_materia: 123, anio: 1, campo: "CFB" },
  { id_carrera: 53, id_materia: 124, anio: 1, campo: "CFB" },
  { id_carrera: 53, id_materia: 222, anio: 1, campo: "CFB" },
  { id_carrera: 53, id_materia: 130, anio: 1, campo: "CFB" },
  { id_carrera: 53, id_materia: 31, anio: 2, campo: "CFC" },
  { id_carrera: 53, id_materia: 922, anio: 2, campo: "CFE" },
  { id_carrera: 53, id_materia: 923, anio: 2, campo: "CFE" },
  { id_carrera: 53, id_materia: 925, anio: 2, campo: "CFE" },
  { id_carrera: 53, id_materia: 125, anio: 2, campo: "CFB" },
  { id_carrera: 53, id_materia: 126, anio: 2, campo: "CFB" },
  { id_carrera: 53, id_materia: 221, anio: 2, campo: "CFB" },
  { id_carrera: 53, id_materia: 223, anio: 2, campo: "CFB" },
  { id_carrera: 53, id_materia: 140, anio: 2, campo: "CFB" },
  { id_carrera: 53, id_materia: 957, anio: 3, campo: "CFC" },
  { id_carrera: 53, id_materia: 924, anio: 3, campo: "CFE" },
  { id_carrera: 53, id_materia: 926, anio: 3, campo: "CFE" },
  { id_carrera: 53, id_materia: 927, anio: 3, campo: "CFE" },
  { id_carrera: 53, id_materia: 928, anio: 3, campo: "CFE" },
  { id_carrera: 53, id_materia: 929, anio: 3, campo: "CFE" },
  { id_carrera: 53, id_materia: 930, anio: 3, campo: "CFE" },
  { id_carrera: 53, id_materia: 224, anio: 3, campo: "CFB" },
  { id_carrera: 53, id_materia: 136, anio: 3, campo: "CFB" },
  { id_carrera: 53, id_materia: 44, anio: 4, campo: "CFC" },
  { id_carrera: 53, id_materia: 931, anio: 4, campo: "CFE" },
  { id_carrera: 53, id_materia: 932, anio: 4, campo: "CFE" },
  { id_carrera: 53, id_materia: 933, anio: 4, campo: "CFE" },
  { id_carrera: 53, id_materia: 934, anio: 4, campo: "CFE" },
  { id_carrera: 53, id_materia: 935, anio: 4, campo: "CFE" },
  { id_carrera: 53, id_materia: 936, anio: 4, campo: "CIC" },
  { id_carrera: 53, id_materia: 135, anio: 4, campo: "CFB" },
  { id_carrera: 53, id_materia: 474, anio: 4, campo: "CFB" },
  { id_carrera: 53, id_materia: 937, anio: 5, campo: "CIC" },
  { id_carrera: 53, id_materia: 938, anio: 5, campo: "CIC" },
  { id_carrera: 53, id_materia: 939, anio: 5, campo: "CIC" },
  { id_carrera: 53, id_materia: 940, anio: 5, campo: "CIC" },
  { id_carrera: 53, id_materia: 472, anio: 5, campo: "CFB" },
  { id_carrera: 53, id_materia: 473, anio: 5, campo: "CFB" }
])
```

```
db.SubjectData.insertMany([
  { id_carrera: 2, id_materia: 4, anio: 1, campo: "CFC" },
  { id_carrera: 2, id_materia: 7, anio: 2, campo: "CFB" },
  { id_carrera: 2, id_materia: 10, anio: 1, campo: "CFB" },
  { id_carrera: 2, id_materia: 52, anio: 1, campo: "CFB" },
  { id_carrera: 2, id_materia: 15, anio: 2, campo: "CFB" },
  { id_carrera: 2, id_materia: 22, anio: 1, campo: "CFB" },
  { id_carrera: 2, id_materia: 29, anio: 3, campo: "CFB" },
  { id_carrera: 2, id_materia: 31, anio: 3, campo: "CFC" },
  { id_carrera: 2, id_materia: 39, anio: 3, campo: "CFB" },
  { id_carrera: 2, id_materia: 41, anio: 4, campo: "CFC" },
  { id_carrera: 2, id_materia: 44, anio: 4, campo: "CFC" },
  { id_carrera: 2, id_materia: 49, anio: 4, campo: "CFB" },
  { id_carrera: 2, id_materia: 54, anio: 1, campo: "CFE" },
  { id_carrera: 2, id_materia: 55, anio: 1, campo: "CIC" },
  { id_carrera: 2, id_materia: 56, anio: 1, campo: "CFE" },
  { id_carrera: 2, id_materia: 57, anio: 1, campo: "CFE" },
  { id_carrera: 2, id_materia: 58, anio: 1, campo: "CIC" },
  { id_carrera: 2, id_materia: 59, anio: 2, campo: "CFE" },
  { id_carrera: 2, id_materia: 60, anio: 2, campo: "CFE" },
  { id_carrera: 2, id_materia: 61, anio: 2, campo: "CIC" },
  { id_carrera: 2, id_materia: 62, anio: 2, campo: "CFE" },
  { id_carrera: 2, id_materia: 63, anio: 2, campo: "CFE" },
  { id_carrera: 2, id_materia: 64, anio: 2, campo: "CFE" },
  { id_carrera: 2, id_materia: 65, anio: 2, campo: "CFE" },
  { id_carrera: 2, id_materia: 66, anio: 2, campo: "CFE" },
  { id_carrera: 2, id_materia: 67, anio: 3, campo: "CIC" },
  { id_carrera: 2, id_materia: 68, anio: 3, campo: "CFE" },
  { id_carrera: 2, id_materia: 69, anio: 3, campo: "CFE" },
  { id_carrera: 2, id_materia: 70, anio: 3, campo: "CFE" },
  { id_carrera: 2, id_materia: 71, anio: 3, campo: "CFE" },
  { id_carrera: 2, id_materia: 72, anio: 3, campo: "CFE" },
  { id_carrera: 2, id_materia: 73, anio: 3, campo: "CFE" },
  { id_carrera: 2, id_materia: 74, anio: 3, campo: "CFE" },
  { id_carrera: 2, id_materia: 75, anio: 4, campo: "CIC" },
  { id_carrera: 2, id_materia: 76, anio: 4, campo: "CIC" },
  { id_carrera: 2, id_materia: 77, anio: 4, campo: "CFE" },
  { id_carrera: 2, id_materia: 78, anio: 4, campo: "CFE" },
  { id_carrera: 2, id_materia: 79, anio: 4, campo: "CFE" },
  { id_carrera: 2, id_materia: 80, anio: 4, campo: "CFE" },
  { id_carrera: 2, id_materia: 82, anio: 4, campo: "CFE" }
])
```

```
db.SubjectData.insertMany([
  { id_carrera: 11, id_materia: 4, anio: 1, campo: "CFC" },
  { id_carrera: 11, id_materia: 10, anio: 1, campo: "CFB" },
  { id_carrera: 11, id_materia: 52, anio: 1, campo: "CFB" },
  { id_carrera: 11, id_materia: 22, anio: 1, campo: "CFB" },
  { id_carrera: 11, id_materia: 319, anio: 1, campo: "CFE" },
  { id_carrera: 11, id_materia: 320, anio: 1, campo: "CFE" },
  { id_carrera: 11, id_materia: 321, anio: 1, campo: "CFE" },
  { id_carrera: 11, id_materia: 322, anio: 1, campo: "CFE" },
  { id_carrera: 11, id_materia: 323, anio: 1, campo: "CIC" },
  { id_carrera: 11, id_materia: 7, anio: 2, campo: "CFB" },
  { id_carrera: 11, id_materia: 15, anio: 2, campo: "CFB" },
  { id_carrera: 11, id_materia: 29, anio: 2, campo: "CFB" },
  { id_carrera: 11, id_materia: 31, anio: 2, campo: "CFC" },
  { id_carrera: 11, id_materia: 324, anio: 2, campo: "CFE" },
  { id_carrera: 11, id_materia: 325, anio: 2, campo: "CFE" },
  { id_carrera: 11, id_materia: 326, anio: 2, campo: "CIC" },
  { id_carrera: 11, id_materia: 327, anio: 2, campo: "CFE" },
  { id_carrera: 11, id_materia: 328, anio: 2, campo: "CIC" },
  { id_carrera: 11, id_materia: 39, anio: 3, campo: "CFB" },
  { id_carrera: 11, id_materia: 41, anio: 3, campo: "CFC" },
  { id_carrera: 11, id_materia: 44, anio: 3, campo: "CFC" },
  { id_carrera: 11, id_materia: 49, anio: 3, campo: "CFB" },
  { id_carrera: 11, id_materia: 329, anio: 3, campo: "CFE" },
  { id_carrera: 11, id_materia: 330, anio: 3, campo: "CFE" },
  { id_carrera: 11, id_materia: 331, anio: 3, campo: "CFE" },
  { id_carrera: 11, id_materia: 332, anio: 3, campo: "CIC" },
  { id_carrera: 11, id_materia: 333, anio: 3, campo: "CFE" },
  { id_carrera: 11, id_materia: 334, anio: 3, campo: "CIC" },
  { id_carrera: 11, id_materia: 335, anio: 4, campo: "CFE" },
  { id_carrera: 11, id_materia: 336, anio: 4, campo: "CFE" },
  { id_carrera: 11, id_materia: 337, anio: 4, campo: "CFE" },
  { id_carrera: 11, id_materia: 338, anio: 4, campo: "CFE" },
  { id_carrera: 11, id_materia: 339, anio: 4, campo: "CFE" },
  { id_carrera: 11, id_materia: 340, anio: 4, campo: "CFE" },
  { id_carrera: 11, id_materia: 341, anio: 4, campo: "CFE" },
  { id_carrera: 11, id_materia: 342, anio: 4, campo: "CIC" }
])
```

```
db.SubjectData.insertMany([
  { id_carrera: 12, id_materia: 4, anio: 1, campo: "CFC" },
  { id_carrera: 12, id_materia: 7, anio: 2, campo: "CFB" },
  { id_carrera: 12, id_materia: 10, anio: 2, campo: "CFB" },
  { id_carrera: 12, id_materia: 52, anio: 3, campo: "CFB" },
  { id_carrera: 12, id_materia: 15, anio: 3, campo: "CFB" },
  { id_carrera: 12, id_materia: 22, anio: 4, campo: "CFB" },
  { id_carrera: 12, id_materia: 29, anio: 1, campo: "CFB" },
  { id_carrera: 12, id_materia: 31, anio: 1, campo: "CFC" },
  { id_carrera: 12, id_materia: 39, anio: 1, campo: "CFB" },
  { id_carrera: 12, id_materia: 41, anio: 2, campo: "CFC" },
  { id_carrera: 12, id_materia: 44, anio: 2, campo: "CFC" },
  { id_carrera: 12, id_materia: 49, anio: 2, campo: "CFB" },
  { id_carrera: 12, id_materia: 371, anio: 2, campo: "CFE" },
  { id_carrera: 12, id_materia: 372, anio: 3, campo: "CFE" },
  { id_carrera: 12, id_materia: 373, anio: 3, campo: "CFE" },
  { id_carrera: 12, id_materia: 374, anio: 3, campo: "CFE" },
  { id_carrera: 12, id_materia: 375, anio: 3, campo: "CFE" },
  { id_carrera: 12, id_materia: 376, anio: 3, campo: "CFE" },
  { id_carrera: 12, id_materia: 377, anio: 3, campo: "CFE" },
  { id_carrera: 12, id_materia: 378, anio: 4, campo: "CFE" },
  { id_carrera: 12, id_materia: 379, anio: 4, campo: "CFE" },
  { id_carrera: 12, id_materia: 380, anio: 4, campo: "CIC" },
  { id_carrera: 12, id_materia: 381, anio: 4, campo: "CFE" },
  { id_carrera: 12, id_materia: 382, anio: 4, campo: "CFE" },
  { id_carrera: 12, id_materia: 383, anio: 4, campo: "CFE" },
  { id_carrera: 12, id_materia: 384, anio: 4, campo: "CFE" },
  { id_carrera: 12, id_materia: 385, anio: 2, campo: "CIC" },
  { id_carrera: 12, id_materia: 386, anio: 1, campo: "CFE" },
  { id_carrera: 12, id_materia: 387, anio: 2, campo: "CFE" },
  { id_carrera: 12, id_materia: 388, anio: 1, campo: "CFE" },
  { id_carrera: 12, id_materia: 389, anio: 1, campo: "CFE" },
  { id_carrera: 12, id_materia: 390, anio: 2, campo: "CFE" },
  { id_carrera: 12, id_materia: 395, anio: 1, campo: "CFE" },
  { id_carrera: 12, id_materia: 320, anio: 3, campo: "CFE" },
  { id_carrera: 12, id_materia: 323, anio: 2, campo: "CIC" },
  { id_carrera: 12, id_materia: 326, anio: 3, campo: "CIC" },
  { id_carrera: 12, id_materia: 328, anio: 2, campo: "CIC" },
  { id_carrera: 12, id_materia: 329, anio: 3, campo: "CFE" },
  { id_carrera: 12, id_materia: 332, anio: 4, campo: "CIC" },
  { id_carrera: 12, id_materia: 336, anio: 1, campo: "CFE" }
])
```

