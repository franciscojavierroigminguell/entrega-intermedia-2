Clase Task (para representar una tarea)

// Task.h
#ifndef TASK_H
#define TASK_H

#include <string>

class Task {
private:
    std::string title;
    std::string description;
    std::string dueDate;
    bool completed;

public:
    Task(const std::string& title, const std::string& description, const std::string& dueDate);
    
    // Getters y Setters
    std::string getTitle() const;
    void setTitle(const std::string& title);
    
    std::string getDescription() const;
    void setDescription(const std::string& description);
    
    std::string getDueDate() const;
    void setDueDate(const std::string& dueDate);
    
    bool isCompleted() const;
    void markAsCompleted();
    
    // Métodos adicionales
    void displayTask() const;
};

#endif

Clase TaskManager (para gestionar un conjunto de tareas)

// TaskManager.h
#ifndef TASKMANAGER_H
#define TASKMANAGER_H

#include <vector>
#include "Task.h"

class TaskManager {
private:
    std::vector<Task> tasks;

public:
    // Funciones para gestionar tareas
    void addTask(const Task& task);
    void removeTask(const std::string& title);
    void listTasks() const;
    void saveTasksToFile(const std::string& filename) const;
    void loadTasksFromFile(const std::string& filename);
};

#endif

Función Principal (main.cpp)

// main.cpp
#include <iostream>
#include "TaskManager.h"

int main() {
    TaskManager taskManager;
    taskManager.loadTasksFromFile("tasks.txt");
    
    int choice;
    do {
        std::cout << "1. Add Task\n2. Remove Task\n3. List Tasks\n4. Save and Exit\n";
        std::cin >> choice;

        switch (choice) {
            case 1: {
                std::string title, description, dueDate;
                std::cout << "Enter title: ";
                std::cin >> title;
                std::cout << "Enter description: ";
                std::cin >> description;
                std::cout << "Enter due date: ";
                std::cin >> dueDate;
                
                Task task(title, description, dueDate);
                taskManager.addTask(task);
                break;
            }
            case 2: {
                std::string title;
                std::cout << "Enter title of task to remove: ";
                std::cin >> title;
                taskManager.removeTask(title);
                break;
            }
            case 3:
                taskManager.listTasks();
                break;
            case 4:
                taskManager.saveTasksToFile("tasks.txt");
                std::cout << "Tasks saved. Exiting.\n";
                break;
            default:
                std::cout << "Invalid option.\n";
        }
    } while (choice != 4);
