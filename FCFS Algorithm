#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include "task.h"
#include "cpu.h"
#include "schedulers.h"
// Kích thước mảng task.
#define SIZE 100
static int i=0;
Task task[SIZE];
// Thêm 1 task vào danh sách.
void add(char *name, int priority, int arrival, int burst) {
	task[i].name = name;
	task[i].burst = burst;
	task[i].arrival = arrival;
	task[i].priority = priority;
	i++;
}
// Invoke scheduler FCFS.
void schedule(){
	int j=0;
	int time=0;
	// Mảng chứa thời gian chờ và thời gian quay vòng.	
	int wt[SIZE], tt[SIZE];
	float awt = 0, att = 0;
	// Sắp xếp theo tiêu chí fcfs.
	for(j=0;j<i;j++) {
		for(int k = j+1;k<i;k++) {
			if(task[j].arrival > task[k].arrival) {
				Task temp = task[j];
				task[j] = task[k];
				task[k] = temp;
			}
		}
	}
	// Chạy task đã được sắp xếp và tình thời gian chờ, thời gian quay vòng.
	for(j=0 ; j < i ; j++) {
		// Thời gian trống không có task.
		if(task[j].arrival > time){
			printf("Running task = IDLE from %d to %d.\n",time,task[j].arrival); 	
			time=task[j].arrival;
		}
		wt[j] = time - task[j].arrival;
		tt[j] = wt[j] + task[j].burst;
		awt += wt[j];
		att += tt[j];
		run(&task[j],time,task[j].burst);
		time += task[j].burst;
	}
	printf("Average waiting time: %f\n", awt / (float) i);
	printf("Average turnaround time: %f\n", att / (float) i);
}
