# NaesVladASSIGNMENT2
## How to run the system
The system runs by providing a menu of options to the user. The user selects an option, and the system performs the corresponding action. For example, if the user selects "Add a new student," the system prompts for the student's information and adds it to the database.
The system also has a feature that removes a student if necessary.

## Changes made to the code
The changes made are 
1. The "class Student" function had 2 jobs one being to give a way for student details to be added and a display student details task , but now there's a separate area in the code to handle the display student details job
2. An error handling feature was added for when someone puts in invalid information which the previous code did not
3. The options to be selected like "Add new student", "remove student", "update student" and "show all students" were added
4. Functionality was added to the options listed previously

## The Code

#adding student details

class Student:
    def __init__(self, id, name, age, major):
        self.__id = id
        self.__name = name
        self.__age = age
        self.__major = major

    @property
    def name(self):
        return self.__name

    @name.setter
    def name(self, new_name):

        self.__name = new_name

    def update_student(self, name=None, age=None, major=None):
        if name:
            self.__name = name
        if age:
            self.__age = age
        if major:
            self.__major = major

    def display_student(self):
        print(f"ID: {self.__id}, Name: {self.__name}, Age: {self.__age}, Major: {self.__major}")

#adding options to be chosen

class StudentRepository:
    def __init__(self):
        self.students = []

    def add_student(self, student):
        self.students.append(student)

    def remove_student(self, student_id):
        for i, student in enumerate(self.students):
            if student.id == student_id:
                del self.students[i]
                return
        print(f"Student with ID {student_id} not found.")

    def update_student_info(self, student_id, name=None, age=None, major=None):
        for student in self.students:
            if student.id == student_id:
                student.update_student(name, age, major)
                return
        print(f"Student with ID {student_id} not found.")

    def show_all_students(self):
        if not self.students:
            print("No students found.")
            return
        for student in self.students:
            student.display_student()

#adding functionality to the code

class StudentDatabase(StudentRepository):
    pass  

class StudentManagementSystem:
    def __init__(self):
        self.database = StudentDatabase()

    def display_menu(self):
        print("Student Management System")
        print("1. Add a new student")
        print("2. Remove a student")
        print("3. Update student information")
        print("4. Show all students")
        print("5. Exit")

    def run(self):
        while True:
            self.display_menu()
            choice = int(input("Enter your choice: "))

            if choice == 1:
                id = int(input("Enter student ID: "))
                name = input("Enter student name: ")
                age = int(input("Enter student age: "))
                major = input("Enter student major: ")
                self.database.add_student(Student(id, name, age, major))
                print("Student added successfully.")
            elif choice == 2:
                student_id = int(input("Enter student ID to remove: "))
                self.database.remove_student(student_id)
            elif choice == 3:
                student_id = int(input("Enter student ID to update: "))
                name = input("Enter new name (leave blank to keep current): ")
                age = input("Enter new age (leave blank to keep current): ")
                major = input("Enter new major (leave blank to keep current): ")
                self.database.update_student_info(student_id, name, age, major)
                print("Student information updated successfully.")
            elif choice == 4:
                self.database.show_all_students()
            elif choice == 5:
                print("Exiting the system...")
                break
            else:
                print("Invalid Entry. Please try again.")

#Example Usage
system = StudentManagementSystem()
system.run()
