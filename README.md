# code682023
ملف الكود الربمجي لسيارة ذاتية القيادة من فريق ضواحي القدس الشريف

from WePort import *
from WeUltrasonicSensor import *
from WeDCMotor import *
import time
from WeServo import *

ultrasonic_A = WeUltrasonicSensor(PORT_A)
dc_1 = WeDCMotor(1)
ultrasonic_B = WeUltrasonicSensor(PORT_B)
ultrasonic_C = WeUltrasonicSensor(PORT_C)
servo_1 = WeServo(1, 0)

while True:
	if ultrasonic_A.distanceCM() < 15:
		dc_1.run(0)
		ultrasonic_A.rgbShow(3, 247, 3, 3)
		time.sleep(0.1)
		while not ultrasonic_A.distanceCM() > 50:
			dc_1.run(-100)
	else:
		if ultrasonic_B.distanceCM() < ultrasonic_C.distanceCM():
			servo_1.write_angle(105)
			dc_1.run(150)
			ultrasonic_B.rgbShow(3, 247, 3, 3)
		if ultrasonic_C.distanceCM() < ultrasonic_B.distanceCM():
			servo_1.write_angle(70)
			dc_1.run(150)
			ultrasonic_C.rgbShow(3, 247, 3, 3)
		if ultrasonic_C.distanceCM() == ultrasonic_B.distanceCM():
			servo_1.write_angle(85)
			dc_1.run(180)
			ultrasonic_C.rgbShow(3, 247, 3, 3)

