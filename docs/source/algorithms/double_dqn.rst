.. _dqn:


Double DQN
==========

`Double Deep Q-Network (Double DQN) <https://arxiv.org/abs/1509.06461>`_ is one of the most important extensions of vanilla DQN. It resolves the issue of overestimation in vanilla DQN by a simple trick: decoupling the max operation in the target into action selection and action evaluation. 

Without having to introduce additional networks, we use the Q-network to select the best next action among all the available next actions and use the target network to evaluate its Q-value. Similar to DQN implementation, this implementation supports the following extensions:

-  Experience replay: ✔️
-  Target network: ✔️
-  Gradient clipping: ✔️
-  Reward clipping: ❌
-  Prioritized Experience Replay (PER): ✔️
-  Dueling network architecture: ✔️


Example
------------

.. code-block:: python

    import torch
    from elegantrl.run import Arguments, train_and_evaluate
    from elegantrl.env import build_env
    from elegantrl.agent import AgentDoubleDQN
    
    # train and save
    args = Arguments(env=build_env('CartPole-v0'), agent=AgentDoubleDQN())
    args.cwd = 'demo_CartPole_DoubleDQN'
    args.target_return = 195
    train_and_evaluate(args) 
    
    # test
    agent = AgentDoubleDQN()
    agent.init(args.net_dim, args.state_dim, args.action_dim)
    agent.save_or_load_agent(cwd=agrs.cwd, if_save=False)
    
    env = build_env('CartPole-v0')
    state = env.reset()
    episode_reward = 0
    for i in range(2 ** 10):
        action = agent.select_action(state)
        next_state, reward, done, _ = env.step(action)
        
        episode_reward += reward
        if done:
            print(f'Step {i:>6}, Episode return {episode_return:8.3f}')
            break
        else:
            state = next_state
        env.render()
              
              
              
Parameters
---------------------

.. autoclass:: elegantrl.agent.AgentDoubleDQN
   :members:
   
.. _dqn_networks:
   
Networks
-------------

.. autoclass:: elegantrl.net.QNet
   :members:
   
.. autoclass:: elegantrl.net.QNetDuel
   :members:
