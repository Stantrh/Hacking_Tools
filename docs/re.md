# 🧬 Reverse Engineering

> Tools, writeups and resources related to static and dynamic analysis of binaries or software behavior.

## 🛠️ Tools
- [WSL](https://learn.microsoft.com/fr-fr/windows/wsl/install) : Linux subsystem to use linux tools on windows while reversing.
- [Ghidra](https://github.com/NationalSecurityAgency/ghidra?tab=readme-ov-file) : Reverse software.
- [GDB](https://sourceware.org/gdb/) : Dynamic debugger.
- [WinDbg](https://learn.microsoft.com/windows-hardware/drivers/debugger/) : Microsoft debugger (symbols, NT APIs).
- [DnSpy](https://github.com/dnspyex/dnSpy) : .NET decompiler/debugger + IL editor.
- [JADX](https://github.com/skylot/jadx) : Dex/Apk/Jar → Java (CLI + GUI).
- [GDRETools](https://github.com/GDRETools/gdsdecomp) : Godot RE Tools.


## 📚 Articles / Writeups
- 

## 🧠 Notes
- 
## ⚙️ Installation

### Ghidra

#### Windows
```ps
choco install temurin --version=21.0.6.7 -y   # install JDK 21 (required)
choco install ghidra -y                       # install Ghidra 11.4.1
```

#### Kali
```bash
sudo apt update
sudo apt install -y ghidra
```

#### Ubuntu
```sh
# 1) OpenJDK 21 (also available through APT)
sudo apt update
sudo apt install -y openjdk-21-jdk unzip wget 
java -version

# 2) Downloading Ghidra
cd /tmp
wget https://github.com/NationalSecurityAgency/ghidra/releases/download/Ghidra_11.4.1_build/ghidra_11.4.1_PUBLIC_20250731.zip
sha256sum ghidra_11.4.1_PUBLIC_20250731.zip 

# 3) Clean install
sudo mkdir -p /opt/ghidra
sudo unzip -q ghidra_11.4.1_PUBLIC_20250731.zip -d /opt/ghidra
sudo ln -sf /opt/ghidra/ghidra_11.4.1_PUBLIC/ghidraRun /usr/local/bin/ghidra
```

### GDB + pwndbg
```sh
sudo apt update
sudo apt install -y gdb gdbserver gdb-multiarch build-essential file strace ltrace patchelf

# For better experience with gdb, pwndbg
git clone https://github.com/pwndbg/pwndbg ~/pwndbg
cd ~/pwndbg && ./setup.sh
```
- ``gdb`` : Debug.
- ``gdbserver`` : Remote debug.
- ``gdb-multiarch`` : Different architectures, ARM for example.
- ``file/strace/ltrace`` : Fast sorting.
- ``patchelf`` : Tink an ELF.

### WSL

#### Powershell install 
```ps
wsl --install -d Ubuntu
```

#### WSL RE setup 
```sh
sudo apt update
sudo apt install -y build-essential gdb gdb-multiarch gdbserver file strace ltrace patchelf python3 python3-pip

git clone https://github.com/pwndbg/pwndbg ~/pwndbg && cd ~/pwndbg && ./setup.sh

sudo apt install -y binutils # strings, objdump, readelf..
```

#### WSL file mounting
To work on the exact same file as on the Windows host (no copy), you have two options:

1. Work directly under `/mnt/c`
```sh
# Example
cd "/mnt/c/Users/<USERNAME>/Desktop/Reverse/crackmes/basic_crackme"
```

2. Create a shortcut with a symli
```sh
mkdir -p ~/re
ln -s "/mnt/c/Users/<USERNAME>/Desktop/Reverse/crackmes/basic_crackme" ~/re/basic_crackme-win
ls -l ~/re/basic_crackme-win      # → symlink to C:
file ~/re/basic_crackme-win/basic_crackme
```

### WinDbg
#### Powershell install
```ps
winget install -e --id Microsoft.WinDbg
setx _NT_SYMBOL_PATH "srv*C:\Symbols*https://msdl.microsoft.com/download/symbols" # config symbols path
```

### DnSpy
#### Powershell install
```ps
winget install -e --id dnSpyEx.dnSpy
```

### JADX
#### Powershell install
```
winget install -e --id Skylot.jadx
```

### GDRE Tools
#### Powershell install
```
winget install --id=GDRETools.gdsdecomp -e
```
