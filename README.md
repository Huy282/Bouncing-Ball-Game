import pygame
import random

pygame.init()

WIDTH, HEIGHT = 600, 600
screen = pygame.display.set_mode((WIDTH, HEIGHT))
pygame.display.set_caption("Bouhncing Ball Game")

BG_COLOR = (255, 255, 255)
BALL_RADIUS = 25
BALL_COLOR = (255, 0, 0)
ball_pos = [WIDTH // 2, HEIGHT // 2 ]
ball_speed = [random.choice([-7,7]), random.choice([-7,7])]

bounce_sound = pygame.mixer.Sound("bounce.wav")

running = True
clock = pygame.time.Clock()

while running:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False
    ball_pos[0] += ball_speed[0]
    ball_pos[1] += ball_speed[1]

    if ball_pos[0] <= BALL_RADIUS or ball_pos[0] >= WIDTH - BALL_RADIUS:
        ball_speed[0] = -ball_speed[0]
        bounce_sound.play()
    if ball_pos[1] <= BALL_RADIUS or ball_pos[1] >= HEIGHT - BALL_RADIUS:
        ball_speed[1] = -ball_speed[1]
        bounce_sound.play()   

    screen.fill(BG_COLOR)
    pygame.draw.circle(screen, BALL_COLOR, ball_pos, BALL_RADIUS)
    pygame.display.flip()

    clock.tick(120)  # 120 FPS

pygame.quit()
