import pygame
from pygame.locals import *
import random

# Inizializzazione del gioco
pygame.init()

# Definizione delle dimensioni della finestra di gioco
larghezza_finestra = 800
altezza_finestra = 600

# Creazione della finestra di gioco
schermo = pygame.display.set_mode((larghezza_finestra, altezza_finestra))
pygame.display.set_caption("Donkey Kong")

# Colori
NERO = (0, 0, 0)
BIANCO = (255, 255, 255)

# Caricamento delle immagini dei personaggi
giovanni_immagine = pygame.image.load("giovanni.png")
barile_immagine = pygame.image.load("barile.png")

# Posizione iniziale del personaggio principale
giovanni_x = 400
giovanni_y = 500

# Posizione iniziale del barile
barile_x = random.randint(50, 750)
barile_y = 50

# Velocità di movimento del personaggio principale
velocita_giovanni = 5

# Velocità di caduta del barile
velocita_barile = 3

# Variabile per il controllo del gioco in esecuzione
in_esecuzione = True

# Loop principale del gioco
while in_esecuzione:
    for event in pygame.event.get():
        if event.type == QUIT:
            in_esecuzione = False

    # Movimento del personaggio principale
    tasti = pygame.key.get_pressed()
    if tasti[K_LEFT] and giovanni_x > 0:
        giovanni_x -= velocita_giovanni
    if tasti[K_RIGHT] and giovanni_x < larghezza_finestra - giovanni_immagine.get_width():
        giovanni_x += velocita_giovanni

    # Movimento del barile
    barile_y += velocita_barile
    if barile_y > altezza_finestra:
        barile_x = random.randint(50, 750)
        barile_y = 50

    # Controllo delle collisioni tra il personaggio principale e il barile
    if giovanni_x < barile_x + barile_immagine.get_width() and giovanni_x + giovanni_immagine.get_width() > barile_x \
            and giovanni_y < barile_y + barile_immagine.get_height() and giovanni_y + giovanni_immagine.get_height() > barile_y:
        # Game over
        in_esecuzione = False

    # Riempimento dello sfondo con il colore nero
    schermo.fill(NERO)

    # Disegno del personaggio principale e del barile
    schermo.blit(giovanni_immagine, (giovanni_x, giovanni_y))
    schermo.blit(barile_immagine, (barile_x, barile_y))

    # Aggiornamento dello schermo
    pygame.display.update()

# Chiusura del gioco
pygame.quit()
