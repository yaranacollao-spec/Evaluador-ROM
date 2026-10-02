# 🦾 Evaluador Kinemático de ROM de Hombro en Navegador

Aplicación web interactiva para la evaluación cinemática del Rango de Movimiento (ROM) activo de hombro en los planos de **abducción** y **flexión**. Implementa detección de poses mediante visión por computadora en tiempo real utilizando la librería MediaPipe Pose directamente en el navegador (*Client-Side Processing*).

---

## 🔗 Demo en Vivo y Enlace Público

- **Aplicación Web Desplegada:** [https://evaluador-rom.vercel.app] (https://evaluador-rom.vercel.app)
- **Repositorio de Código:** [https://github.com/yaranacollao-spec/evaluador-rom]

---

## 📌 Características Principales

- **Procesamiento Local (Privacidad Garantizada):** El video de la cámara web se procesa 100% en el cliente mediante WebAssembly y WebGL. Ningún dato audiovisual es enviado a servidores externos.
- **Cálculo Vectorial Dinámico:** Determinación matemática continua del ángulo formado por los landmarks de la articulación glenohumeral y la cadena biomecánica: **Cadera $\rightarrow$ Hombro $\rightarrow$ Codo**.
- **Métricas e Indicadores Clínicos:**
  - Mapeo en tiempo real del ángulo actual.
  - Registro dinámico del Rango de Movimiento Máximo alcanzado (**ROM Peak**).
  - Gráfico interactivo temporal de la curva del movimiento mediante `Chart.js`.
- **Lienzo Anatómico (Canvas 2D):** Superposición transparente de los segmentos óseos directamente sobre la imagen capturada por la cámara.

---

## 📐 Lógica del Procesamiento Kinemático

La extracción de puntos clave (*landmarks*) utiliza el modelo de MediaPipe Pose:

- **Punto A (Origen / Referencia):** Cadera (`LEFT_HIP` - ID 23)
- **Punto B (Vértice Articular):** Hombro (`LEFT_SHOULDER` - ID 11)
- **Punto C (Segmento Móvil):** Codo (`LEFT_ELBOW` - ID 13)

### Formulación Matemática
Dados los vectores $\vec{u} = \vec{BA}$ y $\vec{v} = \vec{BC}$, el ángulo articular $\theta$ se calcula a partir del producto escalar:

$$\theta = \arccos\left( \frac{\vec{u} \cdot \vec{v}}{\Vert{}\vec{u}\Vert{} \Vert{}\vec{v}\Vert{}} \right) \times \left( \frac{180}{\pi} \right)$$

---

## 💻 Requisitos y Dependencias

Para la ejecución de la plataforma no se requiere instalación previa de entornos de desarrollo complejos, ya que todas las dependencias son importadas vía CDN:

* **Frameworks y Librerías:**
  * `@mediapipe/pose` (v0.5) - Extracción e inferencia de keypoints anatómicos.
  * `@mediapipe/camera_utils` (v0.4) - Manejo de streams de video y cámara.
  * `chart.js` (v4.x) - Visualización gráfica de la evolución angular.
* **Compatibilidad de Navegadores:**
  * Funciona en Safari (iOS/iPadOS), Google Chrome, Microsoft Edge y Firefox con soporte para WebGL y permisos de cámara sobre protocolo **HTTPS**.

---

## 📖 Guía de Uso Clínico

1. **Inclusión del Paciente:** Colocar al paciente/sujeto a una distancia de entre **1.5 y 2.0 metros** frente a la cámara de la tablet/computadora.
2. **Plano de Evaluación:**
   * **Abducción:** Sujeto en *plano frontal* (mirando directamente a la cámara).
   * **Flexión:** Sujeto en *plano sagital* (de perfil a la cámara).
3. **Inicio de la Prueba:** Abrir la web y aceptar los permisos de uso de la cámara.
4. **Ejecución del Movimiento:** Realizar la elevación máxima del brazo de forma pausada.
5. **Lectura de Resultados:** Observar el valor máximo en la casilla **ROM Máximo** y analizar la fluidez de la curva angular en la gráfica inferior.
6. **Reinicio:** Presionar el botón **Reiniciar Peak** para comenzar una nueva repetición o evaluar el brazo contralateral.
