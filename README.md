# ice-cream
first mini project , ice cream shop where you can order your favourite ice cream

from tkinter import*
from tkinter import messagebox 
import ttkbootstrap as ttk
from ttkbootstrap.constants import *

root=ttk.Window(themename="flatly")
root.geometry('1500x1500')
root.title("Ice cream shop")
root.configure(bg='Light blue')

tops=Frame(root,width=180,height=100,bd=14,relief=RAISED,bg='beige')
tops.pack(side=TOP,fill=X)

lab=Label(tops,text='  ICE CREAM SHOP  ',bg='azure',font=("Arial",30))
lab.pack(side=LEFT)

canvas=Canvas(tops,width=100,bg='pink',height=150)
canvas.pack(anchor=NW,fill=Y)

lab=ttk.Label(root,text='Additional topings')
lab.pack(anchor=NW,padx=10,pady=10)

entry=ttk.Entry(root,width=50,font=("Arial",20))
entry.pack(anchor=NW)

order_list=[]
total_bill=0

order_view=Text(root,width=40,height=10, font=("Arial",10))
order_view.pack(anchor=SE,padx=10,pady=10)

def order():
    global order_placed
    username = entry.get()
    print(username)
    entry.config(state=DISABLED)
    order_placed = True
    selected_item = listbox.curselection()
    if selected_item:
        item = listbox.get(selected_item)
        price = int(item.split('Rs ')[1]) 
        print(f"You ordered: {item}")
        global total_bill
        total_bill += price 
        order_view.insert(END, f"You ordered: {item}\n") 
    else:
        print("Please select an item from the list")
    entry.config(state=NORMAL)
    entry.delete(0, END)
    askagain()

def delete():
    global order_placed
    entry.delete(0, END)
    order_placed = False
    messagebox.showinfo(title="Cancel order?", message="Order cancelled")
    order_view.delete(1.0, END)

def askagain():
    response=messagebox.askyesno(title="Another order?",message="Do you want to make another order?")
    if response:
     entry.config(state=NORMAL) 
    else:
        print("Your total bill is:",total_bill)
    order_view.insert(END, f"Your total bill is: Rs {total_bill}\n") 

label=ttk.Label(root,text='Flavors of ice-cream',font=("Arial",15))
label.pack(anchor=W,padx=10,pady=10)

listbox=Listbox(root,width=30,bg='slategray1',font=("Arial",15))
listbox.insert(0,"1 Chocolate Rs 150")
listbox.insert(1,'2 Vanilla Rs 140')
listbox.insert(2,'3 Blueberry Rs 180')
listbox.insert(3,'4 Strawberry Rs 160')
listbox.insert(4,'5 Mint Rs 150')
listbox.insert(5,'6 Cookies and cream Rs 140')
listbox.pack(anchor=NW)

btn=ttk.Button(root,text='order',bootstyle="success",command=order)
btn.pack(side=RIGHT,padx=10,pady=10)

delbut=ttk.Button(root,text="cancel",bootstyle="danger",command=delete)
delbut.pack(side=RIGHT,padx=10,pady=10)






root.mainloop()





