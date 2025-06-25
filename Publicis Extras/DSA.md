
---

### Next larger

Using monotonic stack

```java
static int [] nextLargerElement(int nums[], int n){
	Stack<Integer> st = new Stack<>();
	int[] ans = new int[n];
	for(int i=n-1;i>=0;i--){
		while(!st.isEmpty() && st.peek()<=nums[i]){
			st.pop();
		}
		
		if(!st.isEmpty()){
			ans[i]=st.peek();
		}else{
			ans[i]=-1;
		}
		st.push(nums[i]);
	}
	return ans;
}
```

Longest valid parenthesis:

We push the index opening brackets in stack. Now once we encounter closing bracket we take it out. 
Now stack can be empty we push current index to indicate that this is valid pos for starting new valid parenthesis. Otherwise we calc answer as diff of current index and top element.

```java
static int longestValidParentheses(String str){

	Stack<Integer> st = new Stack<>();
	st.push(-1);
	int ans = 0;
	for(int i=0;i<str.length();i++){
		char ch = str.charAt(i);
		if(ch=='('){
			st.push(i);
		}else{
			st.pop();
			if(st.isEmpty())st.push(i);
			else ans = Math.max(ans,i-st.peek());
		}
	}
	return ans;
}
```

reverse Linked list:

At any moment of point we will be having three consecutive nodes into consideration.
prev , curr , next -> linked list upto prev is already reversed.

![[Pasted image 20250625122946.png]]

Now we will update the curr->next pointer to point to prev and curr and prev both are moved. 
Observe that at end curr will be null and we will return prev.

```java
public ListNode reverseLinkedList(ListNode head){
	ListNode curr=head,prev=null;
	while(curr!=null){
		ListNode next=curr.next;
		curr.next=prev;
		prev=curr;
		curr=next;
	}
	return prev;
}
```

Making middle the head of ll:

Idea : Use small and fast pointer when fast will reach end slow will be at middle. we will keep prev slow to update nodes.

```cpp
while(fast!=NULL && fast->next!=NULL){
	prev = slow;
	fast = fast->next->next;
	slow = slow->next;
}
```

Deleting kth from end:

Idea: Fast pointer moves k steps first. Now both slow and fast pointer will move at same speed. Observe that slow will be at n-k th from start when fast reaches end.

```cpp
ListNode* deleteKthToLast(ListNode* head , int k){
	ListNode* fast=head;
	ListNode* slow=head;
	for(int i=0;i<k;i++){
		fast=fast->next;
	}
	if(fast==NULL){
		return head->next;
	}
	while(fast->next!=NULL){
		fast=fast->next;
		slow=slow->next;
	}
	slow->next=slow->next->next; // slow will be at prev of kth to end
	return head;
}
```

Deleting node in linked list

![[Pasted image 20250625123943.png]]

Suppose we have to delete B. First we move value of C to B. and then delete C. 

```java
public static void deleteGivenNode(ListNode node) {
	ListNode next = node.next;
	node.val=next.val;
	node.next=next.next;
}
```

Insert element in a sorted curcular list:

First if linked list is empty then we create a circular list.
Otherwise we check where to insert two cases 

```java
public ListNode insertIntoSortedCircularList(ListNode head,int insertVal){
	ListNode node = new ListNode(insertVal);
	if (head == null) {
		node.next = node;
		return node;
	}
	ListNode curr = head;
	do{
		ListNode next = curr.next;
		// insert in between curr and next
		if (curr.val <= insertVal && insertVal <= next.val) {
			node.next = next;
			curr.next = node;
			return head;
		}
		// if u rached at point curr > next insert in between
		if (curr.val > next.val && (insertVal >= curr.val || insertVal <= next.val)) {
			node.next = next;
			curr.next = node;
			return head;
		}
		curr = curr.next;
	}while(curr != head);
	
	node.next = head.next;
	head.next = node;
	return head;
}
```

Write a program to find the node at which the intersection of two singly linked lists begins.

The idea is we start traversing both the lists. Once anyone of the pointer becomes null it will track other linked list. it is guaranteed that loop will terminate in max 2*n iterations.

```java
public static ListNode listIntersectionPoint(ListNode head1, ListNode head2){
	if(head1==null || head2==null){
		return null;
	}
	ListNode a=head1,b=head2;
	while(head1!=head2){
		head1=(head1==null?b:head1.next);	
		head2=(head2==null?a:head2.next);
	}
	return head1;
}
```

#### Binary tree 

Diameter:

rec() returns the max depth of any node and ans keeps track of diamter of tree. diameter stacks the edges so its value edges = nodes on path -1

```java
private int ans=0;

public int diameterOfBinaryTree(TreeNode root){
	rec(root);
	return ans;
}

public int rec(TreeNode root){
	
	if(root==null) return 0;
	int lft = rec(root.left);	
	int rgt = rec(root.right);

	ans = Math.max(ans,lft+rgt);
	return 1+Math.max(lft,rgt);
}
```

Right view:

Do the level wise traversal and keep the last node of the level into ans.

```java
public ArrayList<Long> rightViewBinaryTree(TreeNode root){
	ArrayList<Long> ans = new ArrayList<>();
	Queue<TreeNode> q = new LinkedList<>();
	q.offer(root);
	while(!q.isEmpty()){
		int sz = q.size();
		long rgt_val=0;
		for(int i=0;i<sz;i++){
			TreeNode curr = q.poll();
			rgt_val = curr.val;
			if(curr.left!=null){
				q.offer(curr.left);
			}
			if(curr.right!=null){
				q.offer(curr.right);
			}
		}
		ans.add(rgt_val);
	}
	return ans;
}
```

inorder Traversal -> left,print(curr),right
Preorder Traversal -> print(curr),left,right
Postorder Traversal -> left,right,print(curr)

#### BST

Validating bst enough to alidate evety node. For this we can return max_value and min_value of every node recursively. 
More clever approach: Idea is to maintain the valid range of values for a given node. 
Obvously we will start with inf value of min=-inf and max=inf. If node is not the range then bst is invalid.

When we will go more in depth ranges will shrunk on both sides.

```java
public boolean check(TreeNode root,int mn,int mx){
	if(root==null){
		return true;
	}
	
	if(root.val<mn || root.val>mx)return false;
	return check(root.left,mn,(int)root.val-1) && check(root.right,(int)root.val+1,mx);
}
```

LCA in BST:

A general LCA in binary tree requires us to do level wise traversal. We can however solve the lca in bst more wisely.

If current node value is more than both nodes then lca must be in left. 
If current node value is less than both nodes than lca must be on right.
Current node is the answer if its value is larger than one node and smaller than other node.

```java
public TreeNode lowestCommonAncestorInBST(TreeNode root, TreeNode p, TreeNode q){
	if(root==null){
		return null;
	}
	if(root.val>p.val && root.val>q.val){
		return lowestCommonAncestorInBST(root.left,p,q);
	}
	if(root.val<p.val && root.val<q.val){
		return lowestCommonAncestorInBST(root.right,p,q);
	}
	return root;
}
```

Inorder successor:

```java
public int inorderSuccessor(TreeNode root,TreeNode p){
	succ = null;
	while(root!=null){
		if(p.val < root.val){
			succ = root;
			root = root.left;
		}else{
			root = root.right;
		}
	}
	if(succ==null)return -1;
	return (int)succ.val;
}
```

if current node has value more than target then we go left but this is possible solution.
Similarly if current node has value more than target then we go right.

Binary tree from inorder and postorder:

Done recursively->

we have start end index of current range. 
- Start from the last element in postorder (root).
- Find this root in inorder to divide into left and right subtrees.
- Recurse:
    - Build **right subtree first**, because in postorder, right subtree comes before left subtree (when going backward).
    - Then build **left subtree**.


```java
private TreeNode helper(int[] inorder,int[] postorder,int st,int end){
	if(st>end)return null;
	int val = postorder[idx--];
	TreeNode root = new TreeNode(val);
	int i = mp.get(val);
	root.right = helper(inorder,postorder,i+1,end);
	root.left = helper(inorder,postorder,st,i-1);
	return root;
}
```

Kth largest in BST:

We go to right subtree first and check there. If count was less than k that means there were less than k elements in right subtree.

Now we can move to left subtree. Here either this is kth largest node or we should find it in left subtree. 

```java
private int dfs(TreeNode root,int k){
	if(root==null)return -1;	
	int res = dfs(root.right,k);
	if(res!=-1)return res;
	cnt++;
	if(cnt==k){
		return (int)root.val;
	}
	return dfs(root.left,k);
}
```

