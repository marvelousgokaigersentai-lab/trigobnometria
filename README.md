<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Momento de Inercia en Coronas Circulares — Ingeniería Industrial</title>
  
  <!-- FontAwesome Icons -->
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
  
  <!-- Estilos del Proyecto -->
  <link rel="stylesheet" href="style.css">
  
  <!-- Configuración de MathJax para Fórmulas LaTeX -->
  <script>
    window.MathJax = {
      tex: {
        inlineMath: [['\\(', '\\)']],
        displayMath: [['\\[', '\\]']]
      },
      svg: { fontCache: 'global' },
      startup: {
        ready: () => {
          MathJax.startup.defaultReady();
        }
      }
    };
  </script>
  <script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-svg.js"></script>
</head>
<body>

  <!-- Enlace de Accesibilidad -->
  <a href="#main-content" class="skip-link">Saltar al contenido principal</a>

  <div class="app-container">
    
    <!-- Cabecera Principal -->
    <header class="main-header">
      <h1>MOMENTOS DE INERCIA EN CORONAS CIRCULARES</h1>
      <p>Optimización Geométrica y Resistencia Mecánica en Volantes de Inercia para Ingeniería Industrial</p>
    </header>

    <!-- Navegación por Pestañas (Blooms) -->
    <nav role="tablist" aria-label="Pestañas del panel educativo" class="tabs-navigation">
      <button role="tab" aria-selected="true" aria-controls="tab-lab" id="tab-btn-lab" tabindex="0" class="tab-btn">
        <i class="fa-solid fa-flask-bubble"></i> 1. Intro & Lab
      </button>
      <button role="tab" aria-selected="false" aria-controls="tab-classification" id="tab-btn-classification" tabindex="-1" class="tab-btn">
        <i class="fa-solid fa-sliders"></i> 2. Clasificación
      </button>
      <button role="tab" aria-selected="false" aria-controls="tab-properties" id="tab-btn-properties" tabindex="-1" class="tab-btn">
        <i class="fa-solid fa-book-bookmark"></i> 3. Propiedades
      </button>
      <button role="tab" aria-selected="false" aria-controls="tab-elements" id="tab-btn-elements" tabindex="-1" class="tab-btn">
        <i class="fa-solid fa-bezier-curve"></i> 4. Elementos
      </button>
      <button role="tab" aria-selected="false" aria-controls="tab-engineering" id="tab-btn-engineering" tabindex="-1" class="tab-btn">
        <i class="fa-solid fa-industry"></i> 5. Ingeniería
      </button>
      <button role="tab" aria-selected="false" aria-controls="tab-interactive-ex" id="tab-btn-interactive-ex" tabindex="-1" class="tab-btn">
        <i class="fa-solid fa-graduation-cap"></i> 6. Ejercicios Interactivos
      </button>
      <button role="tab" aria-selected="false" aria-controls="tab-proposed-ex" id="tab-btn-proposed-ex" tabindex="-1" class="tab-btn">
        <i class="fa-solid fa-pen-ruler"></i> 7. Ejercicios Propuestos
      </button>
    </nav>

    <!-- Contenedor Principal de Contenido -->
    <main id="main-content">

      <!-- PESTAÑA 1: INTRO & LAB (Recordar/Entender) -->
      <section role="tabpanel" id="tab-lab" aria-labelledby="tab-btn-lab" class="tab-panel active">
        <div class="grid-two-columns">
          
          <!-- Controles del Laboratorio -->
          <div class="control-panel">
            <div class="glass-card">
              <h2 class="glass-card-title"><i class="fa-solid fa-gears"></i> Parámetros de Diseño</h2>
              
              <!-- Slider R -->
              <div class="control-group">
                <div class="control-label">
                  <span>Radio Exterior (R)</span>
                  <span id="label-R" class="control-value">10.0 cm</span>
                </div>
                <input type="range" id="input-R" class="custom-range" min="5" max="20" step="0.5" value="10" aria-valuemin="5" aria-valuemax="20" aria-valuenow="10">
              </div>

              <!-- Slider r -->
              <div class="control-group">
                <div class="control-label">
                  <span>Radio Interior (r)</span>
                  <span id="label-r" class="control-value">5.0 cm</span>
                </div>
                <input type="range" id="input-r" class="custom-range" min="0" max="19" step="0.1" value="5" aria-valuemin="0" aria-valuemax="19" aria-valuenow="5">
              </div>

              <!-- Selector de Acoplamiento -->
              <div class="control-group">
                <label for="select-lados" class="control-label">
                  <span>Acople Central (Polígono)</span>
                </label>
                <select id="select-lados" class="btn btn-sm" style="width: 100%; background: rgba(15, 23, 42, 0.4); text-align: left; padding: 10px;">
                  <option value="4" selected>Cuadrado (4 lados - Diseño Crítico)</option>
                  <option value="6">Hexágono (6 lados - Alternativo)</option>
                  <option value="8">Octágono (8 lados - Alternativo)</option>
                </select>
              </div>

              <!-- Slider Velocidad de Rotación -->
              <div class="control-group">
                <div class="control-label">
                  <span>Velocidad de Giro (&omega;)</span>
                  <span id="label-omega" class="control-value">10 rad/s</span>
                </div>
                <input type="range" id="input-omega" class="custom-range" min="0" max="50" step="2" value="10" aria-valuemin="0" aria-valuemax="50" aria-valuenow="10">
              </div>
            </div>

            <!-- Estado de Seguridad -->
            <div class="glass-card">
              <h2 class="glass-card-title"><i class="fa-solid fa-shield-halved"></i> Estado Estructural</h2>
              <div id="status-badge" class="status-badge safe">
                <i class="fa-solid fa-circle-check"></i> Estructura Segura
              </div>
              <p style="font-size: 0.85rem; color: var(--text-secondary); line-height: 1.4;">
                La integridad del volante es segura mientras el canal interior \(r\) no corte los vértices del acoplamiento poligonal (\(r \le a\)).
              </p>
            </div>
          </div>

          <!-- Visualización y Métricas -->
          <div class="visual-panel">
            <div class="glass-card" style="padding: 15px; margin-bottom: 20px;">
              <div class="canvas-wrapper">
                <canvas id="canvas-lab" role="img" aria-label="Visualización interactiva en 2D de la corona circular en rotación, mostrando los radios exterior e interior, la fuerza centrífuga en los vértices del acople inscrito, y el estado estructural del sistema."></canvas>
              </div>
            </div>

            <!-- Panel de Métricas de Ingeniería -->
            <div class="glass-card">
              <h2 class="glass-card-title"><i class="fa-solid fa-chart-line"></i> Indicadores de Rendimiento (Métricas)</h2>
              <div class="metrics-display">
                <div class="metric-card">
                  <div class="metric-label">Área de la Corona (\(A\))</div>
                  <div id="metric-area" class="metric-value">235.6 cm²</div>
                </div>
                <div class="metric-card">
                  <div class="metric-label">Inercia Polar (\(J\))</div>
                  <div id="metric-inertia" class="metric-value">14726.2 cm⁴</div>
                </div>
                <div class="metric-card">
                  <div class="metric-label">Ahorro de Masa</div>
                  <div id="metric-mass-saving" class="metric-value" style="color: var(--accent);">25.0%</div>
                </div>
                <div class="metric-card">
                  <div class="metric-label">Inercia Retenida</div>
                  <div id="metric-inertia-retention" class="metric-value" style="color: var(--secondary);">93.8%</div>
                </div>
              </div>
              
              <div class="metric-card" style="margin-top: 15px; text-align: left; display: flex; justify-content: space-between; align-items: center;">
                <div>
                  <div class="metric-label" style="text-align: left;">Apotema del Acople (\(a\))</div>
                  <div style="font-size: 0.85rem; color: var(--text-secondary);">Límite estructural para radio interior (\(r_{\text{máx}}\))</div>
                </div>
                <div id="metric-apothem" class="metric-value" style="color: var(--warning);">7.07 cm</div>
              </div>
            </div>
          </div>
          
        </div>
      </section>

      <!-- PESTAÑA 2: CLASIFICACIÓN (Comprender) -->
      <section role="tabpanel" id="tab-classification" aria-labelledby="tab-btn-classification" class="tab-panel">
        <div class="glass-card">
          <h2 class="glass-card-title"><i class="fa-solid fa-shapes"></i> Clasificación de Diseños Industriales</h2>
          <p style="color: var(--text-secondary); margin-bottom: 20px;">
            El equilibrio entre masa, momento de inercia y estabilidad mecánica define las cuatro clases principales de componentes de transmisión. Haz clic en cualquiera de ellos para cargar sus parámetros de forma automática en el laboratorio de pruebas de la primera pestaña.
          </p>

          <div class="classification-grid">
            <!-- Caso 1: Disco Sólido -->
            <div class="class-card class-safe" data-preset="solid">
              <div class="class-card-header">
                <span class="class-title">Disco Sólido</span>
                <span class="class-status-dot"></span>
              </div>
              <p class="class-desc">Estructura maciza sin cavidad central (\(r = 0\)). Máxima seguridad pero ineficiente en términos de inercia/peso.</p>
              <div class="class-metrics">
                <div class="class-metric-row"><span>Relación r/R:</span> <strong>0.00</strong></div>
                <div class="class-metric-row"><span>Ahorro Masa:</span> <strong style="color: var(--danger);">0.0%</strong></div>
                <div class="class-metric-row"><span>Inercia Retenida:</span> <strong>100%</strong></div>
                <div class="class-metric-row"><span>Estado:</span> <span style="color: var(--accent);">Estable</span></div>
              </div>
            </div>

            <!-- Caso 2: Corona Óptima -->
            <div class="class-card class-safe" data-preset="optimal">
              <div class="class-card-header">
                <span class="class-title">Corona Óptima</span>
                <span class="class-status-dot"></span>
              </div>
              <p class="class-desc">Punto de balance geométrico de diseño (\(r/R = 0.707\)). Remueve el 50% de la masa y retiene el 75% de inercia sin fallar.</p>
              <div class="class-metrics">
                <div class="class-metric-row"><span>Relación r/R:</span> <strong>0.71</strong></div>
                <div class="class-metric-row"><span>Ahorro Masa:</span> <strong style="color: var(--accent);">50.0%</strong></div>
                <div class="class-metric-row"><span>Inercia Retenida:</span> <strong>75.0%</strong></div>
                <div class="class-metric-row"><span>Estado:</span> <span style="color: var(--accent);">Excelente</span></div>
              </div>
            </div>

            <!-- Caso 3: Corona Delgada -->
            <div class="class-card class-fail" data-preset="thin">
              <div class="class-card-header">
                <span class="class-title">Corona Delgada</span>
                <span class="class-status-dot"></span>
              </div>
              <p class="class-desc">Diseño al límite o superando la seguridad de soporte (\(r/R = 0.85\)). Reducción drástica de peso pero con fractura del acoplamiento.</p>
              <div class="class-metrics">
                <div class="class-metric-row"><span>Relación r/R:</span> <strong>0.85</strong></div>
                <div class="class-metric-row"><span>Ahorro Masa:</span> <strong style="color: var(--accent);">72.3%</strong></div>
                <div class="class-metric-row"><span>Inercia Retenida:</span> <strong>47.8%</strong></div>
                <div class="class-metric-row"><span>Estado:</span> <span style="color: var(--danger);">FALLA</span></div>
              </div>
            </div>

            <!-- Caso 4: Anillo Ultrafino -->
            <div class="class-card class-fail" data-preset="ultrathin">
              <div class="class-card-header">
                <span class="class-title">Anillo Ultrafino</span>
                <span class="class-status-dot"></span>
              </div>
              <p class="class-desc">Anillo de pared sumamente delgada (\(r/R = 0.95\)). Remueve casi todo el peso, pero destruye instantáneamente el soporte del acople.</p>
              <div class="class-metrics">
                <div class="class-metric-row"><span>Relación r/R:</span> <strong>0.95</strong></div>
                <div class="class-metric-row"><span>Ahorro Masa:</span> <strong style="color: var(--accent);">90.3%</strong></div>
                <div class="class-metric-row"><span>Inercia Retenida:</span> <strong>18.5%</strong></div>
                <div class="class-metric-row"><span>Estado:</span> <span style="color: var(--danger);">FALLA</span></div>
              </div>
            </div>
          </div>
        </div>
      </section>

      <!-- PESTAÑA 3: PROPIEDADES (Aplicar) -->
      <section role="tabpanel" id="tab-properties" aria-labelledby="tab-btn-properties" class="tab-panel">
        <div class="glass-card">
          <h2 class="glass-card-title"><i class="fa-solid fa-graduation-cap"></i> Principios Teóricos y Fórmulas Matemáticas</h2>
          
          <div class="theory-section">
            <h3>1. El Área y la Distribución de Masa</h3>
            <p>
              En ingeniería industrial, el peso de los componentes giratorios está directamente ligado al costo del material y a la carga sobre los cojinetes. Para una corona circular con radio exterior \(R\) e interior \(r\), el área de la sección transversal representa la masa por unidad de espesor y densidad:
            </p>
            <div class="theory-formula">
              \[A = \pi(R^2 - r^2)\]
            </div>
          </div>

          <div class="theory-section">
            <h3>2. Momento Polar de Inercia (\(J\)) y su Factorización</h3>
            <p>
              El momento polar de inercia mide la resistencia de un cuerpo a la aceleración angular respecto a un eje perpendicular a su plano. Para una corona circular:
            </p>
            <div class="theory-formula">
              \[J = \frac{\pi}{2}(R^4 - r^4)\]
            </div>
            <p>
              Haciendo uso de la diferencia de cuadrados en álgebra (\(a^2 - b^2 = (a-b)(a+b)\)), podemos factorizar esta expresión:
            </p>
            <div class="theory-formula">
              \[R^4 - r^4 = (R^2 - r^2)(R^2 + r^2)\]
            </div>
            <p>
              Si sustituimos la fórmula del área (\(A = \pi(R^2 - r^2)\)), obtenemos una relación sumamente útil para optimización industrial:
            </p>
            <div class="theory-formula">
              \[J = \frac{A}{2}(R^2 + r^2)\]
            </div>
            <p>
              <strong>Conclusión ingenieril:</strong> Para un área fija \(A\) (masa constante), el momento polar \(J\) se maximiza expandiendo tanto el radio exterior \(R\) como el radio interior \(r\) al máximo posible, reduciendo el espesor de pared.
            </p>
          </div>

          <div class="theory-section">
            <h3>3. Límites Estructurales del Acople Central</h3>
            <p>
              Si el espesor del anillo se reduce excesivamente, la corona no puede albergar un acoplamiento central (como un eje de sección cuadrada) para transmitir el torque. La distancia del centro a los lados planos del acople es la apotema (\(a\)). En un cuadrado inscrito en el círculo exterior de radio \(R\):
            </p>
            <div class="theory-formula">
              \[a = R \cos(45^\circ) = R \frac{\sqrt{2}}{2} \approx 0.7071 \cdot R\]
            </div>
            <p>
              Si el radio interior \(r > a\), el hueco del centro corta el acoplamiento plano, debilitando catastróficamente la resistencia del cubo central ante fuerzas centrífugas y de torque:
            </p>
            <div class="theory-formula">
              \[r_{\text{límite}} = 0.7071 \cdot R\]
            </div>
          </div>

          <div class="theory-section">
            <h3>4. Disipación Térmica (Perímetro)</h3>
            <p>
              Los embragues y volantes de inercia disipan gran cantidad de calor generado por fricción. La capacidad de enfriamiento es proporcional al área superficial expuesta. Para un disco plano, el perímetro mojado exterior e interior define la transferencia por convección:
            </p>
            <div class="theory-formula">
              \[P = 2\pi(R + r)\]
            </div>
            <p>
              Con la relación óptima de diseño (\(r = 0.707 R\)), el perímetro es un 70% mayor que el de un eje macizo (\(2\pi R\)), proporcionando una disipación térmica excelente.
            </p>
          </div>
        </div>
      </section>

      <!-- PESTAÑA 4: ELEMENTOS (Anatomía) -->
      <section role="tabpanel" id="tab-elements" aria-labelledby="tab-btn-elements" class="tab-panel">
        <div class="grid-two-columns">
          
          <!-- Lista de Elementos Interactivos -->
          <div class="control-panel">
            <div class="glass-card">
              <h2 class="glass-card-title"><i class="fa-solid fa-circle-nodes"></i> Anatomía de la Corona</h2>
              <p style="font-size: 0.85rem; color: var(--text-secondary); margin-bottom: 15px;">
                Coloca el cursor o haz clic en cualquiera de los elementos geométricos listados para visualizarlos y aislarlos dinámicamente en el esquema técnico.
              </p>

              <div class="anatomy-list">
                <!-- Radio Exterior -->
                <div class="anatomy-item active" data-element="radio-ext">
                  <div class="anatomy-bullet"></div>
                  <div>
                    <div class="anatomy-item-title">Radio Exterior (\(R\))</div>
                    <p style="font-size: 0.75rem; color: var(--text-secondary);">Distancia del centro al extremo externo de la corona.</p>
                  </div>
                </div>

                <!-- Radio Interior -->
                <div class="anatomy-item" data-element="radio-int">
                  <div class="anatomy-bullet"></div>
                  <div>
                    <div class="anatomy-item-title">Radio Interior (\(r\))</div>
                    <p style="font-size: 0.75rem; color: var(--text-secondary);">Define el límite de la cavidad o agujero interno.</p>
                  </div>
                </div>

                <!-- Apotema -->
                <div class="anatomy-item" data-element="apotema">
                  <div class="anatomy-bullet"></div>
                  <div>
                    <div class="anatomy-item-title">Apotema (\(a\))</div>
                    <p style="font-size: 0.75rem; color: var(--text-secondary);">Distancia perpendicular del centro a la cara del acople plano.</p>
                  </div>
                </div>

                <!-- Corona Circular -->
                <div class="anatomy-item" data-element="corona">
                  <div class="anatomy-bullet"></div>
                  <div>
                    <div class="anatomy-item-title">Corona Sólida</div>
                    <p style="font-size: 0.75rem; color: var(--text-secondary);">Área de material estructural (\(A = \pi(R^2 - r^2)\)).</p>
                  </div>
                </div>

                <!-- Acoplamiento -->
                <div class="anatomy-item" data-element="acople">
                  <div class="anatomy-bullet"></div>
                  <div>
                    <div class="anatomy-item-title">Polígono Inscrito (Acople)</div>
                    <p style="font-size: 0.75rem; color: var(--text-secondary);">Límites planos de la sujeción del cubo o chaveta de torque.</p>
                  </div>
                </div>
              </div>
            </div>
          </div>

          <!-- Canvas para Anatomía -->
          <div class="visual-panel">
            <div class="glass-card" style="padding: 15px;">
              <div class="canvas-wrapper">
                <canvas id="canvas-elements" role="img" aria-label="Dibujo técnico detallado que señala y desglosa los elementos de la corona circular, incluyendo los radios, el apotema y la sección de acoplamiento."></canvas>
              </div>
            </div>
          </div>
          
        </div>
      </section>

      <!-- PESTAÑA 5: INGENIERÍA / PRÁCTICA (Evaluar) -->
      <section role="tabpanel" id="tab-engineering" aria-labelledby="tab-btn-engineering" class="tab-panel">
        <div class="glass-card">
          <h2 class="glass-card-title"><i class="fa-solid fa-industry"></i> Aplicaciones Prácticas en la Industria</h2>
          <p style="color: var(--text-secondary); margin-bottom: 25px;">
            El análisis del momento de inercia polar y las restricciones de acoplamiento plano se aplican en diversos campos clave de la ingeniería mecánica e industrial moderna.
          </p>

          <div class="engineering-card-grid">
            <!-- Aplicación 1 -->
            <div class="engineering-card">
              <div class="engineering-icon"><i class="fa-solid fa-rotate"></i></div>
              <h3>Volantes de Inercia (Flywheels)</h3>
              <p>
                Utilizados en motores alternativos y prensas de estampado para amortiguar las fluctuaciones de velocidad almacenando energía cinética. El volante óptimo (\(r = 0.707 R\)) maximiza la energía almacenada reduciendo a la mitad el peso del motor, mejorando la respuesta dinámica y el ahorro energético.
              </p>
            </div>

            <!-- Aplicación 2 -->
            <div class="engineering-card">
              <div class="engineering-icon"><i class="fa-solid fa-cogs"></i></div>
              <h3>Gears de Transmisiones Planetarias</h3>
              <p>
                Las coronas dentadas exteriores en cajas de cambio automáticas e industriales requieren una optimización de espesor. El análisis geométrico define el límite crítico de su espesor antes de que los esfuerzos radiales de los engranajes satélites deformen plásticamente el aro exterior.
              </p>
            </div>

            <!-- Aplicación 3 -->
            <div class="engineering-card">
              <div class="engineering-icon"><i class="fa-solid fa-bolt"></i></div>
              <h3>Sistemas KERS (Fórmula 1)</h3>
              <p>
                Los volantes de inercia avanzados de fibra de carbono giran a más de 60,000 RPM para almacenar energía eléctrica en frenados. Para evitar la rotura por fuerza centrífuga, su geometría debe seguir de forma estricta el límite de relación de radios e incorporar cubos interiores de titanio.
              </p>
            </div>

            <!-- Aplicación 4 -->
            <div class="engineering-card">
              <div class="engineering-icon"><i class="fa-solid fa-fire-flame-simple"></i></div>
              <h3>Discos de Freno Ventilados</h3>
              <p>
                Los frenos disipan energía cinética en forma de calor. Las coronas circulares de frenado están diseñadas con canales interiores de ventilación. La relación óptima maximiza el flujo de aire convectivo (perímetro interior) y la masa de frenado (área sólida) para evitar el agrietamiento térmico.
              </p>
            </div>
          </div>
        </div>
      </section>

      <!-- PESTAÑA 6: EJERCICIOS INTERACTIVOS (Crear) -->
      <section role="tabpanel" id="tab-interactive-ex" aria-labelledby="tab-btn-interactive-ex" class="tab-panel">
        <div class="grid-two-columns">
          
          <!-- Listado y Enunciado del Ejercicio -->
          <div class="control-panel">
            <div class="glass-card">
              <h2 class="glass-card-title"><i class="fa-solid fa-list-check"></i> Ejercicios Guiados</h2>
              <div class="exercise-selector-panel">
                <span style="font-size: 0.8rem; font-weight: 600; color: var(--text-secondary);">Selecciona un Problema:</span>
                
                <div class="exercise-selector-list" id="exercise-list-container">
                  <!-- JS inyectará aquí los 12 botones de ejercicios E1 a E12 -->
                </div>
              </div>
            </div>

            <div class="glass-card" id="exercise-statement-card">
              <span id="ex-difficulty" class="difficulty-badge diff-basico">Básico</span>
              <h3 id="ex-title" style="margin-bottom: 10px; font-family: var(--font-title); font-weight: 800;">Ejercicio 1: Cálculo del Área Básica</h3>
              <p id="ex-statement" style="font-size: 0.9rem; color: var(--text-secondary); line-height: 1.5; margin-bottom: 15px;">
                Cargando enunciado...
              </p>
              
              <!-- Pasos del ejercicio -->
              <div class="exercise-steps-container" id="exercise-steps-container">
                <!-- JS inyectará los pasos del ejercicio activo aquí -->
              </div>

              <!-- Navegación del Ejercicio -->
              <div class="exercise-navigation">
                <button class="btn btn-sm" id="btn-ex-prev"><i class="fa-solid fa-arrow-left"></i> Anterior</button>
                <span id="ex-step-indicator" style="font-family: var(--font-title); font-weight: 700; font-size: 0.85rem; color: var(--text-secondary);">Paso 1 / 3</span>
                <button class="btn btn-sm btn-primary" id="btn-ex-next">Siguiente <i class="fa-solid fa-arrow-right"></i></button>
              </div>
            </div>
          </div>

          <!-- Lienzo Técnico del Ejercicio -->
          <div class="visual-panel">
            <div class="glass-card" style="padding: 15px; margin-bottom: 20px;">
              <div class="canvas-wrapper">
                <canvas id="canvas-exercises" role="img" aria-label="Esquema técnico dinámico que dibuja los elementos del ejercicio seleccionado y se actualiza de acuerdo al paso actual de la resolución paso a paso."></canvas>
              </div>
            </div>
            
            <!-- Tarjeta de Ayuda Pedagógica -->
            <div class="glass-card">
              <h3 class="glass-card-title"><i class="fa-solid fa-lightbulb" style="color: var(--warning);"></i> Pista Pedagógica</h3>
              <p id="ex-pedagogical-hint" style="font-size: 0.85rem; color: var(--text-secondary); line-height: 1.4;">
                Cargando pista...
              </p>
            </div>
          </div>
          
        </div>
      </section>

      <!-- PESTAÑA 7: EJERCICIOS PROPUESTOS (Crear) -->
      <section role="tabpanel" id="tab-proposed-ex" aria-labelledby="tab-btn-proposed-ex" class="tab-panel">
        <div class="glass-card">
          <h2 class="glass-card-title"><i class="fa-solid fa-pen-fancy"></i> Ejercicios de Autoevaluación</h2>
          <p style="color: var(--text-secondary); margin-bottom: 25px;">
            Resuelve los siguientes 12 ejercicios de nivel universitario para evaluar tu comprensión sobre la geometría y resistencia mecánica de las coronas circulares. Despliega cada acordeón para contrastar tu planteamiento con la solución detallada en código LaTeX.
          </p>

          <div class="proposed-list" id="proposed-list-container">
            <!-- JS inyectará dinámicamente aquí los 12 acordeones de ejercicios propuestos -->
          </div>
        </div>
      </section>

    </main>

    <!-- Footer de la Aplicación -->
    <footer class="app-footer">
      <p>&copy; 2026 Plataforma Educativa STEM. Todos los derechos reservados.</p>
      <p style="font-size: 0.75rem; margin-top: 5px; color: var(--text-muted);">
        Diseñado bajo los principios del Handoff IA y WCAG 2.1 Nivel AA.
      </p>
    </footer>

  </div>

  <!-- Carga del Controlador Principal de la Aplicación (Module) -->
  <script type="module" src="app.js"></script>
</body>
</html>
