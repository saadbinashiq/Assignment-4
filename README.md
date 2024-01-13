# Assignment-4
//Inventory Management System using vectors:

// inventory_management.cpp
#include <iostream>
#include <vector>

using namespace std;

struct Product {
    int id;
    string name;
    // Add other relevant product information
    // Constructor
    Product(int i, const string& n) : id(i), name(n) {}
};

vector<Product> inventory;

void addProduct(int id, const string& name) {
    // Check if the product with the given ID already exists
    for (const auto& product : inventory) {
        if (product.id == id) {
            cout << "Product with ID " << id << " already exists in the inventory.\n";
            return;
        }
    }

  // If the product does not exist, add it to the inventory
    inventory.emplace_back(id, name);
    cout << "Product added to the inventory.\n";
}

void removeProduct(int id) {
    // Use erase-remove idiom to remove the product with the specified ID
    inventory.erase(remove_if(inventory.begin(), inventory.end(),
                    [id](const Product& p) { return p.id == id; }), inventory.end());

  cout << "Product with ID " << id << " removed from the inventory.\n";
}

int main() {
    // Example usage
    addProduct(1, "Laptop");
    addProduct(2, "Smartphone");
    addProduct(3, "Headphones");
    removeProduct(2);
    return 0;
}
// sorting_performance.cpp
#include <iostream>
#include <vector>
#include <algorithm>
#include <chrono>

using namespace std;

int main() {
    const int size = 100000;
    vector<int> numbers(size);

   // Initialize the vector in descending order
    for (int i = 0; i < size; ++i) {
        numbers[i] = size - i;
    }
    // Measure execution time for Bubble Sort
    auto start_bubble = chrono::high_resolution_clock::now();
    // Bubble Sort implementation here
    for (int i = 0; i < size - 1; ++i) {
        for (int j = 0; j < size - i - 1; ++j) {
            if (numbers[j] > numbers[j + 1]) {
                swap(numbers[j], numbers[j + 1]);
            }
        }
    }
    auto end_bubble = chrono::high_resolution_clock::now();
    chrono::duration<double> duration_bubble = end_bubble - start_bubble;
    // Measure execution time for STL sort
    auto start_stl_sort = chrono::high_resolution_clock::now();
    sort(numbers.begin(), numbers.end());
    auto end_stl_sort = chrono::high_resolution_clock::now();
    chrono::duration<double> duration_stl_sort = end_stl_sort - start_stl_sort;
    // Print execution times
    cout << "Bubble Sort Execution Time: " << duration_bubble.count() << " seconds\n";
    cout << "STL Sort Execution Time: " << duration_stl_sort.count() << " seconds\n";
    // Print first 10 and last 10 integers
    cout << "First 10 integers: ";
    for (int i = 0; i < 10; ++i) {
        cout << numbers[i] << " ";
    }
    cout << "\n";
    cout << "Last 10 integers: ";
    for (int i = size - 10; i < size; ++i) {
        cout << numbers[i] << " ";
    }
    cout << "\n";
    return 0;
}
