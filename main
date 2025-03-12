import time

class MenuItem:
    def __init__(self, item_id, name, price):
        self.item_id = item_id
        self.name = name
        self.price = price

class Menu:
    def __init__(self):
        self.tiffins = [
            MenuItem(1, "Idly", 20), MenuItem(2, "Dosa", 30), MenuItem(3, "Puri", 30),
            MenuItem(4, "Vada", 25), MenuItem(5, "Bonda", 20), MenuItem(6, "Chapathi", 40)
        ]
        self.meals = [
            MenuItem(7, "Chicken Biryani (Mini)", 180), MenuItem(8, "Chicken Biryani (Large)", 250),
            MenuItem(9, "Mutton Biryani (Mini)", 300), MenuItem(10, "Mutton Biryani (Large)", 350),
            MenuItem(11, "Veg Biryani (Mini)", 150), MenuItem(12, "Veg Biryani (Large)", 200),
            MenuItem(13, "Veg Meals", 120)
        ]
        self.beverages = [
            MenuItem(14, "Tea", 10), MenuItem(15, "Green Tea", 30), MenuItem(16, "Ginger Tea", 20),
            MenuItem(17, "Thumsup (250 ml)", 30), MenuItem(18, "Sting (250 ml)", 30),
            MenuItem(19, "Coke (250 ml)", 30), MenuItem(20, "Sprite (250 ml)", 30)
        ]

    def display_menu(self):
        print("\n*Menu*")
        print("\n*Tiffins*")
        for item in self.tiffins:
            print(f"{item.item_id} {item.name} --> Rs.{item.price}")
        print("\n*Meals*")
        for item in self.meals:
            print(f"{item.item_id} {item.name} --> Rs.{item.price}")
        print("\n*Beverages*")
        for item in self.beverages:
            print(f"{item.item_id} {item.name} --> Rs.{item.price}")

    def get_item(self, choice):
        for category in [self.tiffins, self.meals, self.beverages]:
            for item in category:
                if item.item_id == choice:
                    return item
        raise ValueError("Item not found in menu. Please select a valid item.")

class Order(Menu):
    def __init__(self):
        super().__init__()
        self.ordered_items = []
        self.total_amount = 0
        self.completed = False

    def add_item(self, item, quantity):
        for ordered_item in self.ordered_items:
            if ordered_item[0].item_id == item.item_id:
                ordered_item[1] += quantity
                self.total_amount += item.price * quantity
                return
        self.ordered_items.append([item, quantity])
        self.total_amount += item.price * quantity

    def cancel_item(self, item_id):
        for item in self.ordered_items:
            if item[0].item_id == item_id:
                self.total_amount -= item[0].price * item[1]
                print(f"{item[0].name} has been cancelled.")
                self.ordered_items.remove(item)
                self.display_order()
                return
        print("Item not found in your order.")

    def display_order(self):
        print("\nOrder Details:")
        for item in self.ordered_items:
            print(f"{item[0].name} x {item[1]} - Rs.{item[0].price * item[1]}")
        print(f"Total Amount: Rs.{self.total_amount}")
        print(f"Status: {'Completed' if self.completed else 'Pending'}")

    def process_payment(self):
        print("Please pay the payment using any UPI methods.")
        print("Redirecting to payment....")
        time.sleep(5)
        print("Payment Successful")
        self.completed = True

class User:
    def __init__(self):
        self.name = ""
        self.phone_number = ""
        self.address = ""
        self.order = Order()

    def register_user(self):
        self.name = input("Enter your name: ")
        while True:
            self.phone_number = input("Enter your phone number: ")
            if len(self.phone_number) == 10 and self.phone_number.isdigit() and self.phone_number[0] in "6789":
                break
            print("Please enter a valid phone number (10 digits, starting with 6, 7, 8, or 9).")
        self.address = input("Enter your address: ")
        print("User registered successfully.")

    def view_user_details(self):
        print("\nUser Details:")
        print(f"Name: {self.name}")
        print(f"Phone Number: {self.phone_number}")
        print(f"Address: {self.address}")

    def show_menu(self):
        while True:
            print("\n1. Display menu\n2. Place Order\n3. Cancel items in Order\n4. Complete Order\n5. Exit user")
            choice = input("Enter your choice: ")
            if choice == '1':
                self.order.display_menu()
            elif choice == '2':
                self.order.display_menu()
                while True:
                    try:
                        item_id = int(input("Enter the item number to order: "))
                        quantity = int(input("Enter quantity: "))
                        item = self.order.get_item(item_id)
                        self.order.add_item(item, quantity)
                        if input("Would you like to order another item? (y/n): ").lower() != 'y':
                            break
                    except ValueError as e:
                        print(e)
                self.order.display_order()
            elif choice == '3':
                item_id = int(input("Enter item id to cancel: "))
                self.order.cancel_item(item_id)
            elif choice == '4':
                self.order.process_payment()
                self.order.display_order()
            elif choice == '5':
                print("Thank you for visiting. Visit again.")
                break
            else:
                print("Invalid choice. Please select from the given options.")

if __name__ == "__main__":
    users = []
    while True:
        print("\n1. Register user\n2. View records\n3. Exit")
        choice = input("Enter your choice: ")
        if choice == '1':
            user = User()
            user.register_user()
            user.show_menu()
            users.append(user)
        elif choice == '2':
            if input("Enter password: ") == "123":
                if users:
                    for user in users:
                        user.view_user_details()
                        user.order.display_order()
                else:
                    print("No Records Found")
            else:
                print("Incorrect Password.")
        elif choice == '3':
            print("Exiting the program...")
            break
        else:
            print("Invalid choice. Please select from the given options.")
