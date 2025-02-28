
    class CrashBandicootMLP(nn.Module):
    
      def __init__(self, wumpa, crates, cortex):
        super(CrashBandicootMLP, self).__init__()
        self.spin = nn.Linear(wumpa, crates)
        self.boost = nn.ReLU()
        self.smash = nn.Linear(crates, cortex)
        
      def forward(self, x):
        x = self.spin(x)
        x = self.boost(x)
        x = self.smash(x)
        return x
