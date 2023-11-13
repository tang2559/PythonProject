class Menu:
    def __init__(self):
        self.menu_items = {
            "1": {"name": "Chicken Burger", "price": 45},
            "2": {"name": "Pizza", "price": 50},
            "3": {"name": "Salad", "price": 47},
            "4": {"name": "Pasta", "price": 60},
            "5": {"name": "Soda", "price": 8},
            "6": {"name": "mineral water", "price": 15},
            "7": {"name": "Iced Coffee", "price": 45},
            "8": {"name": "Coca-Cola", "price": 15},
            "9": {"name": "Pepsi", "price": 15},
            "10": {"name": "Sprite", "price": 15},
            "11": {"name": "Orange Juice", "price": 27},
            "12": {"name": "Grape Juice", "price": 27},
            "13": {"name": "Coconut Water", "price": 20},
            "14": {"name": "Original Cold Brew coffee", "price": 35},
            "15": {"name": "Chocolate Milk", "price": 25},
            "16": {"name": "Latte", "price": 40},
        }

    def display_menu(self):
        print("Menu:")
        for key, item in self.menu_items.items():
            print(f"{key}. {item['name']}: ${item['price']}")

    def order_menu_items(self):
        order = []
        while True:
            self.display_menu()
            choice = input("Enter the number of the item you want to order (or 'q' to quit): ")

            if choice.lower() == 'q':
                break

            if choice in self.menu_items:
                order.append({"name": self.menu_items[choice]['name'], "price": self.menu_items[choice]['price']})
                print(f"{self.menu_items[choice]['name']} added to your order.")
            else:
                print("Invalid choice. Please enter a valid menu number.")

        return order

    def calculate_total_cost(self, order):
        total_cost = sum(item['price'] for item in order)
        return total_cost

    def receive_money(self):
        while True:
            try:
                received_amount = float(input("Enter the amount of money you are providing: "))
                if received_amount >= 0:
                    return received_amount
                else:
                    print("Please enter a non-negative amount.")
            except ValueError:
                print("Invalid input. Please enter a valid number.")

    def return_change(self, total_cost, received_amount):
        change = received_amount - total_cost
        if change < 0:
            print("Insufficient funds. Please provide enough money.")
            return None
        else:
            return change


def main():
    menu = Menu()
    print("Welcome to the Restaurant!")

    order = menu.order_menu_items()

    if order:
        print("\nYour Order:")
        for item in order:
            print(f"{item['name']}: ${item['price']}")

        total_cost = menu.calculate_total_cost(order)
        print(f"\nTotal Cost: ${total_cost:.2f}")

        received_amount = menu.receive_money()
        change = menu.return_change(total_cost, received_amount)

        if change is not None:
            print(f"Received: ${received_amount:.2f}")
            print(f"Change: ${change:.2f}")

    print("Thank you for dining with us!")

if __name__ == "__main__":
    main()
