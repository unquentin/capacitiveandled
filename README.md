# capacitiveandled
ARDUINO UNO fade a LED depending on the value measured by a capacitive sensor


#include <CapacitiveSensor.h>

int led = 9; 
int brightness = 0;    // how bright the LED is
int fadeAmount = 5; 
CapacitiveSensor   cs_2_4 = CapacitiveSensor(2,4);        // 2 x 1M resistor between pins 2 & 4, pin 4 is sensor pin, add a wire and or foil if desired

void setup()                    
{
   pinMode(led, OUTPUT);
   Serial.begin(9600);
}

void loop()                    
{
    long start = millis();
    long total1 =  cs_2_4.capacitiveSensor(30);
    
    Serial.print(millis() - start);        
    Serial.print("\t");                    

    Serial.print(total1);                  
    brightness = map(total1, 0, 25000, 0, 1023);
    analogWrite(led, brightness);
    
    delay(50);                            
}
