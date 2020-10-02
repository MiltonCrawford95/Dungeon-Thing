import pygame
import sys
from pygame.locals import *
pygame.init()


walk_right1 = [pygame.image.load('Maze/R1.jpg'), pygame.image.load(
    'Maze/R2.jpg'), pygame.image.load('Maze/R3.jpg')]
walk_left1 = [pygame.image.load('Maze/L1.jpg'), pygame.image.load(
    'Maze/L2.jpg'), pygame.image.load('Maze/L3.jpg')]
walk_forward1 = [pygame.image.load('Maze/F1.jpg'), pygame.image.load(
    'Maze/FL1.jpg'), pygame.image.load('Maze/FR1.jpg')]
walk_back1 = [pygame.image.load(
    'Maze/BL1.jpg'), pygame.image.load('Maze/BR1.jpg')]
character_still1 = pygame.image.load('Maze/B1.jpg')
background_image = pygame.image.load('Maze/Thisone.jpg')

clock = pygame.time.Clock()

# Screen
width = 800
height = 802
background_color = (255, 255, 255)

# Players
player_size = 32

player_color1 = (255, 0, 0)
player1_position = [width/2, height - 2 * (player_size)]
x1 = player1_position[0]
y1 = player1_position[1]
left1 = False
right1 = False
forward1 = False
backward1 = False
walk_count1x = 0
walk_count1y = 0

player_color2 = (0, 255, 0)
player2_position = [(width/2) - (player_size),
                    (height - (2 * (player_size)))]
x2 = player2_position[0]
y2 = player2_position[1]
left2 = False
right2 = False
forward2 = False
backward2 = False
walk_count2x = 0
walk_count2y = 0

player_color3 = (0, 0, 255)
player3_position = [(width/2) + (player_size),
                    (height - (2 * (player_size)))]
x3 = player3_position[0]
y3 = player3_position[1]
left3 = False
right3 = False
forward3 = False
backward3 = False
walk_count3x = 0
walk_count3y = 0




def redraw_game_window():
    global walk_count1x
    global walk_count1y
    global walk_count2x
    global walk_count2y
    global walk_count3x
    global walk_count3y

    screen.blit(background_image, (0, 0))

    if walk_count1x + 1 >= 100:
        walk_count1x = 0
    if left1:
        screen.blit(walk_left1[walk_count1x // 3], (x1, y1))
        walk_count1x += 1
    elif right1:
        screen.blit(walk_right1[walk_count1x // 3], (x1, y1))
        walk_count1x += 1

    if walk_count1y + 1 >= 100:
        walk_count1y = 0
    if forward1:
        screen.blit(walk_forward1[walk_count1y // 3], (x1, y1))
        walk_count1y += 1
    elif backward1:
        screen.blit(walk_back1[walk_count1y // 3], (x1, y1))
        walk_count1y += 1
    else:
        screen.blit(character_still1, (x1, y1))

    pygame.draw.rect(screen, (player_color2),
                     (player2_position[0], player2_position[1], player_size, player_size))

    pygame.draw.rect(screen, (player_color3),
                     (player3_position[0], player3_position[1], player_size, player_size))


screen = pygame.display.set_mode((height, width))
pygame.display.set_caption("Dungeon Thing")

game_over = False

while not game_over:

    clock.tick(30)

    for event in pygame.event.get():

        if event.type == pygame.QUIT:
            sys.exit()

    # player mvmt

        if event.type == pygame.KEYDOWN:
            x1 = player1_position[0]
            y1 = player1_position[1]

            # Player1 mvmt
            # X-Axis
            if event.key == pygame.K_LEFT:
                x1 -= (player_size)
                if x1 <= 1:
                    x1 = player1_position[0]
                left1 = True
                right1 = False
            elif event.key == pygame.K_RIGHT:
                x1 += player_size
                if x1 >= (width-(player_size)):
                    x1 = player1_position[0]
                right1 = True
                left1 = False
            else:
                right1 = False
                left1 = False
                walk_count1x = 0

            # Y-Axis
            if event.key == pygame.K_UP:
                y1 -= player_size
                if y1 <= -2:
                    y1 = player1_position[1]
                forward1 = True
                backward1 = False
            elif event.key == pygame.K_DOWN:
                y1 += player_size
                if y1 >= height:
                    y1 = player1_position[-1]
                backward1 = True
                forward1 = False
            else:
                forward1 = False
                backward1 = False
                walk_count1y = 0

        if event.type == pygame.KEYDOWN:
            x2 = player2_position[0]
            y2 = player2_position[1]
            # Player2 mvmt
            # X axis
            if event.key == pygame.K_a:
                x2 -= player_size
                if x2 <= -1:
                    x2 = player2_position[0]
                left2 = True
                right2 = False
            elif event.key == pygame.K_d:
                x2 += player_size
                if x2 >= (width - (player_size)):
                    x2 = player2_position[0]
                right2 = True
                left2 = False
            else:
                right2 = False
                left2 = False
                walk_count2x = 0

            # Y Axis
            if event.key == pygame.K_w:
                y2 -= player_size
                if y2 <= -2:
                    y2 = player2_position[1]
                forward2 = True
                backward2 = False
            elif event.key == pygame.K_s:
                y2 += player_size
                if y2 >= height:
                    y2 = player2_position[-1]
                backward2 = True
                forward2 = False
            else:
                backward2 = False
                forward2 = False
                walk_count2y = 0

        if event.type == pygame.KEYDOWN:
            x3 = player3_position[0]
            y3 = player3_position[1]
            # Player 3 mvmt:
            # X Axis
            if event.key == pygame.K_j:
                x3 -= player_size
                if x3 <= 1:
                    x3 = player3_position[0]
                left3 = True
                right3 = False
            elif event.key == pygame.K_l:
                x3 += player_size
                if x3 >= (width - (player_size)):
                    x3 = player3_position[0]
                right3 = True
                left3 = False
            else:
                right3 = False
                left3 = False
                walk_count3x = 0

            # Y Axis
            if event.key == pygame.K_i:
                y3 -= player_size
                if y3 <= -2:
                    y3 = player3_position[1]
                forward3 = True
                backward3 = False
            elif event.key == pygame.K_k:
                y3 += player_size
                if y3 >= height:
                    y3 = player3_position[-1]
                backward3 = True
                forward3 = False
            else:
                forward3 = False
                backward3 = False
                walk_count3y = 0

        player1_position = [x1, y1]
        player2_position = [x2, y2]
        player3_position = [x3, y3]

        redraw_game_window()

        pygame.display.update()
