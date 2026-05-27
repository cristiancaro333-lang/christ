<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>SISTEMA DE MATRÍCULA UNIVERSAL 2026</title>
    <style>
        /* --- ESTILOS GENERALES Y PALETA DE COLORES --- */
        :root {
            --primary-color: #1e3a8a; /* Azul Universitario */
            --secondary-color: #0284c7; /* Celeste */
            --accent-color: #10b981; /* Verde Éxito */
            --danger-color: #ef4444; /* Rojo Eliminar */
            --dark-bg: #0f172a;
            --light-bg: #f8fafc;
            --text-color: #334155;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background: linear-gradient(135deg, #e2e8f0 0%, #cbd5e1 100%);
            color: var(--text-color);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
        }

        .container {
            background-color: white;
            width: 100%;
            max-width: 1000px;
            border-radius: 16px;
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.15);
            overflow: hidden;
            transition: all 0.3s ease;
        }

        /* --- PANTALLA DE LOGIN --- */
        .login-card {
            max-width: 450px;
            margin: auto;
            padding: 40px;
            text-align: center;
        }

        .login-card h2 {
            color: var(--primary-color);
            margin-bottom: 10px;
            font-size: 24px;
        }

        .login-card p {
            color: #64748b;
            margin-bottom: 30px;
            font-size: 14px;
        }

        /* --- COMPONENTES DE FORMULARIO --- */
        .form-group {
            margin-bottom: 20px;
            text-align: left;
        }

        .form-group label {
            display: block;
            margin-bottom: 8px;
            font-weight: 600;
            font-size: 14px;
            color: #475569;
        }

        .form-group input, .form-group select {
            width: 100%;
            padding: 12px;
            border: 2px solid #cbd5e1;
            border-radius: 8px;
            font-size: 15px;
            outline: none;
            transition: border-color 0.2s;
        }

        .form-group input:focus, .form-group select:focus {
            border-color: var(--secondary-color);
        }

        button {
            width: 100%;
            background-color: var(--primary-color);
            color: white;
            padding: 12px;
            border: none;
            border-radius: 8px;
            font-size: 16px;
            font-weight: bold;
            cursor: pointer;
            transition: background-color 0.2s, transform 0.1s;
        }

        button:hover {
            background-color: #172554;
        }

        button:active {
            transform: scale(0.98);
        }

        /* --- PANEL PRINCIPAL (OCULTO POR DEFECTO) --- */
        .dashboard {
            display: none; /* Se activa con JS */
        }

        header {
            background-color: var(--primary-color);
            color: white;
            padding: 20px 30px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        header h1 {
            font-size: 20px;
            letter-spacing: 1px;
        }

        .logout-btn {
            background-color: transparent;
            border: 2px solid white;
            padding: 6px 15px;
            width: auto;
            font-size: 14px;
        }

        .logout-btn:hover {
            background-color: white;
            color: var(--primary-color);
        }

        .main-content {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 30px;
            padding: 30px;
        }

        @media (max-width: 768px) {
            .main-content {
                grid-template-columns: 1fr;
            }
        }

        .card {
            background: #f8fafc;
            border: 1px solid #e2e8f0;
            border-radius: 12px;
            padding: 24px;
        }

        .card h3 {
            color: var(--primary-color);
            margin-bottom: 20px;
            border-bottom: 2px solid #e2e8f0;
            padding-bottom: 8px;
        }

        /* --- TABLAS Y DISEÑO DE HORARIOS --- */
        .table-container {
            overflow-x: auto;
        }

        table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 10px;
            background: white;
        }

        th, td {
            padding: 12px;
            text-align: left;
            border-bottom: 1px solid #e2e8f0;
            font-size: 14px;
        }

        th {
            background-color: #f1f5f9;
            color: #475569;
            font-weight: 600;
        }

        .btn-delete {
            background-color: var(--danger-color);
            padding: 6px 10px;
            font-size: 12px;
            width: auto;
        }

        .btn-delete:hover {
            background-color: #b91c1c;
        }

        /* --- SECCIÓN DE PAGOS --- */
        .pago-row {
            display: flex;
            justify-content: space-between;
            margin-bottom: 12px;
            font-size: 15px;
        }

        .pago-total {
            border-top: 2px dashed #cbd5e1;
            margin-top: 15px;
            padding-top: 15px;
            font-size: 18px;
            font-weight: bold;
            color: var(--accent-color);
        }

        .alert-descuento {
            background-color: #d1fae5;
            color: #065f46;
            padding: 10px;
            border-radius: 6px;
            font-size: 13px;
            margin-top: 15px;
            text-align: center;
            font-weight: 500;
        }

        .autores {
            text-align: center;
            padding: 15px;
            font-size: 12px;
            color: #94a3b8;
            background: #f1f5f9;
            border-top: 1px solid #e2e8f0;
        }
    </style>
</head>
<body>

    <div class="container">
        
        <div id="loginSection" class="login-card">
            <h2>SISTEMA DE MATRÍCULA</h2>
            <p>Por favor, inicia sesión para gestionar tus asignaturas.</p>
            
            <form id="loginForm" onsubmit="iniciarSesion(event)">
                <div class="form-group">
                    <label for="usuario">Usuario / Código Estudiantil</label>
                    <input type="text" id="usuario" placeholder="Ej: JorgeG2026" required>
                </div>
                <div class="form-group">
                    <label for="password">Contraseña</label>
                    <input type="password" id="password" placeholder="••••••••" required>
                </div>
                <button type="submit">Ingresar al Sistema</button>
            </form>
            <div style="margin-top: 15px; font-size: 11px; color: #94a3b8;">
                *Nota: Puedes ingresar usando cualquier usuario y contraseña para pruebas.
            </div>
        </div>

        <div id="dashboardSection" class="dashboard">
            <header>
                <div>
                    <h1>SISTEMA UNIVERSAL DE MATRÍCULA 2026</h1>
                    <small>Estudiante: <span id="nombreEstudiante" style="font-weight: bold; color: var(--secondary-color);"></span></small>
                </div>
                <button class="logout-btn" onclick="cerrarSesion()">Cerrar Sesión</button>
            </header>

            <div class="main-content">
                <div class="card">
                    <h3>1. Registrar Nueva Materia</h3>
                    <form id="materiaForm" onsubmit="registrarMateria(event)">
                        <div class="form-group">
                            <label for="nomMateria">Nombre de la Asignatura</label>
                            <input type="text" id="nomMateria" placeholder="Ej: Cálculo Integral" required>
                        </div>
                        
                        <div class="form-group">
                            <label for="diaMateria">Día de la semana</label>
                            <select id="diaMateria" required>
                                <option value="">Seleccione un día...</option>
                                <option value="Lunes">Lunes</option>
                                <option value="Martes">Martes</option>
                                <option value="Miércoles">Miércoles</option>
                                <option value="Jueves">Jueves</option>
                                <option value="Viernes">Viernes</option>
                                <option value="Sábado">Sábado</option>
                            </select>
                        </div>

                        <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 10px;">
                            <div class="form-group">
                                <label for="horaInicio">Hora Inicio (24h)</label>
                                <input type="number" id="horaInicio" min="6" max="22" placeholder="Ej: 8" required>
                            </div>
                            <div class="form-group">
                                <label for="horaFin">Hora Fin (24h)</label>
                                <input type="number" id="horaFin" min="7" max="23" placeholder="Ej: 10" required>
                            </div>
                        </div>

                        <div class="form-group">
                            <label for="creditosMateria">Número de Créditos</label>
                            <input type="number" id="creditosMateria" min="1" max="6" placeholder="Ej: 3" required>
                        </div>

                        <button type="submit" style="background-color: var(--secondary-color);">Guardar Materia</button>
                    </form>
                </div>

                <div class="card">
                    <h3>2. Resumen de Pago Liquidado</h3>
                    <div id="resumenPago">
                        <div class="pago-row">
                            <span>Total Créditos:</span>
                            <span id="pagoCreditos" style="font-weight: bold;">0</span>
                        </div>
                        <div class="pago-row">
                            <span>Valor por Crédito:</span>
                            <span>$120.000</span>
                        </div>
                        <div class="pago-row">
                            <span>Subtotal:</span>
                            <span id="pagoSubtotal">$0</span>
                        </div>
                        <div class="pago-row" style="color: var(--danger-color);">
                            <span>Descuento (10% por >10 créd.):</span>
                            <span id="pagoDescuento">-$0</span>
                        </div>
                        <div class="pago-row pago-total">
                            <span>TOTAL A PAGAR:</span>
                            <span id="pagoTotal">$0</span>
                        </div>
                    </div>
                    <div id="alertaDescuento" class="alert-descuento" style="display: none;">
                        🎉 ¡Felicidades! Se ha aplicado el 10% de descuento por superar los 10 créditos.
                    </div>
                </div>

                <div class="card" style="grid-column: 1 / -1;">
                    <h3>3. Mi Horario de Clases Actual</h3>
                    <div class="table-container">
                        <table>
                            <thead>
                                <tr>
                                    <th>Asignatura</th>
                                    <th>Día</th>
                                    <th>Horario</th>
                                    <th>Créditos</th>
                                    <th>Acción</th>
                                </tr>
                            </thead>
                            <tbody id="tablaMaterias">
                                <tr>
                                    <td colspan="5" style="text-align: center; color: #94a3b8;">No tienes materias registradas aún.</td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>
        </div>

        <div class="autores">
            Desarrollado por: <strong>Jorge Garcia - Nelson Peñates</strong> &copy; 2026
        </div>
    </div>

    <script>
        // Estructuras de datos (Vectores paralelos como en su código de Python)
        let nombres = [];
        let dias = [];
        let horas_inicio = [];
        let horas_fin = [];
        let creditos = [];

        // Constantes del negocio
        const VALOR_CREDITO = 120000;

        // 1. CONTROL DE SESIÓN
        function iniciarSesion(event) {
            event.preventDefault(); // Evita que la página se recargue
            
            const usuarioInput = document.getElementById('usuario').value;
            
            // Simulación de login exitoso
            document.getElementById('nombreEstudiante').innerText = usuarioInput;
            document.getElementById('loginSection').style.display = 'none';
            document.getElementById('dashboardSection').style.display = 'block';
        }

        function cerrarSesion() {
            // Limpiar datos al salir
            nombres = []; dias = []; horas_inicio = []; horas_fin = []; creditos = [];
            actualizarTabla();
            actualizarPago();
            document.getElementById('loginForm').reset();
            
            // Alternar pantallas
            document.getElementById('dashboardSection').style.display = 'none';
            document.getElementById('loginSection').style.display = 'block';
        }

        // 2. REGISTRAR MATERIA
        function registrarMateria(event) {
            event.preventDefault();

            const nom = document.getElementById('nomMateria').value;
            const d = document.getElementById('diaMateria').value;
            const h_i = parseInt(document.getElementById('horaInicio').value);
            const h_f = parseInt(document.getElementById('horaFin').value);
            const cre = parseInt(document.getElementById('creditosMateria').value);

            // Validación de lógica horaria básica
            if (h_i >= h_f) {
                alert("Error: La hora de inicio no puede ser mayor o igual a la hora de fin.");
                return;
            }

            // Guardar en los arreglos (Similares al .append de Python)
            nombres.push(nom);
            dias.push(d);
            horas_inicio.push(h_i);
            horas_fin.push(h_f);
            creditos.push(cre);

            // Limpiar el formulario y refrescar interfaz
            document.getElementById('materiaForm').reset();
            actualizarTabla();
            actualizarPago();
        }

        // 3. BORRAR MATERIA (Uso del método .pop personalizado por índice)
        function eliminarMateria(index) {
            if (confirm(`¿Estás seguro de que deseas borrar: ${nombres[index]}?`)) {
                nombres.splice(index, 1);
                dias.splice(index, 1);
                horas_inicio.splice(index, 1);
                horas_fin.splice(index, 1);
                creditos.splice(index, 1);

                actualizarTabla();
                actualizarPago();
            }
        }

        // 4. ACTUALIZAR INTERFAZ DE LA TABLA
        function actualizarTabla() {
            const tabla = document.getElementById('tablaMaterias');
            tabla.innerHTML = ""; // Limpiar tabla

            if (nombres.length === 0) {
                tabla.innerHTML = `<tr><td colspan="5" style="text-align: center; color: #94a3b8;">No tienes materias registradas aún.</td></tr>`;
                return;
            }

            for (let i = 0; i < nombres.length; i++) {
                const fila = document.createElement('tr');
                
                fila.innerHTML = `
                    <td style="font-weight: 600;">${nombres[i]}</td>
                    <td>${dias[i]}</td>
                    <td>${horas_inicio[i]}:00 - ${horas_fin[i]}:00</td>
                    <td><span style="background: #e2e8f0; padding: 3px 8px; border-radius: 4px;">${creditos[i]}</span></td>
                    <td><button class="btn-delete" onclick="eliminarMateria(${i})">Borrar</button></td>
                `;
                tabla.appendChild(fila);
            }
        }

        // 5. CALCULAR PAGO (CON DESCUENTOS)
        function actualizarPago() {
            // sum(creditos) en JavaScript
            const total_cre = creditos.reduce((a, b) => a + b, 0);
            const pago_base = total_cre * VALOR_CREDITO;
            
            let descuento = 0;
            if (total_cre > 10) {
                descuento = pago_base * 0.10;
                document.getElementById('alertaDescuento').style.display = 'block';
            } else {
                document.getElementById('alertaDescuento').style.display = 'none';
            }

            const total_final = pago_base - descuento;

            // Renderizar los valores formateados en moneda colombiana / local sin decimales
            document.getElementById('pagoCreditos').innerText = total_cre;
            document.getElementById('pagoSubtotal').innerText = "$" + pago_base.toLocaleString('es-CO');
            document.getElementById('pagoDescuento').innerText = "-$" + descuento.toLocaleString('es-CO');
            document.getElementById('pagoTotal').innerText = "$" + total_final.toLocaleString('es-CO');
        }
    </script>
</body>
</html>
