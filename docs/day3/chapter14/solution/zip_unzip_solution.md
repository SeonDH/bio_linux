## [답지] 파일 압축

1. `tar` 명령어를 이용하여 `~/zip` 하위 파일과 디렉터리를 압축한다.

    ```
    cd ~/zip
    tar -cvf ~/zip2/tar/archive.tar file1 file2 file3 inner/
    ```

2. `tar`와 `gzip`을 함께 사용하여 `~/zip` 하위 파일들을 압축한다.

    ```
    cd ~/zip
    tar -xvf archive.tar -C ~/zip2/tar
    ```

3. `tar`와 `gzip`을 함께 사용하여 `~/zip` 하위 파일들을 압축한다.

    ```
    cd ~/zip
    tar -czvf archive.tar.gz file1 file2 file3 inner/
    ```

4. 압축 파일을 `~/zip2/gzip` 디렉터리에 해제한다.

    ```
    cd ~/zip
    tar -xzvf archive.tar.gz -C ~/zip2/gzip
    ```

5. `tar`와 `bzip2`를 함께 사용하여 `~/zip` 하위 파일들을 압축한다.

    ```
    cd ~/zip
    tar -cjvf archive.tar.bz2 file1 file2 file3 inner/
    ```

6. 압축 파일을 `~/zip2/bzip2` 디렉터리에 해제한다.

    ```
    cd ~/zip
    tar -xjvf archive.tar.bz2 ./bzip2
    ```

7. `zip` 명령어를 사용하여 `~/zip` 하위 파일들을 압축한다.

    ```
    cd ~/zip
    zip -r archive.zip file1 file2 file3 inner/
    ```

8. 압축 파일을 `~/zip2/zip` 디렉터리에 해제한다.
    ```
    cd ~/zip
    unzip ~/archive.zip -d ~/zip2/zip
    ```