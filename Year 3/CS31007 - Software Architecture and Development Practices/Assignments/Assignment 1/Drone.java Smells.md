| Location | Smell               | Problem(s) Caused | Refactoring Method             | Refactoring Example | Why Refactor                        |
| -------- | ------------------- | ----------------- | ------------------------------ | ------------------- | ----------------------------------- |
| 15 - 17  | Primitive Obsession |                   | Replace Data Value with Object | [[#15 - 17]]        | Allows Location to be used anywhere |
| 58 - 67  | Feature Envy        |                   | Move Method                    | [[#58 - 17]]        |                                     |
|          | Comments?           |                   |                                |                     |                                     |
## Refactors
### 15 - 17
```Java
public class Location {
	private double lat;
	private double lng;
	private double alt;
	
	// Getters and Setters for Location class
}
```
### 58 - 17
```Java
// Inside MainCircuit class

public string getHealth() {
	if ((voltage < 10.5) &&(capacitorLevel < 0.5) && (capacitorCharge < 10.2) && (acFade == false)) {
		return "MAINTENANCE_REQUIRED";
	}
	else {
		return "HEALTH_OK";
	}
}
```