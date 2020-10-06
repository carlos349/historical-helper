<template>
  <q-page class="bg-grey-3 column">
    <div class="row q-pa-sm bg-primary">
      <q-input 
        filled 
        bg-color="white"
        bottom-slots 
        class="col"
        v-model="find" 
        label="Escriba su busqueda" 
        dense>
        <template v-slot:after >
          <q-btn 
            @click="findQuestion"
            round 
            dense 
            flat 
            icon="send"/>
        </template>
      </q-input>
    </div>
    <div class="q-mt-none q-pa-lg" v-if="noQuestions">
      <template v-for="answer of data">
        <q-card :key="answer.whyAnswer" v-if="answer.posibleAnswer != ''" class="my-card q-mt-md">
          <q-card-section>
            <div class="text-h6">{{answer.posibleAnswer}}</div>
            <div class="text-subtitle2">Pregunta: {{answer.posible}}</div>
          </q-card-section>
          <q-separator inset />
          <q-card-section>
            <div class="text-weight-medium">
              {{ answer.whyAnswer }}
            </div>
            <img 
            v-if="answer.imgAnswer !== ''"
              :src="'img/'+answer.imgAnswer"
              style="width:100%;height:50vh;margin-top:10px;"
              class="rounded-borders shadow-2">
          </q-card-section>
        </q-card>
      </template>
      <q-card v-if="odontodiagrama" class="my-card q-mt-md">
        <q-card-section>
          <div class="text-h6">Explicación.</div>
          <div class="text-subtitle2">Pregunta: Odontodiagrama</div>
        </q-card-section>
        <q-separator inset />
        <q-card-section>
          <div class="text-weight-medium">
            El odontodiagrama constituye desde el punto de vista clínico y legal, de una gran importancia ya que permite la identificación de un individuo gracias a los tratamientos odontológicos recibidos a lo largo de su vida. <br>
            <strong>Nomenclatura para el llenado del Odontodiagrama:</strong>
            <ul>
              <li>Caries o restauración provisional: señalando el área afectada en ROJO.</li>
              <li>Lesiones cervicales no cariosas, señalar con las iniciales en color NEGRO (Er= erosión, Abr= abrasión y abf= Abfraccion). </li>
              <li>Restauraciones u obturación en buen estado (amalgama, ionomero o resina en buen estado) solo el área restaurada en AZUL.</li>
              <li>Restauraciones u obturaciones defectuosas (amalgama, resina o ionomero fracturado o en mal estado) AZUL con borde ROJO.</li>
              <li>Endodoncias indicadas: línea vertical sobre el conducto de la UD en ROJO.</li>
              <li>Endodoncia realizada: línea vertical sobre el conducto en la UD en AZUL.</li>
              <li>Exodoncias realizadas o diente ausente: X en AZUL sobre la UD.</li>
              <li>Exodoncias indicadas o resto radicular: X en ROJO sobre la UD.</li>
              <li>Diente en erupción: circulo en AZUL sobre la UD.</li>
              <li>Diente en erupción con inflamación (pericoronaritis): circulo en ROJO sobre la UD.</li>
            </ul>
          </div>
          <img 
            src="img/odontometriaFirst.png"
            style="width:100%;height:50vh;margin-top:10px;"
            class="rounded-borders shadow-2"><br>
          <img 
            src="img/odontometriaSecond.png"
            style="width:100%;height:50vh;margin-top:10px;"
            class="rounded-borders shadow-2">
        </q-card-section>
      </q-card>
      <q-card v-if="moyer" class="my-card q-mt-md">
        <q-card-section>
          <div class="text-h6">Explicación.</div>
          <div class="text-subtitle2">Pregunta: Análisis de moyers</div>
        </q-card-section>
        <q-separator inset />
        <q-card-section>
          <div class="text-weight-medium">
            Este análisis utiliza el valor de los anchos mesiodistales de los incisivos inferiores permanentes para predecir el tamaño MD de caninos y premolares no erupcionados: el valor de esta predicción es llamado en la literatura espacio requerido de caninos y premolares. Se representa en una tabla de probabilidades que se usan selectivamente de acuerdo al maxilar analizado y según el sexo del paciente.<br><br>
            El Método de Moyers dispone de Tablas de predicción del tamaño Mesio distal de caninos y premolares (o tamaño esperado de caninos y premolares) que se usan selectivamente de acuerdo al maxilar analizado y según el sexo del paciente.<br><br>
            Para realizar el análisis de dentición mixta de Moyers para obtener  la medida de los caninos y premolares según el percentil en el que se busque, Moyers recomendaba el uso de los percentiles 50 y 75.
            <br><br>
            <strong>Pasos: <br> Modelo inferior</strong>
            <ul>
              <li>
                Medir el diámetro mesio – distal de los cuatro incisivos inferiores. <br>
                <img 
                  src="img/moyerFirst.png"
                  style="width:100%;height:50vh;margin-top:10px;"
                  class="rounded-borders shadow-2">
              </li>
              <li>Se suma el ancho MD del IC  y IL derecho y luego los izquierdo se suma cada lado para determinar el espacio que ocupan, para dar la sumatoria de ERAnt. Tanto mandibular como maxilar.</li>
              <li>El resultado obtenido de la sumatoria de los incisivos inferiores, se busca en las tablas de percentiles o de probabilidad.</li>
              <li>
                El siguiente paso es determinar el espacio disponible en el sector posterior.
                <img 
                  src="img/moyerSecond.png"
                  style="width:100%;height:50vh;margin-top:10px;"
                  class="rounded-borders shadow-2">
              </li>
              <li>Se mide con un calibrador desde: distal de los segundos molares temporarios  o mesial de los molares permanentes, hasta mesial de los caninos temporario o distal de los laterales permanentes, se mide la distancia real existente. Este es el espacio disponible para los caninos y premolares permanentes.</li>
              <li>El resultado de la tabla de probabilidad utilizando percentiles de 50-75% según moyers nos da el espacio requerido para canino y premolares. </li>
            </ul>
          </div>
          <img 
            src="img/moyerThird.png"
            style="width:100%;height:50vh;margin-top:10px;"
            class="rounded-borders shadow-2"><br>
          <img 
            src="img/moyerFourth.png"
            style="width:100%;height:50vh;margin-top:10px;"
            class="rounded-borders shadow-2">
            <div class="text-weight-medium">
            <ul>
              <li>
                Se resta el espacio disponible  del espacio requerido obteniendo la discrepancia (ED-ER: DISCREPANCIA) <br>
              </li>
            </ul><br><br>
            <strong>Si los resultados dan positivos hay espacio disponible</strong>  <br><br>
            <strong>Si los resultados dan negativo señala que hay falta de espacio</strong>
          </div>
        </q-card-section>
      </q-card>
      <q-card v-if="tercios" class="my-card q-mt-md">
        <q-card-section>
          <div class="text-h6">Explicación.</div>
          <div class="text-subtitle2">Pregunta: Análisis de los tercios faciales</div>
        </q-card-section>
        <q-separator inset />
        <q-card-section>
          <div class="text-weight-medium">
            La toma de la fotografía, el paciente debe estar de pie, asumiendo la posición natural de su cabeza,  la vista hacia el frente hacia un punto distante y a la altura de sus ojos.<br>
          </div>
          <img 
            src="img/terciosFirst.png"
            style="width:100%;height:50vh;margin-top:10px;"
            class="rounded-borders shadow-2"><br><br>
          <div class="text-weight-medium">
            <strong>Se divide la cara en tres tercios.</strong><br>
            <ul>
              <li>El tercio superior va desde el trichion o línea del cabello hasta la glabela.</li>
              <li>El tercio medio que va desde la glabela hasta el punto subnasal.</li>
              <li>El tercio inferior que se extiende desde el punto subnasal hasta el mentoniano.</li>
            </ul>
          </div>
          <img 
            src="img/terciosSecond.png"
            style="width:100%;height:50vh;margin-top:10px;"
            class="rounded-borders shadow-2"><br><br>
          <div class="text-weight-medium">
            El segundo estudio es el de los dos tercios inferiores, que va desde el punto nasión hasta el subnasal y de éste hasta el mentoniano.<br>
            <ul>
              <li>En el primer método los tercios son iguales, pero estas medidas tienen dos inconvenientes, uno de ellos es que la línea del cabello es muy variable y el otro es que la glabela es una referencia de localización subjetiva, sobre todo en aquellos casos donde se encuentra poco marcada.</li>
              <li>La glabela es un punto de la línea media en el que confluyen las dos crestas supraorbitarias y refiere que las anomalías del tercio superior raramente requieren de correcciones quirúrgicas, debido a que un correcto peinado puede enmascarar la alteración. E n el segundo método, el nasión marca el límite superior de la nariz y es mucho más fácil de localizar que la glabela. Los dos tercios no son iguales como en el método anterior, debido a que existe una diferencia de proporciones.</li>
            </ul><br>
            Por lo tanto, si consideramos la medida nasión-mentoniano como un 100%, un 43% corresponde a la porción superior nasión-subnasal y un 57% a la porción inferior subnasal-mentoniano.
          </div><br>
          <img 
            src="img/terciosThird.png"
            style="width:100%;height:50vh;margin-top:10px;"
            class="rounded-borders shadow-2">
        </q-card-section>
      </q-card>
      <q-card v-if="cefa" class="my-card q-mt-md">
        <q-card-section>
          <div class="text-h6">Explicación.</div>
          <div class="text-subtitle2">Pregunta: Análisis cefalométrico</div>
        </q-card-section>
        <q-separator inset />
        <q-card-section>
          <div class="text-weight-medium">
            La Radiografía Cefálica Lateral es una exposición lateral del cráneo del paciente, con la que podemos evaluar anomalías de desarrollo de las estructuras óseas y dentarias desde el plano sagital, relación de los maxilares individualmente y en conjunto, posición de los dientes, relación de tejidos blandos.<br>
          </div>
          <img 
            src="img/cefaFirst.png"
            style="width:100%;height:50vh;margin-top:10px;"
            class="rounded-borders shadow-2"><br><br>
          <div class="text-weight-medium">
            <strong>Análisis de Steiner.</strong><br><br>
            <strong>Esquelético maxilar:</strong><br>
            -SNA: valor promedio 82o  ángulo formado por el plano silla-nasion y nasion-punto A.  Diagnostica el retrognatismo o prognatismo del maxilar, valor aumentado avance del maxilar y la disminución una posible deficiencia maxilar.<br>
            <strong>Esquelético mandibular:</strong><br>
            -SNB: valor promedio 80o  ángulo formado por la unión del plano silla-nasion-punto B. Diagnostica el retrognatismo o prognatismo mandibular, valor aumentado nos indica protrusión mandibular y disminución indicaría retrognatismo. <br>
            -SND: valor promedio 76o/77o  ángulo formado por los planos silla-nasion y nasion-punto D. Relaciona la mandíbula con la base del cráneo en sentido anteroposterior, valor aumentado protrusión y disminución retrusión.<br>
            <strong>Maxilar – mandibular</strong><br>
            -ANB: valor promedio 2o  es la diferencia entre los ángulos SNA Y SNB, relaciona el maxilar con la mandíbula en sentido anteroposterior este ángulo nos da referencia para diagnosticar la clase esqueletal, cuando el valor es mayor a 4 nos indica una  disto-oclusión clase II esqueletal, menor que 0 nos indica mesio-oclusion   o clase III esqueletal y si es 2 clase I esqueletal.
          </div>
          <img 
            src="img/steinerFirst.png"
            style="width:100%;height:50vh;margin-top:10px;"
            class="rounded-borders shadow-2"><br><br>
          <div class="text-weight-medium">
            <strong>Interdental</strong><br>
            -1s-1i: valor promedio 135o  relación de los ejes mayores de los incisivos centrales superiores e inferiores, valor aumentado nos indica que los incisivos están rectos y valor disminuidos hay protrusión de los dientes.<br>
            <strong>Dentoalveolar maxilar</strong><br>
            -1s-NS: valor promedio 103o  relación dental y maxilar, valor aumentado nos indica protrusión dentaria con respecto a la base del craneal, valores menores nos indican retrusion dentaria con respecto a la base craneal.<br>
            -1s NA: (grados) valor promedio 22o relaciona el incisivo central superior con respecto al plano nasion-A, valor aumentado protrusión dental y disminuido retrusion.<br>
            -1s NA: (mm) valor promedio 4mm valor aumentado nos indica protrusión y disminución retrusion.<br>
            <strong>Dentoalveolar mandibular</strong><br>
            -1i PL. Mand: Valor promedio 90o  valor aumentado nos indica protrusión mayor del incisivo inferior y disminuido incisivos inferior recto o retruido.<br>
            -1i NB: (grados) valor promedio 25o valor aumentado nos indica mayor inclinación vestibular y disminución menor inclinación vestibular lingual.<br>
            -1i NB: (mm) valor promedio 4mm valor aumentado protrusión dental y disminuido retrusion dental.<br><br>
            <strong>Análisis de Mcnamara</strong><br><br>
            Es esta oportunidad se toma en cuenta el triángulo de mcnamara.  <br>
            Los valores promedio de los puntos cefalométricos varían dependiendo de la edad del paciente, y se miden en milímetros.<br>
            -Co-A (mm)<br>
            -Co-Gn (mm)<br>
            -Ena-Me (mm) <br>
            Los valores se pueden reflejar aumentados o disminuidos.<br>
            <img 
            src="img/macnamaraFirst.png"
            style="width:100%;height:50vh;margin-top:10px;"
            class="rounded-borders shadow-2"><br><br>
            <strong>Analisis de Rickets</strong><br><br>
            <strong>Proporcion facial </strong><br>
            -NS-GN : valor normal 67o indica direcciones de crecimiento del rostro, valor alto indica mordida abiertaretrusion del maxilar pacientes dolicofacial rotacion del maxilarhacia atrás. Disminucion crecimientohorizintal y aumentado crecimiento vertical.<br>
            -NS-PL Mand.: valor normal 32o nos permiten relacionar el plano mandibular con respecto a la base cranel, valor mayor indican mordida abierta, retrusion de la mandibula pacientes dolicofaciales, valor disminuido indican mordida cerrada, labios cerrados, dimension vertical disminuida son pacientes braquifaciales. <br>
            -FH-PL Mand.: valor normal 24o, valor aumentadoretrusion de la mandibula y disminuido mordida cerrada.<br><br>
            <strong>Perfil facial </strong><br><br>
            <strong>Linea E: </strong>indica la relacion entre los labios y relacion nariz menton. El labio inferior se apoya en la cara vestibular del incisivo la protusion de este diente producira un labio inferior protusivo, valores negativos indican que el labio esta por detrás del plano E.<br>
            <strong>superior: </strong>valor normal -4mm .<br>
            <strong>inferior: </strong>valor normal -2mm.<br>
            Valores positivos protusion labial  / valores negativos retrusion <br>
            <strong>NAP: </strong>valor normal 0o , angulo de convexidad facial, medido en tejido oseo si es aumentado es retrusion.<br>
          </div>
        </q-card-section>
      </q-card>
    </div>
    <div v-else class="absolute-center">
      <q-circular-progress
        v-if="lookingFor"
        indeterminate
        size="50px"
        color="light-blue"
      />
      <div v-else>
        <q-icon 
          class="q-ml-lg"
          name="info"
          size="100px"
          color="primary"/>
        <div class="text-h5 text-primary text-center">
          Sin respuestas
        </div>
      </div>
    </div>
    
  </q-page>
</template>

<script>
export default {
  data(){
    return{
      lookingFor: false,
      noQuestions: false,
      data: [],
      find: '',
      odontodiagrama:false,
      tercios: false,
      moyer: false,
      cefa: false, 
      dataFor: [
        {
          question: 'Insercion de frenillo',
          answers: [
            {
              posibleAnswer: 'Vestibular superior.',
              posible: 'Inserción de frenillo.',
              whyAnswer: 'NORMAL: repliegue de mucosa que va desde la cara interna del labio superior y se inserta en la encía hasta el paladar. ALTERADO: frenillo corto, largo o inexistente.',
              imgAnswer: ''
            },
            {
              posibleAnswer: 'Vestibular inferior.',
              posible: 'Inserción de frenillo.',
              whyAnswer: 'NORMAL: repliegue de mucosa en la línea mediana de la boca, que conecta el labio inferior con la encía. ALTERADO: frenillo corto, largo o inexistente',
              imgAnswer: ''
            },
            {
              posibleAnswer: 'Lingual',
              posible: 'Inserción de frenillo.',
              whyAnswer: 'NORMAL: cordón fibroso que va desde la cara ventral de la lengua hasta el suelo de la boca donde se inserta. ALTERADO: frenillo corto o largo.',
              imgAnswer: ''
            }
          ]
        },
        {
          question: 'Tipo de denticion',
          answers: [
            {
              posibleAnswer: 'Primaria.',
              posible: 'Tipo de denticion.',
              whyAnswer: 'Son los primeros dientes del niño. Conocida como “dientes de leche”.  Formada por 20 piezas dentales.',
              imgAnswer: ''
            },
            {
              posibleAnswer: 'Mixta.',
              posible: 'Tipo de denticion.',
              whyAnswer: 'Es el periodo en el cual en la boca del niño conviven dientes primarios y dientes permanentes a la vez (suele ocurrir ente los 6 y 12 años de edad).',
              imgAnswer: ''
            },
            {
              posibleAnswer: 'Permanentes.',
              posible: 'Tipo de denticion.',
              whyAnswer: 'Periodo en el cual ya han sido mudados todos los dientes primarios de la arcada. Formado por 32 unidades dentarias.',
              imgAnswer: ''
            }
          ]
        },
        {
          question: 'Relacion Canina',
          answers: [
            {
              posibleAnswer: 'Clase I ',
              posible: 'Relación Canina.',
              whyAnswer: 'La cúspide del canino superior ocluye entre el canino inferior y el primer premolar inferior.',
              imgAnswer: ''
            },
            {
              posibleAnswer: 'Clase II ',
              posible: 'Relación Canina.',
              whyAnswer: 'El canino superior ocluye entre el canino y el incisivo lateral inferior.',
              imgAnswer: ''
            },
            {
              posibleAnswer: 'Clase III ',
              posible: 'Relación Canina.',
              whyAnswer: 'El canino superior ocluye muy distal al canino inferior.',
              imgAnswer: ''
            }
          ]
        },
        {
          question: 'Plano post-lacteo denticion primaria',
          answers: [
            {
              posibleAnswer: 'Nivelado o plano vertical (recto)',
              posible: 'Plano post-lácteo Denticion primaria.',
              whyAnswer: 'La superficie distal de los dientes superiores e inferiores está nivelada, por lo tanto, situada en el mismo plano vertical.',
              imgAnswer: 'planeFirst.png'
            },
            {
              posibleAnswer: 'Tipo escalón mesial',
              posible: 'Plano post-lácteo Denticion primaria.',
              whyAnswer: 'La superficie distal de los molares inferiores es más mesial que el superior.',
              imgAnswer: 'planeSecond.png'
            },
            {
              posibleAnswer: 'Tipo escalón distal:',
              posible: 'Plano post-lácteo Denticion primaria.',
              whyAnswer: 'La superficie distal de los molares inferiores es más distal que los superiores.',
              imgAnswer: 'planeThird.png'
            }
          ]
        },
        {
          question: 'Clase molar denticion permanente',
          answers: [
            {
              posibleAnswer: 'Clase I (Normal)',
              posible: 'Clase molar denticion permanente.',
              whyAnswer: 'El primer molar inferior ocluye la cúspide mesiovestibular de los primeros molares superiores con el surco mesiovestibular de los molares inferiores.',
              imgAnswer: 'classFirst.png'
            },
            {
              posibleAnswer: 'Clase II',
              posible: 'Clase molar denticion permanente.',
              whyAnswer: 'El primer molar inferior se encuentra en relación distal respecto al superior y se reconocen dos divisiones, según la inclinación de los incisivos superiores, y dos subdivisiones: División 1, con protrusión de los incisivos superiores; Subdivisión: unilateralmente distal, con protrusión de los incisivos superiores. División 2, con retrusión de los incisivos superiores; Subdivisión: unilateralmente distal, con retrusión de los incisivos superiores.',
              imgAnswer: 'classSecond.png'
            },
            {
              posibleAnswer: 'Clase III',
              posible: 'Clase molar denticion permanente.',
              whyAnswer: 'El primer molar inferior se encuentra en relación mesial respecto del superior. La articulación dentaria a nivel del área de los incisivos está habitualmente invertida. Subdivisión: condición unilateral.',
              imgAnswer: 'classThird.png'
            }
          ]
        },
        {
          question: 'Analisis Sagital',
          answers: [
            {
              posibleAnswer: 'Overjet.',
              posible: 'Análisis sagital.',
              whyAnswer: 'Es la distancia antero-posterior entre la cara lingual del incisivo central superior y la cara vestibular del inferior. Normal: 2- 3mm.',
              imgAnswer: 'sagFirst.png'
            },
            {
              posibleAnswer: 'Mordida Cruzada anterior.',
              posible: 'Análisis sagital.',
              whyAnswer: 'Se ha definido como una maloclusión en la cual los incisivos y/o caninos del maxilar superior se encuentran en posición lingual con respecto a sus homólogos de la mandíbula.',
              imgAnswer: 'sagSecond.png'
            },
            {
              posibleAnswer: 'Borde a Borde.',
              posible: 'Análisis sagital.',
              whyAnswer: 'Se considera que un paciente presenta mordida borde a borde anterior cuando los bordes incisales de los dientes anteriores superiores quedan en contacto con los borde de los dientes anteriores inferiores.',
              imgAnswer: 'sagThird.png'
            }
          ]
        },
        {
          question: 'Analisis vertical',
          answers: [
            {
              posibleAnswer: 'Obervite.',
              posible: 'Análisis vertical.',
              whyAnswer: 'Es la distancia vertical entre el borde incisal del incisivo central superior e inferior. Normal = 2,5 – 3 mm.',
              imgAnswer: ''
            },
            {
              posibleAnswer: 'Mordida abierta.',
              posible: 'Análisis vertical.',
              whyAnswer: 'Es una alteración facial que se define por la imposibilidad de cerrar los dientes frontales o posteriores. Esto es, no existe el contacto entre los dientes anteriores o posteriores de la arcada superior con los anteriores o posteriores de la inferior.',
              imgAnswer: 'vertFirst.png'
            },
            {
              posibleAnswer: 'Mordida profunda.',
              posible: 'Análisis vertical.',
              whyAnswer: 'Es un estado de sobremordida vertical aumentada en donde la dimensión entre los márgenes incisales dentales superiores e inferiores es excesiva.',
              imgAnswer: ''
            }
          ]
        },
        {
          question: 'Analisis transversal',
          answers: [
            {
              posibleAnswer: 'Normal.',
              posible: 'Análisis transversal.',
              whyAnswer: 'En condiciones normales, las cúspides vestibulares de la arcada superior ocluyen por fuera de la inferior.',
              imgAnswer: 'transFirst.png'
            },
            {
              posibleAnswer: 'Cruzada posterior.',
              posible: 'Análisis transversal.',
              whyAnswer: 'Estamos en presencia de mordida cruzada Si las piezas están más inclinadas hacia labial. estas alteraciones pueden ser uní o bilaterales.',
              imgAnswer: 'transSecond.png'
            },
            {
              posibleAnswer: 'Diastema.',
              posible: 'Análisis transversal.',
              whyAnswer: 'Es un área de espacio adicional entre dos o más dientes. El diastema puede observarse con mayor frecuencia en los dos dientes anteriores del área maxilar superior.',
              imgAnswer: ''
            },
            {
              posibleAnswer: 'DX INTRAORAL.',
              posible: 'Análisis transversal.',
              whyAnswer: 'En este recuadro se va a colocar toda la conclusión de los problemas antes nombrados que presente el paciente, en orden de cómo se fue respondiendo y fue dando una respuesta anormal. Lo que esta bien, es decir No patológico no se coloca aquí.',
              imgAnswer: ''
            }
          ]
        },
        {
          question: 'Habitos bucales',
          answers: [
            {
              posibleAnswer: 'Deglución. Normal.',
              posible: 'Hábitos bucales.',
              whyAnswer: 'La deglución normal se describe tradicionalmente en cuatro etapas. Dependiendo del sujeto esas etapas pueden tener una duración absoluta diferente. Para que corrobores que hay una deglución normal el paciente debe realizar las 4 fases: fase preoperatoria, Fase oral, Fase Faríngea Y Fase esofágica.',
              imgAnswer: ''
            },
            {
              posibleAnswer: 'Atípica.',
              posible: 'Hábitos bucales.',
              whyAnswer: 'La deglución atípica consiste en la postura y uso inadecuados de la lengua en el acto de deglución. Se define como la presión anterior o lateral de la lengua contra las arcadas dentarias. La lengua se posiciona entre los incisivos o se apoya contra su cara posterior al acabar la fase de masticación y realiza una presión contra ellos durante la fase de deglución.',
              imgAnswer: ''
            },
            {
              posibleAnswer: 'Succión digital.',
              posible: 'Hábitos bucales.',
              whyAnswer: 'Significa “chupar dedo”. O Llevar el dedo a la boca.',
              imgAnswer: ''
            },
            {
              posibleAnswer: 'Insuficiencia nasal.',
              posible: 'Hábitos bucales.',
              whyAnswer: 'Dificultad para respirar por la nariz. La respiración nasal o normal es aquella en la que el aire ingresa por la nariz sin esfuerzo con un cierre simultáneo de la cavidad oral. Se crea así una presión negativa entre la lengua y el paladar duro en el momento de la inspiración. La lengua se eleva y se apoya contra el paladar produciendo un estimulo positivo para su desarrollo. Las fosas nasales limpian y calienta el aire antes de conducirlo hacia las vías aéreas.',
              imgAnswer: ''
            },
            {
              posibleAnswer: 'Bruxismo.',
              posible: 'Hábitos bucales.',
              whyAnswer: 'Es el apretamiento o rozamiento de los dientes, en mayor o menor intensidad, que se puede producir durante el día o la noche. Generalmente su movimiento es inconsciente y en él participan los músculos de la masticación.',
              imgAnswer: ''
            },
            {
              posibleAnswer: 'Bruxismo céntrico.',
              posible: 'Hábitos bucales.',
              whyAnswer: 'Se caracteriza por que no aparece el frotamiento sino apretamiento de los dientes y la principal característica sobre estos es la aparición de cúspides invertidas y desgastes de cuello.',
              imgAnswer: ''
            },
            {
              posibleAnswer: 'Bruxismo excéntrico.',
              posible: 'Hábitos bucales.',
              whyAnswer: 'Se caracteriza por el frotamiento de los dientes que produce un desgaste de toda la cara de masticación del diente. El diente se queda plano.',
              imgAnswer: ''
            },
            {
              posibleAnswer: 'Onicofagia.',
              posible: 'Hábitos bucales.',
              whyAnswer: 'Es un hábito compulsivo que se manifiesta en que la persona que lo sufre se come las uñas.',
              imgAnswer: ''
            },
            {
              posibleAnswer: 'Queilofagia.',
              posible: 'Hábitos bucales.',
              whyAnswer: 'Es el acto inconsciente y automatizado de morderse, lamerse o succionarse los labios en forma excesiva y continúa.',
              imgAnswer: ''
            }
          ]
        },
        {
          question: 'Patron Masticatorio',
          answers: [
            {
              posibleAnswer: 'Explicación.',
              posible: 'Patrón Masticatorio.',
              whyAnswer: 'Para observar que patrón masticatorio tiene el paciente es unilateral o bilateral puedes colocar una torunda de algodón de cada lado de la arcada y decirle al paciente que mastique, y el lado de trabajo te guiara a saber si es unilateral o bilateral.',
              imgAnswer: ''
            }
          ]
        },
        {
          question: 'Apertura bucal',
          answers: [
            {
              posibleAnswer: 'Explicación.',
              posible: 'Apertura bucal.',
              whyAnswer: 'La apetura máxima en niños es de 40mm.',
              imgAnswer: ''
            }
          ]
        },
        {
          question: 'Palpacion de ganglios',
          answers: [
            {
              posibleAnswer: 'Explicación.',
              posible: 'Palpación de ganglios.',
              whyAnswer: 'Debes palpar todos los ganglios del paciente y describir si ves alguna lesión.',
              imgAnswer: ''
            }
          ]
        },
        {
          question: 'Analisis de los quintos',
          answers: [
            {
              posibleAnswer: 'Explicación.',
              posible: 'Analisis de los quintos.',
              whyAnswer: 'Al realizar las líneas correspondientes a los quintos se procede a colocar aquí los mm que arrojo cada línea paralela, en las cuales encontramos líneas que pasan por los cantos internos y externos del ojo y por los puntos más externos a la altura de los parietales.',
              imgAnswer: 'quintosFirst.png'
            }
          ]
        },
        {
          question: 'Presencia de simetria',
          answers: [
            {
              posibleAnswer: 'Explicación.',
              posible: 'Presencia de simetría',
              whyAnswer: 'Gracias al análisis de los quintos podrás saber y colocar en este recuadro si hay alguna asimetría y de qué lado.',
              imgAnswer: ''
            }
          ]
        },
        {
          question: 'Angulo de convergencia',
          answers: [
            {
              posibleAnswer: 'Explicación.',
              posible: 'Angulo de convergencia',
              whyAnswer: 'Indica si una cara es normal, cuadrada o angosta. Se traza una línea que pasa por las comisuras externas de ambos ojos y por la unión de los labios superior e inferior a nivel de las comisuras labiales. Su intercepción forma un ángulo con un promedio de 45°. Valores mayores indican una cara mas ancha y cuadrada. Valores menores indican una cara más larga y angosta.',
              imgAnswer: ''
            }
          ]
        },
        {
          question: 'Forma de la cara',
          answers: [
            {
              posibleAnswer: 'Cuadrada.',
              posible: 'Forma de la cara',
              whyAnswer: '',
              imgAnswer: 'faceFirst.png'
            },
            {
              posibleAnswer: 'Alargada.',
              posible: 'Forma de la cara',
              whyAnswer: '',
              imgAnswer: 'faceSecond.png'
            },
            {
              posibleAnswer: 'Ovalada.',
              posible: 'Forma de la cara',
              whyAnswer: '',
              imgAnswer: 'faceThird.png'
            },
            {
              posibleAnswer: 'Redonda.',
              posible: 'Forma de la cara',
              whyAnswer: '',
              imgAnswer: 'faceFourth.png'
            }
          ]
        },
        {
          question: 'Tipo de cara',
          answers: [
            {
              posibleAnswer: 'Mesofacial.',
              posible: 'Tipo de cara',
              whyAnswer: 'Son individuos de rostro armónico, proporcionado, guardando buena relación en el ancho y alto de la cara, los tercios faciales son equilibrados. La dirección del crecimiento de la mandíbula es hacia abajo y adelante.',
              imgAnswer: ''
            },
            {
              posibleAnswer: 'Dólicofacial.',
              posible: 'Tipo de cara',
              whyAnswer: 'Son individuos que en su rostro predomina el largo sobre el ancho. El tercio inferior se encuentra aumentado, el perfil es convexo, la musculatura débil, generalmente asociados a problemas funcionales. La dirección del crecimiento de la mandíbula es hacia abajo y atrás, predomina el crecimiento vertical.',
              imgAnswer: ''
            },
            {
              posibleAnswer: 'Braquifacial.',
              posible: 'Tipo de cara',
              whyAnswer: 'Son individuos que en su cara predomina el ancho sobre el largo. Caras cuadradas, musculatura fuerte, con una dirección de crecimiento mandibular con predominio de componente horizontal o posteroanterior. Tienen diámetros bicigomáticos y mandibulares superiores a la norma.',
              imgAnswer: ''
            }
          ]
        },
        {
          question: 'Linea media facial coincide con la línea media dentala',
          answers: [
            {
              posibleAnswer: 'Explicación.',
              posible: 'Linea media facial coincide con la línea media dental',
              whyAnswer: 'Este es un punto importante a evaluar y que debemos tomar en cuenta con la foto del paciente sonriendo para poder observarlo.',
              imgAnswer: ''
            }
          ]
        },
        {
          question: 'Cierre labial',
          answers: [
            {
              posibleAnswer: 'Adecuado.',
              posible: 'Cierre labial',
              whyAnswer: 'El cierre labial es adecuado cuando estos en reposo cierran y se posa uno sobre el otro naturalmente sin necesidad de hacer algún tipo de fuerza o presión.',
              imgAnswer: ''
            },
            {
              posibleAnswer: 'Incompetente.',
              posible: 'Cierre labial',
              whyAnswer: 'Este ocurre cuando los labios no cierran al mantener los mismo en estado relajado.',
              imgAnswer: ''
            }
          ]
        },
        {
          question: 'Interdental',
          answers: [
            {
              posibleAnswer: '1s-1i.',
              posible: 'Interdental',
              whyAnswer: 'Valor promedio 135°  relación de los ejes mayores de los incisivos centrales superiores e inferiores, valor aumentado nos indica que los incisivos están rectos y valor disminuidos hay protrusión de los dientes.',
              imgAnswer: ''
            }
          ]
        },
        {
          question: 'Dentoalveolar maxilar',
          answers: [
            {
              posibleAnswer: '1s-NS.',
              posible: 'Dentoalveolar maxilar',
              whyAnswer: 'Valor promedio 103°  relación dental y maxilar, valor aumentado nos indica protrusión dentaria con respecto a la base del craneal, valores menores nos indican retrusión dentaria con respecto a la base craneal.',
              imgAnswer: ''
            },
            {
              posibleAnswer: '1s NA (grados).',
              posible: 'Dentoalveolar maxilar',
              whyAnswer: 'Valor promedio 22° relaciona el incisivo central superior con respecto al plano nasion-A, valor aumentado protrusión dental y disminuido retrusión.',
              imgAnswer: ''
            },
            {
              posibleAnswer: '1s NA (mm).',
              posible: 'Dentoalveolar maxilar',
              whyAnswer: 'Valor promedio 4mm valor aumentado nos indica protrusión y disminución retrusión.',
              imgAnswer: ''
            }
          ]
        },
        {
          question: 'Dentoalveolar mandibular',
          answers: [
            {
              posibleAnswer: '1i PL. Mand.',
              posible: 'Dentoalveolar maxilar',
              whyAnswer: 'Valor promedio 90°  valor aumentado nos indica protrusión mayor del incisivo inferior y disminuido incisivos inferior recto o retruido.',
              imgAnswer: ''
            },
            {
              posibleAnswer: '1i NB (grados).',
              posible: 'Dentoalveolar maxilar',
              whyAnswer: 'Valor promedio 25° valor aumentado nos indica mayor inclinación vestibular y disminución menor inclinación vestibular lingual.',
              imgAnswer: ''
            },
            {
              posibleAnswer: '1i NB (mm).',
              posible: 'Dentoalveolar maxilar',
              whyAnswer: 'Valor promedio 4mm valor aumentado protrusión dental y disminuido retrusión dental.',
              imgAnswer: ''
            }
          ]
        },
        {
          question: 'Datos personales -	Historia N°',
          answers: [
            {
                posibleAnswer: 'Explicación.',
                posible: 'Datos personales -	Historia N°',
                whyAnswer: 'Cédula de identidad del paciente (Px) o pasaporte o C.I. del representante.',
                imgAnswer: ''
            },
          ]
        },
        {
          question: 'Datos personales -	Nombre',
          answers: [
            {
                posibleAnswer: 'Explicación.',
                posible: 'Datos personales -	Nombre',
                whyAnswer: 'Permite diferenciar al paciente de los demás, se debe escribir el nombre completo con los dos apellidos como en el registro de identidad.',
                imgAnswer: ''
            },
          ]
        },
        {
          question: 'Datos personales -	Edad',
          answers: [
            {
                posibleAnswer: 'Explicación.',
                posible: 'Datos personales -	Edad',
                whyAnswer: 'Establece un parámetro muy importante dentro de las enfermedades bucodentales, la secuencia y grado de erupción dental y la conducta o el comportamiento del niño dentro del consultorio y tratamiento odontológico.',
                imgAnswer: ''
            },
          ]
        },
        {
          question: 'Datos personales -	Sexo',
          answers: [
            {
                posibleAnswer: 'Explicación.',
                posible: 'Datos personales -	Sexo',
                whyAnswer: 'Representa un factor importante en ciertas enfermedades generales; se debe tener en cuenta que las mujeres llegan al estado de maduración más rápido durante la etapa de crecimiento y desarrollo.',
                imgAnswer: ''
            },
          ]
        },
        {
          question: 'Datos personales -	Fecha y lugar de nacimiento',
          answers: [
            {
                posibleAnswer: 'Explicación.',
                posible: 'Datos personales - Fecha y lugar de nacimiento',
                whyAnswer: 'La primera permite conocer la edad exacta del paciente, mientras que el lugar puede tener importancia diagnóstica.',
                imgAnswer: ''
            },
          ]
        },
        {
          question: 'Datos personales -	Historia N°',
          answers: [
            {
                posibleAnswer: 'Explicación.',
                posible: 'Datos personales -	Historia N°',
                whyAnswer: 'Cédula de identidad del paciente (Px) o pasaporte o C.I. del representante',
                imgAnswer: ''
            },
          ]
        },
        {
          question: 'Datos personales -	Dirección y teléfono',
          answers: [
            {
                posibleAnswer: 'Explicación.',
                posible: 'Datos personales -	Dirección y teléfono',
                whyAnswer: 'Para localizar al paciente en un momento determinado. Permite tener una idea del nivel social, cultural y económico del paciente.',
                imgAnswer: ''
            },
          ]
        },
        {
          question: 'Datos personales -	Representante',
          answers: [
            {
                posibleAnswer: 'Explicación.',
                posible: 'Datos personales - Representante',
                whyAnswer: 'Nombre completo de la persona responsable del menor, escribiendo entre paréntesis el tipo de relación que guarda con el niño.',
                imgAnswer: ''
            },
          ]
        },
        {
          question: 'Motivo de Consulta',
          answers: [
            {
                posibleAnswer: 'Explicación.',
                posible: 'Motivo de Consulta',
                whyAnswer: 'Es un breve relato donde los padres o el propio niño expresan las quejas o causas que los hizo acudir a la consulta. Debe ser llenada usando las propias palabras del paciente. Debe ser colocada entre comillas.',
                imgAnswer: ''
            },
          ]
        },
        {
          question: 'Anamnesis',
          answers: [
            {
                posibleAnswer: 'Explicación.',
                posible: 'Anamnesis',
                whyAnswer: 'Comprende un interrogatorio o entrevista sistémica acumulativa de datos personales y familiares que se agrupan para facilitar el diagnóstico. Entrevista dirigida, semidirigida o abierta.',
                imgAnswer: ''
            },
          ]
        },
        {
          question: 'Antecedentes odontologicos',
          answers: [
            {
                posibleAnswer: 'Explicación.',
                posible: 'Antecedentes odontológicos',
                whyAnswer: 'Comprende la experiencia del paciente con la odontología. Se debe determinar la frecuencia con la que visita al Odontólogo, experiencias agradable o desagradable, frecuencia de los hábitos de higiene oral, enfermedades sufridas  por el paciente.',
                imgAnswer: ''
            },
          ]
        },
        {
          question: 'Dientes supernumerarios',
          answers: [
            {
                posibleAnswer: 'Explicación.',
                posible: 'Dientes supernumerarios',
                whyAnswer: 'Pueden aparecer en algunas personas y son unos dientes en exceso, es decir, dientes sobrantes.',
                imgAnswer: ''
            },
          ]
        },
        {
          question: 'Agenesia dental',
          answers: [
            {
                posibleAnswer: 'Explicación.',
                posible: 'Agenesia dental',
                whyAnswer: 'Se define como un desorden heterogéneo determinado genéticamente que se manifiesta como la ausencia congénita de uno o más dientes.',
                imgAnswer: ''
            },
          ]
        },
        {
          question: 'traumatismo dental',
          answers: [
            {
                posibleAnswer: 'Explicación.',
                posible: 'Traumatismo dental',
                whyAnswer: 'Son muy frecuentes en la infancia y adolescencia. Se considera que es la segunda causa de demanda odontológica urgente después de la caries dental.',
                imgAnswer: ''
            },
          ]
        },
        {
          question: 'Sangramiento de encias',
          answers: [
            {
                posibleAnswer: 'Explicación.',
                posible: 'Sangramiento de encías',
                whyAnswer: 'Las encías sangrantes pueden ser un signo de que usted tiene o está en riesgo de enfermedad periodontal. El sangrado persistente de las encías puede deberse a la acumulación de placa en los dientes.',
                imgAnswer: ''
            },
          ]
        },
        {
          question: 'Sensibilidad dental',
          answers: [
            {
                posibleAnswer: 'Explicación.',
                posible: 'Sensibilidad dental',
                whyAnswer: 'Es el dolor o molestia que se produce debido a un desgaste de la superficie dental o retracción del tejido gingival.',
                imgAnswer: ''
            },
          ]
        },
        {
          question: 'Dolor en la ATM',
          answers: [
            {
                posibleAnswer: 'Explicación.',
                posible: 'Dolor en la ATM',
                whyAnswer: 'Es el área en que se produce la conexión cráneo mandibular. Sus componentes son: cóndilo, disco interauricular, fosa glenoidea, conducto auditivo externo, tubérculo articular, liquido sinovial y ligamentos principales. Los sonidos articulares se registran como Chasquidos, crepitaciones y click. Un chasquido es un sonido único de corta duración. La crepitación es un sonido como de gravilla, que se describe como áspero. Puede presentar dolor, como desviación en cierre y apertura.',
                imgAnswer: ''
            },
          ]
        },
        {
          question: 'Palpacion',
          answers: [
            {
                posibleAnswer: 'Explicación.',
                posible: 'Palpación',
                whyAnswer: 'Se ubican los dedos por delante del orificio auricular y se le indica al paciente que realice movimientos lentos de apertura y cierre bucal.',
                imgAnswer: ''
            },
          ]
        },
        {
          question: 'Higiene bucal',
          answers: [
            {
                posibleAnswer: 'Explicación.',
                posible: 'Higiene bucal',
                whyAnswer: 'Es el número de cepillados al día que hace el paciente, con el uso de enjuague bucal y uso de hilo dental; son preguntas obligadas que se reflejan a la hora de llenar la historia clínica.',
                imgAnswer: ''
            },
          ]
        },
        {
          question: 'Alimentacion Materna (6-24 meses)',
          answers: [
            {
                posibleAnswer: 'Explicación.',
                posible: 'Alimentación Materna (6-24 meses)',
                whyAnswer: 'Estimula el crecimiento de los maxilares y desarrollo de los músculos, además transmite calorías, proteínas y anticuerpos al bebé.',
                imgAnswer: ''
            },
          ]
        },
        {
          question: 'Alimentacion Artificial',
          answers: [
            {
                posibleAnswer: 'Explicación.',
                posible: 'Alimentación Artificial',
                whyAnswer: 'La procedencia de la leche es animal o vegetal.',
                imgAnswer: ''
            },
          ]
        },
        {
          question: 'Odontodiagrama',
          answers: [
            {
                posibleAnswer: '',
                posible: 'Odontodiagrama',
                whyAnswer: '',
                imgAnswer: ''
            },
          ]
        },
        {
          question: 'Analisis cefalometrico',
          answers: [
            {
              posibleAnswer: '',
              posible: 'Analisis cefalometrico',
              whyAnswer: '',
              imgAnswer: ''
            }
          ]
        },
        {
          question: 'Analisis de los tercios faciales',
          answers: [
            {
                posibleAnswer: '',
                posible: 'Analisis de los tercios faciales',
                whyAnswer: '',
                imgAnswer: ''
            },
          ]
        },
        {
          question: 'Analisis de moyers',
          answers: [
            {
                posibleAnswer: '',
                posible: 'Analisis de moyers',
                whyAnswer: '',
                imgAnswer: ''
            },
          ]
        },
        {
          question: 'Perfil facial',
          answers: [
            {
                posibleAnswer: 'Recto.',
                posible: 'Perfil facial',
                whyAnswer: 'Cuando una línea recta une la punta de la nariz, el borde anterior de los labios, y el borde anterior del mentón.',
                imgAnswer: 'profileFirst.png'
            },
            {
                posibleAnswer: 'Convexo.',
                posible: 'Perfil facial',
                whyAnswer: 'Si los labios están por delante de la línea que une la punta de la nariz con el mentón. ',
                imgAnswer: 'profileFirst.png'
            },
            {
                posibleAnswer: 'Concavo.',
                posible: 'Perfil facial',
                whyAnswer: 'Si los labios están por dentro de la línea.',
                imgAnswer: 'profileFirst.png'
            },
          ]
        },
        {
          question: 'Analisis Panoramico (Levandoski)',
          answers: [
            {
                posibleAnswer: '(Linea 1) Línea media vertical maxilar.',
                posible: 'Análisis Panorámico (Levandoski)',
                whyAnswer: 'Colocar la punta del compás en el extremo de la tuberosidad maxilar (altura distal del 2do lateral)',
                imgAnswer: 'panoramicFirst.png'
            },
            {
                posibleAnswer: '(Línea 2) Perpendicular a la línea media.',
                posible: 'Análisis Panorámico (Levandoski)',
                whyAnswer: 'Si los labios están por delante de la línea que une la punta de la nariz con el mentón.',
                imgAnswer: 'panoramicSecond.png'
            },
            {
                posibleAnswer: '(Línea 3) Perpendicular a la línea media maxilar.',
                posible: 'Análisis Panorámico (Levandoski)',
                whyAnswer: 'Se dibujan ramificaciones siguiendo el borde posterior de cada rama (una de  cada lado).',
                imgAnswer: 'panoramicFourth.png'
            },
            {
                posibleAnswer: '(Línea 5 y 6).',
                posible: 'Análisis Panorámico (Levandoski)',
                whyAnswer: 'Se traza una línea de cóndilo a línea media de incisivos superiores e inferiores, se hace igual de cada lado.',
                imgAnswer: 'panoramicFifth.png'
            },
            {
                posibleAnswer: '(Línea 7).',
                posible: 'Análisis Panorámico (Levandoski)',
                whyAnswer: 'Se mide entre gonión y condileon de cada rama. (LINEA VERDE).',
                imgAnswer: 'panoramicSixth.png'
            },
            {
                posibleAnswer: '(Línea 8).',
                posible: 'Análisis Panorámico (Levandoski)',
                whyAnswer: 'Desde gonión hasta la punta de las apófisis coronoides de cadarama. (LINEA NARANJA).',
                imgAnswer: 'panoramicSixth.png'
            },
            {
                posibleAnswer: '(Línea 9).',
                posible: 'Análisis Panorámico (Levandoski)',
                whyAnswer: 'Se coloca el compas en distal de un lado al otro lado. Aquí se observa la longitud real del maxilar, si existe una diferencia de 2 a 3 mm entre los 2 segmentos. (Comparamos derecho e izquierdo).',
                imgAnswer: 'panoramicSeventh.png'
            },
            {
                posibleAnswer: '(Línea 10).',
                posible: 'Análisis Panorámico (Levandoski)',
                whyAnswer: 'De concavidad a concavidad de la rama (análisis de Wilma Simoes). Medimos el ancho de la rama.',
                imgAnswer: 'panoramicEigth.png'
            },
          ]
        },
        {
          question: 'Angulo nasolabial',
          answers: [
            {
                posibleAnswer: 'Explicación.',
                posible: 'Ángulo nasolabial',
                whyAnswer: 'Es el ángulo formado entre la base de la nariz y el labio superior. Se trazan dos líneas que parten del punto subnasal, donde una es tangente al punto más anterior de la nariz y la otra es tangente al borde mucocutáneo del labio superior. Los valores normales de este ángulo se encuentran comprendidos entre los 90º y 110º. Sin embargo, McCollum refiere que el ángulo puede variar entre los 110º y 120º en las mujeres, mientras que en los hombres se encuentra entre los 100º y 110º.',
                imgAnswer: 'nasoFirst.png'
            },
          ]
        },
        {
          question: 'Diagnostico de modelos',
          answers: [
            {
                posibleAnswer: 'Explicación.',
                posible: 'Diagnóstico de modelos',
                whyAnswer: 'Los modelos de estudio o modelos de ortodoncia, hacen referencia a una réplica exacta de la estructura dental del paciente. A partir del modelo de estudio, puede observarse si hay alguna alteración en el tamaño de los dientes, la forma, los espacios entre ellos.',
                imgAnswer: 'modelsFirst.png'
            },
          ]
        },
        {
          question: 'Distancia Intercanina',
          answers: [
            {
                posibleAnswer: 'Explicación.',
                posible: 'Distancia Intercanina',
                whyAnswer: 'Es la distancia lineal entre las cimas de las cúspides de los caninos centrales, o en el caso de faceta de desgaste se toma en centro de la superficie de desgaste, producido por la función masticatoria.',
                imgAnswer: 'canineFirst.png'
            },
          ]
        },
        {
          question: 'Distancia Intermolar',
          answers: [
            {
                posibleAnswer: 'Explicación.',
                posible: 'Distancia Intermolar',
                whyAnswer: 'Es la distancia lineal entre la fosa mesial del molar derecho al molar izquierdo en sus caras oclusales.',
                imgAnswer: 'molarSecond.png'
            },
          ]
        },
        {
          question: '•	Distancia  Interpremolar superior',
          answers: [
            {
                posibleAnswer: 'Explicación.',
                posible: '•	Distancia  Interpremolar superior',
                whyAnswer: 'Se toma como punto de referencia o localización el punto medio de la fisura de la primera premolar derecha al lado izquierdo.',
                imgAnswer: 'molarFirst.png'
            },
          ]
        },
        {
          question: '•	Distancia  Interpremolar inferior',
          answers: [
            {
                posibleAnswer: 'Explicación.',
                posible: '•	Distancia  Interpremolar inferior',
                whyAnswer: 'Se toma como referencia el punto de contacto entre ambos premolares por ser este el punto que coincide con el superior en el momento de la oclusión.',
                imgAnswer: 'molarFirst.png'
            },
          ]
        },
      ]
    }
  },
  methods: {
    findQuestion(){
      this.data = []
      this.lookingFor = true
      this.odontodiagrama = false
      this.moyer = false
      this.cefa = false
      this.tercios = false
      var finded = false
      for (let index = 0; index < this.dataFor.length; index++) {
        const element = this.dataFor[index];
        if (element.question.toLowerCase().indexOf(this.removeAccents(this.find.toLowerCase())) >= 0) {
          for (let j = 0; j < element.answers.length; j++) {
            this.data.push(element.answers[j])
          }
          finded = true
        }
      }
      for (let i = 0; i < this.data.length; i++) {
        const odonto = this.data[i];
        if (odonto.posible == 'Odontodiagrama') {
          this.odontodiagrama = true
        }
        if (odonto.posible == 'Analisis de los tercios faciales') {
          this.tercios = true
        }
        if (odonto.posible == 'Analisis de moyers') {
          this.moyer = true
        }
        if (odonto.posible == 'Analisis cefalometrico') {
          this.cefa = true
        }
      }
      if (finded) {
        setTimeout(() => {
          this.lookingFor = false
          this.noQuestions = true
        }, 500);
      }else{
        setTimeout(() => {
          this.$q.notify('No se encontro alguna pregunta relacionada')
          this.lookingFor = false
          this.noQuestions = false
        }, 500);
      }
    },
    removeAccents(str) {
      return str.normalize("NFD").replace(/[\u0300-\u036f]/g, "");
    } 
  }
}
</script>
<style lang="scss">
  label{
    padding-bottom: 0 !important;
  }
</style>
