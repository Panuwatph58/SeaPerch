//Keyboard Controls:

// 1 -Motor 1 Left

// 2 -Motor 1 Stop

// 3 -Motor 1 Right

// 4 -Motor 2 Left

// 5 -Motor 2 Stop

// 6 -Motor 2 Right

// 7 -Motor 3 Up

// 8 -Motor 3 Stop

// 9 -Motor 3 Down
// Declare L298N Dual H-Bridge Motor Controller directly since there is not a library to load.

// Motor 1

int dir1PinA = 2;

int dir2PinA = 3;

int speedPinA = A0; // Needs to be a PWM pin to be able to control motor speed

// Motor 2

int dir1PinB = 4;

int dir2PinB = 5;

int speedPinB = A1; // Needs to be a PWM pin to be able to control motor speed

// Motor 3

int dir1PinC = 6;

int dir2PinC = 7;

int speedPinC = A2; // Needs to be a PWM pin to be able to control motor speed
 

void setup() {  // Setup runs once per reset

            Serial.begin(9600);

//Define L298N Dual H-Bridge Motor Controller Pins

    pinMode(dir1PinA,OUTPUT);

    pinMode(dir2PinA,OUTPUT);

    pinMode(speedPinA,OUTPUT);

    pinMode(dir1PinB,OUTPUT);

    pinMode(dir2PinB,OUTPUT);

    pinMode(speedPinB,OUTPUT);
    
    pinMode(dir1PinC,OUTPUT);

    pinMode(dir2PinC,OUTPUT);

    pinMode(speedPinC,OUTPUT);

}

void loop() {

// Initialize the Serial interface:

if (Serial.available() > 0) {

int inByte = Serial.read();

int speed; // Local variable

switch (inByte) {

      //______________Motor 1______________

      case '2': // ถอยหลัง

          analogWrite(speedPinA, 255);//Sets speed variable via PWM 
          analogWrite(speedPinB, 255);
          digitalWrite(dir1PinA, LOW);
          digitalWrite(dir1PinB, LOW);
          digitalWrite(dir2PinA, HIGH);
          digitalWrite(dir2PinB, HIGH);
          Serial.println("backward");

      break;

      case '8': // เดินหน้า

          analogWrite(speedPinA, 255);
          analogWrite(speedPinB, 255);
          digitalWrite(dir1PinB, HIGH);
          digitalWrite(dir2PinB, LOW);
          digitalWrite(dir1PinA, HIGH);
          digitalWrite(dir2PinA, LOW);
          Serial.println("forward");

      break;

      case '4': // เลี้ยวซ้าย

          analogWrite(speedPinB, 255);

          digitalWrite(dir1PinB, HIGH);

          digitalWrite(dir2PinB, LOW);
          analogWrite(speedPinA, 130);

          digitalWrite(dir1PinA, LOW);

          digitalWrite(dir2PinA, HIGH);
          
          Serial.println("backward");

      break;

      case '6': // เลี้ยวขวา

          analogWrite(speedPinA, 255);

          digitalWrite(dir1PinA, HIGH);

          digitalWrite(dir2PinA, LOW);
          analogWrite(speedPinB, 130);

          digitalWrite(dir1PinB, LOW);

          digitalWrite(dir2PinB, HIGH);
          
          Serial.println("backward");

      break;
      
      case '5': // Motor 1 Stop 

          analogWrite(speedPinA, 0);
          analogWrite(speedPinB, 0);

          digitalWrite(dir1PinB, LOW);

          digitalWrite(dir2PinB, HIGH);

          digitalWrite(dir1PinA, LOW);

          digitalWrite(dir2PinA, HIGH);

          Serial.println("Motor 1 Stop");

          Serial.println("   ");

      break;

      //______________Motor 3______________

      case 'S': // Motor 3 UP

          analogWrite(speedPinC, 255);

          digitalWrite(dir1PinC, LOW);

          digitalWrite(dir2PinC, HIGH);

          Serial.println("Motor 3 Up");

          Serial.println("   ");

      break;

      case 'F': // Motor 3 stop

          analogWrite(speedPinC, 0);

          digitalWrite(dir1PinC, LOW);

          digitalWrite(dir2PinC, HIGH);

          Serial.println("Motor 3 Stop  ");

          Serial.println("   ");

      break;

      case 'W': // Motor 3 down

          analogWrite(speedPinC, 255);
          

          digitalWrite(dir1PinC, HIGH);

          digitalWrite(dir2PinC, LOW);

          Serial.println("Motor 2 Reverse");

          Serial.println("   ");

      break;

       case '7': // ไปข้างหน้าทางซ้าย

          analogWrite(speedPinA, 255);//Sets speed variable via PWM 
          analogWrite(speedPinB, 130);
          digitalWrite(dir1PinA, LOW);
          digitalWrite(dir1PinB, LOW);
          digitalWrite(dir2PinA, HIGH);
          digitalWrite(dir2PinB, HIGH);
          Serial.println("backward");
      break;

      case '9': // ไปข้างหน้าทางขวา

          analogWrite(speedPinA, 130);//Sets speed variable via PWM 
          analogWrite(speedPinB, 255);
          digitalWrite(dir1PinA, LOW);
          digitalWrite(dir1PinB, LOW);
          digitalWrite(dir2PinA, HIGH);
          digitalWrite(dir2PinB, HIGH);
          Serial.println("backward");
      break;

      case '1': // ถอยหลังทางซ้าย

          analogWrite(speedPinA, 255);
          analogWrite(speedPinB, 130);
          digitalWrite(dir1PinB, HIGH);
          digitalWrite(dir1PinA, HIGH);
          digitalWrite(dir2PinB, LOW);
          digitalWrite(dir2PinA, LOW);
      break;

      case '3': // ถอยหลังทางขวา

          analogWrite(speedPinA, 130);
          analogWrite(speedPinB, 255);
          digitalWrite(dir1PinB, HIGH);
          digitalWrite(dir1PinA, HIGH);
          digitalWrite(dir2PinB, LOW);
          digitalWrite(dir2PinA, LOW);
      break;
      
    default:

      // turn all the connections off if an unmapped key is pressed:

      for (int thisPin = 2; thisPin < 11; thisPin++) 

      {

        digitalWrite(thisPin, LOW);

      }

    }

  }

} 
