    class CrashWumpaEnv:
        def __init__(self, grid_size=5, max_steps=50):
            self.grid_size = grid_size
            self.max_steps = max_steps
            self.action_space = [0, 1, 2, 3]  # 0: up, 1: right, 2: down, 3: left
            self.reset()
    
        def reset(self):
            # Crash starts at a random position
            self.crash_pos = [np.random.randint(self.grid_size), np.random.randint(self.grid_size)]
            # The Wumpa fruit is placed randomly (not on Crash)
            self.wumpa_pos = [np.random.randint(self.grid_size), np.random.randint(self.grid_size)]
            while self.wumpa_pos == self.crash_pos:
                self.wumpa_pos = [np.random.randint(self.grid_size), np.random.randint(self.grid_size)]
            self.steps = 0
            return self._get_state()
    
        def _get_state(self):
            # State is represented as (crash_x, crash_y, wumpa_x, wumpa_y)
            return tuple(self.crash_pos + self.wumpa_pos)

        def step(self, action):
            # Crash moves in the grid based on the action
            if action == 0:  # up
                self.crash_pos[0] = max(0, self.crash_pos[0] - 1)
            elif action == 1:  # right
                self.crash_pos[1] = min(self.grid_size - 1, self.crash_pos[1] + 1)
            elif action == 2:  # down
                self.crash_pos[0] = min(self.grid_size - 1, self.crash_pos[0] + 1)
            elif action == 3:  # left
                self.crash_pos[1] = max(0, self.crash_pos[1] - 1)
    
            self.steps += 1
            reward = -1  # Step penalty to encourage efficiency
            done = False
    
            # If Crash reaches the Wumpa fruit, reward him and respawn the fruit
            if self.crash_pos == self.wumpa_pos:
                reward = 10
                self.wumpa_pos = [np.random.randint(self.grid_size), np.random.randint(self.grid_size)]
                while self.wumpa_pos == self.crash_pos:
                    self.wumpa_pos = [np.random.randint(self.grid_size), np.random.randint(self.grid_size)]

            if self.steps >= self.max_steps:
                done = True
    
            return self._get_state(), reward, done
