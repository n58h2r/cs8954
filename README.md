java c1.1  Introduction

Volunteer work is admirable, but many people enjoy being paid 
for the work they do for an employer. Depending on the type of 
employee, said employee may be paid by the hour, a ﬁﬁxed rate 
(salaried), or be on some bonus/commission payment scale.

For this assignment, I provide an interface called IEmployee. Do 
not modify, extend, or in any way alter this interface - other than 
to embellish the JavaDoc if required to pass the checkStyle tests.

You will create two concrete classes that implement this 
interface: HourlyEmployee and SalariedEmployee. You will 
also provide a test class that will test your code. This class must 
be named IEmployeeTest.

1.2  What to do

EMPLOYEES

All of your assets for this assignment must be placed in a 
package named student.

We're dealing with money for this example (US dollars). Consider 
investigating the BigDecimal and DecimalFormat classes to 
help you deal with fractional items. The rounding mode you 
should use for this assignment is RoundingMode.HALF_UP (in 
other words, round up the fractional parts beyond the second 
decimal place)

You must implement the provided IEmployee interface.

package student;
/**
 * An interface representing the concept of Employees.
Note: This assignment is a bit diﬀﬀerent from the previous homework, and asks you to 
practice with JUnit 5. Ensure you read the instructions carefully and submit what is 
required. */
public interface IEmployee {
 // NOTES (you may remove these notes after you understand the assignment if they 
cause checkStyle issues): 
 // The max HOURLY base salary is $50.00 (per hour). 
 // The max Salaried base salary is $1 million per year.
 // HourlyEmployees earn 1.5x base salary for any time worked > 40 hours in a 
period.
 // SalariedEmployees are paid monthly. For one pay period their salary should be 
baseSalary/12
 
 /**
 * @return the employee's pay for the given period.
 * Hourly employees are paid weekly based on the number of hours worked.
 * Salaried employees are paid monthly, with a given paycheck of 1/12 their yearly 
salary
 *
 */
 double getPayForThisPeriod();
 /**
 * @return the employee's base salary.
 * Hourly employees answer their hourly rate.
 * Salaried employees answer their yearly salary
 */
 double getBaseSalary();
 /**
 * @param raisePercent raises the employee's base salary from 0% (minimum) to 10% 
maximum.
 * The parameter is a value between 0.0 and 10.0. This method converts that value 
to a decimal value
 * 0 - 0.10 when required for calculations.
 */
 void giveRaiseByPercent(double raisePercent);
 /**
 * @return Returns employee ID.
 */
 String getID();
 /**
 * @return Returns employee name.
 */
 String getName();
}
Create two concrete classes (remember, both of these classes 
should be created in the student package as 
well): HourlyEmployee and SalariedEmployee.
Your HourlyEmployee class must include a constructor that 
follows this signature:

public HourlyEmployee(String name, String id, double hourlySalary, double normalHours)
HourlyEmployees also have an additional method NOT listed 
in the shared interface:

/**
 * This method allows HourlyEmployees to supersede the number of hours worked for the 
week.
 */
public void setSpecialHours(double hours)
HourlyEmployees have a name, ID, and an hourly salary. When 
created, these employees specify the "normal" number of hours 
they typically work each week. The weekly hours cannot be  less 
than zero (0) and cannot be more than 80.0. If this constraint is 
not met, your HourlyEmployee should throw 
an IllegalArgumentException.

An HourlyEmployee also gets paid "time and one-half" (1.5x) 
for any hours worked over 40.0 
hours. HourlyEmployees override their "normal" hours by 
calling the setSpecialHours() method. By calling this 
method, an HourlyEmployee temporarily sets their "hours for 
the week" to the value passed to this method (same constraints 
as described above - the value must be between 0 and 80.0 
hours).
This "override" does not persist, so after the代 写data、Java
代做程序编程语言 
method getPayForThisPeriod() is called, the employee's 
"normal hours" are re-activated for any subsequent payments.

Your SalariedEmployee class must include a constructor that 
follows this signature:

public SalariedEmployee(String name, String id, double yearlySalary)
For both types of employees, if their constructors are given a 
salary less than zero (0) or greater than the maximum allowable 
salary (based on the type of employee), throw 
an IllegalArgumentException.For both types of employees, if their constructors are given null 
or an empty String ("") for either the name or ID, throw 
an IllegalArgumentException.

When the giveRaiseByPercent() method is called for either 
type of employee, the base salary for the employee object should 
be increased by the percentage speciﬁﬁed by the parameter 
passed in. Allowable values for the raise percentage is any 
number between 0 and 10.0. Any value outside of this range 
should raise an IllegalArgumentException.
Note: The maximum salary constraint must be maintained during 
this operation. Therefore, if a "raise" request would take the 
employee's salary above the maximum, this request should be 
ignored. Do NOT throw an exception. Instead, leave the 
employee's salary unchanged.

void giveRaiseByPercent(double raisePercent);
 

IEmployeeTest

Design your IEmployeeTest class to be a JUnit5 test class. 
Here is some starter code - you may opt to use this if you wish:

// This is a placeholder for student code.
package student;
import org.junit.jupiter.api.*;
import static org.junit.jupiter.api.Assertions.*;
public class IEmployeeTest {
    HourlyEmployee snoopyHours = new HourlyEmployee("Snoopy", "111-CHLY-BRWN", 17.50, 
20);
 SalariedEmployee lucy = new SalariedEmployee("Lucy", "222-22-2222", 70000.00);
 IEmployee woodStock = new SalariedEmployee("Woodstock", "33-CHIRP", 180000.50);;
 // sample test provided to students
 @Test
 public void testGetErrorWhenCreatingEmployee() {
 Assertions.assertThrows(IllegalArgumentException.class, () -> { IEmployee e = new HourlyEmployee(null, null, 15.51, 30);
 });
 Assertions.assertThrows(IllegalArgumentException.class, () -> {
 IEmployee e = new HourlyEmployee("Part-timer", "PT-TIME", -1, 30);
 });
 }
 @Test
 public void testGetHappyDayEmployee() {
 }
 @Test
 public void testGetPayForThisPeriod() {
 }
 @Test
 public void testGetBaseSalary() {
 }
 @Test
 public void testGetID() {
 }
 @Test
 public void testGetName() {
 }
}
Note: Unlike our the assignments we'll be doing for the rest of 
the semester, I'm asking you to place ALL of your assets in the 
same package (the one called student).

You need to have the six methods preﬁﬁxed by "testGet" methods 
above. The automated grader we're using for this assignment is 
diﬀﬀerent than the one used on homework 1  2, so your test 
methods need to follow this form. Spelling and case-sensitivity is 
important here so I suggest you copy the template given above.

You should write more tests than what I've given you here. 
However, at the very least, be sure you develop the six "starter 
tests" I've given you.
Notes:

For this assignment, we'll be running your JUnit tests against 
your code, our exemplar code (what we think is correct) and a 
sample of code in which we have purposely injected some bugs/
defects. Of course, your tests should validate your code (and 
your solution should pass your tests). Additionally, your JUnit 
tests will be evaluated on how well it exercises our code (and 
detects the errors we have in the "buggy" solution). We'll also be 
running a test code coverage analyzer to see how much of your 
solution code you test with your JUnit. Part of your grade will be 
calculated based on code coverage (of your own code, not of 
ours).

You should provide a suitable .toString() method for 
Employees:
Name: Clark Kent
ID: SUPS-111
Base Salary: $416.50
As part of your submission, remember:

• Create a UML class diagram that describes your solution 
and include it with your submission

         
加QQ：99515681  WX：codinghelp  Email: 99515681@qq.com
