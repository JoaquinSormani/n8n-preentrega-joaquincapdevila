# Pre-entrega: Monitor de Clima para Eventos

## Descripción del Caso
Workflow diseñado para organizadores de eventos. Permite monitorear condiciones climáticas en tiempo real en una ubicación específica y recibir alertas automáticas si la temperatura supera un umbral de seguridad definido por el usuario.

## Estructura del Workflow
Flujo: **Webhook → API Clima → IF → Email Alert**.

### Disparador (Trigger)
- **Tipo:** Webhook (POST).
- **Función:** Recibe coordenadas (`lat`, `lon`) y un umbral de temperatura (`temp_maxima`).

### Nodos
1. **API Open-Meteo:** Consulta el pronóstico en tiempo real usando las coordenadas provistas. No requiere API Key.
2. **Condicional (IF):** Evalúa si la temperatura actual (`current_weather.temperature`) supera el límite establecido por el usuario.
3. **Notificación (Gmail):** Si la condición es verdadera (True), envía un correo de advertencia con los datos actuales.
4. **Log Seguro (False):** Si la temperatura es segura, registra el evento sin enviar notificaciones.

### Buenas Prácticas
- **Modularidad:** Las coordenadas son dinámicas, permitiendo usar el mismo flujo para cualquier ciudad del mundo.
- **Eficiencia:** Uso de parámetros GET en el nodo HTTP para construir la consulta de forma limpia.
- **UX:** Respuesta inmediata al Webhook para evitar timeouts en el cliente (Postman).
