import pygame
import sys
# initialisation de pygame
pygame.init()

# configuration de la fenêtre
LARGEUR, HAUTEUR = 800, 600
fenêtre = pygame.display.set_mode((LARGEUR, HAUTEUR))
pygame.display.set_caption("déplacement du Cube")

# couleurs (R, G, B)
NOIR = (0, 0, 0)
ROUGE = (255, 50, 50)

# propriétés du cube
taille_cube = 50
x = LARGEUR // 2 - taille_cube // 2 # Position X initiale (au centre)
y = HAUTEUR // 2 - taille_cube // 2 # Position Y initiale (au centre)
vitesse = 5                         # vitesse de deplacement

# Horloge pour contrôler les images par seconde (FPS)
horloge = pygame.time.Clock()

# Boucle principale du jeu 
en_cours = True
while en_cours:
    # 1. Gestion des evenements (fermeture du jeu)
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            en_cours = False

    # 2. Gestion des touches enfoncées
    touches = pygame.key.get_pressed()

    if (touches[pygame.K_LEFT] or touches[pygame.K_q]) and x > 0:
        x -= vitesse
    if (touches[pygame.K_RIGHT] or touches[pygame.K_d]) and x < LARGEUR - taille_cube:
        x += vitesse
    if (touches[pygame.K_UP] or touches[pygame.K_z]) and y > 0:
        y -= vitesse
    if (touches[pygame.K_DOWN] or touches[pygame.K_s]) and y < HAUTEUR - taille_cube:
        y += vitesse

    # 3. Affichage / Dessin
    fenetre.fill(NOIR)  # Efface l'écran précédent
    pygame.draw.rect(fenetre, ROUGE, (x, y, taille_cube, taille_cube))  # Dessine le cube

    # 4. Mettre à jour l'écran
    pygame.display.flip()

    # Limiter le jeu à 60 FPS
    horloge.tick(60)

# Quitter Pygame proprement
pygame.quit()
sys.exit()
