# 算法笔记

### 1. 时间复杂度和空间复杂度

``` 
常见的七种时间复杂度
```
![1574174177351](C:\Users\Mechrevo\AppData\Roaming\Typora\typora-user-images\1574174177351.png)


####   1. 常数复杂度
![1574175041189](C:\Users\Mechrevo\AppData\Roaming\Typora\typora-user-images\1574175041189.png)

#### 2. 线性时间复杂度
![1574175345790](C:\Users\Mechrevo\AppData\Roaming\Typora\typora-user-images\1574175345790.png)

#### 3. 跳表

```
升维, 时间换空间, 提升查询速度
```

#### 4. 移动0

```
方法一: 
1. 定义索引j记录0的位置;
2. 遍历数组, 非0数字放到j的index,j向前移动,i!=j,index[i]置0;
```
```java
class Solution {
    public void moveZeroes(int[] nums) {
         if (nums == null || nums.length == 1) {
            return;
        }
        // j 记录0的位置
        int j = 0;
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] != 0) {
                nums[j] = nums[i];
                if (i != j) {
                    nums[i] = 0; 
                }
                j++;
            }
        }
    }
}
```

#### 5. 三数之和

```
方法一:
1. 将数组排序
2. 遍历数组,固定muns[i], 匹配右侧L~R; 去重;
```
![1574259995051](C:\Users\Mechrevo\AppData\Roaming\Typora\typora-user-images\1574259995051.png)

![1574261038068](C:\Users\Mechrevo\AppData\Roaming\Typora\typora-user-images\1574261038068.png)

![1574261056076](C:\Users\Mechrevo\AppData\Roaming\Typora\typora-user-images\1574261056076.png)

```java
 public List<List<Integer>> threeSum(int[] nums) {
        List<List<Integer>> lists = new ArrayList<>();
        int length = nums.length;
        if (nums == null || length < 3) {
            return lists;
        }
        // 排序
        Arrays.sort(nums);
        for (int i = 0; i < length; i++) {
            // 大于0的数, 三数之和不可能等于0
            if (nums[i] > 0) {
                continue;
            }
            // 去除重复元素
            if (i > 0 && nums[i] == nums[i - 1]) {
                continue;
            }
            int left = i + 1;
            int right = length - 1;
            while (left < right) {
                int sum = nums[left] + nums[right] + nums[i];
                if (sum == 0) {
                    lists.add(Arrays.asList(nums[left], nums[i], nums[right]));
                    // 去除重复元素
                    while (left < right && nums[left] == nums[left + 1]) {
                        left++;
                    }
                    // 去除重复元素
                    while (left < right && nums[right] == nums[right - 1]) {
                        right--;
                    }
                    left++;
                    right--;
                } else if (sum > 0) {
                    right--;
                } else {
                    left++;
                }
            }
        }
        return lists;
    }
```

#### 6. 旋转数组

```java
class Solution {
    public void rotate(int[] nums, int k) {
       int length = nums.length;
        // 使用新的数组
        int[] newNums = new int[length];
        for (int i = 0; i < length; i++) {
            newNums[(i + k) % length] = nums[i];
        }
        for (int i = 0; i < nums.length; i++) {
            nums[i] = newNums[i];
        }
    }
}
```

