# ProductManagement
import java.util.HashMap;
import java.util.Map;

class Product {
    private String productId;
    private String title;
    private String author;
    private double basePrice;
    private int quantity;
    public Product(String productId, String title, String author, double basePrice, int quantity) {
        this.productId = productId;
        this.title = title;
        this.author = author;
        this.basePrice = basePrice;
        this.quantity = quantity;
    }
    public String getProductId() {
        return productId;
    }

    public void setBasePrice(double basePrice) {
        this.basePrice = basePrice;
    }
    public double applyDiscount(double discountPercentage) {
        double discountAmount = basePrice * (discountPercentage / 100);
        return basePrice - discountAmount;
    }
    public double applyTax(double taxRate) {
        double taxAmount = basePrice * (taxRate / 100);
        return basePrice + taxAmount;
    }
}

class ProductCatalog {
    private Map<String, Product> catalog;

    public ProductCatalog() {
        this.catalog = new HashMap<>();
    }
    public void addProduct(Product product) {
        catalog.put(product.getProductId(), product);
    }
    public String updateProductPrice(String productId, String type, double value) {
        Product product = catalog.get(productId);

        if (product == null) {
            return "Product not found";
        }

        if ("discount".equalsIgnoreCase(type)) {
            double discountedPrice = product.applyDiscount(value);
            product.setBasePrice(discountedPrice);
            return "Discount applied successfully. Updated price: " + discountedPrice;
        } else if ("tax".equalsIgnoreCase(type)) {
            double finalPrice = product.applyTax(value);
            product.setBasePrice(finalPrice);
            return "Tax applied successfully. Updated price: " + finalPrice;
        } else {
            return "Invalid operation type. Use 'discount' or 'tax'.";
        }
    }
}
public class ProductManagement {
    public static void main(String[] args) {
        ProductCatalog productCatalog = new ProductCatalog();
        Product fictionBook = new Product("1", "The Adventure", "Author X", 30.0, 50);
        productCatalog.addProduct(fictionBook);
        String discountResult = productCatalog.updateProductPrice("1", "discount", 10.0);
        System.out.println(discountResult);
        Product nonFictionBook = new Product("2", "Tax Law Handbook", "Author Y", 40.0, 30);
        productCatalog.addProduct(nonFictionBook);
        String taxResult = productCatalog.updateProductPrice("2", "tax", 5.0);
        System.out.println(taxResult);
    }
}
