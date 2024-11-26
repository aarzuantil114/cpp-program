#include <iostream>
using namespace std;
struct Process
{
    int pid;
    int arrival_time;
    int burst_time;
    int completion_time;
    int turn_around_time;
    int waiting_time;
};
void getCT(Process arr[], int n)
{
    arr[0].completion_time = arr[0].burst_time;
    for (int i = 1; i < n; i++)
    {
        arr[i].completion_time = arr[i - 1].completion_time + arr[i].burst_time;
    }
}
void getTAT(Process arr[], int n)
{
    for (int i = 0; i < n; i++)
    {
        arr[i].turn_around_time = arr[i].completion_time - arr[i].arrival_time;
    }
}
void getWT(Process arr[], int n)
{
    for (int i = 0; i < n; i++)
    {
        arr[i].waiting_time = arr[i].turn_around_time - arr[i].burst_time;
    }
}
void findFCFS(Process arr[], int n)
{
    getCT(arr, n);
    getTAT(arr, n);
    getWT(arr, n);
}
void display(Process arr[], int n)
{
    int count = 0;
    float wt = 0;
    float tat = 0;
    cout << "\t\t\t\tFCFS TABLE" << endl;
    cout << "Process ID   Arrival Time   Burst Time  Completion Time  Turn Around Time  Waiting Time" << endl;
    for (int i = 0; i < n; i++)
    {
        cout << arr[i].pid << "\t\t" << arr[i].arrival_time << "\t\t" << arr[i].burst_time << "\t\t" << arr[i].completion_time << "\t\t" << arr[i].turn_around_time << "\t\t" << arr[i].waiting_time << endl;
        count++;
        wt += arr[i].waiting_time;
        tat += arr[i].turn_around_time;
    }
    cout << "The average waiting time is " << (wt / count) << endl;
    cout << "The average turn around time is " << (tat / count) << endl;
}
void sortt(Process arr[], int n)
{
    for (int i = 0; i < n - 1; i++)
    {
        for (int j = 0; j < n - i - 1; j++)
        {
            if (arr[j].arrival_time > arr[j + 1].arrival_time)
            {
                swap(arr[j].arrival_time, arr[j + 1].arrival_time);
                swap(arr[j].burst_time, arr[j + 1].burst_time);
                swap(arr[j].pid, arr[j + 1].pid);
            }
        }
    }
}
int main()
{
    // int n = 5;
    // Process arr[n] = {{1, 0, 5}, {2, 1, 3}, {3, 2, 2}, {4, 3, 4}, {5, 4, 1}};
    int n;
    cout << "Enter the number of processes" << endl;
    cin >> n;
    Process arr[n];
    for (int i = 0; i < n; i++)
    {
        cout << "Enter the Process id,arrival time and burst time" << endl;
        cin >> arr[i].pid >> arr[i].arrival_time >> arr[i].burst_time;
    }
    sortt(arr, n);
    findFCFS(arr, n);
    display(arr, n);
}
