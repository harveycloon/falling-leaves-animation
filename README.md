# falling-leaves-animation
import pygame
import random

# Initialize pygame
pygame.init()

# Screen settings
WIDTH, HEIGHT = 800, 600
screen = pygame.display.set_mode((WIDTH, HEIGHT))
pygame.display.set_caption("🍂 Falling Leaves Animation 🍁")

# Load leaf images
leaf_images = [pygame.image.load("leaf1.png"), pygame.image.load("leaf2.png"), pygame.image.load("leaf3.png")]
leaf_images = [pygame.transform.scale(img, (40, 40)) for img in leaf_images]

# Colors
SKY_BLUE = (135, 206, 250)

# Leaf class
class Leaf:
    def __init__(self):
        self.image = random.choice(leaf_images)
        self.x = random.randint(0, WIDTH)
        self.y = random.randint(-100, -40)
        self.speed_y = random.uniform(1, 3)
        self.speed_x = random.uniform(-1, 1)
        self.angle = random.uniform(0, 360)
        self.rotation_speed = random.uniform(-2, 2)

    def move(self):
        self.y += self.speed_y
        self.x += self.speed_x
        self.angle += self.rotation_speed
        if self.y > HEIGHT:
            self.y = random.randint(-100, -40)
            self.x = random.randint(0, WIDTH)

    def draw(self, screen):
        rotated_image = pygame.transform.rotate(self.image, self.angle)
        screen.blit(rotated_image, (self.x, self.y))

# Create leaf list
leaves = [Leaf() for _ in range(20)]

running = True
clock = pygame.time.Clock()

while running:
    screen.fill(SKY_BLUE)
    
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False
    
    # Update and draw leaves
    for leaf in leaves:
        leaf.move()
        leaf.draw(screen)
    
    pygame.display.flip()
    clock.tick(30)

pygame.quit()
