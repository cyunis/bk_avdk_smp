Armino AI Setup Guide (Simple Version for Students, macOS)
Use this guide to build beken_genie by yourself.
1. Open Terminal and create workspace
mkdir -p ~/armino
cd ~/armino

2. Install Apple Command Line Tools (if not installed)
xcode-select --install

If it says already installed, continue.
3. Clone both repos (same version branch)
cd ~/armino
git clone https://github.com/bekencorp/bk_avdk_smp.git -b release/v3.1.1
git clone https://github.com/bekencorp/bk_solution_ai.git -b release/v3.1.1

4. Install Python/build dependencies
python3 -m pip install --user --upgrade pip
python3 -m pip install --user click cmake ninja pycryptodome future click_option_group cryptography jinja2 PyYAML cbor2 intelhex

5. Add user tools to PATH
export PATH="$HOME/Library/Python/3.9/bin:$PATH"

Optional (make it permanent):
echo 'export PATH="$HOME/Library/Python/3.9/bin:$PATH"' >> ~/.zshrc
source ~/.zshrc

6. Download ARM toolchain
mkdir -p ~/armino/toolchains
cd ~/armino/toolchains
curl -L -o gcc-arm-none-eabi-10.3-2021.10-mac.tar.bz2 https://developer.arm.com/-/media/Files/downloads/gnu-rm/10.3-2021.10/gcc-arm-none-eabi-10.3-2021.10-mac.tar.bz2
tar -xjf gcc-arm-none-eabi-10.3-2021.10-mac.tar.bz2

7. Build project
cd ~/armino/bk_solution_ai/projects/beken_genie
export SDK_DIR=~/armino/bk_avdk_smp
export PATH="$HOME/Library/Python/3.9/bin:$PATH"
make clean
make bk7258 COMPILER_TOOLCHAIN_PATH=~/armino/toolchains/gcc-arm-none-eabi-10.3-2021.10/bin

8. Check output files
ls -lh ~/armino/bk_solution_ai/projects/beken_genie/build/bk7258/beken_genie/package/

You should see:
all-app.bin
app_pack.rbl
build_summary.txt

How to know what environment/tool is missing
Run these checks:
which git
which python3
which cmake
which ninja
python3 -m pip show click
ls ~/armino/toolchains/gcc-arm-none-eabi-10.3-2021.10/bin/arm-none-eabi-gcc
echo $SDK_DIR

Read the error message and map quickly
git: command not found -> install Command Line Tools (xcode-select --install)
No module named click -> python3 -m pip install --user click
cmake must be available on the PATH -> install cmake + add PATH
arm-none-eabi-gcc not found -> toolchain not installed / wrong path
SDK_DIR empty or wrong -> export correct SDK path

Check if required files/folders are missing
ls ~/armino/bk_avdk_smp
ls ~/armino/bk_solution_ai/projects/beken_genie

If missing, clone failed or wrong directory.
For this project, key paths must exist:
~/armino/bk_avdk_smp
~/armino/bk_solution_ai
~/armino/bk_solution_ai/projects/beken_genie
~/armino/toolchains/gcc-arm-none-eabi-10.3-2021.10/bin/arm-none-eabi-gcc

<img width="1200" height="628" alt="litheli_logo_1200X628__1" src="https://github.com/user-attachments/assets/6044651e-5a9d-4c66-bd2a-f1c163f31a59" />


If your laptop environment is complete.
You can follow this instruction: 
Step 1: Create workspace
mkdir -p ~/armino
cd ~/armino

Step 2: Clone SDK
git clone https://github.com/bekencorp/bk_avdk_smp.git

Step 3: Clone AI solutiongit clone 
https://github.com/bekencorp/bk_solution_ai.git -b 
release/v3.1.1

Step 4: Enter project
cd ~/armino/bk_solution_ai/projects/beken_genie

Step 5: Set SDK path
export SDK_DIR=~/armino/bk_avdk_smp

Step 6: Build
make clean
make bk7258

