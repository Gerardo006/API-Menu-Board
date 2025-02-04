# API-Menu-Board

INTEGRANTES:

Miguel Veintimilla
Ariana Cordova
Cristhian Davila
Gerardo Naula
Camila Chimbo

IMPLEMENTACION:


![Captura de pantalla 2025-02-04 002757](https://github.com/user-attachments/assets/a85651c4-d5b0-49f1-8449-544be24373a5)



## Documentación
# Implementación de Google Maps API

## Descripcion del Proyecto

Este proyecto integra la API de Google Maps para proporcionar a los usuarios una funcionalidad que les permite visualizar la ruta desde su ubicación actual hasta un destino predefinido.

La Implementación de esta permite:

- Mostrar un mapa interactivo dentro de la página web.
- Identificar la ubicación actual del usuario mediante geolocalización.
- Calcular y mostrar la mejor ruta al destino.
- Agregar un marcador visual para indicar el destino.

## Funcionalidad agregada

La API de Google Maps permite a los usuarios obtener direcciones y ver la mejor ruta desde su ubicación hasta un punto específico. 

La funcionalidad se basa en:

- **Geolocalización:** Determina la ubicación actual del usuario con navigator.geolocation.getCurrentPosition.

- **Mapa interactivo:** Se crea y muestra un mapa con google.maps.Map.

- **Marcadores:** Se señala el destino con google.maps.Marker.

- **Cálculo de rutas:** Se utiliza google.maps.DirectionsService y google.maps.DirectionsRenderer para trazar la ruta entre la ubicación del usuario y el destino.

## Implementación

Requisitos previos a tomar en cuenta para que el codigo se pueda ejecutar:

- Una clave de API de Google Maps, obtenida desde Google Cloud Console.
- Un proyecto en Django donde se almacenen los archivos estáticos.

### Estructura del código

### HTML

1. Se cargan los recursos estaticos (static)

```html
{% load static %}
<link rel="stylesheet" href="{% static 'css/ubicacion.css' %}">
```

2. Contenedor principal:

```html
<div class="container">
    <div id="map"></div>
    <div class="image-container">
        <img src="{% static 'images/resubi.png' %}" alt="Imagen del destino">
    </div>
</div>
```
3. Boton de regreso:

```html
<a href="{% url 'home' %}" class="back-button">Regresar</a>
```

### Javascript

1. Inicializar el mapa y marcador

```html
function initMap() {
    const destination = { lat: -4.0329396, lng: -79.2051226 };
    const map = new google.maps.Map(document.getElementById("map"), {
        zoom: 8,
        center: destination,
    });
    new google.maps.Marker({
        position: destination,
        map: map,
        title: "Destino",
    });
}
```

2. Obtener Ubicación del usuario

```html
if (navigator.geolocation) {
    navigator.geolocation.getCurrentPosition(
        (position) => {
            const currentLocation = {
                lat: position.coords.latitude,
                lng: position.coords.longitude,
            };

```

3. Calcular la ruta

```html
const directionsService = new google.maps.DirectionsService();
const directionsRenderer = new google.maps.DirectionsRenderer({ map: map });

directionsService.route(
    {
        origin: currentLocation,
        destination: destination,
        travelMode: google.maps.TravelMode.DRIVING,
    },
    (response, status) => {
        if (status === "OK") {
            directionsRenderer.setDirections(response);
        } else {
            console.error("Error al obtener la ruta. Estado:", status);
        }
    }
);
```

4. Cargar el script del API de Google Maps en el HTML.

```html
<script async src="https://maps.googleapis.com/maps/api/js?key=TU_API_KEY&callback=initMap"></script>
```

## Uso de APIs y Librerías Estándar

## Criterio

### Integración de API
- Google Maps API se utiliza para la geolocalización y cálculo de rutas.

### Documentación clara
- Se explica cómo se estructura e implementa la funcionalidad.

### Eficiencia
- La API optimiza el cálculo de rutas y la interacción del usuario.

## Instrucciones para Ejecutar el Proyecto

1. Agregar la clave de API en el archivo HTML en la línea:
   ```html
   <script async src="https://maps.googleapis.com/maps/api/js?key=TU_API_KEY&callback=initMap"></script>
   ```
2. Asegurar que los archivos estáticos (`ubicacion.css`, `resubi.png`) estén ubicados en la carpeta `static` de Django.
3. Ejecutar el servidor Django:
   ```sh
   python manage.py runserver
   ```
4. Acceder a la URL donde esté alojada la página para visualizar el mapa interactivo.

## Conclusión

Esta implementación de **Google Maps API** mejora la experiencia del usuario al proporcionar una ruta dinámica hacia un destino predefinido. La integración en **Django** permite un diseño modular y adaptable para futuras expansiones.

