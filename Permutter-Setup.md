# Qiskit + Jupyter Environment Setup on NERSC

This guide provides a one-and-done shell script for setting up a Python 3.12 virtual environment with Qiskit on NERSC (e.g., Perlmutter), registering it as a Jupyter kernel, and ensuring it works correctly inside JupyterHub.

---

## 🔧 Setup Script: `setup_qiskit_jupyter_env.sh`

```bash
#!/bin/bash

# Customize these
VENV_DIR=$HOME/.venvs/qiskit_env
KERNEL_NAME="qiskit312"
DISPLAY_NAME="Qiskit 3.12 (NERSC)"

echo "🔁 Loading Python 3.12 module..."
module load python/3.12

echo "📦 Creating virtual environment at $VENV_DIR ..."
python -m venv $VENV_DIR
source $VENV_DIR/bin/activate

echo "⬆ Upgrading pip..."
pip install --upgrade pip

echo "🔧 Installing Qiskit and Jupyter kernel support..."
pip install qiskit ipykernel

echo "📚 Registering Jupyter kernel as '$DISPLAY_NAME'..."
python -m ipykernel install --user --name $KERNEL_NAME --display-name "$DISPLAY_NAME"

echo "✅ Done. Kernel should now appear in JupyterHub under '$DISPLAY_NAME'."

# Optional: Append to .bashrc if not already there
MARKER="# >>> Qiskit env activation for Slurm <<<"
if ! grep -q "$MARKER" ~/.bashrc; then
  echo "📝 Adding environment activation to your .bashrc for Slurm jobs..."

  cat <<EOF >> ~/.bashrc

$MARKER
if [[ \$SLURM_JOB_ID ]]; then
    module load python/3.12
    source $VENV_DIR/bin/activate
fi
# <<< Qiskit env activation for Slurm <<<
EOF

  echo "✅ Added to ~/.bashrc"
else
  echo "ℹ️  Activation logic already present in ~/.bashrc"
fi
```

---

## ✅ How to Use It

1. SSH into your NERSC system:
```bash
ssh your-username@perlmutter.nersc.gov
```

2. Allocate an interactive compute node:
```bash
salloc -C cpu -q interactive -t 00:30:00 -A your-project
```

3. Run the script:
```bash
bash setup_qiskit_jupyter_env.sh
```

---

## 🚀 After Setup
- Go to [https://jupyter.nersc.gov](https://jupyter.nersc.gov)
- Launch a notebook
- Select the kernel: **"Qiskit 3.12 (NERSC)"**
- You're now running with Qiskit and Python 3.12 inside JupyterHub 🎉

---

## 🧠 Notes
- The virtual environment and kernel persist across logins
- The `.bashrc` logic ensures activation in Slurm jobs (like Jupyter)
- You can modify this to include other packages like `cudaq`


