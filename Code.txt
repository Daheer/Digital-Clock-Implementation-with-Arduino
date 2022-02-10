#include <LiquidCrystal.h>

int hoursPin = 7;
int hoursSwStateOld = 1;
int hoursSwStateNew;

int minutesPin = 6;
int minutesSwStateOld = 1;
int minutesSwStateNew;

int hours;
int minutes;
int seconds;
int tick;

int rs = 8;
int e = 9;
int d4 = 10;
int d5 = 11;
int d6 = 12;
int d7 = 13;

String meridian = "AM";
String extra_zero_hr = "0";
String extra_zero_min = "0";
String extra_zero_sec = "0";

LiquidCrystal Display(rs, e, d4, d5, d6, d7);

void setup() {
  pinMode(hoursPin, INPUT);
  digitalWrite(hoursPin, HIGH);
  pinMode(minutesPin, INPUT);
  digitalWrite(minutesPin, HIGH);
  Serial.begin(9600);
  Display.begin(16, 2);
}

void loop() {

  Display.clear();

  hoursSwStateNew = digitalRead(hoursPin);
  minutesSwStateNew = digitalRead(minutesPin);

  if (hoursSwStateNew == 0 && hoursSwStateOld == 1) {
    if (hours < 11) {
      meridian = "AM";
    } else {
      meridian = "PM";
    }
    if (hours == 23) {
      hours = 0;
      meridian = "AM";
    } else {
      hours += 1;
    }
    if (hours < 10) {
      extra_zero_hr = "0";
    } else {
      extra_zero_hr = "";
    }
    Serial.print("Time is: ");
    Serial.print(hours);
    Serial.print(" : ");
    Serial.print(minutes);
    Serial.print(" : ");
    Serial.println(seconds);
    Display.setCursor(0, 0);
    Display.print(extra_zero_hr);
    Display.print(hours);
    Display.print(" : ");
    Display.print(extra_zero_min);
    Display.print(minutes);
    Display.print(" : ");
    Display.print(extra_zero_sec);
    Display.print(seconds);
    Display.print(" ");
    Display.print(meridian);
    delay(200);
  }
  else if (minutesSwStateNew == 0 && minutesSwStateOld == 1) {
    if (minutes >= 60) {
      minutes = 0;
      hours += 1;
    } else {
      minutes += 1;
    }
    if (minutes < 10) {
      extra_zero_min = "0";
    } else {
      extra_zero_min = "";
    }
    Serial.print("Time is: ");
    Serial.print(hours);
    Serial.print(" : ");
    Serial.print(minutes);
    Serial.print(" : ");
    Serial.println(seconds);
    Display.setCursor(0, 0);
    Display.print(extra_zero_hr);
    Display.print(hours);
    Display.print(" : ");
    Display.print(extra_zero_min);
    Display.print(minutes);
    Display.print(" : ");
    Display.print(extra_zero_sec);
    Display.print(seconds);
    Display.print(" ");
    Display.print(meridian);
    delay(200);
  } else {
    if (tick == 9) {
      seconds += 1;
      if (seconds == 59) {
        seconds = 0;
        minutes += 1;
      }
      tick = 0;
    }
    tick += 1;
    if (seconds < 10) {
      extra_zero_sec = "0";
    } else {
      extra_zero_sec = "";
    }
    if (minutes == 60) {
      minutes = 0;
      hours += 1;
    } 
    if (hours == 23) {
      hours = 0;
      meridian = "AM";
    }   
    if (minutes < 10) {
      extra_zero_min = "0";
    } else {
      extra_zero_min = "";
    }
    if (hours < 10) {
      extra_zero_hr = "0";
    } else {
      extra_zero_hr = "";
    }
    if (hours < 11) {
      meridian = "AM";
    } else {
      meridian = "PM";
    }
    Serial.print("Time is: ");
    Serial.print(hours);
    Serial.print(" : ");
    Serial.print(minutes);
    Serial.print(" : ");
    Serial.println(seconds);
    Display.setCursor(0, 0);
    Display.print(extra_zero_hr);
    Display.print(hours);
    Display.print(" : ");
    Display.print(extra_zero_min);
    Display.print(minutes);
    Display.print(" : ");
    Display.print(extra_zero_sec);
    Display.print(seconds);
    Display.print(" ");
    Display.print(meridian);
    delay(100);
  }
  
}