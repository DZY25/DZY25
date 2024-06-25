#include <stdio.h>

// 定义进程控制块（PCB）
struct PCB {
    char process_name[10]; // 进程名
    int priority;          // 进程优先级
    int required_time;     // 进程所需时间
    int arrival_time;      // 进程到达时间
    int cpu_time;          // CPU占用时间
    char state[10];        // 进程状态（例如，"running", "waiting", "terminated"）
};

// 显示PCB信息的函数
void display_PCB(struct PCB pcb) {
    printf("Process Name: %s\n", pcb.process_name);
    printf("Priority: %d\n", pcb.priority);
    printf("Required Time: %d\n", pcb.required_time);
    printf("Arrival Time: %d\n", pcb.arrival_time);
    printf("CPU Time: %d\n", pcb.cpu_time);
    printf("State: %s\n", pcb.state);
}

// FCFS（先来先服务）调度算法
void fcfs(struct PCB pcb[], int num_processes) {
    printf("FCFS Scheduling:\n");
    for (int i = 0; i < num_processes; i++) {
        display_PCB(pcb[i]);
    }
}

// 优先级调度算法
void priorityScheduling(struct PCB pcb[], int num_processes) {
    printf("Priority Scheduling:\n");
    // 根据优先级对PCB进行排序（简单的冒泡排序用于演示）
    for (int i = 0; i < num_processes - 1; i++) {
        for (int j = 0; j < num_processes - i - 1; j++) {
            if (pcb[j].priority > pcb[j + 1].priority) {
                struct PCB temp = pcb[j];
                pcb[j] = pcb[j + 1];
                pcb[j + 1] = temp;
            }
        }
    }
    for (int i = 0; i < num_processes; i++) {
        display_PCB(pcb[i]);
    }
}

// 主函数
int main() {
    int num_processes;
    printf("Enter the number of processes: ");
    scanf("%d", &num_processes);

    struct PCB processes[num_processes];

    for (int i = 0; i < num_processes; i++) {
        printf("Enter details for Process %d:\n", i + 1);
        printf("Process Name: ");
        scanf("%s", processes[i].process_name);
        printf("Priority (lower number means higher priority): ");
        scanf("%d", &processes[i].priority);
        printf("Required Time: ");
        scanf("%d", &processes[i].required_time);
        printf("Arrival Time: ");
        scanf("%d", &processes[i].arrival_time);
        processes[i].cpu_time = 0; // 初始CPU占用时间为0
        sprintf(processes[i].state, "waiting"); // 初始状态为等待
    }

    // 选择调度算法
    int choice;
    printf("Choose a scheduling algorithm:\n1. FCFS\n2. Priority Scheduling\nEnter your choice: ");
    scanf("%d", &choice);

    switch (choice) {
        case 1:
            fcfs(processes, num_processes);
            break;
        case 2:
            priorityScheduling(processes, num_processes);
            break;
        default:
            printf("Invalid choice\n");
            break;
    }

    return 0;
}
