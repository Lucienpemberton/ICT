
## Projecten

Welkom op mijn projecten pagina van ICT in de Wolken. Hier onder vind je ze allemaal.

### Microbit bot
##### In samenwerking met [Siebe Roeleveld](https://siebefloris.github.io/ICT)
Dit is ons eerste programma voor de micro:bit. Door deze code, branden de lampjes groen als er voldoende licht aan de sensor is. Als er niet voldoende licht op de sensor valt gaan de lampjes rood branden. De robot heeft 2 licht sensoren, met deze code hebben we er voor gezorgd dat de linker lampjes en de rechter lampjes los van elkaar kunnen branden als er voldoende licht bij de respectieve sensor zit. Je kunt de sensor met je hand blokkeren om het systeem te testen.

```
from microbit import *
import neopixel

np = neopixel.NeoPixel(pin13, 12)

leftLineSensor = pin11
rightLineSensor = pin5

lightSensor = pin2
sensorSelect = pin16

def leftLights(Red, Green, Blue):
    for pixel_id in range(0, 6):
        np[pixel_id] = (Red, Green, Blue)
    np.show()

def rightLights(Red, Green, Blue):
    for pixel_id in range(6, 12):
        np[pixel_id] = (Red, Green, Blue)
    np.show()

def lineDetector(side):  # 0 == left, 1 == right
    if(side == 0):
        isLine = leftLineSensor.read_digital()
    else:
        isLine = rightLineSensor.read_digital()

    if(isLine == 1):  # Sensor can see the line
        return True
    else:
        return False
        
        
while True:
    isLeftLight = lineDetector(0)
    isRightLight = lineDetector(1)
    
    if(isLeftLight is True) and (isRightLight is False):
        leftLights(0,255,0)
        rightLights(255,0,0)

    elif(isRightLight is True) and (isLeftLight is False):
        rightLights(0,255,0)
        leftLights(255,0,0)

    elif(isRightLight is False) and (isLeftLight is False):
        rightLights(255,0,0)
        leftLights(255,0,0)
        
    else:
        leftLights(0,255,0)
        rightLights(0,255,0)
```

Hierna hebben wij deze code uitgebreid door bewegingsmogenlijkheden toe te passen. met deze nieuwe versie van de code kan de micro:bit een lijn detecteren en hem volgen. als een van de licht sensoren over de lijn rijden, merkt de robot dit en beweegt hij in de andere riching zodat de lijn tussen de twee sensoren in blijft.

```
from microbit import *
import neopixel  # Neopixel Library so we can control the NeoPixels lights

np = neopixel.NeoPixel(pin13, 12)

leftSpeed = pin0
leftDirection = pin8
rightSpeed = pin1
rightDirection = pin12

leftLineSensor = pin11
rightLineSensor = pin5

lightSensor = pin2
sensorSelect = pin16


def leftLights(Red, Green, Blue):
    for pixel_id in range(0, 6):  # Start of for loop
        np[pixel_id] = (Red, Green, Blue)  # Code to be executed in the loop
    np.show() # Change the NeoPixels colour


def rightLights(Red, Green, Blue):
    for pixel_id in range(6, 12):
        np[pixel_id] = (Red, Green, Blue)
    np.show()


def setBrightness(minValue):
    sensorSelect.write_digital(0)
    brightnessLeft = lightSensor.read_analog()
    sensorSelect.write_digital(1)
    brightnessRight = lightSensor.read_analog()

    brightness = int((brightnessLeft + brightnessRight) / 2)
    brightness = int(brightness / 25)
    if(brightness < minValue):
        brightness = minValue
        return brightness


def lineDetector(side):  # 0 == left, 1 == right
    if(side == 0):
        isLine = leftLineSensor.read_digital()
    else:
        isLine = rightLineSensor.read_digital()

    if(isLine == 1):  # Sensor can see the line
        return True
    else:
        return False

def move(_leftSpeed, _rightSpeed, _leftDirection, _rightDirection):
    # speed values between 1 - 1023
    # smaller values == faster speed moving backwards
    # Smaller values == lower speeds when moving forwards
    # direction 0 == forwards, 1 == backwards
    leftSpeed.write_analog(_leftSpeed)  # Set the speed of left motor
    rightSpeed.write_analog(_rightSpeed)  # Set the speed of right motor
    if (_leftDirection != 2):
        leftDirection.write_digital(_leftDirection)  # left motor
        rightDirection.write_digital(_rightDirection)  # right motor


def drive(speed):
    if (speed > 0):
        move(speed, speed, 0, 0)  # move the motors forwards
    else:
        speed = 1023 + speed
        move(speed, speed, 1, 1)  # move the motors backwards


def sharpRight():
    move(100, 1023 + -200, 0, 1)


def sharpLeft():
    move(1023 + -200, 100, 1, 0)


def gentleRight():
    move(200, 0, 0, 0)


def gentleLeft():
    move(0, 200, 0, 0)


def coast():
    move(0, 0, 2, 2)


def stop():
    move(0, 0, 0, 0)


sleep(1000)
while True:
    isLeftLine = lineDetector(0)
    isRightLine = lineDetector(1)
    if(isLeftLine is True) and (isRightLine is False):
        leftLights(setBrightness(1), 0, 0)
        stop()
        sleep(50)
        sharpLeft()
        sleep(200)
        stop()
        sleep(50)
        while(lineDetector(0) is True):
            leftLights(setBrightness(1), 0, 0)
            gentleLeft()

    elif(isRightLine is True) and (isLeftLine is False):
        rightLights(setBrightness(1), 0, 0)
        stop()
        sleep(50)
        sharpRight()
        sleep(200)
        stop()
        sleep(50)
        while(lineDetector(1) is True):
            rightLights(setBrightness(1), 0, 0)
            gentleRight()

    elif(isRightLine is False) and (isLeftLine is False):
        leftLights(0, setBrightness(1), 0)
        rightLights(0, setBrightness(1), 0)
        drive(150)
    else:
        leftLights(0, setBrightness(1), setBrightness(1))
        rightLights(0, setBrightness(1), setBrightness(1))
        stop()
        sleep(200)
```

### AI Project
##### In samenwerking met [Siebe Roeleveld](https://siebefloris.github.io/ICT)

Voor blok 3 hebben wij gekozen voor het AI project. In dit project moeten wij een spel programmeren en er voor zorgen dat de computer hem bovenmenselijk leert spelen.
WIj hebben als spel voor Flappy Bird gekozen, dit spel is vrij simpel en kan makkelijk nagemaakt worden.
We hebben er voor gekozen om het in python te schrijven, hier hebben wij al ervaring mee van vorige projecten en er bestaan vele AI libraries die makkelijk te implementeren zijn.


[terug naar homepage](https://lucienpemberton.github.io/ICT/)
