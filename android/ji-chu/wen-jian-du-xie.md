# 文件读写

## Asset

```java
context.getAssets().open(path);
context.getAssets().openFd(path);
```

## Resource

```java
context.getResources().openRawResource(id);
context.getResources().openRawResourceFd(id);
```

## File

```java
FileInputStream inputStream = new FileInputStream(path);
FileOutputStream outputStream = new FileOutputStream(path);
inputStream.getFD();
outputStream.getFD();
```

## JavaPackage

