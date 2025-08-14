import pygame
import time
import random

pygame.init()

# Constants
SCREEN_HEIGHT = 1000
SCREEN_WIDTH = 1750
bot = 1

p1x = 500
p2x = 1000

healthp1 = 100
healthp2 = 100

stamp1 = 100
stamp2 = 100

classp1 = 0
classp2 = 0

#0 = norm
#1 = stam
#2 = atk
#3 = def
atkspeed1 = 0.25
atkspeed2 = 0.25

dmg1 = 1
dmg2 = 1

block1 = 1
block2 = 10

sprite1 = 0
sprite2 = 0

x = 0
wait = float("inf")
#sprite chart
#normal = 0
#jab = 1
#cross = 2
#kick = 3
#block = 4


atk = False

if classp1 == 1:
	x = 0.1
	dmg1 = 0.7
	stamp1 = 115
if classp1 == 2:
	x = 0
	dmg1 = 1.7
	atkspeed1 = 0.5
if classp1 == 3:
	x = 0
	block = 12
	dmg1 = 0.7

if classp2 == 2:
	atkspeed2 = 0.2
	dmg2 = 0.7
	stamp2 = 115
if classp2 == 2:
	dmg2 = 1.7
	atkspeed2 = 0.5
if classp2 == 3:
	block = 12
	dmg2 = 0.7

clock = pygame.time.Clock()
FPS = 40



screen = pygame.display.set_mode((SCREEN_WIDTH, SCREEN_HEIGHT))
pygame.display.set_caption("Fighting Game")




#make this automate my file loading after im done with everything
normalp1 = pygame.image.load(R"C:\Users\sushi\OneDrive\Desktop\Assets folder\cropped boxing\normalp1.png")
normalp1 = pygame.transform.scale_by(normalp1,(12,12))
normalp2 = pygame.image.load(R"C:\Users\sushi\OneDrive\Desktop\Assets folder\cropped boxing\normalp2.png")
normalp2 = pygame.transform.scale_by(normalp2,(12,12))
jabp1 = pygame.image.load(R"C:\Users\sushi\OneDrive\Desktop\Assets folder\cropped boxing\jabp1.png")
jabp1 = pygame.transform.scale_by(jabp1,(12,12))
jabp2 = pygame.image.load(R"C:\Users\sushi\OneDrive\Desktop\Assets folder\cropped boxing\jabp2.png")
jabp2 = pygame.transform.scale_by(jabp2,(12,12))
crossp1 = pygame.image.load(R"C:\Users\sushi\OneDrive\Desktop\Assets folder\cropped boxing\crossp1.png")
crossp1 = pygame.transform.scale_by(crossp1,(12,12))
crossp2 = pygame.image.load(R"C:\Users\sushi\OneDrive\Desktop\Assets folder\cropped boxing\crossp2.png")
crossp2 = pygame.transform.scale_by(crossp2,(12,12))
kickp1 = pygame.image.load(R"C:\Users\sushi\OneDrive\Desktop\Assets folder\cropped boxing\kickp1.png")
kickp1 = pygame.transform.scale_by(kickp1,(12,12))
kickp2 = pygame.image.load(r"C:\Users\sushi\OneDrive\Desktop\Assets folder\cropped boxing\kickp2.png")
kickp2 = pygame.transform.scale_by(kickp2,(12,12))

ground = pygame.Rect(0, 800, 1750, 200)

healthbar1 = pygame.Rect(10,10, int(healthp1),10)
stambar1 = pygame.Rect(10,10,stamp1,10)

healthbar2 = pygame.Rect(10,10, int(healthp2),10)
stambar2 = pygame.Rect(10,10,stamp2,10)

hitbox_p1 = pygame.Rect(p1x,0,288,432)

game = True


while game:
    
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False

    healthbar1 = pygame.Rect(40,60, healthp1*5,30)
    stambar1 = pygame.Rect(40,120, stamp1*5,30)

    healthbar2 = pygame.Rect(1210,60, int(healthp2)*5,30)
    stambar2 = pygame.Rect(1210,120,stamp2*5,30)
    
    
    screen.fill((0, 0, 0))  



    
    pygame.draw.rect(screen, "tan", ground)

    pygame.draw.rect(screen, "green", healthbar1)
    pygame.draw.rect(screen,"white",stambar1)

    pygame.draw.rect(screen, "green", healthbar2)
    pygame.draw.rect(screen,"white",stambar2)

    
   	
    if sprite1 == 0 or sprite1 == 4:
    	screen.blit(normalp1, (p1x, 368))
    	hitbox_p1 = pygame.Rect(p1x,386,252,432)
    elif sprite1 == 1:
    	screen.blit(jabp1,(p1x,368))
    	hitbox_p1 = pygame.Rect(p1x,386,288,432)
    elif sprite1 == 2:
    	hitbox_p1 = pygame.Rect(p1x,386,264,432)
    	screen.blit(crossp1,(p1x,368))
    elif sprite1 == 3:
    	screen.blit(kickp1,(p1x,368))
    	hitbox_p1 = pygame.Rect(p1x,386,276,432)
    if sprite2 == 0:
    	screen.blit(normalp2, (p2x, 368)) 
    	hitbox_p2 = pygame.Rect(p2x,386,252,432)
    elif sprite2 == 1:

    elif sprite2 == 2:

    elif sprite2 == 3:



  


    key = pygame.key.get_pressed()
    if p1x - 150 != p2x:
	    if key[pygame.K_a] == True:
	           
	        p1x = p1x-10
    if p1x + 150 != p2x:
	    if key[pygame.K_d] == True:

	        p1x = p1x+10

    if sprite1 == 3:
    	atkspeed1 = 0.8-x
    elif sprite1 == 2:
    	atkspeed1 == 0.4-x
    elif sprite1 == 1:
    	atkspeed1 == 0.25-x
    if sprite1 == 0:
    	if key[pygame.K_k] == True:
    		wait = time.time()
    		sprite1 = 3
    		stam = 3
    		stamp1 = stamp1 - stam
    if sprite1 == 0:
    	if key[pygame.K_j]:
    		wait = time.time()
    		sprite1= 1
    		stam = 0.5
    		stamp1 = stamp1- stam
    if sprite1 == 0:
	    if key[pygame.K_h]:
	    	wait = time.time()
	    	sprite1 = 2
	    	stam = 1
	    	stamp1 = stamp1 - stam
    if wait + atkspeed1 <= time.time():
    	sprite1 = 0

    if key[pygame.K_s] == True:
    	print('block')
    	if sprite2 == 1 or sprite2 == 2 or sprite2 == 3 :
    		if collide(kickp2) or collide(jabp2) or collide(crossp2):
    			block == block-1








    	
    	
    
                


    
    pygame.display.update()
    clock.tick(FPS)
    
   


pygame.quit()

