```
/*
 * Below is the interface for Iterator, which is already defined for you.
 * **DO NOT** modify the interface for Iterator.
 *
 *  class Iterator {
 *		struct Data;
 * 		Data* data;
 *  public:
 *		Iterator(const vector<int>& nums);
 * 		Iterator(const Iterator& iter);
 *
 * 		// Returns the next element in the iteration.
 *		int next();
 *
 *		// Returns true if the iteration has more elements.
 *		bool hasNext() const;
 *	};
 */

class PeekingIterator : public Iterator {
private:
    int current_value;        // 当前元素的值
    bool has_next_element;   // 是否还有下一个元素

public:
    // 构造函数
    PeekingIterator(const vector<int>& nums) : Iterator(nums) {
        // 初始化 has_next_element 和 current_value
        has_next_element = Iterator::hasNext();
        if (has_next_element) {
            current_value = Iterator::next();
        }
    }

    // 返回当前元素的值，不移动迭代器
    int peek() {
        return current_value;
    }

    // 返回当前元素的值，并更新 has_next_element 和 current_value
    int next() {
        int value = current_value;  // 保存当前元素的值
        has_next_element = Iterator::hasNext();
        if (has_next_element) {
            current_value = Iterator::next();
        }
        return value;
    }

    // 返回是否还有下一个元素
    bool hasNext() const {
        return has_next_element;
    }
};
```

