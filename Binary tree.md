# CN
package tree;

import java.util.Scanner;

public class BinaryTreeUse {
public static BinaryTreeNode<Integer>takeTreeInputBetter(boolean isRoot,int parentData,boolean isLeft){
		if(isRoot) {
		System.out.println("Enter Root Data");
		}else {
			if(isLeft) {
				System.out.println("Enter Left child of "+ parentData);
			}else {
				System.out.println("Enter Right child of "+ parentData);
			}
		}
		Scanner s=new Scanner(System.in);
		int rootData=s.nextInt();
		
		if(rootData==-1) {
			return null;
		}
		BinaryTreeNode<Integer>root=new BinaryTreeNode<Integer>(rootData);
		BinaryTreeNode<Integer>leftChild=takeTreeInputBetter(false,rootData,true);
		BinaryTreeNode<Integer>rightChild=takeTreeInputBetter(false,rootData,false);
		root.left=leftChild;
		root.right=rightChild;
		return root;
	}
	public static BinaryTreeNode<Integer>takeTreeInput(){
		System.out.println("Enter Root Data");
		Scanner s=new Scanner(System.in);
		int rootData=s.nextInt();
		
		if(rootData==-1) {
			return null;
		}
		BinaryTreeNode<Integer>root=new BinaryTreeNode<Integer>(rootData);
		BinaryTreeNode<Integer>leftChild=takeTreeInput();
		BinaryTreeNode<Integer>rightChild=takeTreeInput();
		root.left=leftChild;
		root.right=rightChild;
		return root;
	}
	public static void printTreeBetter(BinaryTreeNode<Integer>root) {
		//take care of base case (recursively printing)
		if(root==null) {
			return;
		}
		System.out.print(root.data +":");
		if(root.left!=null) {
			System.out.print("L" + root.left.data + ',');
		}
		if(root.right!=null) {
			System.out.print("R" + root.right.data );
		}
		System.out.println();
		
		printTreeBetter(root.left);

		printTreeBetter(root.right);
		
}
	
	public static void printTree(BinaryTreeNode<Integer>root) {
		//take care of base case (recursively printing)
		if(root==null) {
			return;
		}
		System.out.println(root.data);
		
		printTree(root.left);
		
		printTree(root.right);
//		System.out.println(root.data);
//		if(root.left!=null) {
//		printTree(root.left);
//		}
//		if(root.right!=null) {
//		printTree(root.right);
//		}
		
	}
	public static int numNodes(BinaryTreeNode<Integer>root) {
		if(root==null) {
			return 0;
		}
		int leftNodeCount=numNodes(root.left);
		int rightNodeCount=numNodes(root.right);
		return 1+leftNodeCount +rightNodeCount;
	}
	public static int getSum(BinaryTreeNode<Integer> root) {
		if(root==null) {
			return 0;
		}
		int sumLeft=getSum(root.left);
		int sumRight=getSum(root.right);
		return root.data +sumLeft+sumRight;
	}
	
	
	public static int largestNode(BinaryTreeNode<Integer>root) {
		if(root==null) {
			return -1;
		}
		int largestLeft=largestNode(root.left);
	int largestRight=largestNode(root.right);
	return Math.max(root.data, Math.max(largestLeft, largestRight));
	}
	
	public static int countNodesGreaterThanX(BinaryTreeNode<Integer>root,int x) {
		if(root==null) {
			return 0;
		}
		int nodesLeft=countNodesGreaterThanX(root.left,0);
	int nodesRight=countNodesGreaterThanX(root.right,0);
	if(root.data>x) {
		return 1+ nodesLeft+nodesRight;
	}else {
		return nodesLeft+nodesRight;
	}
	
	}
	
	public static int height(BinaryTreeNode<Integer> root) {
		//Your code goes here
		if(root==null){
			return 0;
		}
		int heightLeft=height(root.left);
		int heightRight = height(root.right);

		return 1+Math.max(heightLeft,heightRight);

	}
	
	public static int numLeaf(BinaryTreeNode<Integer>root) {
		if(root==null) {
			return 0;
		}
		if(root.left==null && root.right==null) {
			return 1;
		}
		int leafLeft=numLeaf(root.left);
		int leafRight=numLeaf(root.right);
		return leafLeft+leafRight;
	}
	
	public static void printAtDepthK(BinaryTreeNode<Integer>root,int k) {
		if(root==null) {
			return;
		}
		if(k==0) {
			System.out.println(root.data);
			return;
			
		}
		printAtDepthK(root.left,k-1);

		printAtDepthK(root.right,k-1);
	}
	public static void changeToDepthTree(BinaryTreeNode<Integer> root) {
		if(root==null) {
			return;
		}
//		if(root.left==null && root.right==null) {
//			return ;
//		}

		changeToDepthTree(root.left);

		changeToDepthTree(root.right);
	}
	
	public static boolean isNodePresent(BinaryTreeNode<Integer> root, int x) {
	    //Your code goes here
		if(root==null){
			return false ;
		}
		if(root.data==x) {
			return true;
	}
		boolean NodeinLeft=isNodePresent(root.left,x);
		boolean NodeinRight=isNodePresent(root.right,x);
		return (NodeinLeft || NodeinRight);
}
	
	public static BinaryTreeNode<Integer>removeLeaves(BinaryTreeNode<Integer>root){
		if(root==null) {
			return null;
		}
		if(root.left==null && root.right==null) {
			return null;
		}
		root.left=removeLeaves(root.left);
		root.right=removeLeaves(root.right);
		return root;
	}
	public static boolean isBalanced(BinaryTreeNode<Integer>root) {
	if(root==null) {
		return true;
	}
	int leftHeight=height(root.left);
	int rightHeight=height(root.right);
	
	if(Math.abs(leftHeight - rightHeight) > 1) {
		return false;
	}
	boolean isLeftBalanced=isBalanced(root.left);
	boolean isRightBalanced=isBalanced(root.right);
	return isLeftBalanced && isRightBalanced;
	}
	
	public static BalancedTreeReturn isBalancedBetter(BinaryTreeNode<Integer>root) {
		if(root==null) {
			int height=0;
			boolean isBal=true;
			BalancedTreeReturn ans=new BalancedTreeReturn();
			ans.height=height;
			ans.isBal=isBal;
			return ans;
		}
		BalancedTreeReturn leftOutput=isBalancedBetter(root.left);
		BalancedTreeReturn rightOutput=isBalancedBetter(root.right);
        boolean isBal=true;
        int height= 1+ Math.max(leftOutput.height, rightOutput.height);
        
        if(Math.abs(leftOutput.height - rightOutput.height)>1 ) {
        	isBal=false;
        }
        
        if(!leftOutput.isBal || !rightOutput.isBal) {
        	isBal=false;
        }
	
        BalancedTreeReturn ans=new BalancedTreeReturn();
        ans.height=height;
        ans.isBal=isBal;
        return ans;
	
	}
	public static void main(String[]args) {
//BinaryTreeNode<Integer>root=new BinaryTreeNode<Integer>(1);
//BinaryTreeNode<Integer>rootLeft=new BinaryTreeNode<Integer>(2);
//BinaryTreeNode<Integer>rootRight=new BinaryTreeNode<Integer>(3);
//root.left= rootLeft;
//root.right=rootRight;
//
////printTreeBetter(root);
//
//
//
//BinaryTreeNode<Integer>twoRight=new BinaryTreeNode<>(4);
//BinaryTreeNode<Integer>threeLeft=new BinaryTreeNode<>(5);
//rootLeft.right=twoRight;
//rootRight.left=threeLeft;

		BinaryTreeNode<Integer>root=takeTreeInputBetter(true,0,true);

printTreeBetter(root);
System.out.println("Num of Nodes "+numNodes(root));
	System.out.println("sum of nodes"+getSum(root));
	System.out.println("Count " +countNodesGreaterThanX(root,2));
	System.out.println("Height " +height(root));
	System.out.println("Num of Leaves"+numLeaf(root));
	System.out.println("print at depth k");
     printAtDepthK(root,2);
     System.out.println("isBalanced "+isBalancedBetter(root).isBal);
    System.out.println("Node is Present"+isNodePresent(root,3));
    BinaryTreeNode<Integer>newRoot=removeLeaves(root);
    printTreeBetter(newRoot);
   
	
	}
	
}
