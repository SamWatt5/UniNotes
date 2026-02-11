| Location   | Smell                  | Problem(s) Caused | Refactoring Method             | Refactoring Example | Why Refactor?   |
| ---------- | ---------------------- | ----------------- | ------------------------------ | ------------------- | --------------- |
| 42-58      | Innapropriate Intimacy |                   | Remove methods from this class |                     |                 |
| 26, 29, 33 | Magic Numbers          |                   | Use Global Variables           |                     | [[#26, 29, 33]] |
| 19         | Law of Demeter         |                   |                                |                     |                 |
## Examples
### 26, 29, 33
```Java
public Static Final Double PRICE_PER_KG = 1.5;

public Static Final Double LARGE_PACKAGE_CHARGE = 10.0;

public Static Final Double PRIORITY_PACKAGE_CHARGE = 5.0;

public double getShippingCost(Package p) {
	double base = p.getWeight() * PRICE_PER_KG; // standard rate of £1.50 per kg
	if (p.getDimensions().equals("LARGE")) {
		base = base + LARGE_PACKAGE_CHARGE;  // extra £10 added for large packages            
	}
	if (p.isPriority()) {
		base = base + PRIORITY_PACKAGE_CHARGE;  // extra £5 added for priority items
	}
	return base;
}
```
### 19
```Java
// Inside Warehouse class
public String getZipCode() {
	// ### Add getZipCode to Inventory class too!
	return inventory.getZipCode();
}

// Inside PackageProcessor class
public String getPackageZipCode() {
	return warehouse.getZipCode();
}
```