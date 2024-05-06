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
Data hazards refer to conflicts or dependencies between instructions in a computer program that can potentially lead to incorrect behavior or unexpected results. These hazards arise primarily in pipelined processors, where instructions are overlapped in execution to improve performance. However, when instructions depend on the results of previous instructions that have not yet completed, data hazards can occur.

upcoming technologies:
Several upcoming technologies aim to address or mitigate data hazards in various ways:

Out-of-Order Execution: 
This technology allows processors to execute instructions in a different order than they appear in the program, thereby potentially avoiding data hazards by executing independent instructions simultaneously.
Speculative Execution:
Speculative execution involves predicting the outcome of certain branches in code and executing instructions ahead of time based on these predictions. If the predictions are correct, this can hide latency and improve performance. However, if the predictions are incorrect, the speculatively executed instructions may need to be discarded.
Data Forwarding: 
Also known as bypassing, this technique allows a processor to forward the results of a computation directly from one stage of the pipeline to another, avoiding the need to wait for the result to be written back to the register file.
Register Renaming:
Register renaming is a technique used to avoid data hazards caused by dependencies on specific registers. It involves mapping logical registers to physical registers dynamically, allowing instructions to use different physical registers even if they refer to the same logical register.
Hardware Interlock Mechanisms: 
These mechanisms detect and stall the pipeline when a data hazard is detected, allowing the necessary data to propagate through the pipeline before proceeding with the dependent instruction.
Advanced Compiler Optimizations:
Compiler optimizations play a crucial role in minimizing data hazards by reordering instructions, inserting NOPs (no-operation instructions) where necessary, and restructuring code to reduce dependencies.
Cache Hierarchies and Memory Access Optimization: Improvements in cache hierarchies and memory access patterns can reduce the frequency and impact of data hazards by minimizing memory latency and improving data locality.
Hardware Transactional Memory (HTM):
HTM is a technology that enables multiple transactions to occur concurrently in memory without interfering with each other. By allowing transactions to execute speculatively and providing mechanisms for detecting conflicts, HTM can help alleviate data hazards related to memory access.
These technologies are continually evolving to meet the increasing demands for performance and efficiency in modern computing systems.
Control hazards (branch hazards or instruction hazards)
Control hazard occurs when the pipeline makes wrong decisions on branch prediction and therefore brings instructions into the pipeline that must subsequently be discarded. The term branch hazard also refers to a control hazard.

Eliminating hazards
Generic
Pipeline bubbling
Main article: Bubble (computing)
Bubbling the pipeline, also termed a pipeline break or pipeline stall, is a method to preclude data, structural, and branch hazards. As instructions are fetched, control logic determines whether a hazard could/will occur. If this is true, then the control logic inserts no operations (NOPs) into the pipeline. Thus, before the next instruction (which would cause the hazard) executes, the prior one will have had sufficient time to finish and prevent the hazard. If the number of NOPs equals the number of stages in the pipeline, the processor has been cleared of all instructions and can proceed free from hazards. All forms of stalling introduce a delay before the processor can resume execution.

Flushing the pipeline occurs when a branch instruction jumps to a new memory location, invalidating all prior stages in the pipeline. These prior stages are cleared, allowing the pipeline to continue at the new instruction indicated by the branch.

Data hazards
There are several main solutions and algorithms used to resolve data hazards:

insert a pipeline bubble whenever a read after write (RAW) dependency is encountered, guaranteed to increase latency, or
use out-of-order execution to potentially prevent the need for pipeline bubbles
use operand forwarding to use data from later stages in the pipeline
In the case of out-of-order execution, the algorithm used can be:

scoreboarding, in which case a pipeline bubble is needed only when there is no functional unit available
the Tomasulo algorithm, which uses register renaming, allowing continual issuing of instructions
The task of removing data dependencies can be delegated to the compiler, which can fill in an appropriate number of NOP instructions between dependent instructions to ensure correct operation, or re-order instructions where possible.
![image](https://github.com/Noorjahan22/Data-Hazards/assets/168285209/51382942-feb4-48f6-a1ce-8cee8d34145d)


EXAMPLE


![image](https://github.com/Noorjahan22/Data-Hazards/assets/168285209/48c4f524-76d1-46aa-b807-d2ede3c8eb28)
If we look at this particular pipeline execution of these instructions. We find that data
hazard is arising in spite of the fact that results are already available in the pipeline
registers. Although it has not had been data has not had been written into the register that
register where it has to be written that is r 1, but those values which was computed here
in the third clock cycle are already available in different pipeline registers.

Operand forwarding
Main article: Operand forwarding
Examples
In the following examples, computed values are in bold, while Register numbers are not.
For example, to write the value 3 to register 1, (which already contains a 6), and then add 7 to register 1 and store the result in register 2, i.e.:

i0: R1 = 6
i1: R1 = 3
i2: R2 = R1 + 7 = 10
Following execution, register 2 should contain the value 10. However, if i1 (write 3 to register 1) does not fully exit the pipeline before i2 starts executing, it means that R1 does not contain the value 3 when i2 performs its addition. In such an event, i2 adds 7 to the old value of register 1 (6), and so register 2 contains 13 instead, i.e.:

i0: R1 = 6
i2: R2 = R1 + 7 = 13
i1: R1 = 3
This error occurs because i2 reads Register 1 before i1 has committed/stored the result of its write operation to Register 1. So when i2 is reading the contents of Register 1, register 1 still contains 6, not 3.

Forwarding (described below) helps correct such errors by depending on the fact that the output of i1 (which is 3) can be used by subsequent instructions before the value 3 is committed to/stored in Register 1.

Forwarding applied to the example means that there is no wait to commit/store the output of i1 in Register 1 (in this example, the output is 3) before making that output available to the subsequent instruction (in this case, i2). The effect is that i2 uses the correct (the more recent) value of Register 1: the commit/store was made immediately and not pipelined.

With forwarding enabled, the Instruction Decode/Execution (ID/EX) stage of the pipeline now has two inputs: the value read from the register specified (in this example, the value 6 from Register 1), and the new value of Register 1 (in this example, this value is 3) which is sent from the next stage Instruction Execute/Memory Access (EX/MEM). Added control logic is used to determine which input to use.

Control hazards (branch hazards)
To avoid control hazards microarchitectures can:

insert a pipeline bubble (discussed above), guaranteed to increase latency, or
use branch prediction and essentially make educated guesses about which instructions to insert, in which case a pipeline bubble will only be needed in the case of an incorrect prediction
In the event that a branch causes a pipeline bubble after incorrect instructions have entered the pipeline, care must be taken to prevent any of the wrongly-loaded instructions from having any effect on the processor state excluding energy wasted processing them before they were discovered to be loaded incorrectly.

Other techniques
Memory latency is another factor that designers must attend to, because the delay could reduce performance. Different types of memory have different accessing time to the memory. Thus, by choosing a suitable type of memory, designers can improve the performance of the pipelined data path.

To mitigate data hazards, various techniques are employed:

Hardware Interlocking: 
This involves detecting hazards at runtime and stalling the pipeline until the required data is available. Stalls can significantly impact performance, so minimizing them is crucial.
Data Forwarding (Bypassing):
![image](https://github.com/Noorjahan22/Data-Hazards/assets/168285209/8b624ceb-64bb-4f96-88ac-2320f8702667)
, whenever we do forwarding this particular diagram shows, how forwarding is
helping in overcoming data hazards. And as you can see, earlier we were trying to read
this value from this register, instead of reading from this register now, for the second
instruction that the value will be coming from this particular pipeline register, instead of
the register bank that is present in that ALU. So, it is reading from there, so since it is in
the forward direction there is no hazard.
Similarly, we can see here also in the third instruction is also getting the upper hand from
the pipeline register; that means, this r 1 is also read from the pipeline register, and that is
being applied to the one arm of the ALU. And similarly of course, the third instruction
that operant is being read from the register itself.

Instead of stalling the pipeline, this technique forwards data directly from the output of one pipeline stage to the input of another, allowing dependent instructions to proceed without waiting for the data to be written back to registers.
Register Renaming:
By dynamically mapping logical register names to physical register locations, register renaming allows multiple instructions to use the same logical register without causing hazards.
Compiler Optimizations: 
Compilers can rearrange instructions or insert additional instructions to reduce hazards. Techniques like loop unrolling, software pipelining, and instruction scheduling are commonly used.
Software Prefetching: 
By predicting future memory accesses and bringing data into cache preemptively, software prefetching can reduce the impact of memory hazards.
Speculative Execution: 
This technique involves predicting the outcome of conditional branches and executing instructions speculatively along the predicted path. If the prediction is incorrect, the speculatively executed instructions are discarded.
Addressing data hazards effectively requires a combination of hardware and software techniques tailored to the specific characteristics of the processor architecture and the workload being executed. As technology advances, new approaches and optimizations continue to emerge to improve performance and reduce the impact of data hazards in modern computing systems.


Detection and Resolution:

Pipeline Stalls:
When a hazard cannot be resolved immediately (e.g., due to a cache miss or data dependency), the pipeline may need to stall, delaying the execution of subsequent instructions until the hazard is resolved.
Impact on Performance:
Data hazards can significantly impact processor performance by introducing pipeline stalls and reducing instruction throughput.
Pipeline bubbles, caused by stalls due to hazards, reduce the overall efficiency of the processor, leading to lower instructions per cycle (IPC) and degraded performance.
Efficient hazard handling mechanisms, such as data forwarding and register renaming, help minimize the performance impact of data hazards by reducing the frequency and duration of pipeline stalls.
Types of Dependencies:
In addition to RAW, WAR, and WAW hazards, dependencies between instructions can manifest in other forms:
Control Dependencies:
Arise due to conditional branches and determine the flow of execution based on the outcome of previous instructions.
Output Dependencies:
Occur when an instruction produces a result that is used by another instruction but does not involve reading from the same resource (e.g., memory or registers).
Handling these dependencies efficiently is crucial for maximizing instruction-level parallelism and minimizing stalls in the pipeline.
Software Techniques:
Beyond hardware solutions, software optimizations can also help mitigate data hazards:
Compiler Optimizations:
Compilers employ techniques like loop unrolling, software pipelining, and instruction scheduling to reorganize code and minimize dependencies, thereby reducing the likelihood of hazards.
Software Prefetching:
Predictive algorithms can be used to prefetch data into cache ahead of its actual use, reducing the latency associated with memory accesses and mitigating hazards related to memory dependencies.
Understanding and effectively managing data hazards are essential for designing high-performance processors and optimizing software for efficient execution on modern computing systems. By employing a combination of hardware and software techniques, designers can minimize the impact of hazards and maximize the throughput of pipelined processors.
ADVANTAGES /DISADVANTAGES
![image](https://github.com/Noorjahan22/Data-Hazards/assets/168285209/04102573-c695-4346-b223-9f65c6eef47a)
![image](https://github.com/Noorjahan22/Data-Hazards/assets/168285209/88621511-a98d-40c0-a8df-1ea68ae2b007)
![image](https://github.com/Noorjahan22/Data-Hazards/assets/168285209/6f18e42a-584f-4d76-81e1-8ed4f2e4680a)
![image](https://github.com/Noorjahan22/Data-Hazards/assets/168285209/cea08770-e822-4c09-b214-308b3fcb1cd9)
![image](https://github.com/Noorjahan22/Data-Hazards/assets/168285209/78a13671-ffc0-4f89-a84a-4a7139fbf493)
![image](https://github.com/Noorjahan22/Data-Hazards/assets/168285209/034a631d-f078-4067-b804-8cdab2adcefc)



Solution


![image](https://github.com/Noorjahan22/Data-Hazards/assets/168285209/86f58c0f-cd38-456c-b872-0d77b0b4f277)
Now, this is the how can we overcome these hazards, there are several techniques by
which this data hazards can be overcome. The first technique is known as forwarding and
bypassing, forwarding and bypassing technique is based on hardware approach; that
means, you have to add some additional hardware to overcome data hazards. And we
shall see how it can be implemented, the other techniques are essentially software based
first one is basic compiler pipeline scheduling.
And we shall see, how compiler can help in scheduling instructions such that the data
hazard is eliminated or it is impact is reduced. Then this the scheduling that is being done
by compiler is known as static scheduling, on the other hand this scheduling can be done
with the help of hardware, which is known as dynamic scheduling which I shall also
discuss.


* Usually solved by data or register forwarding (bypassing or short-circuiting). This is based on the fact that the data selected is not really used in ID but in the next stage: ALU.

Forwarding works as follows: ALU result from EX/MEM buffer is always fed back to the ALU input keys. If the forwarding hardware detects that its source operand has a new value, the logic selects the newer result rather than the value read from the register file.






