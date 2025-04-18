mport tkinter as tk

class CookieClicker:
    def __init__(self, master):
        self.master = master
        master.title("Cookie Clicker")

        self.cookies = 0

        self.label = tk.Label(master, text="Печеньки: 0")
        self.label.pack()

        self.click_button = tk.Button(master, text="Кликни на печеньку!", command=self.click_cookie)
        self.click_button.pack()

        self.auto_click_button = tk.Button(master, text="Купить автокликер (10 печенек)", command=self.buy_auto_clicker)
        self.auto_click_button.pack()

        self.auto_clicking = False

    def click_cookie(self):
        self.cookies += 1
        self.update_label()

    def update_label(self):
        self.label.config(text=f"Печеньки: {self.cookies}")

    def buy_auto_clicker(self):
        if self.cookies >= 10:
            self.cookies -= 10
            self.update_label()
            self.auto_clicking = True
            self.master.after(1000, self.auto_click)

    def auto_click(self):
        if self.auto_clicking:
            self.cookies += 1
            self.update_label()
            self.master.after(1000, self.auto_click)

if __name__ == "__main__":
    root = tk.Tk()
    cookie_clicker = CookieClicker(root)
    root.mainloop()