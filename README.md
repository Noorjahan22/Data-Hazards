# Data-Hazards

Data hazards are a significant concern in computer organization, particularly in pipelined architectures where multiple instructions are executed concurrently. These hazards occur when there is a dependency between instructions that can result in incorrect execution or stalls in the pipeline. Here are the main types of data hazards:
1.	Read-After-Write (RAW) Hazard: This occurs when an instruction tries to read a register before a prior instruction writes to it.
2.	 For example:
ADD R1,R2,R3;R1 R2 R3

SUB R4,R1,R5;R4 R1 R5

Write-After-Read (WAR) Hazard: This occurs when an instruction writes to a register that a later instruction reads from.
For example:

SUB R1,R2,R3  ;R1 R2 R3

ADD R4,R1,R5 ; R4 R1 R5

Write-After-Write (WAW) Hazard: This occurs when two instructions write to the same register and the order of execution matters.
For example:

ADD R1,R2,R3;R1 R2 R3

SUB R1,R4,R5;R1 R4 R5

DATA DEPENDENCIES:
 
Overcome: Data Hazards

•	1.Stalling the Pipeline

•	2.Operand Forwarding

•	3. Software approaches


This first two approach is hardware approach

STALLING THE PIPELINE
 
![image](https://github.com/Noorjahan22/Data-Hazards/assets/168285209/9cca8734-411a-41ac-8c51-83921daf7875)

OPERAND FORWARDING

![image](https://github.com/Noorjahan22/Data-Hazards/assets/168285209/aa3ea52c-198b-4430-a299-bfd06d874e82)


![image](https://github.com/Noorjahan22/Data-Hazards/assets/168285209/e48e3285-b569-4a1e-a019-857ce7618906)

AFTER THE MODIFICATION OF  DATAPATH

![image](https://github.com/Noorjahan22/Data-Hazards/assets/168285209/4b682989-4885-41b3-9c0a-b043473fa3ed)

Handling Data Dependencies in Software

•	The compiler identifies the data dependency between two successive instruction Ij and Ij+1. And insert three explicit NOP instruction between them.

•	Delay ensures new value available in register but causes total execution time to increase

![image](https://github.com/Noorjahan22/Data-Hazards/assets/168285209/f39006be-d25f-4dc5-aa98-5e3d76081081)

![image](https://github.com/Noorjahan22/Data-Hazards/assets/168285209/ebb0c879-f54c-41a2-9e0f-1fdce8705585)









