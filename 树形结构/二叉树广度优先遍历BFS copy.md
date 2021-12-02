## 使用队列

    public class Solution {
        public ArrayList<Integer> PrintFromTopToBottom(TreeNode root) {
            ArrayList<Integer> lists=new ArrayList<Integer>();
            if(root==null)
                return lists;
            Queue<TreeNode> queue=new LinkedList<TreeNode>();
            queue.offer(root);
            while(!queue.isEmpty()){
                TreeNode tree=queue.poll();
                if(tree.left!=null)
                    queue.offer(tree.left);
                if(tree.right!=null)
                    queue.offer(tree.right);
                lists.add(tree.val);
            }
            return lists;
        }
