	# If Crash reaches the Wumpa fruit, reward him and respawn the fruit
	if self.crash_pos == self.wumpa_pos:
		reward = 10
		self.wumpa_pos = [np.random.randint(self.grid_size), np.random.randint(self.grid_size)]
		while self.wumpa_pos == self.crash_pos or self.wumpa_pos in self.nitro_crates:
			self.wumpa_pos = [np.random.randint(self.grid_size), np.random.randint(self.grid_size)]
		return self._get_observation(), reward, False, False, {"outcome": "collected"}

## 💻 Top Languages
</div>

![Top Languages](https://github-readme-stats.vercel.app/api/top-langs/?username=nglguarino&layout=compact&theme=radical)
