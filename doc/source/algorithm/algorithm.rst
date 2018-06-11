Art of computer - algorithm
=============================

算法的评估
-----------

* O
* Ω
* θ

快速排序算法
------------

算法复杂度
^^^^^^^^^^^^^^^

快速排序的时间复杂度为θ(n2),虽然最坏情况下时间复杂度很差，但快速排序通常在实际应用中是最好的选择，因为他的平均性能好。


算法基本思想
^^^^^^^^^^^^^^^^


* 分解
	
	将数组A[p..r]划分为两个（可能为空）子数组A[p, q-1] 和 A[q+1, r]。使得A[p, q-1]中的每个元素小于等于A[q], A[q+1, r]中的每个元素大于等于A[q];

* 解决

	通过递归调用快速排序，对子数组A[p, q-1] 和 A[q+1, r]进行排序。

* 归并
	
	因为子数组都是原址排序的，所以不需要合并操作


伪代码
^^^^^^^^^

.. code-block:: c++

QUICK_SORT(A, p, r):
	if(p < r)
		q = PARTITION(A, p, r)
		QUICK_SORT(A, p, q-1)
		QUICK_SORT(A, q+1, r)


PARTITION(A, p, r)
	x = A[r]
	i = p-1
	for j = p to r-1
		if A[j] <= x
			i = i+1
			exchange A[i] with A[j]

exchange A[i+1] with A[r]
return i+1


快速排序的随机化版本
^^^^^^^^^^^^^^^^^^^^^^^

上面的版本中A[r]称作主元，在随机化版本里面，主元是随机抽取。然后跟A[r]交换。

.. code-block:: c++

	RANDOMIZED-PARTITION(A, p, r)
		i = RANDOM(p, r)
		exchange A[i] with A[r]

随机化版本性能
^^^^^^^^^^^^^^^

todo

			
冒泡排序算法
------------

插入排序
--------

归并排序
--------
