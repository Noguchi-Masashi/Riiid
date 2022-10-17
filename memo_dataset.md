## train.csv
- ユーザの強さ，問題の難しさを表すレーティング特徴量
- ユーザの属性

## questions.csv
- correct_answerのlag特徴量は重要そう（2回以上連続して同じ番号が正解だったとき，次の回答は別の番号になりそうだから）
どうやって求める？
- type_of(string):講義の目的．value_counts()で調べよう
- tagの個数が少ないと正解しやすい？
    - どうやってtagの個数をカウントする？
``` bash
questions_df.tags.value_counts()
8                 738
73                617
53                523
1                 413
96                373
                 ... 
157 144 81          1
157 144 38          1
106 169 162 81      1
157 169 162 81      1
157 169 92          1
Name: tags, Length: 1519, dtype: int64
```

# lectures.csv
- lecturesの`tag`は1つだけっぽい
- `type_of`は講義の目的．intentionは何だろう？

``` bash
lectures_df['type_of'].value_counts()

concept             222
solving question    186
intention             7
starter               3
Name: type_of, dtype: int64
```

## 作りたい特徴量
1. Target Encoding の特徴量
    Kaggle本では，CVを組んだ Target Encoding
    もし，


2. lag特徴量
    同じ問題を解いていた場合，現時点までの timestap の差分
3. レーティング特徴量
4. ユーザ同士の類似度を表す特徴量
5. 問題同士の類似度を表す特徴量


## 質問
1. content_df['answered_correctly_avg_c']は問題の難易度だと思っていい？
2. add_user_feats()のfor の中身の順番について．上2行と下2行は逆な気がする．
    - Comment で同じことを聞いている人がいた．読んだが理解できていない．

3.  `answered_correctly_avg_c` は train_df から算出されて content_df に格納されており，test_dfに join している
    - `answered_correctly_avg_u` は テストバッチが来るたび更新しているのに，`answered_correctly_avg_c`は更新していないのは変な気がする
4. ファイルの利用方法について．「Add data」が反応しない？

## 特徴量とAUCの記録
FEATS = ['answered_correctly_avg_u', 'answered_correctly_sum_u', 'count_u', 'answered_correctly_avg_c', 'part', 'prior_question_had_explanation', 'prior_question_elapsed_time']
AUC = 0.7213


