
# Open Repository

dependencies
    pip install gitpython

imports
    import os
    from git import Repo

current folder
    import os
    os.getcwd()

folder exists
    os.path.isdir(path)

clone repo
    url = 'https://github.com/fcatae/study-python.git'
    path = './t1'
    repo = Repo.clone_from(url, path)

open existing repo
    repo = Repo(path)


