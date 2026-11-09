
import json
import os

FILE_NAME = "students.json"


def load_students():
    if os.path.exists(FILE_NAME):
        try:
            with open(FILE_NAME, "r") as file:
                return json.load(file)
        except:
            return []
    return []


def save_students(students):
    with open(FILE_NAME, "w") as file:
        json.dump(students, file, indent=4)


def add_student(students):
    roll = input("Enter Roll Number: ")

    for student in students:
        if student["roll"] == roll:
            print("Roll Number Already Exists!")
            return

    name = input("Enter Student Name: ")
    course = input("Enter Course: ")

    try:
        marks = float(input("Enter Marks: "))
        if marks < 0 or marks > 100:
            print("Marks must be between 0 and 100.")
            return
    except ValueError:
        print("Please enter valid marks.")
        return

    student = {
        "roll": roll,
        "name": name,
        "course": course,
        "marks": marks
    }

    students.append(student)
    save_students(students)
    print("Student Added Successfully!")


def view_students(students):
    if not students:
        print("No Student Records Found!")
        return

    print("\n----- Student Records -----")

    for student in students:
        print("Roll Number:", student["roll"])
        print("Name:", student["name"])
        print("Course:", student["course"])
        print("Marks:", student["marks"])
        print("--------------------------")


def search_student(students):
    roll = input("Enter Roll Number to Search: ")

    for student in students:
        if student["roll"] == roll:
            print("\nStudent Found!")
            print("Name:", student["name"])
            print("Course:", student["course"])
            print("Marks:", student["marks"])
            return

    print("Student Not Found!")


def update_student(students):
    roll = input("Enter Roll Number to Update: ")

    for student in students:
        if student["roll"] == roll:
            student["name"] = input("Enter New Name: ")
            student["course"] = input("Enter New Course: ")

            try:
                marks = float(input("Enter New Marks: "))
                if marks < 0 or marks > 100:
                    print("Marks must be between 0 and 100.")
                    return
                student["marks"] = marks
            except ValueError:
                print("Invalid marks.")
                return

            save_students(students)
            print("Student Updated Successfully!")
            return

    print("Student Not Found!")


def delete_student(students):
    roll = input("Enter Roll Number to Delete: ")

    for student in students:
        if student["roll"] == roll:
            students.remove(student)
            save_students(students)
            print("Student Deleted Successfully!")
            return

    print("Student Not Found!")


def main():
    students = load_students()

    while True:
        print("\n===== STUDENT MANAGEMENT SYSTEM =====")
        print("1. Add Student")
        print("2. View Students")
        print("3. Search Student")
        print("4. Update Student")
        print("5. Delete Student")
        print("6. Exit")

        choice = input("Enter Your Choice: ")

        if choice == "1":
            add_student(students)

        elif choice == "2":
            view_students(students)

        elif choice == "3":
            search_student(students)

        elif choice == "4":
            update_student(students)

        elif choice == "5":
            delete_student(students)

        elif choice == "6":
            print("Thank You!")
            break

        else:
            print("Invalid Choice! Try Again.")


if __name__ == "__main__":
    main()
