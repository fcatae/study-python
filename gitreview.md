
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


def get_commit_diff(commit):
    if(len(commit.parents) == 0):
        return None
    prev_commit = commit.parents[0]
    return commit.diff(prev_commit)


def get_commit_filenames(commit):
    diff = get_commit_diff(commit)
    if(diff is None):
        return
    for d in diff:
        if ( d.a_path != None ):
            yield d.a_path
        if ( d.a_path != None) and (d.a_path != d.b_path):
            yield d.b_path


def print_filenames(commit):
    for filename in get_commit_filenames(commit):
        print "   * " + filename


def enum_commit(commit, callback):
    while commit != None:
        callback(commit)

        next_commit = enum_next_commit(commit)


def show_commit(commit):
    print_commit(commit)
    print_filenames(commit)


def show(repo):
    enum_commit(repo.head.commit, show_commit)


# Traverse files

    for item in tree.traverse():
        print item.name

>>> for d in diffs:
...   print d.a_path
...   print d.b_path