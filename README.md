# ping-pong
HOW to build a game
import pygame

# Initialize pygame and create a window
pygame.init()
screen = pygame.display.set_mode((800, 600))
pygame.display.set_caption("Ping Pong")

# Create the paddles and ball
paddle1 = pygame.Rect(10, 250, 20, 100)
paddle2 = pygame.Rect(770, 250, 20, 100)
ball = pygame.Rect(390, 290, 20, 20)

# Create the ball's velocity vector
ball_velocity = [5, 5]

# Create the paddles' velocity variables
paddle1_velocity = 0
paddle2_velocity = 0

# Main game loop
running = True
while running:
    for event in pygame.event.get():
        # Handle quitting the game
        if event.type == pygame.QUIT:
            running = False

        # Handle movement of paddles
        if event.type == pygame.KEYDOWN:
            if event.key == pygame.K_w:
                paddle1_velocity = -5
            elif event.key == pygame.K_s:
                paddle1_velocity = 5
            elif event.key == pygame.K_UP:
                paddle2_velocity = -5
            elif event.key == pygame.K_DOWN:
                paddle2_velocity = 5
        elif event.type == pygame.KEYUP:
            if event.key in (pygame.K_w, pygame.K_s):
                paddle1_velocity = 0
            elif event.key in (pygame.K_UP, pygame.K_DOWN):
                paddle2_velocity = 0

    # Move the paddles
    paddle1.y += paddle1_velocity
    paddle2.y += paddle2_velocity

    # Check if paddles are going off screen
    if paddle1.top < 0:
        paddle1.top = 0
    elif paddle1.bottom > 600:
        paddle1.bottom = 600
    if paddle2.top < 0:
        paddle2.top = 0
    elif paddle2.bottom > 600:
        paddle2.bottom = 600

    # Move the ball
    ball.x += ball_velocity[0]
    ball.y += ball_velocity[1]

    # Check if ball is going off screen
    if ball.top < 0 or ball.bottom > 600:
        ball_velocity[1] = -ball_velocity[1]
    if ball.left < 0:
        ball_velocity[0] = -ball_velocity[0]
    elif ball.right > 800:
        ball_velocity[0] = -ball_velocity[0]

    # Check if ball hit paddles
    if ball.colliderect(paddle1) or ball.colliderect(paddle2):
        ball_velocity[0] = -ball_velocity[0]

    # Clear the screen
    screen.fill((255, 255, 255))

    # Draw the paddles and ball
    pygame.draw.rect(screen,
