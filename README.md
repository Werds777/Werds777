import pygame
import sys

# Инициализация Pygame
pygame.init()

# Константы для цветов
BLACK = (0, 0, 0)
WHITE = (255, 255, 255)
RED = (255, 0, 0)

# Размеры экрана
SCREEN_WIDTH = 800
SCREEN_HEIGHT = 600

# Создание экрана
screen = pygame.display.set_mode((SCREEN_WIDTH, SCREEN_HEIGHT))
pygame.display.set_caption("Mario")

# Класс для игрока (Марио)
class Player(pygame.sprite.Sprite):
    def __init__(self):
        super().__init__()
        self.image = pygame.Surface((50, 50))
        self.image.fill(RED)
        self.rect = self.image.get_rect()
        self.rect.center = (SCREEN_WIDTH // 2, SCREEN_HEIGHT // 2)
        self.speed = 5

    def update(self):
        keys = pygame.key.get_pressed()
        if keys[pygame.K_LEFT]:
            self.rect.x -= self.speed
        if keys[pygame.K_RIGHT]:
            self.rect.x += self.speed

# Главный игровой цикл
def main():
    # Создание игрока
    player = Player()

    # Создание группы спрайтов и добавление игрока в эту группу
    all_sprites = pygame.sprite.Group()
    all_sprites.add(player)

    # Главный цикл игры
    running = True
    while running:
        # Обработка событий
        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                running = False

        # Обновление игры
        all_sprites.update()

        # Отрисовка игры
        screen.fill(WHITE)
        all_sprites.draw(screen)
        pygame.display.flip()

        # Задержка для правильной скорости обновления экрана
        pygame.time.Clock().tick(30)

    # Выход из игры
    pygame.quit()
    sys.exit()

if __name__ == "__main__":
    main() 
