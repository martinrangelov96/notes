# notes

          REGEX
          
.split("(?<=[.!?])");
---split without removing the elements you split by: [.!?]

Pattern.compile("^[^.!?]*[.!?]");
---legit sentance, edinng with [.!?]


System.out.println(String.join(", ", candidates));
---doesn't print last comma

          MAPS/SORTING ETC     

employees.stream()
                .collect(Collectors.groupingBy(Employee::getDepartment))
---makes a Map<Department, List<Employees>
  
  sorted((e1, e2) -> Double.compare(
                        e2.getValue().stream().mapToDouble(Employee::getSalary).average().getAsDouble(),
                        e1.getValue().stream().mapToDouble(Employee::getSalary).average().getAsDouble()))
                .limit(1) 
---comparing by average value and gets only the best one by .limint(1)

.forEach(d-> {
                    StringBuilder result = new StringBuilder();
                    result.append(String.format("Highest Average Salary: %s", d.getKey()))
                            .append(System.lineSeparator());
                    d.getValue().stream()
                            .sorted(Comparator.comparing(Employee::getSalary, Comparator.reverseOrder()))
                            .forEach(employee -> result.append(employee).append(System.lineSeparator()));
                    System.out.println(result.toString());
                });
---using StringBuilder (faster)
