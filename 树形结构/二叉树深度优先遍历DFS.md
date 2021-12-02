## 使用队列

    public class Solution {
    public ArrayList<Integer> PrintFromTopToBottom(TreeNode root) {
        ArrayList<Integer> lists=new ArrayList<Integer>();
        if(root==null)
            return lists;
        Stack<TreeNode> stack=new Stack<TreeNode>();
        stack.push(root);
        while(!stack.isEmpty()){
            TreeNode tree=stack.pop();
            if(tree.right!=null)//先往栈中压入右节点，再压左节点，这样出栈就是先左节点后右节点了
                stack.push(tree.right);
            if(tree.left!=null)
                stack.push(tree.left);
            lists.add(tree.val);
        }
        return lists;
      }
    }
