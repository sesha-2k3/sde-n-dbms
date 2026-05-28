## SOLID Principles:

- Single Responsibility Principle:
    - A class should have only one reason to change, that is, it should have only one job. 
    - Example: if we create a calculator app, we should have a class for addition, a class for subtraction, a class for multiplication, and a class for division. We should not have a class for all the operations. 
    - Code:
    ```python
    """This is before refactoring, that is, the class Order has multiple responsibilities such as adding items, processig payment and calculating the total price. But in the future, if we want to add a new payment method, we would have to modify the class Order.
    """

    class Order:

    def __init__(self):
        self.items = []
        self.quantities = []
        self.prices = []
        self.status = "open"

    def add_item(self, name, quantity, price):
        self.items.append(name)
        self.quantities.append(quantity)
        self.prices.append(price)

    def total_price(self):
        total = 0
        for i in range(len(self.prices)):
            total += self.quantities[i] * self.prices[i]
        return total

    def pay(self, payment_type, security_code):
        if payment_type == "debit":
            print("Processing debit payment type")
            print(f"Verifying security code: {security_code}")
            self.status = "paid"
        elif payment_type == "credit":
            print("Processing credit payment type")
            print(f"Verifying security code: {security_code}")
            self.status = "paid"
        else:
            raise Exception(f"Unknown payment type: {payment_type}")


    order = Order()
    order.add_item("Keyboard", 1, 50)
    order.add_item("SSD", 1, 150)
    order.add_item("USB cable", 2, 5)

    print(order.total_price())
    order.pay("debit", "0372846")


    """
    This is the code after refactoring, that is the class Order has only one responsibility, that is, it has only one job to do, which is adding items to the order and calculating the total price. We can further create a class for payment processing and another class for adding items to the order.
    """
    class Order:

    def __init__(self):
        self.items = []
        self.quantities = []
        self.prices = []
        self.status = "open"

    def add_item(self, name, quantity, price):
        self.items.append(name)
        self.quantities.append(quantity)
        self.prices.append(price)

    def total_price(self):
        total = 0
        for i in range(len(self.prices)):
            total += self.quantities[i] * self.prices[i]
        return total


    class PaymentProcessor:
        def pay_debit(self, order, security_code):
            print("Processing debit payment type")
            print(f"Verifying security code: {security_code}")
            order.status = "paid"

        def pay_credit(self, order, security_code):
            print("Processing credit payment type")
            print(f"Verifying security code: {security_code}")
            order.status = "paid"


    order = Order()
    order.add_item("Keyboard", 1, 50)
    order.add_item("SSD", 1, 150)
    order.add_item("USB cable", 2, 5)

    print(order.total_price())
    processor = PaymentProcessor()
    processor.pay_debit(order, "0372846")
    ```


- Open/Close Principle:
    - The class should be open for extension but closed for modification, which means that the code you write, should not  be modified in the long run. It should be written in such a way that it can be extended in the future without modifying the existing code.
    - Example: if we want to add a new payment method to the Order class that we wrote above, we would have to modify the existing code (the PaymentProcessor class, by adding a new method, like pay_applepay(), etc.). This can be avoided by using the Open/Close Principle. To be more specific, we can create an abstract class, understanding that the sole purpose of this class is to define payment, and all the classes that inherit from this class will have to implement the pay method, but in their own way. This is abstraction.
    ```python
    """
    Before refactoring.
    """
    class Order:

    def __init__(self):
        self.items = []
        self.quantities = []
        self.prices = []
        self.status = "open"

    def add_item(self, name, quantity, price):
        self.items.append(name)
        self.quantities.append(quantity)
        self.prices.append(price)

    def total_price(self):
        total = 0
        for i in range(len(self.prices)):
            total += self.quantities[i] * self.prices[i]
        return total


    class PaymentProcessor:
        def pay_debit(self, order, security_code):
            print("Processing debit payment type")
            print(f"Verifying security code: {security_code}")
            order.status = "paid"

        def pay_credit(self, order, security_code):
            print("Processing credit payment type")
            print(f"Verifying security code: {security_code}")
            order.status = "paid"


    order = Order()
    order.add_item("Keyboard", 1, 50)
    order.add_item("SSD", 1, 150)
    order.add_item("USB cable", 2, 5)

    print(order.total_price())
    processor = PaymentProcessor()
    processor.pay_debit(order, "0372846")

    """
    After refactoring.
    """
        from abc import ABC, abstractmethod


    class Order:

        def __init__(self):
            self.items = []
            self.quantities = []
            self.prices = []
            self.status = "open"

        def add_item(self, name, quantity, price):
            self.items.append(name)
            self.quantities.append(quantity)
            self.prices.append(price)

        def total_price(self):
            total = 0
            for i in range(len(self.prices)):
                total += self.quantities[i] * self.prices[i]
            return total


    class PaymentProcessor(ABC):

        @abstractmethod
        def pay(self, order, security_code):
            pass


    class DebitPaymentProcessor(PaymentProcessor):
        def pay(self, order, security_code):
            print("Processing debit payment type")
            print(f"Verifying security code: {security_code}")
            order.status = "paid"


    class CreditPaymentProcessor(PaymentProcessor):
        def pay(self, order, security_code):
            print("Processing credit payment type")
            print(f"Verifying security code: {security_code}")
            order.status = "paid"


    order = Order()
    order.add_item("Keyboard", 1, 50)
    order.add_item("SSD", 1, 150)
    order.add_item("USB cable", 2, 5)

    print(order.total_price())
    processor = DebitPaymentProcessor()
    processor.pay(order, "0372846")
    ```

- Liskov Substitution Principle:
    - 

- Interface Segregation Principle:
    - 

- Dependency Inversion Principle:
    - 


## 