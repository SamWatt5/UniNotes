# Exercise 1
| Example | Code Smell       | Refactor                              | Refactored Code |
| ------- | ---------------- | ------------------------------------- | --------------- |
| 1       | Data clumps      | Parameter Object                      | [[#Example 1]]  |
| 2       | Magic Numbers    | Replace magic numbers with constants  | [[#Example 2]]  |
| 3       | Switch Statement | Replace conditional with polymorphism |                 |
| 4       |                  |                                       |                 |
## Refactored Code
### Example 1
```java
class Address {
	String street;
	String city;
	String zip;
	String state;
}

public void createAppointment(Address address, Date time) {
	// ... logic ...
}

public void updateShippingAddress(Address address) {
	// ... logic ...
}
```
### Example 2
```Java
static final double DEFAULT_PRODUCT_COST = 34.99;
private static final String CURRENCY_SYMBOL = "$";

double productCost = DEFAULT_PRODUCT_COST;

```
### Example 3
```java
	public interface Country {
		public double calculateSpeed();
	}
	public class UK implements Country {
		public double calculateSpeed() {
			
		}
	}
```

### Example 4

# Exercise 2
| Line(s) | Smell       | Refactoring Option(s)    | Refactor Example |
| ------- | ----------- | ------------------------ | ---------------- |
| 16      | Data Clump  | Make Parameter an Object | [[#16]]          |
| 16-101  | Long Method | Extract Method           |                  |
## Refactored Code
### 16
```Java
public class Address {
	private String street;
	private String city;
	private String zip;
	private String country;
	
	public Address(String street, String city, String zip, String country) {
		this.street = street;
		this.city = city;
		this.zip = zip;
		this.country = country;
	}
	
	// Getters and Setters for Address
}

public class Shipment {
	private String customerName;
	private String email;
	private String phone;
	private Address address;
	private List<String> itemNames;
	private List<Double> itemPrices;
	private List<Double> itemWeights;
	private int shippingType;
	private boolean insurance;
	
	// Constructor
	
	// Getters and Setters
}

...

public void processShipment(Shipment shipment)
```
### 16-101
```Java
public final static VAT_RATE = 0.15;

private Double calculateSubtotal(List<Double> itemPrices) {
	double subtotal = 0;
	for (int i=0; i<itemPrices.size(); i++) {
		subtotal += itemPrices.get(i);
	}
	return subtotal;
}

private Double calculateCombinedWeight(List<Double> itemWeights) {
	double weight = 0;
	for (double w : itemWeights) {
		weight += w;
	}
	return weight;
}

private double calculateTax(Double cost) {
	double tax = cost * VAT_RATE;
}

public void processShipment(Shipment shipment) {
	subtotal = calculateSubtotal(itemPrices);
	weight = calculateCombinedWeight(itemWeights);
	tax = calculateTax(subtotal);
}
```