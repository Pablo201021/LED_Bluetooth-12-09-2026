/*
 * Práctica: Control de un LED por Bluetooth con App Inventor + ESP32
 * Tecnológico Sudamericano — Prof. Galo Hurtado — www.profegalo.com
 *
 * La app envía:
 *   '1' -> enciende el LED
 *   '0' -> apaga el LED
 * El ESP32 responde con un texto de confirmación (opcional para la app).
 *
 * Requisitos:
 *   - Placa: ESP32 Dev Module (ESP32 "clásico", con Bluetooth Clásico).
 *     OJO: ESP32-S2, S3, C3 y C6 NO tienen Bluetooth Clásico y no funcionan
 *     con el componente BluetoothClient de App Inventor.
 *   - Paquete de placas "esp32 by Espressif Systems" en el Arduino IDE.
 *   - LED en GPIO 2 (en muchas placas ya hay un LED azul integrado en ese pin).
 */

#include "BluetoothSerial.h"

#if !defined(CONFIG_BT_ENABLED) || !defined(CONFIG_BLUEDROID_ENABLED)
#error "Bluetooth no está habilitado. Usa la placa 'ESP32 Dev Module'."
#endif

#if !defined(CONFIG_BT_SPP_ENABLED)
#error "Bluetooth Serial (SPP) no disponible en este chip. Usa un ESP32 clásico."
#endif

BluetoothSerial SerialBT;

const int PIN_LED = 2;                 // GPIO del LED (cambia si usas otro pin)
const char *NOMBRE_BT = "ESP32_LED";   // Nombre que verás al emparejar en el celular

void setup() {
  Serial.begin(115200);
  pinMode(PIN_LED, OUTPUT);
  digitalWrite(PIN_LED, LOW);          // El LED inicia apagado

  SerialBT.begin(NOMBRE_BT);           // Inicia Bluetooth en modo esclavo
  Serial.println("Bluetooth listo. Empareja el celular con: ESP32_LED");
}

void loop() {
  if (SerialBT.available()) {
    char dato = SerialBT.read();       // Lee un carácter enviado por la app

    if (dato == '1') {
      digitalWrite(PIN_LED, HIGH);
      SerialBT.println("LED ENCENDIDO");
      Serial.println("Recibido 1 -> LED ENCENDIDO");
    }
    else if (dato == '0') {
      digitalWrite(PIN_LED, LOW);
      SerialBT.println("LED APAGADO");
      Serial.println("Recibido 0 -> LED APAGADO");
    }
    // Cualquier otro carácter (saltos de línea, etc.) se ignora
  }
  delay(10);
}
