# FCFS
To understand FCFS ,Basic Termlogy ,Pseudo-Code and actual implementation with problems.

# Introduction:-
---------------------------
Full form of FCFS is that first come and first serve 
That's means if any process come first in ready queue
then that will be run first according to our order.
=>If this process is start then cann't be preempted in running process
after completion of this process another process will be start.

# Basic Termology In FCFS CPU Scheduling:-
-------------------------------------
1.Burst Time(BT)=>This time required by the process to complete execution.
2.Waiting Time(WT) =>This is a waiting time after enter in the ready queue,
its wait for own order for execution.
3.Turnaround Time(TAT) => This a total time taken from submission to completion of process.
           TAT=BT+WT

4.Arrival Time(AT)=> The time at which the process complete its execution.


# FXFS Algorithms Steps  :-
-----------------------------
(i) Initialize WT of the 1st process as 0.
(ii) For every subsquent process:
               WT[i]=BT[i-1]+WT[i-1]
               
(iii)Calculate TAT for all process :
     TAT[i]=BT[i]+WT[i]

(iv)Calculate Average WT & TAT:
avg_tat=Total TAT/No. of process
avg_wt=Total WT/No. of process



---.---.---.---.---.---.---.---.---.---.---.---.---.---.---.---.---.
Problem Statement
Given a set of processes with their burst times and arrival times, 
calculate the waiting time and turnaround time for each process using FCFS scheduling.

Process Details
------------------------
Process  | Arrival Time | Burst Time
P1       | 0            | 4
P2       | 1            | 3
P3       | 2            | 2
P4       | 3            | 1

FCFS Algorithm
----------------------------
1.Sort processes by their arrival time.

2.Calculate the waiting time for each process.

3.Calculate the turnaround time for each process.

Numerical Solution
-----------------------
Calculate Waiting Time:

Waiting Time (WT) = Start Time (ST) - Arrival Time (AT)

Start Time for the first process is its arrival time.

For subsequent processes, Start Time = Finish Time of the previous process.

Calculate Turnaround Time:

Turnaround Time (TAT) = Waiting Time (WT) + Burst Time (BT)

Calculation Table:
Process	Arrival Time (AT)	Burst Time (BT)	Start Time (ST)	Finish Time (FT)	Waiting Time (WT) = ST - AT	Turnaround Time (TAT) = WT + BT
P1	0	 4	0	 4	0	4
P2	1	 3	4	 7	3	6
P3	2	 2	7  9	5	7
P4  3	 1	9	10	6	7

Explanation
----------------------------------------------------------------------------------------
P1: Arrives at time 0, starts immediately. WT = 0, TAT = 4.

P2: Arrives at time 1, starts after P1 completes. ST = 4, WT = 3 (4 - 1), TAT = 6 (3 + 3).

P3: Arrives at time 2, starts after P2 completes. ST = 7, WT = 5 (7 - 2), TAT = 7 (2 + 5).

P4: Arrives at time 3, starts after P3 completes. ST = 9, WT = 6 (9 - 3), TAT = 7 (1 + 6).

Key Metrics:
Average Waiting Time = (0 + 3 + 5 + 6) / 4 = 3.5

Average Turnaround Time = (4 + 6 + 7 + 7) / 4 = 6


# Programs
------------------------------------



#include<stdio.h>
int main()
{
   int n,at[10],bt[10],wt[10],tat[10],ct[10],sum,i,j,k;
   float totaltat=0,totalwt=0;
   printf("enter the total number of processes:");
   scanf("%d",&n);
    printf("\nEnter The Process Arrival Time & Burst Time\n");
    for(i=0;i<n;i++)
    {        printf("Enter Arrival time of process[%d]:",i+1);
             scanf("%d",&at[i]);
            printf("Enter Burst time of process[%d]:",i+1);
             scanf("%d",&bt[i]);
    }
   /*Calculate completion time of processes*/
  sum=at[0];
  for(j=0;j<n;j++)
  {
          sum=sum+bt[j];
          ct[j]=sum;
  }
   /*Calculate Turn Around time */
  for(k=0;k<n;k++)
  {
           tat[k]=ct[k]-at[k];
           totaltat=totaltat+tat[k];
  }
     /*  Calculate Waiting time  */
  for(k=0;k<n;k++)
  {
           wt[k]=tat[k]-bt[k];
    totalwt=totalwt+wt[k];
  }

   printf("\nProcess\tAT\tBT\tCT\tTAT\tWT\n\n\n");
 for(i=0;i<n;i++)
 {
      printf("\nP%d\t %d\t %d\t %d\t %d\t %d\t\n",i+1,at[i],bt[i],ct[i],tat[i],wt[i]);
} 
    printf("\nAverage TurnaroundTime:%f\n",totaltat/n);
    printf("\nAverage Waiting Time:%f",totalwt/n);
    return 0;
}
