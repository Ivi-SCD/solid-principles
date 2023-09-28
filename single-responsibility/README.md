# Single Responsability Principle (SRP)

The Single Responsibility Principle (SRP) is one of the SOLID principles of software design, **emphasizing the importance of having a single reason to change** for each class or component in your codebase. In essence, a class should have one and only one responsibility.

## Importance

SRP helps you create code that is clean, focused, and easier to maintain. When a class adheres to SRP, it becomes more straightforward to understand, test, and extend. Here's why SRP is essential:

* **Maintainability** (Changes in one responsibility are less likely to affect other parts of the codebase)
* **Testability** (You can focus on specific behavior without dealing with unrelated concerns)
* **Reusability** (Classes with narrowly focused responsibilities can be employed in various contexts)

## How to Apply SRP in Java?

To implement SRP effectively, you can follow these steps:

1. **Identify Responsabilities**: Understand the different responsibilities or tasks your class performs. A class should encapsulate a single responsibility.
2. **Separate Concerns**: Split the responsibilities into separate classes or components. Each class should focus on one aspect of the functionality.
3. **Delegate Responsibilities**: If a class becomes too complex due to a single responsibility, delegate parts of that responsibility to other classes.

#

### Explicit Violation of SRP:

```java
public class Employee {
    private String name;
    private String address;
    private double salary;
    
    public Employee(String name, String address, double salary) {
        this.name = name;
        this.address = address;
        this.salary = salary;
    }
    
    public void calculateSalary() {
        // Logic for calculating the employee's salary
    }
    
    public String generatePerformanceReport() {
        // Logic for generating the performance report
    }
    
    public void recordAttendance() {
        // Logic for recording employee attendance
    }

    public void requestLeave(Date startDate, Date endDate) {
        // Logic for processing leave requests
    }
    
    // Getters and setters for name, address, and salary
}
```

This class violates SRP because it has multiple reasons to change, making it difficult to maintain, test, and understand. To adhere to SRP, you should refactor this class into separate classes, each responsible for a single aspect of an employee's functionality, as shown in the previous response.

#

### Application of SRP

#### Identifying the responsibilities:

That Employee Class have the respective responsibilities:
* Storing employee information (name, address, and salary).
* Calculating the employee's salary.
* Generating employee performance reports.
* Managing employee attendance and leave records.

#### Separate the Concerns: 

```java
public class EmployeeInfo {
    private String name;
    private String address;
    // other personal details, getters, and setters
}
```

```java
public class EmployeeSalary {
    public double calculateSalary(EmployeeInfo employee) {
        // Logic for calculating the employee's salary
    }
}
```

```java
public class EmployeeReport {
    public String generatePerformanceReport(EmployeeInfo employee) {
        // Logic for generating the performance report
    }
}
```

```java
public class EmployeeAttendance {
    public void recordAttendance(EmployeeInfo employee) {
        // Logic for recording employee attendance
    }

    public void requestLeave(EmployeeInfo employee, Date startDate, Date endDate) {
        // Logic for processing leave requests
    }
}
```

By breaking down the responsibilities into separate classes, you ensure that each class has a single reason to change and follows the SRP. This makes the codebase more modular, easier to maintain, and allows for better separation of concerns.

#### Delegate Responsibilities:

The `Employee` class no longer holds these responsibilities, but it can use these new classes to delegate tasks:

```java
public class Employee {
    private EmployeeInfo employeeInfo;
    private EmployeeSalary employeeSalary;
    private EmployeeReport employeeReport;
    private EmployeeAttendance employeeAttendance;
    
    public Employee(String name, String address, double salary) {
        employeeInfo = new EmployeeInfo(name, address, salary);
        employeeSalary = new EmployeeSalary();
        employeeReport = new EmployeeReport();
        employeeAttendance = new EmployeeAttendance();
    }
    
    // You can delegate tasks to the respective classes as needed.
    
    public double calculateSalary() {
        return employeeSalary.calculateSalary(employeeInfo);
    }
    
    public String generatePerformanceReport() {
        return employeeReport.generatePerformanceReport(employeeInfo);
    }
    
    public void recordAttendance() {
        employeeAttendance.recordAttendance(employeeInfo);
    }

    public void requestLeave(Date startDate, Date endDate) {
        employeeAttendance.requestLeave(employeeInfo, startDate, endDate);
    }
}
```

By following these steps, we've refactored the `Employee` class to adhere to the Single Responsibility Principle (SRP), separating concerns and delegating responsibilities to dedicated classes. This approach makes the code more modular, maintainable, and easier to understand.