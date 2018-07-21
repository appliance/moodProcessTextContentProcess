# -情感分析，单篇文本内容获取预处理
文件读取，jieba分词，去停用词，列表形式保存
'''
    要求： 
    
        利用txt地址读取内容保存到列表中
        
        jieba对文件内容进行分词，去停用词以列表形式返回
        
        将分词+标签 保存到测试列表中去 用作分类训练
        
    注：
    
        列表转化为字符串    ''.join(list)
        
        区分 什么时候返回的是列表 或者是 字符串，对于拼接处理需要进行列表转化
'''

import jieba

# 从test2.rlabelclass文件中读取第一行txt文件的名字，字符串拼接返回txt文件本地保存的地址
with open('C:/Users/Administrator/Desktop/NLP/review_sentiment.v1/test2.rlabelclass', 'r') as f:

    first_line = f.readlines()[0]
    
    first_txt_name = (first_line.strip()).split(' ')[0]          # first_txt_name 返回的是一个列表要转化为字符串才能够拼接
    
    first_txt_tag = (first_line.strip()).split(' ')[1]
    
first_txt_url = 'C:/Users/Administrator/Desktop/NLP/review_sentiment.v1/test2/' + ''.join(first_txt_name)

print('首个文本的地址为：', first_txt_url)

# 读取当前文件中的内容

first_txt_content = []

with open(first_txt_url, 'r') as f:

    for line in f.readlines():
    
        first_txt_content.append(line.strip())

# 利用jieba分词并返回去停用词，返回文件内容切分出来的词语集

first_txt_tokens = list(jieba.cut(''.join(first_txt_content)))

print(first_txt_tokens)

# 获取去停用词
stopwords = []

with open('C:/Users/Administrator/Desktop/NLP/stopwords.txt', 'r') as f:

    for stopword in f.readlines():
    
        stopwords.append(stopword.strip())          
        # 读取每行的去停用词的时候需要把后面的换行去除，否则下面循环匹配去停用词的时候，根本都匹配不上

final_txt_tokens = []

# 将文本中的停用词进行出去
for token in first_txt_tokens:

    if token not in stopwords:
    
        final_txt_tokens.append(token)
        
print(len(final_txt_tokens))


res = [(final_txt_tokens, first_txt_tag)]

print(res)



