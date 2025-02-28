### 1、哈希表

```cpp
class FoodRatings {
private:
    // 存储食物名称到其评分和菜系的映射
    unordered_map<string, pair<int, string>> food_map;

    // 存储每个菜系对应的食物及其评分，使用 set 维护排序
    unordered_map<string, set<pair<int, string>>> cuisine_map;

public:
    FoodRatings(vector<string>& foods, vector<string>& cuisines, vector<int>& ratings) {
        for (int i = 0; i < foods.size(); i++) {
            auto& food = foods[i];
            auto& cuisine = cuisines[i];
            int rating = ratings[i];
            food_map[food] = {rating, cuisine};
            // 使用 -rating 实现从高到低排序，评分相同时按字典序排序
            cuisine_map[cuisine].emplace(-rating, food);
        }
    }

    void changeRating(string food, int newRating) {
        auto& [rating, cuisine] = food_map[food];
        auto& st = cuisine_map[cuisine];
        // 移除旧数据
        st.erase({-rating, food});
        // 插入新数据
        st.emplace(-newRating, food);
        // 更新 food_map 中的评分
        rating = newRating;
    }

    string highestRated(string cuisine) {
        // 返回评分最高且字典序最小的食物
        return cuisine_map[cuisine].begin()->second;
    }
};

```

