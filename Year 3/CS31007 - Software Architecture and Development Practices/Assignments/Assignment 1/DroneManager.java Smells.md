
| Location | Smell            | Problem(s) Caused | Refactoring Method                    | Refactoring Example | Why Refactor? |
| -------- | ---------------- | ----------------- | ------------------------------------- | ------------------- | ------------- |
| 34-58    | Switch statement |                   | Replace Conditional with Polymorphism | [[#34 - 58]]        |               |
| 20-68    | Long Method      |                   | Split Method into Smaller Methods     |                     |               |
| 74-76    | Dead Code        |                   | Remove Method                         |                     |               |
## Examples
### 34 - 58
```Java
public interface Customer {
	public void checkDrone();
}

public class PremiumCustomer implements Customer {
	@Override
	public Drone selectDrone(List<Drone> availableDrones) {
        for (Drone d : availableDrones) {
            // ### assume logic here to check drone features and qualities, e.g., speed, model, capacity,
            // ### range, stealth properties catered specifically to a Premium client configuration
        }
        return selectedDrone;
    }
}

public class StandardCustomer implements Customer {
	@Override
	public Drone selectDrone(List<Drone> availableDrones) {
        for (Drone d : availableDrones) {
            // ### assume logic here to check drone features and qualities, e.g., speed, model, capacity,
            // ### range, stealth properties catered specifically to a Standard client configuration
        }
        return selectedDrone;
    }
}

public class GovernmentCustomer implements Customer {
	@Override
	public Drone selectDrone(List<Drone> availableDrones) {
        for (Drone d : availableDrones) {
            // ### assume logic here to check drone features and qualities, e.g., speed, model, capacity,
            // ### range, stealth properties catered specifically to a Government client configuration
        }
        return selectedDrone;
    }
}
```
### 20 - 68
```Java
private void displayStatus(){
	System.out.println("Initiating dispatch sequence...");
}

private List<Drone> identifyAvailableDrones() {
	List<Drone> availableDrones = new ArrayList<>();
	for (Drone d : drones) {
		if (d.getStatus().equals("IDLE") && d.getBatteryLevel() > 20 && d.getHealth().equals("HEALTH_OK")) {
			availableDrones.add(d);
		}
	}
	return availableDrones;
}

private void selectDrone(List<Drone> availableDrones) {
	
}

private double calculateDistance(Drone selected) {
	return Math.sqrt(Math.pow(lat - selected.getLat(), 2) + Math.pow(lng - selected.getLng(), 2));
}

private void displayDroneInformation(Drone selectedDrone, double distance) {
	System.out.println("Drone " + selectedDrone.getID() + " flying " + distance + "km at speed " + selectedDrone.getSpeed());
}

public void dispatchDrone(double lat, double lng, double weight, int priority, String customerType) {
	List<Drone> availableDrones = identifyAvailableDrones();
	selectedDrone = selectDrone(availableDrones);
	double distance = calculateDistance(selectedDrone);
	displayDroneInformation(selectedDrone, distance);
}
```

