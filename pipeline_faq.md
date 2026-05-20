# Frequently Asked Questions for Assignment 5
1. Is it alright that we invalidate our hypothesis, and have little clue why the data invalidates the hypotheses? 

    Yes

2. There are no arguments being passed to the workload. 

    Correct.

3. `daxpy` or `daxpy-gem5`

    You can look inside the `workload/daxpy/Makefile` to see how they differ. `-DGEM5`: In your `daxpy.cpp` code, there are sections wrapped in `#ifdef GEM5`. This flag activates those sections. **ISA** homework showed you what these gem5 functions will do.

4. For the Research questions, the assignment says "Use the data from the experiments that you ran in Step II to answer the following questions."  I believe we should use the data from the experiments in Step 3 instead, is that right? Or must we ignore our experiment result from step 3 and only guess based on step 2?

    You should use the data from Step II, here you are doing the same analysis as Step I, but with the actual instruction mix from simulation. 

5. For the first research question, should we provide reasoning to support our observations? Or, we only explain our reasoning when "Explain your reasoning" is in the question, right? Or, should we explain our reasoning for every single question? 

    You should explain you answer with stats from simulation or observation (step I). The questions repeat themselves, if your explaination is the same, you can refer to the previous explaination.

6. For the second research question, do we mean other factors as in coming up with more independent variables, like number of pipelining stages and the number of instructions? ("these changes", as in, latencies and other independent variables) Or,  do we mean other factors like what is changing in the system compared to the baseline, like how we observed simulation time to change depending on our independent variables. ("these changes", as in, the changes in the system) 

    This is an open ended question, you can say yes or no. If you say no, you can talk about things like pipeline depth, clock rate, etc.

7. One question I have is am I supposed to write two different scripts, one for step 2 - the SinglecycleCPU and one for step 3 - the PipelineCPU, or should I have one script for both step 2 and step 3?

    Either way works, just make sure to explain how to use your script in the `question.md`
