
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


# List commits

how many branches
    branch_list = repo.branches

inspect commits
    repo.head          # ref
    repo.head.commit   # commit


def print_commit(commit):
    message = commit.message.split('\n')[0]
    author = commit.author.name
    committer = commit.committer.name
    time = commit.authored_datetime.strftime('%Y-%m-%d %H:%M')
    print "{0} {1}: {2}".format(time, author, message)

def enum_next_commit(commit):
    more_parents = len(commit.parents)
    if(more_parents == 0):
        return None
    parent = commit.parents[0]
    return parent

def enum_commit(commit):
    while commit != None:
        print_commit(commit)
        commit = enum_next_commit(commit)

def show_commit(repo):
    enum_commit(repo.head.commit)        
