# Gui-Calculstor
import tkinter as tk
from math import sqrt

class CalculatorApp:
    def __init__(self, master):
        self.master = master
        master.title("GUI Based Calculator")
        master.configure(bg='#000000')  # Set background color to black

        self.display = tk.Entry(master, width=25, borderwidth=5, font=('Comic Sans MS', 16), justify='right', bg='#000000', fg='#FFFF00')  # Yellow text on black background
        self.display.grid(row=0, column=0, columnspan=4, padx=10, pady=10)

        # Define button colors
        num_color = '#000000'  # Black
        op_color = '#FFFF00'  # Yellow

        # Define buttons
        buttons = [
            ('7', 1, 0), ('8', 1, 1), ('9', 1, 2), ('/', 1, 3),
            ('4', 2, 0), ('5', 2, 1), ('6', 2, 2), ('*', 2, 3),
            ('1', 3, 0), ('2', 3, 1), ('3', 3, 2), ('-', 3, 3),
            ('0', 4, 0), ('.', 4, 1), ('=', 4, 2), ('+', 4, 3),
            ('x^2', 5, 0), ('x^3', 5, 1), ('%', 5, 2), ('sqrt', 5, 3)
        ]

        # Create buttons
        for (text, row, col) in buttons:
            if text in ['/', '*', '-', '+']:
                btn = tk.Button(master, text=text, command=lambda t=text: self.on_button_click(t), bg=op_color, fg='#000000', font=('Comic Sans MS', 15), width=4, height=2)
            elif text == '=':
                btn = tk.Button(master, text=text, command=lambda t=text: self.on_button_click(t), bg='#000000', fg='#FFFF00', font=('Comic Sans MS', 15), width=4, height=2)
            elif text == 'sqrt':
                btn = tk.Button(master, text=text, command=lambda t=text: self.on_button_click(t), bg='#FFFF00', fg='#000000', font=('Comic Sans MS', 15), width=4, height=2)
            else:
                btn = tk.Button(master, text=text, command=lambda t=text: self.on_button_click(t), bg=num_color, fg='#FFFFFF', font=('Comic Sans MS', 15), width=4, height=2)
            btn.grid(row=row, column=col, sticky='nsew')

        # Configure row and column weights
        for i in range(6):
            master.grid_rowconfigure(i, weight=1)
        for i in range(4):
            master.grid_columnconfigure(i, weight=1)

    def on_button_click(self, text):
        current_text = self.display.get()

        if text == '=':
            try:
                result = eval(current_text)
                self.display.delete(0, tk.END)
                self.display.insert(tk.END, str(result))
            except Exception:
                self.display.delete(0, tk.END)
                self.display.insert(tk.END, "Error")

        elif text == 'x^2':
            try:
                result = eval(current_text) ** 2
                self.display.delete(0, tk.END)
                self.display.insert(tk.END, str(result))
            except Exception:
                self.display.delete(0, tk.END)
                self.display.insert(tk.END, "Error")

        elif text == 'x^3':
            try:
                result = eval(current_text) ** 3
                self.display.delete(0, tk.END)
                self.display.insert(tk.END, str(result))
            except Exception:
                self.display.delete(0, tk.END)
                self.display.insert(tk.END, "Error")

        elif text == '%':
            try:
                result = eval(current_text) / 100
                self.display.delete(0, tk.END)
                self.display.insert(tk.END, str(result))
            except Exception:
                self.display.delete(0, tk.END)
                self.display.insert(tk.END, "Error")

        elif text == 'sqrt':
            try:
                result = sqrt(eval(current_text))
                self.display.delete(0, tk.END)
                self.display.insert(tk.END, str(result))
            except Exception:
                self.display.delete(0, tk.END)
                self.display.insert(tk.END, "Error")

        else:
            self.display.insert(tk.END, text)

def main():
    root = tk.Tk()
    app = CalculatorApp(root)
    root.mainloop()

if __name__ == "__main__":
    main()
