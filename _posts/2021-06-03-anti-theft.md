---
layout: post
title: 도난 방지 프로젝트의 파이썬 코드입니다.
---

Anti-theft.py 

<pre>

<code>
from picamera import PiCamera
from time import sleep
import serial
import datetime

camera = PiCamera()


if __name__ == '__main__':
	ser = serial.Serial('/dev/ttyACM0', 9600, timeout=1)
	ser.flush()
	while True:
		if ser.in_waiting > 0:
			line = ser.readline().decode('utf-8').rstrip()
			print(line)
			line = float(line)
			if line:
				camera.start_preview()
				sleep(1)
				saveFileName=datetime.datetime.now().strftime('%y%m%d%H%M%S%f')+'.jpg'
				camera.capture('/home/pi/anti-theft/pictures/' +saveFileName)
				camera.stop_preview()

</code>
</pre>
다음에는 도난 방지 프로젝트의 아두이노 스케치를 게시 하겠습니다.
