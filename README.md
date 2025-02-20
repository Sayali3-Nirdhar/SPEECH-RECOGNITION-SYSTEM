# SPEECH-RECOGNITION-SYSTEM

**company** = CODTECH IT SOLUTIONS

**NAME** = SAYALI SANTOSH NIRDHAR 

**INTERN ID** = CT08JED

**DOMAIN** = Embedded Systems 

**BATCH DURATION** = January 20th, 2025 to February 20th, 2025 

**MENTOR NAME** = Neela Santhosh 

#include <SoftwareSerial.h>
#include <VoiceRecognitionV3.h>

SoftwareSerial mySerial(2, 3);  
VR myVR;
const int relayPin = 8;  
#define CMD_TURN_ON   1 
#define CMD_TURN_OFF  2  
void setup() {
    Serial.begin(9600);
    mySerial.begin(9600);
    if (myVR.begin(mySerial)) {
        Serial.println("Voice Recognition Module Ready");
    } else {
        Serial.println("Voice Module Initialization Failed");
        while (1);
    }  
    pinMode(relayPin, OUTPUT);
    digitalWrite(relayPin, LOW);  
}

void loop() {
    uint8_t records[7];  
    uint8_t num;    
    if (myVR.recognize(records, &num) > 0) {  
        Serial.print("Command ID: ");
        Serial.println(records[0]);      
        if (records[0] == CMD_TURN_ON) {
            digitalWrite(relayPin, HIGH);
            Serial.println("Device Turned ON");
        } else if (records[0] == CMD_TURN_OFF) {
            digitalWrite(relayPin, LOW);
            Serial.println("Device Turned OFF");
        }
    }
}

# output of task 4
