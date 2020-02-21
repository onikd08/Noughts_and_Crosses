
# A program that simulates a GUI which enables Noughts and Crosses game

"""
Project Name: Noughts and Crosses Game.

 Rules of the Game:

 1. Noughts and Crosses is a game for two players, X and O, who take turns
    marking the spaces in a 3×3 grid.
 2. Player 1's mark is Cross (X) and Player 2's mark is Noughts (O)
 3. The player who succeeds in placing three of their marks in a horizontal,
    vertical, or diagonal row wins the game.
 4. If both of the player fails to fulfill the wining condition, then it is
    considered as a draw.

 How the Game Works:

 1. When the program is run, a 'Welcome' window will open where player has to
    write their names. 
 2. The "Welcome" window will also contain a start button which will start the
    game and a quit button which will terminate the program when they are
    pressed. The start button will not start the game until both the player
    names are entered. The program will give an error message if Player names
    are not entered or they contain only whitespaces.
 3. Players name can not be same. In that case the program will give an error
    message and the game wont get started until the users enter their names and
    the names are different.
 4. If the players enter their names and press the start button,a "Game Window"
    will open which will contain 3x3 grid = 9 buttons with empty texts where
    players will place their marks. Player 1 will make the first move. Players
    can place marks until one of the player wins or the match is a draw.
 5. If a player wins, "Congratulations" message box will pop up which will
    contain the winner's name and the "Game Window" buttons will be disabled. 
    The "Game Result" frame will be opened where the game result is shown. 
    In case of "Draw", this frame will be opened directly without pop up the 
    "Congratulations" message box.
 6. The "Game Result" frame will contain 3 buttons:
        a. "Play Again" button will allow players to start the game again by
        opening the "Game Window". Previous game result will be stored.
        b. Scoreboard button will open "Score Board" frame which will show the
        current score. It contains 2 buttons, "Play Again" and "Quit Game".
        c. "Quit" button will terminate the program.

"""

from tkinter import *
from tkinter import messagebox

PLAYER1_MOVE = "X"  # Default mark placed by Player 1
PLAYER2_MOVE = "O"  # Default mark place by Player 2
HEIGHT = 4          # Height of the buttons where the mark will be placed
WIDTH = 8           # Width of the buttons where the mark will be placed
ROW = 3
COLUMN = 3

turn = 0            # Player's turn, odd number for Player 1 and even number
                    # for Player 2

MAXIMUM_TURN = 9


class Gui:
    """
       The Gui class that simulates 2 Player 3x3 Noughts and Cross Game
    """
    def __init__(self):
        """
        initializes a Tk window(self.__window), player names(self.__player1 and
        self.__player2), winner's name(self.__winner), and game result
        (self.__player1_score,self.__player2_score and self.__draw). 
        :param None
        :return None
        """
        self.__window = Tk()
        self.__window.title("Noughts and Crosses")
        # self.__window.geometry("450x350")
        self.__player1 = StringVar()
        self.__player2 = StringVar()
        self.__winner = StringVar()
        self.__player1_score = 0
        self.__player2_score = 0
        self.__draw = 0
        self.create_widgets()

    def create_widgets(self):
        """
        Creates all the widgets.

        :return: Nonne
        """
        self.__main_frame = Frame()             # main frame window
        self.__main_frame.pack(padx=10, pady=10)

        Label(self.__main_frame, text="Welcome!", font=50).pack()

        frame1 = Frame(self.__main_frame)
        frame1.pack()

        Label(frame1, text="Player 1(X):").grid(padx=5, pady=5)
        # Taking the name of Player 1 who's mark will be "X" by default
        Entry(frame1, textvariable=self.__player1).grid(row=0, column=1,
                                                        padx=5, pady=5)

        Label(frame1, text="Player 2(O):").grid(padx=5, pady=5)
        # Taking the name of Player 2 who's mark will be "O" by default

        Entry(frame1, textvariable=self.__player2).grid(row=1, column=1,
                                                        padx=5, pady=5)

        self.__result_frame = Frame()       # result frame window
        self.__score_frame = Frame()        # scoreboard frame window

        start_button = Button(self.__main_frame, text="Start Game",
                              command=self.start_game).pack()
        quit_button = Button(self.__main_frame, text="Quit",
                             command=self.quit_game).pack()

    def start_game(self):
        """
        Starts a New Game when Start Game or Play Again button is pressed.
        This method handles two errors which includes checking name the players
        are entered or not and players names are different or not. Each of the
        error cases, it gives the error message in the messagebox of the Tk
        window. If no error found, it will go to the game window where the
        buttons (3x3 grid = 9) are created and initially the will have an empty 
        string ("") as a mark (Button text). It will also store the buttons into
        a 2D list (self.__button_list)
        :return: None
        """

        self.__result_frame.destroy()
        self.__score_frame.destroy()

        player1 = self.__player1.get()      # Storing the name of Player 1
        player2 = self.__player2.get()      # Storing the name of Player 2
        player1 = ''.join(player1.split())
        player2 = ''.join(player2.split())

        # List that will store the location of all marks placed by Player 1
        self.__player1_places = []

        # List that will store the location of all marks placed by Player 2
        self.__player2_places = []

        # List for storing the buttons
        self.__button_list = []

        if player1 != "" and player2 != "" and player1 != player2:

            self.__new_window = Tk()       # This is the game window
            self.__new_window.title("Game Window")
            self.__flag = 0  # this value will be used for checking the winner.
                             # The value will be changed to 1 if one player
                             # manages to win, otherwise it will be 0

            # Creating 3x3 grid of buttons
            for r in range(ROW):
                row_buttons = []
                for c in range(COLUMN):

                    def change_button_text(button, r, c):
                        """
                        This is a lambda function which will check the event of
                        clicking a button and changes the text of the
                        button if a Player can place move. If a mark is placed
                        then it checks for the winner or a tie.

                        :param button: button who's mark will be placed.
                                        Initially, it's mark is an empty string
                                        ("").
                        :param r: int, row number
                        :param c: int, column number
                        :return: None
                        """
                        global turn

                        if button["text"] == "" and turn % 2 == 0:
                            button["text"] = PLAYER1_MOVE
                            self.__player1_places.append(str(r)+str(c))
                            turn += 1
                            self.__flag = check_if_win(self.__player1_places)

                            if self.__flag:
                                turn = 0
                                self.__player1_score += 1
                                we_have_a_winner(player1)

                        elif button["text"] == "" and turn % 2 != 0:
                            button["text"] = PLAYER2_MOVE
                            self.__player2_places.append(str(r) + str(c))
                            turn += 1
                            self.__flag = check_if_win(self.__player2_places)

                            if self.__flag:
                                turn = 0
                                self.__player2_score += 1
                                we_have_a_winner(player2)

                        if turn == MAXIMUM_TURN and not self.__flag:
                            self.__winner.set("Match Drawn!")
                            self.__draw += 1
                            turn = 0
                            show_result()

                    def we_have_a_winner(player_name):
                        """
                        Shows the winner
                        :param player_name: str, Name of the winner
                        :return: None
                        """
                        self.__winner.set(player_name +
                                          " Wins!")
                        disable_buttons()
                        messagebox.showinfo("Congratulations!",
                                            player_name)
                        show_result()

                    def disable_buttons():
                        """
                        This will disable all the buttons in the Game Window.
                        :return: None 
                        """
                        for i in range(len(self.__button_list)):
                            for j in range(len(self.__button_list[r])):
                                self.__button_list[i][j].config(state=DISABLED,bg="white")

                    def show_result():
                        """
                        This function will be called for showing result
                        (Win/Draw).
                        It will destroy previous two windows(Welcome window and
                        game window) and create a new window where the winner's
                        name will be displayed. It will also provide the
                        functionality to start the game again ('Play again'
                        button), go to the score board where both of the
                        player's scores are shown ('Score Board' button) and
                        quiting the game ('Quit' button).
                        :return: None
                        """
                        self.__main_frame.forget()
                        self.__result_frame = Frame()

                        self.__result_frame.pack(padx=100, pady=50)

                        Label(self.__result_frame, text="Game Result",
                              font=50).pack()

                        frame1 = Frame(self.__result_frame)
                        frame1.pack()

                        Label(frame1,textvariable=self.__winner,font=50)\
                            .grid(padx=5, pady=5)

                        # Play again button
                        Button(self.__result_frame,text="Play Again",
                               command=self.start_game).pack()
                        self.__new_window.destroy()
                        # Score board button
                        Button(self.__result_frame,text="Score Board",
                               command= self.show_score_board).pack()
                        # Quit Button
                        Button(self.__result_frame, text="Quit",
                               command=self.quit_game).pack()

                    def check_if_win(place):
                        """
                        Checks if there is a winner or match is drawn. It
                        returns 0 if the match is drawn, else it returns 1
                        :param place: list, that have the locations of marks
                                      placed by a Player
                        :return: 1: if player wins
                                 0: if match is drawn
                        """

                        if '00' in place and '10' in place and '20' in place:
                            return True
                        if '01' in place and '11' in place and '21' in place:
                            return True
                        if '02' in place and '12' in place and '22' in place:
                            return True
                        if '00' in place and '01' in place and '02' in place:
                            return True
                        if '10' in place and '11' in place and '12' in place:
                            return True
                        if '20' in place and '21' in place and '22' in place:
                            return True
                        if '00' in place and '11' in place and '22' in place:
                            return True
                        if '02' in place and '11' in place and '20' in place:
                            return True
                        else:
                            return False

                    button = Button(self.__new_window,
                                    text="", font='Times 20 bold', bg='gray',
                                    fg='white', height=HEIGHT, width=WIDTH)
                    button.configure(command=lambda but=button,row=r,col=c:
                                     change_button_text(but,row,col))

                    row_buttons.append(button)
                    button.grid(row=r, column=c, sticky=S + N + E + W)

                # Storing the buttons into a 2D list
                self.__button_list.append(row_buttons)

            self.__new_window.mainloop()

        elif player1 == "" or player2 == "":
            messagebox.showinfo("ERROR", "Enter player names")

        elif player1 == player2:
            messagebox.showinfo("ERROR","Player names are same")

    def start(self):
        """
        Starts a game.
        :return: None
        """
        self.__window.mainloop()

    def quit_game(self):
        """
        Quits the game when Quit button is pressed
        :return: None
        """
        self.__window.destroy()

    def show_score_board(self):
        """
        Show the updated score boards.
        :return: None
        """
        self.__result_frame.destroy()
        self.__score_frame = Frame()

        player1_info = self.__player1.get() + "'s Score: " + \
                        str(self.__player1_score)

        player2_info = self.__player2.get() + "'s Score: " + \
                        str(self.__player2_score)

        draw_info = "Draw: " + str(self.__draw)

        self.__score_frame.pack(padx=100, pady=50)

        Label(self.__score_frame, text="Score Board",
              font=50).pack()

        frame1 = Frame(self.__score_frame)
        frame1.pack()

        Label(frame1, text=player1_info, font=50).grid(padx=5, pady=5)
        Label(frame1, text=player2_info, font=50).grid(padx=5,pady=5)
        Label(frame1, text=draw_info, font=50).grid(padx=5, pady=5)

        Button(self.__score_frame, text="Play Again",
               command=self.start_game).pack()

        Button(self.__score_frame, text="Quit Game",
               command=self.quit_game).pack()


def main():
    """
    Creates an object of class Gui and starts game by calling start() method
    :return: None
    """
    ui = Gui()
    ui.start()  # starting a new game


main()
