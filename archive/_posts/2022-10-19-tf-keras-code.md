---
layout: post
title: <텐서플로> 딥러닝 코드 샘플
description: >
  코드 샘플
# sitemap: false
hide_last_modified: false
comments: true

---


~~~python
import numpy as np
import tensorflow as tf
from visual import *

import logging, os
logging.disable(logging.WARNING)
os.environ['TF_CPP_MIN_LOG_LEVEL'] = '3' 

# 데이터를 전처리하는 함수

def sequences_shaping(sequences, dimension):
    
    results = np.zeros((len(sequences), dimension))
    for i, word_indices in enumerate(sequences):
        results[i, word_indices] = 1.0 
    
    return results


def OPT_model(word_num):
    
    model = tf.keras.Sequential([
        tf.keras.layers.Dense(100, input_dim=word_num, activation='relu'),
        tf.keras.layers.Dense(100, activation='relu'),
        tf.keras.layers.Dense(1, activation='sigmoid')
    ])
    
    return model

def main():
    
    word_num = 100
    data_num = 25000
    
    # Keras에 내장되어 있는 imdb 데이터 세트를 불러오고 전처리합니다.
    
    (train_data, train_labels), (test_data, test_labels) = tf.keras.datasets.imdb.load_data(num_words = word_num)
    
    train_data = sequences_shaping(train_data, dimension = word_num)
    test_data = sequences_shaping(test_data, dimension = word_num)
    
    adagrad_model = OPT_model(word_num)  # Adagrad를 사용할 모델입니다.
    rmsprop_model = OPT_model(word_num)  # RMSProp을 사용할 모델입니다.
    adam_model = OPT_model(word_num)     # Adam을 사용할 모델입니다.
    
    adagrad_opt = tf.keras.optimizers.Adagrad(lr=0.01, epsilon=0.00001, decay=0.4)
    adagrad_model.compile(optimizer=adagrad_opt, loss='binary_crossentropy', metrics=['accuracy', 'binary_crossentropy'])
    
    rmsprop_opt = tf.keras.optimizers.RMSprop(lr=0.001) 
    rmsprop_model.compile(optimizer=rmsprop_opt, loss='binary_crossentropy', metrics=['accuracy', 'binary_crossentropy'])
    
    adam_opt = tf.keras.optimizers.Adam(lr=0.01, beta_1=0.9, beta_2=0.999)
    adam_model.compile(optimizer=adam_opt, loss='binary_crossentropy', metrics=['accuracy', 'binary_crossentropy'])
    
    adagrad_model.summary()
    rmsprop_model.summary()
    adam_model.summary()


    adagrad_history = adagrad_model.fit(train_data, train_labels, epochs=20, batch_size=500, validation_data=(test_data, test_labels), verbose=0)
    print('\n')
    rmsprop_history = rmsprop_model.fit(train_data, train_labels, epochs=20, batch_size=500, validation_data=(test_data, test_labels), verbose=0)
    print('\n')
    adam_history = adam_model.fit(train_data, train_labels, epochs=20, batch_size=500, validation_data=(test_data, test_labels), verbose=0)
    
    scores_adagrad = adagrad_model.evaluate(test_data, test_labels)
    scores_rmsprop = rmsprop_model.evaluate(test_data, test_labels)
    scores_adam = adam_model.evaluate(test_data, test_labels)
    
    print(adagrad_history.history)

    print('\nscores_adagrad: ', scores_adagrad[-1])
    print('scores_rmsprop: ', scores_rmsprop[-1])
    print('scores_adam: ', scores_adam[-1])
    
    Visulaize([('Adagrad', adagrad_history),('RMSprop', rmsprop_history),('Adam', adam_history)])
    
    return adagrad_history, rmsprop_history, adam_history
    
if __name__ == "__main__":
    main()

~~~

## L1, L2 정규화

ratio : 가중치에 L1 정규화를 적용하는 비율 (0.001 ~0.005)

~~~python
tf.keras.layers.Dense(kernel_regularizer = tf.keras.regularizers.l2(ratio))

~~~

## drop out

prob: 드롭 아웃 적용 확률 0.1~0.5

~~~python
tf.keras.layers.Dropout(prob)

~~~

## Batch Normalization

~~~python
tf.keras.layers.BatchNormalization()

tf.keras.layers.Activation()
~~~


<!-- 
{% if page.comments %}

<div id="disqus_thread"></div>
<script>
    /**
    *  RECOMMENDED CONFIGURATION VARIABLES: EDIT AND UNCOMMENT THE SECTION BELOW TO INSERT DYNAMIC VALUES FROM YOUR PLATFORM OR CMS.
    *  LEARN WHY DEFINING THESE VARIABLES IS IMPORTANT: https://disqus.com/admin/universalcode/#configuration-variables    */
    
    <!-- var disqus_config = function () {
    this.page.url = https://sanhaa-github-io;  // Replace PAGE_URL with your page's canonical URL variable
    this.page.identifier = PAGE_IDENTIFIER; // Replace PAGE_IDENTIFIER with your page's unique identifier variable
    }; -->
    
    (function() { // DON'T EDIT BELOW THIS LINE
    var d = document, s = d.createElement('script');
    s.src = 'https://sanhaa-github-io.disqus.com/embed.js';
    s.setAttribute('data-timestamp', +new Date());
    (d.head || d.body).appendChild(s);
    })();
</script>
<noscript>Please enable JavaScript to view the <a href="https://disqus.com/?ref_noscript">comments powered by Disqus.</a></noscript>

{% endif %} -->