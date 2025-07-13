#include<iostream>
using namespace std;
class node{
    public:
    int data;
    node* left;
    node* right;
    node(int val){
        data=val;
        left=right=NULL;
    }
};
void insertAtstart(node* &head,int data){
    node* new_node=new node(data);
    if(head==NULL){
        head=new_node;
    }
    else{
        new_node->right=head;
        head->left=new_node;
        head=new_node;
    }
}
void insertAtend(node* &head,int data){
    node* new_node=new node(data);
    if(head==NULL){
        insertAtstart(head,data);
        return;
    }else{
        node* temp=head;
        while(temp->right!=NULL){
            temp=temp->right;
        }
        temp->right=new_node;
        new_node->left=temp;
    }
}
void insertAtPosition(node* &head,int data,int pos){
    node* new_node=new node(data);
    if(head==NULL){
        insertAtstart(head,data);
        return;
    }
    else{
        node* temp=head;
        int curr_position=1;
        while(temp!=NULL && curr_position<pos-1){
            temp=temp->right;
            curr_position++;
        }
        new_node->right=temp->right;
        new_node->left=temp;
        temp->right->left=new_node;
        temp->right=new_node;
        
    }
}
void deleteAtPosition(node* &head,int pos){
    if(head==NULL){
        cout<<"invalid postion to delete";
        return;
    }
    else{
        int curr_pos=1;
        node* temp=head;
        while(temp!=NULL && curr_pos<pos-1){
            temp=temp->right;
            curr_pos++;
        }
        node* to_delete = temp->right;
        temp->right = to_delete->right;
        if (to_delete->right != NULL)        
        to_delete->right->left = temp;
        delete to_delete;    

    }
}
void display(node* head){
    node* temp=head;
    while(temp!=NULL){
        cout<<temp->data<<"<=>";
        temp=temp->right;
    }
    cout<<"NULL"<<endl;
}
int main(){
    node* head=NULL;
    insertAtstart(head,30);
    insertAtstart(head,20);
    insertAtstart(head,10);
    insertAtend(head,70);
    insertAtPosition(head,90,3);
    display(head);
    return 0;
}
