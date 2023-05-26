//2nd term project EMPLOYEE RECORD SYSTEM 04-15-23

//PREPROCESSOR DECLARATION
#include <stdio.h>
#include <string.h>
#include <stdlib.h>

#define MAX_EMPLOYEE 100

//STRUCTURE DECLARATION WITH A MEMBERS OF ID,NAME,POSITION,SALARY,DEPARTMENT
//structure for storing employee information
struct Employee{
    int id;
    char name[999];
    char department[999];
    char position[999];
    float salary;

};
//FUNCTION DECLARATION
void toLowerCase(char* str);

void addEmployee(struct Employee *employees, int *numEmployees);
// This function adds a new employee to the array of employees.

void deleteEmployee(struct Employee *employees, int *numEmployees);
//This function deletes an existing employee from the array of employees.

void viewEmployees(struct Employee *employees, int numEmployees);
// This function displays the details of all employees.

void searchEmployee(struct Employee *employees, int numEmployees);
// This function searches for an employee based on certain criteria.

void editEmployee(struct Employee *employees, int numEmployees);
 // This function allows editing the details of an existing employee.

void printIntroduction();
void printEmployeeRecordSystem();
void viewDisplay();

int findEmployeeIndexByID(struct Employee *employees, int numEmployees, int id);
// This function finds the index of an employee with the given ID in the array of employees.

int findEmployeeIndexByName(struct Employee *employees, int numEmployees, const char *name);
// This function finds the index of an employee with the given name in the array of employees.

void printEmployeeDetails(struct Employee employee);
void shiftEmployees(struct Employee *employees, int numEmployees, int startIndex);
// This function shifts the positions of employees in the array to fill any gaps left by deleted employees.


//MAIN FUNCTION
int main()
{

        struct Employee employees[50];      //Initialize an array of Employee structures with a maximum capacity of 50 employees.
        int numEmployees = 0;               //Initialize the number of employees to 0, indicating that there are currently no employees.
        int choice;                         //Declare a variable 'choice' to store the user's input for menu selection.

        printIntroduction();

        system("cls");                      //clear the screen

do
    {
    system("cls");
    printEmployeeRecordSystem();
    printf("\n\n\n\n\n\n\n\n\n");
    printf("                                                                          MENU                        \n");
    printf("\n                                                            +-----------------------------+");
    printf("\n                                                            | 1.ADD EMPLOYEE              |");
    printf("\n                                                            | 2.DELETE EMPLOYEE           |");
    printf("\n                                                            | 3.VIEW EMPLOYEE             |");
    printf("\n                                                            | 4.SEARCH EMPLOYEE           |");
    printf("\n                                                            | 5.EDIT EMPLOYEE             |");
    printf("\n                                                            | 6.Exit                      |");
    printf("\n                                                            +-----------------------------+\n");
    printf("\n\n                                                           Enter choice (1-5): ");
    scanf("%d", &choice);

    switch (choice)
        {
    case 1:
        addEmployee(employees, &numEmployees);          // Call the 'addEmployee()' function to add a new employee.
        break;
    case 2:
        deleteEmployee(employees, &numEmployees);       // Call the 'deleteEmployee()' function to delete an existing employee.
        break;
    case 3:
        viewEmployees(employees, numEmployees);         // Call the 'viewEmployees()' function to display the details of all employees.
        break;
    case 4:
        searchEmployee(employees, numEmployees);        // Call the 'searchEmployee()' function to search for an employee.
        break;
    case 5:
        editEmployee(employees, numEmployees);          // Call the 'editEmployee()' function to edit the details of an existing employee.
    case 6:
    printf("\n                                                             Exiting...\n");
    getchar();
    getchar();
    break;
    default:
    printf("\n                                                           Invalid choice. Try again.\n");
    getchar();
    getchar();
            }
    } while (choice != 6);                              // Code to be executed repeatedly until 'choice' is equal to 6.


    return 0;
}
//FUNCTION FOR ADDING A EMPLOYEE
void addEmployee(struct Employee *employees, int *numEmployees) {
    system("cls");
    struct Employee newEmployee;
    int idTaken;

    printf("\n                                     +=========================================================================+");
    printf("\n                                     |                                                                         |");
    printf("\n                                     |                                                                         |");
    printf("\n                                     |                          PLEASE ADD A EMPLOYEE                          |");
    printf("\n                                     |                                                                         |");
    printf("\n                                     |                                                                         |");
    printf("\n                                     +=========================================================================+");
    do {
    printf("\n\n\n\n\n\n\n\n\n");
    printf("                                       Enter employee ID: ");
        scanf("%d", &newEmployee.id);

        idTaken = 0;

        for (int i = 0; i < *numEmployees; i++) {
            if (employees[i].id == newEmployee.id) {
                idTaken = 1;
                break;
            }
        }

        if (idTaken) {
    printf("\n                                       ID is already in use. \nPlease enter a different ID.");
        }
    } while (idTaken);

    printf("\n                                       Enter employee name: ");
    scanf(" %[^\n]s", newEmployee.name);
    toLowerCase(newEmployee.name);

    printf("\n                                       Enter employee department: ");
    scanf(" %[^\n]s", newEmployee.department);
    toLowerCase(newEmployee.department);

    printf("\n                                       Enter employee position: ");
    scanf(" %[^\n]s", newEmployee.position);
    toLowerCase(newEmployee.position);

    printf("\n                                       Enter employee salary: ");
    scanf("%f", &newEmployee.salary);

    employees[*numEmployees] = newEmployee;
    (*numEmployees)++;

    printf("\n                                       Employee added successfully.");
    printf("\n                                       Do you want to enter another employee? (Y/N): ");
    char choice;
    scanf(" %c", &choice);

    if (choice == 'Y' || choice == 'y') {
        addEmployee(employees, numEmployees);
    } else {
        printf("\n\n                                   Press Enter to continue...");
        getchar();
    }
}
//FUNCTION FOR SEARCHING AN EMPLOYEE
void searchEmployee(struct Employee* employees, int numEmployees) {
    int choice;                 // Variable to store the user's choice for the search method.
    char searchString[50];      // Array to store the search string entered by the user.
    int found = 0;              // Variable to track whether an employee matching the search criteria is found.
    int searchID;               // Variable to store the employee ID entered for searching.
    float minSalary;            // Variable to store the minimum salary entered for searching.
    system("cls");
    printf("\n                                     +=========================================================================+");
    printf("\n                                     |                                                                         |");
    printf("\n                                     |                                                                         |");
    printf("\n                                     |                          PLEASE SEARCH THE EMPLOYEE                     |");
    printf("\n                                     |                                                                         |");
    printf("\n                                     |                                                                         |");
    printf("\n                                     +=========================================================================+\n");
    printf("                                       Search Employee by:\n");
    printf("                                       1. Name\n");
    printf("                                       2. ID\n");
    printf("                                       3. Position\n");
    printf("                                       4. Salary\n");
    printf("                                       5. Department\n");
    printf("                                       Enter your choice: ");
    scanf("%d", &choice);

    switch (choice) {
        case 1:
            printf("\n                             Enter the name of the employee to search for: ");
            scanf(" %[^\n]s", searchString);
            toLowerCase(searchString);
            getchar();
            break;
        case 2:
            printf("\n                             Enter the ID of the employee to search for: ");
            scanf("%d", &searchID);
            getchar();
            break;
        case 3:
            printf("\n                             Enter the position of the employee to search for: ");
            scanf(" %[^\n]s", searchString);
            toLowerCase(searchString);
            getchar();
            break;
        case 4:
            printf("\n                             Enter the minimum salary: ");
            scanf("%f", &minSalary);
            getchar();
            break;
        case 5:
            printf("\n                             Enter the department of the employee to search for: ");
            scanf(" %[^\n]s", searchString);
            toLowerCase(searchString);
            getchar();
            break;
        default:
            printf("\nInvalid choice.\n");
            return;
    }
    for (int i = 0; i < numEmployees; i++) {
        struct Employee currentEmployee = employees[i];
        switch (choice) {
            case 1: // Search by Name
                if (strcasecmp(currentEmployee.name, searchString) == 0) {
                    printEmployeeDetails(currentEmployee);
                    found = 1;
                    break;
                }
                break;
            case 2: // Search by ID
                if (currentEmployee.id == searchID) {
                    printEmployeeDetails(currentEmployee);
                    found = 1;
                    break;
                }
                break;
            case 3: // Search by Position
                if (strcasecmp(currentEmployee.position, searchString) == 0) {
                    printEmployeeDetails(currentEmployee);
                    found = 1;
                    break;
                }
                break;
            case 4: // Search by Salary
                if (currentEmployee.salary >= minSalary) {
                    printEmployeeDetails(currentEmployee);
                    found = 1;
                    break;
                }
                break;
            case 5: // Search by Department
                if (strcasecmp(currentEmployee.department, searchString) == 0) {
                    printEmployeeDetails(currentEmployee);
                    found = 1;
                    break;
                }
                break;
            default:
                break;
        }
    }

    if (!found) {
        printf("\n                                   No employees found matching the search criteria.\n");
    }
            getchar();
}
//FUNCTION FOR DELETING A EMPLOYEE
void deleteEmployee(struct Employee *employees, int *numEmployees){
                    system("cls");

    printf("\n                                     +=========================================================================+");
    printf("\n                                     |                                                                         |");
    printf("\n                                     |                                                                         |");
    printf("\n                                     |                              DELETE EMPLOYEE                            |");
    printf("\n                                     |                                                                         |");
    printf("\n                                     |                                                                         |");
    printf("\n                                     +=========================================================================+");

    printf("\n\n\n\n\n\n\n\n\n");
    printf("                                       Delete an Employee\n");
    printf("                                       --------------------\n");
    printf("                                       1. Delete by ID\n");
    printf("                                       2. Delete by Name\n");
    printf("                                       --------------------\n");
    printf("                                       Enter choice (1-2): ");

    /* Comment: This code snippet handles the deletion of an employee based on the user's choice.
    It prompts the user to enter either the ID or the name of the employee to be deleted and performs the deletion accordingly.*/

    int choice;
    scanf("%d", &choice);

    if (choice == 1) {
    int deleteID;
    int found = 0;

    do {
    printf("\n                                       Enter ID of the employee to delete: ");
    scanf("%d", &deleteID);

    // Find the employee index by ID
    int employeeIndex = findEmployeeIndexByID(employees, *numEmployees, deleteID);

    if (employeeIndex != -1) {
    // Display employee record
    printf("                                         Employee Information:\n");
    printEmployeeDetails(employees[employeeIndex]);

    // Confirm deletion
    char confirmation;
    printf("\n                                       Are you sure you want to delete this employee? (Y/N): ");
                                scanf(" %c", &confirmation);

                                if (confirmation == 'Y' || confirmation == 'y') {
                                    // Shift remaining employees to fill the gap
                                    shiftEmployees(employees, *numEmployees, employeeIndex);

                                    (*numEmployees)--;

                                    found = 1;

    printf("\n                                       Employee deleted successfully.\n");
                                } else {
    printf("\n                                       Deletion canceled.\n");
                                    return;
                                }
                            } else {
    printf("\n                                       Employee with ID %d not found.\n", deleteID);

                                char tryAgain;
    printf("\n                                       Do you want to enter the ID again? (Y/N): ");
                                scanf(" %c", &tryAgain);

                                if (tryAgain == 'N' || tryAgain == 'n') {
                                    break;
                                }
                            }
                        } while (!found);
                    } else if (choice == 2) {

                        char deleteName[999];
                        int found = 0;

                        do {
    printf("\n                                        Enter the name of the employee to delete: ");
                            scanf(" %[^\n]s", deleteName);

                            // Find the employee index by name
                            int employeeIndex = findEmployeeIndexByName(employees, *numEmployees, deleteName);

                            if (employeeIndex != -1) {
                                // Display employee record
    printf("\n                                        Employee Information:\n");
                                printEmployeeDetails(employees[employeeIndex]);

                                // Confirm deletion
                                char confirmation;
    printf("\n                                        Are you sure you want to delete this employee? (Y/N): ");
                                scanf(" %c", &confirmation);

                                if (confirmation == 'Y' || confirmation == 'y') {
                                    // Shift remaining employees to fill the gap
                                    shiftEmployees(employees, *numEmployees, employeeIndex);

                                    (*numEmployees)--;

                                    found = 1;

    printf("\n                                        Employee deleted successfully.\n");
                                } else {
    printf("\n                                        Deletion canceled.\n");
                                    return;
                                }
                            } else {
    printf("\n                                        Name %s not found.\n", deleteName);

                                char tryAgain;
    printf("\n                                        Do you want to enter the name again? (Y/N): ");
                                scanf(" %c", &tryAgain);

                                if (tryAgain == 'N' || tryAgain == 'n') {
                                    break;
                                }
                            }
                        } while (!found);
                    } else {
    printf("\n                                        Invalid choice. Please try again.\n");
                    }

    printf("\n                                        Press Enter to continue...");
                    getchar();
                    getchar();
                }
//FUNCTION FOR VIEWING AN EMPLOYEE
void viewEmployees(struct Employee *employees, int numEmployees){

    system("cls");
    viewDisplay();



    if (numEmployees == 0)
    {
    printf("\n\n\n\n\n\t\t\t\t\t\tNo employees found.\n");
    printf("\n\t\t\t\t\t\tPress enter to continue...");
    getchar();
    getchar();
    return;
    }

    int currentPage = 1;
    int totalPages = (numEmployees + 9) / 10; // Calculate the total number of pages

    while (1)
    {
    system("cls");
    viewDisplay();


    printf("\n\n\n\n\n");
    printf("                                 +----------------------------------------------------------------------------------\n");
    printf("                                  %-12s | %-15s | %-15s | %-15s | %-10s   \n", "Employee ID", "Name", "Department", "Position", "Salary\n");
    printf("                                 -----------------------------------------------------------------------------------\n");
    /* This code calculates the starting index of employees for a specific page in a pagination system.
    Assuming each page displays 10 employees, the currentPage variable represents the current page number.*/
    int startIndex = (currentPage - 1) * 10;

    int endIndex = startIndex + 9;
    // Comment: This code snippet calculates the ending index of employees for a specific page in a pagination system.
    // Assuming each page displays 10 employees, the startIndex represents the starting index of the employees on the current page.

    if (endIndex >= numEmployees)
        {
        endIndex = numEmployees - 1;
        }
    //If the endIndex is greater than or equal to numEmployees, it is adjusted to be the last valid index in the array, which is numEmployees - 1.
    //This ensures that the range of employees to display on the current page does not exceed the available number of employees.

    for (int i = startIndex; i <= endIndex; i++) {
    printf("\n                                  %-12d | %-15s | %-15s | %-15s | $%-9.2f |\n", employees[i].id, employees[i].name, employees[i].department, employees[i].position, employees[i].salary);
    }

    printf("\n                                 -----------------------------------------------------------------------------------\n");

    printf("\n                                                               Page %d of %d\n", currentPage, totalPages);
    printf("\n                                                           1. Next Page\n");
    printf("                                                             2. Previous Page\n");
    printf("                                                             3. Back to Main Menu\n");
    printf("\n                                                           Enter choice (1-3): ");

                                int choice;
                                scanf("%d", &choice);

                                if (choice == 1) {
                                    if (currentPage < totalPages) {
                                        currentPage++;
                                    } else {
                                        printf("\n\t\t\t\t\tYou have reached the end of the record system.\n");
                                        printf("\n\t\t\t\t\tPress enter to continue...");
                                getchar();
                                getchar();

                                    }
                                } else if (choice == 2) {
                                    if (currentPage > 1) {
                                        currentPage--;
                                    } else {
                                        printf("\n\t\t\t\t\tYou are already at the beginning of the record system.\n");
                                        printf("\n\t\t\t\t\tPress enter to continue...");
                                getchar();
                                getchar();
                                    }
                                } else if (choice == 3) {
                                    break;
                                } else {
                                    printf("\n\t\t\t\t\tInvalid choice. Please try again.\n");
                                }


                            }
                            printf("\n\t\t\t\t\tPress enter to continue...");
                                getchar();
                                getchar();
                        }
//FUNCTION FOR EDITTING DETAILS OF AN EMPLOYEE
void editEmployee(struct Employee *employees, int numEmployees) {
    system("cls");

    printf("\n                                     +=========================================================================+");
    printf("\n                                     |                                                                         |");
    printf("\n                                     |                                                                         |");
    printf("\n                                     |                          EDIT YOUR EMPLOYEE INFO                        |");
    printf("\n                                     |                                                                         |");
    printf("\n                                     |                                                                         |");
    printf("\n                                     +=========================================================================+");
    if (numEmployees == 0) {
    printf("\n                                     +=========================================================================+");
    printf("\n                                     |                           No employees found.                           |");
    printf("\n                                     |                         Press enter to continue...                      |");
    printf("\n                                     +=========================================================================+");
        getchar();
        getchar();
        return;
    }

    int id;
    printf("\n\n\n\n\n\n\n\n\n");
    printf("\n                                                             Enter Employee ID to edit:");
    scanf("%d", &id);
    getchar();



    int index = findEmployeeIndexByID(employees, numEmployees, id);
    if (index == -1) {
    printf("\n                                     +=========================================================================+");
    printf("\n                                     |                          Employee not found.                            |");
    printf("\n                                     |                       Press enter to continue...                        |");
    printf("\n                                     +=========================================================================+");
        getchar();
        getchar();
        return;
    }

    printf("\n                                     +=========================================================================+");
    printf("\n                                     |                              Edit Menu                                  |");
    printf("\n                                     +=========================================================================+");
    printf("\n                                     |                                                                         |");
    printf("\n                                     |                           1. Edit Name                                  |");
    printf("\n                                     |                           2. Edit Position                              |");
    printf("\n                                     |                           3. Edit Department                            |");
    printf("\n                                     |                           4. Edit Salary                                |");
    printf("\n                                     |                           5. Cancel                                     |");
    printf("\n                                     |                                                                         |");
    printf("\n                                     +=========================================================================+");
    printf("\n\n                                                        Enter choice (1-5):");

    int choice;
    scanf("%d", &choice);

    switch (choice) {
        case 1: {
    printf("\n                                     +=========================================================================+");
    printf("\n                                                          Enter new name: ");
            getchar();  // Consume newline character
            fgets(employees[index].name, sizeof(employees[index].name), stdin);
// The code reads a line of input from the user for the name field of an employee and removes the trailing newline character.
/*The fgets() function is used to read input from stdin (standard input) and store it in the name field of the employee at the given
 index. The sizeof(employees[index].name) argument specifies the maximum number of characters to read, ensuring that
 it doesn't exceed the size of the name field.*/
 /*After reading the input, the strcspn() function is used to find the position of the newline character ('\n') in the name string.
 The strcspn() function returns the length of the initial segment of the string that does not contain any of the characters specified
  in the second argument (in this case, just '\n').*/
            employees[index].name[strcspn(employees[index].name, "\n")] = '\0';
/*The obtained index of the newline character is then used to replace it with a null character ('\0').
This effectively removes the newline
character from the name string, ensuring that it doesn't interfere with further processing or display.*/
    printf("\n                                                          Name updated successfully.\n");
    printf("\n                                     +=========================================================================+");
            break;
        }
        case 2: {
    printf("\n                                     +=========================================================================+");
    printf("\n                                                          Enter new position: ");
            getchar();  // Consume newline character
            fgets(employees[index].position, sizeof(employees[index].position), stdin);
            employees[index].position[strcspn(employees[index].position, "\n")] = '\0';
    printf("\n                                                          Position updated successfully.\n");
    printf("\n                                     +=========================================================================+");
            break;
        }
        case 3: {
    printf("\n                                     +=========================================================================+");
    printf("\n                                                          Enter new department: ");
            getchar();  // Consume newline character
            fgets(employees[index].department, sizeof(employees[index].department), stdin);
            employees[index].department[strcspn(employees[index].department, "\n")] = '\0';
    printf("\n                                                          Department updated successfully.\n");
    printf("\n                                     +=========================================================================+");
            break;
        }
        case 4: {
            printf("\n                             +=========================================================================+");
            printf("\n                                                Enter new salary: ");
            scanf("%f", &employees[index].salary);
            printf("\n                                                Salary updated successfully.\n");
            printf("\n                             +=========================================================================+");
            break;
        }
        case 5:
            printf("\n                             +=========================================================================+");
            printf("\n                                                Editing canceled.\n");
            break;
        default:
            printf("\n                                                Invalid choice. Editing canceled.\n");
            printf("\n                             +=========================================================================+");
            break;
    }

    printf("\n                                                         Press enter to continue...");
    getchar();
    getchar();
}
void printIntroduction() {
    printf("\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n");
    printf("\n                                             **-**-**-**-**-**-**-**-**-**-**-**-**-**-**-**-**-**-**\n");
    printf("\n                                                   =-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=");
    printf("\n                                                   =                  WELCOME                  =");
    printf("\n                                                   =                    TO                     =");
    printf("\n                                                   =               Employee Record             =");
    printf("\n                                                   =                 MANAGEMENT                =");
    printf("\n                                                   =                   SYSTEM                  =");
    printf("\n                                                   =-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=\n");
    printf("\n                                             **-**-**-**-**-**-**-**-**-**-**-**-**-**-**-**-**-**-**\n");
    printf("\n                                                     2nd term project EMPLOYEE RECORD SYSTEM                  ");
    printf("\n                                                                   04-15-23\n                                 ");
    printf("\n                                                              Developed by: GROUP 2                           ");

    printf("\n\n                                                           Press enter to proceed...                        ");
    getchar();
}
void printEmployeeRecordSystem() {

    printf("\n                                     +=========================================================================+");
    printf("\n                                     |                                                                         |");
    printf("\n                                     |                                                                         |");
    printf("\n                                     |                          EMPLOYEE RECORD SYSTEM                         |");
    printf("\n                                     |                                                                         |");
    printf("\n                                     |                                                                         |");
    printf("\n                                     +=========================================================================+");

}
/*// Comment: This code  defines a function findEmployeeIndexByID that searches for an employee in the employees array based
on their ID. It takes the array of employees, the number of employees (numEmployees), and the ID of the employee to search for (id)
as input parameters.*/
int findEmployeeIndexByID(struct Employee *employees, int numEmployees, int id) {
    for (int i = 0; i < numEmployees; i++)
        {
        if (employees[i].id == id) {
            return i;  // Found employee, return index
        }
    }
    return -1;  // Employee not found, return -1
}
int findEmployeeIndexByName(struct Employee *employees, int numEmployees, const char *name) {

    /*  This code searches for an employee in the employees array based on their name.
    It iterates over the array elements and compares the name field of each employee with the given name using the strcmp function.
    If a match is found, it returns the index of the employee.
    If no match is found after iterating through all employees, it returns -1 to indicate that the employee was not found*/
    for (int i = 0; i < numEmployees; i++) {
        if (strcmp(employees[i].name, name) == 0)   // Code to be executed if the names match
            {
            return i;                               // Found employee, return index
        }
    }
    return -1;                                      // Employee not found, return -1
}
void printEmployeeDetails(struct Employee employee) {
    printf("\n\t\t\t\t\t\t\t\tID: %d\n", employee.id);
    printf("\t\t\t\t\t\t\t\tName: %s\n", employee.name);
    printf("\t\t\t\t\t\t\t\tDepartment: %s\n", employee.department);
    printf("\t\t\t\t\t\t\t\tPosition: %s\n", employee.position);
    printf("\t\t\t\t\t\t\t\tSalary: %.2f\n", employee.salary);
}
void shiftEmployees(struct Employee *employees, int numEmployees, int startIndex) {

    /* Comment: This code snippet shifts the elements of the employees array to the left starting from the startIndex up to numEmployees - 1.
     It effectively removes an element from the array by overwriting it with the next element in the array.*/
    for (int i = startIndex; i < numEmployees - 1; i++) {
        employees[i] = employees[i + 1];// Shift elements to the left
        /*After this loop, the element at index startIndex will be replaced with the element that was originally at
        index startIndex + 1, and so on, effectively removing the element at startIndex from the array.*/
    }
}
void toLowerCase(char* str) {

                /*This code iterates over each character of the string until it encounters the null character ('\0'),
            which indicates the end of the string. The loop continues as long as the current character is not equal to '\0'*/
    for (int i = 0; str[i] != '\0'; i++) // Code to be executed for each character of the string
    {
        if (str[i] >= 'A' && str[i] <= 'Z') // Code to be executed if the character is an uppercase letter
            {
            str[i] = str[i] + 32;       // Convert uppercase letter to lowercase
        }
    }
}
void viewDisplay(){
    printf("\n                                     +=========================================================================+");
    printf("\n                                     |                                                                         |");
    printf("\n                                     |                                                                         |");
    printf("\n                                     |                          VIEW YOUR EMPLOYEE INFO                        |");
    printf("\n                                     |                                                                         |");
    printf("\n                                     |                                                                         |");
    printf("\n                                     +=========================================================================+");

}

