# python
Project Cal Boxes
``` PYTHON
import tkinter as tk

# Create a main
root = tk.Tk()

# Set the main title
root.title("Box Calculator")
#getting screen width and height of display
display_width = root.winfo_screenwidth()
display_height = root.winfo_screenheight()
#setting tkinter window size
root.geometry("%dx%d" % (display_width, display_height))

def calculate_boxes():
    try:
        box_width = float(box_width_entry.get())
        box_length = float(box_length_entry.get())
        box_height = float(box_height_entry.get())
        
        total_boxes = 0
        
        for item in items:
            item_width = float(item[0])
            item_length = float(item[1])
            item_height = float(item[2])
            item_quantity = int(item[3])

            # Calculate the number of boxes needed for each dimension
            width_boxes = int(item_width / box_width) + (1 if item_width % box_width != 0 else 0)
            length_boxes = int(item_length / box_length) + (1 if item_length % box_length != 0 else 0)
            height_boxes = int(item_height / box_height) + (1 if item_height % box_height != 0 else 0)

            total_boxes += width_boxes * length_boxes * height_boxes * item_quantity

        result_label.config(text=f"The total number of boxes needed is {total_boxes}")
    except ValueError:
        result_label.config(text="Please enter valid numbers")

def add_item():
    try:
        width = float(width_entry.get())
        length = float(length_entry.get())
        height = float(height_entry.get())
        quantity = int(quantity_entry.get())

        items.append([width, length, height, quantity])

        item_listbox.insert(tk.END, f"{width} x {length} x {height}, {quantity}")
    except ValueError:
        result_label.config(text="Please enter valid numbers")

def delete_item():
    selected_item_index = item_listbox.curselection()
    if selected_item_index:
        items.pop(selected_item_index[0])
        item_listbox.delete(selected_item_index)

def update_item():
    try:
        selected_item_index = item_listbox.curselection()
        item = items[selected_item_index[0]]

        width = float(width_entry.get())
        length = float(length_entry.get())
        height = float(height_entry.get())
        quantity = int(quantity_entry.get())

        item[0] = width
        item[1] = length
        item[2] = height
        item[3] = quantity

        item_listbox.delete(selected_item_index)
        item_listbox.insert(selected_item_index, f"{width} x {length} x {height}, {quantity}")
    except (IndexError, ValueError):
        result_label.config(text="Please select an item and enter valid numbers")

items = []

# Item size labels and entries
item_label = tk.Label(root, text="Item size:")
item_label.grid(row=0, column=0)

width_label = tk.Label(root, text="Width:")
width_label.grid(row=1, column=0)

width_entry = tk.Entry(root)
width_entry.grid(row=1, column=1)

length_label = tk.Label(root, text="Length:")
length_label.grid(row=2, column=0)

length_entry = tk.Entry(root)
length_entry.grid(row=2, column=1)

height_label = tk.Label(root, text="Height:")
height_label.grid(row=3, column=0)

height_entry = tk.Entry(root)
height_entry.grid(row=3, column=1)

quantity_label = tk.Label(root, text="Quantity:")
quantity_label.grid(row=4, column=0)

quantity_entry = tk.Entry(root)
quantity_entry.grid(row=4, column=1)

add_button = tk.Button(root, text="Add Item", command=add_item)
add_button.grid(row=5, column=0)

# Item list
item_list_label = tk.Label(root, text="Item list")
# Item listbox and scrollbars

item_listbox_frame = tk.Frame(root)
item_listbox_frame.grid(row=6, column=0, columnspan=2)

item_listbox = tk.Listbox(item_listbox_frame, width=50, height=10)
item_listbox.pack(side=tk.LEFT, fill=tk.BOTH)

item_listbox_scrollbar_y = tk.Scrollbar(item_listbox_frame, orient=tk.VERTICAL)
item_listbox_scrollbar_y.pack(side=tk.RIGHT, fill=tk.Y)

item_listbox_scrollbar_x = tk.Scrollbar(root, orient=tk.HORIZONTAL)
item_listbox_scrollbar_x.grid(row=7, column=0, columnspan=2, sticky="EW")

item_listbox.config(yscrollcommand=item_listbox_scrollbar_y.set, xscrollcommand=item_listbox_scrollbar_x.set)
item_listbox_scrollbar_y.config(command=item_listbox.yview)
item_listbox_scrollbar_x.config(command=item_listbox.xview)

# Item action buttons
delete_button = tk.Button(root, text="Delete Item", command=delete_item)
delete_button.grid(row=8, column=0)

update_button = tk.Button(root, text="Update Item", command=update_item)
update_button.grid(row=8, column=1)

# Box size labels and entries
box_label = tk.Label(root, text="Box size:")
box_label.grid(row=0, column=2)

box_width_label = tk.Label(root, text="Width:")
box_width_label.grid(row=1, column=2)

box_width_entry = tk.Entry(root)
box_width_entry.grid(row=1, column=3)

box_length_label = tk.Label(root, text="Length:")
box_length_label.grid(row=2, column=2)

box_length_entry = tk.Entry(root)
box_length_entry.grid(row=2, column=3)

box_height_label = tk.Label(root, text="Height:")
box_height_label.grid(row=3, column=2)

box_height_entry = tk.Entry(root)
box_height_entry.grid(row=3, column=3)

calculate_button = tk.Button(root, text="Calculate", command=calculate_boxes)
calculate_button.grid(row=4, column=2)

# Result label
result_label = tk.Label(root)
result_label.grid(row=4, column=3)

# Run the main
root.mainloop()

```
