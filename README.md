## FOSSASIA 2016 : Deep Learning Workshop

*  http://2016.fossasia.org/


This repo will include the source to build a VM to be used for the Workshop participants.

The VM itself will include (subject to change) : 

* Jupyter (iPython's successor)
  * Running as a server available to the host machine's browser
* Data
  * MNIST training and test sets
  * Trained model from one of the 'big' ImageNet winners
* Tool chain (mostly Python-oriented)
  * Choice 1 : Tensorflow / Keras
  * Fallback : Theano / Lasagne / Keras (not Caffe)


### Working 

*  Create working Fedora 23 installation inside VM
*  Transform the VM into a VirtualBox appliance

*  Tested out Convnet.js for :
   *  Demonstration of gradient descent
   *  Demonstration of MNIST learning


### Still TODO 

*  Buy thumb-drives for actual workshop
*  Create rsync-able image :
   *  VirtualBox appliance image
   *  VirtualBox binaries for several likely platforms

*  Data directory to live inside image (heavy reliance on people being able to do VirtualBox)

*  Test workshop notebooks
   *  Tensorflow / Keras MNIST
   *  Tensorflow / Keras image synthesis
      +  Deep dream
      +  Style transfer
   *  Tensorflow "commercial application" : transfer learning

   

### Notes : Git-friendly iPython Notebooks

Using the code from : http://pascalbugnion.net/blog/ipython-notebooks-and-git.html (and
https://gist.github.com/pbugnion/ea2797393033b54674af ), 
you can enable this kind of feature just on one repository, 
rather than installing it globally, as follows...

Within the repository, run : 
```
# Set the permissions for execution :
chmod 754 ./bin/ipynb_optional_output_filter.py

git config filter.dropoutput_ipynb.smudge cat
git config filter.dropoutput_ipynb.clean ./bin/ipynb_optional_output_filter.py
```
this will add suitable entries to ``./.git/config``.

or, alternatively, create the entries manually by ensuring that your ``.git/config`` includes the lines :
```
[filter "dropoutput_ipynb"]
	smudge = cat
	clean = ./bin/ipynb_output_filter.py
```

Note also that this repo includes a ``<REPO>/.gitattributes`` file containing the following:
```
*.ipynb    filter=dropoutput_ipynb
```

Doing this causes git to run ``ipynb_optional_output_filter.py`` in the ``REPO/bin`` directory, 
which only uses ``import json`` to parse the notebook files (and so can be executed as a plain script).  

To disable the output-cleansing feature in a notebook (to disable the cleansing on a per-notebook basis), 
simply add to its metadata (Edit-Metadata) as a first-level entry (``true`` is the default): 

```
  "git" : { "suppress_outputs" : false },
```


### Useful resources

* [MathJax](http://nbviewer.ipython.org/github/olgabot/ipython/blob/master/examples/Notebook/Typesetting%20Math%20Using%20MathJax.ipynb)
* [Bokeh](http://bokeh.pydata.org/en/latest/docs/quickstart.html)

