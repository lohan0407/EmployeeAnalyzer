
# EmployeeAnalyzer
import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

class Employee {
    private String name;
    private String gender;
    private double salary;

    public Employee(String name, String gender, double salary) {
        this.name = name;
        this.gender = gender;
        this.salary = salary;
    }

    public String getGender() {
        return gender;
    }

    public double getSalary() {
        return salary;
    }
}

public class EmployeeAnalyzer {
    private List<Employee> employees;

    public EmployeeAnalyzer() {
        employees = new ArrayList<>();
    }

    public void addEmployee(String name, String gender, double salary) {
        Employee employee = new Employee(name, gender, salary);
        employees.add(employee);
    }

    public Map<String, Double> calculateAverageSalaryByGender() {
        Map<String, Double> averageSalaries = new HashMap<>();
        Map<String, Integer> genderCount = new HashMap<>();

        for (Employee employee : employees) {
            String gender = employee.getGender();
            double salary = employee.getSalary();

            
            averageSalaries.put(gender, averageSalaries.getOrDefault(gender, 0.0) + salary);
            genderCount.put(gender, genderCount.getOrDefault(gender, 0) + 1);
        }

        
        for (String gender : averageSalaries.keySet()) {
            double totalSalary = averageSalaries.get(gender);
            int count = genderCount.get(gender);
            double average = totalSalary / count;
            averageSalaries.put(gender, average);
        }

        return averageSalaries;
    }

    public static void main(String[] args) {
        EmployeeAnalyzer analyzer = new EmployeeAnalyzer();

        
        analyzer.addEmployee("John", "Male", 50000);
        analyzer.addEmployee("Alice", "Female", 60000);
        analyzer.addEmployee("Bob", "Male", 55000);
        analyzer.addEmployee("Eve", "Female", 65000);

        
        Map<String, Double> averageSalaries = analyzer.calculateAverageSalaryByGender();
        for (Map.Entry<String, Double> entry : averageSalaries.entrySet()) {
            System.out.println("Average Salary for " + entry.getKey() + ": $" + entry.getValue());
        }
    }
}
