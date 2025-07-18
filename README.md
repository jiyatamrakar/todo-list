//todo list
import java.util.ArrayList;
import java.util.Scanner;

class Task {
    String title;
    boolean isDone;

    public Task(String title) {
        this.title = title;
        this.isDone = false;
    }

    public void markDone() {
        isDone = true;
    }

    public String toString() {
        return (isDone ? "[✓] " : "[ ] ") + title;
    }
}

class Main {
    private static ArrayList<Task> tasks = new ArrayList<>();

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int choice;

        do {
            System.out.println("\n===== TO-DO LIST MENU =====");
            System.out.println("1. Add Task");
            System.out.println("2. View Tasks");
            System.out.println("3. Mark Task as Completed");
            System.out.println("4. Delete Task");
            System.out.println("5. Exit");
            System.out.print("Choose an option: ");
            choice = sc.nextInt();
            sc.nextLine();  // consume newline

            switch (choice) {
                case 1:
                    System.out.print("Enter task title: ");
                    String title = sc.nextLine();
                    tasks.add(new Task(title));
                    System.out.println("Task added!");
                    break;

                case 2:
                    viewTasks();
                    break;

                case 3:
                    viewTasks();
                    System.out.print("Enter task number to mark as completed: ");
                    int doneIndex = sc.nextInt() - 1;
                    if (isValidIndex(doneIndex)) {
                        tasks.get(doneIndex).markDone();
                        System.out.println("Task marked as completed!");
                    } else {
                        System.out.println("Invalid task number.");
                    }
                    break;

                case 4:
                    viewTasks();
                    System.out.print("Enter task number to delete: ");
                    int delIndex = sc.nextInt() - 1;
                    if (isValidIndex(delIndex)) {
                        tasks.remove(delIndex);
                        System.out.println("Task deleted!");
                    } else {
                        System.out.println("Invalid task number.");
                    }
                    break;

                case 5:
                    System.out.println("Exiting... Thanks for using!");
                    break;

                default:
                    System.out.println("Invalid option. Try again.");
            }
        } while (choice != 5);
        sc.close();
    }

    private static void viewTasks() {
        if (tasks.isEmpty()) {
            System.out.println("No tasks added yet.");
            return;
        }
        System.out.println("\nYour To-Do List:");
        for (int i = 0; i < tasks.size(); i++) {
            System.out.println((i + 1) + ". " + tasks.get(i));
        }
    }

    private static boolean isValidIndex(int index) {
        return index >= 0 && index < tasks.size();
    }
}
