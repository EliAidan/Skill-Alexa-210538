# Skill-Alexa-210538
Practica desarrollada en Amazon Developer como practica de la materia de Desarrollo Movil Integral

# **Documentación**

<div style="display: flex; justify-content: space-between;">
    <img align="left" src="img/LOGO TIC (4).png?raw=true" alt="Logo 1" width="300"; />
    <img align="right" src="img/LOGO UTXJ PNG.png?raw=true" alt="Logo 2" width="300";/>
</div><br><br><br><br><br>

# **UNIVERSIDAD TECNOLÓGICA DE XICOTEPEC DE JUÁREZ**

## **Materia:** Desarrollo Móvil Integral

## **Practica realizada por:**

| Nombre Completo | Matricula|
|-----------------|----------|
|Eli Aidan Melo Calva|210538|

### LISTA DE HERRAMIENTAS
![Amazon Developer](https://img.shields.io/badge/Amazon%20Developer-FF9900?style=for-the-badge&logo=amazon&logoColor=white)

## **Descripcion**
 ### El desarrollar una Skill para Amazon Alexa implica crear aplicaciones o funciones personalizadas que amplían las capacidades del asistente virtual Alexa, permitiéndole realizar tareas específicas, responder preguntas, controlar dispositivos inteligentes, proporcionar contenido interactivo o ejecutar acciones según comandos de voz. Estas habilidades se integran al ecosistema Alexa y se pueden desarrollar para satisfacer necesidades personales, empresariales o de entretenimiento.

 ## **Desarrollo**
 ### Lo que implica el desarrollo de una skill es clave porque amplía las capacidades del asistente de voz, ofreciendo experiencias personalizadas y útiles que mejoran la interacción entre los usuarios y la tecnología.

 ## **Parte del codigo que nos permitio conseguir que alexa nos diera el clima**
```bash
const Alexa = require('ask-sdk-core');
const axios = require('axios');

const LaunchRequestHandler = {
  canHandle(handlerInput) {
    return Alexa.getRequestType(handlerInput.requestEnvelope) === 'LaunchRequest';
  },
  handle(handlerInput) {
    const speakOutput = 'Esta es la skill hecha por Elí Aidan, ¿Qué quieres hacer?';

    return handlerInput.responseBuilder
      .speak(speakOutput)
      .reprompt(speakOutput)
      .getResponse();
  }
};

const WeatherIntentHandler = {
  canHandle(handlerInput) {
    return (
      Alexa.getRequestType(handlerInput.requestEnvelope) === 'IntentRequest' &&
      Alexa.getIntentName(handlerInput.requestEnvelope) === 'Clima'
    );
  },
  async handle(handlerInput) {
    try {
      const apiKey = 'c677e31d5aaf53b8ec958cd20b41a5b2'; // Reemplaza con tu clave de API de OpenWeatherMap
      const lat = 20.247141; // Reemplaza con la latitud deseada
      const lon = -97.967629; // Reemplaza con la longitud deseada

      const response = await axios.get(
        `https://api.openweathermap.org/data/2.5/weather?lat=${lat}&lon=${lon}&appid=${apiKey}&units=metric&lang=es`
      );

      const temperature = response.data.main.temp;
      const weatherDescription = response.data.weather[0].description;
      const location = response.data.name;
      const humedad = response.data.main.humidity;
      const tem_max = response.data.main.temp_min;
      //NUEVO
      const sepone = response.data.sys.sunset;
      const sunsetDate = new Date(sepone);
      const sunsetHour = sunsetDate.getHours();
      const sunsetMinutes = sunsetDate.getMinutes();

      

      const speakOutput = `La temperatura actual en ${location} es de ${temperature} grados Celsius y la humedad es de ${humedad} y el sol se oculta a las ${sunsetHour}:${sunsetMinutes}.`;

      return handlerInput.responseBuilder.speak(speakOutput).getResponse();
    } catch (error) {
      console.log('Error al obtener el clima:', error);

      const speakOutput = 'Lo siento, no pude obtener la información del clima en este momento.';
      return handlerInput.responseBuilder.speak(speakOutput).getResponse();
    }
  },
};
```
#### Este código implementa una Skill para Amazon Alexa que ofrece información del clima utilizando la API de OpenWeatherMap. Utiliza ask-sdk-core para manejar las interacciones de Alexa y axios para realizar solicitudes HTTP.

#### El LaunchRequestHandler responde al comando inicial del usuario con un mensaje de bienvenida. Por su parte, el WeatherIntentHandler procesa un intent llamado Clima, solicita datos meteorológicos a la API basados en coordenadas geográficas (latitud y longitud) y devuelve información como la temperatura, la humedad y la hora del atardecer. Si hay un error al obtener los datos, responde con un mensaje genérico de disculpa. El código está diseñado para ofrecer una interacción natural y datos en tiempo real, mejorando la utilidad de Alexa para el usuario.

## **Evidencias**

<div style="display: flex; justify-content: space-between; flex-wrap: wrap;">
    <img src="./img/result/Evidencia.png?raw=true" alt="img1" width="700">
</div>