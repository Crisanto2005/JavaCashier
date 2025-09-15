# JavaCashier

class Product {
    String name;
    double price;
    int stock;

    Product(String name, double price, int stock) {
        this.name = name;
        this.price = price;
        this.stock = stock;
    }
}

class Purchase {
    Product product;
    int quantity;

    Purchase(Product product, int quantity) {
        this.product = product;
        this.quantity = quantity;
    }

    double getTotal() {
        return product.price * quantity;
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

}

   // Update stock and add to cart
            selected.stock -= qty;
            cart.add(new Purchase(selected, qty));
            System.out.printf("%d x %s added to cart.%n", qty, selected.name);

            // Validation loop for Y/N input
            while (true) {
                System.out.print("Add more items? (Y/N): ");
                moreItems = sc.next().charAt(0);

                if (moreItems == 'Y' || moreItems == 'y' ||
                    moreItems == 'N' || moreItems == 'n') {
                    break;
                } else {
                    System.out.println("ERROR: Please enter only 'Y' or 'N'.");
                }
            }

        } while (moreItems == 'Y' || moreItems == 'y');

        // Generate receipt
        System.out.println("\n===== RECEIPT =====");
        System.out.printf("%-15s %5s %8s %10s%n", "Item", "Qty", "Price", "Total");
        System.out.println("------------------------------------------------");
        double grandTotal = 0;
        for (Purchase p : cart) {
            double total = p.getTotal();
            System.out.printf("%-15s %5d %8.2f %10.2f%n",
                    p.product.name, p.quantity, p.product.price, total);
            grandTotal += total;
        }
        System.out.println("------------------------------------------------");
        System.out.printf("%-30s %10.2f%n", "GRAND TOTAL:", grandTotal);

        // Payment handling
        double cash = 0;
        while (cash < grandTotal) {
            System.out.print("Enter cash received: ");
            cash += sc.nextDouble();

            if (cash < grandTotal) {
                System.out.printf("Insufficient payment. Remaining balance: %.2f%n", grandTotal - cash);
            }
        }

        double change = cash - grandTotal;
        System.out.printf("Change: %.2f%n", change);
        System.out.println("Thank you for your purchase!");

        sc.close();
    }
}
