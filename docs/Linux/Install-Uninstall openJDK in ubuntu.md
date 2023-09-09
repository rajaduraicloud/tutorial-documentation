### Install JDK

```
sudo apt install openjdk-8-jdk
```

### Find JDK path

```
update-alternatives --list java
```

### To uninstall OpenJDK
> (if installed). First, check which OpenJDK packages are installed

```
sudo dpkg --list | grep -i jdk
```

### To remove OpenJDK

```
sudo apt-get purge openjdk*
```

### Uninstall OpenJDK-related packages

```
sudo apt-get purge icedtea-* openjdk-*
```

### Check that all OpenJDK packages have been removed

```
sudo dpkg --list | grep -i jdk
```

### Switch between Java versions
> enter the number

```
sudo update-alternatives --config java
```
