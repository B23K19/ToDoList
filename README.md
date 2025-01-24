
 To-Do List Console App in C#

A simple console App to-do list application built using C#..

 Features

- Add task 
- View task
- Remove task.
- Save and exit

You can add as many lists as you like


Code

using System;
using System.IO;
using System.Collections.Generic;

class ToDoList
{
    //declaring a private list to store tasks
     private static List<string> tasks = new List<string>();
    //file where the tasks will be saved
     private const string fileName = "tasks.txt";
    //Function to add tasks to the file
    static void AddTask()
    {
        Console.WriteLine("Enter the task:");
        string task = Console.ReadLine();
        tasks.Add(task);
        Console.WriteLine("Task added.");

    }
    //function to view the task in the file
    static void ViewTask()
    {
        if(tasks.Count == 0)
        {
            Console.WriteLine("No task available.");
        }
        else
        {
            Console.WriteLine("Your Task : ");
            for(int i=0; i < tasks.Count; i++)
            {
                Console.WriteLine($"{i + 1}.{tasks[i]}");
            }
        }
    }
    //function to remove tasks from the file
    static void RemoveTask()
    {
        ViewTask();
        if(tasks.Count > 0)
        {
            Console.WriteLine("Enter the number of the task to remove: ");
            string pass = Console.ReadLine();
            //converting user input to int and checking few conditions
            if(int.TryParse(pass,out int taskNumber)&& taskNumber > 0 && taskNumber<=tasks.Count)
            {
                tasks.RemoveAt(taskNumber - 1);
                Console.WriteLine("Task removed");
            }
            else
            {
                Console.WriteLine("Invalid task number.");
            }
        }
    }
    //function to save tasks to the file
    static void SaveTasks()
    {
        File.WriteAllLines(fileName,tasks);
    }
    //function to load tasks from the file
    static void LoadTask()
    {
        if(File.Exists(fileName))
        {
            //load task from the list
            tasks = new List<string>(File.ReadAllLines(fileName));
        }
    }



    static void Main(string[] args)
    {
        LoadTask();
        string choice;

        do
        {
            Console.WriteLine("\n\t\t\t_______To-Do List_______\n"); 
            Console.WriteLine("1.Add a task");
            Console.WriteLine("2.View tasks");
            Console.WriteLine("3.Remove task");
            Console.WriteLine("4.Save and exit");

            Console.WriteLine("Choose an option: ");
            choice = Console.ReadLine();
            //compare 
            switch(choice)
            {
                case "1":
                    AddTask();
                    break;
                case "2":
                    ViewTask();
                    break;
                case "3":
                    RemoveTask();
                    break;
                case "4":
                    SaveTasks();
                    Console.WriteLine("Tasks saved.");
                    break;
                default:
                    Console.WriteLine("Invalid choice.Please try again");
                    break;

            }
        }while(choice != "4");
    }
}
/*another program that show removed data and can restore them*/
