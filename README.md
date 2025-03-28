# Virtual-os-for-Educational-Simulations
# --------- Module 1: Data Collection ---------
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>

#define MAX_PROCESSES 5

typedef struct VirtualProcess {
    char name[50];
    int pid;
    int memory; // Simulated memory allocation
    int execution_time;
} VirtualProcess;

VirtualProcess* process_list[MAX_PROCESSES];
int process_count = 0;

void create_process(char* name, int memory, int execution_time) {
    if (process_count >= MAX_PROCESSES) {
        printf("Process limit reached! Cannot create more.\n");
        return;
    }
    VirtualProcess* new_process = (VirtualProcess*)malloc(sizeof(VirtualProcess));
    strcpy(new_process->name, name);
    new_process->pid = process_count + 1;
    new_process->memory = memory;
    new_process->execution_time = execution_time;
    process_list[process_count++] = new_process;
    printf("Process '%s' created with PID %d.\n", name, new_process->pid);
}

void list_processes() {
    printf("\nActive Virtual Processes:\n");
    for (int i = 0; i < process_count; i++) {
        printf("PID: %d, Name: %s, Memory: %d MB, Execution Time: %d sec\n", 
               process_list[i]->pid, process_list[i]->name, process_list[i]->memory, process_list[i]->execution_time);
    }
}

void execute_processes() {
    printf("\nExecuting Virtual Processes:\n");
    for (int i = 0; i < process_count; i++) {
        printf("Executing process %s (PID %d)...\n", process_list[i]->name, process_list[i]->pid);
        sleep(process_list[i]->execution_time);
        printf("Process %s (PID %d) completed.\n", process_list[i]->name, process_list[i]->pid);
    }
}

void remove_process(int pid) {
    for (int i = 0; i < process_count; i++) {
        if (process_list[i]->pid == pid) {
            printf("Removing process %s (PID %d)...\n", process_list[i]->name, pid);
            free(process_list[i]);
            for (int j = i; j < process_count - 1; j++) {
                process_list[j] = process_list[j + 1];
            }
            process_list[--process_count] = NULL;
            return;
        }
    }
    printf("Process with PID %d not found.\n", pid);
}

# --------- Module 2: Machine Learning Prediction ---------
// Placeholder for future ML-based resource allocation and prediction implementation.
// In C, implementing ML requires integrating external libraries like TensorFlow C API or OpenCV.

# --------- Module 3: Real-Time Monitoring & Resource Allocation ---------
void monitor_resources() {
    printf("\nReal-Time Resource Monitoring:\n");
    for (int i = 0; i < process_count; i++) {
        printf("Process %s (PID %d): Memory Usage: %d MB\n", 
               process_list[i]->name, process_list[i]->pid, process_list[i]->memory);
    }
}

# --------- Execution Pipeline ---------
// Execution logic and pipeline to simulate an OS scheduler.

int main() {
    int choice, memory, execution_time, pid;
    char name[50];
    
    while (1) {
        printf("\nVirtual OS for Educational Simulations\n");
        printf("1. Create Process\n");
        printf("2. List Processes\n");
        printf("3. Execute Processes\n");
        printf("4. Remove Process\n");
        printf("5. Monitor Resources\n");
        printf("6. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);
        getchar();
        
        switch (choice) {
            case 1:
                printf("Enter process name: ");
                fgets(name, sizeof(name), stdin);
                name[strcspn(name, "\n")] = 0;
                printf("Enter memory allocation (MB): ");
                scanf("%d", &memory);
                printf("Enter execution time (sec): ");
                scanf("%d", &execution_time);
                create_process(name, memory, execution_time);
                break;
            case 2:
                list_processes();
                break;
            case 3:
                execute_processes();
                break;
            case 4:
                printf("Enter PID to remove: ");
                scanf("%d", &pid);
                remove_process(pid);
                break;
            case 5:
                monitor_resources();
                break;
            case 6:
                printf("Exiting Virtual OS Simulation.\n");
                for (int i = 0; i < process_count; i++) {
                    free(process_list[i]);
                }
                return 0;
            default:
                printf("Invalid choice!\n");
        }
    }
}

# --------- Appendix ---------
## A. AI-Generated Project Elaboration/Breakdown Report
### 1. Data Collection Module
- Monitors CPU, Memory, Disk, and Network Usage.
- Logs system metrics over time for analysis.
### 2. Machine Learning Module
- Processes data for model training.
- Predicts future resource utilization.
### 3. Data Visualization & Alert System
- Displays real-time usage & predictions.
- Alerts administrators on threshold breaches.
### 4. Data Storage and History Module
- Stores historical usage data.
- Enables long-term trend analysis.

## B. Problem Statement
**"Virtual Operating Systems for Educational Simulations"**
- Simulates OS behavior for educational purposes.
- Uses ML for predictive analytics in resource allocation.
- Ensures efficient simulation and learning environment.

## Future Enhancements
- Advanced ML & AI Integration.
- Cloud-Based Resource Management.
- Multi-cloud and Hybrid Cloud Support.
