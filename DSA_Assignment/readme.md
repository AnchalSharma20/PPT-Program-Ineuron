DSA-Assignments
===============
Assignment-1
------------
Q1.
```Java
public int[] twoSum(int[] nums, int target) {
        Map < Integer, Integer > seen = new HashMap < > ();
        for (int i = 0; i < nums.length; i++) {
            int complement = target - nums[i];
            if (seen.containsKey(complement)) {
                return new int[] {
                    seen.get(complement), i
                };
            }
            seen.put(nums[i], i);
        }
        return null; 
    }
```

Q2.
```Java
public int removeElement(int[] nums, int val) {
     int i=0;
        int j=0;
        while(j < nums.length)
        {
            if(nums[j] != val)
            {
                nums[i] = nums[j];
                i++;
            }
            j++;
        }
        return i;
    }
```

Q3.
```Java
public int searchInsert(int[] nums, int target) {
        int l=0;
        int r=nums.length-1;
        while(l<=r)
        {
            int mid=l+(r-1)/2;
            if(nums[mid]==target) return mid;
           else if(nums[mid]>target){
               r=mid-1;
           }else l=mid+1;
        }
        return l;
    }
```

Q4.
```Java
public int[] plusOne(int[] digits) {
for (int i = digits.length - 1; i >= 0; i--) {
	if (digits[i] < 9) {
		digits[i]++;
		return digits;
	}
	digits[i] = 0;
}

digits = new int[digits.length + 1];
digits[0] = 1;
return digits;

        
    }
```

Q5.
```Java
public void merge(int[] nums1, int m, int[] nums2, int n) {
        int[] nums1Copy = new int[m];
        for (int i = 0; i < m; i++) {
            nums1Copy[i] = nums1[i];
        }
         int p1 = 0;
        int p2 = 0;
       for (int p = 0; p < m + n; p++) {
           
            if (p2 >= n || (p1 < m && nums1Copy[p1] < nums2[p2])) {
                nums1[p] = nums1Copy[p1++];
            } else {
                nums1[p] = nums2[p2++];
            }
        }
        
    }
```

Q6.
```Java
public boolean containsDuplicate(int[] nums) {
        HashMap<Integer,Integer> map = new HashMap<>();
        for (int i = 0; i < nums.length; i++) {
            if (map.containsKey(nums[i])) {
                return true;
            }
            map.put(nums[i],1);
        }
        return false;
        
    }
```

 Q7.
 ```Java
 public void moveZeroes(int[] nums) {
        int n=nums.length;
        int count=0;
        for(int i=0;i<n;i++){
            if(nums[i]!=0){
                swap(i,count,nums);
                count++;
            }
        }

        
    }
    public void swap(int i,int j,int[] nums){
        int temp=nums[i];
        nums[i]=nums[j];
        nums[j]=temp;
    }
```

Q8.
```Java
public int[] findErrorNums(int[] nums) {
        int[] res=new int[2];

        HashSet<Integer> set= new HashSet<>();
        int sum=0;
        for(int num: nums){
            if(set.contains(num)){
                res[0]=num;
            }else {
                
                set.add(num);
                 sum+=num;
            
        }
       
        }
        // we got the number which was repeated twice

        int n=nums.length;
        res[1]=(n*(n+1)/2)-(sum);



return res;
    }
```
    
Assignment-2
------------
Q1.
```Java
public int arrayPairSum(int[] nums) {
         Arrays.sort(nums);
        int sum = 0;
        for(int i = 0 ; i < nums.length-1; i= i+2){
            sum = sum+ Math.min(nums[i],nums[i+1]);
        }
        return sum;
    }
```

Q2.
```Java
public int distributeCandies(int[] candyType) {
     
     int n=candyType.length;
     int candysAllowed=n/2;
     if(candysAllowed<=findTypesOfCandy(candyType)){
         return candysAllowed;
     }else return findTypesOfCandy(candyType);

        
    }
    public int findTypesOfCandy(int[] ct){
        Arrays.sort(ct);
        int count=1;
        for(int i=1;i<ct.length;i++){
            if(ct[i]!=ct[i-1]) count++;
        }
        return count;
    }
```

Q3.
```Java
public int findLHS(int[] nums) {
         Map<Integer,Integer> m=new HashMap<>();
        for(int i:nums)
            m.put(i,m.getOrDefault(i,0)+1);
        
        int max=0;
        for(int i:m.keySet())
            if(m.containsKey(i+1)) max=Math.max(max,m.get(i)+m.get(i+1)); 
        
        return max;
    }
```

Q4.
```Java
public boolean canPlaceFlowers(int[] flowerbed, int n) {
         int planted=0;
        for(int i=0;i<flowerbed.length;i++){
            if(flowerbed[i]==0){
              int prev=(i==0||flowerbed[i-1]==0)?0:1;
              int next=((i==flowerbed.length-1) || flowerbed[i+1]==0)?0:1;
              if(prev==0 && next==0) {
                  planted++;
                  flowerbed[i]=1;
              }

            }
        }
        return planted>=n;
       
        
    }
```

Q5.
```Java
public int maximumProduct(int[] nums) {
    
        int maxProduct=Integer.MIN_VALUE;
        int prod=1;
        int left=0;
        for(int i=0;i<3;i++) {
         prod=prod*nums[i];
        }
      maxProduct=  Math.max(prod,maxProduct);
        for(int i=3;i<nums.length;i++){
            prod=prod/nums[left]*nums[i];
            left++;
        }
        maxProduct= Math.max(prod,maxProduct);
        return maxProduct;
        
    }
```

Q6.
```Java
public int search(int[] nums, int target) {
       if(nums.length==0) return -1;

       int l=0;
       int r=nums.length-1;
       while(l<=r){
        int mid=l+(r-l)/2;
        if(nums[mid]==target) return mid;

       else if(nums[mid]>target) r=mid-1;
        else l=mid+1;

       }
       return -1;

        
    }
```

Q7.
```Java
public boolean isMonotonic(int[] nums) {
            for(int i = 0; i < nums.length - 1; i++){
            if(nums[i] < nums[i + 1]) {
                
                for(int j = i + 1; j < nums.length - 1; j++){
                    if(nums[j] > nums[j + 1]) return false;
                }

                return true;
            }else if(nums[i] > nums[i + 1]) {
                
                for(int j = i + 1; j < nums.length - 1; j++){
                    if(nums[j] < nums[j + 1]) return false;
                }

                return true;
            }
        }

        return true;
    }
```

Q8.
```Java
public int smallestRangeI(int[] nums, int k) {
         //find max and min element 
        int max, min;
        max=min=nums[0];
        for(int i=0;i<nums.length;i++){
            max=Math.max(max,nums[i]);
            min=Math.min(min,nums[i]);

        }
        // how will be the difference will be minimum
        // when we max=max-k and min=min+k;

        int diff= (max-k)-(min+k);

        return (diff>0) ? diff : 0;
    }
```
Assignment-3
------------
Q1.
```Java
public int threeSumClosest(int[] nums, int target) {
           Arrays.sort(nums);
        int minDistance = Integer.MAX_VALUE;
        int closestSum = 0;

        for(int i = 0; i < nums.length - 2; i++) {
            int start = i + 1;
            int end = nums.length - 1;

            while(start < end) {
                int sum = nums[i] + nums[start] + nums[end];
                int distance = Math.abs(target - sum);

                if(sum == target) {
                    return sum;
                }  

                if(distance < minDistance) {
                    minDistance = distance;
                    closestSum = sum;
                }

                if(sum < target) {
                    start++;
                } else {
                    end--;
                }
            }
        }
        return closestSum;
    }
```

Q2.
```Java
public List<List<Integer>> fourSum(int[] nums, int target) {
               int n=nums.length;
        Arrays.sort(nums);
        List<List<Integer>> ans=new ArrayList<>();
        if(n==0||n<3){
            return ans;
        }
     
        for(int i=0;i<n;i++){
            for(int j=i+1;j<n;j++){
                int low=j+1;
                int high=n-1;
                int sum=target-nums[i]-nums[j];
                while(low<high){
                    if(nums[low]+nums[high]==sum){
                        List<Integer> temp=new ArrayList<>();
                        temp.add(nums[i]);
                        temp.add(nums[j]);
                        temp.add(nums[low]);
                        temp.add(nums[high]);
                        ans.add(temp);
                        while(low<high&&nums[low]==nums[low+1]){
                            low++;
                        }
                        while(low<high&&nums[high]==nums[high-1]){
                            high--;
                        }
                        low++;
                        high--;
                    }
                    else if(nums[low]+nums[high]<sum){
                        low++;
                    }
                    else{
                        high--;
                    }
                }
                while(j+1<n&&nums[j+1]==nums[j]){
                    j++;
                }
            }
            while(i+1<n&&nums[i+1]==nums[i]){
                i++;
            }
        }
        return ans;
    }
```

Q3.
```Java
public void nextPermutation(int[] nums) {
        int i=nums.length-2;
        while(i>=0 && nums[i]>=nums[i+1]) i--;

        if(i>=0){
            int j=nums.length-1;
            while(j>=0 && nums[j]<=nums[i]) j--;

            swap(nums,i,j);
        }
        reverse(nums,i+1);
        
    }
    public void swap(int[] nums,int i,int j){
        int temp=nums[i];
        nums[i]=nums[j];
        nums[j]=temp;
    }
    public void reverse(int[] nums,int i){
      int start =i;
      int end=nums.length-1;
      while(start<end){
          swap(nums,start,end);
          start++;
          end--;
      }

    }
```

Q4.
```Java
 public int searchInsert(int[] nums, int target) {
        int start = 0;
        int end = nums.length-1;

        while (start <= end) {
            int mid = start + (end-start)/2;
            if (nums[mid] == target) return mid;
            else if (nums[mid] > target) end = mid-1;
            else start = mid+1;
        }

        return start;
    }
```

Q5.
```Java
public int[] plusOne(int[] digits) {
for (int i = digits.length - 1; i >= 0; i--) {
	if (digits[i] < 9) {
		digits[i]++;
		return digits;
	}
	digits[i] = 0;
}

digits = new int[digits.length + 1];
digits[0] = 1;
return digits;

        
    }
```

Q6.
```Java
public int singleNumber(int[] nums) {
        int ans=0; //since XOR with 0 returns same number 
        for(int i=0; i<nums.length; i++){
            ans ^= nums[i];  // ans = (ans) XOR (array element at i) 
        }
        return ans;    
    }
```

Q7.
```Java
public List<String> findMissingRanges(int[] nums, int lower, int upper) {
        List<String> res = new ArrayList<String>();
        int next = lower;
        for (int i = 0; i < nums.length; i++) {
            // 1. We don't need to add [Integer.MAX_VALUE, ...] to result
            if(lower == Integer.MAX_VALUE) return res;
            if (nums[i] < next) {
                continue;
            }
            if (nums[i] == next) {
                next++;
                continue;
            }
            res.add(getRange(next, nums[i] - 1));
            // 2. We don't need to proceed after we have process Integer.MAX_VALUE in array
            if(nums[i] == Integer.MAX_VALUE) return res;
            next = nums[i] + 1;
        }
        
        if (next <= upper) {
            res.add(getRange(next, upper));
        }
        return res;
    }
    
    public String getRange(int n1, int n2) {
        return n1 == n2 ? String.valueOf(n1) : String.format("%d->%d" , n1, n2);
    }
```

Q8.
```Java
public boolean canAttendMeetings(int[][] intervals) {
    Arrays.sort(intervals, new Comparator<int[]>() {
      public int compare(int[] i1, int[] i2) {
        return i1[0] - i2[0];
      }
    });
    for (int i = 0; i < intervals.length - 1; i++) {
      if (intervals[i][1] > intervals[i + 1][0])
        return false;
    }
    return
```

Assignment-4
-------------

Q1.
```Java
public List<Integer> arraysIntersection(int[] arr1, int[] arr2, int[] arr3) {
        List<Integer> intersection = new ArrayList<Integer>();
        int length1 = arr1.length, length2 = arr2.length, length3 = arr3.length;
        int index1 = 0, index2 = 0, index3 = 0;
        while (index1 < length1 && index2 < length2 && index3 < length3) {
            int num1 = arr1[index1], num2 = arr2[index2], num3 = arr3[index3];
            if (num1 == num2 && num1 == num3) {
                intersection.add(num1);
                index1++;
                index2++;
                index3++;
            } else {
                int increment1 = 0, increment2 = 0, increment3 = 0;
                if (num1 < num2 || num1 < num3)
                    increment1 = 1;
                if (num2 < num1 || num2 < num3)
                    increment2 = 1;
                if (num3 < num1 || num3 < num2)
                    increment3 = 1;
                index1 += increment1;
                index2 += increment2;
                index3 += increment3;
            }
        }
        return intersection;
    }
```

Q2.
```Java
public List<List<Integer>> findDifference(int[] nums1, int[] nums2) {
        List<List<Integer>> ans = new ArrayList<>();
        HashSet<Integer> set1 = new HashSet<>();
        HashSet<Integer> set2 = new HashSet<>();
          
        for(int i = 0 ; i < nums1.length; i ++){
            set1.add(nums1[i]);
        }
          for(int i = 0 ; i < nums2.length; i ++){
            set2.add(nums2[i]);
        }
         List<Integer> list1 = new ArrayList<>();
          for(int i = 0 ; i < nums1.length; i ++){
            if(!set2.contains(nums1[i]) && !list1.contains(nums1[i])){
                list1.add(nums1[i]);
            }
        }
         ans.add(list1);
          List<Integer> list2 = new ArrayList<>();
          for(int i = 0 ; i < nums2.length; i ++){
            if(!set1.contains(nums2[i]) && !list2.contains(nums2[i])){
                list2.add(nums2[i]);
            }
        }
        ans.add(list2);
        return ans;
        

    }
```

Q3.
```Java
public int[][] transpose(int[][] matrix) {
        int row=matrix.length;
        int col=matrix[0].length;
        int arr[][]=new int[col][row];
        for(int i=0;i<col;i++)
        {
            for(int j=0;j<row;j++)
            {
            arr[i][j]=matrix[j][i];
            }
        }
        return arr;
        
    }
```

Q4.
```Java
public int arrayPairSum(int[] nums) {
        Arrays.sort(nums);
        int n = nums.length;
        int sum = 0;
        for (int i = 0; i < n; i += 2) {
            sum += nums[i];
        }
        return sum;
    }
```

Q5.
```Java
public int arrangeCoins(int n) {
         int i = 1; // which row we are on
		while(n > 0){ // checking to see if we have used all our coins
			i++; // increasing our row
			n = n-i; // adding coins to our row
		}
		return i-1;
    }
```

Q6.
```Java
public int[] sortedSquares(int[] nums) {
        int n = nums.length;
        int[] result = new int[n];
        int left = 0;
        int right = n - 1;
        int i = n - 1;

        while (left <= right) {
            int leftSquare = nums[left] * nums[left];
            int rightSquare = nums[right] * nums[right];

            if (leftSquare > rightSquare) {
                result[i] = leftSquare;
                left++;
            } else {
                result[i] = rightSquare;
                right--;
            }

            i--;
        }

        return result;
    }
```

Q7.
```Java
public int maxCount(int m, int n, List<List<Integer>> ops) {
        Map<Integer, Integer> xs = new HashMap<>();
        Map<Integer, Integer> ys = new HashMap<>();

        for (List<Integer> op : ops) {
            for (int i = 1; i <= op.get(0); i++) {
                xs.put(i, xs.getOrDefault(i, 0) + 1);
            }
            for (int j = 1; j <= op.get(1); j++) {
                ys.put(j, ys.getOrDefault(j, 0) + 1);
            }
        }

        int maxX = m;
        int maxY = n;
        int maxXval = 0;
        int maxYval = 0;

        for (Map.Entry<Integer, Integer> entry : xs.entrySet()) {
            int k = entry.getKey();
            int v = entry.getValue();
            if (v >= maxXval) {
                maxX = k;
                maxXval = v;
            }
        }

        for (Map.Entry<Integer, Integer> entry : ys.entrySet()) {
            int k = entry.getKey();
            int v = entry.getValue();
            if (v >= maxYval) {
                maxY = k;
                maxYval = v;
            }
        }

        return maxX * maxY;
    }
```

Q8.
```Java
public int[] shuffle(int[] nums, int n) {
        int[] ans=new int[nums.length];
        int mid=nums.length/2;
        int j=0;
        for(int i=0;i<nums.length;i=i+2){
           ans[i]=nums[j];
           j++;
        }
        j=mid;
         for(int i=1;i<nums.length;i=i+2){
           ans[i]=nums[j];
           j++;
        }
        return ans;
    }
```

Assignment-5
-------------

Q1.
```Java
public int[][] construct2DArray(int[] original, int m, int n) {
        if(m * n != original.length) return new int[][]{};
        int[][] ans=new int[m][n];
        int k=0;
        for(int i=0;i<m;i++){
            for(int j=0;j<n;j++){
                ans[i][j]=original[k++];
            }
        }
        return ans;
    }
```

Q2.
```Java
public int arrangeCoins(int n) {
         int i = 1; // which row we are on
		while(n > 0){ // checking to see if we have used all our coins
			i++; // increasing our row
			n = n-i; // adding coins to our row
		}
		return i-1;
    }
```

Q3.
```Java
public int[] sortedSquares(int[] nums) {
        int n = nums.length;
        int[] result = new int[n];
        int left = 0;
        int right = n - 1;
        int i = n - 1;

        while (left <= right) {
            int leftSquare = nums[left] * nums[left];
            int rightSquare = nums[right] * nums[right];

            if (leftSquare > rightSquare) {
                result[i] = leftSquare;
                left++;
            } else {
                result[i] = rightSquare;
                right--;
            }

            i--;
        }

        return result;
    }
```

Q4.
```Java
public List<List<Integer>> findDifference(int[] nums1, int[] nums2) {
        List<List<Integer>> ans = new ArrayList<>();
        HashSet<Integer> set1 = new HashSet<>();
        HashSet<Integer> set2 = new HashSet<>();
          
        for(int i = 0 ; i < nums1.length; i ++){
            set1.add(nums1[i]);
        }
          for(int i = 0 ; i < nums2.length; i ++){
            set2.add(nums2[i]);
        }
         List<Integer> list1 = new ArrayList<>();
          for(int i = 0 ; i < nums1.length; i ++){
            if(!set2.contains(nums1[i]) && !list1.contains(nums1[i])){
                list1.add(nums1[i]);
            }
        }
         ans.add(list1);
          List<Integer> list2 = new ArrayList<>();
          for(int i = 0 ; i < nums2.length; i ++){
            if(!set1.contains(nums2[i]) && !list2.contains(nums2[i])){
                list2.add(nums2[i]);
            }
        }
        ans.add(list2);
        return ans;
        

    }
```

Q5.
```Java
public int findTheDistanceValue(int[] arr1, int[] arr2, int d) {
        int ans=0;
        for (int i =0;i<arr1.length;i++){
            for (int j =0;j<arr2.length;j++){
                if (Math.abs(arr1[i]-arr2[j])<=d){
                   ans++;
                   break;
                }
            }
        }
        return (arr1.length-ans); 
    }
```

Q6.
```Java
public List<Integer> findDuplicates(int[] nums) {
       int n = nums.length;
        int[] cs = new int[n+1];
        ArrayList<Integer> al = new ArrayList<>();
        for(int i = 0; i < n; i++){
            cs[nums[i]] += 1;
        }
        for(int i = 0; i < cs.length; i++){
            if(cs[i] == 2){
                al.add(i);
            }
        }
        return al;
    }
        
    }
```

Q7.
```Java
public int findMin(int[] nums) {
        int n = nums.length;
        int flag = 0;
    
        for(int i=0; i<n-1; i++)
        {
            if(nums[i] > nums[i+1]) {
                flag = 1;
                break;
            }
        }

        if(flag == 0) {
            return nums[0];
        }
        
        int s = 0;
        int e = n-1;
        int mid = s + (e-s)/2;

        while(s<e) 
        {
            if(nums[0] <= nums[mid]) {
                s = mid+1;
            }
            else if(nums[0] > nums[mid]) {
                e = mid;
            }
            mid = s+(e-s)/2;
        }
        return nums[s];
    }
```

Q8.
```Java
public int[] findOriginalArray(int[] changed) {
        
        int len = changed.length;
        if((len&1) != 0) return new int[0];
        
        // Sorting the array
        Arrays.sort(changed);
        
        // Store frequencies in map
        Map<Integer,Integer> map = new HashMap<>();
        for(int e : changed) map.put(e,map.getOrDefault(e,0)+1);
        
        int[] res = new int[len/2];
        int k = 0;
        for(int i=0; i<len; i++){
            int ele = changed[i];
            
            // if map contains 'ele'
            if(map.containsKey(ele)){
                
                // if map contains 'ele*2'
                if(map.containsKey(ele*2)){
                    res[k++] = ele;
                    
                    // reduce frequency of 'ele' and 'ele*2' 
                    map.put(ele,map.get(ele)-1);
                    map.put(ele*2,map.get(ele*2)-1);
                    
                    // if freq of any key becomes <=0, remove it from map 
                    if(map.get(ele)<=0) map.remove(ele);
                    if(map.containsKey(ele*2) && map.get(ele*2)<=0) map.remove(ele*2);
                }
                else return new int[0];
            }
            
        }
        return res;
    }
```

Assignment-6
-------------

Q1.
```Java
public int[] diStringMatch(String s) {
        int[] result = new int[s.length() + 1];
        int end = result.length - 1, start = 0;
        int index = 0;
        while(index < s.length()){
            if(s.charAt(index) == 'I'){
                result[index] = start;   
                start++;
            }else{
                result[index] = end;
                end--;
            }
            index++;
        }
        result[result.length - 1] = start;
        return result;
    }
```

Q2.
```Java
public boolean searchMatrix(int[][] matrix, int target) {
        
     int n=matrix[0].length-1;
     for(int i=0;i<matrix.length;i++){
         if(target<=matrix[i][n]){
             int s=0;
             int e=n;
             while(s<=e){
                 int m=(s+e)/2;
                 if(matrix[i][m]==target) return true;
                 else if(matrix[i][m]<target){
                     s=m+1;
                 }else{
                     e=m-1;
                 }

             }


         }
     }
     return false;
```

Q3.
```Java
public boolean validMountainArray(int[] arr) {
        int n = arr.length;
        if (n < 3) return false; 
        int i = 0;
        while (i < n-1 && arr[i] < arr[i+1]) {
            i++;
        }
        if (i == 0 || i == n-1) return false;
        
        while (i < n-1 && arr[i] > arr[i+1]) {
            i++;
        }
        return i == n-1; 
    }
```

Q4.
```Java
public int findMaxLength(int[] nums) {
        HashMap<Integer,Integer>  hmap = new HashMap<>();
        int maxLength = 0;
        int sum = 0;
        for(int i = 0 ; i < nums.length; i++) {
            sum += (nums[i] == 0 ? -1 : nums[i]);
            if(sum == 0)
                maxLength = i+1;
            else if(hmap.containsKey(sum)) {
                maxLength = Math.max(maxLength,i - hmap.get(sum));
            }
            else 
                hmap.put(sum,i);
        }
        return maxLength;
    }
```

Q5.
```Java
public int minProductSum(int[] nums1, int[] nums2) {
        int ans = 0;
        // Sort nums1 and nums2 in ascending order.
        Arrays.sort(nums2);
        Arrays.sort(nums1);
        
        int i = 0;
        int j = nums2.length-1;
              
        while(i < nums1.length && j >= 0)
        {
            ans += nums1[i] * nums2[j];
            i++;
            j--;
        }
        
        return ans;
    }
```

Q6.
```Java
public int[] findOriginalArray(int[] changed) {
        
        int len = changed.length;
        if((len&1) != 0) return new int[0];
        
        // Sorting the array
        Arrays.sort(changed);
        
        // Store frequencies in map
        Map<Integer,Integer> map = new HashMap<>();
        for(int e : changed) map.put(e,map.getOrDefault(e,0)+1);
        
        int[] res = new int[len/2];
        int k = 0;
        for(int i=0; i<len; i++){
            int ele = changed[i];
            
            // if map contains 'ele'
            if(map.containsKey(ele)){
                
                // if map contains 'ele*2'
                if(map.containsKey(ele*2)){
                    res[k++] = ele;
                    
                    // reduce frequency of 'ele' and 'ele*2' 
                    map.put(ele,map.get(ele)-1);
                    map.put(ele*2,map.get(ele*2)-1);
                    
                    // if freq of any key becomes <=0, remove it from map 
                    if(map.get(ele)<=0) map.remove(ele);
                    if(map.containsKey(ele*2) && map.get(ele*2)<=0) map.remove(ele*2);
                }
                else return new int[0];
            }
            
        }
        return res;
    }
```

Q7.
```Java
public int[][] generateMatrix(int n) {
        int [][] a = new int[n][n];
        int l=0,t=0,b=n-1,r=n-1,v=1;
        while(t<=b||l<=r){
         if(t<=b){
             for(int i=l;i<=r;i++)
                a[t][i]=v++;
             t++;
         }
         if(l<=r){
             for(int i=t;i<=b;i++)
                 a[i][r]=v++;
             r--;
         }
         if(t<=b){
             for(int i=r;i>=l;i--)
             a[b][i]=v++;
             b--;
         }
         if(t<=b){
             for(int i=b;i>=t;i--)
             a[i][l]=v++;
         }
         l++;
        }
        return a;
    }
```

Q8.
```Java
public int[][] multiply(int[][] mat1, int[][] mat2) {
        int r1 = mat1.length, c1 = mat1[0].length, c2 = mat2[0].length;
        int[][] res = new int[r1][c2];
        Map<Integer, List<Integer>> mp = new HashMap<>();
        for (int i = 0; i < r1; ++i) {
            for (int j = 0; j < c1; ++j) {
                if (mat1[i][j] != 0) {
                    mp.computeIfAbsent(i, k -> new ArrayList<>()).add(j);
                }
            }
        }
        for (int i = 0; i < r1; ++i) {
            for (int j = 0; j < c2; ++j) {
                if (mp.containsKey(i)) {
                    for (int k : mp.get(i)) {
                        res[i][j] += mat1[i][k] * mat2[k][j];
                    }
                }
            }
        }
        return res;
    }
```
    
Assignment-7
------------

Q1.
```Java
public boolean isIsomorphic(String s, String t) {

        int map1[]=new int[200];
        int map2[]=new int[200];

        if(s.length()!=t.length())
            return false;


        for(int i=0;i<s.length();i++)
        {
            if(map1[s.charAt(i)]!=map2[t.charAt(i)])
                return false;

            map1[s.charAt(i)]=i+1;
            map2[t.charAt(i)]=i+1;
        }
        return true;
    }
```

Q2.
```Java
public boolean isStrobogrammatic(String num) {
        HashMap<Character, Character> dict = new HashMap<>();
        dict.put('0','0');
        dict.put('1','1');
        dict.put('8','8');
        dict.put('6','9');
        dict.put('9','6');
        int i=0; 
        int j = num.length()-1;
        while(i<=j){
            char f = num.charAt(i);
            char b = num.charAt(j);
            if(dict.containsKey(f) && dict.containsKey(b) && dict.get(f) == b){
                i++;j--;
            }else{
                return false;
            }
        }
        return true;

    }
```

Q3.
```Java
public String addStrings(String num1, String num2) {
        StringBuilder sb = new StringBuilder();

        int i = num1.length() - 1, j = num2.length() - 1;
        int carry = 0;

        while (i >= 0 || j >= 0) {
            int sum = carry;

            if (i >= 0) sum += (num1.charAt(i--) - '0');
            if (j >= 0) sum += (num2.charAt(j--) - '0');

            sb.append(sum % 10);
            carry = sum / 10;
        }

        if (carry != 0) sb.append(carry);
        return sb.reverse().toString();
    }
```

Q4.
```Java
public String reverseWords(String s) {
        int l=0;
        int r=0;
        char a[]=s.toCharArray();
        while(l<s.length()){
            while(r<s.length() && a[r]!=' '){    
                r++;
            }
            //reverse part
            
            //r-1 because r is pointing current at blank space
            //Let's
            //    |
            //    r
            reverse(a,l,r-1);             
            l=r+1;
            r=l;
        }
        return String.valueOf(a);
    }
     public String reverse(char s[],int l,int r){
         while(l<r){
             char temp=s[l];
             s[l]=s[r];
             s[r]=temp;
             l++;
             r--;
         }
         return String.valueOf(s);
     }
```

Q5.
```Java
public String reverseStr(String s, int k) {
        char[] str = s.toCharArray();
        int n = str.length;
        for(int i = 0 ; i <= n-1; i += 2*k){
            if(i+k-1 <= n-1){
                reverseK(i,i+k-1,str);
            }else{
				//for fewer than k characters left (edge case)
                reverseK(i,n-1,str);
            }
        }
        String ans = new String(str);
        return ans;
    }
    public void reverseK(int i, int j, char[] str){
        while(i < j){
            char temp = str[i];
            str[i] = str[j];
            str[j] = temp;
            i++;
            j--;
        }
    }
```

Q6.
```Java
public boolean rotateString(String s, String goal) {
        if(s ==null || goal == null){
            return false;
        }
        if(s.length() != goal.length()) return false;
        if(s.length() == 0){
            return true;
        }
        int i =0, j =0;
        while(i < s.length() && j < goal.length()){
            if(s.charAt(i) == goal.charAt(j)){
                i++; j++;
            }
            else{
                if(j == 0){
                    i++;
                }
                else{
                    j= 0;
                }
            }
        }
        return (s.substring(0,goal.length() - j).equals(goal.substring(j)));
    }
```

Q7.
```Java
public boolean backspaceCompare(String s, String t) {
        return buildString(s).equals(buildString(t));
    }

    private String buildString(String str) {
        Stack<Character> stack = new Stack<>();
        for (char c : str.toCharArray()) {
            if (c != '#') {
                stack.push(c);
            } else if (!stack.isEmpty()) {
                stack.pop();
            }
        }
        StringBuilder sb = new StringBuilder();
        while (!stack.isEmpty()) {
            sb.append(stack.pop());
        }
        return sb.toString();
    }
```

Q8.
```Java
public boolean checkStraightLine(int[][] c) {
        
        
        int xMove = c[1][0] - c[0][0];
        int yMove = c[1][1] - c[0][1];
        
        for(int i=1; i<c.length; i++){

            int x = c[i][0] - c[i-1][0];
            int y = c[i][1] - c[i-1][1];
            
// linear function -> y = k * x + b;
// Here need to discuss y = k * x;
// k = yMove / xMove;
// y * xMove = x * yMove;
            
            if(y * xMove != x * yMove) return false;
        }
```

Assignment-8
------------

Q1.
```Java
class Solution {
    int func(String s1, String s2, int i, int j, HashSet<Character> hs, int[][] dp) {
        if (i >= s1.length() || j >= s2.length()) {
            if (i >= s1.length()) {
                int x = 0;
                while (j < s2.length()) {
                    x += (int) s2.charAt(j);
                    j++;
                }
                return x;
            } else {
                int x = 0;
                while (i < s1.length()) {
                    x += (int) s1.charAt(i);
                    i++;
                }
                return x;
            }
        }
        if (dp[i][j] != 0) {
            return dp[i][j];
        }
        char a = s1.charAt(i);
        char b = s2.charAt(j);
        if (!hs.contains(a)) {
            dp[i][j] = func(s1, s2, i + 1, j, hs, dp) + (int) a;
        } else if (!hs.contains(b)) {
            dp[i][j] = func(s1, s2, i, j + 1, hs, dp) + (int) b;
        } else if (a == b) {
            dp[i][j] = func(s1, s2, i + 1, j + 1, hs, dp);
        } else {
            dp[i][j] = Math.min(func(s1, s2, i + 1, j, hs, dp) + (int) a, func(s1, s2, i, j + 1, hs, dp) + (int) b);
        }
        return dp[i][j];
    }
    
    public int minimumDeleteSum(String s1, String s2) {
        int[][] dp = new int[s1.length()][s2.length()];

        HashSet<Character> hs1 = new HashSet<>();
        HashSet<Character> hs2 = new HashSet<>();

        for (char c : s1.toCharArray()) {
            hs1.add(c);
        }

        for (char c : s2.toCharArray()) {
            hs2.add(c);
        }
        hs1.retainAll(hs2);
        
        return func(s1, s2, 0, 0, hs1, dp);
    }
}
```

Q2.
```Java
public boolean checkValidString(String s) {
        int openCount = 0;
        for (char c : s.toCharArray()) {
            if (c == '(') {
                openCount++;
            } else if (c == ')') {
                openCount--;
            }
            if (openCount < 0) return false;    // Currently, don't have enough open parentheses to match close parentheses-> Invalid
                                                // For example: ())(
        }
        return openCount == 0; // Fully match open parentheses with close parentheses
    }
```

Q3.
```Java
public int minDistance(String word1, String word2) {
        int m = word1.length();
        int n = word2.length();
        
        int[] dp = new int[n+1];
        // as java already contain 0 as default value no need to initailize the dp array
        for(int i = 1 ; i < m+1 ;i++){
            int[] temp = new int[n+1];
            for(int j = 1 ; j < n+1 ; j++){
                if(word1.charAt(i-1) == word2.charAt(j-1))
                     temp[j] = 1+dp[j-1];
                 
                 else
                     temp[j] = Math.max(dp[j] , temp[j-1]);       
            }
            dp = temp;
        }
         return m+n-(2*dp[n]);
     }
```

Q4.
```Java
StringBuilder sb;
    private void doEv(TreeNode root){
        if(root == null)return;
        if(root.left == null && root.right==null){
            sb.append(root.val);
            return;
        }
        sb.append(root.val);
        sb.append('(');
        doEv(root.left);
        sb.append(')');
        if(root.right!=null){
        sb.append('(');
        doEv(root.right);
        sb.append(')');
        }
        return;
    }
    public String tree2str(TreeNode t) {
        sb = new StringBuilder();
        doEv(t);
        return sb.toString();
    }
```

Q5.
```Java
public int compress(char[] chars) {
        String s="";
        int c=1;
        int i;
        for (i=0;i<chars.length-1;i++)
        {
            if(chars[i]==chars[i+1]){
                  c++;
            }else{
                if(c>1)s+=chars[i]+""+c;
                else s+=chars[i];
                c=1;
            }
        }
        if(c>1)s+=chars[i]+""+c;
        else s+=chars[i];
        int k=0;
        for(char c1:s.toCharArray())
        {
            chars[k++]=c1;
        }

        return s.length();
       

    }
```

Q6.
```Java
static boolean isequal(int counta[],int countb[]){
       
        boolean ans=true;
        for(int i=0;i<26;i++){
            if(counta[i]!=countb[i]){
                ans= false;
                break;
            }
        }
        return ans;

    }

    public List<Integer> findAnagrams(String s, String p) {
        int k=p.length();
        List<Integer> l=new ArrayList<>();
        if(s.length()<k){
            return l;
        }
        
        int counts[]=new int[26];
        int countp[]=new int[26];
        for(int i=0;i<k;i++){
            counts[s.charAt(i)-'a']++;
            countp[p.charAt(i)-'a']++;
        }
        if(isequal(counts,countp)){
            l.add(0);
        }
        for(int i=k;i<s.length();i++){
            counts[s.charAt(i)-'a']++;
            counts[s.charAt(i-k)-'a']--;
            if(isequal(counts,countp)){
                l.add(i-k+1);
            }
        }
        return l;
    }
```

Q7.
```Java
public String decodeString(String s) {
        Stack<Integer> is = new Stack<>();
        Stack<StringBuilder> ss = new Stack<>();

        int n = s.length(), num = 0;
        StringBuilder str = new StringBuilder();

        for(char ch : s.toCharArray()) {
            // There will be 4 types of characters --> number, [ , ], character

            if(ch >= '0' && ch <= '9') {
                num = (num * 10) + ch - '0';
            } else if(ch == '[') {
                ss.push(str);
                str = new StringBuilder();

                is.push(num);
                num = 0;
            } else if(ch == ']') {
                StringBuilder temp = str;
                str = ss.pop();
                int count = is.pop();

                while(count-- > 0) {
                    str.append(temp);
                }
            } else {
                str.append(ch);
            }
        }
        return str.toString();
    }
```

Q8.
```Java
public boolean buddyStrings(String s, String goal) {
        int m = s.length(), n = goal.length();
        if (m != n) {
            return false;
        }
        int diff = 0;
        int[] cnt1 = new int[26];
        int[] cnt2 = new int[26];
        for (int i = 0; i < n; ++i) {
            int a = s.charAt(i), b = goal.charAt(i);
            ++cnt1[a - 'a'];
            ++cnt2[b - 'a'];
            if (a != b) {
                ++diff;
            }
        }
        boolean f = false;
        for (int i = 0; i < 26; ++i) {
            if (cnt1[i] != cnt2[i]) {
                return false;
            }
            if (cnt1[i] > 1) {
                f = true;
            }
        }
        return diff == 2 || (diff == 0 && f);
    }

        
        return true;
    }
```


Assignment-9
------------

Q1.
```Java
public boolean isPowerOfTwo(int n) {
         if (n==0) return false;
       else if (n==1) return true;
       else if(n%2==0 && isPowerOfTwo(n/2)) return true;
       else return false;
        
    }
```

Q2.
```Java
public static int findSum(int n)
	 {
	 if (n <= 1)
	 {
	 return n;
	 }
	 else
	 {
	 return n + findSum(n - 1);
	 }
	 }
```

Q3.
```Java
static int factorial(int n)
    {
        if (n == 0)
            return 1;
  
        return n * factorial(n - 1);
    }
```

Q4.
```Java
public double myPow(double x, int n) {
        if(x == 1) return 1;
        if(n == -2147483648 && x > 1) return 0;
        if(n >= 0) return ans(x, n);
        else return 1 / ans(x, -1*n);
    }

    double ans(double x,int n){
        double ans = 1;
        while(n > 0){
            if((n & 1) == 1){
                ans *= x;
            }
            x *= x;
            n = n >> 1;
        }
        return ans;
    }
```

Q5.
```Java
public int findMaxRec(int A[], int n)
{
    if (n == 1)
        return A[0];
    return Math.max(A[n-1], findMaxRec(A, n-1));
}
```

Q6.
```Java
public static int Nth_of_AP(int a,
                                int d,
                                int N){
return ( a + (N - 1) * d );
}
```

Q7.
```Java
static void permute(String s, String answer)
    {
        if (s.length() == 0) {
            System.out.print(answer + "  ");
            return;
        }
 
        for (int i = 0; i < s.length(); i++) {
            char ch = s.charAt(i);
            String left_substr = s.substring(0, i);
            String right_substr = s.substring(i + 1);
            String rest = left_substr + right_substr;
            permute(rest, answer + ch);
        }
    }
```

Q8.
```Java
static int product(int[] arr,n)
    {
        if(n==1) return arr[0];
  
        return arr[n-1]*product(arr,n-1);
    }
```
    
 Assignment-10
 -------------

 Q1.
 ```Java
bool isPowerOfThree(int n) {
        if(n==1)return true;
        if(n==0 || n<0 || n%3 >0)return false;
        return isPowerOfThree(n/3);
    }
```

Q2.
```Java
public int lastRemaining(int n) {
        boolean left = true;
        int head = 1;
        int step = 1;
        int remain = n;
        while(remain > 1){
            if(left || remain % 2 == 1){
                head = head + step;
            }
            step = step * 2;
            remain = remain / 2;
            left = !left;
        }
        return head;
    }
```

Q3.
```Java
static void powerSet(String str, int index, String curr)
    {
        int n = str.length();
 
        // base case
        if (index == n) {
            return;
        }
        System.out.println(curr);
 
        // Try appending remaining characters
        // to current subset
        for (int i = index + 1; i < n; i++) {
            curr += str.charAt(i);
            powerSet(str, i, curr);
 
            curr = curr.substring(0, curr.length() - 1);
        }
    }
```

Q4.
```Java
private static int recLen(String str)
    {
        if (str.equals(""))
            return 0;
        else
            return recLen(str.substring(1)) + 1;
    }
```

Q5.
```Java
static boolean checkEquality(String s)
    {
        return (s.charAt(0) == s.charAt(s.length() - 1));
    }
      
    static int countSubstringWithEqualEnds(String s)
    {
        int result = 0;
        int n = s.length();
      
        // Starting point of substring
        for (int i = 0; i < n; i++)
           for (int len = 1; len <= n-i; len++)
              if (checkEquality(s.substring(i, i + len)))
                result++;
      
        return result;
    }
```

Q6.
```Java
public long toh(int n, int from, int to, int aux) {
       
       if(n<=0) return 0;


       long x = toh(n-1,from,aux,to);


       System.out.println("move disk "+n+" from rod "+from+" to rod "+        to);
       long y = toh(n-1,aux,to,from);
       
       return x+y+1; 
   }
```

Q7.
```Java
static void printPermutn(String str, String ans)
    {
 
       
        if (str.length() == 0) {
            System.out.print(ans + " ");
            return;
        }
 
        for (int i = 0; i < str.length(); i++) {
 
          
            char ch = str.charAt(i);
 
          
            String ros = str.substring(0, i) +
                        str.substring(i + 1);
 
         
            printPermutn(ros, ans + ch);
        }
    }
```

Q8.
```Java
static boolean isConsonant(char ch)
    {
      
        ch = Character.toUpperCase(ch);
       
        return !(ch == 'A' || ch == 'E' || 
                ch == 'I' || ch == 'O' || 
                ch == 'U') && ch >= 65 && ch <= 90;
    }
   
    static int totalConsonants(String str)
    {
        int count = 0;
        for (int i = 0; i < str.length(); i++) 
       
            
            if (isConsonant(str.charAt(i)))
                ++count;
        return count;
    }
```

Assignment-11
-------------

Q1.
```Java
public class Question01 {

	public static void main(String[] args) {
        int x = 4;

        int sqrt = mySqrt(x);

        System.out.println(sqrt); // Output: 2
    }

    public static int mySqrt(int x) {
        if (x == 0 || x == 1) {
            return x;
        }

        int left = 1;
        int right = x / 2;

        while (left <= right) {
            int mid = left + (right - left) / 2;

            if (mid == x / mid) {
                return mid;
            } else if (mid < x / mid) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }

        return right;
    }
	 
  }

```

Q2.
```Java
public class Question2 {
	 public int findPeakElement(int[] nums) {
	        int left = 0;
	        int right = nums.length - 1;
	        
	        while (left < right) {
	            int mid = left + (right - left) / 2;
	            
	            if (nums[mid] > nums[mid + 1]) {
	                right = mid;
	            } else {
	                left = mid + 1;
	            }
	        }
	        
	        return left;
	    }
	 
	 public static void main(String[] args) {
	        int[] nums = {1, 2, 3, 1};
	        
	        Question2 solution = new Question2();
	        int peakIndex = solution.findPeakElement(nums);
	        
	        System.out.println(peakIndex); // Output: 2
	    }
	 
}

```


Q3.
```Java
public class Question3 {
	 public int missingNumber(int[] nums) {
	        int n = nums.length;
	        int missing = n;
	        
	        for (int i = 0; i < n; i++) {
	            missing ^= nums[i];
	            missing ^= i;
	        }
	        
	        return missing;
	    }
	 public static void main(String[] args) {
	        int[] nums = {9,6,4,2,3,5,7,0,1};
	        
	        Question3 solution = new Question3();
	        int missingNumber = solution.missingNumber(nums);
	        
	        System.out.println(missingNumber); // Output: 2
	    }
}

```


Q4.
```Java
public class Question4 {

	public static void main(String[] args) {
        int[] nums = {1, 3, 4, 2, 2};
        
        Question4 solution = new Question4();
        int repeatedNumber = solution.findDuplicate(nums);
        
        System.out.println(repeatedNumber); // Output: 2
    }
	  public int findDuplicate(int[] nums) {
	        int slow = nums[0];
	        int fast = nums[0];
	        
	        // Find the meeting point inside the cycle
	        do {
	            slow = nums[slow];
	            fast = nums[nums[fast]];
	        } while (slow != fast);
	        
	        fast = nums[0];
	        
	        // Find the start of the cycle
	        while (slow != fast) {
	            slow = nums[slow];
	            fast = nums[fast];
	        }
	        
	        return slow;
	    }
   
}

```

Q5.
```Java
public class Question5 {
	
	

	public static void main(String[] args) {
        int[] nums1 = {1, 2, 2, 1};
        int[] nums2 = {2, 2};
        
        Question5 solution = new Question5();
        int[] intersection = solution.intersection(nums1, nums2);
        
        System.out.println(Arrays.toString(intersection)); // Output: [2]
    }
	 public int[] intersection(int[] nums1, int[] nums2) {
	        Set<Integer> set = new HashSet<>();
	        
	        for (int num : nums1) {
	            set.add(num);
	        }
	        
	        List<Integer> intersection = new ArrayList<>();
	        
	        for (int num : nums2) {
	            if (set.contains(num)) {
	                intersection.add(num);
	                set.remove(num);
	            }
	        }
	        
	        int[] result = new int[intersection.size()];
	        
	        for (int i = 0; i < intersection.size(); i++) {
	            result[i] = intersection.get(i);
	        }
	        
	        return result;
	    }
}



```

Q6.
```Java
public class Question6 {
	
	 public int findMin(int[] nums) {
	        int left = 0;
	        int right = nums.length - 1;
	        
	        while (left < right) {
	            int mid = left + (right - left) / 2;
	            
	            if (nums[mid] < nums[right]) {
	                right = mid;
	            } else {
	                left = mid + 1;
	            }
	        }
	        
	        return nums[left];
	    }
	 
	 public static void main(String[] args) {
	        int[] nums = {3, 4, 5, 1, 2};
	        
	        Question6 solution = new Question6();
	        int minElement = solution.findMin(nums);
	        
	        System.out.println(minElement); // Output: 1
	    }
    
}



```

Q7.
```Java
public class Question7 {
	 public int[] searchRange(int[] nums, int target) {
	        int[] result = {-1, -1};
	        
	        // Find the leftmost occurrence
	        int left = 0;
	        int right = nums.length - 1;
	        
	        while (left <= right) {
	            int mid = left + (right - left) / 2;
	            
	            if (nums[mid] == target) {
	                result[0] = mid;
	                right = mid - 1;
	            } else if (nums[mid] > target) {
	                right = mid - 1;
	            } else {
	                left = mid + 1;
	            }
	        }
	        
	        // Find the rightmost occurrence
	        left = 0;
	        right = nums.length - 1;
	        
	        while (left <= right) {
	            int mid = left + (right - left) / 2;
	            
	            if (nums[mid] == target) {
	                result[1] = mid;
	                left = mid + 1;
	            } else if (nums[mid] > target) {
	                right = mid - 1;
	            } else {
	                left = mid + 1;
	            }
	        }
	        
	        return result;
	    }
	 public static void main(String[] args) {
	        int[] nums = {5,7,7,8,8,10};
	        int target = 8;
	        
	        Question7 solution = new Question7();
	        int[] range = solution.searchRange(nums, target);
	        
	        System.out.println("Output: [" + range[0] + ", " + range[1] + "]"); // Output: [3, 4]
	    }
}

```

Q8.
```Java
public class Question8 {
	

	 public static void main(String[] args) {
	        int[] nums1 = {1, 2, 2, 1};
	        int[] nums2 = {2, 2};
	        
	        Question8 solution = new Question8();
	        int[] intersection = solution.intersect(nums1, nums2);
	        
	        System.out.println(Arrays.toString(intersection)); // Output: [2, 2]
	    }
	 public int[] intersect(int[] nums1, int[] nums2) {
	        Map<Integer, Integer> freqMap = new HashMap<>();
	        
	        for (int num : nums1) {
	            freqMap.put(num, freqMap.getOrDefault(num, 0) + 1);
	        }
	        
	        List<Integer> intersection = new ArrayList<>();
	        
	        for (int num : nums2) {
	            if (freqMap.containsKey(num) && freqMap.get(num) > 0) {
	                intersection.add(num);
	                freqMap.put(num, freqMap.get(num) - 1);
	            }
	        }
	        
	        int[] result = new int[intersection.size()];
	        
	        for (int i = 0; i < intersection.size(); i++) {
	            result[i] = intersection.get(i);
	        }
	        
	        return result;
	    }
   
}

```
Assignment-11
-------------

Q1.
```Java
class ListNode {
    int val;
    ListNode next;
    
    public ListNode(int val) {
        this.val = val;
    }
}

public class Question01 {

	

	
	    public static ListNode deleteMiddleNode(ListNode head) {
	        if (head == null || head.next == null) {
	            return null;
	        }
	        
	        ListNode slowPtr = head;
	        ListNode fastPtr = head;
	        ListNode prevPtr = null;
	        
	        while (fastPtr != null && fastPtr.next != null) {
	            fastPtr = fastPtr.next.next;
	            prevPtr = slowPtr;
	            slowPtr = slowPtr.next;
	        }
	        
	        prevPtr.next = slowPtr.next;
	        slowPtr.next = null;
	        
	        return head;
	    }
	    
	    public static void printLinkedList(ListNode head) {
	        ListNode curr = head;
	        while (curr != null) {
	            System.out.print(curr.val + " ");
	            curr = curr.next;
	        }
	        System.out.println();
	    }
	    
	    public static void main(String[] args) {
	        ListNode head = new ListNode(1);
	        head.next = new ListNode(2);
	        head.next.next = new ListNode(3);
	        head.next.next.next = new ListNode(4);
	        head.next.next.next.next = new ListNode(5);
	        
	        System.out.println("Original linked list:");
	        printLinkedList(head);
	        
	        head = deleteMiddleNode(head);
	        
	        System.out.println("Modified linked list:");
	        printLinkedList(head);
	    }
	}




```

Q2.
```Java

class LinkedListNode  {
    int val;
    LinkedListNode  next;
    
    public LinkedListNode (int val) {
        this.val = val;
    }
}

public class Question2 {
    public static boolean hasLoop(LinkedListNode  head) {
    	LinkedListNode  slowPtr = head;
    	LinkedListNode  fastPtr = head;
        
        while (fastPtr != null && fastPtr.next != null) {
            slowPtr = slowPtr.next;
            fastPtr = fastPtr.next.next;
            
            if (slowPtr == fastPtr) {
                return true; // Loop detected
            }
        }
        
        return false; // No loop found
    }
    
    public static void main(String[] args) {
    	LinkedListNode  head = new LinkedListNode (1);
        head.next = new LinkedListNode (3);
        head.next.next = new LinkedListNode (4);
        
        // Create a loop by connecting the tail to the second node
        head.next.next.next = head.next;
        
        boolean hasLoop = hasLoop(head);
        System.out.println("Does the linked list have a loop? " + hasLoop);
    }
}
```

Q3.
```Java
class ListNode {
    int val;
    ListNode next;

    public ListNode(int val) {
        this.val = val;
    }
}

public class Question3 {
    public static int findNthFromEnd(ListNode head, int N) {
        if (head == null || N <= 0) {
            return -1;
        }

        ListNode slowPtr = head;
        ListNode fastPtr = head;

        // Move the fast pointer N positions ahead
        for (int i = 0; i < N; i++) {
            if (fastPtr == null) {
                return -1; // N is greater than the length of the linked list
            }
            fastPtr = fastPtr.next;
        }

        // Move both pointers until the fast pointer reaches the end
        while (fastPtr != null) {
            slowPtr = slowPtr.next;
            fastPtr = fastPtr.next;
        }

        // At this point, the slow pointer is at the Nth node from the end
        return slowPtr.val;
    }

    public static void main(String[] args) {
        ListNode head = new ListNode(1);
        head.next = new ListNode(2);
        head.next.next = new ListNode(3);
        head.next.next.next = new ListNode(4);
        head.next.next.next.next = new ListNode(5);
        head.next.next.next.next.next = new ListNode(6);
        head.next.next.next.next.next.next = new ListNode(7);
        head.next.next.next.next.next.next.next = new ListNode(8);
        head.next.next.next.next.next.next.next.next = new ListNode(9);

        int N = 2;
        int result = findNthFromEnd(head, N);
        System.out.println("Nth node from the end: " + result);
    }
}




```

Q4.
```Java
class ListNode {
    char val;
    ListNode next;
    
    public ListNode(char val) {
        this.val = val;
    }
}

public class Question4 {
    public static boolean isPalindrome(ListNode head) {
        if (head == null || head.next == null) {
            return true;
        }
        
        ListNode slowPtr = head;
        ListNode fastPtr = head;
        
        // Move slowPtr to the middle of the linked list and reverse the first half
        ListNode prev = null;
        while (fastPtr != null && fastPtr.next != null) {
            fastPtr = fastPtr.next.next;
            
            ListNode next = slowPtr.next;
            slowPtr.next = prev;
            prev = slowPtr;
            slowPtr = next;
        }
        
        // If the linked list has an odd number of nodes, move slowPtr one step forward
        if (fastPtr != null) {
            slowPtr = slowPtr.next;
        }
        
        // Compare the reversed first half with the second half
        while (slowPtr != null) {
            if (slowPtr.val != prev.val) {
                return false; // Not a palindrome
            }
            slowPtr = slowPtr.next;
            prev = prev.next;
        }
        
        return true; // Palindrome
    }
    
    public static void main(String[] args) {
        ListNode head1 = new ListNode('R');
        head1.next = new ListNode('A');
        head1.next.next = new ListNode('D');
        head1.next.next.next = new ListNode('A');
        head1.next.next.next.next = new ListNode('R');
        
        boolean isPalindrome1 = isPalindrome(head1);
        System.out.println("Is the linked list a palindrome? " + (isPalindrome1 ? "Yes" : "No"));
        
        ListNode head2 = new ListNode('C');
        head2.next = new ListNode('O');
        head2.next.next = new ListNode('D');
        head2.next.next.next = new ListNode('E');
        
        boolean isPalindrome2 = isPalindrome(head2);
        System.out.println("Is the linked list a palindrome? " + (isPalindrome2 ? "Yes" : "No"));
    }
}

```

Q5.
```Java
class ListNode {
    int val;
    ListNode next;

    public ListNode(int val) {
        this.val = val;
    }
}

public class Question5 {
    public static void removeLoop(ListNode head) {
        if (head == null || head.next == null) {
            return;
        }

        ListNode slowPtr = head;
        ListNode fastPtr = head;
        ListNode loopNode = null;

        // Detect the loop using Floyd's cycle detection algorithm
        while (fastPtr != null && fastPtr.next != null) {
            slowPtr = slowPtr.next;
            fastPtr = fastPtr.next.next;

            if (slowPtr == fastPtr) {
                loopNode = slowPtr;
                break;
            }
        }

        // If a loop is found, remove it
        if (loopNode != null) {
            slowPtr = head;

            // If the loop starts at the head of the linked list
            if (slowPtr == loopNode) {
                while (fastPtr.next != slowPtr) {
                    fastPtr = fastPtr.next;
                }
            } else {
                while (slowPtr.next != fastPtr.next) {
                    slowPtr = slowPtr.next;
                    fastPtr = fastPtr.next;
                }
            }

            // Remove the loop by setting the next pointer of the last node to null
            fastPtr.next = null;
        }
    }

    public static void printLinkedList(ListNode head) {
        ListNode curr = head;
        while (curr != null) {
            System.out.print(curr.val + " ");
            curr = curr.next;
        }
        System.out.println();
    }

    public static void main(String[] args) {
        ListNode head = new ListNode(1);
        head.next = new ListNode(3);
        head.next.next = new ListNode(4);
        head.next.next.next = head.next; // Creating a loop at position X = 2

        System.out.println("Original linked list:");
        printLinkedList(head);

        removeLoop(head);

        System.out.println("Modified linked list:");
        printLinkedList(head);
    }
}

```

Q6.
```Java
class ListNode {
    int val;
    ListNode next;

    public ListNode(int val) {
        this.val = val;
    }
}

public class Question6 {
    public static ListNode retainAndDelete(ListNode head, int M, int N) {
        if (head == null || M <= 0 || N <= 0) {
            return head;
        }

        ListNode curr = head;
        int count;

        while (curr != null) {
            // Retain M nodes
            for (count = 1; count < M && curr != null; count++) {
                curr = curr.next;
            }

            if (curr == null) {
                break;
            }

            // Delete N nodes
            ListNode next = curr.next;
            for (count = 1; count <= N && next != null; count++) {
                next = next.next;
            }

            curr.next = next; // Connect the last retained node to the next node after deleted nodes
            curr = next; // Move to the next retained node
        }

        return head;
    }

    public static void printLinkedList(ListNode head) {
        ListNode curr = head;
        while (curr != null) {
            System.out.print(curr.val + " ");
            curr = curr.next;
        }
        System.out.println();
    }

    public static void main(String[] args) {
        ListNode head1 = new ListNode(1);
        head1.next = new ListNode(2);
        head1.next.next = new ListNode(3);
        head1.next.next.next = new ListNode(4);
        head1.next.next.next.next = new ListNode(5);
        head1.next.next.next.next.next = new ListNode(6);
        head1.next.next.next.next.next.next = new ListNode(7);
        head1.next.next.next.next.next.next.next = new ListNode(8);

        System.out.println("Original linked list:");
        printLinkedList(head1);

        int M1 = 2;
        int N1 = 2;
        ListNode modifiedHead1 = retainAndDelete(head1, M1, N1);

        System.out.println("Modified linked list:");
        printLinkedList(modifiedHead1);

        ListNode head2 = new ListNode(1);
        head2.next = new ListNode(2);
        head2.next.next = new ListNode(3);
        head2.next.next.next = new ListNode(4);
        head2.next.next.next.next = new ListNode(5);
        head2.next.next.next.next.next = new ListNode(6);
        head2.next.next.next.next.next.next = new ListNode(7);
        head2.next.next.next.next.next.next.next = new ListNode(8);
        head2.next.next.next.next.next.next.next.next = new ListNode(9);
        head2.next.next.next.next.next.next.next.next.next = new ListNode(10);

        System.out.println("Original linked list:");
        printLinkedList(head2);

        int M2 = 3;
        int N2 = 2;
        ListNode modifiedHead2 = retainAndDelete(head2, M2, N2);

        System.out.println("Modified linked list:");
        printLinkedList(modifiedHead2);

        ListNode head3 = new ListNode(1);
        head3.next = new ListNode(2);
        head3.next.next = new ListNode(3);
        head3.next.next.next = new ListNode(4);
        head3.next.next.next.next = new ListNode(5);
        head3.next.next.next.next.next = new ListNode(6);
        head3.next.next.next.next.next.next = new ListNode(7);
        head3.next.next.next.next.next.next.next = new ListNode(8);
        head3.next.next.next.next.next.next.next.next = new ListNode(9);
        head3.next.next.next.next.next.next.next.next.next = new ListNode(10);

        System.out.println("Original linked list:");
        printLinkedList(head3);

        int M3 = 1;
        int N3 = 1;
        ListNode modifiedHead3 = retainAndDelete(head3, M3, N3);

        System.out.println("Modified linked list:");
        printLinkedList(modifiedHead3);
    }
}


```

Q7.
```Java
class Node {
    int data;
    Node next;

    public Node(int data) {
        this.data = data;
        this.next = null;
    }
}

public class Question7 {
    public static void mergeLists(Node first, Node second) {
        if (first == null || second == null) {
            return;
        }

        Node firstCurrent = first;
        Node secondCurrent = second;

        while (firstCurrent != null && secondCurrent != null) {
            Node firstNext = firstCurrent.next;
            Node secondNext = secondCurrent.next;

            firstCurrent.next = secondCurrent;
            secondCurrent.next = firstNext;

            firstCurrent = firstNext;
            secondCurrent = secondNext;
        }

        second = secondCurrent;
    }

    public static void printList(Node head) {
        Node current = head;
        while (current != null) {
            System.out.print(current.data + " ");
            current = current.next;
        }
        System.out.println();
    }

    public static void main(String[] args) {
        Node first = new Node(5);
        first.next = new Node(7);
        first.next.next = new Node(17);
        first.next.next.next = new Node(13);
        first.next.next.next.next = new Node(11);

        Node second = new Node(12);
        second.next = new Node(10);
        second.next.next = new Node(2);
        second.next.next.next = new Node(4);
        second.next.next.next.next = new Node(6);

        System.out.println("Before merging:");
        System.out.print("First list: ");
        printList(first);
        System.out.print("Second list: ");
        printList(second);

        mergeLists(first, second);

        System.out.println("After merging:");
        System.out.print("First list: ");
        printList(first);
        System.out.print("Second list: ");
        printList(second);
    }
}

```

Q8.
```Java
class ListNode {
    int val;
    ListNode next;

    public ListNode(int val) {
        this.val = val;
        this.next = null;
    }
}

public class Question8 {
    public static boolean isCircular(ListNode head) {
        if (head == null || head.next == null) {
            return false;
        }

        ListNode slowPtr = head;
        ListNode fastPtr = head.next;

        while (fastPtr != null && fastPtr.next != null) {
            if (slowPtr == fastPtr || slowPtr == fastPtr.next) {
                return true; // Linked list is circular
            }
            slowPtr = slowPtr.next;
            fastPtr = fastPtr.next.next;
        }

        return false; // Linked list is not circular
    }

    public static void main(String[] args) {
        ListNode head = new ListNode(1);
        head.next = new ListNode(2);
        head.next.next = new ListNode(3);
        head.next.next.next = new ListNode(4);
        head.next.next.next.next = head; // Make the list circular

        boolean isCircular = isCircular(head);
        System.out.println("Is the linked list circular? " + (isCircular ? "Yes" : "No"));
    }
}



```

Assignment-11
-------------

Q1.
```Java
class ListNode {
    int val;
    ListNode next;

    public ListNode(int val) {
        this.val = val;
        this.next = null;
    }
}

public class Question01 {
    public static ListNode createNewList(ListNode list1, ListNode list2) {
        ListNode head = null;
        ListNode tail = null;

        while (list1 != null && list2 != null) {
            int val1 = list1.val;
            int val2 = list2.val;

            int greaterVal = Math.max(val1, val2);
            ListNode newNode = new ListNode(greaterVal);

            if (head == null) {
                head = newNode;
                tail = newNode;
            } else {
                tail.next = newNode;
                tail = tail.next;
            }

            list1 = list1.next;
            list2 = list2.next;
        }

        return head;
    }

    public static void printList(ListNode head) {
        ListNode current = head;
        while (current != null) {
            System.out.print(current.val + " ");
            current = current.next;
        }
        System.out.println();
    }

    public static void main(String[] args) {
        // Example 1
        ListNode list1 = new ListNode(5);
        list1.next = new ListNode(2);
        list1.next.next = new ListNode(3);
        list1.next.next.next = new ListNode(8);

        ListNode list2 = new ListNode(1);
        list2.next = new ListNode(7);
        list2.next.next = new ListNode(4);
        list2.next.next.next = new ListNode(5);

        ListNode newList = createNewList(list1, list2);
        System.out.print("New list: ");
        printList(newList);

        // Example 2
        ListNode list3 = new ListNode(2);
        list3.next = new ListNode(8);
        list3.next.next = new ListNode(9);
        list3.next.next.next = new ListNode(3);

        ListNode list4 = new ListNode(5);
        list4.next = new ListNode(3);
        list4.next.next = new ListNode(6);
        list4.next.next.next = new ListNode(4);

        ListNode newList2 = createNewList(list3, list4);
        System.out.print("New list: ");
        printList(newList2);
    }
}

```

Q2.
```Java
class ListNode {
    int val;
    ListNode next;

    public ListNode(int val) {
        this.val = val;
        this.next = null;
    }
}

public class Question2 {
    public static ListNode removeDuplicates(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        }

        ListNode current = head;

        while (current != null && current.next != null) {
            if (current.val == current.next.val) {
                current.next = current.next.next;
            } else {
                current = current.next;
            }
        }

        return head;
    }

    public static void printList(ListNode head) {
        ListNode current = head;
        while (current != null) {
            System.out.print(current.val + " ");
            current = current.next;
        }
        System.out.println();
    }

    public static void main(String[] args) {
        ListNode head = new ListNode(11);
        head.next = new ListNode(11);
        head.next.next = new ListNode(11);
        head.next.next.next = new ListNode(21);
        head.next.next.next.next = new ListNode(43);
        head.next.next.next.next.next = new ListNode(43);
        head.next.next.next.next.next.next = new ListNode(60);

        System.out.print("Original list: ");
        printList(head);

        ListNode newList = removeDuplicates(head);
        System.out.print("List after removing duplicates: ");
        printList(newList);
    }
}


```

Q3.
```Java
class ListNode {
    int val;
    ListNode next;

    public ListNode(int val) {
        this.val = val;
        this.next = null;
    }
}

public class Question3 {
    public static ListNode reverseKGroup(ListNode head, int k) {
        if (head == null || head.next == null || k == 1) {
            return head;
        }

        ListNode dummy = new ListNode(0);
        dummy.next = head;
        ListNode prevGroupTail = dummy;
        ListNode current = head;
        int count = 0;

        while (current != null) {
            count++;
            if (count % k == 0) {
                prevGroupTail = reverseGroup(prevGroupTail, current.next);
                current = prevGroupTail.next;
            } else {
                current = current.next;
            }
        }

        return dummy.next;
    }

    public static ListNode reverseGroup(ListNode prevGroupTail, ListNode nextGroupHead) {
        ListNode prev = prevGroupTail.next;
        ListNode current = prev.next;

        while (current != nextGroupHead) {
            ListNode next = current.next;
            current.next = prev;
            prev = current;
            current = next;
        }

        ListNode groupHead = prevGroupTail.next;
        groupHead.next = nextGroupHead;
        prevGroupTail.next = prev;

        return groupHead;
    }

    public static void printList(ListNode head) {
        ListNode current = head;
        while (current != null) {
            System.out.print(current.val + " ");
            current = current.next;
        }
        System.out.println();
    }

    public static void main(String[] args) {
        ListNode head = new ListNode(1);
        head.next = new ListNode(2);
        head.next.next = new ListNode(3);
        head.next.next.next = new ListNode(4);
        head.next.next.next.next = new ListNode(5);

        int k = 3;

        System.out.print("Original list: ");
        printList(head);

        ListNode reversed = reverseKGroup(head, k);

        System.out.print("Reversed list: ");
        printList(reversed);
    }
}

```

Q4.
```Java
class ListNode {
    int val;
    ListNode next;
    
    public ListNode(int val) {
        this.val = val;
    }
}

public class Question4 {
    public static ListNode reverseAlternateKNodes(ListNode head, int k) {
        if (head == null || k <= 1) {
            return head;
        }

        ListNode current = head;
        ListNode previous = null;

        // Reverse k nodes
        int count = 0;
        while (current != null && count < k) {
            ListNode nextNode = current.next;
            current.next = previous;
            previous = current;
            current = nextNode;
            count++;
        }

        // Skip the next k nodes
        count = 0;
        while (current != null && count < k) {
            current = current.next;
            count++;
        }

        // Recursively reverse the remaining alternate k nodes
        if (current != null) {
            head.next = reverseAlternateKNodes(current, k);
        }

        return previous;
    }

    public static void printList(ListNode head) {
        ListNode current = head;
        while (current != null) {
            System.out.print(current.val + " ");
            current = current.next;
        }
        System.out.println();
    }

    public static void main(String[] args) {
        ListNode head = new ListNode(1);
        head.next = new ListNode(2);
        head.next.next = new ListNode(3);
        head.next.next.next = new ListNode(5);
        head.next.next.next.next = new ListNode(2);
        head.next.next.next.next.next = new ListNode(10);

        int k = 2;

        System.out.println("Original list:");
        printList(head);

        head = reverseAlternateKNodes(head, k);

        System.out.println("Reversed list:");
        printList(head);
    }
}

```

Q5.
```Java
class ListNode {
    int val;
    ListNode next;
    
    public ListNode(int val) {
        this.val = val;
    }
}

public class Question5 {
    public static ListNode deleteLastOccurrence(ListNode head, int key) {
        if (head == null)
            return null;

        ListNode prev = null;
        ListNode lastOccurrence = null;
        ListNode current = head;
        ListNode nextNode = null;

        // Find the last occurrence of the key
        while (current != null) {
            if (current.val == key)
                lastOccurrence = prev;
            prev = current;
            current = current.next;
        }

        // If last occurrence is found, delete the node
        if (lastOccurrence != null) {
            nextNode = lastOccurrence.next;
            lastOccurrence.next = nextNode.next;
        } else {
            // If last occurrence is the head node, update the head
            nextNode = head;
            head = head.next;
        }

        // Clean up memory
        nextNode.next = null;

        return head;
    }

    public static void printList(ListNode head) {
        ListNode current = head;
        while (current != null) {
            System.out.print(current.val + " ");
            current = current.next;
        }
        System.out.println();
    }

    public static void main(String[] args) {
        ListNode head = new ListNode(1);
        head.next = new ListNode(2);
        head.next.next = new ListNode(3);
        head.next.next.next = new ListNode(5);
        head.next.next.next.next = new ListNode(2);
        head.next.next.next.next.next = new ListNode(10);

        int key = 2;

        System.out.println("Original list:");
        printList(head);

        head = deleteLastOccurrence(head, key);

        System.out.println("Modified list:");
        printList(head);
    }
}

```

Q6.
```Java
class ListNode {
    int val;
    ListNode next;

    public ListNode(int val) {
        this.val = val;
    }
}

public class Question6 {
    public static ListNode mergeSortedLists(ListNode a, ListNode b) {
        // Create a dummy node as the head of the merged list
        ListNode dummyNode = new ListNode(0);
        ListNode current = dummyNode;

        // Traverse both lists and compare the nodes
        while (a != null && b != null) {
            if (a.val <= b.val) {
                current.next = a;
                a = a.next;
            } else {
                current.next = b;
                b = b.next;
            }
            current = current.next;
        }

        // Attach the remaining nodes of the non-empty list
        if (a != null) {
            current.next = a;
        } else if (b != null) {
            current.next = b;
        }

        // Return the head of the merged list
        return dummyNode.next;
    }

    public static void printList(ListNode head) {
        ListNode current = head;
        while (current != null) {
            System.out.print(current.val + " ");
            current = current.next;
        }
        System.out.println();
    }

    public static void main(String[] args) {
        ListNode a = new ListNode(5);
        a.next = new ListNode(10);
        a.next.next = new ListNode(15);

        ListNode b = new ListNode(2);
        b.next = new ListNode(3);
        b.next.next = new ListNode(20);

        System.out.println("List a:");
        printList(a);

        System.out.println("List b:");
        printList(b);

        ListNode merged = mergeSortedLists(a, b);

        System.out.println("Merged list:");
        printList(merged);
    }
}

```

Q7.
```Java
class Node {
    int data;
    Node prev;
    Node next;

    public Node(int data) {
        this.data = data;
    }
}

public class Question7 {
    public static Node reverseDoublyLinkedList(Node head) {
        if (head == null || head.next == null) {
            return head;
        }

        Node current = head;
        Node previous = null;

        while (current != null) {
            // Swap previous and next pointers
            Node temp = current.next;
            current.next = previous;
            current.prev = temp;

            // Move to the next nodes
            previous = current;
            current = temp;
        }

        // Update the head to the last node
        head = previous;

        return head;
    }

    public static void printList(Node head) {
        Node current = head;
        while (current != null) {
            System.out.print(current.data + " ");
            current = current.next;
        }
        System.out.println();
    }

    public static void main(String[] args) {
        // Create the original doubly linked list
        Node head = new Node(10);
        Node node1 = new Node(8);
        Node node2 = new Node(4);
        Node node3 = new Node(2);

        head.next = node1;
        node1.prev = head;
        node1.next = node2;
        node2.prev = node1;
        node2.next = node3;
        node3.prev = node2;

        System.out.println("Original Linked List:");
        printList(head);

        // Reverse the doubly linked list
        head = reverseDoublyLinkedList(head);

        System.out.println("Reversed Linked List:");
        printList(head);
    }
}

```

Q.8
```Java
class Node {
    int data;
    Node prev;
    Node next;

    public Node(int data) {
        this.data = data;
    }
}

public class Question8 {
    public static Node deleteNode(Node head, int position) {
        if (head == null)
            return null;

        // Case 1: Deleting the head node
        if (position == 1) {
            Node newHead = head.next;
            if (newHead != null)
                newHead.prev = null;
            head.next = null;
            return newHead;
        }

        Node current = head;
        int count = 1;

        // Traverse to the position to be deleted
        while (current != null && count < position) {
            current = current.next;
            count++;
        }

        // Case 2: Deleting a node
        if (current != null) {
            // Update the previous node's next pointer
            if (current.prev != null)
                current.prev.next = current.next;

            // Update the next node's previous pointer
            if (current.next != null)
                current.next.prev = current.prev;

            // Disconnect the current node
            current.prev = null;
            current.next = null;
        }

        return head;
    }

    public static void printList(Node head) {
        Node current = head;
        while (current != null) {
            System.out.print(current.data + " ");
            current = current.next;
        }
        System.out.println();
    }

    public static void main(String[] args) {
        // Create the doubly linked list
        Node head = new Node(1);
        Node node1 = new Node(3);
        Node node2 = new Node(4);

        head.next = node1;
        node1.prev = head;
        node1.next = node2;
        node2.prev = node1;

        System.out.println("Original Doubly Linked List:");
        printList(head);

        int positionToDelete = 3;
        head = deleteNode(head, positionToDelete);

        System.out.println("Doubly Linked List after deleting node at position " + positionToDelete + ":");
        printList(head);
    }
}
```
