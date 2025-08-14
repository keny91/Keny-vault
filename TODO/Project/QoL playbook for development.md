#todo

- Symlink to mounted data
- ll = ls -la command
- Make a file and path macro:

```
makepathfile() {
  local fullpath="$1"

  # Extract directory and filename
  local dirpath
  dirpath=$(dirname "$fullpath")
  local filename
  filename=$(basename "$fullpath")

  # Create the directory and the file
  mkdir -p "$dirpath" && touch "$dirpath/$filename"
}
```

For all users put it **sudo nano /usr/local/bin/makepathfile**

Paste this in it:
```
sudo nano /usr/local/bin/makepathfile

```


### Macros:

```
echo "alias ll='ls -la'" >> ~/.bashrc
source ~/.bashrc
```


### Dowload package and all its dependencies 

1. Using `apt-get download` + `apt-rdepends` (manual but flexible)

```
# Install apt-rdepends (on a system with internet)
sudo apt-get install apt-rdepends

# Create a folder for your offline packages
mkdir jenkins_offline && cd jenkins_offline

# Download all dependencies (without installing)
apt-rdepends jenkins | grep -v "^ " | xargs apt-get download
```

- This gets **.deb** files for `jenkins` and all required dependencies.
    
- You can later copy this folder to your offline machine and install:

```
sudo dpkg -i *.deb
sudo apt-get -f install   # to fix missing deps from your local folder
```

	