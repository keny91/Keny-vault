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