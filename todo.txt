from tkinter import *
from tkinter import ttk

class todo:
    def __init__(self, root):
        self.root = root
        self.root.title('To-do-List')
        self.root.geometry('650x410+300+150')

        self.label = Label(self.root, text='To-do-List', font=('ariel', 25, 'bold'), width=10, bd=5, bg='light blue', fg='Black')
        self.label.pack(side='top', fill=BOTH)

        self.label2 = Label(self.root, text='Add Task', font=('ariel', 18, 'bold'), width=10, bd=5, bg='light blue', fg='Black')
        self.label2.place(x=40, y=54)

        self.label3 = Label(self.root, text='Tasks', font=('ariel', 20, 'bold'), width=10, bd=5, bg='light blue', fg='Black')
        self.label3.place(x=320, y=54)

        self.main_text = Listbox(self.root, height=9, bd=5, width=23, font=('arial', 20, 'italic bold'))
        self.main_text.place(x=280, y=100)

        self.text = Text(self.root, height=2, bd=5, width=30, font=('ariel', 10, 'bold'))
        self.text.place(x=20, y=120)

        # Read data from file and populate Listbox
        with open('data.txt') as file:
            read = file.readlines()
            for i in read:
                ready = i.split()
                self.main_text.insert(END, ready)
            file.close()

        # Add Task Button
        self.button = Button(self.root, text="Add", font=('sarif', 20, 'italic bold'), width=10, bd=5, bg="sky blue", fg='black', command=self.add)
        self.button.place(x=30, y=200)

        # Delete Button
        self.button1 = Button(self.root, text="Delete", font=('sarif', 20, 'italic bold'), width=10, bd=5, bg="sky blue", fg='black', command=self.delete)
        self.button1.place(x=30, y=300)

    # Add Task Method
    def add(self):
        content = self.text.get(1.0, END)
        self.main_text.insert(END, content)
        with open('data.txt', 'a') as file:
            file.write(content)
        self.text.delete(1.0, END)

    # Delete Task Method
    def delete(self):
        delete_ = self.main_text.curselection()
        if delete_:
            look = self.main_text.get(delete_)
            with open('data.txt', 'r+') as fr:
                new_f = fr.readlines()
                fr.seek(0)
                for line in new_f:
                    item = str(look)
                    if item not in line:
                        fr.write(line)
                fr.truncate()
            self.main_text.delete(delete_)

def main():
    root = Tk()
    u1 = todo(root)
    root.mainloop()

if __name__ == "__main__":
    main()
