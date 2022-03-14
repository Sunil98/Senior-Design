
//start
#include <Servo.h>
int pivot_flag=0;
unsigned long currentMillis = 0;
unsigned long previousMillis = 0;
unsigned long millistimer = 50;//50,500


int pivot_servo_pin = 19;
int left_servo_pin = 18;
int pin_recieve = 14;
int pin_send = 15;

void Pivot_Movement();
void timer_delay();


Servo pivot_servo;
Servo left_servo;



void setup(){
  Serial.begin(9600);

  pivot_servo.attach(pivot_servo_pin);
  left_servo.attach(left_servo_pin);

  pinMode(pivot_servo_pin,OUTPUT);
  pinMode(left_servo_pin,OUTPUT);
  pinMode(pin_send,OUTPUT);
  pinMode(pin_recieve,INPUT);
  
  digitalWrite(pin_send,LOW);

  pivot_servo.write(20);
  left_servo.write(10);
  
}


int pivot_angle=2;//20
int left_angle=10;

int read_val;
int bool_stop = 0;
void loop(){


  //if(1){
  //if(digitalRead(pin_recieve)==HIGH){
  //if (bool_stop == 0){
  read_val = analogRead(pin_recieve);
  Serial.print("first read_val " );
  Serial.println(read_val);
  
  if (read_val > 500){//126
  Serial.println("INSIDE FIRST IF");
  Pivot_Movement();
  digitalWrite(pin_send,HIGH);
  timer_delay(1000);
  digitalWrite(pin_send,LOW);
  timer_delay(1000);
  }
  //bool_stop = 1;
  //}//if bool_stop
  
  //if(1){
  //if(digitalRead(pin_recieve)==HIGH){
  //if (bool_stop == 1){
  read_val = analogRead(pin_recieve);
  Serial.print("second read_val " );
  Serial.println(read_val);
  
  if(read_val > 500){//126 
  Serial.println("INSIDE SECOND IF");
  //Pivot_actual_inverse();
  Pivot_Movement_inverse();
  digitalWrite(pin_send,HIGH);
  timer_delay(1000);
  digitalWrite(pin_send,LOW);
  timer_delay(1000);
  }
  //bool_stop = 0;
  
  //}//bool_stop
  

  
  
}




void timer_delay(unsigned long ms){
currentMillis=millis();
previousMillis=currentMillis;
while(currentMillis-previousMillis<ms){currentMillis=millis();}
}




void Pivot_Movement(){
while (pivot_angle<60){
  timer_delay(25);
  pivot_angle=pivot_angle+1;
  pivot_servo.write(pivot_angle);
  left_servo.write(left_angle);
}//end of while

while (left_angle<175){
currentMillis = millis();
  timer_delay(25);
  left_angle=left_angle+3;
  pivot_servo.write(pivot_angle);
  left_servo.write(left_angle);
  }//end of while

while (pivot_angle>2){
  timer_delay(25);
  pivot_angle=pivot_angle-1;
  pivot_servo.write(pivot_angle);
  left_servo.write(left_angle);

}
}//end of func



void Pivot_actual_inverse(){
while (pivot_angle<60){
  timer_delay(25);
  pivot_angle=pivot_angle+1;
  pivot_servo.write(pivot_angle);
  left_servo.write(left_angle);
}//end of while

while (left_angle>10){
currentMillis = millis();
  timer_delay(25);
  left_angle=left_angle-3;
  pivot_servo.write(pivot_angle);
  left_servo.write(left_angle);
  }//end of while


while (pivot_angle>2){
  timer_delay(25);
  pivot_angle=pivot_angle-1;
  pivot_servo.write(pivot_angle);
  left_servo.write(left_angle);

}
}//end of func

//left is pi
void Pivot_Movement_inverse(){
  
while (left_angle>10){
currentMillis = millis();
  timer_delay(25);
  left_angle=left_angle-3;
  pivot_servo.write(pivot_angle);
  left_servo.write(left_angle);
  }//end of while


}//end of func
