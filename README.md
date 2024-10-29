https://1drv.ms/b/s!AiMXIn2bEgCcmUpgvREzHAv3cJI-?e=G8QFdp

135. Kẹo
Có trẻ em đứng xếp hàng. Mỗi đứa trẻ được gán một xếp hạng giá trị được đưa ra trong xếp hạng mảng số nguyên.

Bạn đang tặng kẹo cho các em với điều kiện sau:

Mỗi đứa trẻ phải có ít nhất một viên kẹo.
Những đứa trẻ có điểm xếp hạng cao hơn sẽ nhận được nhiều kẹo hơn những đứa trẻ hàng xóm.
Trả lại số kẹo tối thiểu bạn cần để phân phát kẹo cho trẻ em.


class Solution:
    def candy(self, ratings):
        n = len(ratings) 
        candy = [1] * n 
        # Left to right pass
        for i in range(1, n):
            if ratings[i] > ratings[i - 1]:
                candy[i] = candy[i - 1] + 1
        # Right to left pass and summing
        for i in range(n - 2, -1, -1):
            if ratings[i] > ratings[i + 1]:
                candy[i] = max(candy[i], candy[i + 1] + 1)
        # Add the last child's candy
        ans = sum(candy)
        return ans

        ratings = [3 4 3 2 3 1]
        n = 6
        candy = [1 1 1 1 1 1]
        candy = [1 2 1 1 2 1]
        candy = [1 3 2 1 2 1]
        -> ans = 10

134.Trạm xăng

Có những trạm xăng dọc theo tuyến đường tròn, trong đó lượng xăng tại trạm thứ i là gas[i].

Bạn có một chiếc ô tô với bình xăng không giới hạn và bạn phải trả chi phí [i] xăng để đi từ trạm thứ i đến trạm thứ (i + 1) tiếp theo. Bạn bắt đầu cuộc hành trình với một chiếc bình rỗng tại một trong những trạm xăng.

Cho hai mảng số nguyên gas và chi phí, trả về chỉ số của trạm xăng ban đầu nếu bạn có thể đi vòng quanh mạch một lần theo chiều kim đồng hồ, nếu không thì trả về -1. Nếu tồn tại một giải pháp thì nó được đảm bảo là duy nhất.

class Solution {
    public int canCompleteCircuit(int[] gas, int[] cost) {
        int n = gas.length;
        int ans = 0;
        int s = 0;
        int start = 0;
        for(int i = 0; i < n; i++){
            ans += gas[i] - cost[i];
            s += gas[i] - cost[i];
            if(s < 0){
                s = 0;
                start = i + 1;
            }
        }
        return (ans < 0)?-1: start;
    }
}


321.Tạo số lượng tối đa

Bạn được cho hai mảng số nguyên nums1 và nums2 có độ dài lần lượt là m và n. nums1 và nums2 đại diện cho các chữ số của hai số. Bạn cũng được cho một số nguyên k.

Tạo số lượng độ dài tối đa k <= m + n từ các chữ số của hai số. Thứ tự tương đối của các chữ số trong cùng một mảng phải được giữ nguyên.

Trả về một mảng gồm k chữ số đại diện cho câu trả lời.


class Solution:
    def maxNumber(self, nums1: List[int], nums2: List[int], k: int) -> List[int]:        
        def merge(n1, n2):
            res = []
            while (n1 or n2) :
                if n1>n2:
                    res.append(n1[0])
                    n1 = n1[1:]
                else:
                    res.append(n2[0])
                    n2 = n2[1:]
            return res
        def findmax(nums, length):
            l = []
            maxpop = len(nums)-length
            for i in range(len(nums)):
                while maxpop>0 and len(l) and nums[i]>l[-1]:
                    l.pop()
                    maxpop -= 1
                l.append(nums[i])
            return l[:length]
        n1 = len(nums1)
        n2 = len(nums2)
        res = [0]*k
        for i in range(k+1):
            j = k-i
            if i>n1 or j>n2:    continue
            l1 = findmax(nums1, i)
            l2 = findmax(nums2, j)
            res = max(res, merge(l1,l2))
        return res


330. Patching Array

Given a sorted integer array nums and an integer n, add/patch elements to the array such that any number in the range [1, n] inclusive can be formed by the sum of some elements in the array.


class Solution {
public:
    int minPatches(vector<int>& nums, int n) {
        int patches = 0;
        int index = 0;
        long long nextSum = 1;
        while (nextSum <= n) {
            if (index < nums.size() && nums[index] <= nextSum) {
                nextSum += nums[index++];
            } else {
                nextSum += nextSum;
                patches++;
            }
        }
        return patches;
    }
};
