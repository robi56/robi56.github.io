---
layout: post
comments: true
title:  "Lemma Based Word2Vec Model Generation"
excerpt: "Lemma Based Word2Vec Model Generation"
date:   2017-02-04 16:00:00
---

Lemma Based Word2Vec Model in Python 

Sometimes Lemma baded Word2Vec model could be considered for any specific application. like newspaper categorization  
Steps:
1. Read Files in a directory or Single File
2. Lemmitized File removing stopwords
3. Save Output as Files in output directory of Single File  
4. Build and word2vec model 
5. Load model 


Read Data:
Download Link: http://mattmahoney.net/dc/text8.zip

lines = []
with open('/home/rabindra/PycharmProjects/WordEmbedding/Examples/text8') as f:
    for line in f:
        lines.append(line)



#Lemmitize File removing stopwords:

lemmas =[]
for line in lines:
    tknzr = TweetTokenizer()
    tokens=tknzr.tokenize(line)
    filtered_words = [word for word in tokens if word not in stopwords.words('english')]
    for token in filtered_words:
        lemmas.append(lemmatizer.lemmatize(token))


Save Output as Files in output directory or Single File:

  file = open('result.txt', 'w')
  lemmatizedString = ' '.join(str(e) for e in lemmas)
  file.write(lemmatizedString)
  file.close()

 Build and word2vec model:
 word2vec.word2vec('result.txt', 'model.bin', size=100, verbose=True)

Load Model:

model = word2vec.load('/home/rabindra/PycharmProjects/WordEmbedding/Examples/data1.bin')
print model.vocab.size
print model.vectors.shape
print model.vectors
print model.vocab

vocabs = model.vocab
values = model.vectors

#The model information  can be saved in a form word<space>vector<newline>word<space><vector>...
file = open('words.txt','w')
for i in range(0, len(vocabs)):
    file.write(vocabs[i]+" "+' '.join(str(e) for e in values[i])
)
    file.write('\n')

file.close()







 





