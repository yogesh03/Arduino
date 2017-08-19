# Arduino
#blinking of LED when the button id held for more than 5 secs else button acts as switch
const int LED=9;
const  int BUTTON=8;
int i;
int val=0;
int old_val=0;
int state=0;
int brightness=128;
unsigned long startTime=0;
void setup() 
{ 
  pinMode(LED,OUTPUT);
  pinMode(BUTTON,INPUT);
  }
void loop() 
{ 
  val=digitalRead(BUTTON);
  if((val==HIGH)&&(old_val==LOW)) //condition when the state will change(when button is pressed fresh)
  { state=1-state;
    startTime=millis();  //time starts at this pt(i.e.,we note time from the pt the state changes)
    delay(10);  //for managing the on/offs during button's back displacement
    }
    if((val==HIGH)&&(old_val==HIGH)) //button is kept pressed here (excecuted at 2nd run of program after pressing the button)
    {
      if((state==1)&&(millis()-startTime>500)) //after 500ms of pressing, LED starts blinking. (compares whether 500ms are reached or not from start)
     { brightness++;
      if(brightness>255)
      { brightness=0;
      delay(10);
        }}
      }
      old_val=val; //old value is updated
      if(state==1) //what state 1 does is switches on the LED
      { analogWrite(LED,brightness);
        }
        else //what state 0 does is switches off the LED
        {
          analogWrite(LED,0);}
}
