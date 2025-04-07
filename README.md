# vinyl-record-generator
import pygame
import math

# Initialize pygame
pygame.init()

# Screen settings
WIDTH, HEIGHT = 600, 600
screen = pygame.display.set_mode((WIDTH, HEIGHT))
pygame.display.set_caption("Vinyl Record Simulator 🎵")

# Colors
BLACK = (0, 0, 0)
WHITE = (255, 255, 255)
GRAY = (50, 50, 50)

# Load music
pygame.mixer.init()
pygame.mixer.music.load("music.mp3")  # Ensure you have a music.mp3 file in the directory
pygame.mixer.music.play(-1)  # Loop music

# Vinyl settings
record_center = (WIDTH // 2, HEIGHT // 2)
record_radius = 200
angle = 0

running = True
clock = pygame.time.Clock()

while running:
    screen.fill(BLACK)
    
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False
    
    # Draw vinyl record
    pygame.draw.circle(screen, GRAY, record_center, record_radius)
    pygame.draw.circle(screen, BLACK, record_center, record_radius - 20)
    pygame.draw.circle(screen, WHITE, record_center, 10)  # Center hole
    
    # Simulate spinning effect with a moving line
    line_length = record_radius - 20
    line_x = record_center[0] + math.cos(angle) * line_length
    line_y = record_center[1] + math.sin(angle) * line_length
    pygame.draw.line(screen, WHITE, record_center, (line_x, line_y), 3)
    angle += 0.05  # Adjust spin speed
    
    pygame.display.flip()
    clock.tick(60)

pygame.quit()
