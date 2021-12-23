求和在给定范围内的子串数量
先求出0-0，0-1。。。0-n的和数组 sum[n]
则 i到j的子串和为sum[j]-sum[i]
给定范围 [j,k]
只要求基于sum[j]，sum[i]的大小在[sum[i]-k,sum[i]-j]范围内则满足条件

    public static int countRangeSum(int[] nums, int lower, int upper){
        if(nums==null||nums.length==0){
            return 0;
        }
        long[] sum = new long[nums.length];
        sum[0] = nums[0];
        for(int i=1;i<nums.length;i++){
            sum[i]=sum[i-1]+nums[i];
        }
        return process(sum,0,sum.length-1,lower,upper);
    }

    public static int process(long[] sum,int L,int R,int lower,int upper){
        if(L==R){
            return sum[L]>=lower&&sum[L]<=upper?1:0;
        }
        int M = L+((R-L)>>1);
        return process(sum,L,M,lower,upper)+process(sum,M+1,R,lower,upper)+merge(sum,L,M,R,lower,upper);
    }

    public static int merge(long[] arr,int L,int M,int R,int lower,int upper){
        int ans=0;
        int windowL=L;
        int windowR=L;
        for(int i=M+1;i<=R;i++){
            long min=arr[i]-upper;
            long max=arr[i]-lower;
            while(windowR<=M&&arr[windowR]<=max){
                windowR++;
            }
            while(windowL<=M&&arr[windowL]<min){
                windowL++; 
            }
            ans+=windowR-windowL;
        }
        long[] help = new long[R-L+1];
        int i=0;
        int p1=L;
        int p2=M+1;
        while(p1<=M&&p2<=R){
            help[i++]=arr[p1]<=arr[p2]?arr[p1++]:arr[p2++];
        }
        while(p1<=M){
            help[i++]=arr[p1++];
        }
        while(p2<=R){
            help[i++]=arr[p2++];
        }
        for(int i =0;i<help.length;i++){
            arr[L+i]=help[i];
        }
        return ans;
    }