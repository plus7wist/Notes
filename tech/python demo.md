# python demo

最近 python 用的多一点，常查函数名，这里不妨记录一下。大多是从 https://docs.python.org 上抄的。我只抄了我觉得常用的。如果是非常常用的或者使用方式 doc 上说的不详的，我会翻译一下；）。

还有在下倾向于使用 python3，所以查的是 python3 的文档。

## os

- `os.name`
字符串指示正在使用的平台，unix/linux 会得到 `posix`，windows 会得到 `nt`。

### Process

- `os.ctermid()`
Return the filename corresponding to the controlling terminal of the process.

- `os.getpid()` `os.getppid()`
返回当前进程（父进程）的 ID，后一个在 3.2 中添加了对 windows 的支持。

- `os.getenv(key, default=None)`
Return the value of the environment variable key if it exists, or default if it doesn’t. key, default and the result are str.
On Unix, keys and values are decoded with sys.getfilesystemencoding() and 'surrogateescape' error handler. Use os.getenvb() if you would like to use a different encoding.

- `os.putenv(varname, value)`
Set the environment variable named varname to the string value. Such changes to the environment affect subprocesses started with `os.system()`, `popen()` or `fork()` and `execv()`.

- `os.unsetenv(key)`
Unset (delete) the environment variable named key. Such changes to the environment affect subprocesses started with os.system(), popen() or fork() and execv().
When unsetenv() is supported, deletion of items in os.environ is automatically translated into a corresponding call to unsetenv(); however, calls to unsetenv() don’t update os.environ, so it is actually preferable to delete items of os.environ.

- `os.system(str_cmd)`
执行 `str_cmd` 表示的 shell 命令，返回这个命令的执行状态（0 表示执行正确）。

- `os.popen(cmd, mode='r', buffering=-1)`
Open a pipe to or from command cmd. The return value is an open file object connected to the pipe, which can be read or written depending on whether mode is 'r' (default) or 'w'. The buffering argument has the same meaning as the corresponding argument to the built-in open() function. The returned file object reads or writes text strings rather than bytes.
The close method returns None if the subprocess exited successfully, or the subprocess’s return code if there was an error. On POSIX systems, if the return code is positive it represents the return value of the process left-shifted by one byte. If the return code is negative, the process was terminated by the signal given by the negated value of the return code. (For example, the return value might be - signal.SIGKILL if the subprocess was killed.) On Windows systems, the return value contains the signed integer return code from the child process.
This is implemented using subprocess.Popen; see that class’s documentation for more powerful ways to manage and communicate with subprocesses.

## File Object Creation

- `os.fdopen(fd, *args, **kwargs)`
Return an open file object connected to the file descriptor fd. This is an alias of the open() built-in function and accepts the same arguments. The only difference is that the first argument of fdopen() must always be an integer.

## File Descriptor Operations

## Files and Directories

- `os.chdir(path)`
Change the current working directory to path.
This function can support specifying a file descriptor. The descriptor must refer to an opened directory, not an open file.
New in version 3.3: Added support for specifying path as a file descriptor on some platforms.

- `os.chmod(path, mode, *, dir_fd=None, follow_symlinks=True)`
Change the mode of path to the numeric 'mode'. mode may take one of the following values (as defined in the stat module) or bitwise ORed combinations of them:

- `os.getcwd()`
得到当前工作目录的字符串，最后没有 `/`。

- `os.listdir(path='.')`
得到 `path` 指向的目录下的文件名字（不带路径）。每个名字用字符串表示，函数返回这些字符串的列表。

- `os.stat(path, *, dir_fd=None, follow_symlinks=True)`
得到文件的状态，举例：
```py
>>> import os
>>> statinfo = os.stat('somefile.txt')
>>> statinfo
os.stat_result(st_mode=33188, st_ino=7876932, st_dev=234881026,
st_nlink=1, st_uid=501, st_gid=501, st_size=264, st_atime=1297230295,
st_mtime=1297230027, st_ctime=1297230027)
>>> statinfo.st_size
264
```

- `os.chdir(path)`
Change the current working directory to path.
Availability: Unix, Windows.

## directory

- `d.items()` `d.keys()` `d.values()`
```python
d = {1: 'one', 2: 'two', 3:'three'};
print(d.items()); # dict_items([(1, 'one'), (2, 'two'), (3, 'three')])
print(d.keys()); # dict_keys([1, 2, 3])
print(d.values()); # dict_values(['one', 'two', 'three'])
```
