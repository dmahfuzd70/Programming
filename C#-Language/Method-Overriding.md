### Method Overriding:
It's and approach of re-implementing a parent classes method under the child class
with the same signature.

    Class1
    Show(int i)
    Test()

    Class2: Class1
    Show(string i)
    Test()

### Difference between Method Overloading and Overriding

Overloading:
1. In this case we define multiple methods with the
same name by changing their parameters.
2. This can be performed either within a class as well
as between parent child classes also.

    Class1
    Show(int i)
    Test()

    Class2: Class1
    Show(string i)
    Test()

3. While overloading a paren classes method under the
class, child class doesn't require to take any 
permission from the parent class.


    using System;

    namespace ProgramPractice
    {
    class LoadParent
    {
      public void Show()
      {
       Console.WriteLine("Parent's Show Method is Called.");
      }
      public void Test()
      {
       Console.WriteLine("Parent's Test Method is Called.");
      }
    }
    class LoadChild:LoadParent
    {

      public void Show(int i)
      {
       Console.WriteLine("Child;s Show Method is Called.");
      }
       static void Main(string args)
       {
        LoadChild c = new LoadChild();
        c.Show();
        c.Show(10);
        c.Test();	
       }
    }
    }  	




### Overriding:
1. In this case we define multiple methods with the same
name same and the same parameters.
2. This can be performed only between parent child class
never be performed with in the same class.

3. While overriding a parent's method under child class
child class require permission from it's parent.

Note: If we want to override a parent's method under the 
child class first that method should be declared by
using virtual modifier in parent class.
