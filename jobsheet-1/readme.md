
# Jobsheet 1 
DASAR PEMROGRAMAN ESP32 UNTUK PEMROSESAN DATA INPUT/OUTPUT ANALOG DAN DIGITAL


## Anggota Kelompok

- [Dionysius Brammetya Yudhistira]
- [Noviantie Putriastuti]

## 1. GPIO
Program di bawah ini mengendalikan led menggunakan push button.

```c
// set pin numbers
const int buttonPin1 = 15;  // the number of the pushbutton pin 
const int buttonPin2 = 2;
const int buttonPin3 = 4;
const int ledPin1 =  5;    // the number of the LED pin
const int ledPin2 =  18;
const int ledPin3 =  19;
int button1, button2, button3;
// variable for storing the pushbutton status 
int buttonState = 0;
void setup() {
Serial.begin(115200);  
// initialize the pushbutton pin as an input 
pinMode(buttonPin1, INPUT);
pinMode(buttonPin2, INPUT);
pinMode(buttonPin3, INPUT);
// initialize the LED pin as an output 
pinMode(ledPin1, OUTPUT);
pinMode(ledPin2, OUTPUT);
pinMode(ledPin3, OUTPUT);
}
void loop() {
// read the state of the pushbutton value 
button1 = digitalRead(buttonPin1); 
button2 = digitalRead(buttonPin2); 
button3 = digitalRead(buttonPin3); 
// check if the pushbutton is pressed. 
// if it is, the buttonState is HIGH 
if (button1 == HIGH) {
    digitalWrite(ledPin1, HIGH);
}  else if (button2 == HIGH){
    digitalWrite(ledPin2, HIGH);
    delay(500);
    digitalWrite(ledPin2, LOW);
    delay(500);
} else if (button3 == HIGH) {
    digitalWrite(ledPin1, HIGH);
    delay(500);
    digitalWrite(ledPin1, LOW);
    delay(500);
    digitalWrite(ledPin2, HIGH);
    delay(500);
    digitalWrite(ledPin2, LOW);
    delay(500);
    digitalWrite(ledPin3, HIGH);
    delay(500);
    digitalWrite(ledPin3, LOW);
    delay(500);
}
}
```


https://user-images.githubusercontent.com/121749328/210791851-bdbed79e-9386-46c0-803f-116085364fd8.mp4


Tambahkan 1 LED dan 1 push button pada rangkaian. Kemudian tambahkan program agar ketika push button ke-2 ditekan, LED akan melakukan blink setiap 500 ms sekali.
```c
// set pin numbers
const int buttonPin = 4;
const int buttonPin2 = 16;
const int ledPin = 5;
const int ledPin2 = 18;
int buttonState = 0;
int buttonState2 = 0;

void setup() {
 Serial.begin(115200);
 pinMode(buttonPin, INPUT);
 pinMode(buttonPin2, INPUT);
 pinMode(ledPin, OUTPUT);
 pinMode(ledPin2, OUTPUT);
}

void loop() {
 buttonState = digitalRead(buttonPin);
 buttonState2 = digitalRead(buttonPin2);
 Serial.println(buttonState);
 Serial.println(buttonState2);
 
 if (buttonState == HIGH) {
 digitalWrite(ledPin, HIGH);
 } else {
 digitalWrite(ledPin, LOW);
 }
 
 if (buttonState2 == HIGH) {
 digitalWrite(ledPin2, HIGH);
 delay(500);
 digitalWrite(ledPin2, LOW);
 delay(500);
 } else {
 digitalWrite(ledPin2, LOW);
 }
}
```


https://user-images.githubusercontent.com/121749328/210792374-627f1fc5-5a17-4922-96a3-61de993d3793.mp4


Tambahkan 3 LED dan 1 push button pada rangkaian, kemudian kembangkan program agar ketika push button ke-3 ditekan, LED akan menyala menjadi running led (menyala bergantian dari kiri ke kanan).
```c
// set pin numbers
const int buttonPin = 4;
const int buttonPin2 = 16;
const int buttonPin3 = 17;
const int ledPin = 5;
const int ledPin2 = 18;
const int ledPin3 = 19;
const int ledPin4 = 21;
const int ledPin5 = 3;
int buttonState = 0;
int buttonState2 = 0;
int buttonState3 = 0;

void setup() {
 Serial.begin(115200);
 pinMode(buttonPin, INPUT);
 pinMode(buttonPin2, INPUT);
 pinMode(buttonPin3, INPUT);
 pinMode(ledPin, OUTPUT);
 pinMode(ledPin2, OUTPUT);
 pinMode(ledPin3, OUTPUT);
 pinMode(ledPin4, OUTPUT);
 pinMode(ledPin5, OUTPUT);
}

void loop() {
 buttonState = digitalRead(buttonPin);
 buttonState2 = digitalRead(buttonPin2);
 buttonState3 = digitalRead(buttonPin3);
 Serial.println(buttonState);
 Serial.println(buttonState2);
 Serial.println(buttonState3);
 
 if (buttonState == HIGH) {
 digitalWrite(ledPin, HIGH);
 } else {
 digitalWrite(ledPin, LOW);
 }
 
 if (buttonState2 == HIGH) {
 digitalWrite(ledPin2, HIGH);
 delay(500);
 digitalWrite(ledPin2, LOW);
 delay(500);
 } else {
 digitalWrite(ledPin2, LOW);
 }
 
 if (buttonState3 == HIGH) {
 digitalWrite(ledPin5, LOW);
 digitalWrite(ledPin3, HIGH);
 delay(100);
 digitalWrite(ledPin3, LOW);
 digitalWrite(ledPin4, HIGH);
 delay(100);
 digitalWrite(ledPin4, LOW);
 digitalWrite(ledPin5, HIGH);
 delay(100);
 } else {
 digitalWrite(ledPin3, LOW);
 digitalWrite(ledPin4, LOW);
 digitalWrite(ledPin5, LOW);
 }
}
```


https://user-images.githubusercontent.com/121749328/210792851-e5a80166-60de-4990-b809-b2b86587b080.mp4


## 2. PWM
### Program


## ADC DAC
Dalam pekerjaan Analog Digital Converter dan Digital Analog Converter dicontohkan dengan membaca input dari sebuah potensiometer yang diterjemahkan secara digital melalui pemrogaman sebagai berikut.
```c
potValue = analogRead(potPin); 
delay(500);
volt = potValue*5/4095;
Serial.println("Nilai ADC");
Serial.println(potValue);
Serial.println("Nilai Tegangan");
Serial.println(volt);
```
Fungsi ini akan membaca setiap putaran potensio dan menghasilkan angka sesuai dengan putaran potensiometer.

Percobaan ADC DAC kedua mengimplementasikan angka yang dibaca oleh ESP32 menjadi nyala lampu LED, jika potensiometer diputar yang paling kecil maka LED tidak menyala dan sebaliknya jika potensiometer diputar pada kapasitas maksimum maka LED akan nyala paling terang. Koding untuk percobaan kedua yang berfungsi untuk membaca dan memberikan perintah ke LED untuk menyala adalah sebagai berikut.
```c
sensorValue = analogRead(analogInPin); // read the analog in value:
outputValue = map(sensorValue, 0, 4095, 0, 255); // map it to the range of the analog out:
ledcWrite(ledChannel, outputValue); // change the analog out value:
// print the results to the Serial Monitor:
Serial.print("sensor = ");
Serial.print(sensorValue);
Serial.print("\t output = ");
Serial.println(outputValue);
// wait 2 milliseconds before the next loop for the analog-to-digital 
// converter to settle after the last reading:
delay(500);
```


# Dokumentasi
## GPIO

## PWM


https://user-images.githubusercontent.com/121749328/210416793-6b9a9dc1-b29f-4858-a8ad-7eb260195db8.mp4



https://user-images.githubusercontent.com/121749328/210416818-dd38e8d6-91b6-4d4f-acea-c1897abdb9c6.mp4


## ADC & DAC


https://user-images.githubusercontent.com/121749328/210416998-927bdc52-c8c6-4134-828a-638b16c1748e.mp4



https://user-images.githubusercontent.com/121749328/210417015-786b9367-aaf7-4ccb-958e-172663e94ac0.mp4

