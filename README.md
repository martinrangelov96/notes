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
                            //.sorted(Comparator.comparing(Employee::getSalary, Comparator.reverseOrder()))
                            .sorted((e1, e2) -> Double.compare(e2.getSalary(), e1.getSalary()))
                            .forEach(employee -> result.append(employee.toString()).append(System.lineSeparator()));
                    System.out.println(result.toString());
                });

---using StringBuilder (faster)

if(str == null || str.trim().isEmpty()){throw new ...}

---String that cannot be null, empty or whitespace

          SPRING MVC

---ApplicationSecurityConfiguration example:

@Configuration
@EnableWebSecurity
@EnableGlobalMethodSecurity(prePostEnabled = true)
public class ApplicationSecurityConfiguration extends WebSecurityConfigurerAdapter {

    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http
                .csrf()
                .csrfTokenRepository(csrfTokenRepository())
                .and()
                .authorizeRequests()
                .antMatchers("/", "/users/login", "/users/register").anonymous()
                .antMatchers("/admin/**").hasAuthority("ADMIN")
                .anyRequest().authenticated()
                .and()
                .formLogin()
                .loginPage("/users/login")
                .usernameParameter("username")
                .passwordParameter("password")
                .defaultSuccessUrl("/home")
                .and()
                .logout();
    }

    private CsrfTokenRepository csrfTokenRepository() {
        HttpSessionCsrfTokenRepository repository =
                new HttpSessionCsrfTokenRepository();
        repository.setSessionAttributeName("_csrf");
        return repository;
    }
}
