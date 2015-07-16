this extension by Thomas Kluyver checks in a stripped version of a notebook called
mynotebook.ipynb.clean every time mynotebok.ipynb is saved.   mynotebook.ipynb.clean
is the version that is kept under version control, so that diffs between edits
can be merged cleanly.  When mynotebook.ipynb is opened, a diff is performed with
mynotebook.ipynb.clean and modified input cells from the clean notebook are
moved/merged into mynotebook.ipynb

The alternative is to strip all output cells from mynotebook.ipynb using a gitcommit
hook, but that means that mynotebook.ipynb never has its output cells/plots/results
and has to be rerun and copied to be displayed.

See  http://permalink.gmane.org/gmane.comp.python.ipython.devel/15497

to use:

cd ~/repos

git clone https://github.com/phaustin/recombinecm.git

then add the following to

~/.ipython/profile_default/ipython_notebook_config.py

import site,os
site.addsitedir('{}/repos/recombinecm'.format(os.environ['HOME']))
import recombinecm

...

c.NotebookApp.contents_manager_class = 'recombinecm.RecombineContentsManager'


To test:

~/repos/recombinecm phil@rail% nosetests test_recombine.py
.....
----------------------------------------------------------------------
Ran 5 tests in 0.005s

OK

