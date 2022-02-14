# อธิบายโปรแกรม
การเขียนโปรแกรมจะมี 2 ส่วนหลักๆ คือ 
   1. Setup เขียนขึ้นด้วยภาษา C และ C++ ซึ่งจะรันเพียงครั้งเดียว
   2. Loop โดย Loop จะรันตลอดไป
  
ในแต่ละโปรแกรมเมื่อใช้ใน Platformio จะมี Configuration file ชื่อว่า Platformio.ini
ซึ่ง Configuration file จะเป็นตัวบอกว่าเป็น Platform หรือเป็นผลิตภัณฑ์ของบริษัทใด มีบอร์ดชื่ออะไร เป็นต้น

## การทดลองที่ 1 เรื่อง การเขียนโปรแกรมเพื่อรันบนไมโครคอนโทรเลอร์
    #include <Arduino.h>

    int cnt = 0;	#Count(cnt) เริ่มต้นที่ 0

    void setup()	
    {
		Serial.begin(115200);	#Set Serial.begin ด้วยความเร็ว 115200
    }

    void loop()		#ในส่วน Loop จะแสดงผลของ Count(cnt)
    {
	    	cnt++;		#มีการเพิ่มตัวแปร Count(cnt) ขึ้นเรื่อยๆ
		Serial.printf("PATTANI :%d\n",cnt); 	#ให้แสดงผลตัวแปร Count(cnt) ออกมา
		int s = cnt % 5 + 1;
		int d = s * 1000; 	
		delay(d);	#ทุกๆค่าของ Count(cnt) ที่ออกมานั้นจะ delay ห่างกันทุกๆ 1 วินาที หรือ 1000 mS
    }

Platformio.ini การทดลองที่ 1

	; IOT for KIDS
	;
	; By Dr.Choompol Boonmee
	; 

	[env:exercise01]
	platform = espressif8266	#platform ของบริษัท espressif8266
	board = esp01_1m	#ชื่อบอร์ด (บอร์ด ชื่อ esp01_1m)
	framework = arduino	#วิธีที่ใช้เขียนโปรแกรม(เขียนโปรแกรมแบบ arduino)
	board_build.flash_mode = dout

	upload_port = /dev/cu.usbserial-1420	#Port ที่ใช้ติดต่อ
	;upload_port = COM3	#ใช้พอร์ท COM3

	monitor_port = /dev/cu.usbserial-1420 #Port ที่ใช้สังเกตการณ์
	;monitor_port = COM3	#ใช้พอร์ท COM4
	monitor_speed = 115200	#Monitor มีคววามเร็ว 115200
	
## การทดลองที่ 2 เรื่อง การเขียนโปรแกรมค้นหาไวไฟ
	#include <Arduino.h>
	#include <ESP8266WiFi.h>

	int cnt = 0;	#Count(cnt) เริ่มต้นที่ 0
	
	void setup()	#ในส่วนของ Setup ใช้ Setup ไวไฟให้เตรียมพร้อมทำงาน 
	{
		 Serial.begin(115200);	#Set Serial.begin ด้วยความเร็ว 115200
	      	 WiFi.mode(WIFI_STA);
	      	 WiFi.disconnect();
	      	 delay(100);	#ทุกๆค่าที่แสดงออกมานั้นจะ delay ห่างกันทุกๆ 100 mS
	      	 Serial.println("\n\n\n");

	}

	void loop()	#ในส่วน Loop จะรันไปเรื่อยๆแสดงผลตามคำสั่ง 
	{

		Serial.println("========== เริ่มต้นแสกนหา Wifi ===========");	#แสดงผลว่า " เริ่มแสกนหา Wifi "
		int n = WiFi.scanNetworks();
		if(n == 0) {	#ถ้า n = 0 แสดงผล "NO NETWORK FOUND"
			Serial.println("NO NETWORK FOUND");
		} else {
			for(int i=0; i<n; i++) { 	#แสดงผลว่าไวไฟรอบตัวมีอะไรบ้าง
				Serial.print(i + 1);
				Serial.print(": ");
				Serial.print(WiFi.SSID(i));
				Serial.print(" (");
				Serial.print(WiFi.RSSI(i));
				Serial.println(")");
				Serial.print(WiFi.channel(i));
				delay(10);
			}


		}
		Serial.println("\n\n");
		delay(10 * 1000);	#ทุกๆค่าที่แสดงออกมานั้นจะ delay ห่างกันทุกๆ 10*1000 mS

	}
	
Platformio.ini	การทดลองที่ 2

	; IOT for KIDS
	;
	; By Dr.Choompol Boonmee
	; 

	[env:exercise01]
	platform = espressif8266	#platform ของบริษัท espressif8266
	board = esp01_1m	#ชื่อบอร์ด (บอร์ด ชื่อ esp01_1m)
	framework = arduino	#วิธีที่ใช้เขียนโปรแกรม(เขียนโปรแกรมแบบ arduino)
	board_build.flash_mode = dout

	upload_port = /dev/cu.usbserial-1420	#Port ที่ใช้ติดต่อ
	;upload_port = COM3	#ใช้พอร์ท COM3

	monitor_port = /dev/cu.usbserial-1420	#Port ที่ใช้สังเกตการณ์
	;monitor_port = COM3	#ใช้พอร์ท COM3
	monitor_speed = 115200	#Monitor มีคววามเร็ว 115200
	
## การทดลองที่ 3 เรื่อง การเขียนโปรแกรมเอ้าพุทสัญญาณดิจิทัล
	#include <Arduino.h>
	#include <ESP8266WiFi.h>

	int cnt = 0;	#Count(cnt) เริ่มต้นที่ 0

	void setup()
	{
		Serial.begin(115200);	#Set Serial.begin ด้วยความเร็ว 115200
		pinMode(0, OUTPUT);	#Set ให้พอร์ทเลข 0 เป็นพอร์ท Output
		Serial.println("\n\n\n");
	}

	void loop()
	{
		cnt++;	#มีการเพิ่มตัวแปร Count(cnt) ขึ้นเรื่อยๆ
		if(cnt % 2) {	#ถ้า Count(cnt) เป็นเลขคี่ใน ON ก็คือส่งค่า HIGH ไปที่พอร์ท 0 โดยจะมีแสงสว่างที่หลอดไฟ
			Serial.println("========== ON ===========");
			digitalWrite(0, HIGH);
		} else {	#แต่ถ้า Count(cnt) เป็นเลขคู่ใน OFF ก็คือส่งค่า LOW ไปที่พอร์ท 0
			Serial.println("========== OFF ===========");
			digitalWrite(0, LOW);
		}
		delay(500); #วนลูปทุกครึ่งวินาที หรือ 500 mS
	}
	
Platformio.ini	การทดลองที่ 3

	; IOT for KIDS
	;
	; By Dr.Choompol Boonmee
	; 

	[env:exercise01]	
	platform = espressif8266	#platform ของบริษัท espressif8266
	board = esp01_1m	#ชื่อบอร์ด (บอร์ด ชื่อ esp01_1m)
	framework = arduino	#วิธีที่ใช้เขียนโปรแกรม(เขียนโปรแกรมแบบ arduino)
	board_build.flash_mode = dout	

	upload_port = /dev/cu.usbserial-1420	#Port ที่ใช้ติดต่อ
	;upload_port = COM3	#ใช้พอร์ท COM3

	monitor_port = /dev/cu.usbserial-1420	#Port ที่ใช้สังเกตการณ์
	;monitor_port = COM3	#ใช้พอร์ท COM3
	monitor_speed = 115200	#Monitor มีคววามเร็ว 115200
	
## การทดลองที่ 4 เรื่อง การเขียนโปรแกรมอินพุทสัญญาณดิจิทัล
	#include <Arduino.h>
	#include <ESP8266WiFi.h>

	int cnt = 0;	#Count(cnt) เริ่มต้นที่ 0

	void setup()
	{
		Serial.begin(115200);	
		pinMode(0, INPUT);	#Set ให้พอร์ท 0 เป็น INPUT
		pinMode(2, OUTPUT);	#Set ให้พอร์ท 2 เป็น OUTPUT
		Serial.println("\n\n\n");
	}

	void loop()
	{
		int val = digitalRead(0);	#การอ่านข้อมูลจากพอร์ท พอร์ทในที่นี้ คือ พอร์ท 0
		Serial.printf("======= read %d\n", val);	#แสดงผลว่าอ่านได้เท่าไหร่ เป็น 0 หรือ 1 (digital เลขฐานสอง)
		if(val==1) {	#ถ้าเป็น 1 ให้ LOW ไปที่พอร์ท 2 ถ้ามีหลอดไฟไฟจะดับ
			digitalWrite(2, LOW);
		} else {	#ถ้าเป็น 0 ให้ HIGH ไปที่พอร์ท 2 ถ้ามีหลอดไฟไฟจะสว่าง
			digitalWrite(2, HIGH);
		}
		delay(100);	#วนลูปทุกๆ 100 mS
	}

Platformio.ini	การทดลองที่ 4

	; IOT for KIDS
	;
	; By Dr.Choompol Boonmee
	; 

	[env:exercise01]
	platform = espressif8266	#platform ของบริษัท espressif8266
	board = esp01_1m	#ชื่อบอร์ด (บอร์ด ชื่อ esp01_1m)
	framework = arduino	#วิธีที่ใช้เขียนโปรแกรม(เขียนโปรแกรมแบบ arduino)
	board_build.flash_mode = dout

	upload_port = /dev/cu.usbserial-1420	#Port ที่ใช้ติดต่อ
	;upload_port = COM3	#ใช้พอร์ท COM3
	
	monitor_port = /dev/cu.usbserial-1420	#Port ที่ใช้สังเกตการณ์
	;monitor_port = COM3	#ใช้พอร์ท COM3
	monitor_speed = 115200	#Monitor มีคววามเร็ว 115200
	
## การทดลองที่ 5 เรื่อง การเขียนโปรแกรมเชื่อมต่อไวไฟและเว็บเซอร์เวอร์
เนื่องจากมีการเชื่อมต่อไวไฟที่มีอยู่แล้ว จะต้องใส่ชื่อไวไฟ และรหัสผ่านลงไปด้วย

	#include <ESP8266WiFi.h>
	//#include <WiFiClient.h>
	#include <ESP8266WebServer.h>

	const char* ssid = "HI_BMFWIFI_2.4G"; 	#ใส่ชื่อไวไฟ
	const char* password = "0819110933";	#ใส่รหัสไวไฟ

	ESP8266WebServer server(80);

	int cnt = 0;	#Count(cnt) เริ่มต้นที่ 0

	void setup(void){
		Serial.begin(115200);

		WiFi.mode(WIFI_STA);	#ตั้งแต่บรรทัด 218-225 เป็นการเชื่อมต่อกับไวไฟที่ตั้งไว้
		WiFi.begin(ssid, password);
		while (WiFi.status() != WL_CONNECTED) {
			delay(500);
			Serial.print(".");
		}
		Serial.print("\n\nIP address: ");
		Serial.println(WiFi.localIP());

		server.onNotFound([]() {	#Setup Web server
			server.send(404, "text/plain", "Path Not Found");
		});

		server.on("/", []() {
			cnt++;	#มีการเพิ่มตัวแปร Count(cnt) ขึ้นเรื่อยๆ
			String msg = "Hello cnt: ";	#ถ้ามีการเชื่อมต่อก็แสดงข้อความว่า "Hello cnt: " ตามจำนวนลูป
			msg += cnt;
			server.send(200, "text/plain", msg);
		});

		server.begin();
		Serial.println("HTTP server started");
	}

	void loop(void){
	  server.handleClient();
	}	
	
Platformio.ini	การทดลองที่ 5

	; IOT for KIDS
	;
	; By Dr.Choompol Boonmee
	; 

	[env:exercise01]	
	platform = espressif8266	#platform ของบริษัท espressif8266
	board = esp01_1m	#ชื่อบอร์ด (บอร์ด ชื่อ esp01_1m)
	framework = arduino	#วิธีที่ใช้เขียนโปรแกรม(เขียนโปรแกรมแบบ arduino)
	board_build.flash_mode = dout

	upload_port = /dev/cu.usbserial-1420	#Port ที่ใช้ติดต่อ
	;upload_port = COM3	#ใช้พอร์ท COM3
	
	monitor_port = /dev/cu.usbserial-1420	#Port ที่ใช้สังเกตการณ์
	;monitor_port = COM3	#ใช้พอร์ท COM3
	monitor_speed = 115200	#Monitor มีคววามเร็ว 115200

## การทดลองที่ 6 เรื่อง การเขียนโปรแกรมสร้างไวไฟแอคเซสพอยต์ (Wifi AP)
เนื่องจากมีการสร้างไวไฟขึ้นมา จะต้องมีการกำหนดชื่อไวไฟ และรหัสผ่านลงไปด้วย

	#include <ESP8266WiFi.h>
	//#include <WiFiClient.h>
	#include <ESP8266WebServer.h>

	const char* ssid = "MY-ESP8266";	#สร้างชื่อไวไฟ
	const char* password = "choompol";	#สร้างรหัสไวไฟ

	IPAddress local_ip(192, 168, 1, 1);	#ใส่ IPAddress local_ip ของ Microcontroller
	IPAddress gateway(192, 168, 1, 1);	#ใส่ IPAddress gateway
	IPAddress subnet(255, 255, 255, 0);	#ใส่ IPAddress subnet

	ESP8266WebServer server(80);	#เปิดเว็บเซิร์ฟเวอร์ที่พอร์ท 80

	int cnt = 0;	#Count(cnt) เริ่มต้นที่ 0

	void setup(void){
	Serial.begin(115200);	#Set การสร้างแอคเซสพอยต์
	
		WiFi.softAP(ssid, password);	#กำหนด ssid และรหัสผ่าน
		WiFi.softAPConfig(local_ip, gateway, subnet);	#กำหนด local_ip, gateway และ subnet
		delay(100);	#delay ทุกๆ 100 mS

		server.onNotFound([]() {
			server.send(404, "text/plain", "Path Not Found");	#หา server ไม่พบให้แสดง "Path Not Found"
		});

		server.on("/", []() {
			cnt++;	#มีการเพิ่มตัวแปร Count(cnt) ขึ้นเรื่อยๆ
			String msg = "Hello cnt: ";	#หา server พบให้แสดง "Hello cnt: " ตามจำนวน cnt
			msg += cnt;
			server.send(200, "text/plain", msg);
		});

		server.begin();
		Serial.println("HTTP server started");
	}

	void loop(void){
 	 server.handleClient();
	}

Platformio.ini	การทดลองที่ 6

	; IOT for KIDS
	;
	; By Dr.Choompol Boonmee
	; 

	[env:exercise01]
	platform = espressif8266	#platform ของบริษัท espressif8266
	board = esp01_1m	#ชื่อบอร์ด (บอร์ด ชื่อ esp01_1m)
	framework = arduino	#วิธีที่ใช้เขียนโปรแกรม(เขียนโปรแกรมแบบ arduino)
	board_build.flash_mode = dout

	upload_port = /dev/cu.usbserial-1420	#Port ที่ใช้ติดต่อ
	;upload_port = COM3	#ใช้พอร์ท COM3

	monitor_port = /dev/cu.usbserial-1420	#Port ที่ใช้สังเกตการณ์
	;monitor_port = COM3	#ใช้พอร์ท COM3
	monitor_speed = 115200	#Monitor มีคววามเร็ว 115200

