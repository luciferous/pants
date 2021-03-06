=======================
About the documentation
=======================

Pants documentation is generated from `reStructuredText`_ sources by `Sphinx`_,
the tool Python itself is documented with. This site was modeled on
the `Python documentation`_.

.. _reStructuredText: http://docutils.sf.net/rst.html
.. _Sphinx: http://sphinx.pocoo.org/
.. _Python Documentation: http://docs.python.org

-------------------
Generating the site
-------------------

The following commands must be run from the pants repo root.

::

  # Sphinx must be installed locally to generate the site.
  # This is only required once per machine.
  easy_install -U Sphinx
  pip install sphinx_rtd_theme

  # Build pants, which triggers downloading egg dependencies
  # which are required when Sphinx inspects pants sources.
  cd /path/to/pants/repo
  rm pants.pex
  ./pants.bootstrap
  # Build the BUILD dictionary data.
  ./pants goal builddict # (or ./pants py src/python/pants goal builddict to try out local tweaks)

  # Doc generation commands must be run from the doc dir.
  cd src/python/pants/docs
  # Generate rst files.
  ./gen.py
  # Generate the site.
  make clean html

The site will be generated into ``_build/html``, which should not be checked
in. ``open _build/html/index.html`` to view your changes.

.. note:: If you make a change to a pydoc comment in the pants source code, you need to follow the
          complete set of steps above, starting by deleting ``pants.pex``, in order to see your
          change in the resulting HTML.

-------------------
Publishing the site
-------------------

Publishing the site simply involves making the contents of ``_build/html``
available on a web server.

.. TODO(travis): Update publishing section with how to publish.
