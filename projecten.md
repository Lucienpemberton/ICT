
## Projecten

Welkom op mijn projecten pagina van ICT in de Wolken. Hier onder vind je ze allemaal.

### Microbit bot

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
    isLeftLine = lineDetector(0)
    isRightLine = lineDetector(1)
    
    if(isLeftLine is True) and (isRightLine is False):
        leftLights(0,255,0)
        rightLights(255,0,0)

    elif(isRightLine is True) and (isLeftLine is False):
        rightLights(0,255,0)
        leftLights(255,0,0)

    elif(isRightLine is False) and (isLeftLine is False):
        rightLights(255,0,0)
        leftLights(255,0,0)
        
    else:
        leftLights(0,255,0)
        rightLights(0,255,0)
```


[terug naar homepage](https://lucienpemberton.github.io/ICT/)
