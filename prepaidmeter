//PREPAID ENERGY METER BY YASH GAJERA
//VERSION 1.0


#include "EmonLib.h"                 
EnergyMonitor emon1;                 
#include <LiquidCrystal.h>
#include <Keypad.h>

LiquidCrystal lcd(9,8,A0,A1,A2,A3 );

const byte ROWS = 4;
const byte COLS = 3;
char keys[ROWS][COLS] = {
{'1','2','3'},
{'4','5','6'},
{'7','8','9'},
{'*','0','#'}
};
byte rowPins[ROWS] = {7,6,5,4};
byte colPins[COLS] = {3,2,1};

Keypad kpd = Keypad( makeKeymap(keys), rowPins, colPins, ROWS, COLS );

float total;
float test;
float test1=0;
float test2=0;
float unit=0;
#define relay 12

void setup()
{
  pinMode(relay,OUTPUT);
  digitalWrite(relay, HIGH);  
  Serial.begin(9600);
  emon1.voltage(4, 255, 10); 
  emon1.current(5, 9);     
  lcd.begin(16, 2);   
  lcd.noCursor();     
  lcd.setCursor(0, 0);
  lcd.print("Energy Meter");
  delay(1000);
  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("by YASH GAJERA");
  delay(1000);
  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("Enter Recharge:");
  input();
  digitalWrite(relay, LOW);
  unitcal();
  balance();
  
  
}
void loop()
{
}

void unitcal(void)
{
  unit = (total/52000)*3600000;
  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("your Recharge");
  lcd.print(unit);
}
void input(void)
{
   lable: test = kpd.getKey();
    if(test)
    {
      test=test-48;
      test=test*100;
      goto lable1;
    }
    else
    {
      goto lable;
    lable1: test1 = kpd.getKey();
    if(test1)
    {
      test1=test1-48;
      test1=test1*10;
      goto lable2;
    }
    else
    {
      goto lable1;
    }
   lable2: test2 = kpd.getKey();
    if(test2)
    {
      test2=test2-48;
      goto total;
    }
    else
    {
      goto lable2;
    }  
    total:total=test+test1+test2;
    lcd.setCursor(0, 1);
    lcd.print(total);
    delay(1000); 
    }
}

void balance(void)
{
        emon1.calcVI(20,2000);
        float realPower = 0-emon1.realPower;
        emon1.calcVI(20,2000);
        realPower = emon1.realPower;
  unitc:emon1.calcVI(20,2000);
        realPower = emon1.realPower;
        lcd.print(realPower);
        lcd.clear();
        lcd.setCursor(0, 0);
        
        lcd.setCursor(0, 1);
        lcd.print(unit);
    
  if(unit > 0)
  {
     unit = unit + realPower;
     delay(1000);
     goto unitc;
  }
  else
  {
    digitalWrite(relay,HIGH);
    exit();
  }
     
  
  }

void exit(void)
{
  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("Balance Zero");
  lcd.setCursor(0, 1);
  lcd.print("Plz Recharge");
}

