# res about python class #

## built-in class attributes ##
内置的类属性

常见的类属性：
- __doc__ #文档注释
- __name__ #类名
- __module__ #模块名
- __bases__ #父类
- __dict__ #所有属性，方法的map集合
    
    class Employee:
   'Common base class for all employees'
   	empCount = 0

   	def __init__(self, name, salary):
    	self.name = name
    	self.salary = salary
    	Employee.empCount += 1
   
   	def displayCount(self):
    	print ("Total Employee %d" % Employee.empCount)

   	def displayEmployee(self):
    	print ("Name : ", self.name,  ", Salary: ", self.salary)

	emp1 = Employee("Zara", 2000)
	emp2 = Employee("Manni", 5000)
	print ("Employee.__doc__:", Employee.__doc__)
	print ("Employee.__name__:", Employee.__name__)
	print ("Employee.__module__:", Employee.__module__)
	print ("Employee.__bases__:", Employee.__bases__)
	print ("Employee.__dict__:", Employee.__dict__ )