
# nb_steps_warmup
Often times in reinforcement learning the error rate of the first few steps will be very large and may cause your parameters to oscillate. This is usually attributed to the lack of specificity of the deeper layers in your network. Thus we can come up with some schemes where the learning rate changes in a pre-determined way. For example we can use constant warm-up or gradual warm-up.

The convergence of stochastic gradient descent is a function of the learning rate and the batch size. When the batch size is increased too much then the needed increase in the learning rate can be such that it is beyond the possible curvature of the loss function. We thus introduce warm up as a means by which we can introduce large learning rates without the instability.


# forward 
method predicts the action to be taken for any given observation from the given algorithm's policy.

# backward 
method trains the function approximator (neural network) for a given sample. It also stores the experience replay memory (DQN) for generating samples at the time of learning.
