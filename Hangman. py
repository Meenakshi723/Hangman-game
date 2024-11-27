import tkinter as tk
from tkinter import messagebox
import random

class HangmanApp:
    def __init__(self, master):  
        self.master = master
        self.master.title("Hangman Game")
        
        self.score = 0
        
        self.word_to_guess = self.choose_word()
        self.guessed_letters = []
        self.attempts = 6
        
        self.word_display = tk.StringVar()
        self.word_display.set(self.display_word())
        
        self.word_label = tk.Label(master, textvariable=self.word_display, font=("Helvetica", 24))
        self.word_label.pack()
        
        self.guess_label = tk.Label(master, text="Enter a letter:", font=("Helvetica", 16))
        self.guess_label.pack()
        
        self.guess_entry = tk.Entry(master, font=("Helvetica", 16))
        self.guess_entry.pack()
        
        self.guess_button = tk.Button(master, text="Guess", command=self.process_guess, font=("Helvetica", 16))
        self.guess_button.pack()
        
        self.update_attempts_label()
        
    def choose_word(self):
        words = ["python", "programming", "zombie", "computer", "squirrel", "excellence", "focus", "zinc"]
        print(words)
        return random.choice(words)

    def display_word(self):
        display = ""
        for letter in self.word_to_guess:
            if letter in self.guessed_letters:
                display += letter + " "
            else:
                display += "_ "
        return display

    def process_guess(self):
        guess = self.guess_entry.get().lower()
        self.guess_entry.delete(0, tk.END)
        
        if guess in self.guessed_letters:
            messagebox.showinfo("Hangman", "You already guessed that letter!")
            return
        elif len(guess) != 1 or not guess.isalpha():
            messagebox.showinfo("Hangman", "Please enter a single letter.")
            return
        
        self.guessed_letters.append(guess)
        
        if guess not in self.word_to_guess:
            self.attempts -= 1
        
        if "_" not in self.display_word():
            self.score += 10
            self.congratulate_player()  
            self.next_word()
        elif self.attempts == 0:
            messagebox.showinfo("Game Over", "Sorry, you ran out of attempts.\nThe word was: " + self.word_to_guess + "\nYour score is: " + str(self.score))
            self.play_again()
        else:
            self.word_display.set(self.display_word())
        
        self.update_attempts_label()

    def next_word(self):
        self.word_to_guess = self.choose_word()
        self.guessed_letters = []
        self.attempts = 6
        self.word_display.set(self.display_word())
        
    def update_attempts_label(self):
        self.guess_label.config(text="Attempts left: " + str(self.attempts))
        
    def play_again(self):
        choice = messagebox.askyesno("Play Again?", "Do you want to play again?")
        if choice:
            self.score = 0
            self.next_word()
        else:
            self.master.destroy()
    
    def congratulate_player(self):
        messagebox.showinfo("Congratulations!", "You guessed the word correctly!")

class WelcomeWindow:
    def __init__(self, master):
        self.master = master
        self.master.title("Hangman")
        
        self.label = tk.Label(master, text="Welcome to Hangman\nAdventure!", font=("Helvetica", 24))
        self.label.pack(pady=20)
        
        self.start_button = tk.Button(master, text="Start Game", command=self.start_game, font=("Helvetica", 16))
        self.start_button.pack(pady=20)
    
    def start_game(self):
        self.master.destroy()
        self.open_main_game()

    def open_main_game(self):
        root = tk.Tk()
        app = HangmanApp(root)
        root.mainloop()

def main():
    root = tk.Tk()
    welcome_app = WelcomeWindow(root)
    root.mainloop()

if __name__ == "__main__":  
    main()
