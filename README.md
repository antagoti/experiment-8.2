# experiment-8.2
exp8.2
Design and implement a hash table of fixed size. Use the division method for the hash function 
and resolve collisions using linear probing. Allow the user to perform the following operations: 
• Insert a key 
• Search for a key  
• Delete a key  
• Display the table 

class HashTable:
    def __init__(self, size):
        self.size = size
        self.table = [None] * size

    def hash_function(self, key):
        """Division method"""
        return key % self.size

    def insert(self, key):
        """Insert a key into the hash table"""
        index = self.hash_function(key)
        original_index = index
        while self.table[index] is not None and self.table[index] != "DELETED":
            index = (index + 1) % self.size
            if index == original_index:  # Table full
                print(" Hash Table is full. Cannot insert key:", key)
                return
        self.table[index] = key
        print(f" Key {key} inserted at index {index}")

    def search(self, key):
        """Search for a key"""
        index = self.hash_function(key)
        original_index = index
        while self.table[index] is not None:
            if self.table[index] == key:
                print(f" Key {key} found at index {index}")
                return
            index = (index + 1) % self.size
            if index == original_index:
                break
        print(f" Key {key} not found.")

    def delete(self, key):
        """Delete a key"""
        index = self.hash_function(key)
        original_index = index
        while self.table[index] is not None:
            if self.table[index] == key:
                self.table[index] = "DELETED"
                print(f" Key {key} deleted from index {index}")
                return
            index = (index + 1) % self.size
            if index == original_index:
                break
        print(f" Key {key} not found for deletion.")

    def display(self):
        """Display the entire hash table"""
        print("\n Current Hash Table:")
        for i, val in enumerate(self.table):
            print(f"Index {i}: {val}")
        print()


# --- Main Program ---
if __name__ == "__main__":
    size = int(input("Enter the size of hash table: "))
    ht = HashTable(size)

    while True:
        print("\n--- MENU ---")
        print("1. Insert a key")
        print("2. Search for a key")
        print("3. Delete a key")
        print("4. Display table")
        print("5. Exit")

        choice = input("Enter your choice (1-5): ")

        if choice == '1':
            key = int(input("Enter key to insert: "))
            ht.insert(key)
        elif choice == '2':
            key = int(input("Enter key to search: "))
            ht.search(key)
        elif choice == '3':
            key = int(input("Enter key to delete: "))
            ht.delete(key)
        elif choice == '4':
            ht.display()
        elif choice == '5':
            print("Exiting program...")
            break
        else:
            print(" Invalid choice. Try again.")
