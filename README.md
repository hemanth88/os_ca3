# os_ca3
#include<stdio.h>
#include<conio.h>
int main()
{
  printf("\t\t\t----------------------- Scheduling -----------------------\n\n\n\n");
  int n,i=0,j=0;
  printf("Enter Number of Processes : ");
  scanf("%d",&n ); 
  float pri[n],bt[n],at[n],pro[n],wt[n],tt[n], temp,ct[n];
  float avg_waiting,avg_turnaround,wait_final,wait_avg,turnaround_final,turnaround_avg;
  float min,sum=0,sum2=0;
  for(i=0;i<n;i++)
  {
  	printf("Enter Arrival Time for Process p%d : ", i+1 );
    scanf("%f", &at[i] );
    printf("Enter Burst Time for  Process  p%d : ", i+1 );
    scanf("%f", &bt[i]);  
    pro[i]=i+1;
  }
  for(i=0;i<n;i++)
  {
    for(j=0;j<n;j++)
    {
      if(at[i]<at[j])
      {
        
        temp = bt[j];
        bt[j] = bt[i];
        bt[i] = temp;
	
	      temp = pro[j];
        pro[j] = pro[i];
        pro[i] = temp;

	      temp = at[j];
        at[j] = at[i];
        at[i] = temp;
      
      }
    }
  }
  
  int k = 1;
  float b_time = 0;
  for(j=0;j<n;j++)
  {
    b_time = b_time + bt[j];
    min = bt[k];

    for(i=k;i<n;i++)
    {
      if((b_time >= at[i])&&(bt[i]<min))
      {
        temp = bt[k];
        bt[k] = bt[i];
        bt[i] = temp;

        temp = at[k];
        at[k] = at[i];
        at[i] = temp;

        temp = pro[k];
        pro[k] = pro[i];
        pro[i] = temp;
      }
    }
    k++;
  }
  wt[0] = 0;
  for(i=1;i<n;i++)
  {
    sum += bt[i-1];
    wt[i] = sum - at[i];
    wait_final += wt[i]; 
  }
  wait_avg = wait_final/n;
  for(i=0;i<n;i++)
  {
    sum2 += bt[i];
    tt[i] = sum2 - at[i];
    turnaround_final += tt[i];
  }
  turnaround_avg=turnaround_final/n;  
  ct[0] = bt[0];
  for(i=1;i<n;i++)
  {
    ct[i] = ct[i-1] + bt[i];
  }
  for(i=0;i<n;i++)
  {
    pri[i] = 1+wt[i]/ct[i];
    printf("\npriorty p%d of :%f",i+1,pri[i]);
  }
printf("\n");

  printf("\t\tProcess\tArrival Time\tBurst Time\tWaiting Time\tTurn Around Time\n");
  printf("\t-------------------------------------------------------------------------------------\n");
  printf("\t\t P%0.0f \t\t %0.0f \t\t %0.0f \t\t %0.0f \t\t %0.0f \n",pro[0],at[0],bt[0],wt[0],tt[0]);
  for(i=n-1;i>0;i--)
  {
  printf("\t\t P%0.0f \t\t %0.0f \t\t %0.0f \t\t %0.0f \t\t %0.0f \n",pro[i],at[i],bt[i],wt[i],tt[i]);
  }
  printf("\t--------------------------------------------------------------------------------------\n");

  printf("\n\n\n\t\t\tAverage Turn Around Time : %f",turnaround_avg);
  printf("\n\t\t\tAverage Waiting Time     : %f\n\n",wait_avg);
	
  getch();
  return 0;
}
