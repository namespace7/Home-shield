# Home-shield
recieve data from ardunio uno to android via bluetooth with multifunction


Arduino uno code



          #####
                  /*
          Pinout:
          8 --> BT module Tx
          9 --> BT module Rx
          */
          #include <SoftwareSerial.h>
          SoftwareSerial bluetoothdata(9,8); // RX, TX

          int ledPin = 13;      // LED 
          int pirPin = 2;                 // PIR Out pin 
          int pirStat = 0;                   // PIR status
          int calibrate = 30000;
          int flag =0;

          void setup() {
           pinMode(ledPin, OUTPUT);     
           pinMode(pirPin, INPUT);     
           Serial.begin(9600);
           bluetoothdata.begin(9600);
           Serial.println("calibrating the environment ");
           delay(calibrate);
           Serial.println("calibrating complete ");

          }
          void loop(){
           pirStat = digitalRead(pirPin); 
                   if (pirStat == HIGH)
                     {        // if motion detected
                          digitalWrite(ledPin, HIGH);  // turn LED ON
                          Serial.println("Motion Detected");
                          bluetoothdata.print("1");
                          // bluetoothdata.write(incomingData);        // Write the characters to Bluetooth
                     } else {
                             Serial.println("Idle");
                             digitalWrite(ledPin, LOW); // turn LED OFF if we have no motion
                                bluetoothdata.print("Idle");
                             //  bluetoothdata.write(incomingData);        // Write the characters to Bluetooth
                     }
        } 
