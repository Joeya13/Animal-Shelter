class Animal:
    def __init__(self, age, name, species, weight_kg):
        self.age = age
        self.name = name
        self.species = species
        self.weight_kg = weight_kg

    def __str__(self):
        return f"Age: {self.age}, Name: {self.name}, Species: {self.species}, Weight: {self.weight_kg} kg"

class AnimalShelter:
    def __init__(self):
        self.animals = []
        self.current_index = -1

    def add_animal(self, animal):
        self.animals.append(animal)
        print(f"Animal {animal.name} added.")

    def remove_animal(self, name):
        self.animals = [animal for animal in self.animals if animal.name != name]
        print(f"Animal with name {name} removed.")

    def modify_animal(self, name, new_name=None, species=None, age=None, weight_kg=None):
        for animal in self.animals:
            if animal.name == name:
                if new_name:
                    animal.name = new_name
                if species:
                    animal.species = species
                if age:
                    animal.age = age
                if weight_kg:
                    animal.weight_kg = weight_kg
                print(f"Animal with name {name} modified.")
                return
        print(f"Animal with name {name} not found.")

    def sort_animals(self, key):
        self.animals.sort(key=lambda animal: getattr(animal, key))
        print(f"Animals sorted by {key}.")

    def lookup_animal(self, name):
        for animal in self.animals:
            if animal.name == name:
                return animal
        return None

    def print_animals(self):
        for animal in self.animals:
            print(animal)

    def next_animal(self):
        if self.current_index < len(self.animals) - 1:
            self.current_index += 1
            print(self.animals[self.current_index])
        else:
            print("No more animals.")

    def previous_animal(self):
        if self.current_index > 0:
            self.current_index -= 1
            print(self.animals[self.current_index])
        else:
            print("No previous animals.")

# Example usage
shelter = AnimalShelter()

print("Hello! Welcome to the Animal Shelter Management System.")
while True:
    print("\nWhat would you like to do today? Options: add, remove, modify, sort, lookup, print, next, previous, exit")
    choice = input("Enter your choice: ").strip().lower()

    if choice == "add":
        age = int(input("Enter age: "))
        name = input("Enter name: ")
        species = input("Enter species: ")
        weight_kg = float(input("Enter weight (kg): "))
        shelter.add_animal(Animal(age, name, species, weight_kg))

    elif choice == "remove":
        print("\nCurrent animals:")
        shelter.print_animals()
        name = input("Enter name of the animal to remove: ")
        shelter.remove_animal(name)

    elif choice == "modify":
        print("\nCurrent animals:")
        shelter.print_animals()
        name = input("Enter name of the animal to modify: ")
        new_name = input("Enter new name (leave blank to keep current): ")
        species = input("Enter new species (leave blank to keep current): ")
        age = input("Enter new age (leave blank to keep current): ")
        weight_kg = input("Enter new weight (kg) (leave blank to keep current): ")
        shelter.modify_animal(name, new_name or None, species or None, int(age) if age else None, float(weight_kg) if weight_kg else None)

    elif choice == "sort":
        key = input("Enter attribute to sort by (age, name, species, weight_kg): ").strip().lower()
        shelter.sort_animals(key)

    elif choice == "lookup":
        name = input("Enter name to lookup: ")
        animal = shelter.lookup_animal(name)
        if animal:
            print(animal)
        else:
            print("Animal not found.")

    elif choice == "print":
        shelter.print_animals()

    elif choice == "next":
        shelter.next_animal()

    elif choice == "previous":
        shelter.previous_animal()

    elif choice == "exit":
        print("Thank you! Have a great day!")
        break

    else:
        print("Invalid choice. Please try again.")
