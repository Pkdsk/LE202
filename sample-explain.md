# อธิบายโปรแกรม
การเขียนโปรแกรมจะมี 2 ส่วนใหญ่ๆ คือ 
   1. Setup
   2. Loop
## การทดลองที่ 1 เรื่อง การเขียนโปรแกรมเพื่อรันบนไมโครคอนโทรเลอร์
#include <Arduino.h>

int cnt = 0;    *#การนับเริ่มต้นที่ 0*

void setup()    *#เข้าสู่ช่วงของ Setup*

{

	      Serial.begin(115200);

}


void loop()     *#เข้าสู่ช่วงของ Loop*

{

	      cnt++;\
	      Serial.printf("PATTANI :%d\n",cnt);\
	      int s = cnt % 5 + 1;\
	      int d = s * 1000;\
	      delay(d);
 
}

## การทดลองที่ 2 เรื่อง การเขียนโปรแกรมค้นหาไวไฟ
#include <Arduino.h>
#include <ESP8266WiFi.h>


int cnt = 0;


void setup()


{
	       Serial.begin(115200);\
	       WiFi.mode(WIFI_STA);\
	       WiFi.disconnect();\
	       delay(100);\
	       Serial.println("\n\n\n");

}


void loop()


{

	Serial.println("========== เริ่มต้นแสกนหา Wifi ===========");\
	int n = WiFi.scanNetworks();\
	if(n == 0) {\
		Serial.println("NO NETWORK FOUND");\
	} else {\
		for(int i=0; i<n; i++) {\
			Serial.print(i + 1);\
			Serial.print(": ");\
			Serial.print(WiFi.SSID(i));\
			Serial.print(" (");\
			Serial.print(WiFi.RSSI(i));\
			Serial.println(")");\
			Serial.print(WiFi.channel(i));\
			delay(10);


		}


	}
	Serial.println("\n\n");\
	delay(10 * 1000);

}

## การทดลองที่ 3 เรื่อง การเขียนโปรแกรมเอ้าพุทสัญญาณดิจิทัล
## การทดลองที่ 4 เรื่อง การเขียนโปรแกรมอินพุทสัญญาณดิจิทัล
## การทดลองที่ 5 เรื่อง การเขียนโปรแกรมเชื่อมต่อไวไฟและเว็บเซอร์เวอร์
## การทดลองที่ 6 เรื่อง การเขียนโปรแกรมสร้างไวไฟแอคเซสพอยต์ (Wifi AP)
