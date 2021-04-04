from tkinter import*
from time import*
from random import*
window = Tk()
c = Canvas(window, height=400, width=300, bg='black')
l = Text(window, height=1, width=6)
l.pack()
c.pack()
player = c.create_rectangle(0, 380, 20, 400, fill='white', outline='white')
c.move(player, 140, 0)
s = Text(window, height=1, width=6)
s.pack()
b = Text(window, height=1, width=6)
b.pack()
play = c.create_rectangle(0, 0, 80, 40, fill='white', outline='white')
tlay = c.create_text(150, 220, text='[L]PLAY', fill='black', font=('', 15))
title = c.create_text(150, 90, text='ASTEROID', fill='white', font=('', 30))
Quit = c.create_rectangle(0, 0, 80, 40, fill='white', outline='white')
tuit = c.create_text(150, 270, text='[Q]QUIT', fill='black', font=('', 15))
pause = c.create_rectangle(0, 0, 80, 40, fill='white', outline='white')
tause = c.create_text(40, 30, text='[P]PAUSE', fill='black', font=('', 15))
c.move(play, 110, 200)
c.itemconfig(player, state=HIDDEN)
c.move(Quit, 110, 250)
c.move(pause, 0, 10)
class tetris:
    blocks = []
    score = 0
    bullet = []
    wait = 0.1
    lives = 3
    bullets = 20
    powers = []
    interface = 'menu'
def reset_settings():
    tetris.score = ''
    tetris.lives = ''
    tetris.bullets = ''
def game_settings():
    tetris.score = 0
    tetris.lives = 3
    tetris.bullets = 20
def move(d):
    if d == "Up" and not c.coords(player)[1] <= 0:
        c.move(player, 0, -10)
    elif d == "Left" and not c.coords(player)[0] <= 0:
        c.move(player, -10, 0)
    elif d == "Right" and not c.coords(player)[2] >= 300:
        c.move(player, 10, 0)
    elif d == "Down" and not c.coords(player)[3] >= 400:
        c.move(player, 0, 10)
def ccreate():
    return put_block(randint(0, 29), 'pink')
def reload():
    if tetris.bullets < 20:
        tetris.bullets = tetris.bullets + 1
def move_player(direction):
    d = direction.keysym
    di = direction
    move(d)
    if di.char == ' ' and tetris.interface == 'playing':
        shoot()
    if di.char == 'l' and tetris.interface == 'menu':
        tetris.interface = 'playing'
        game_settings()
    elif di.char == 'q' and tetris.interface == 'menu':
        quit()
    elif di.char == 'm' and tetris.interface == 'lose' or tetris.interface == 'pause':
        tetris.interface = 'menu'
    elif di.char == 'p' and tetris.interface == 'playing':
        tetris.interface = 'pause'
def event(event):
    move_player(event)
c.bind_all('<Key>', event)
def menu(e):
    if tetris.interface == 'lose' or tetris.interface == 'pause':
        tetris.interface = 'menu'
c.bind_all('<Key-m>', menu)
def resume(e):
    if tetris.interface == 'pause':
        tetris.interface = 'playing'
        game_settings()
c.bind_all('<Key-r>', resume)
def shoot():
    if not tetris.bullets == 0:
        tetris.bullets = tetris.bullets - 1
        p = c.coords(player)
        tetris.bullet.append(c.create_rectangle(p[0], p[1], p[2], p[3], fill='white', outline='white'))
def put_block(x, col):
    x = x * 10
    y = 0
    if col == 'pink':
        out = 'white'
    else:
        out = col
    return c.create_rectangle(x, y, x + 10, y + 10, fill=col, outline=out)
def move_block(num):
    c.move(num, 0, 10)
def create():
    return put_block(randint(0, 29), choice(['green', 'red', 'yellow', 'blue']))
def stringer(List):
    s = ''
    for i in List:
        s = s + str(i)
    return s
def ffind(l, o):
    count = 0
    for i in l:
        if i == o:
            re = count
            break
        count += 1
    return count
while True:
    if tetris.interface == 'playing':
        c.itemconfig(pause, state=NORMAL)
        c.itemconfig(tause, state=NORMAL)
        c.itemconfig(title, state=HIDDEN)
        c.itemconfig(play, state=HIDDEN)
        c.itemconfig(tlay, state=HIDDEN)
        c.itemconfig(Quit, state=HIDDEN)
        c.itemconfig(tuit, state=HIDDEN)
        c.itemconfig(player, state=NORMAL)
        if randint(0, 5) == 0:
            tetris.blocks.append(create())
        elif randint(0, 10) == 0:
            tetris.powers.append(ccreate())
        if tetris.lives == 0:
            c.itemconfig(player, state=HIDDEN)
            tetris.interface = 'lose'
        for i in tetris.blocks:
            if len(c.coords(i)) == 4:
                move_block(i)
                if c.coords(i)[3] == 410:
                    c.delete(i)
                    del tetris.blocks[ffind(tetris.blocks, i)]
        for i in tetris.powers:
            if len(c.coords(i)) == 4:
                move_block(i)
                if c.coords(i)[3] == 410:
                    c.delete(i)
                    del tetris.powers[ffind(tetris.powers, i)]
        for i in tetris.bullet:
            c.move(i, 0, -10)
            if c.coords(i)[1] == 0:
                c.delete(i)
                del tetris.bullet[ffind(tetris.bullet, i)]
            else:
                for o in tetris.blocks:
                    if len(c.coords(i)) == 4 and len(c.coords(o)) == 4:
                        op = c.coords(o)
                        ip = c.coords(i)
                        if ((op[3] == ip[1] or op[1] == ip[1]) and (op[0] == ip[0] or op[2] == ip[2])):
                            c.delete(o)
                            del tetris.blocks[ffind(tetris.blocks, o)]
                            tetris.score = tetris.score + 1
                            del tetris.bullet[ffind(tetris.bullet, i)]
                            c.delete(i)
        i = player
        for o in tetris.blocks:
                    if len(c.coords(i)) == 4 and len(c.coords(o)) == 4:
                        op = c.coords(o)
                        ip = c.coords(i)
                        if ((op[3] == ip[1] or op[1] == ip[1]) and (op[0] == ip[0] or op[2] == ip[2])):
                            c.delete(o)
                            del tetris.blocks[ffind(tetris.blocks, o)]
                            tetris.lives = tetris.lives - 1
        for o in tetris.powers:
                    if len(c.coords(i)) == 4 and len(c.coords(o)) == 4:
                        op = c.coords(o)
                        ip = c.coords(i)
                        if ((op[3] == ip[1] or op[1] == ip[1]) and (op[0] == ip[0] or op[2] == ip[2])):
                            c.delete(o)
                            del tetris.powers[ffind(tetris.powers, o)]
                            reload()
    elif tetris.interface == 'menu':
        c.itemconfig(title, state=NORMAL)
        c.itemconfig(play, state=NORMAL)
        c.itemconfig(tlay, state=NORMAL)
        c.itemconfig(Quit, state=NORMAL)
        c.itemconfig(tuit, state=NORMAL)
        c.itemconfig(player, state=HIDDEN)
        c.itemconfig(tlay, text='[L]PLAY')
        c.itemconfig(title, text='ASTEROID')
        c.itemconfig(pause, state=HIDDEN)
        c.itemconfig(tause, state=HIDDEN)
        c.itemconfig(tuit, text='[Q]QUIT')
        if True:
            for o in tetris.powers:
                c.delete(o)
                del tetris.powers[ffind(tetris.powers, o)]
            for o in tetris.blocks:
                c.delete(o)
                del tetris.blocks[ffind(tetris.blocks, o)]
            for i in tetris.bullet:
                c.delete(i)
                del tetris.bullet[ffind(tetris.bullet, i)]
        reset_settings()
    elif tetris.interface == 'lose':
        c.itemconfig(Quit, state=HIDDEN)
        c.itemconfig(tuit, state=HIDDEN)
        c.itemconfig(title, state=NORMAL)
        c.itemconfig(play, state=NORMAL)
        c.itemconfig(tlay, state=NORMAL)
        c.itemconfig(pause, state=HIDDEN)
        c.itemconfig(tause, state=HIDDEN)
        c.itemconfig(title, text='GAME OVER')
        c.itemconfig(tlay, text='[M]MENU')
    elif tetris.interface == 'pause':
        c.itemconfig(Quit, state=NORMAL)
        c.itemconfig(tuit, state=NORMAL)
        c.itemconfig(title, state=NORMAL)
        c.itemconfig(play, state=NORMAL)
        c.itemconfig(tlay, state=NORMAL)
        c.itemconfig(pause, state=HIDDEN)
        c.itemconfig(tause, state=HIDDEN)
        c.itemconfig(title, text='PAUSED')
        c.itemconfig(tuit, text='[R]RESUME')
        c.itemconfig(tlay, text='[M]MENU')
    s.delete(0.0, END)
    s.insert(END, tetris.score)
    b.delete(0.0, END)
    b.insert(END, tetris.bullets)
    l.delete(0.0, END)
    l.insert(END, tetris.lives)
    sleep(tetris.wait)
    c.update()
