## SOLID Principles:
(Inspired from ArjanCodes, YouTube channel)

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

    # Abstract class for payment processing, and letting other classes to inherit and implement the pay method their own way.
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
    - If we have the object of a parent class, then we can replace it with the object of its child class, without altering the correctness of the program, or breaking the code. This was quite confusing to understand initially, but after seeing several examples and implementing it, I got the hang of it.
    - Example: Let us say we have a task to calculate the area of shapes. The shapes we need are rectangle and square. Initially, we might think of creating a class for square that inherits from rectangle. But square is a special type of rectangle, where the length and breadth are equal. So, if we create a class for square that inherits from rectangle, we would have to override the set_length and set_breadth methods to set both the length and breadth to the same value. This is not a good approach. Instead, we can create a class for rectangle and a class for square that inherits from a common parent class, that is, shape. This way, we can avoid violating the Liskov Substitution Principle.
    - Let me represent another example using Orders that we were discussing before.
    ```python
    """
    Before refactoring (violating Liskov Substitution Principle).
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


    class PaypalPaymentProcessor(PaymentProcessor):
        def pay(self, order, security_code):
            print("Processing paypal payment type")
            print(f"Using email address: {security_code}")
            order.status = "paid"


    order = Order()
    order.add_item("Keyboard", 1, 50)
    order.add_item("SSD", 1, 150)
    order.add_item("USB cable", 2, 5)

    print(order.total_price())
    processor = PaypalPaymentProcessor()
    processor.pay(order, "hi@arjancodes.com")

    """
    After refactoring (satisfies Liskov Substitution Principle).
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
        def pay(self, order):
            pass


    class DebitPaymentProcessor(PaymentProcessor):

        def __init__(self, security_code):
            self.security_code = security_code

        def pay(self, order):
            print("Processing debit payment type")
            print(f"Verifying security code: {self.security_code}")
            order.status = "paid"


    class CreditPaymentProcessor(PaymentProcessor):

        def __init__(self, security_code):
            self.security_code = security_code

        def pay(self, order):
            print("Processing credit payment type")
            print(f"Verifying security code: {self.security_code}")
            order.status = "paid"


    class PaypalPaymentProcessor(PaymentProcessor):

        def __init__(self, email_address):
            self.email_address = email_address

        def pay(self, order):
            print("Processing paypal payment type")
            print(f"Using email address: {self.email_address}")
            order.status = "paid"


    order = Order()
    order.add_item("Keyboard", 1, 50)
    order.add_item("SSD", 1, 150)
    order.add_item("USB cable", 2, 5)

    print(order.total_price())
    processor = PaypalPaymentProcessor("hi@arjancodes.com")
    processor.pay(order)
    ```

- Interface Segregation Principle:
    - 

- Dependency Inversion Principle:
    - 


## 