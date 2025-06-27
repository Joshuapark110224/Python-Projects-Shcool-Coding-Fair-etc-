# Python-TypingGame

import turtle as t
import time
import random

screen = t.Screen()
screen.setup(1000,600)
screen.title("Typing Game - G8 Joshua")
screen.bgcolor("black")
#screen.bgpic("Background.gif")
screen.tracer(0)

high_easy_score = 0
high_int_score = 0
high_dif_score = 0
high_exp_score = 0

high_easy_name = ""
high_int_name = ""
high_dif_name = ""
high_exp_name = ""

try:
    with open("score.txt") as file:
        high_easy_score = int(file.readline())
        high_easy_name = file.readline().strip()
        high_int_score = int(file.readline())
        high_int_name = file.readline().strip()
        high_dif_score = int(file.readline())
        high_dif_name = file.readline().strip()
        high_exp_score = int(file.readline())
        high_exp_name = file.readline().strip()

except:
    with open("score.txt", "w") as file:
        file.write("0\n")
        file.write("no record\n")
        file.write("0\n")
        file.write("no record\n")
        file.write("0\n")
        file.write("no record\n")
        file.write("0\n")
        file.write("no record")

high_easy = str(high_easy_score) + " (" + high_easy_name + ")"
high_int = str(high_int_score) + " (" + high_int_name + ")"
high_dif = str(high_dif_score) + " (" + high_dif_name + ")"
high_exp = str(high_exp_score) + " (" + high_exp_name + ")"

#---------------- CHOOSE MODE ----------------#
pen = t.Turtle()
pen.speed(0)
pen.shape("turtle")
pen.penup()
pen.color("white")
pen.goto(-200, 200)
pen.write("Typing Game", font=("Arial", 20, "bold"))
pen.goto(330, -280)
pen.write("G8 Joshua", font=("Arial", 15, "bold"))
pen.goto(-200, 100)
pen.write("Easy (a)", font=("Arial", 15, "normal"))
pen.goto(-200, 60)
pen.write("Intermediate (a, 1)", font=("Arial", 15, "normal"))
pen.goto(-200, 20)
pen.write("Difficult (a, 1, A)", font=("Arial", 15, "normal"))
pen.goto(-200, -20)
pen.write("Expert (a, 1, A, #)", font=("Arial", 15, "normal"))
pen.goto(-400, -150)
pen.write("Highest Scores ", font=("Arial", 15, "bold"))
pen.goto(-400, -200)
pen.color("chartreuse")
pen.write("Easy: " + high_easy, font=("Arial", 15, "normal"))
pen.goto(-400, -230)
pen.color("yellow")
pen.write("Intermediate: " + high_int, font=("Arial", 15, "normal"))
pen.goto(-400, -260)
pen.color("orange")
pen.write("Difficult: " + high_dif, font=("Arial", 15, "normal"))
pen.goto(-400, -290)
pen.color("DeepPink")
pen.write("Expert: " + high_exp, font=("Arial", 15, "normal"))
pen.color("white")
pen.goto(-230, 112)

def go_down():
    pen.sety(pen.ycor() - 40)

def go_up():
    pen.sety(pen.ycor() + 40)

game_mode = 0
current_highest = ""

def enter_game():
    global game_mode, current_highest
    if pen.ycor() == 112:
        game_mode = 1
        current_highest = high_easy
    elif pen.ycor() == 72:
        game_mode = 2
        current_highest = high_int
    elif pen.ycor() == 32:
        game_mode = 3
        current_highest = high_dif
    elif pen.ycor() == -8:
        game_mode = 4
        current_highest = high_exp

#Keyboard Input
screen.listen()
screen.onkeypress(go_up, "Up")
screen.onkeypress(go_down, "Down")
screen.onkeypress(enter_game, "Return")

while True:
    screen.update()
    if game_mode != 0:
        break

pen.clear()
pen.hideturtle()

available_letters = []

def choose_letters():
    global available_letters
    if game_mode == 1:
        available_letters = ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j', 'k', 'l', 'm', 'n', 'o', 'p', 'q', 'r', 's', 't', 'u', 'v', 'w', 'x', 'y', 'z']

    elif game_mode == 2:
        available_letters = ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j', 'k', 'l', 'm', 'n', 'o', 'p', 'q', 'r', 's', 't', 'u', 'v', 'w', 'x', 'y', 'z','1', '2', '3', '4', '5', '6', '7', '8', '9', '0']
        
    elif game_mode == 3:
        available_letters = ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j', 'k', 'l', 'm', 'n', 'o', 'p', 'q', 'r', 's', 't', 'u', 'v', 'w', 'x', 'y', 'z', 'A', 'B', 'C', 'D', 'E', 'F', 'G', 'G', 'I', 'J', 'K', 'L', 'M', 'N', 'O', 'P', 'Q', 'R', 'S', 'T', 'U', 'V', 'W', 'X', 'Y', 'Z','1', '2', '3', '4', '5', '6', '7', '8', '9', '0']

    elif game_mode == 4:
        available_letters = ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j', 'k', 'l', 'm', 'n', 'o', 'p', 'q', 'r', 's', 't', 'u', 'v', 'w', 'x', 'y', 'z', 'A', 'B', 'C', 'D', 'E', 'F', 'G', 'G', 'I', 'J', 'K', 'L', 'M', 'N', 'O', 'P', 'Q', 'R', 'S', 'T', 'U', 'V', 'W', 'X', 'Y', 'Z', '1', '2', '3', '4', '5', '6', '7', '8', '9', '0']
                             
#Add later '!', '@', '#', '$', '%', '^', '&'

choose_letters()

#Score point
sp = t.Turtle()
sp.penup()
sp.goto(-450, 240)
sp.hideturtle()
sp.color("white")
sp.write("Score : 0", font=("Arial", 20, "bold"))

#Life point
lp = t.Turtle()
lp.penup()
lp.goto(-450, 210)
lp.hideturtle()
lp.color("white")
lp.write("Lives : ", font=("Arial", 20, "bold"))

lp1 = t.Turtle()
lp1.shape("circle")
lp1.penup()
lp1.color("white")
lp1.goto(-345, 225)

lp2 = t.Turtle()
lp2.penup()
lp2.shape("circle")
lp2.color("white")
lp2.goto(-315, 225)

lp3 = t.Turtle()
lp3.penup()
lp3.shape("circle")
lp3.color("white")
lp3.goto(-285, 225)

#Level
lv = t.Turtle()
lv.penup()
lv.goto(-450, 180)
lv.hideturtle()
lv.color("white")
lv.write("Level : ", font=("Arial", 20, "bold"))

# Highest score
hs = t.Turtle()
hs.penup()
hs.goto(100, 250)
hs.hideturtle()
hs.color("lightblue")
hs.write("Highest Score : " + current_highest, font=("Arial", 20, "bold"))

#Game Over
game_over = t.Turtle()
game_over.hideturtle()

score = 0
lives = 3
timer = 0
letters = {}
game_running = True

def increase_speed():
    if game_running == True:
        #print("speed increased")
        global speed
        speed = speed + 1
        screen.ontimer(increase_speed, 8000)

def add_letter():
    if game_running == True:
        l = t.Turtle()
        l.hideturtle()
        l.color("white")
        l.penup()
        l.sety(400)
        l.setx(random.randint(-480, 480)) # Random x coordinate
        letter = random.choice(available_letters)
        if letter not in letters:
            letters[letter] = l
            #letters[letter].speed(random.randint(1, 9)) # Random speed
        screen.update()
        screen.ontimer(add_letter, random.randint(50, 800))

def press_letter(x):
    global score, lives
    if x in letters:
        letters[x].clear()
        letters.pop(x)
        score += 1
        sp.clear()
        sp.write(f"Score : {score}", font=("Arial", 20, "bold"))

def play_game():
    global game_running, lives, score, game_over, speed, game_mode, high_dif, high_easy, high_int, high_exp
    global high_easy_score, high_dif_score, high_int_score, high_exp_score
    global high_easy_name, high_dif_name, high_int_name, high_exp_name
    lives = 3
    score = 0
    speed = 1
    lp.clear()
    lp.write(f"Lives : ", font=("Arial", 20, "bold"))
    lp1.showturtle()
    lp2.showturtle()
    lp3.showturtle()
    game_over.clear()

    add_letter()
    increase_speed()

    while game_running:
        if len(letters) > 0:
            for i in letters:
                letters[i].clear()
                letters[i].sety(letters[i].ycor() - speed)
                letters[i].write(i, align="center", font=("Tahoma", 25, "bold"))
                if letters[i].ycor() < -300:
                    lives = lives - 1
                    lp.clear()
                    lp.write(f"Lives : ", font=("Arial", 20, "bold"))
                    letters[i].clear()
                    letters.pop(i)
                    if lives == 2:
                        lp3.hideturtle()
                    elif lives == 1:
                        lp2.hideturtle()
                    elif lives == 0:
                        lp1.hideturtle()
                    break

        screen.update()
        lv.clear()
        lv.write(f"Level : {speed-1}", font=("Arial", 20, "bold"))

        if lives == 0:
            game_running = False
            game_over.penup()
            game_over.goto(-250, 0)
            game_over.hideturtle()
            game_over.color("pink")
            game_over.write("Game Over! Press ESC to play again", font=("Arial", 20, "bold"))
            hs.clear()
            name = t.textinput("Highest Score", "Enter your name:")
            if game_mode == 1:
                if score > high_easy_score:
                    high_easy_score = score
                    high_easy_name = name
                    high_easy = str(high_easy_score) + " (" + high_easy_name + ")"
            elif game_mode == 2:
                if score > high_int_score:
                    high_int_score = score
                    high_int_name = name
                    high_int = str(high_int_score) + " (" + high_int_name + ")"
            elif game_mode == 3:
                if score > high_dif_score:
                    high_dif_score = score
                    high_dif_name = name
                    high_dif = str(high_dif_score) + " (" + high_dif_name + ")"
            elif game_mode == 4:
                if score > high_exp_score:
                    high_exp_score = score
                    high_exp_name = name
                    high_exp = str(high_exp_score) + " (" + high_exp_name + ")"

            with open("score.txt", "w") as file:
                file.write(f"{high_easy_score}\n{high_easy_name}")
                file.write(f"\n{high_int_score}\n{high_int_name}")
                file.write(f"\n{high_dif_score}\n{high_dif_name}")
                file.write(f"\n{high_exp_score}\n{high_exp_name}")

            screen.listen()

        time.sleep(0.03)

screen.listen()
screen.onkeypress(lambda: press_letter("a"), "a")
screen.onkeypress(lambda: press_letter("b"), "b")
screen.onkeypress(lambda: press_letter("c"), "c")
screen.onkeypress(lambda: press_letter("d"), "d")
screen.onkeypress(lambda: press_letter("e"), "e")
screen.onkeypress(lambda: press_letter("f"), "f")
screen.onkeypress(lambda: press_letter("g"), "g")
screen.onkeypress(lambda: press_letter("h"), "h")
screen.onkeypress(lambda: press_letter("i"), "i")
screen.onkeypress(lambda: press_letter("j"), "j")
screen.onkeypress(lambda: press_letter("k"), "k")
screen.onkeypress(lambda: press_letter("l"), "l")
screen.onkeypress(lambda: press_letter("m"), "m")
screen.onkeypress(lambda: press_letter("n"), "n")
screen.onkeypress(lambda: press_letter("o"), "o")
screen.onkeypress(lambda: press_letter("p"), "p")
screen.onkeypress(lambda: press_letter("q"), "q")
screen.onkeypress(lambda: press_letter("r"), "r")
screen.onkeypress(lambda: press_letter("s"), "s")
screen.onkeypress(lambda: press_letter("t"), "t")
screen.onkeypress(lambda: press_letter("u"), "u")
screen.onkeypress(lambda: press_letter("v"), "v")
screen.onkeypress(lambda: press_letter("w"), "w")
screen.onkeypress(lambda: press_letter("x"), "x")
screen.onkeypress(lambda: press_letter("y"), "y")
screen.onkeypress(lambda: press_letter("z"), "z")
screen.onkeypress(lambda: press_letter("A"), "A")
screen.onkeypress(lambda: press_letter("B"), "B")
screen.onkeypress(lambda: press_letter("C"), "C")
screen.onkeypress(lambda: press_letter("D"), "D")
screen.onkeypress(lambda: press_letter("E"), "E")
screen.onkeypress(lambda: press_letter("F"), "F")
screen.onkeypress(lambda: press_letter("G"), "G")
screen.onkeypress(lambda: press_letter("H"), "H")
screen.onkeypress(lambda: press_letter("I"), "I")
screen.onkeypress(lambda: press_letter("J"), "J")
screen.onkeypress(lambda: press_letter("K"), "K")
screen.onkeypress(lambda: press_letter("L"), "L")
screen.onkeypress(lambda: press_letter("M"), "M")
screen.onkeypress(lambda: press_letter("N"), "N")
screen.onkeypress(lambda: press_letter("O"), "O")
screen.onkeypress(lambda: press_letter("P"), "P")
screen.onkeypress(lambda: press_letter("Q"), "Q")
screen.onkeypress(lambda: press_letter("R"), "R")
screen.onkeypress(lambda: press_letter("S"), "S")
screen.onkeypress(lambda: press_letter("T"), "T")
screen.onkeypress(lambda: press_letter("U"), "U")
screen.onkeypress(lambda: press_letter("V"), "V")
screen.onkeypress(lambda: press_letter("W"), "W")
screen.onkeypress(lambda: press_letter("X"), "X")
screen.onkeypress(lambda: press_letter("Y"), "Y")
screen.onkeypress(lambda: press_letter("Z"), "Z")
screen.onkeypress(lambda: press_letter("1"), "1")
screen.onkeypress(lambda: press_letter("2"), "2")
screen.onkeypress(lambda: press_letter("3"), "3")
screen.onkeypress(lambda: press_letter("4"), "4")
screen.onkeypress(lambda: press_letter("5"), "5")
screen.onkeypress(lambda: press_letter("6"), "6")
screen.onkeypress(lambda: press_letter("7"), "7")
screen.onkeypress(lambda: press_letter("8"), "8")
screen.onkeypress(lambda: press_letter("9"), "9")
screen.onkeypress(lambda: press_letter("0"), "0")
#screen.onkeypress(lambda: press_letter("!"), "!")
#screen.onkeypress(lambda: press_letter("@"), "@")
#screen.onkeypress(lambda: press_letter("#"), "#")
#screen.onkeypress(lambda: press_letter("$"), "$")
#screen.onkeypress(lambda: press_letter("%"), "%")
#screen.onkeypress(lambda: press_letter("^"), "^")
#screen.onkeypress(lambda: press_letter("&"), "&")

play_game()

def play_again():
    global game_mode, game_running
    game_running = False
    lp.clear()
    lv.clear()
    sp.clear()
    game_over.clear()
    for i in letters:
        letters[i].clear()
    letters.clear()
    game_mode = 0
    lp1.hideturtle()
    lp2.hideturtle()
    lp3.hideturtle()

    pen.shape("turtle")
    pen.color("white")
    pen.goto(-200, 200)
    pen.color("white")
    pen.goto(-200, 200)
    pen.write("Typing Game", font=("Arial", 20, "bold"))
    pen.goto(330, -280)
    pen.write("G8 Joshua", font=("Arial", 15, "bold"))
    pen.goto(-200, 100)
    pen.write("Easy (a)", font=("Arial", 15, "normal"))
    pen.goto(-200, 60)
    pen.write("Intermediate (a, 1)", font=("Arial", 15, "normal"))
    pen.goto(-200, 20)
    pen.write("Difficult (a, 1, A)", font=("Arial", 15, "normal"))
    pen.goto(-200, -20)
    pen.write("Expert (a, 1, A, #)", font=("Arial", 15, "normal"))
    pen.goto(-400, -150)
    pen.write("Highest Scores ", font=("Arial", 15, "bold"))
    pen.goto(-400, -200)
    pen.color("chartreuse")
    pen.write("Easy: " + high_easy, font=("Arial", 15, "normal"))
    pen.goto(-400, -230)
    pen.color("yellow")
    pen.write("Intermediate: " + high_int, font=("Arial", 15, "normal"))
    pen.goto(-400, -260)
    pen.color("orange")
    pen.write("Difficult: " + high_dif, font=("Arial", 15, "normal"))
    pen.goto(-400, -290)
    pen.color("DeepPink")
    pen.write("Expert: " + high_exp, font=("Arial", 15, "normal"))
    pen.color("white")
    pen.goto(-230, 112)
    pen.showturtle()

    while True:
        screen.update()
        if game_mode != 0:
            break

    pen.clear()
    pen.hideturtle()

    choose_letters()
    game_running = True

    sp.goto(-450, 240)
    sp.hideturtle()
    sp.color("white")
    sp.write("Score : 0", font=("Arial", 20, "bold"))

    # Highest score
    hs.penup()
    hs.goto(100, 250)
    hs.hideturtle()
    hs.color("lightblue")
    hs.write("Highest Score : " + current_highest, font=("Arial", 20, "bold"))

    play_game()

screen.listen()
screen.onkeypress(play_again, "Escape")
screen.mainloop()
