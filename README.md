import speech_recognition as sr
import RPi.GPIO as GPIO

# Define LED pin
led_pin = 17

# Initialize GPIO
GPIO.setmode(GPIO.BCM)
GPIO.setup(led_pin, GPIO.OUT)

# Initialize speech recognition
r = sr.Recognizer()

while True:
    with sr.Microphone() as source:
        audio = r.listen(source)
        try:
            command = r.recognize_google(audio).lower()
            if "turn on" in command:
                GPIO.output(led_pin, GPIO.HIGH)
            elif "turn off" in command:
                GPIO.output(led_pin, GPIO.LOW)
        except sr.UnknownValueError:
            print("Speech recognition could not understand audio") Cod-task-4
