https://wikidocs.net/66228

import pygame #파이 게임 모듈 임포트
import random

pygame.init() #파이 게임 초기화
SCREEN_WIDTH = 600
SCREEN_HEIGHT = 800
screen = pygame.display.set_mode((SCREEN_WIDTH, SCREEN_HEIGHT)) #화면 크기 설정
clock = pygame.time.Clock() 

#변수

BLACK = (0, 0, 0)
RED = (255, 0, 0)
YELLOW = (255, 255, 0)
#font_name = 'malgungothic' #윈도우
font_name = 'applegothicttf' #맥
large_font = pygame.font.SysFont(font_name, 72)
small_font = pygame.font.SysFont(font_name, 36)
score = 0
game_over = False

bomb_image = pygame.image.load('bomb.png')
bombs = []
for i in range(2):
    bomb = pygame.Rect(bomb_image.get_rect())
    bomb.left = random.randint(0, SCREEN_WIDTH)
    bomb.top = -100
    dy = random.randint(3, 9)
    bombs.append((bomb, dy))

girl_image = pygame.image.load('girl.png')
girl = pygame.Rect(girl_image.get_rect())
girl.left = SCREEN_WIDTH // 2 - girl.width // 2
girl.top = SCREEN_HEIGHT - girl.height
girl_dx = 0
girl_dy = 0

pygame.mixer.music.load('music.mid') #배경 음악
pygame.mixer.music.play(-1) #-1: 무한 반복, 0: 한번
game_over_sound = pygame.mixer.Sound('game_over.wav')

while True: #게임 루프
    screen.fill(BLACK) #단색으로 채워 화면 지우기

    #변수 업데이트

    event = pygame.event.poll() #이벤트 처리
    if event.type == pygame.QUIT:
        break
    elif event.type == pygame.KEYDOWN and game_over == 0:
        if event.key == pygame.K_LEFT:
            girl_dx = -5
        elif event.key == pygame.K_RIGHT:
            girl_dx = 5
    elif event.type == pygame.KEYUP and game_over == 0:
        if event.key == pygame.K_LEFT:
            girl_dx = 0
        elif event.key == pygame.K_RIGHT:
            girl_dx = 0

    if game_over == 0:  
        for (bomb, dy) in bombs:
            bomb.top += dy
            if bomb.top > SCREEN_HEIGHT:
                bombs.remove((bomb, dy))
                bomb = pygame.Rect(bomb_image.get_rect())
                bomb.left = random.randint(0, SCREEN_WIDTH)
                bomb.top = -100
                dy = random.randint(3, 9)
                bombs.append((bomb, dy))
                score += 1

        girl.left = girl.left + girl_dx

        if girl.left < 0:
            girl.left = 0
        elif girl.left > SCREEN_WIDTH - girl.width:
            girl.left = SCREEN_WIDTH - girl.width

        for (bomb, dy) in bombs:
            if bomb.colliderect(girl):
                #print('충돌')
                #print(bomb)
                #print(girl)
                game_over = True
                pygame.mixer.music.stop()
                game_over_sound.play()

    #화면 그리기

    for (bomb, dy) in bombs:
        screen.blit(bomb_image, bomb)

    screen.blit(girl_image, girl)

    score_image = small_font.render('점수 {}'.format(score), True, YELLOW)
    screen.blit(score_image, (10, 10))

    if game_over == 1:
        game_over_image = large_font.render('게임 종료', True, RED)
        screen.blit(game_over_image, (SCREEN_WIDTH // 2 - game_over_image.get_width() // 2, SCREEN_HEIGHT // 2 - game_over_image.get_height() // 2))

    pygame.display.update() #모든 화면 그리기 업데이트
    clock.tick(30) #30 FPS (초당 프레임 수) 를 위한 딜레이 추가, 딜레이 시간이 아닌 목표로 하는 FPS 값

학교에서 한버전 음악 없음

import pygame #파이 게임 모듈 임포트
import random

pygame.init() #파이 게임 초기화
SCREEN_WIDTH = 600
SCREEN_HEIGHT = 800
screen = pygame.display.set_mode((SCREEN_WIDTH, SCREEN_HEIGHT)) #화면 크기 설정
clock = pygame.time.Clock() 

#변수
background_image = pygame.image.load('background.jpg')
BLACK = (0, 0, 0)
RED = (255, 0, 0)
YELLOW = (255, 255, 0)
#font_name = 'malgungothic' #윈도우
font_name = 'applegothicttf' #맥
large_font = pygame.font.SysFont(font_name, 72)
small_font = pygame.font.SysFont(font_name, 36)
score = 0
game_over = False

bomb_image = pygame.image.load('bomb.png')
bombs = []
for i in range(2):
    bomb = pygame.Rect(bomb_image.get_rect())
    bomb.left = random.randint(0, SCREEN_WIDTH)
    bomb.top = -100
    dy = random.randint(3, 9)
    bombs.append((bomb, dy))

girl_image = pygame.image.load('girl.png')
girl = pygame.Rect(girl_image.get_rect())
girl.left = SCREEN_WIDTH // 2 - girl.width // 2
girl.top = SCREEN_HEIGHT - girl.height
girl_dx = 0
girl_dy = 0



while True: #게임 루프
    screen.fill(BLACK) #단색으로 채워 화면 지우기

    #변수 업데이트

    event = pygame.event.poll() #이벤트 처리
    if event.type == pygame.QUIT:
        break
    elif event.type == pygame.KEYDOWN and game_over == 0:
        if event.key == pygame.K_LEFT:
            girl_dx = -5
        elif event.key == pygame.K_RIGHT:
            girl_dx = 5
    elif event.type == pygame.KEYUP and game_over == 0:
        if event.key == pygame.K_LEFT:
            girl_dx = 0
        elif event.key == pygame.K_RIGHT:
            girl_dx = 0

    if game_over == 0:  
        for (bomb, dy) in bombs:
            bomb.top += dy
            if bomb.top > SCREEN_HEIGHT:
                bombs.remove((bomb, dy))
                bomb = pygame.Rect(bomb_image.get_rect())
                bomb.left = random.randint(0, SCREEN_WIDTH)
                bomb.top = -100
                dy = random.randint(3, 9)
                bombs.append((bomb, dy))
                score += 1

        girl.left = girl.left + girl_dx

        if girl.left < 0:
            girl.left = 0
        elif girl.left > SCREEN_WIDTH - girl.width:
            girl.left = SCREEN_WIDTH - girl.width

        for (bomb, dy) in bombs:
            if bomb.colliderect(girl):
                #print('충돌')
                #print(bomb)
                #print(girl)
                game_over = True
                pygame.mixer.music.stop()

    #화면 그리기

    for (bomb, dy) in bombs:
        screen.blit(bomb_image, bomb)

    screen.blit(girl_image, girl)

    score_image = small_font.render('점수 {}'.format(score), True, YELLOW)
    screen.blit(score_image, (10, 10))

    if game_over == 1:
        game_over_image = large_font.render('게임 종료', True, RED)
        screen.blit(game_over_image, (SCREEN_WIDTH // 2 - game_over_image.get_width() // 2, SCREEN_HEIGHT // 2 - game_over_image.get_height() // 2))

    pygame.display.update() #모든 화면 그리기 업데이트
    clock.tick(30) #30 FPS (초당 프레임 수) 를 위한 딜레이 추가, 딜레이 시간이 아닌 목표로 하는 FPS 값
