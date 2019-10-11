## Welkom

Dit is de homepage van mijn ICT in de Wolken website. je kan mijn projecten voor ICT [hier](https://lucienpemberton.github.io/ICT/projecten.md) vinden.


Verder kun je [hier](https://infvo.nl/ictindewolken/index.php/Gebruiker:LucienKerssens) mijn leerlingen wiki bekijken.

---

## Anders

#### [Galgje in Python](https://lucienpemberton.github.io/ICT/galgje.py)

```
import time
import random

print ("Gemaakt door Lucien Kerssens en Siebe Roeleveld; 5V5")
print ("Welkom bij galje")

time.sleep(1)

print("\nJe hebt in totaal 10 pogingen om het woord te raden.")
time.sleep(1)

words = ["geheim", "code", "python", "programmeren", "galgje"]

word = words[random.randint(0, len(words) - 1)]

guesses = ''

turns = 10

while turns > 0:         

    failed = 0             

    for char in word:      

        if char in guesses:    
    
            print (char, end=" ")

        else:
    
            print ("_", end=" ")
       
            failed += 1    

    if failed == 0:        
        print ("\nJe hebt het woord geraden!")  

        break              


    guess = input("\nTyp een letter...")
    print("\n")

    guesses += guess                    

    if guess not in word:  
 
        turns -= 1        
 
        print ("\nFout!")
 
        print ("Je hebt nog " + str(turns) + " pogingen")
 
        if turns == 0:           
    
            print ("Je hebt het woord niet geraden :(")
            print ("Het woord was: " + word)
```
