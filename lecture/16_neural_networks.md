# Neural Networks
---
# What is an Artificial Neural Network?
Model inspired in brain biology.
Stacked layers.

---
# Multilayer perceptron
* The model of each neuron in the network includes a nonlinear activation function that is differentiable
* The network contains one or more layers that are hidden from both input and output nodes
* The network exhibits a high degree of connectivity, the extent of which is determined by synaptic weights.

---
# Tensorflow
* Graph based 

---
# Single layer model

```
x = tf.placeholder(tf.float32, [None, 784])
y_ = tf.placeholder(tf.float32, [None, 10])
W = tf.Variable(tf.zeros([784, 10]))
b = tf.Variable(tf.zeros([10]))
y = tf.matmul(x, W) + b
```
---

# Softmax activation function
* The idea of softmax is to define a new type of output layer for our neural network. 
* In the output layer we apply the softmax activation function to the activation potential.
* Output activations are guaranteed to sum up to 1.
* Output activations are always positive.
* Softmax layer can be thought of as a probability distribution.
* Output layer has a simple interpretation.

$$ \phi_j(v_j) = \frac{e^{v_j}}{\sum_k e^{v_k}}$$


---
# Playground
http://playground.tensorflow.org/

---
# Cost function and optimizer
```python
cross_entropy = tf.reduce_mean(
  tf.nn.softmax_cross_entropy_with_logits(labels=y_,
                                          logits=y))
train_step = tf.train.GradientDescentOptimizer(0.5)\
            .minimize(cross_entropy)
```

---
# Train
```
sess = tf.InteractiveSession()
tf.global_variables_initializer().run()
# Train
for _ in range(1000):
    batch_xs, batch_ys = mnist.train.next_batch(100)
    sess.run(train_step, feed_dict={x: batch_xs,
                                    y_: batch_ys})
```

---
# Test model
```
correct_prediction = \
    tf.equal(tf.argmax(y, 1), tf.argmax(y_, 1))
accuracy = tf.reduce_mean(
               tf.cast(correct_prediction, tf.float32))
print(sess.run(
    accuracy, feed_dict={x: mnist.test.images, 
                         y_: mnist.test.labels}))
```

---
# Notebook
* **Goal**: Create and train a neural network with accuracy of ~95% on the testing set.
* **Steps**:
    - Create a neural network with two hidden layers and 300 hidden nodes per layer.
    - Train your model with 10 epochs.
    - For each epoch, print the accuracy.
    - Print the final accuracy on the training set.
    - Print the final accuracy on the testing set