## [답안 에시] 파일 압축

1. 

```
cd ~/zip
tar -cvf ~/zip2/tar/archive.tar ./*
```

or 

```
cd ~/zip
tar -cvf archive.tar ./*
```

2. 

```
cd ~/zip
tar -xvf archive.tar -C ~/zip2/tar
```

3. 

```
cd ~/zip
tar -czvf archive.tar.gz file1 file2 file3 inner/
```

4. 

```
cd ~/zip
tar -xzvf archive.tar.gz -C ~/zip2/gzip
```

5. 

```
cd ~/zip
tar -cjvf archive.tar.bz2 file1 file2 file3 inner/
```

6. 

```
cd ~/zip
tar -xjvf archive.tar.bz2 ./bzip2
```

7. 

```
cd ~/zip
zip -r archive.zip file1 file2 file3 inner/
```

8.
```
cd ~/zip
unzip ~/archive.zip -d ~/zip2/zip
```

