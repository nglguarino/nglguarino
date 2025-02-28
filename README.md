    # If Crash reaches the Wumpa fruit, reward him and respawn the fruit
    if self.crash_pos == self.wumpa_pos:
        reward = 10
        self.wumpa_pos = [np.random.randint(self.grid_size), np.random.randint(self.grid_size)]
        while self.wumpa_pos == self.crash_pos:
            self.wumpa_pos = [np.random.randint(self.grid_size), np.random.randint(self.grid_size)]
