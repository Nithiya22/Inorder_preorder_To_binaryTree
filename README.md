# Inorder_preorder_To_binaryTree
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        HashMap<Integer,Integer> mp=new HashMap<>();
        for(int i=0;i<inorder.length;i++){
            mp.put(inorder[i],i);
            
        }
        TreeNode root= BuildTree(preorder,0,preorder.length-1,inorder,0,inorder.length-1,mp);
        return root;
        
    }
    public static TreeNode BuildTree(int[] preorder,int prestart,int preend,int[] inorder,int instart,int inend,HashMap<Integer,Integer> mp){
        if(prestart>preend || instart>inend){
            return null;
        }
        //t data=mp.get(prestart);
        TreeNode root=new TreeNode(preorder[prestart]);
        int  inroot=mp.get(root.val);
        int  numsleft=inroot-instart;
        root.left=BuildTree(preorder,prestart+1,prestart+numsleft,inorder,instart,inroot-1,mp);
        root.right=BuildTree(preorder,prestart+numsleft+1,preend,inorder,inroot+1,inend,mp);
        return root;
    }
}
