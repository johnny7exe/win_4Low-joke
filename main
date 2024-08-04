import win32gui
import win32con
import time
import threading
import random
import pygame

# Функция для сворачивания всех окон
def minimize_all():
    hwnd = win32gui.GetForegroundWindow()
    win32gui.ShowWindow(hwnd, win32con.SW_MINIMIZE)

# Функция для вывода надписи
def show_message():
    pygame.init()
    screen = pygame.display.set_mode((800, 600), pygame.NOFRAME, pygame.SRCALPHA)
    tr_sur = pygame.Surface((800, 600), pygame.SRCALPHA)
    tr_sur.fill((0, 0, 0, 0))
    screen.blit(tr_sur, (0, 0))
    font = pygame.font.Font(None, 72)
    text = font.render("С ДР, дружок!", True, (255, 255, 255))
    text_rect = text.get_rect(center=(400, 300))
    screen.blit(text, text_rect)
    pygame.display.flip()
    time.sleep(180)
    pygame.quit()

# Функция для запуска салюта
def launch_firework(x, y):
    for _ in range(10):
        color = (random.randint(0, 255), random.randint(0, 255), random.randint(0, 255))
        radius = random.randint(5, 15)
        pygame.draw.circle(screen, color, (x, y), radius)

        pygame.display.update()
        time.sleep(0.1)

# Функция для воспроизведения музыки
def play_music():
    pygame.mixer.init()
    pygame.mixer.music.load("Frank Sinatra_happy Birthday.mp3")  # Замените на путь к вашему файлу
    pygame.mixer.music.play()
    for event in pygame.event.get():
        if event.type == pygame.mixer.music.get_endevent():
            print("финиш")
    # while pygame.mixer.music.get_busy():
    #     pygame.time.Clock().tick(5000)

# Запускаем потоки для салютов
firework_threads = []
for _ in range(5):
    x = random.randint(0, 800)
    y = random.randint(500, 600)
    thread = threading.Thread(target=launch_firework, args=(x, y))
    firework_threads.append(thread)
    thread.start()

# Сворачиваем окна
minimize_all()

# Запускаем потоки для надписи и музыки
message_thread = threading.Thread(target=show_message)
music_thread = threading.Thread(target=play_music)
message_thread.start()
music_thread.start()

while True:
    if not pygame.mixer.music.get_busy():
        break
    time.sleep(1)

# Ожидаем завершения потоков
for thread in firework_threads:
    thread.join()
message_thread.join()
music_thread.join()
