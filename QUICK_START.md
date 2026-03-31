# ⚡ Quick Start Guide - NNTrainer Visualizer Extension

## 🎯 5 Minute Setup

### Step 1: Install Extension (1 min)

**Copy the file path of:** `nntrainer-visualizer-1.0.0.vsix`

Then run:
```bash
code --install-extension /path/to/nntrainer-visualizer-1.0.0.vsix
```

Or in VS Code:
- Extensions (Ctrl+Shift+X)
- Click "..." menu
- "Install from VSIX..."
- Select the file

### Step 2: Verify Installation (1 min)

1. Reload VS Code: Ctrl+Shift+P → "Reload Window"
2. Extensions → Search "NNTrainer"
3. Should show as installed ✓

### Step 3: Prepare Your Model (1 min)

Make sure you have:
```
my_model/
├── model.ini
├── model.bin (optional)
└── layer_timing_profile.txt  ← C++ generates this
```

**Important:** Your C++ code must generate the timing file:
```cpp
network_graph->saveTimingData("layer_timing_profile.txt");
```

### Step 4: Visualize (1 min)

1. Open project folder: `code my_model/`
2. Right-click `model.ini`
3. Select "Visualize NNTrainer Model"
4. Visualizer window opens

### Step 5: Load Timing (1 min)

1. Click "Load Timing Data" button
2. See color-coded layer timing
3. Click any layer for details

---

## 🎨 What You'll See

### Left Panel: Model Graph
```
        [Input]
           ↓
      [Conv2D_1]
           ↓
      [Conv2D_2]
           ↓
       [Flatten]
           ↓
       [Dense]
           ↓
       [Output]
```

### Right Panel: Timing Data
```
⏱ Layer Timing
──────────────────────────
input        0.002 ms  🟢
conv2d_1     5.430 ms  🔴  ← Bottleneck!
conv2d_2     4.820 ms  🔴
flatten      0.150 ms  🟢
dense        2.100 ms  🟡

Summary:
├─ Total: 12.502 ms
├─ Layers: 5
└─ Bottleneck: conv2d_1 (5.430 ms)
```

Click a layer → See function breakdown:
```
Function Breakdown
├─ Forward    2.100 ms
├─ Backward   3.330 ms
└─ Weight Update 0.000 ms
```

---

## ✅ Quick Checklist

- [ ] VSIX file installed
- [ ] VS Code reloaded
- [ ] C++ code writes timing data
- [ ] Timing file is `layer_timing_profile.txt`
- [ ] Timing file in same folder as `.ini`
- [ ] Can right-click `.ini` file
- [ ] Extension command appears in menu
- [ ] Visualizer window opens
- [ ] "Load Timing Data" button works
- [ ] Timing data displays ✓

---

## 🚨 Common Issues (Quick Fixes)

### ❌ "Command not found"
→ Reload VS Code (Ctrl+Shift+P → "Reload Window")

### ❌ "Right-click menu missing"
→ File must be `.ini` extension and in workspace

### ❌ "Timing data not loading"
→ Check file exists: `ls layer_timing_profile.txt`
→ File must be same folder as `.ini`

### ❌ "Wrong timing file location"
→ Edit `extension.js` line ~55:
```javascript
const timingPath = path.join(folder, 'layer_timing_profile.txt');
```

---

## 💡 Tips

1. **Fast layers** are 🟢 green (< 0.5ms)
2. **Slow layers** are 🔴 red (> 75% of slowest)
3. **Bottleneck layer** is highlighted in summary
4. Click any layer to see detailed breakdown
5. Colors are VS Code theme-aware

---

## 🎓 Next: Load Your Model

```bash
# 1. Open your NNTrainer project
code /path/to/my_model

# 2. Run training (generates timing data)
$NNTRAINER_ROOT/bin/nntrainer model.ini

# 3. Right-click model.ini in VS Code
# 4. Select "Visualize NNTrainer Model"
# 5. Click "Load Timing Data"
# 6. See color-coded timing! 🎉
```

---

## 📖 Need More Help?

- Full guide: `INSTALLATION_GUIDE.md`
- Troubleshooting: `INSTALLATION_GUIDE.md` → Troubleshooting section
- File format: Check `layer_timing_profile.txt` format section
- Configuration: Edit colors and thresholds in `extension.js`

---

**That's it! You're ready to profile your NNTrainer models. 🚀**

Start by visualizing your model and checking which layers are the bottlenecks!
