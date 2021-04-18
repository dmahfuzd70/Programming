### Method Overloading:

Method overloading is a approach of defining multiple behaviour
of method. 

In method overloading output can change depand on input. Input 
change means Type of input, Number of input, Order of input.

      public void Test()                
      public void Test(int i)           //Here change type of input
      public void Test(string s)        //Here change type of input
      public void Test(int i, string s) //Here chage number of input 
      public void Test(string s, int i) //Here change order of input. 


public string Test() //invalid

Note: It is invalid because return type not consideration
like string or void there consideration is only parameter of
method.


      namespace OverloadProject
      {
         class Program
         {
           public void Test()
           {
             Console.WriteLine("1st Method");
           }
            public void Test(int i)
           {
              Console.WriteLine("2nd Method");
           }
           public void Test(string s)
           {
              Console.WriteLine("3rd Method");
           }
           public void Test(int i, string s)
           {
              Console.WriteLine("4th Method");
           }
           public void Test(string s, int i)
           {
              Console.WriteLine("5th Method");
           }       
           public static void Main(string[] args)
           {
               Program p = new Program();
               p.Test();
               p.Test(10);
               p.Test("Mahfuz");
               p.Test(10,"Mahfuz");
               p.Test("Mahfuz",10);     
           }		
         }
      }
