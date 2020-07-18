# binary-tree-project-18.7.2020
c++ tree project 
#include<iostream>
#include<vector>
#include<string>
#include<cassert>
using namespace std; 
template<class Data_type>
struct Node
{
	Data_type info; 
	Node* left;
	Node* right;
};
template<class Data_type>
class binary_tree_search
{
	Node<Data_type>* root;

	bool isEmpty()
	{
		return root == NULL;
	}

	void insert_in_tree(Data_type element, Node<Data_type>*& root)
	{
		if (root == NULL)
		{
			root = new Node<Data_type>;   // here why to use <type_data>
			root->info = element;                // Do we have to do the same 
			root->right = NULL;					//	definition of element 
			root->left = NULL;
		}
		else
		{
			if (root->info > element)
			{
				insert_in_tree(element, root->left);
			}
			else
			{
				insert_in_tree(element, root->right);
			}
		}
	}
 
	int count_nodes(Node <Data_type >* p)
	{
		if (p == NULL)
			return 0;
		else
			return 1 + count_nodes(p->left) + count_nodes(p->right);
	}

	bool search_tree(Data_type item, Node<Data_type> *current)
	{
		if (current == NULL)return false; 

		if (current->info == item)
			return true;
		if (current->info > item)
			return search_tree(item, current->left);
		else
	    	return search_tree(item, current->right);
		
	}

	int search_max_in_leftsubtree(Data_type item, Node<Data_type>* current)
	{
		if (current == NULL)return 0;
		if (current->info > item)
			return current->info; 
		else
			return search_tree(item, current->left);
	}

	int height(Node<Data_type>* pointer)
	{
		if (pointer == NULL)return 0;
		else
		{
			int x = 1 + height(pointer->left);
			int y = 1 + height(pointer->right);
			return  x > y ? x : y;
		}
	}

	int num_leaves(Node <Data_type>* ptr)
	{
		if (ptr == 0)
			return 0; 
		else if ((ptr->left == NULL) && (ptr->right == NULL))
			return 1;// if the under of two leaves are zero
		else        //in this case we have leaf 
			return  num_leaves(ptr->left) + num_leaves(ptr->right);
	}

	int check_max_in_left_tree(Data_type element, Node<Data_type>* p)
	{
		int variable; 
		variable = element;
		variable=search_max_in_leftsubtree(variable, p->left);
		return variable; 
	}

	 Node<Data_type>* Remove_Node_tree(Node<Data_type>* p, Data_type element)
	 {
		// Node<Data_type>*current; 
		 //Node<Data_type>*trailcurrent;
		 Node<Data_type>*temp;

		 if (p == nullptr)
		 {
			 cout << "NULL===>> no removing at all" << endl;
			 return root;
		 }
		 else if (p->info > element)
		 {
			 root->left = Remove_Node_tree(root->left, element); 
		 }
		 else if (p->info < element)
		 {
			 root->right = Remove_Node_tree(root->right, element);
		 }
		 else
		 {
			 if (p->left == nullptr)
			 {
				 // the idea of left subtree is empty
				 temp = p;
				 p = temp->right;
				 temp = NULL;
				 delete temp;
			 }
			 else if (p->right == nullptr)
			 {
				 // the idea of left subtree is empty
				 temp = p;
				 p = temp->left;
				 temp = NULL;
				 delete temp;
			 }
			 else
			 { // the idea of two children are already existed here 
				 int maxValue = this->getMaxhelper(root->left); 
				 root->info = maxValue; 
				 root->left = Remove_Node_tree(root->left, maxValue); 
			 }
		 }
		 return root; 
	 }

	 int getMaxhelper(Node<Data_type>* p)
	 {
		 Node<Data_type>* temp = root; 
		 while (temp->left != nullptr)
		 {
			 temp = temp->left; 
		 }
		 return temp->info; 
	 }

	 /*int getMinhelper(Node<Data_type>* p)
	 {
		 Node<Data_type>* temp = root;
		 while (temp->left != nullptr)
		 {
			 temp = temp->left;
		 }
	 }*/

	 // end deletefromtree
	void print(Node <Data_type>* root)
	{

		if (root != NULL)
		{
			print(root->left);
			cout << root->info << endl;
			print(root->right);
		}
	}

public:
 
	/*
	////void insert(int item)
	////{
	////	Type* current;
	////	Type* trailcurrent;
	////	Type* newNode;
	////	newNode = new Type;
	////	assert(newNode != NULL);
	////	newNode->info = item;
	////	newNode->left = NULL;
	////	newNode->right = NULL;
	////	if (root == NULL)//means there is node at all in tree body
	////		root = newNode;
	////	else
	////	{
	////		root = current;
	////		while (current != NULL)
	////		{
	////			trailcurrent = current;
	////			if (current->info == item)
	////			{
	////				cout << "the insert item is already in the list--";
	////				cout << "duplicates are now allowed " << endl;
	////				return;
	////			}
	////			else
	////				if (current->info > item)
	////					current = current->left;
	////				else
	////					current = current->right;
	////		}
	////	}
	////	if (trailcurrent->info > item)
	////		trailcurrent->left = newNode;
	////	else
	////	trailcurrent->right = newNode;
	////}
	///*void insert(newtype element)
	//{
	//	nodeType<newtype>* current;
	//	nodeType<newtype>* trailcurrent;
	//	nodeType<newtype>* newnode;
	//	newnode = new nodeType<newtype>;
	//	assert(newnode != NULL);
	//	newnode->info = element;
	//	newnode->left = NULL;
	//	newnode->right = NULL;
	//
	//	current = root;
	//	trailcurrent = current;
	//	if (root == NULL)
	//		root = newnode;
	//	else
	//	{
	//
	//		current = root;
	//		if (current->info == element)
	//		{
	//			cout << "not able to add" << endl;
	//		}
	//		else
	//		{
	//			while (newnode != NULL)
	//			{
	//				trailcurrent = current;
	//				if (current->info > element)
	//					current = current->left;
	//				else
	//					current = current->right;
	//			}
	//		}
	//		if (trailcurrent->info > element)
	//			trailcurrent->left = newnode;
	//		else
	//			trailcurrent->right = newnode;
	//	}
	//}*/

	binary_tree_search()
	{
		root = NULL;
	}

	void insert2(Data_type element)
	{
		insert_in_tree(element, root);
	}

	int get_height()
	{
		Node<Data_type>* curr = root;
		return height(curr);
	}

	int get_num_nodes()
	{
		return count_nodes(root);
	}

	int get_num_leaves()
	{
		return num_leaves(root);
	}

	bool search(Data_type item)
	{
		return search_tree(item, root);
	}

	void remove(Data_type x)
	{
		root=Remove_Node_tree( root,x); 
	}

	void print1()
	{
		print(root);
	}
};

int main() 
{
	binary_tree_search<int> ob;

	//insert data
	{
		ob.insert2(78);
		ob.insert2(32);
		ob.insert2(60);
		ob.insert2(89);
		ob.insert2(46);
		ob.insert2(98);
		ob.insert2(28);
		ob.insert2(28);
		ob.insert2(53);
		ob.insert2(-232); 
		ob.insert2(4343);
		ob.insert2(99); 
		ob.insert2(4000);
		ob.insert2(67); 
	}

	//print
	 {
		ob.print1();
		cout << " >>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>" << endl;
	}

	//delete specific node
	cout << "enter the number that you want to remove" << endl; 
	while (true)
	{
		int x = 0; cin >> x; 
		ob.remove(x);
		{
			ob.print1();
			cout << "__________--------____________" << endl;
		}
	}
	//print function 
	//ob.print1();

	// search 
	/*{
		cout << "enter number to search for" << endl;
		while (true)
		{
			int x = 0; cin >> x;
			if (ob.search(x))cout << "existed" << endl;
			else cout << "not existed" << endl;
		}
	}*/
	

	//get_leaves
	/*{
		cout << "nodes_leaves=" << ob.get_num_leaves() << endl;
	}*/

	//get_node
	/*{
		cout << "the number of nodes in our tree" << endl;
		cout << "nodes_number=" << ob.get_num_nodes() << endl;
	}*/

	//Height
	/*{
	cout << "the height of tree in our tree" << endl;
	cout << "Height=" << ob .get_height() << endl;
	}*/

	//search_specific number
	/*while (true)
	{
		cout << "enter the number to check 26 -1-88-5-199-34-5-199-34-(-654)-0-8 " << endl; 
		int x = 0; 
		cin >> x; 
		bool check = ob.search(x);
		if (check == true)
			cout << "your purpose is right" << endl;
		else 
			cout << "your purpose is wrong" << endl;
	}*/

	//check empty
	//check empty function 
	/*cout << "\nfirst tree" << endl; 
	 cout << ob.Empty() << endl;
	 
	 cout << "\nsecond tree" << endl;
     cout << ob2.Empty() << endl; */ 

} 
 

 
