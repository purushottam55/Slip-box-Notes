![[Screenshot_2025-08-06-00-42-23-34_439a3fec0400f8974d35eed09a31f914.jpg]]

#ocpquestion 
Pod pending state.

Need to correct the memory size

Ans - 

$ oc edit deployment deployment_name


Go down :

Resources:
   Request:
    Memory :          

Remove this 3 parameters pod will come in running state.

----

As application produces output check route if not expose and check.


[[Breakdown OCP - Exam]]