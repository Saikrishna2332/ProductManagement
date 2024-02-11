//ProductManagement
import java.util.HashMap;
import java.util.Map;
class Product {
    private int productId;
    private String title;
    private String author;
    private double basePrice;
    private int quantity;
    public Product(int productId, String title, String author, double basePrice, int quantity) {
        this.productId = productId;
        this.title = title;
        this.author = author;
        this.basePrice = basePrice;
        this.quantity = quantity;
    }
    public void applyDiscount(double discountPercentage) {
        double discountAmount = basePrice * discountPercentage / 100;
        basePrice -= discountAmount;
    }
    public void applyTax(double taxRate) {
        double taxAmount = basePrice * taxRate / 100;
        basePrice += taxAmount;
    }
    public void displayDetails() {
        System.out.println("Product ID: " + productId);
        System.out.println("Title: " + title);
        System.out.println("Author: " + author);
        System.out.println("Base Price: ₹" + basePrice);
        System.out.println("Quantity: " + quantity);
    }
}
class ProductManager {
    private Map<Integer, Product> catalog;
    public ProductManager() {
        this.catalog = new HashMap<>();
        catalog.put(123, new Product(123, "The Adventure", "Author X", 30.0, 50));
        catalog.put(456, new Product(456, "Tax Law Handbook", "Author Y", 40.0, 30));
    }
    public void applyDiscountOrTax(int productId, double discountOrTax, boolean isDiscount) {
        Product product = catalog.get(productId);
        if (product != null) {
            if (isDiscount) {
                product.applyDiscount(discountOrTax);
                System.out.println("Discount applied successfully.");
            } else {
                product.applyTax(discountOrTax);
                System.out.println("Tax applied successfully.");
            }
            product.displayDetails();
        } else {
            System.out.println("Product with ID " + productId + " not found.");
        }
    }
}
public class ProductManagement {
    public static void main(String[] args) {
        ProductManager manager = new ProductManager();
        manager.applyDiscountOrTax(123, 10.0, true);
        manager.applyDiscountOrTax(456, 5.0, false);
    }
}
