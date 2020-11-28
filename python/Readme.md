# Python tips

## Working with Anaconda

### anaconda environments

List all local environments

    conda env list

Activate environment

    source activate {envname}

### anaconda maintaining

Update all packages in the current active environment

    conda update --all

## Working with virtual environment

    python3 -m venv ~/tools/scikit
    source ~/tools/scikit/bin/activate


## Installing older python3 versions via homebrew

In case homebrew delivers to new version instal older version and switch to this. E.g. if tensorflow is not yet compatible with python 3.7 (as in end 2018)

Example to install python 3.6 beside python 3.7

* finding version of brew formular on [github in history](https://github.com/Homebrew/homebrew-core/commits/master/Formula/python.rb)
* for version 3.6.5_1 take the [raw link](https://raw.githubusercontent.com/Homebrew/homebrew-core/f2a764ef944b1080be64bd88dca9a1d80130c558/Formula/python.rb)
* infos where found on [stackoverflow](https://stackoverflow.com/questions/51125013/how-can-i-install-a-previous-version-of-python-3-in-macos-using-homebrew/51125014#51125014)

    [0] % brew unlink python 
    [0] % brew install https://raw.githubusercontent.com/Homebrew/homebrew-core/f2a764ef944b1080be64bd88dca9a1d80130c558/Formula/python.rb # 
    [0] % python3 --version
    Python 3.6.5
    [0] % brew list --versions python 
    python 3.7.1 3.6.5_1
    [0] % brew switch python 3.7.1  
    Cleaning /usr/local/Cellar/python/3.7.1
    Cleaning /usr/local/Cellar/python/3.6.5_1
    24 links created for /usr/local/Cellar/python/3.7.1
    [0] % python3 --version
    Python 3.7.1

