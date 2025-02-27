### 1、对顶栈

```
class TextEditor {
    string leftText, rightText; // 光标左侧和右侧的字符

    // 返回光标左侧最多 10 个字符
    string getCursorLeftText() {
        int length = min((int)leftText.size(), 10); // 取左侧字符数和 10 的较小值
        return leftText.substr(leftText.size() - length); // 返回左侧最后 length 个字符
    }

public:
    // 在光标左侧添加文本,O(m)
    void addText(string text) {
        leftText += text; // 将文本追加到左侧字符的末尾
        //因为需要将 text 追加到 leftText 的末尾，字符串追加操作的时间复杂度为 O(m)。
    }

    // 删除光标左侧的 k 个字符，返回实际删除的字符数，O(1)
    int deleteText(int k) {
        k = min(k, (int)leftText.size()); // 取 k 和左侧字符数的较小值，避免越界
        leftText.resize(leftText.size() - k); // 调整左侧字符的长度，删除最后 k 个字符
        //resize 操作的时间复杂度是 O(1)，因为它只是调整字符串的长度，而不涉及额外的复制或移动。
        return k; // 返回实际删除的字符数
    }

     string cursorLeft(int k) {
            while (k && !leftText.empty()) {
                rightText += leftText.back(); // 左手倒右手
                leftText.pop_back();
                k--;
            }
            return getCursorLeftText();
        }

	//O(k)
    string cursorRight(int k) {
        while (k && !rightText.empty()) {
            leftText += rightText.back(); // 右手倒左手
            rightText.pop_back();
            k--;
        }
        return getCursorLeftText();
    }

};
```

- 时间：addText 为 O(∣*text*∣)，其他O(k)
- 空间：n，所有text字符串长度之和
