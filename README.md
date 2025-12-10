#include <iostream>
#include <vector>
using namespace std;

class Medicine {
private:
    string name;
    double price;
    int stock;
public:
    Medicine(string n, double p, int s) : name(n), price(p), stock(s) {}
    void sell(int q) { 
        if(q <= stock) { stock -= q; cout << "Sold " << q << " of " << name << endl; }
        else cout << "Not enough stock\n";
    }
    void print() { cout << name << " - $" << price << " (" << stock << " left)\n"; }
    int getStock() { return stock; }
};

class Customer {
private:
    string name;
    double totalSpent;
public:
    Customer(string n) : name(n), totalSpent(0) {}
    void addPurchase(double amount) { totalSpent += amount; }
    void print() { cout << name << " spent: $" << totalSpent << endl; }
};

class Pharmacy {
private:
    vector<Medicine> medicines;
    vector<Customer> customers;
public:
    void addMedicine(string n, double p, int s) { medicines.push_back(Medicine(n,p,s)); }
    void addCustomer(string n) { customers.push_back(Customer(n)); }
    
    void sell(int medIndex, int custIndex, int qty) {
        if(medIndex < medicines.size() && custIndex < customers.size()) {
            double price = 10.0; // Fixed price for simplicity
            medicines[medIndex].sell(qty);
            customers[custIndex].addPurchase(price * qty);
        }
    }
    
    void showAll() {
        cout << "Medicines:\n";
        for(auto& m : medicines) m.print();
        cout << "\nCustomers:\n";
        for(auto& c : customers) c.print();
    }
};

int main() {
    Pharmacy p;
    p.addMedicine("Paracetamol", 5.0, 100);
    p.addMedicine("Vitamin C", 8.0, 50);
    p.addCustomer("Ali");
    p.addCustomer("Sara");
    
    p.sell(0, 0, 2);
    p.sell(1, 1, 1);
    
    p.showAll();
    return 0;
}
