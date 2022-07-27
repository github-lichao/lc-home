### 快速排序

快速排序又是一种**分而治之**思想在排序算法上的典型应用。本质上来看, 快速排序应该算是在冒泡排序基础上的递归分治法。

快速排序的名字起的是简单粗暴, 虽然 Worst Case 的时间复杂度达到了 O(n²), 但是在大多数情况下都比平均时间复杂度为 O(n logn) 的排序算法表现要更好, 这是为什么呢? 在《算法艺术与信息学竞赛》上的解释：

> 快速排序的最坏运行情况是 O(n²), 比如说顺序数列的快排。但它的平摊期望时间是 O(nlogn), 且 O(nlogn) 记号中隐含的常数因子很小, 比复杂度稳定等于 O(nlogn) 的归并排序要小很多。所以, 对绝大多数顺序性较弱的随机数列而言, 快速排序总是优于归并排序。

快速排序算法步骤:
1. 从数列中挑出一个元素, 称为 “基准”（pivot）
2. 重新排序数列, 所有元素比基准值小的摆放在基准前面, 所有元素比基准值大的摆在基准的后面（相同的数可以到任一边）。在这个分区退出之后, 该基准就处于数列的中间位置。这个称为分区（partition）操作；
3. 递归地（recursive）把小于基准值元素的子数列和大于基准值元素的子数列排序；

```js
function sortArray(nums) {
  quickSort(0, nums.length - 1, nums);
  return nums;
}

function quickSort(start, end, arr) {
  if (start < end) {
    const mid = sort(start, end, arr);
    quickSort(start, mid - 1, arr);
    quickSort(mid + 1, end, arr);
  }
}

function sort(start, end, arr) {
  const base = arr[start];
  let left = start;
  let right = end;
  while (left !== right) {
    while (arr[right] >= base && right > left) {
      right--;
    }
    arr[left] = arr[right];
    while (arr[left] <= base && right > left) {
      left++;
    }
    arr[right] = arr[left];
  }
  arr[left] = base;
  return left;
}
```