# restaurant-manage-system
to manage restaurents

# Restaurant Management System

menu = {
    1: {"name": "Burger", "price": 120},
    2: {"name": "Pizza", "price": 250},
    3: {"name": "Sandwich", "price": 100},
    4: {"name": "French Fries", "price": 80},
    5: {"name": "Coffee", "price": 50},
    6: {"name": "Cold Drink", "price": 40}
}

total_sales = 0
order_number = 1


def display_menu():
    print("\n========== RESTAURANT MENU ==========")
    print(f"{'ID':<5}{'Food Item':<20}{'Price (Rs.)':>12}")
    print("-" * 37)

    for item_id, item in menu.items():
        print(
            f"{item_id:<5}{item['name']:<20}"
            f"{item['price']:>12}"
        )


def take_order():
    global total_sales, order_number

    order = []
    grand_total = 0

    customer = input("\nEnter customer name: ").strip()

    if not customer:
        print("Customer name cannot be empty.")
        return

    while True:
        display_menu()
        print("\nEnter 0 to finish ordering.")

        try:
            item_id = int(input("Enter food item ID: "))

            if item_id == 0:
                break

            if item_id not in menu:
                print("Invalid item ID!")
                continue

            quantity = int(input("Enter quantity: "))

            if quantity <= 0:
                print("Quantity must be greater than zero.")
                continue

            item = menu[item_id]
            amount = item["price"] * quantity

            order.append({
                "name": item["name"],
                "price": item["price"],
                "quantity": quantity,
                "amount": amount
            })

            grand_total += amount
            print(f"{item['name']} added to order.")

        except ValueError:
            print("Please enter a valid number.")

    if not order:
        print("No items ordered.")
        return

    total_sales += grand_total

    print("\n========== CUSTOMER RECEIPT ==========")
    print(f"Order Number: {order_number}")
    print(f"Customer: {customer}")
    print("-" * 42)
    print(f"{'Item':<16}{'Qty':>5}{'Price':>9}{'Amount':>12}")
    print("-" * 42)

    for item in order:
        print(
            f"{item['name']:<16}"
            f"{item['quantity']:>5}"
            f"{item['price']:>9}"
            f"{item['amount']:>12}"
        )

    print("-" * 42)
    print(f"{'Grand Total:':<29} Rs. {grand_total}")
    print("=" * 42)
    print("Thank you! Visit again.")

    order_number += 1


def show_sales():
    print("\n========== SALES REPORT ==========")
    print(f"Total Sales: Rs. {total_sales}")


def main():
    while True:
        print("\n===== RESTAURANT MANAGEMENT SYSTEM =====")
        print("1. Display Menu")
        print("2. Take Customer Order")
        print("3. View Total Sales")
        print("4. Exit")

        choice = input("Enter your choice: ").strip()

        if choice == "1":
            display_menu()

        elif choice == "2":
            take_order()

        elif choice == "3":
            show_sales()

        elif choice == "4":
            print("Thank you for using the system!")
            break

        else:
            print("Invalid choice. Please try again.")


if __name__ == "__main__":
    main()
