
Tried pygit2 but it failed.

    # pip install pygit2
    # -- failed

But the documentation is good.
http://www.pygit2.org/objects.html


GitPython
===========

pip install gitpython

from git import Repo
repo = Repo('/path/project')

# List the headers
repo.heads

# Select a repo
repo.heads.master

# Get the corresponding commit
repo.heads.master.commit

# Commit Properties
commit.author
commit.authored_date
commit.message

- Note: authored_date = seconds since epoch (1970). 
- Convert with time.gmtime()

commit.parents
commit.tree

# reflog entries
branch = repo.heads.master

# get a specific commit
repo.commit('sha1')

for


# r.object('id')
# r.head('master') -> commit

head is a named reference to commit



