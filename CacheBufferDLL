/* @Author
Student Name: Yusuf Utku GÜL
Student ID: 150150006
Date: 19.10.2019 */

#include <iostream>
#include <cstdlib>		//for abs function
#include <fstream>		// for text processes
using namespace std;
struct node {			//define node
	int size;
	int quant;
	node* next;
};
struct stock {			// define stock
	node* head;
	void create();
	void add_stock(int);
	void sell(int);
	void current_stock();
	void clear();
};
void stock::create() {		//stock creation
	head = NULL;
}
void stock::add_stock(int size) {
	bool size_exist=false;
	node* tmp = head;
	while (tmp != NULL) {				// checks if input size already exists
		if (tmp->size == size) {
			size_exist = true;
			tmp->quant++;				//increase quantity if exist
		}
		tmp = tmp->next;
	}
	if (!size_exist) {										//if not exist create a new node 
		node* new_node = new node;
		new_node->size = size;
			new_node->quant = 1;							// set quantity to 1 
		if (head == NULL || size < head->size) {		// check if the input is the smallest in the list
			new_node->next = head;
			head = new_node;
		}
		else {
			node* temp = head;
			while (temp->next && size > temp->next->size) {
				temp = temp->next;
			}
					new_node->next = temp->next;
					temp->next = new_node;
		}
	}
}
void stock::current_stock() {				// print stock info
	node* temp = head;
	while ( temp != NULL) {
		if (temp->quant>0) {
			cout << temp->size << ":" << temp->quant << endl;
		}
		else {
			cout << "NO_STOCK" << endl;
		}
		temp = temp->next;
	}
}
void stock::sell(int size) {
	bool size_exist = false;
	node* temp = head;
	while (temp != NULL) {				// checks if size already exists in the stock
		if (temp->size == size) {
			size_exist = true;
			break;
		}
		temp = temp->next;
	}
	 temp = head;
	if (size_exist) {			// if exists and has only 1 quantity deletes the node
		 temp = head;
		node* tail = temp;
		while (temp->size != size) {	// which size to delete
			tail = temp;
			temp = temp->next;
		}
		if (temp->quant - 1 < 1) {
			if (temp == head) {		// if number first on the list
				head = temp->next;
				delete temp;
			}
			else {
				if (temp->next == NULL) {	// if number is last on the list
					tail->next = NULL;
					delete temp;
				}
				else {							//in middle
					tail->next = temp->next;
					delete temp;
				}
			}
		}
		else {					// if quantity > 1 decrease by 1
			temp->quant--;
		}
	}
	else {				// if size doesnt exist in the stock prints "NO_STOCK" 
		cout << "NO_STOCK" << endl;
	}
}
void stock::clear() {			// clears all nodes 
	node* temp = NULL;
		while (head != NULL) {
			temp = head;
			head = head->next;
			delete temp;
		}
}

int main() {		//----------------main-----------------
	stock mystock;
	mystock.create();
	fstream inputfile;
	inputfile.open("input.txt");
	int number;
	while (!inputfile.eof()) {		// text processes
		inputfile >> number;
		if (number == 0) {
			mystock.current_stock();
		}
		else if (number > 0) {
			mystock.add_stock(number);
		}
		else if (number < 0) {
			mystock.sell(abs(number));
		}
	}
	inputfile.close();
	mystock.clear();		// clear stock
	
	return 0;
}
