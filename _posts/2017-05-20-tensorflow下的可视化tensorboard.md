1,    
放在各变量的上一行  
with tf.name_scope('name'):   
只要遵守Python格式就行   
    
2,   
增加
writer = tf.summary.FileWriter("logs/", sess.graph)

   
3,   
执行   
tensorboard --logdir=logs    
