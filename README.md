import tkinter as tk
from tkinter import filedialog, messagebox

def open_file():
    file_path = filedialog.askopenfilename(
        filetypes=[("Text Files", "*.txt"), ("All Files", "*.*")]
    )
    if file_path:
        try:
            with open(file_path, "r") as file:
                content = file.read()
                text_widget.delete("1.0", tk.END) 
                text_widget.insert("1.0", content)  
        except Exception as e:
            messagebox.showerror("Error", f"Unable to open file: {e}")

def save_file():
   
    file_path = filedialog.asksaveasfilename(
        defaultextension=".txt",
        filetypes=[("Text Files", "*.txt"), ("All Files", "*.*")]
    )
    if file_path:
        try:
            with open(file_path, "w") as file:
                content = text_widget.get("1.0", tk.END)
                file.write(content.strip()) 
        except Exception as e:
            messagebox.showerror("Error", f"Unable to save file: {e}")

def exit_app():
    root.destroy()

root = tk.Tk()
root.title("Simple Notepad")
root.geometry("800x600") 

text_widget = tk.Text(root, wrap="word", font=("Arial", 12))
text_widget.pack(expand=True, fill="both")

menu_bar = tk.Menu(root)

file_menu = tk.Menu(menu_bar, tearoff=0)
file_menu.add_command(label="Open", command=open_file)
file_menu.add_command(label="Save", command=save_file)
file_menu.add_separator()
file_menu.add_command(label="Exit", command=exit_app)
menu_bar.add_cascade(label="File", menu=file_menu)

root.config(menu=menu_bar)

root.mainloop()
