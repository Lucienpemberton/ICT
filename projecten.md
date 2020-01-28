
## Projecten

Welkom op mijn projecten pagina van ICT in de Wolken. Hier onder vind je ze allemaal.

### Microbit bot
 In samenwerking met [Siebe Roeleveld] (https://siebefloris.github.io/ICT)
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


[terug naar homepage](https://lucienpemberton.github.io/ICT/)
