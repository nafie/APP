# Biliing App
import tkinter as tk
from tkinter import messagebox

# Menu data
menu = {
    "Burger": 50,
    "Pizza": 150,
    "Pasta": 100,
    "Cold Drink": 30
}

# Initialize order dictionary
order = {}

# Add item to order
def add_item(item_name):
    price = menu[item_name]
    quantity = int(quantity_var.get())
    if quantity > 0:
        if item_name in order:
            order[item_name]['quantity'] += quantity
        else:
            order[item_name] = {'price': price, 'quantity': quantity}
        messagebox.showinfo("Success", f"Added {quantity} {item_name}(s) to the order.")
    else:
        messagebox.showerror("Error", "Quantity must be greater than zero.")

# Show bill
def show_bill():
    total = 0
    bill_details = "Your Order:\n\n"
    for item, details in order.items():
        item_total = details['price'] * details['quantity']
        total += item_total
        bill_details += f"{item} x {details['quantity']} = ₹{item_total}\n"
    bill_details += f"\nTotal Bill: ₹{total}"
    messagebox.showinfo("Bill", bill_details)

# Reset order
def reset_order():
    global order
    order = {}
    messagebox.showinfo("Reset", "Order has been reset!")

# Create main window
app = tk.Tk()
app.title("Billing App")
app.geometry("300x400")

# Add menu labels and buttons
tk.Label(app, text="Menu", font=("Arial", 16)).pack(pady=10)
for item, price in menu.items():
    frame = tk.Frame(app)
    frame.pack(pady=5)
    tk.Label(frame, text=f"{item} - ₹{price}", font=("Arial", 12)).pack(side="left", padx=10)
    quantity_var = tk.StringVar(value="0")
    tk.Entry(frame, textvariable=quantity_var, width=5).pack(side="left")
    tk.Button(frame, text="Add", command=lambda i=item: add_item(i)).pack(side="left", padx=5)

# Add action buttons
tk.Button(app, text="Show Bill", command=show_bill, bg="green", fg="white", font=("Arial", 12)).pack(pady=10)
tk.Button(app, text="Reset Order", command=reset_order, bg="red", fg="white", font=("Arial", 12)).pack(pady=5)

# Run the app
app.mainloop()


