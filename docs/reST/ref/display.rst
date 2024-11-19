import pygame
import sys

# Initialize Pygame
pygame.init()

# Screen settings
WIDTH, HEIGHT = 800, 600
screen = pygame.display.set_mode((WIDTH, HEIGHT))
pygame.display.set_caption("Simple Football Game")

# Colors
WHITE = (255, 255, 255)
GREEN = (0, 128, 0)
RED = (255, 0, 0)
BLUE = (0, 0, 255)

# Ball and players
ball = pygame.Rect(WIDTH//2, HEIGHT//2, 20, 20)
player1 = pygame.Rect(50, HEIGHT//2 - 50, 20, 100)
player2 = pygame.Rect(WIDTH - 70, HEIGHT//2 - 50, 20, 100)

# Ball movement
ball_speed_x = 4
ball_speed_y = 4

# Clock
clock = pygame.time.Clock()

# Main game loop
while True:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            pygame.quit()
            sys.exit()
    
    # Player controls
    keys = pygame.key.get_pressed()
    if keys[pygame.K_w]:
        player1.y -= 5
    if keys[pygame.K_s]:
        player1.y += 5
    if keys[pygame.K_UP]:
        player2.y -= 5
    if keys[pygame.K_DOWN]:
        player2.y += 5

    # Ball movement
    ball.x += ball_speed_x
    ball.y += ball_speed_y

    # Collision with walls
    if ball.top <= 0 or ball.bottom >= HEIGHT:
        ball_speed_y *= -1

    # Collision with players
    if ball.colliderect(player1) or ball.colliderect(player2):
        ball_speed_x *= -1

    # Draw everything
    screen.fill(GREEN)
    pygame.draw.rect(screen, RED, player1)
    pygame.draw.rect(screen, BLUE, player2)
    pygame.draw.ellipse(screen, WHITE, ball)
    pygame.draw.aaline(screen, WHITE, (WIDTH//2, 0), (WIDTH//2, HEIGHT))

    pygame.display.flip()
    clock.tick(60)
