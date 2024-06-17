import java.util.ArrayList;
import java.util.List;

class Process {
    private final String name;
    private final int arrivalTime;
    private final int burstTime;

    public Process(String name, int arrivalTime, int burstTime) {
        this.name = name;
        this.arrivalTime = arrivalTime;
        this.burstTime = burstTime;
    }

    public String getName() {
        return name;
    }

    public int getArrivalTime() {
        return arrivalTime;
    }

    public int getBurstTime() {
        return burstTime;
    }
}

public class FCFS {
    public static void main(String[] args) {
        List<Process> processes = new ArrayList<>();
        processes.add(new Process("P1", 0, 24));
        processes.add(new Process("P2", 0, 3));
        processes.add(new Process("P3", 0, 3));

        int totalProcesses = processes.size();
        int totalTime = 0;

        System.out.println("Process\tArrival Time\tBurst Time\tCompletion Time\tTurnaround Time\tWaiting Time");

        for (Process process : processes) {
            int completionTime = totalTime + process.getBurstTime();
            int turnaroundTime = completionTime - process.getArrivalTime();
            int waitingTime = turnaroundTime - process.getBurstTime();

            System.out.printf("%s\t\t%d\t\t\t%d\t\t\t%d\t\t\t%d\t\t\t%d%n",
                    process.getName(), process.getArrivalTime(), process.getBurstTime(),
                    completionTime, turnaroundTime, waitingTime);

            totalTime = completionTime;
        }

        double averageTurnaroundTime = processes.stream()
                .mapToInt(p -> p.getBurstTime())
                .average()
                .orElse(0);

        double averageWaitingTime = processes.stream()
                .mapToInt(p -> p.getBurstTime())
                .average()
                .orElse(0);

        System.out.println("\nAverage Turnaround Time: " + averageTurnaroundTime);
        System.out.println("Average Waiting Time: " + averageWaitingTime);
    }
}
