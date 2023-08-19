import RPi.GPIO as GPIO
import time
import requests

# Set up GPIO mode and pins
GPIO.setmode(GPIO.BCM)
PIR_PIN = 4

# Ubidots token
UBIDOTS_TOKEN = "BBFF-FVadVsFGjZLV6VRjyTdGtD6ANKzDD6"

# Initialize GPIO pins
GPIO.setup(PIR_PIN, GPIO.IN)

def send_to_ubidots(value):
    payload = {'motion': value}
    try:
        r = requests.post(f'http://industrial.api.ubidots.com/api/v1.6/devices/raspberry_pir/?token={UBIDOTS_TOKEN}', data=payload)
        print('Posting motion data to Ubidots')
        print(payload)
    except Exception as e:
        print(f'Error: {e}')

try:
    while True:
        motion_value = GPIO.input(PIR_PIN)
        send_to_ubidots(motion_value)
        time.sleep(1)  # Wait between motion checks

except KeyboardInterrupt:
    GPIO.cleanup()
