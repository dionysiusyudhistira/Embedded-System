
# Jobsheet 2 
PROTOKOL KOMUNIKASI DAN SENSOR

## Anggota Kelompok

- Dionysius Brammetya Yudhistira
- Noviantie Putriastuti


## 1. ESP32 Capacitive Touch Sensor
# Program
a-capasitivetouchsensor - Hanya membaca sentuhan yang dilakukan dan menampilkan di serial monitor
```c
// ESP32 Touch Test
// Just test touch pin - Touch0 is T0 which is on GPIO 4. 
void setup() {
Serial.begin(115200);
delay(1000); // give me time to bring up serial monitor 
Serial.println("ESP32 Touch Test");
}
void loop() {
Serial.println(touchRead(4));  // menampilkan nilai dari sentuhan yang ada di pin GPIO 4
delay(1000);
}
```


a-capasitivetouchsensorled1 - Jika disentuh maka LED akan menyala ketika disentuh dan tidak menyala jika tidak disentuh
```c
// menginisiasi pin GPIO yang akan dipakai
const int touchPin = 4; //Pin GPIO yang mendeteksi sentuhan
const int ledPin = 16; //Pin GPIO yang akan menyalan LED sebagai keluaran

// change with your threshold value
const int threshold = 20;
// variable for storing the touch pin value 
int touchValue;

void setup(){
  Serial.begin(115200);
  delay(1000); // give me time to bring up serial monitor
  // Inisiasi LED sebagai keluaran
  pinMode (ledPin, OUTPUT);
}

void loop(){
  // membaca sensor sentuhan
  touchValue = touchRead(touchPin);
  Serial.print(touchValue);
  // mengecek apakah ada nilai dari sentuhan
  // jika ada maka LED akan menyala
  if(touchValue < threshold){
    // turn LED on
    digitalWrite(ledPin, HIGH);
    Serial.println(" - LED on");
  }
  else{
    // turn LED off
    digitalWrite(ledPin, LOW);
    Serial.println(" - LED off");
  }
  delay(500);
}
```


a-capasitivetouchsensorled2 - LED Running
```c
// menginisiasi pin GPIO yang akan dipakai
const int touchPin = 4; 
const int ledPin1 = 16;
const int ledPin2 = 18;
const int ledPin3 = 19;

// change with your threshold value
const int threshold = 20;
// variable for storing the touch pin value 
int touchValue;

void setup(){
  Serial.begin(115200);
  delay(1000); // give me time to bring up serial monitor
  // menginisiasi pin GPIO LED sebagai keluaran
  pinMode (ledPin1, OUTPUT);
  pinMode (ledPin2, OUTPUT);
  pinMode (ledPin3, OUTPUT);
}

void loop(){
  // membaca nilai sentuhan
  touchValue = touchRead(touchPin);
  Serial.print(touchValue);
  // mengecek dengan logika IF ELSE dan akan menyalan LED jika terdapat sentuhan
  if(touchValue < threshold){
    // turn LED on
    Serial.println(" - LED on");
    digitalWrite(ledPin1, HIGH);
    delay(500);
    digitalWrite(ledPin1, LOW);
    digitalWrite(ledPin2, HIGH);
    delay(500);
    digitalWrite(ledPin2, LOW);
    digitalWrite(ledPin3, HIGH);
    delay(500);
    digitalWrite(ledPin3, LOW);
       
  }
  else{
    // turn LED off
    digitalWrite(ledPin1, LOW);
digitalWrite(ledPin2, LOW);
digitalWrite(ledPin3, LOW);
    Serial.println(" - LED off");
  }
  delay(500);
}
```
# Kesimpulan
Pratikum ini memberikan kesimpulan bahwa dalam pemanfaatan ESP32 sebagai mikrokontroller dapat membaca sensor berupa sentuhan kemudian dari sentuhan itu dapat diberikan output dalam contoh ini akan menghidupkan LED dan membuat LED running dari kiri ke kanan.


## 2. Mengakses Sensor DHT 11 (Single Wire / BUS)
# Program
```c
//Library yang dibutuhkan
#include "DHT.h"

//Pin yang terkoneksi dengan Sensor DHT
#define DHTPIN 4

//Tipe DHT yang digunakan
#define DHTTYPE DHT11 // DHT 11
//#define DHTTYPE DHT22 // DHT 22 (AM2302), AM2321
//#define DHTTYPE DHT21 // DHT 21 (AM2301)
DHT dht(DHTPIN, DHTTYPE); //Inisialisasi DHT dengan PIN
void setup() {

//Inisialisasi Serial Monitor untuk debugging
 Serial.begin(9600);
 Serial.println(F("DHT11 Embedded System Test!"));
 // Inisialisasi DHT
 dht.begin();
}
void loop() {
 //Membaca nilai Sensor dari DHT11
 delay(2000);
 // Reading temperature or humidity takes about 250 milliseconds!
 // Sensor readings may also be up to 2 seconds 'old' (its a very slow sensor)
 float h = dht.readHumidity();
 // Read temperature as Celsius (the default)
 float t = dht.readTemperature();
 // Read temperature as Fahrenheit (isFahrenheit = true)
 float f = dht.readTemperature(true);
 // Check if any reads failed and exit early (to try again).
 if (isnan(h) || isnan(t) || isnan(f)) {
 Serial.println(F("Failed to read from DHT sensor!"));
 return;
 }
 // Compute heat index in Fahrenheit (the default)
 float hif = dht.computeHeatIndex(f, h);
 // Compute heat index in Celsius (isFahreheit = false)
 float hic = dht.computeHeatIndex(t, h, false);
 
 //Print nilai data yang telah dibaca dari sensor ke serial monitor
 Serial.print(F("Humidity: "));
 Serial.print(h);
 Serial.print(F("% Temperature: "));
 Serial.print(t);
 Serial.print(F("°C "));
 Serial.print(f);
 Serial.print(F("°F Heat index: "));
 Serial.print(hic);
 Serial.print(F("°C "));
 Serial.print(hif);
 Serial.println(F("°F"));
}
```c
//Library yang dibutuhkan
#include "DHT.h"

//Pin yang terkoneksi dengan sensor DHT
#define DHTPIN 4

//Tipe DHT yang digunakan
#define DHTTYPE DHT11 // DHT 11
//#define DHTTYPE DHT22 // DHT 22 (AM2302), AM2321
//#define DHTTYPE DHT21 // DHT 21 (AM2301)
DHT dht(DHTPIN, DHTTYPE);

//Pin yang terkoneksi dengan LED
const int ledPin1 = 16;
const int ledPin2 = 18;
const int ledPin3 = 19;

void setup() {
//Inisialisasi Serial Monitor untuk debugging
 Serial.begin(9600);
 Serial.println(F("DHT11 Embedded System Test!"));
 dht.begin(); //Inisialisasi DHT
 
 //Memberikan perintah LED sebagai output
   pinMode (ledPin1, OUTPUT);
   pinMode (ledPin2, OUTPUT);
   pinMode (ledPin3, OUTPUT);

}
void loop() {
 //Membaca sensor DHT 
 delay(2000);
 // Reading temperature or humidity takes about 250 milliseconds!
 // Sensor readings may also be up to 2 seconds 'old' (its a very slow sensor)
 float h = dht.readHumidity();
 // Read temperature as Celsius (the default)
 float t = dht.readTemperature();
 // Read temperature as Fahrenheit (isFahrenheit = true)
 float f = dht.readTemperature(true);
 // Check if any reads failed and exit early (to try again).
 if (isnan(h) || isnan(t) || isnan(f)) {
 Serial.println(F("Failed to read from DHT sensor!"));
 return;
 }
 // Compute heat index in Fahrenheit (the default)
 float hif = dht.computeHeatIndex(f, h);
 // Compute heat index in Celsius (isFahreheit = false)
 float hic = dht.computeHeatIndex(t, h, false);
  
  //Logika IF untuk membuat jika suhu dibawah 30° C maka LED akan berjalan running, ketika suhu diatas 30° C maka LED akan mati
  if(t < 30){
Serial.println(" - LED on");
    digitalWrite(ledPin1, HIGH);
    delay(500);
    digitalWrite(ledPin1, LOW);
    digitalWrite(ledPin2, HIGH);
    delay(500);
    digitalWrite(ledPin2, LOW);
    digitalWrite(ledPin3, HIGH);
    delay(500);
    digitalWrite(ledPin3, LOW);
  }
  else{
    // turn LED off
    digitalWrite(ledPin1, LOW);
digitalWrite(ledPin2, LOW);
digitalWrite(ledPin3, LOW);
    Serial.println(" - LED off");
  }
 
 //Print nilai sensor di serial monitor
 Serial.print(F("Humidity: "));
 Serial.print(h);
 Serial.print(F("% Temperature: "));
 Serial.print(t);
 Serial.print(F("°C "));
 Serial.print(f);
 Serial.print(F("°F Heat index: "));
 Serial.print(hic);
 Serial.print(F("°C "));
 Serial.print(hif);
 Serial.println(F("°F"));
}
```


# Kesimpulan
- Sensor DHT11 berfungsi untuk membaca kelembapan dan suhu yang dapat di ESP32 untuk mengumpulkan data dan menjadikannya sebuah input untuk sebuah sistem seperti dalam contoh jika suhu dibawah 30° C maka LED akan berjalan runnning.
- Sensor DHT11 memiliki delay pembacaan sekitar 2 detik sehingga pembacaan realtime dengan di serial monitor akan mengalami delay.
